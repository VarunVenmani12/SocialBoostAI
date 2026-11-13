# SocialBoost AI — Master Project Rules

**Document:** `master.md`  
**Version:** 1.0  
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

## 2. Product definition

SocialBoost AI is a hybrid video-sharing and organic audience-growth platform for individuals, creators, viewers, and businesses.

It has three product capabilities:

1. **Owned video community:** users can publish and discover videos inside SocialBoost AI.
2. **External distribution:** authorized users can publish approved content to supported third-party social platforms using their official APIs.
3. **AI growth assistance:** AI can help analyze content, draft metadata, and provide evidence-based organic-growth suggestions.

### 2.1 Product principles

- Focus on genuine organic discovery and engagement.
- Never generate fake views, fake followers, bot likes, spam comments, or artificial engagement.
- Never promise viral reach or guaranteed audience growth.
- Do not bypass social platform restrictions, API permissions, rate limits, or review processes.
- User approval is required before an external publishing action.
- Platform-specific analytics must remain clearly attributed to their source and definitions.

### 2.2 Target users

- Individual users and viewers.
- Creators.
- Businesses and their authorized team members.
- Platform administrators and moderators.

### 2.3 Product market

- India-first launch.
- Design for international expansion without adding unsupported localization or compliance features prematurely.
- Store timestamps in UTC; display them in the user's configured timezone.
- Do not hardcode India-specific assumptions into reusable domain logic.

---

## 3. Approved technology stack

Use these technologies unless a change is explicitly approved.

| Area | Approved technology |
|---|---|
| Web frontend | React + TypeScript |
| Mobile frontend | React Native + TypeScript |
| Backend | Django + Django REST Framework |
| Database | PostgreSQL |
| Authentication | JWT with refresh-token rotation and revocation |
| Background jobs | Celery |
| Cache / broker | Redis |
| AI local provider | Ollama with Qwen3 |
| AI cloud provider | Provider adapter; provider selected by configuration |
| Video processing | FFmpeg |
| Speech recognition | Whisper, when its phase is approved |
| Media storage | S3-compatible object storage |
| Video delivery | CDN and HLS, when media phase is approved |
| Containers | Docker / Docker Compose |
| API documentation | OpenAPI using drf-spectacular |
| Backend tests | pytest + pytest-django |
| Version control | Git |
| CI | GitHub Actions, when CI task is approved |

### 3.1 Architecture style

- Use a **modular monolith**.
- Keep Django apps separated by business capability.
- Do not create microservices in the initial product.
- Keep domain logic independent from infrastructure providers where practical.
- Use adapters for external social platforms and AI providers.
- Use asynchronous workers for long-running tasks.
- Keep PostgreSQL as the source of truth.

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

---

## 4. Delivery phases and strict phase gates

### Phase 1 — Foundation, identity, profiles, businesses

Approved scope:

- Repository and project setup.
- Django backend and React web frontend setup.
- PostgreSQL configuration.
- Docker development environment.
- Custom user model.
- Registration and authentication.
- Email verification and password reset.
- JWT authentication and refresh-token revocation.
- User and creator profiles.
- Business profiles and business membership.
- Authorization and tests.
- OpenAPI documentation.

Not included in Phase 1:

- Video upload, video playback, transcoding, or streaming.
- Social feed, likes, comments, follows, or recommendations.
- Instagram, Facebook, YouTube, or other social integrations.
- External publishing or scheduling.
- AI agents, AI content generation, or analytics.
- Monetization.
- React Native implementation.
- Production cloud deployment beyond approved preparation.

### Phase 2 — Video platform

Only after Phase 1 acceptance:
- Video metadata and upload workflow.
- Object storage integration.
- Media validation and processing.
- Thumbnail generation.
- Playback and delivery.
- Internal video feed and interactions, according to approved requirements.

### Phase 3 — External social integration and publishing

Only after Phase 2 acceptance:
- OAuth account connections.
- Official platform API adapters.
- Permission and token management.
- Publishing requests and jobs.
- Scheduling, status tracking, and safe retries.

### Phase 4 — AI assistance

Only after the relevant video and publishing workflows are stable:
- AI provider abstraction.
- Ollama integration.
- Configurable cloud provider.
- Content analysis and metadata generation.
- User review and approval.

### Phase 5 — Analytics and recommendations

Only after reliable event and analytics data exists:
- Internal analytics.
- Permitted external analytics.
- Feed ranking and recommendations.
- Organic-growth suggestions.

### Phase 6 — Production hardening and mobile

Only after scope approval:
- Production deployment and scaling.
- Security and load testing.
- Monitoring and backup validation.
- React Native application.
- Operational readiness.

**Phase gate:** Do not begin a later phase until the current phase's acceptance criteria and tests pass and the project owner explicitly approves progression.

---

## 5. Phase 1 implementation rules

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
- Use `AbstractBaseUser` and `PermissionsMixin`.
- Implement a correct custom user manager.
- Use normalized unique email as the login identifier.
- Do not use Django's default username as the authentication identifier.
- Use UUID primary keys.
- Include explicit account status and timestamps.
- Implement staff/superuser behavior correctly for Django admin.
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
- `feature/phase-1-authentication`
- `feature/phase-1-profiles`
- `feature/phase-1-businesses`
- `fix/<short-description>`

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

**Current phase:** Phase 1 — Foundation  
**Current sprint:** Sprint 1 — Project foundation  
**Current task:** Initial repository and environment inspection, followed by project setup  
**Completed:** Codex extension installed in VS Code  
**Not yet confirmed:** Repository location, existing project files, Python version, Node.js version, Docker availability, PostgreSQL availability, Git status

### Immediate next task

Do not generate application models or database migrations yet.

First inspect the current workspace and report:

1. Current workspace root.
2. Existing files and folders.
3. Git repository status and current branch.
4. Python version.
5. Node.js and npm versions.
6. Docker availability.
7. PostgreSQL availability, without printing credentials.
8. Any existing project configuration that must be preserved.

Do not install, delete, overwrite, migrate, commit, or push anything during this inspection.

After reporting the findings, propose the smallest Sprint 1 setup plan and wait for the project owner's approval before making changes.

---

## 13. Final governing principle

**Stay within SocialBoost AI. Stay within the approved phase. Follow the approved architecture. Do not invent scope. Do not make consequential decisions without approval. Implement, test, report, and stop.**

The project owner has final authority over product scope and architecture.
