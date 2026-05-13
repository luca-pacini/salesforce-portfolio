# High-Level Architecture

```mermaid
flowchart TD
    A[Authorised Salesforce reviewer] -->|"opens"| B[Security observability dashboard]
    B -->|"requests scan"| C[Apex controller]
    C -->|"starts"| D[Queueable scan execution]
    D -->|"orchestrates"| E[Security scan service]
    E -->|"runs"| F[User scanner]
    E -->|"runs"| G[Connected app scanner]
    E -->|"runs"| H[OAuth token scanner]
    E -->|"runs"| I[Session scanner]
    E -->|"runs"| J[Login history scanner]
    E -->|"normalises"| K[Sanitised scan output]
    K -->|"persists"| L[Security posture records]
    L -->|"returns"| B
    B -->|"shows"| M[Metrics findings and drill down]

    N[Future scanner scope] -->|"deferred"| E
    O[Future Gemini advisory summary] -->|"deferred until sanitised"| K

    style A fill:#FDEBD0,stroke:#A04000,color:#000000
    style B fill:#D6EAF8,stroke:#2874A6,color:#000000
    style C fill:#D5F5E3,stroke:#1E8449,color:#000000
    style D fill:#D5F5E3,stroke:#1E8449,color:#000000
    style E fill:#D5F5E3,stroke:#1E8449,color:#000000
    style F fill:#E8DAEF,stroke:#6C3483,color:#000000
    style G fill:#E8DAEF,stroke:#6C3483,color:#000000
    style H fill:#E8DAEF,stroke:#6C3483,color:#000000
    style I fill:#E8DAEF,stroke:#6C3483,color:#000000
    style J fill:#E8DAEF,stroke:#6C3483,color:#000000
    style K fill:#FCF3CF,stroke:#9A7D0A,color:#000000
    style L fill:#FCF3CF,stroke:#9A7D0A,color:#000000
    style M fill:#D6EAF8,stroke:#2874A6,color:#000000
    style N fill:#FADBD8,stroke:#922B21,color:#000000
    style O fill:#FADBD8,stroke:#922B21,color:#000000
```

## Diagram boundary

This diagram is intentionally high-level.

It does not include org identifiers, usernames, internal URLs, credentials, exact Salesforce object mappings, exact scanner queries or proprietary risk rules.
