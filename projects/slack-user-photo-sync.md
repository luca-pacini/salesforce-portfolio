# Controlled Slack-to-Salesforce User Photo Synchronisation

## Summary

Salesforce-native integration pattern for synchronising approved Slack profile photos into Salesforce User profile photos with a secure callout boundary and redacted public implementation detail.

The project treats profile photos as an operational identity consistency problem, not cosmetic polish.

## Business Problem

Salesforce User photos were incomplete or inconsistent, making ownership and collaboration less recognisable across Salesforce user journeys. Manual maintenance did not scale well.

## Architecture Signal

| Area | Evidence |
|---|---|
| Processing | Scheduled Apex and Batch Apex for controlled processing. |
| Integration | Slack API access through Named Credential boundary. |
| Design split | Apex service layer separates orchestration, callout handling and update logic. |
| Security | No hard-coded secrets, mocked data, redacted matching logic and safe logging boundary. |
| Scalability | Batch processing, governor-limit awareness and supportable retry/status pattern. |
| Governance | Public portfolio version excludes tokens, org details, user mappings and production configuration. |

## Technical Design Architect (TDA) Relevance

This project shows how a small operational issue can still require proper architecture discipline: secure integration boundaries, least-privilege thinking, governor-limit awareness, redaction control and supportability.

## Public Artefact

Standalone public repository:

[Open project repo](https://github.com/luca-pacini/sf-slack-userpics-to-salesforce)

## Note on Repository Name

The current public repository name is `sf-slack-userpics-to-salesforce`. If the intended meaning is user profile pictures, this name is acceptable. If the intended meaning was “user picks”, the repository should be renamed before wider CV use.
