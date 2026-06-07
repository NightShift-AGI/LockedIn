# lockedin

**lockedin** is a federated, trust-verified, AI-native professional network designed as a free and open-source alternative to LinkedIn.

The goal is to build a decentralized professional ecosystem where users fully own their data, control their feed algorithms, verify their credentials cryptographically, and grow their careers using private, open-source AI workflows.

## Core Architectural Pillars

- **Federated Identity (ActivityPub & DIDs)**: Rather than relying on a single corporate-owned database, lockedin uses a federated model. Industry hubs, university campuses, and companies can host their own servers (nodes) that communicate seamlessly using the ActivityPub protocol.
- **Cryptographic Trust Verification**: Combat spam, bots, and phishing with decentralized identity verification. Users verify employment, education, and credentials via domain challenges (e.g., DNS TXT or institutional email validation) rather than central authorities.
- **Zero Switching Friction**: Reclaiming data is simple. Users can import their existing professional profiles instantly via standard JSON Resume templates or direct LinkedIn data archive ingestion.
- **Transparent feed algorithms**: Feed algorithms are open-source and customizable. Users adjust direct sliders to prioritize chronological posts, skill-relevant listings, or industry updates.

## Current Stage

Zero stage: idea validation, product planning, architecture planning, team alignment, and MVP definition (aligned with decentralized and federated principles).

## Core Documents

1. [PRD](./PRD.md)
2. [Development Plan](./DEVELOPMENT_PLAN.md)
3. [Architecture](./ARCHITECTURE.md)
4. [Roadmap](./ROADMAP.md)
5. [Intern Execution Plan](./INTERN_EXECUTION_PLAN.md)

## Suggested MVP Goal

Build a working, federation-ready MVP where users can:

- Create a professional profile and verify it using email domain DNS challenges
- Import career history via LinkedIn data archive or JSON Resume
- Post updates and follow users (local and federated schemas)
- Use custom feed algorithms via simple parameter controls (sliders)
- Use abstracted local/open-source AI to improve profile content and post suggestions
- Run and self-host a node locally as an open-source project

