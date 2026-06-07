# lockedin Roadmap

## Phase 0: Idea and Planning

Timeline: Week 0 to Week 1

Goals:

- Finalize product vision
- Finalize MVP scope
- Create docs
- Set up GitHub repo
- Assign intern roles
- Create project board

Deliverables:

- README
- PRD
- Development plan
- Architecture doc
- Roadmap
- Contribution guide

## Phase 1: MVP Foundation & Cryptography

Timeline: Week 1 to Week 3

Goals:
- Set up core Next.js, Postgres database (Prisma), and Tailwind UI stack
- Build local authentication and session validation
- Generate and store user-profile cryptographic RSA public/private keypairs

Deliverables:
- Working local server with auth and database schema
- Secure encrypted private key storage utility
- Basic routing framework

## Phase 2: Ingestion & Onboarding Portability

Timeline: Week 3 to Week 5

Goals:
- Design Profile database schema (supporting local and remote configurations)
- Implement JSON Resume parser and LinkedIn zip archive ingestion services
- Integrate AI-driven auto-extraction for skills and experience mapping

Deliverables:
- Resume/Archive drag-and-drop file uploader UI
- Profile data hydration from uploaded resume archives
- Public profile page rendering parsed history

## Phase 3: Feed & Curation Sliders

Timeline: Week 5 to Week 7

Goals:
- Build posting API (local posts tagged with global URI identifiers)
- Create User Feed interface with customizable ranking sliders
- Implement backend dynamic weighted scoring engine based on feed preferences

Deliverables:
- Post creation card with simple editor
- Dynamic Feed UI displaying posts curated by slider parameter weights
- User feed preference settings storage

## Phase 4: Trust Verification & Federation Base

Timeline: Week 7 to Week 9

Goals:
- Build DNS TXT record crawler to verify company/school domain associations
- Set up challenge-response SMTP verification codes for institutional domains
- Create public Webfinger and ActivityPub Actor route templates

Deliverables:
- Domain verification wizard in profile settings
- Cryptographic verification badge indicator on profiles
- Webfinger resolution endpoints (`/.well-known/webfinger`) and public Actor JSON payloads

## Phase 5: Niche Beta Launch (OS Developers)

Timeline: Week 9 to Week 12

Goals:
- Restrict launch target to open-source developers, university tech hubs, and early startup teams
- Implement GitHub/GitLab verification and repository contribution stats display
- Create comprehensive documentation on self-hosting a local `lockedin` node via Docker Compose
- Acquire first 100 verified professional profiles on the seed node

Deliverables:
- Public beta node deployment
- Comprehensive self-hosting and federation configuration guides
- Developer dashboard with GitHub stats integration
- Community feedback forum

## Phase 6: Post-MVP (Federation & Sustainability)

Potential features:
- **Full Peer Synchronization**: Enable live syncing of posts, follows, and interactions across remote ActivityPub instances
- **Decentralized Moderation**: Shared domain-blocking records, report queues, and local moderator dashboards
- **W3C DIDs Integration**: Cross-instance login authentication using W3C Decentralized Identifiers
- **Enterprise Recruiter ATS APIs**: Paid access endpoints for syncing verified candidate profiles to corporate ATS pipelines (monetization/sustainability model)
- Collaborative workspaces and team pages
- End-to-end encrypted direct messaging

