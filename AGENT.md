# Root Agent Rules

## Operating Mode

- Default to `proposal-first`.
- When given only a product request, first inspect the repo structure and the nearest instructions before doing anything else.
- For each new problem request, study the requirement, reason about suitable features and tech stack options, then propose them for user review before any implementation step.
- Do not ask the user to provide folder paths or prompt templates unless the repo is missing the needed guidance.
- Your first output for a new request should usually be a proposal with recommended features, tech stack, assumptions, and tradeoffs, not code.

## Default Workflow

1. Read this file first, then the closest folder-specific `AGENT.md`.
2. Inspect `README.md`, `config.yaml`, and the feature area related to the request.
3. Infer the smallest feature scope that satisfies the request.
4. Propose the feature set, tech stack, major workflow, assumptions, and open questions for user review.
5. Let the user edit or confirm the proposal before moving to the next step.
6. Create or update only the proposal files after confirmation:
   - `spec.md`
   - `acceptance.md`
   - `feature.manifest.yaml`
   - `AGENT.md`
   - Include the feature's frontend and backend routes in `feature.manifest.yaml`.
7. Stop and wait for human approval.
8. Only after approval, implement code inside `0_app/` and update harness/test artifacts if needed.
9. When a bug is found during a run, add or update a regression test that reproduces the bug before or alongside the fix.

## Hard Rules

- Treat `0_app/` as the only editable product surface.
- Treat `0_agent/` as runtime code, not product logic.
- Treat `0_harness/` as read-only evaluation infrastructure unless a scenario or fixture change is required.
- Do not write production code before approval.
- Do not create or edit proposal files for a new problem until the user has reviewed or confirmed the proposed features and tech stack.
- Do not fix a reproducible bug without adding coverage that would catch the same failure next time.
- Do not expand scope without first calling it out clearly.
- Follow the repository naming convention when creating folders:
  - top-level folders use `0_`
  - first-level child folders use `1_`
  - second-level child folders use `2_`
  - deeper levels continue increasing numerically
- For features, create folders under `0_app/1_features/2_<feature-name>/`.
- Treat `0_app/1_feature_templates/` as reference-only templates, not product features.
- When a real request matches a template, copy and adapt it into `0_app/1_features/2_<feature-name>/` after user confirmation.
- Do not implement, approve, or route product behavior directly from a template folder.
- For feature internals, keep implementation folders numbered to match their shared depth, for example `3_backend/`, `3_frontend/`, and `3_tests/`.
- Every feature manifest must declare route ownership under `routes.frontend` and `routes.backend`, even if one side is an empty list.
- Do not introduce, rename, or remove a frontend page route or backend API route without updating the owning feature's `feature.manifest.yaml`.
- Put bug regression coverage in the closest relevant test location: feature-level `3_tests/` for product bugs, `0_tests/` for agent/runtime plumbing, or `0_harness/1_scenarios/` plus fixtures for harness behavior.

## Repo Discovery

- Prefer reading existing files over asking questions.
- Use the current repository structure as the primary source of truth.
- If a request maps to an existing feature folder, extend that folder instead of creating a new pattern.
- If a request maps to a feature template, use it as proposal guidance but create a real feature folder under `0_app/1_features/`.
- If a request does not fit an existing feature, create a new feature folder under `0_app/1_features/2_<feature-name>/`.

## Output Style

- Keep proposals short, concrete, and reviewable.
- Make assumptions explicit.
- Flag missing information only when it blocks a safe proposal.
- Keep instructions local and easy to trace.
