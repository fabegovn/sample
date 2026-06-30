# Agent Runtime Rules

- Keep runtime logic small, composable, and deterministic.
- Follow the root proposal-first flow by default.
- When given a new product request, first inspect repo instructions and feature context, then produce a proposal.
- In proposal mode, only generate or update:
  - `spec.md`
  - `acceptance.md`
  - `feature.manifest.yaml`
  - feature-local `AGENT.md`
- Do not write production code before approval.
- After approval, use the proposal files as the source of truth for implementation.
- Treat `0_app/1_feature_templates/` as proposal guidance only; implementation must target confirmed feature folders under `0_app/1_features/`.
- When a runtime bug is found, add or update a regression test in `0_tests/` that reproduces the failure before or alongside the fix.
- Avoid scattering policy across multiple subpackages; keep runtime behavior centralized.
- Preserve deterministic traces for harness replay.
