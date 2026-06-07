# lockedin Intern Execution Plan

## Goal

Give interns clear, beginner-friendly work that contributes directly to the MVP.

## Intern Roles

### Frontend Intern

Responsibilities:

- Build reusable UI components
- Create profile pages
- Create feed UI
- Create search page
- Improve responsive design

Starter Tasks:

- Create landing page and auth page UI
- Create drag-and-drop JSON Resume / LinkedIn zip file uploader component
- Add feed customizer UI sliders (Recency, Verified, and Skills weights)
- Create verified domain badge component for public profiles
- Create responsive navigation and feed layouts

### Backend Intern

Responsibilities:

- Build APIs and controller logic
- Work with database models and Prisma clients
- Write parsing and verification routines
- Write integration tests for API endpoints

Starter Tasks:

- Build LinkedIn archive zip and JSON Resume file parsing handler
- Build weighted feed sorting API (reading query parameters for sliders)
- Build DNS TXT record challenge generator and validation API
- Create local SMTP verification mail router
- Create Webfinger lookup (`/.well-known/webfinger`) and public Actor JSON endpoints

### AI Intern

Responsibilities:

- Build prompt templates for profile optimizations
- Design skill auto-extraction and tags indexing layer
- Test output formatting and safety filters

Starter Tasks:

- Prompt engineering for auto-extracting skill arrays from raw resume text
- Prompt for headline improvement suggestions
- Prompt for bio rewrite suggestions
- Add logs tracker for AI calls with injection sanitization

### DevOps/Docs Intern

Responsibilities:

- Maintain documentation
- Configure environment containers
- Set up automated testing pipelines

Starter Tasks:

- Create Docker Compose configuration for spin-up of local self-hosted instances
- Write local setup guide detailing custom domain mapping and SMTP setup
- Add issue templates and PR template files
- Set up GitHub Actions CI for Lint/Test validation

## Weekly Workflow

### Monday

- Sprint planning
- Assign issues
- Clarify acceptance criteria

### Wednesday

- Midweek check-in
- Resolve blockers
- Review PRs

### Friday

- Demo completed work
- Merge finished PRs
- Write weekly update

## Rules for Interns

- Pick one issue at a time
- Ask questions early
- Create small PRs
- Add screenshots for UI PRs
- Explain what changed in every PR
- Never commit secrets
- Keep code readable

## First 10 Issues

1. Set up Next.js app, Postgres connection, and local Prisma DB structure
2. Create landing page and Auth UI (Signup/Login/Logout)
3. Add cryptographic RSA-256 keypair generator upon local signup
4. Build drag-and-drop JSON Resume & LinkedIn archive uploader UI
5. Create parser service to ingest uploaded resumes and hydrate profile records
6. Build public profile page displaying work history, education, and verified badges
7. Build feed dashboard containing algorithm curating weight sliders
8. Build backend weighted feed controller supporting Recency, Verified, and Skills weights
9. Implement DNS TXT validation crawler and SMTP challenge validator
10. Implement Webfinger (`/.well-known/webfinger`) and Actor JSON response paths

