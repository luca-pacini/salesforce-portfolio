# Architecture Decisions

This document includes only Architecture Decision Records (ADRs) supported by the current project evidence.

## ADR 001: Build the scanner and dashboard before adding Gemini

### Context

The project goal is to create a Salesforce security observability capability. Artificial Intelligence (AI) summaries are useful only if the underlying security data model is accurate, sanitised and explainable.

Adding Gemini first would risk producing attractive summaries over unstable or incomplete data.

### Decision

Build the raw Salesforce scanner, persistence model and Lightning Web Component (LWC) dashboard first. Add Gemini only after the scan output, redaction model and dashboard review workflow are stable.

### Alternatives considered

- Add Gemini as the first visible feature.
- Use Gemini to query Salesforce directly.
- Keep the project as a static dashboard with no future Artificial Intelligence (AI) layer.

### Consequences

The first version is less visually dramatic but more defensible. The project can prove security data capture and review before adding advisory summaries.

### Security impact

Positive. Sensitive Salesforce data is collected and sanitised inside Salesforce before any future Artificial Intelligence (AI) use.

### Scalability impact

Positive. A stable normalised scan output can support future executive summaries, trend comparisons and source-org comparisons.

## ADR 002: Keep version 1 read-only

### Context

Security observability and security remediation have different risk profiles. Revoking tokens, removing permissions or changing configuration from a dashboard can create operational disruption if the detection logic is wrong.

### Decision

Version 1 is read-only and advisory. It records posture, metrics and findings but does not revoke OAuth tokens, remove Permission Sets, deactivate users or change org security settings.

### Alternatives considered

- Add one-click remediation.
- Automatically revoke stale OAuth tokens.
- Automatically remove high-risk access.

### Consequences

Manual remediation remains required. The trade-off is deliberate: lower automation speed, but lower security and change-management risk.

### Security impact

Positive. The dashboard cannot accidentally remove access or disrupt integrations.

### Scalability impact

Neutral to positive. The review workflow can mature before automation is added.

## ADR 003: Use a modular scanner service instead of a monolithic controller

### Context

The project needs to cover different Salesforce security domains: users, connected applications, OAuth tokens, sessions, login history, future Health Check, certificates, Named Credentials, Experience Cloud exposure and permissions.

Putting all logic into a dashboard controller would make the system harder to test, extend and review.

### Decision

Separate the architecture into a Lightning Web Component (LWC), Apex controller, scan service, Queueable Apex execution and individual scanner classes.

### Alternatives considered

- Put scan logic directly in the controller.
- Put all scanner logic into one large service class.
- Use only reports and list views.

### Consequences

The codebase has more classes, but each class has a clearer responsibility.

### Security impact

Positive. Security-sensitive retrieval and redaction logic can be isolated by scanner domain.

### Scalability impact

Positive. New scanners can be added without redesigning the dashboard controller.

## ADR 004: Persist normalised posture records instead of showing only live query results

### Context

A security dashboard that only queries live data is useful for a moment, but weak for auditability, trend review and future comparison.

The project needs a durable representation of scans, metrics, findings and assets.

### Decision

Persist normalised scan output in custom Salesforce records.

### Alternatives considered

- Show only live query results.
- Export raw query results to files.
- Use only external logging.

### Consequences

The project needs a custom data model and retention thinking. In return, findings become reviewable after scan execution.

### Security impact

Mixed. Persistence improves auditability but increases the need for redaction and Field Level Security (FLS) controls.

### Scalability impact

Positive. Persisted output supports dashboard refreshes, trend analysis, future exports and source-org grouping.

## ADR 005: Use dashboard drill-down panels instead of dead-end metric cards

### Context

Summary numbers are weak if the reviewer cannot understand what records sit behind the count.

The dashboard should help review risk, not just display statistics.

### Decision

Metric cards should support drill-down where safe detail exists. Detail should open inside the dashboard rather than relying on standard record pages as the main review workflow.

### Alternatives considered

- Keep only top-level metric cards.
- Link users to standard Salesforce record pages.
- Use wide data tables for every section.

### Consequences

The user interface takes more design work, but the review experience is more useful.

### Security impact

Positive if implemented carefully. Detail panels can control exactly which evidence is exposed.

### Scalability impact

Positive. Each metric can expose detail only when the underlying scanner supports it.

## ADR 006: Defer production-org scanning

### Context

The future architecture should support a second Salesforce source org, but production access increases risk and must be handled through secure, read-only integration controls.

### Decision

Build and stabilise local sandbox scanning first. Defer production source-org scanning until the dashboard, data model and Named Credential-based access pattern are stable.

### Alternatives considered

- Add production scanning immediately.
- Build only for the current sandbox.
- Use manual exports from production.

### Consequences

Cross-org comparison is not part of the current working version. The data shape still needs to account for source-org grouping.

### Security impact

Positive. Production access is not added before the security model is ready.

### Scalability impact

Positive. Source-org grouping is considered early, reducing future redesign risk.

## Future Architecture Decision Records (ADRs)

[NEEDS DETAIL: Architecture Decision Record requires a real design decision.]

Potential future Architecture Decision Records (ADRs) after implementation evidence exists:

- Health Check retrieval through Tooling API and Named Credential.
- Paid licence entitlement model using normalised child records.
- Gemini summary contract and sanitisation boundary.
- Scheduled scan cadence and retention policy.
