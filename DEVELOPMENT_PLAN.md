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

### Sprint 1: Auth and User Model

- Auth pages
- User schema
- Session handling
- Protected routes

### Sprint 2: Profile System

- Profile schema
- Profile create/edit UI
- Public profile page
- Skill tags
- Project links

### Sprint 3: Feed

- Post schema
- Create post
- Feed page
- Like/comment basic support
- Follow system

### Sprint 4: AI Assistant

- AI rewrite bio
- AI improve headline
- AI improve post
- AI generate project summary
- Prompt logging

### Sprint 5: Search and Discovery

- User search
- Post search
- Skill filters
- Basic recommendations

### Sprint 6: Polish and Launch

- Landing page
- Documentation
- Seed data
- Bug fixes
- Deployment
- Public GitHub launch

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
