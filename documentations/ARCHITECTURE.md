# lockedin Architecture

## 1. High-Level Architecture

lockedin is built as a federated professional network where independent instances (nodes) can host their own communities while communicating seamlessly via the **ActivityPub** protocol.

The database and backend-relevant services are built using **Supabase** (incorporating Supabase Auth, Supabase Database, Supabase Storage, and Supabase Edge Functions where possible) as our primary technical stack. When serverless/Edge architectures are insufficient (e.g. for custom cryptographic handshakes, ActivityPub signature matching, and complex dynamic routing), Next.js API Routes and standard Prisma query models are used as the fallback backend layer.

```text
               [ Peer lockedin Instance ]
                           ^
                           | (ActivityPub via Webfinger & Inbox/Outbox)
                           v
   User -> [ Next.js Web App / API ]
             |
             +---> [ Ingestion Service ] (LinkedIn/JSON Resume imports)
             +---> [ Verification Service ] (Domain DNS / SMTP check)
             +---> [ Feed Weight Engine ] (Slider-weighted ranking calculations)
             +---> [ AI Service Abstraction ] (Local/OpenAI models)
             +---> [ ActivityPub Engine ] (Inbox/Outbox routing & HTTP signatures)
             |
             v
  [ Supabase (PostgreSQL, Auth, Storage, Edge Functions) + Prisma ]
```

---

## 2. Core Modules

### 2.1 Auth & Key Management Module
- **Responsibilities**: Local user signup, login, session validation, and JWT management (primary implementation utilizes **Supabase Auth**).
- **Federation requirement**: Upon registration, generates a unique RSA-256 key pair for the user. The public key is published on the user's actor profile, and the private key is encrypted and stored in the database, used to sign outbound federated messages (HTTP Signatures).


### 2.2 User/Profile & Verification Module
- **Responsibilities**: Manages local profiles and parses/indexes profiles from other instances.
- **Verification Engine**: Executes email/domain checks. Generates a DNS TXT verification token (e.g., `lockedin-challenge=xxxx`) or sends a confirmation code to a work email address (e.g., `user@company.com`). Once verified, records a trusted verification entry and displays a cryptographic verification badge.

### 2.3 Portability & Ingestion Module
- **Responsibilities**: Handles user onboarding migrations.
- **Ingestion Engine**: Parses a JSON Resume file or LinkedIn archive export (zip file containing CSV/JSON profiles, experiences, education, and skills) and maps it to the Prisma profile schema. Instructs the AI module to auto-tag and match skills from the imported data.

### 2.4 Feed & Weight Engine
- **Responsibilities**: Computes custom feeds dynamically.
- **Dynamic Weighting**: Calculates feed ranks on query requests using client-specified slider parameters:
  $$\text{Post Score} = (w_{\text{recency}} \times \text{RecencyScore}) + (w_{\text{verified}} \times \text{VerificationScore}) + (w_{\text{skills}} \times \text{SkillMatchScore})$$
  This gives users absolute control over algorithmic curation directly from the UI.

### 2.5 ActivityPub Federation Module
- **Responsibilities**: Handles cross-instance follow/post synchronization.
- **Endpoints**:
  - `/.well-known/webfinger`: Resolves user queries (e.g., `bob@instance.org`) to actor profile URIs.
  - `/users/[username]`: Serves the ActivityPub Actor JSON profile.
  - `/users/[username]/inbox`: Receives signed incoming activities (Create, Follow, Accept, Undo).
  - `/users/[username]/outbox`: Publishes activities representing local user actions.

### 2.6 AI Module
- **Responsibilities**: Interface for text improvements (headlines, bios, posts).
- **Rule**: All AI models must be accessed through an abstraction interface to support swapping between OpenAI, local Ollama endpoints, or private Hugging Face instances.

### 2.7 Search Module
- **Responsibilities**: Local database search and discovery. Supports skill filtering, role search, and vector similarity mapping.

---

## 3. Data Model Draft (Prisma Schema Reference)

```prisma
model User {
  id           String    @id @default(uuid())
  email        String    @unique
  passwordHash String
  name         String
  username     String    @unique
  publicKey    String    // For ActivityPub HTTP Signatures
  privateKey   String    // Encrypted RSA private key
  createdAt    DateTime  @default(now())
  updatedAt    DateTime  @updatedAt
  profile      Profile?
  posts        Post[]
  comments     Comment[]
  likes        Like[]
}

model Instance {
  id          String    @id @default(uuid())
  domain      String    @unique // e.g. "lockedin.university.edu"
  sharedInbox String
  status      String    // "ACTIVE", "BLOCKED"
  createdAt   DateTime  @default(now())
  profiles    Profile[]
}

model Profile {
  id             String         @id @default(uuid())
  userId         String?        @unique
  user           User?          @relation(fields: [userId], references: [id])
  instanceId     String?        // Null for local users
  instance       Instance?      @relation(fields: [instanceId], references: [id])
  apActorUri     String?        @unique // URI for remote actors
  headline       String?
  bio            String?
  location       String?
  website        String?
  githubUrl      String?
  jsonResumeData Json?          // Store raw imported data
  experiences    Experience[]
  skills         UserSkill[]
  verifications  Verification[]
}

model Verification {
  id          String    @id @default(uuid())
  profileId   String
  profile     Profile   @relation(fields: [profileId], references: [id])
  domain      String    // Verified organization domain (e.g. "google.com")
  verifiedAt  DateTime  @default(now())
  method      String    // "DNS_TXT" or "EMAIL_CONFIRM"
}

model Skill {
  id        String      @id @default(uuid())
  name      String      @unique
  profiles  UserSkill[]
}

model UserSkill {
  profileId String
  profile   Profile @relation(fields: [profileId], references: [id])
  skillId   String
  skill     Skill   @relation(fields: [skillId], references: [id])
  @@id([profileId, skillId])
}

model Experience {
  id          String    @id @default(uuid())
  profileId   String
  profile     Profile   @relation(fields: [profileId], references: [id])
  company     String
  role        String
  startDate   DateTime
  endDate     DateTime?
  description String?
}

model Post {
  id        String    @id @default(uuid())
  userId    String
  user      User      @relation(fields: [userId], references: [id])
  apId      String    @unique // ActivityPub unique URI for the post
  content   String
  local     Boolean   @default(true) // False if fetched from remote instance
  createdAt DateTime  @default(now())
  updatedAt DateTime  @updatedAt
  comments  Comment[]
  likes     Like[]
}

model Follow {
  id          String   @id @default(uuid())
  followerUri String   // URI of the follower (supports remote actor URIs)
  followingUri String  // URI of the followed actor
  status      String   // "PENDING", "ACCEPTED"
}

model Comment {
  id        String   @id @default(uuid())
  postId    String
  post      Post     @relation(fields: [postId], references: [id])
  userId    String
  user      User     @relation(fields: [userId], references: [id])
  content   String
  createdAt DateTime @default(now())
}

model Like {
  userId String
  user   User   @relation(fields: [userId], references: [id])
  postId String
  post   Post   @relation(fields: [postId], references: [id])
  @@id([userId, postId])
}

model FeedPreference {
  id             String @id @default(uuid())
  userId         String @unique
  recencyWeight  Float  @default(0.5)
  verifiedWeight Float  @default(0.3)
  skillWeight    Float  @default(0.2)
}
```

---

## 4. Security

- **HTTP Signatures**: Validate signature headers on incoming ActivityPub messages against remote public keys to authenticate nodes.
- **Content Sanitization**: Remote posts must pass through a strict HTML/Markdown sanitizer before rendering to eliminate XSS injections.
- **DNS Verification Safeguards**: Verify DNS TXT queries strictly against official name-servers and apply timeouts to prevent server hangs.

---

## 5. Scalability & Sustainability Plan

### MVP
- Single-instance Next.js deployment.
- Database, authentication, and file storage hosted on **Supabase** (utilizing PostgreSQL, Supabase Auth, and Supabase Storage).
- Synchronous ActivityPub processing fallback via Next.js API routes where edge/serverless contexts are not suitable.


### Growth Stage
- Redis queues for background federation tasks (e.g., retrying outbox post deliveries).
- Caching layer for remote profiles and actors.
- Node sharding: Universities and companies spin up individual nodes, distributing infrastructure load and server costs.

### Scale Stage & Sustainability
- **Federated Moderation**: Sharing instance-level blocklists (similar to Mastodon blocklists) to mitigate MLMs and spammers.
- **Enterprise APIs**: Paid access hooks to federated nodes for corporate ATS tools, allowing recruiters to pull verified profiles (granting sustainable revenue to the parent foundation).

