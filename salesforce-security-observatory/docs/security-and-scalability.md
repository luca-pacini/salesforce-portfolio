# Security and Scalability

## Security model

The project uses a security-first, read-only model for version 1.

The dashboard is intended to make Salesforce posture visible without changing configuration, revoking access or performing automatic remediation. This reduces the risk of an observability project becoming an uncontrolled administration tool.

## Access model

Access to the dashboard should be limited to approved Salesforce administrators, architects and security reviewers.

The public repository does not include permission set metadata because the private implementation must be reviewed and sanitised before publication.

Minimum access principles:

- Grant access through Permission Sets.
- Avoid broad administrative access for normal dashboard use.
- Separate viewer access from any future asset-maintenance access.
- Respect Field Level Security (FLS) for user-facing records.
- Do not expose commercial or sensitive asset fields to users without permission.

## Permission Sets

Permission Sets are the preferred access mechanism.

Expected model:

| Permission Set | Purpose | Status |
|---|---|---|
| Security Observatory Viewer | Read dashboard metrics and findings. | [NEEDS DETAIL] Public metadata not included. |
| Security Observatory Runner | Run approved scans. | [NEEDS DETAIL] Public metadata not included. |
| Security Observatory Asset Maintainer | Maintain asset and licence classification fields where Field Level Security (FLS) allows it. | [NEEDS DETAIL] Public metadata not included. |

## Field Level Security (FLS)

Field Level Security (FLS) must be enforced for records returned to the user interface.

Commercial fields, licence fields and owner fields must be hidden or read-only where the running user lacks permission.

Dashboard edit patterns must not bypass Salesforce security. If the user cannot edit a field through normal Salesforce security, the dashboard must not edit it either.

## Create, Read, Update, Delete (CRUD) enforcement

Create, Read, Update, Delete (CRUD) checks are required before user-facing records are read, created or updated.

Version 1 is mainly read-only, but asset maintenance is a planned dashboard capability. Any update path must validate object-level and field-level access before Data Manipulation Language (DML).

## Data protection

The project must not expose:

- Access tokens.
- Session identifiers.
- Refresh tokens.
- Certificate private material.
- Certificate body content.
- Raw secrets.
- Exact internal URLs.
- Real usernames or email addresses in the public repository.
- Raw Internet Protocol (IP) address evidence unless explicitly approved and safely redacted.

Evidence should be summarised, counted, categorised or masked.

## Integration security

No external integration is active in the public version.

Future Tooling API scanner access must use Named Credentials. Hard-coded endpoints, usernames, passwords, session identifiers or bearer tokens are not acceptable.

Future Gemini integration must use sanitised summaries only. Gemini must not query Salesforce directly and must not receive raw secrets, tokens, session identifiers, customer data or uncontrolled personal data.

## Named Credentials

Named Credentials are required for future callouts.

Rules:

- No secrets in Apex.
- No session identifier reuse in public examples.
- Use least-privilege authentication.
- Keep production scanning deferred until sandbox scanner behaviour is stable.

## No hard-coded secrets

The repository intentionally excludes credentials, environment files and deployment scripts.

Any sample credential shown in documentation must be marked as `[DUMMY CREDENTIAL]` and must not be valid.

## Logging and monitoring

The private implementation uses a non-namespaced Nebula Logger wrapper for sanitised runtime telemetry.

Logging must not capture secrets, token values, session identifiers, raw certificate material or sensitive user data.

Recommended logging categories:

- Scan start and completion.
- Scanner-level success or controlled failure.
- Sanitised error context.
- Record counts.
- Duration where safe.
- Redaction failures.

## Auditability

The project persists scan output so findings can be reviewed after the scan completes.

Future audit improvements:

- Review status.
- Accepted risk marker.
- Manual reviewer notes.
- Scan history comparison.
- Future Artificial Intelligence (AI) request logs for Gemini summaries.

## Scalability model

The project uses a modular scanner model instead of one monolithic controller.

Each scanner owns a source area. The scan service orchestrates scanners and returns normalised output. This keeps future extension possible without making every new check a dashboard rewrite.

## Governor-limit considerations

The implementation must remain governor-limit aware:

- Avoid SOQL inside loops.
- Use maps for summarisation where aggregate queries are unreliable or unsupported.
- Keep Data Manipulation Language (DML) batched.
- Keep scanner output compact.
- Avoid returning unnecessary raw rows to the Lightning Web Component (LWC).
- Move long-running scan work away from synchronous user interaction.

## Asynchronous design

Queueable Apex is used for scan execution in the private implementation.

This keeps the dashboard interaction responsive and creates a natural place to expand into scheduled scans later.

## Metadata-driven configuration

The project direction is to move rules, thresholds and asset classification into configurable records or metadata where appropriate.

This matters because scanner logic should not become a hard-coded set of one-off business rules.

Current status: [PARTIAL IMPLEMENTATION]. Public repository does not include exact field definitions or rule mappings.

## Extension points

Planned extension areas:

- Health Check score and risk scanner.
- OAuth and connected app risk enrichment.
- Deactivated users with active OAuth tokens.
- Delegated administrator login-access visibility where Salesforce exposes it safely.
- Certificate expiry.
- Named Credential and External Credential inventory.
- Experience Cloud and public site exposure.
- High-risk Permission Set and assignment review.
- Salesforce product licence availability.
- Paid package licence availability.
- Controlled app functional-role entitlement mapping.
- Sanitised Gemini advisory summaries.

## Risks and mitigations

| Risk | Mitigation |
|---|---|
| Exposing sensitive evidence in the dashboard. | Redact, summarise or suppress sensitive values before display. |
| Turning observability into unsafe remediation. | Keep version 1 read-only and advisory. |
| Overloading the dashboard with dead-end metrics. | Add drill-down panels only where safe evidence exists. |
| Hard-coded scanner rules becoming difficult to maintain. | Move thresholds and classifications into records or metadata where appropriate. |
| Production org access increasing blast radius. | Defer production scanning until sandbox scanner model is stable and use read-only Named Credential-based access. |
| Artificial Intelligence (AI) summary leaking sensitive data. | Defer Gemini and send only sanitised summaries when implemented. |
