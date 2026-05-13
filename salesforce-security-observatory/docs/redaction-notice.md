# Redaction Notice

This repository is a redacted public portfolio artefact.

It is not a production deployment package and must not be treated as complete Salesforce implementation source.

## Redaction principles

The repository must show architecture thinking without exposing live implementation detail, credentials, internal system information or customer data.

The public version may describe patterns, boundaries and sanitised examples. It must not publish copyable private configuration or sensitive evidence.

## Excluded from the public repository

| Item | Status |
|---|---|
| Credentials | Excluded. |
| Tokens | Excluded. |
| Secrets | Excluded. |
| Salesforce org identifiers | Excluded. |
| Internal URLs | Excluded. |
| Real customer data | Excluded. |
| Exact field mappings | Excluded. |
| Production deployment scripts | Excluded. |
| Proprietary business rules | Excluded. |
| Real usernames | Excluded. |
| Real email addresses | Excluded. |
| Sensitive logs | Excluded. |
| Package licence keys | Excluded. |
| Private Slack channels | Excluded. |
| Private Jira project details | Excluded. |
| Private Google, Salesforce or third-party configuration | Excluded. |
| Live Named Credential details | Excluded. |
| Session identifiers | Excluded. |
| Access token values | Excluded. |
| Certificate private material | Excluded. |
| Certificate body content | Excluded. |

## Allowed public content

The following content is allowed if manually reviewed before publication:

- High-level architecture descriptions.
- Sanitised Mermaid diagrams.
- Mock data with obvious placeholder values.
- Redacted metadata examples.
- Non-sensitive class names where they do not expose internal implementation.
- General scanner categories.
- Public-safe implementation boundaries.
- Architecture Decision Records (ADRs) backed by real design decisions.

## Manual publishing checklist

Before publishing any additional file, answer YES to all checks:

- No credentials are present.
- No token values are present.
- No usernames or real email addresses are present.
- No org identifiers are present.
- No internal URLs are present.
- No customer data is present.
- No exact proprietary mappings are present.
- No production deployment scripts are present.
- No sensitive logs are present.
- No secrets are present in comments, examples or test data.
- No live Named Credential configuration is present.
- Any sample data is clearly mocked.
- Any unfinished feature is marked as `[PARTIAL IMPLEMENTATION]` or `[NEEDS DETAIL]`.

## Human publishing gate

Do not publish directly from private Salesforce source into this repository.

Every file must pass a separate manual redaction review first.

If a file cannot be made public safely, mark it `[DO NOT PUBLISH]` rather than weakening the boundary.
