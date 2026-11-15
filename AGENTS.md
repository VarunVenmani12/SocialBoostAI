# Codex Instructions — SocialBoost AI

Before starting any task in this repository:

1. Read the root `master.md` completely. It is the authoritative source for product vision, architecture, roadmap, and development governance.
2. Read the relevant approved documents in `docs/`. If a referenced document is missing or conflicts with `master.md`, report that fact; do not invent its contents or silently resolve the conflict.
3. Follow the current execution status and approved task in `master.md`. Roadmap entries do not authorize work by themselves. Phase 1 formal sign-off is pending and Phase 2 is not approved to start; never start a later phase without explicit project-owner approval.
4. Stay within the approved SocialBoost AI scope and current task. Do not add speculative features, architecture, dependencies, apps, tables, endpoints, or infrastructure.
5. Inspect existing files, tests, and Git status before changing implementation. Preserve user work, secrets, and unrelated changes.
6. Do not install packages, apply migrations, commit, push, deploy, or modify external systems unless the task explicitly authorizes it. Do not run destructive commands.
7. For consequential changes, explain the proposed files and plan before implementation. Prefer small, modular, testable changes and follow existing naming and structure.
8. Add or update tests for implementation changes and run the relevant approved tests. Report actual results; never claim unrun tests passed.
9. At completion, summarize changed files, commands executed, test results, migration status, and outstanding issues or risks.
10. Stop after the approved task. A task approval does not approve the next task or phase; request explicit approval before phase progression.

For ambiguity or conflicts, identify the specific issue and ask the project owner before making a consequential assumption. Never let AI output authorize publishing or another privileged action; backend validation and authorization must enforce permissions. External social integrations must use official, authorized APIs and comply with platform policies.
