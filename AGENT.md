# Root Agent Rules

## Operating Mode

- Default to `proposal-first`.
- When given only a product request, first inspect the repo structure and the nearest instructions before doing anything else.
- Do not ask the user to provide folder paths or prompt templates unless the repo is missing the needed guidance.
- Your first output for a new request should usually be a proposal, not code.

## Default Workflow

1. Read this file first, then the closest folder-specific `AGENT.md`.
2. Inspect `README.md`, `config.yaml`, and the feature area related to the request.
3. Infer the smallest feature scope that satisfies the request.
4. Create or update only the proposal files first:
   - `spec.md`
   - `acceptance.md`
   - `feature.manifest.yaml`
   - `AGENT.md`
5. Stop and wait for human approval.
6. Only after approval, implement code inside `0_app/` and update harness/test artifacts if needed.

## Hard Rules

- Treat `0_app/` as the only editable product surface.
- Treat `0_agent/` as runtime code, not product logic.
- Treat `0_harness/` as read-only evaluation infrastructure unless a scenario or fixture change is required.
- Do not write production code before approval.
- Do not expand scope without first calling it out clearly.
- Follow the repository naming convention when creating folders:
  - top-level folders use `0_`
  - first-level child folders use `1_`
  - second-level child folders use `2_`
  - deeper levels continue increasing numerically
- For features, create folders under `0_app/1_features/2_<feature-name>/`.
- For feature internals, keep implementation folders numbered to match depth, for example `3_backend/`, `4_frontend/`, and `5_tests/`.

## Repo Discovery

- Prefer reading existing files over asking questions.
- Use the current repository structure as the primary source of truth.
- If a request maps to an existing feature folder, extend that folder instead of creating a new pattern.
- If a request does not fit an existing feature, create a new feature folder under `0_app/1_features/2_<feature-name>/`.

## Output Style

- Keep proposals short, concrete, and reviewable.
- Make assumptions explicit.
- Flag missing information only when it blocks a safe proposal.
- Keep instructions local and easy to trace.
