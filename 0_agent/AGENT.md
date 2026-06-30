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
- Avoid scattering policy across multiple subpackages; keep runtime behavior centralized.
- Preserve deterministic traces for harness replay.
