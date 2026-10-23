VPS Infrastructure Incidents

Technical documentation of infrastructure incidents, troubleshooting, remediation, and operational lessons learned from VPS environments.

Objectives

- Document production incidents and their impact.
- Record diagnostic evidence and corrective actions.
- Establish repeatable incident response procedures.
- Track service recovery and follow-up actions.
- Improve infrastructure reliability and operational security.

Environment

- Hosting provider: Contabo
- Operating system: Ubuntu 24.04
- Control panel: HestiaCP
- Web server: Nginx
- Mail transport: Exim4
- DNS resolver: systemd-resolved

See "Environment Documentation" (docs/environment.md) for additional details.

Incident Reports

Date| Incident| Status
2026-10-23| "DNS Resolution and Email Delivery Recovery" (incidents/2026-10-23-dns-email-recovery.md)| Operationally recovered; monitoring required

Documentation

- "Environment Overview" (docs/environment.md)
- "Incident Response Procedure" (docs/incident-response.md)
- "Incident Reports" (incidents/)

Incident Management Principles

1. Collect evidence before changing configurations.
2. Distinguish confirmed causes from hypotheses.
3. Apply controlled and minimal corrective changes.
4. Validate recovery using measurable results.
5. Monitor services after remediation.
6. Protect credentials and sensitive operational data.

Security

Sensitive information must be removed from logs and evidence before publication. Never commit passwords, private keys, access tokens, or customer data.

Disclaimer

This repository documents operational observations and remediation steps. Procedures must be validated against the actual server environment before execution.
