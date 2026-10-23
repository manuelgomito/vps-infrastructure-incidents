Incident Response Procedure

1. Purpose

Define a consistent procedure for diagnosing, mitigating, validating, and documenting incidents affecting VPS infrastructure.

2. Scope

This procedure covers:

- DNS resolution failures
- Email delivery failures and delays
- Web service outages
- HTTPS and TLS certificate errors
- Resource exhaustion and service failures

3. Incident Response Workflow

Step 1 — Identify the Symptoms

Record:

- Incident start time and timezone
- Affected services and domains
- Error messages observed
- Scope and impact on users
- Recent configuration changes

Step 2 — Collect Evidence

Check service status and recent logs before making changes.

uptime
df -h
free -h
systemctl --failed

For email incidents:

sudo exim4 -bpc
sudo exim4 -bp
sudo tail -n 100 /var/log/exim4/mainlog

For DNS incidents:

resolvectl status
resolvectl statistics
resolvectl query gmail.com

For web service incidents:

sudo systemctl status nginx --no-pager
sudo nginx -t

Step 3 — Determine the Likely Cause

Correlate logs, service status, DNS results, and recent changes.

Distinguish between:

- Confirmed root cause
- Probable cause
- Symptoms and contributing factors

Do not report a hypothesis as a confirmed root cause.

Step 4 — Apply a Controlled Mitigation

- Back up the configuration file before editing it.
- Make the smallest change likely to address the issue.
- Validate configuration syntax where supported.
- Restart or reload only the services required.
- Record the exact commands and changes applied.

Step 5 — Validate Recovery

Confirm that the affected service works from the relevant client or external network.

For email incidents, verify sending, receiving, delivery delays, Exim4 logs, and queue status.

For DNS incidents, repeat queries and compare response times and failures.

For web incidents, verify HTTP/HTTPS responses and inspect the certificate presented to clients when relevant.

Step 6 — Monitor

Continue monitoring after recovery to determine whether the problem returns.

Compare new errors and timeouts with previously collected evidence. Remember that cumulative counters may include events from before the mitigation.

Step 7 — Document the Incident

Create a Markdown report in "incidents/" using this naming convention:

"YYYY-MM-DD-short-incident-description.md"

Each report should include:

- Summary and impact
- Symptoms and evidence
- Diagnostic steps
- Changes applied
- Validation results
- Current status
- Follow-up actions
- Root cause and confidence level

4. Security and Data Handling

- Never commit passwords, private keys, access tokens, or unredacted customer data.
- Sanitize logs before publishing them.
- Do not expose message contents or private email addresses unnecessarily.
- Restrict operational changes to authorized administrators.

5. Closure Criteria

An incident may be considered recovered when:

- The affected service passes relevant functional tests.
- Logs no longer show the original failure pattern, or remaining errors are understood.
- Monitoring shows no immediate recurrence.
- Evidence and corrective actions are documented.

Recovery does not automatically mean the root cause has been conclusively established.

6. Related Documentation

- "Environment Overview" (environment.md)
- "Incident Reports" (../incidents/)
