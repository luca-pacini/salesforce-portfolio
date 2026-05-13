# Sanitised Salesforce Metadata Only

This folder is reserved for Salesforce metadata that has passed manual redaction review.

Do not publish private implementation files here until the human publishing gate has been completed.

Current status: `[DO NOT PUBLISH]` for live Apex, Lightning Web Component (LWC), object metadata and permission metadata.

Allowed future content:

- Sanitised Apex examples.
- Sanitised Lightning Web Component (LWC) examples.
- Sanitised metadata examples.
- Mocked test data only.

Excluded content:

- Credentials.
- Tokens.
- Secrets.
- Org identifiers.
- Internal URLs.
- Real usernames.
- Real email addresses.
- Exact field mappings.
- Proprietary rules.
- Production deployment scripts.
- Sensitive logs.
