# Salesforce Architecture Portfolio

Public redacted Salesforce architecture portfolio focused on Technical Design Architect (TDA) evidence: business context, solution design, security, scalability, governance and delivery trade-offs.

This is the portfolio front door. Each project is intentionally sanitised and is designed for recruiters, Salesforce architects and technical hiring managers.

## Portfolio Projects

| Project | Outcome | Technologies | Public artefact |
|---|---|---|---|
| Salesforce Security Posture Observatory | Sandbox-first, read-only Salesforce security observability dashboard for reviewing users, connected applications, OAuth exposure, sessions and login activity. | Lightning Web Components (LWC), Apex, Queueable Apex, SOQL, custom Salesforce records, Salesforce DX, GitHub | [Project summary](projects/security-observatory.md) |
| Controlled Slack-to-Salesforce User Photo Synchronisation | Salesforce-native pattern for synchronising approved Slack profile photos into Salesforce User profile photos with secure callout handling and mocked public data. | Apex, Scheduled Apex, Batch Apex, Named Credentials, mocked HTTP callouts, GitHub | [Project summary](projects/slack-user-photo-sync.md) |

## Reviewer Route

Start here:

1. Read the project summaries in `/projects`.
2. Open the high-level portfolio diagram in `/diagrams`.
3. Follow a standalone project repository where one exists.
4. Review the implementation boundary before reading any code or diagrams.

## Current Repository Map

```text
salesforce-portfolio/
├── README.md
├── projects/
│   ├── security-observatory.md
│   └── slack-user-photo-sync.md
└── diagrams/
    └── portfolio-overview.md
```

## Public Repositories

| Repository | Purpose | Status |
|---|---|---|
| `salesforce-portfolio` | Cohesive public index and project narrative. | Active |
| `sf-slack-userpics-to-salesforce` | Standalone redacted project repo for Slack-to-Salesforce profile photo synchronisation. | Active |
| `sf-security-observatory` | Planned standalone redacted project repo for Salesforce Security Posture Observatory. | To be created |

## Publishing Standard

Every public artefact must be redacted before publication.

Do not publish:

- Credentials, tokens or secrets.
- Salesforce org identifiers.
- Usernames or email addresses.
- Internal URLs.
- Exact field mappings.
- Customer data.
- Proprietary business rules.
- Live Named Credential configuration.
- Deployment scripts containing internal details.
- Sensitive logs or raw evidence.

## Portfolio Positioning

This portfolio is designed to show Salesforce architecture judgement, not to provide copyable production implementations.

The focus is:

- Business problem framing.
- Secure and scalable Salesforce design.
- Deliberate trade-offs.
- Governed delivery.
- Redaction discipline.
- Interview-defensible architecture evidence.
