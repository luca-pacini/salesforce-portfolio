# Solution Design

## Business problem

Salesforce security posture can be difficult to review consistently when evidence is spread across Setup pages, SOQL-accessible records, Tooling API-accessible metadata and manual admin checks.

The project creates a read-only Salesforce observability layer so an admin or architect can review selected security signals from one dashboard without exposing secrets or triggering automatic remediation.

## Current state

Security review is fragmented across multiple areas:

- User access and status.
- Connected applications.
- OAuth token exposure.
- Active sessions.
- Login history.
- Future Health Check and metadata-based checks.
- Future Experience Cloud and public site exposure checks.
- Future paid licence and controlled application checks.

The current working implementation covers users, connected applications, OAuth tokens, active sessions and login history in sandbox.

Areas not yet completed are marked as future scanner scope rather than implied current delivery.

## Target state

The target state is a Salesforce-native dashboard that allows authorised users to:

- Run selected read-only scans.
- See current security posture metrics.
- Review findings with safe evidence.
- Drill into supported details without exposing sensitive raw values.
- Track security assets and controlled applications.
- Add future scanner areas without redesigning the full dashboard.
- Support future source-org grouping for a second read-only Salesforce org.

Version 1 does not remediate. It observes, records and presents risk.

## Users

Primary users:

- Salesforce administrator.
- Salesforce architect.
- Platform owner.
- Security reviewer with approved Salesforce access.

Non-goals:

- General end-user dashboard.
- Automated security enforcement tool.
- Production-grade Security Information and Event Management (SIEM) replacement.
- Gemini-first Artificial Intelligence (AI) dashboard.

## Core components

| Component | Purpose | Current status |
|---|---|---|
| Lightning Web Component (LWC) dashboard | Presents scan metrics, findings and drill-down detail. | Implemented in private sandbox project. |
| Apex controller | Provides dashboard data and scan actions to the user interface. | Implemented in private sandbox project. |
| Queueable Apex scan | Runs scan logic outside the immediate user interaction. | Implemented in private sandbox project. |
| Scan service | Orchestrates scanner classes and normalises results. | Implemented in private sandbox project. |
| Scanner classes | Retrieve and summarise security data by source area. | Partial implementation. |
| Custom Salesforce records | Persist scans, metrics, findings and assets. | Implemented in private sandbox project. |
| Nebula Logger wrapper | Records sanitised runtime telemetry. | Implemented in private sandbox project. |
| Tooling API scanner layer | Retrieves selected metadata and security objects. | [PARTIAL IMPLEMENTATION] Future scanner scope. |
| Gemini advisory service | Produces sanitised risk summaries. | Deferred. |

## Data flow

1. Authorised user opens the dashboard.
2. Dashboard requests the latest scan summary from Apex.
3. User triggers a selected scan.
4. Apex controller starts Queueable Apex.
5. Scan service runs scanner classes.
6. Scanner results are normalised into metrics, findings and asset-related records.
7. Sensitive values are redacted or summarised before storage or display.
8. Dashboard refreshes and presents current posture.
9. User reviews findings and supported drill-down detail.

## User experience

The dashboard is designed around security review rather than visual noise.

Top-level metrics provide a fast posture view. Where safe detail exists, the user should be able to click a metric or finding and open an in-dashboard detail panel. The design avoids dead-end summary cards and avoids sending the reviewer to raw Salesforce record pages as the primary workflow.

Finding detail should include:

- Category.
- Severity.
- Evidence summary.
- Recommendation.
- Source area.
- Related asset where available.
- Manual review action.

## Support model

Version 1 support model:

- Manual scan execution.
- Manual review of findings.
- Sanitised runtime logging through the private Nebula Logger wrapper.
- No automatic remediation.
- No automated revocation of tokens or permissions.

Future support model:

- Scheduled scans after manual scan behaviour is stable.
- Trend views between scans.
- Source-org grouping.
- Export support.
- Sanitised Gemini summary for executive reporting and remediation planning.

## Known constraints

- This is a sandbox-first project.
- Public repository source is redacted and not deployable as-is.
- Production scanning is deferred.
- Gemini is deferred.
- Health Check, certificate, Named Credential, External Credential, site and Experience Cloud scanner areas require additional implementation and safe Tooling API access.
- Real object definitions and field mappings are not exposed publicly.
- Security findings must avoid raw token, session, certificate, IP and user-identifying evidence unless explicitly approved and safely redacted.

## Implementation boundary

This design document describes the real architecture pattern and current private sandbox direction.

It does not publish live Salesforce metadata, credentials, org identifiers, usernames, emails, internal URLs, proprietary rules or exact implementation mappings.
