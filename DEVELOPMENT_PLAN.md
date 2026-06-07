# lockedin Development Plan

## Stage 0: Foundation

Goal: Set up the team, repository, planning documents, and engineering workflow.

### Tasks

- Create GitHub organization/repository
- Add README
- Add PRD, architecture, roadmap, and contribution docs
- Create issue templates
- Create project board
- Define coding standards
- Define branching strategy
- Define MVP scope
- Assign intern tasks

## Stage 1: Technical Setup

### Recommended Stack

Frontend:

- Next.js
- TypeScript
- Tailwind CSS
- shadcn/ui

Backend:

- Next.js API routes or NestJS
- PostgreSQL
- Prisma ORM
- Redis later for caching/jobs

AI:

- OpenAI-compatible API abstraction
- Prompt templates
- AI usage logging
- Safety filters

Infra:

- Docker
- GitHub Actions
- Vercel for frontend
- Supabase/Neon for PostgreSQL
- S3-compatible storage later

## Stage 2: MVP Build

### Sprint 1: Auth, Cryptographic Keys, and Schema
- Auth pages (Signup, Login, Logout)
- Prisma DB Schema setup (supporting local vs. remote profiles, Instance nodes, and verification states)
- Session handling and security filters
- **Cryptographic Key Utility**: Generate unique RSA-256 keypairs on signup (store public key, encrypt and save private key for ActivityPub HTTP signatures)

### Sprint 2: Profile & Ingestion Portability
- Profile schema mapping (experiences, education, skills)
- Profile create/edit forms
- **Resume Ingestion Engine**: Service to upload and parse JSON Resume files or LinkedIn zip archives (mapping csv/json to Profile models)
- Public profile page rendering imported career history

### Sprint 3: Feed & Curation Sliders
- Post schemas (with `local` boolean flag and `apId` ActivityPub URI hooks)
- Create post UI & API
- **Transparent Feed Sliders UI**: Feed dashboard sliders allowing users to weigh Recency vs. Verified Domains vs. Skills
- **Weighted Feed API**: Dynamic PostgreSQL query sorting using slider weights

### Sprint 4: AI & Auto-Tagging Assistant
- AI resume mapping: Auto-extract skills from imported LinkedIn archives using abstracted AI prompts
- AI rewrite bio & improve headline
- AI post tone improvement & project description summaries
- Safety logs and system prompting protections

### Sprint 5: Trust Verification & ActivityPub Foundation
- **Domain Verification Engine**: Email verification codes and DNS TXT record challenge checking
- Verification badge UI elements
- **ActivityPub Actor Endpoints**: Build basic Webfinger endpoint (`/.well-known/webfinger`) and Actor profile JSON payload (`/users/[username]`)
- User search, post search, and verified domain filters

### Sprint 6: Polish, Self-Hosting, & Niche Launch
- UI polish (premium dashboard, glassmorphism, responsive sidebar layout)
- **Local Self-Hosting Config**: Setup Docker Compose templates for easy self-hosting of independent nodes
- Seed mock data (populating local DB with mock peer federated users and posts)
- Production-ready build testing and public GitHub launch


## Engineering Rules

- Every feature must have an issue
- Every PR must be reviewed
- Use TypeScript strictly
- Do not merge broken builds
- Keep commits small
- Write useful PR descriptions
- Add tests for core logic

## Branching Strategy

- `main`: stable production branch
- `dev`: active development
- `feature/<name>`: individual feature branches
- `fix/<name>`: bug fix branches

## Definition of Done

A task is done only when:

- Feature works locally
- Code is reviewed
- No TypeScript errors
- Basic tests pass
- UI is responsive
- Documentation updated if needed
