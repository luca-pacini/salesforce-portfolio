# Deployment Flow

```mermaid
flowchart TD
    A[Local Salesforce DX project] -->|"develop"| B[Developer sandbox]
    B -->|"validate"| C[Sandbox test scan]
    C -->|"review"| D[Human redaction gate]
    D -->|"sanitise"| E[Public GitHub portfolio]
    D -->|"private delivery only"| F[Controlled Salesforce release path]
    F -->|"deferred"| G[Production release]

    style A fill:#D6EAF8,stroke:#2874A6,color:#000000
    style B fill:#D5F5E3,stroke:#1E8449,color:#000000
    style C fill:#D5F5E3,stroke:#1E8449,color:#000000
    style D fill:#FCF3CF,stroke:#9A7D0A,color:#000000
    style E fill:#E8DAEF,stroke:#6C3483,color:#000000
    style F fill:#FDEBD0,stroke:#A04000,color:#000000
    style G fill:#FADBD8,stroke:#922B21,color:#000000
```

## Diagram boundary

This diagram shows the public-safe delivery path.

The public repository is a portfolio artefact. It is not the production deployment source of truth.

Production release is deferred from this public package until a separate private review confirms source safety, test readiness, deployment controls and redaction boundaries.
