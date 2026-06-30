# App Rules

- This is the only place the agent should make product changes.
- Do not edit product code until the feature proposal is approved.
- For a new request, create or update the feature folder under `0_app/1_features/2_<feature-name>/` first.
- Keep folder names aligned with depth-based numbering:
  - `0_` at the top level
  - `1_` for first-level children
  - `2_` for second-level children
  - and so on
- Use `0_app/1_shared/` for code that is genuinely shared across multiple features.
- Keep `spec.md`, `acceptance.md`, `feature.manifest.yaml`, and feature-local `AGENT.md` beside the feature.
- After approval, implement only within the approved feature scope.
- If a change is truly cross-feature, introduce shared code only when reuse is real and obvious.
- Add infrastructure folders only when a cross-feature boundary is real.
- Keep changes localized and avoid broad refactors unless they are part of the approved scope.
