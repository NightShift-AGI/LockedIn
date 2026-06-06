# lockedin Architecture

## 1. High-Level Architecture

lockedin will use a modern web architecture:

- Web frontend
- Backend API
- PostgreSQL database
- AI service layer
- Search layer
- Background jobs later
- Object storage later

## 2. Recommended MVP Architecture

```text
User
  |
  v
Next.js Web App
  |
  |-- Auth
  |-- Profile UI
  |-- Feed UI
  |-- Search UI
  |-- AI Assistant UI
  |
  v
API Layer
  |
  |-- User Service
  |-- Profile Service
  |-- Post Service
  |-- Follow Service
  |-- Search Service
  |-- AI Service
  |
  v
PostgreSQL + Prisma
```

## 3. Core Modules

### 3.1 Auth Module

Responsibilities:

- Register
- Login
- Logout
- Session validation
- Protected routes

### 3.2 User/Profile Module

Responsibilities:

- Store user identity
- Store public profile
- Store skills
- Store experience
- Store projects
- Store education

### 3.3 Feed Module

Responsibilities:

- Create posts
- List feed
- Like posts
- Comment on posts
- Follow-based ranking later

### 3.4 AI Module

Responsibilities:

- Rewrite profile bio
- Improve headline
- Generate post ideas
- Improve post clarity
- Suggest skills
- Generate project descriptions

Important design rule:

All AI providers should be abstracted behind one interface so the project can support OpenAI, open-source models, or local LLMs later.

### 3.5 Search Module

MVP:

- PostgreSQL full-text search

Later:

- Meilisearch, Typesense, or Elasticsearch
- Vector search for semantic discovery

## 4. Data Model Draft

### User

- id
- email
- password_hash
- name
- username
- created_at
- updated_at

### Profile

- id
- user_id
- headline
- bio
- location
- website
- github_url
- linkedin_url
- portfolio_url

### Skill

- id
- name

### UserSkill

- user_id
- skill_id

### Experience

- id
- user_id
- company
- role
- start_date
- end_date
- description

### Project

- id
- user_id
- title
- description
- url
- github_url
- tags

### Post

- id
- user_id
- content
- created_at
- updated_at

### Follow

- follower_id
- following_id

### Comment

- id
- post_id
- user_id
- content
- created_at

### Like

- user_id
- post_id

### AIRequestLog

- id
- user_id
- feature
- prompt_type
- input_hash
- output
- created_at

## 5. Security

- Hash passwords
- Validate all inputs
- Rate-limit AI endpoints
- Prevent prompt injection where possible
- Sanitize user-generated content
- Add moderation for spam later
- Do not expose API keys to client

## 6. Scalability Plan

### MVP

- Monolithic Next.js app
- PostgreSQL
- Simple API routes
- Hosted on Vercel/Render/Fly.io

### Growth Stage

- Separate backend service
- Redis cache
- Search engine
- Background workers
- Object storage
- Observability stack

### Scale Stage

- Microservices only if necessary
- Recommendation service
- Vector database
- Event-driven architecture
