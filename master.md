# SocialBoost AI — Master Project Rules

**Document:** `master.md`  
**Version:** 1.1
**Status:** Baseline project authority  
**Product:** SocialBoost AI  
**Market:** India first  
**Architecture:** Cloud-first modular monolith

---

## 1. Purpose and authority

This document defines the product scope, architecture, engineering standards, security rules, and delivery process for SocialBoost AI.

Every contributor and AI coding agent (including Codex) MUST follow these rules.

### 1.1 Source of truth

1. `master.md` is the authoritative project-wide rulebook.
2. `docs/REQUIREMENTS.md` defines approved product requirements.
3. `docs/ARCHITECTURE.md` defines approved architecture.
4. `docs/DATABASE_SCHEMA.md` defines approved database design.
5. `docs/API_SPECIFICATION.md` defines approved API contracts.
6. `docs/DEVELOPMENT_RULES.md` defines detailed coding conventions.
7. `docs/PHASE_1_TASKS.md` defines the active delivery scope.
8. If documents conflict, stop and report the conflict. Do not silently choose or rewrite architecture.
9. Update documentation when an approved implementation decision changes.

### 1.2 Mandatory scope control

- Work ONLY on the current approved phase and task.
- Do not implement future-phase features early.
- Do not add features, libraries, services, endpoints, database tables, abstractions, or infrastructure unless required by the current task or explicitly approved.
- Do not redesign the architecture because another approach seems preferable.
- Do not rename apps, modules, models, fields, endpoints, or folders without approval.
- Do not introduce microservices.
- Do not add speculative functionality or "nice-to-have" features.
- If a requirement is unclear, ask one concise clarification question before making a consequential assumption.
- If a requested task conflicts with this file, explain the conflict and wait for approval.
- Prefer the smallest complete implementation that satisfies the approved requirement.

**Out-of-scope rule:** When a task is complete, stop. Do not continue to the next task automatically.

---

## 2. Product vision and guardrails

**Product promise:** Create once. Optimize intelligently. Reach more people.

SocialBoost AI is an AI-powered video content optimization, distribution, and discovery platform. Its primary goal is to help creators, individuals, and businesses maximize genuine organic reach and video views, including creators who have zero followers or subscribers. It is not simply another social networking application.

**Primary success metric:** Maximum genuine organic reach and views. This is a product objective, not a guarantee to users.

### 2.1 Main user journey

1. A creator uploads a video.
2. AI analyzes the video and its context and recommends improvements to its organic reach potential.
3. AI generates platform-specific titles, hooks, captions, descriptions, and hashtags.
4. The creator reviews, edits, and approves recommendations.
5. The creator selects one or more destinations and explicitly approves external publishing.
6. SocialBoost distributes the video through supported official platform APIs.
7. SocialBoost's discovery engine can recommend it to relevant viewers, including people who do not follow the creator.
8. The creator reviews available analytics and AI-driven improvement suggestions.

### 2.2 Core capabilities

**AI content optimization** analyzes video content and relevant context. Recommendations may cover the first three seconds and hook, title and opening text, captions and descriptions, hashtags and keywords, format and aspect ratio, audience relevance, platform-specific optimization, and actionable discoverability improvements. All recommendations are editable and require creator approval.

**Creator-controlled distribution** plans support for Instagram Reels, YouTube Shorts, Facebook Reels, and the SocialBoost internal video platform. AI may recommend destinations and optimizations; creators choose destinations and approve publishing. Use only official, authorized APIs and respect permissions, OAuth requirements, app reviews, rate limits, API capabilities, and platform policies. Never use unauthorized browser automation, workarounds, or policy bypasses.

**SocialBoost organic discovery** includes an internal video feed and recommendation engine. Follower count must not be the sole or dominant discovery eligibility factor. Discovery may consider viewer interests and relevance, video content and topic, interactions and feedback, watch duration and completion, content quality and freshness, and safety, moderation, and anti-manipulation signals.

### 2.3 Mandatory product guardrails

- Never generate or facilitate fake views, followers, likes, comments, or watch time; bots; engagement pods; spam; or artificial engagement.
- Never guarantee virality, specific view counts, or audience growth, and never claim control over third-party ranking algorithms.
- AI recommends; creators review, edit, and approve. Explicit creator approval is required before external publishing. AI output cannot authorize publishing or another privileged action.
- Clearly distinguish SocialBoost metrics from third-party metrics. Preserve metric source, definitions, reporting period, and limitations.
- A single user account can have multiple capabilities, such as creator and viewer. Do not create duplicate accounts for these capabilities.
- Avoid unnecessary follower-management features and scope expansion before the core video journey is complete.

## 3. Approved technology architecture

Use these technologies unless a change is explicitly approved.

| Area | Approved technology |
|---|---|
| Frontend | React + TypeScript web application first |
| Mobile | React Native in a later phase |
| Backend | Django + Django REST Framework |
| Database | PostgreSQL |
| Authentication | JWT with refresh-token rotation and revocation |
| Architecture | Modular monolith |
| Background processing | Redis + Celery in a later phase |
| AI integration | Provider abstraction |
| Local AI development | Ollama with Qwen3 |
| Video processing | FFmpeg |
| Video storage | S3-compatible object storage |
| Video delivery | CDN and HLS in a later phase |
| External integrations | Official Instagram, YouTube, and Facebook APIs |
| API documentation | OpenAPI using drf-spectacular |
| Testing | pytest + pytest-django |
| Deployment | Cloud-first production architecture |
| Development environment | Native Windows development first; Docker where available |
| Version control | Git |

### 3.1 Architecture style

- Use a **modular monolith**. Do not introduce microservices without explicit approval.
- Keep Django apps separated by business capability and introduce them only in their approved phase.
- Keep domain logic independent from infrastructure providers where practical.
- Use adapters for external social platforms and AI providers.
- Use Redis and Celery for background processing only in the phase that introduces them.
- Keep PostgreSQL as the source of truth.
- Keep the AI provider layer modular so local Ollama can be used during development and other providers can be added through adapters later.
- Backend validation and authorization enforce permissions. AI output never independently authorizes publishing or another privileged action.

### 3.2 Approved Django app boundaries

Create apps incrementally, only when their phase begins:

- `accounts`
- `profiles`
- `businesses`
- `videos`
- `media_processing`
- `feed`
- `interactions`
- `social_integrations`
- `publishing`
- `analytics`
- `ai_assistant`
- `recommendations`
- `moderation`
- `notifications`

Do not create empty apps simply to match this list. Do not create an app outside this list without approval.

## 4. Locked development roadmap and phase gates

Work follows this sequence. A listed roadmap item is not authorization to start it.

### Phase 1 — Foundation and project setup
- Repository and project structure.
- Django and React setup.
- PostgreSQL configuration.
- Environment configuration and secret management.
- Git readiness and baseline commit.
- Development and governance documentation.

### Phase 2 — Accounts and authentication
- Custom User model before initial migrations, UUID primary key, normalized unique email, custom user manager, Django admin integration, account status, and timestamps.
- JWT authentication with refresh rotation and revocation.
- Role/capability foundation for individual, creator, viewer, business, and admin; profile foundation.
- No social OAuth in this phase.

### Phase 3 — Video upload and media pipeline
- Video upload, file validation and size/type restrictions, storage integration, metadata extraction, FFmpeg processing, thumbnails, preview and playback, processing status and failure handling.

### Phase 4 — AI content optimization
- Ollama/Qwen3 and AI provider abstraction; video/context analysis; hook recommendations; titles, captions, descriptions, and hashtags; platform-specific recommendations; creator review, editing, and approval.

### Phase 5 — SocialBoost discovery and viewer experience
- Internal video feed and relevance-based recommendations; discovery for new creators, including creators with zero followers; basic viewer interactions; moderation and discovery eligibility; impression, playback, watch-time, and completion event collection.

### Phase 6 — External social connections and multi-platform publishing
- OAuth integrations; secure token storage, refresh, and revocation; separate platform adapters; platform capabilities and permissions; destination selection and explicit creator approval; publishing jobs, status tracking, idempotency, and bounded retries; official APIs only.

### Phase 7 — Analytics and growth recommendations
- Internal analytics; external analytics where officially available; metric attribution and definitions; performance comparisons; AI-powered growth recommendations.

### Phase 8 — Production hardening and mobile
- Redis/Celery; production storage and CDN; HLS delivery; monitoring and audit logs; backups and recovery; security review; load and performance testing; production deployment; React Native application.

### 4.1 Approval gates

- The project owner approves the active phase and task. Work only on that scope and never jump ahead.
- A phase is not complete merely because its implementation appears finished. Review its approved acceptance criteria and relevant tests, report results and outstanding issues, and request the project owner's explicit approval to proceed.
- Do not start the next phase until the owner explicitly approves progression. Approval of one task does not approve later tasks or phases.
- Stop after the approved task and wait for the owner's next instruction.

---

## 5. Foundation and implementation rules

### 5.1 Initial project layout

```text
socialboost-ai/
├── master.md
├── AGENTS.md
├── README.md
├── docs/
│   ├── REQUIREMENTS.md
│   ├── ARCHITECTURE.md
│   ├── DATABASE_SCHEMA.md
│   ├── API_SPECIFICATION.md
│   ├── DEVELOPMENT_RULES.md
│   ├── SECURITY.md
│   ├── MIGRATION_PLAN.md
│   └── PHASE_1_TASKS.md
├── backend/
│   ├── config/
│   ├── apps/
│   ├── common/
│   ├── tests/
│   ├── requirements/
│   └── manage.py
├── frontend/
│   └── src/
└── infrastructure/
```

Create directories and files only when needed. Do not add placeholder files without a purpose.

### 5.2 Custom user model — critical rule

- Implement the custom Django user model before the first project migration.
- Set `AUTH_USER_MODEL = "accounts.User"` before generating initial migrations.
- Use Django `AbstractBaseUser` only. Do not use `PermissionsMixin`.
- Use UUID primary keys and normalized unique email as the login identifier.
- Implement a custom user manager, account status, and timestamps.
- Do not use Django default username as the authentication identifier.
- Implement only admin/staff behavior required by the approved design. If Django admin integration requires user-model decisions not documented here, obtain project-owner approval before making them.
- Use `settings.AUTH_USER_MODEL` for user foreign keys in every app.
- Never replace or redesign the user model after migrations have been applied without an approved migration strategy.

### 5.3 Database rules

- PostgreSQL is the development and production relational database.
- Use UUID primary keys for domain entities.
- Use explicit Django field types and model choices.
- Add database-level unique constraints for important uniqueness rules.
- Add indexes based on actual query patterns and approved requirements.
- Use foreign-key deletion behavior deliberately.
- Use transactions for multi-record operations.
- Use migrations for every schema change.
- Never edit an already-applied migration to change database history.
- Never run destructive database commands or delete data without explicit approval.
- Before applying migrations, inspect the migration plan.
- Do not create speculative tables for future phases.

### 5.4 Backend code organization

- Keep API views thin.
- Put business logic in service functions or service classes.
- Use serializers for request validation and response representation.
- Use explicit permission classes.
- Use `select_related` and `prefetch_related` when appropriate.
- Avoid N+1 queries.
- Keep settings separated by environment.
- Read configuration from environment variables.
- Never commit `.env` files, passwords, API keys, tokens, or private credentials.
- Use structured logging without secrets or sensitive payloads.

### 5.5 API rules

- All application endpoints use `/api/v1/`.
- Use REST conventions and correct HTTP methods/status codes.
- Use trailing slashes consistently.
- Validate all user input.
- Apply authentication and resource-level authorization.
- Use consistent JSON response and error structures.
- Paginate collection endpoints.
- Do not expose internal exception traces to clients.
- Document endpoints in OpenAPI.
- Do not create endpoints outside the approved API specification without approval.

### 5.6 Frontend rules

- Use React with TypeScript.
- Keep API calls in service modules, not scattered through components.
- Use typed request and response models.
- Keep reusable UI components separate from feature modules.
- Handle loading, empty, validation, and error states.
- Do not place secrets or social tokens in browser code.
- Do not trust frontend permission checks as backend security.
- Do not add a UI library or state-management dependency without checking whether it is needed and getting approval for material additions.

---

## 6. Security and privacy rules

Security is mandatory from the first implementation.

1. Never hardcode credentials or secrets.
2. Never log passwords, JWTs, OAuth tokens, verification tokens, or sensitive personal data.
3. Hash passwords using Django's supported password hashers.
4. Protect private endpoints by default.
5. Enforce object-level and business-membership authorization on the backend.
6. Use HTTPS in deployed environments.
7. Apply authentication and sensitive-operation rate limits.
8. Validate file content and uploads in the media phase.
9. Encrypt third-party OAuth tokens at rest in the integration phase.
10. Keep AI agents away from unrestricted credentials and direct privileged operations.
11. Require user approval for external publishing.
12. Support account deactivation and applicable data deletion requirements.
13. Do not expose one user's or business's private data to another.
14. Do not weaken security to make tests pass.

For India-first production, review applicable privacy and data-protection obligations, retention, consent, subprocessors, and data deletion before launch. Do not claim legal compliance without an appropriate review.

---

## 7. AI coding agent rules — Codex

Codex MUST behave as a careful implementation assistant, not as an autonomous product owner.

Before each task:

1. Read `AGENTS.md`.
2. Read this `master.md`.
3. Read the relevant approved documents under `docs/`.
4. Inspect the existing repository and current Git status.
5. Identify the exact requested task and its phase.
6. Report the planned files and changes for consequential work.

During implementation:

- Work only on the requested task.
- Preserve existing working behavior.
- Follow existing conventions.
- Prefer small, reviewable changes.
- Do not rewrite unrelated files.
- Do not silently change dependencies or architecture.
- Do not add features outside the approved scope.
- Do not invent requirements.
- Do not delete user work.
- Do not stage, commit, push, deploy, or publish unless explicitly asked.
- Do not run destructive commands.
- Do not change environment or production configuration without approval.

After implementation:

1. List files created or changed.
2. Explain the implementation briefly.
3. List commands executed.
4. Report test results accurately.
5. Report migrations created and their impact.
6. Identify remaining issues or untested behavior.
7. Stop and wait for the next instruction.

If a test fails, investigate the root cause. Do not remove, weaken, skip, or rewrite tests merely to get a passing result.

If an instruction is ambiguous or conflicts with an approved requirement, stop and ask for clarification.

---

## 8. Testing and quality gates

- Every meaningful business rule requires automated tests.
- Test success and failure paths.
- Test authentication and authorization boundaries.
- Test cross-user and cross-business access prevention.
- Test database constraints.
- Do not rely only on manual testing.
- Do not report tests as passed unless they were actually executed.
- Do not hide skipped or failing tests.
- Run relevant tests after each implementation task.
- Run the full Phase 1 suite before requesting Phase 1 acceptance.

A task is complete only when its implementation, tests, documentation, and acceptance criteria are reviewed.

---

## 9. Git and change management

- Use Git from the beginning.
- Keep the main branch stable.
- Use a short-lived feature branch for each substantial task.
- Review `git status` before and after changes.
- Do not overwrite uncommitted user changes.
- Do not commit secrets, generated media, virtual environments, build artifacts, or local databases.
- Do not amend or rewrite existing commits without approval.
- Do not push to remote repositories without explicit approval.

Suggested branch naming:

- `feature/phase-1-project-setup`
- `feature/phase-2-accounts-auth`
- `feature/phase-3-video-upload`

---

## 10. Dependency management

- Add only dependencies required for the current approved task.
- Check compatibility with the project's Python and Node versions.
- Pin or constrain dependencies appropriately.
- Update dependency lock/requirements files when dependencies change.
- Explain why a new dependency is needed.
- Do not install overlapping libraries that solve the same problem without approval.
- Do not upgrade the entire dependency stack as part of an unrelated task.

---

## 11. Definition of done

Every task must satisfy all applicable items:

- [ ] Matches the approved requirement.
- [ ] Stays within the current phase.
- [ ] Follows the approved architecture.
- [ ] Implements backend validation and authorization where applicable.
- [ ] Includes appropriate tests.
- [ ] Relevant tests executed and results reported.
- [ ] Migrations reviewed where applicable.
- [ ] API documentation updated where applicable.
- [ ] No secrets or sensitive data exposed.
- [ ] No unrelated files or behavior changed.
- [ ] Changes summarized for project-owner review.

---

## 12. Current project execution state

**Current phase:** Phase 1 — Foundation and project setup
**Current sprint:** Sprint 1 — Project foundation
**Current status:** Phase 1 technical setup has been implemented and checked. Django system check passed; PostgreSQL connection verified; React production build passed; environment and secret-handling checks performed.

- No application migrations have been created or applied.
- Initial Git baseline commit is pending review and explicit project-owner approval.
- Phase 1 formal sign-off is pending.
- Phase 2 has not been approved to start.

Do not treat these checks as Phase 1 sign-off or authorization to begin Phase 2. Await project-owner review and explicit approval.

## 13. Final governing principle

**Stay within SocialBoost AI. Stay within the approved phase. Follow the approved architecture. Do not invent scope. Do not make consequential decisions without approval. Implement, test, report, and stop.**

The project owner has final authority over product scope and architecture.

## Document change history

- **1.1** — Corrected the approved custom user model guidance, updated Phase 1 execution status, and aligned branch examples with the roadmap.
- **1.0** — Baseline project authority.
