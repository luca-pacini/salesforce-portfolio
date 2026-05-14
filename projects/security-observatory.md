# Salesforce Security Posture Observatory

## Summary

Sandbox-first Salesforce security observability project designed to make platform risk easier to review across users, connected applications, OAuth exposure, active sessions and login activity.

The project prioritises read-only visibility before remediation. It does not revoke tokens, remove permissions or change security configuration automatically.

## Business Problem

Salesforce security posture is often spread across Setup screens, SOQL-accessible data, Tooling API areas and admin knowledge. That makes risk difficult to review consistently and weakens audit readiness.

## Architecture Signal

| Area | Evidence |
|---|---|
| User experience | Lightning Web Component (LWC) dashboard for posture review. |
| Processing | Apex controller and Queueable Apex scan execution. |
| Data model | Custom Salesforce records for scans, metrics, findings and assets. |
| Security boundary | Read-only version 1, no automatic remediation, no secrets, no raw tokens, no session identifiers. |
| Scalability | Scanner classes separated by concern, drill-down-ready data shape and future source-org grouping. |
| Governance | Sandbox-first delivery and public redaction before publication. |

## Technical Design Architect (TDA) Relevance

This project shows business risk framing, security-first architecture, modular Apex design, dashboard usability, future-state planning and deliberate deferral of unsafe automation.

## Public Artefact

The detailed redacted case study currently sits inside this portfolio repo:

[Open redacted project README](../salesforce-security-observatory/README.md)

## Status

Portfolio case study available. Standalone public project repo not yet visible in the connected GitHub account.
