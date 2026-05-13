# Salesforce Security Posture Observatory — Redacted Portfolio Version

## TL;DR / CV Portfolio Summary

Designed a sandbox-first Salesforce security observability dashboard to make security posture visible across users, connected applications, OAuth token exposure, active sessions and login activity.

Implemented a read-only architecture using Lightning Web Components (LWC), Apex, Queueable Apex, SOQL and custom Salesforce records to separate user interaction, scan orchestration and persisted security findings.

Applied a security-first boundary: no automatic remediation, no exposed tokens, no session identifiers, no raw sensitive evidence and no hard-coded secrets.

The current working version proves the scan-and-review pattern. Future scanner areas are deliberately deferred until the base model, dashboard and redaction controls are stable.

## Executive Summary

Salesforce security posture is often spread across Setup screens, audit tables and specialist admin knowledge. That makes it difficult to review risk consistently, explain exposure to non-specialist stakeholders and prove that the platform is being governed rather than inspected reactively.

This project creates a Salesforce-native observability layer for security posture. The first working version runs controlled read-only scans in a sandbox, normalises selected security signals and presents metrics and findings in a Lightning Web Component (LWC) dashboard.

The current implementation focuses on users, connected applications, OAuth token exposure, active sessions and login history. Planned scanner areas include Health Check, certificate expiry, Named Credentials, External Credentials, public site exposure, Experience Cloud exposure, high-risk permission assignments and paid licence availability.

## Implementation Boundary

This repository is a redacted public portfolio version.

| Marker | Meaning |
|---|---|
| [REDACTED] | Sensitive project detail removed from the public repository. |
| [MOCKED DATA] | Example data created only for public demonstration. |
| [ABSTRACTED LOGIC] | Implementation pattern described without exposing copyable internal logic. |
| [DUMMY CREDENTIAL] | Placeholder only. No working credential exists in this repository. |
| [SANITISED EXAMPLE] | Safe example based on the real project pattern. |
| [PARTIAL IMPLEMENTATION] | Area exists as an approved direction but is not yet complete in the public artefact. |
| [NEEDS DETAIL] | Claim requires stronger project evidence before publication. |

What is real:

- Sandbox-first Salesforce Security Observatory concept.
- Lightning Web Component (LWC) dashboard pattern.
- Apex controller and scan service pattern.
- Queueable scan execution pattern.
- Scanner coverage for users, connected applications, OAuth tokens, active sessions and login history.
- Custom Salesforce records used to persist scan outputs, metrics, findings and security asset information.
- Read-only version 1 boundary.
- Design requirement for dashboard drill-down rather than dead-end summary cards.
- Design requirement for future source-org grouping.
- Nebula Logger usage through a non-namespaced wrapper in the private implementation.

What is mocked:

- Public sample data under `mock-data/sample-data.json`.
- User names, record references, org references and evidence values.

What is abstracted:

- Exact scanner queries.
- Exact custom object field definitions.
- Exact security finding rules.
- Exact Lightning Web Component (LWC) layout code.
- Internal naming conventions.

What is redacted:

- Salesforce org identifiers.
- Usernames and email addresses.
- Internal URLs.
- Real session, token or login evidence.
- Exact object mappings.
- Proprietary business rules.
- Deployment scripts.
- Live Named Credential configuration.

What is intentionally excluded:

- Production scanning.
- Automatic remediation.
- Token revocation.
- Permission removal.
- Gemini integration.
- Real Apex source until a dedicated sanitisation pass has been completed.

## Business Context

The business problem is security visibility rather than dashboard cosmetics.

An admin or architect needs a quick way to see where Salesforce security posture needs attention: risky users, connected applications, OAuth exposure, sessions, login issues, public exposure and licence-sensitive assets.

The current state is fragmented. Relevant data exists across Setup, SOQL-accessible objects, Tooling API-accessible objects and admin review processes. Without a normalised view, review quality depends too heavily on manual effort and individual memory.

The target state is a controlled Salesforce dashboard that gives a fast posture view, supports drill-down into underlying evidence where safe and creates a foundation for later executive summaries, trend analysis and remediation planning.

## Solution Overview

The solution uses a Salesforce-native dashboard backed by Apex scanners.

An authorised user runs a scan from the Lightning Web Component (LWC). The Apex controller starts a queueable scan. The scan service runs selected scanner classes, normalises the result and persists safe metrics and findings. The dashboard then displays the latest scan output with drill-down for supported areas.

Version 1 is deliberately read-only. It highlights risk and evidence but does not revoke tokens, change permissions, deactivate users or alter org configuration.

This keeps the project defensible: first make posture visible, then add advisory intelligence and workflow actions only after the data model and review process are stable.

## Architecture Summary

### Salesforce components

- Lightning Web Component (LWC) dashboard.
- Apex controller.
- Queueable Apex scan execution.
- Security scan service.
- Individual scanner classes.
- Custom Salesforce records for scans, metrics, findings and assets.
- Nebula Logger wrapper in the private implementation for sanitised runtime telemetry.

### Integration pattern

No external integration is active in the public version.

Future Tooling API access is expected for Salesforce metadata and security objects that are not available through normal SOQL. That access must use Named Credentials and must not expose session identifiers or hard-coded secrets.

### Configuration versus code split

Code owns scan orchestration, read-only retrieval, normalisation and dashboard response shaping.

Configuration and commercial/security classification are intended to move into Salesforce records and metadata where practical, so scanner logic does not become a hard-coded rules graveyard.

### Data flow

1. Authorised user opens the dashboard.
2. User runs a selected scan.
3. Apex controller starts a queueable scan.
4. Scan service executes scanner classes.
5. Scanner output is normalised into safe metrics and findings.
6. Dashboard reads the latest scan output.
7. User reviews metrics, findings and supported drill-down detail.

### Modularity

Each scanner is isolated by concern. This allows new scanner areas to be added without turning the dashboard controller into a security landfill.

### Extension points

- Health Check scanner.
- Certificate scanner.
- Named Credential scanner.
- External Credential scanner.
- Experience Cloud scanner.
- Public site exposure scanner.
- Permission risk scanner.
- Paid licence and controlled application scanner.
- Future Gemini summary service using sanitised data only.
- Future production source-org grouping through read-only Named Credential-based access.

## Security and Scalability Summary

### Security controls

- Sandbox-first delivery.
- Read-only version 1.
- No automatic remediation.
- No token revocation in version 1.
- No permission removal in version 1.
- No hard-coded secrets.
- No exposed access tokens, session identifiers, certificate bodies or raw sensitive values.
- Dashboard evidence is summarised or redacted where required.
- Field Level Security (FLS) and Create, Read, Update, Delete (CRUD) checks are required where user-facing records are read or edited.
- Least-privilege permission model is required for dashboard access.
- Named Credentials are required for future callouts.
- Gemini is deferred and must only receive sanitised summaries.

### Scalability controls

- Queueable Apex is used for scan execution.
- Scanner classes are separated by source area.
- Aggregation is performed in Apex where Salesforce object behaviour makes aggregate SOQL unreliable.
- Dashboard response shape supports drill-down and future export.
- Source-org grouping is part of the design so the model can later support a second read-only org.
- Licence and asset classification is intended to use normalised child records rather than multi-select picklists.

## Governance and Delivery

The project is being built in sandbox first.

The public repository is not the deployment source of truth. It is a redacted portfolio artefact showing the problem, architecture, boundary and delivery thinking.

Private delivery uses Salesforce DX project structure locally. Production deployment is intentionally out of scope for the public package until the scanner model, dashboard and redaction approach are stable.

Any publishable Salesforce metadata must go through a separate human review before being copied into this repository.

## Impact

Measured production impact is [NEEDS DETAIL].

Observed sandbox impact:

- Created a working scan-and-dashboard pattern for Salesforce security posture.
- Consolidated selected security signals into a single review surface.
- Established a safer first principle: visibility and review before remediation.
- Created a structure that can later support executive summaries, trend analysis, source-org comparison and controlled manual review actions.

## What I Would Improve Next

Future evolution would include deeper scanner coverage, stronger in-dashboard drill-down panels, licence availability checks, controlled app entitlement mapping, Health Check retrieval through a Named Credential, and additional automated tests around scanner normalisation and dashboard response shaping.

Gemini should only be added after the Salesforce data model is stable and after sanitised summary boundaries have been tested.

## Recruiter Summary

This project shows architecture-led Salesforce delivery rather than isolated configuration work.

It starts from a real governance problem: Salesforce security posture is hard to review consistently when the evidence is spread across multiple Setup screens and objects. The solution creates a read-only observability layer that helps an admin or architect review risk without exposing sensitive data or taking unsafe automated action.

The project is relevant to Technical Design Architect (TDA) capability because it connects business risk, security boundaries, data modelling, Apex service design, Lightning Web Component (LWC) user experience, governance and future integration planning.

## Technical Reviewer Summary

The architecture separates the user interface, controller, queueable scan execution, scanner services and persisted posture records.

The design favours read-only visibility before remediation. That is the key trade-off: slower operational automation, but lower security and change-management risk.

The model is built to expand by adding scanner classes and controlled dashboard drill-down areas rather than by growing a monolithic controller. Future production-org comparison and Gemini advisory summaries are explicitly deferred to avoid putting Artificial Intelligence (AI) on top of unstable or unsafe data.
