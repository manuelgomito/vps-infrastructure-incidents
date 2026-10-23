DNS Resolution and Email Delivery Recovery

Date: October 23, 2026
Affected services: systemd-resolved and Exim4
Status: Operationally recovered; monitoring required.

Symptoms

External email sending and receiving were delayed by several minutes.

Exim4 logs included:

- "host lookup did not complete"
- "retry time not reached"
- "sender verify defer"

DNS queries experienced intermittent timeouts and excessive response times.

Configuration Change

File: "/etc/systemd/resolved.conf.d/99-custom-dns.conf"

Configuration applied:

[Resolve]
DNS=8.8.8.8 9.9.9.9
FallbackDNS=1.1.1.1
Domains=~.

The resolver service was restarted:

sudo systemctl restart systemd-resolved

Validation

Twenty consecutive DNS MX queries returned valid responses, with query times between 0 and 8 ms.

The Exim4 queue was empty at the time of inspection:

sudo exim4 -bpc

Observed output: "0".

External email sending and receiving subsequently returned to normal.

Outcome

Email delivery was operationally recovered following the DNS configuration change. The original network-level cause has not been conclusively established.

Follow-up

Monitor DNS timeouts and email delivery. Compare resolver statistics over time rather than relying solely on cumulative timeout counts.
