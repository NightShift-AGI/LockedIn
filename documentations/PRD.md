# lockedin PRD

## 1. Product Name

lockedin

## 2. Vision

Create an AI-native, free, open-source professional networking platform that gives users ownership, transparency, and intelligent career growth tools.

## 3. Problem

LinkedIn is powerful but has major gaps:

- Algorithmic opacity
- Spam and low-quality outreach
- Limited user control
- Paywalled visibility and features
- Weak open-source ecosystem
- Limited AI-native workflows
- Poor experience for builders, students, open-source contributors, and early-career professionals

## 4. Target Users

### Primary Users

- Students
- Developers
- AI engineers
- Founders
- Designers
- Open-source contributors
- Recruiters
- Startup teams
- Interns and early-career professionals

### Early Adopters

- Open-source communities
- AI builders
- Indie hackers
- university communities
- internship/job seekers

## 5. Core Value Proposition

lockedin helps professionals build their public career identity, discover opportunities, and connect meaningfully using AI-native tools in an open-source ecosystem.

## 6. MVP Features

### 6.1 Authentication

- Local Email/password signup and login
- Local session validation and security
- Cryptographic key generation per user profile (used for signing federated activities)

### 6.2 Profile & Portability

- Name, Headline, Bio, Skills, Experience, Education, Projects, and Links
- GitHub/open-source contribution integration
- **Frictionless Onboarding**: Direct parser/importer for JSON Resume files and LinkedIn data archive exports (e.g., parsing profile details, experiences, and education automatically)
- AI-generated profile suggestions based on imported resume data

### 6.3 Cryptographic Trust & Verification

- **Domain-Based Verification**: DNS TXT or institutional email validation (e.g., verification of employment at `company.com` or enrollment at `university.edu` via challenge-response mail matching the domain)
- Cryptographic verification badges displayed on public profiles (indicating verified emails/domains)

### 6.4 Feed & User-Controlled Algorithms

- Create text and link posts
- Like and comment on posts
- Follow local and remote users (data schema supports federated paths)
- **Transparent Feed Controls**: Feed configuration sliders in UI allowing users to set weights (e.g., Recency % vs. Verified Professional % vs. Specific Skill Matching %)
- Chronological raw fallback feed option

### 6.5 AI Assistant & Parsing

- Auto-extract and map skills from imported LinkedIn archives
- Rewrite profile bio and improve headline
- Generate post ideas and refine draft tone
- System-wide prompt logs with safety/injection filters

### 6.6 Federation Readiness (MVP Foundation)

- ActivityPub actor database schema (distinguishing local users from federated actor links)
- Structured API endpoints for ActivityPub Actor, Inbox, and Outbox (MVP focuses on schema readiness, local interactions, and federated modeling)
- Webfinger resolution schema draft

### 6.7 Opportunities & Niche Target

- Focus on open-source projects looking for contributors, early tech startups, and academic lab research positions
- Collaboration requests and job posts containing skill tag requirements
- Developer-specific trust metrics (e.g., verifying active repository contributions)

### 6.8 Open Source & Self-Hosting

- Public GitHub repository with clean issue templates and contribution guidelines
- Comprehensive local self-hosted docker deployment instructions for individual servers/nodes

## 7. Non-MVP Features (Post-MVP Milestones)

- **Full Peer Syncing & ActivityPub Subscriptions**: Live background synchronization of feeds/follows between separate self-hosted nodes
- **Decentralized Content Moderation at Scale**: Shared instance-level blocklists, distributed user reporting queues, and administrator moderation panel
- **W3C Decentralized Identifiers (DIDs)**: Advanced DID registry integration for passwordless cross-instance authentication
- **Enterprise ATS Integration APIs**: Premium paid APIs for corporate Applicant Tracking Systems (monetization/sustainability model)
- Mobile applications (React Native / Flutter)
- Company and team page workspaces

## 8. Success Metrics

### Product Metrics

- Weekly active users across instances
- Profiles completed (via LinkedIn import vs. manual)
- DNS/Email domains successfully verified (measure of trust density)
- User adjustments to feed sliders (active algorithm customization)
- Connections/follows established between nodes
- Opportunity applications/collaboration requests completed

### Open Source Metrics

- GitHub stars and forks
- Number of independent self-hosted instances running
- Contributors and pull requests merged
- Community discussions around algorithm transparency

## 9. User Stories

### Profile & Portability

- **Onboarding**: As a new user, I want to upload my LinkedIn data archive or JSON Resume so that I do not have to manually retype my entire career history.
- **Verification**: As a recruiter or collaborator, I want to see a cryptographic verification badge on a user's profile indicating they verified ownership of their work email (e.g., `engineer@google.com`) so that I can trust their career claims.

### Feed & Algorithm

- **Custom Feeds**: As a user, I want to adjust sliders in my feed (e.g., turn down thought leadership and increase skill matches) so that I have absolute, transparent control over what I see.
- **Posting**: As a user, I want to post my open-source project updates so that my followers across my local instance and peer nodes can see it.

### Discovery & Opportunities

- **Niche Search**: As an open-source maintainer, I want to filter professionals by verified domain and specific skill tags so that I can recruit credible collaborators for my project.

## 10. MVP Release Criteria

The MVP is ready when:

- Users can sign up, log in, and generate cryptographic signing keys
- Users can import career data from a JSON Resume or LinkedIn archive file
- Domain-based email verification (challenge-response) successfully assigns verification badges
- Users can customize feed sorting via ranking weight sliders in the interface
- Users can post updates, follow local accounts, and interact with the feed
- The database schema is fully ActivityPub-compatible (local vs. remote actors)
- Developers can launch and configure a local self-hosted instance using Docker compose
- Unit tests cover the resume parser, feed weighting engines, and verification email routers

