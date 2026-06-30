# MVP Structure

This repo is trimmed for an MVP agent + harness workflow.
The current shape is intentionally small:

- `0_agent/` contains the runtime logic for planning, context loading, tool wiring, and LLM adapters.
- `0_app/` contains the product code the agent is allowed to edit.
- `0_harness/` contains the runner, evaluator, tracer, metrics, report generation, and scenarios.
- `0_tests/` contains fast checks for agent and harness plumbing.
- `config.yaml` is the single source of truth for runtime settings.
- `AGENT.md` files define instruction precedence from repo root to folder-specific rules.

## Naming Convention

- Top-level folders use `0_`.
- First-level child folders use `1_`.
- Second-level child folders use `2_`.
- Deeper levels continue increasing numerically.
- Feature folders live under `0_app/1_features/2_<feature-name>/`.
- Feature templates live under `0_app/1_feature_templates/2_<template-name>/`.
- Feature internals use the same feature number, for example `3_backend/`, `3_frontend/`, and `3_tests/`.

## Design Rules

- Keep the runtime small and predictable.
- For new problem requests, have the agent propose suitable features and tech stack for user review before writing proposal files or implementation code.
- Use `0_app/1_feature_templates/` only as reference material; real product features still belong under `0_app/1_features/`.
- Keep feature instructions next to the feature.
- Keep evaluation data separate from production code.
- Add regression coverage whenever a bug is found during a run, so the same failure is caught next time.
- Prefer one module per concern until the concern grows enough to justify splitting.
- Keep configuration in one root file until the settings become genuinely hard to navigate.

## How To Use It

1. Read the root [AGENT.md](AGENT.md) first, then the closest folder-specific `AGENT.md`.
2. Put product changes under `0_app/`, ideally inside a feature folder such as `0_app/1_features/2_auth/`.
3. Use templates such as `0_app/1_feature_templates/2_auth/` only to shape proposals; copy and adapt them into `0_app/1_features/2_<feature-name>/` after user confirmation.
4. Describe the feature in `spec.md`, `acceptance.md`, and `feature.manifest.yaml`.
5. Use `0_app/1_shared/` for reusable UI, utilities, or types that are truly cross-feature.
6. Add or update a harness scenario in `0_harness/1_scenarios/` when you want a reproducible run.
7. Store stable eval inputs and goldens in `0_harness/1_fixtures/`, with level-2 subfolders such as `2_expected/`, `2_inputs/`, and `2_screenshots/`.
8. Keep runtime settings in `config.yaml` instead of scattering them across multiple files.
9. Put fast safety checks in `0_tests/` so the agent and harness plumbing stays honest.

## Runtime Artifacts

The harness is expected to write generated files outside source folders, typically under `artifacts/` for:

- traces
- reports
- failures

These files are runtime output, not source of truth.
