VPS Infrastructure Environment

1. Overview

This document describes the production VPS environment managed for hosting websites, DNS resolution, and email services.

2. Server Information

- Hostname: "srv1"
- Provider: Contabo
- Operating System: Ubuntu 24.04
- Control Panel: HestiaCP
- Primary Role: Web hosting and email services

3. Core Services

Service| Purpose
HestiaCP| Web hosting and server administration
Nginx| HTTP/HTTPS traffic handling
Exim4| Outbound and inbound email transport
systemd-resolved| System DNS resolution
Let's Encrypt| TLS certificate issuance and renewal

4. DNS Resolution

System DNS resolution is managed by "systemd-resolved".

Configuration file:

"/etc/systemd/resolved.conf.d/99-custom-dns.conf"

Current configuration:

[Resolve]
DNS=8.8.8.8 9.9.9.9
FallbackDNS=1.1.1.1
Domains=~.

Apply configuration changes by restarting the resolver:

sudo systemctl restart systemd-resolved

Validate DNS resolution with:

resolvectl status
resolvectl query gmail.com

5. Email Infrastructure

Exim4 handles email transport.

Useful diagnostic commands:

sudo exim4 -bpc
sudo exim4 -bp
sudo tail -n 100 /var/log/exim4/mainlog

- "exim4 -bpc" reports the number of messages in the queue.
- "exim4 -bp" displays queued messages.
- "mainlog" records email delivery and routing events.

DNS resolution failures can affect mail routing, sender verification, and delivery times.

6. Web and TLS Infrastructure

Nginx handles web traffic and HTTPS connections for hosted domains.

TLS certificates and virtual host configurations are managed within the HestiaCP environment.

Certificate validation should verify the certificate served to clients, its subject alternative names, issuer, and validity period.

7. Operational Principles

- Validate configuration before restarting services.
- Collect logs and command output before making changes.
- Apply the smallest practical corrective change.
- Test affected services after each change.
- Monitor the system after recovery.
- Document confirmed facts separately from hypotheses.
- Never commit passwords, private keys, API tokens, or sensitive customer data to version control.

8. Related Documentation

- "Incident Reports" (../incidents/)
- "Incident Response Procedure" (incident-response.md)

9. Maintenance

Update this document whenever the server architecture, core services, DNS configuration, or operational procedures change.

Note: This document describes the known environment. Verify the live server configuration before relying on it for operational changes.
