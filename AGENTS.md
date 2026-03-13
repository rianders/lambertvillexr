# AGENTS.md

## Project Values

- Preserve the production site at `https://flowingtogether.lambertvillenj.org/`.
- Treat this project as a static site first. Builds should continue to work from `.output/public`.
- Prefer low-risk, incremental changes over broad rewrites.
- Keep fork previews easy to use without breaking the production custom-domain deployment.
- Favor practical XR usability over cleverness. If an interaction is hard to use on-device, simplify it.

## Hosting Rules

- Production is deployed through GitHub Pages and mapped to the custom domain `flowingtogether.lambertvillenj.org`.
- Production builds must keep `NUXT_APP_BASE_URL=/`.
- Fork or branch previews may use repo-subpath URLs under `https://<owner>.github.io/lambertvillexr/previews/<branch-name>/`.
- Do not change the production hosting model unless there is an explicit decision to move away from the custom domain root.

## Development Rules

- Use Node 20.
- Prefer `npm ci` over `npm install` for reproducible setup.
- Validate static output with `npm run generate` after meaningful changes.
- When testing locally, prefer static preview behavior over dev-only behavior if the issue affects deployment or XR device testing.

## XR / Quest Priorities

- Quest usability matters for both controllers and hand tracking.
- Important interactions should not depend on only one input mode if a practical fallback exists.
- Tutorial and entry flows should always provide an obvious exit or skip path.
- If HTML overlay controls do not work reliably in immersive XR, provide an in-scene fallback.

## Change Guidelines

- Keep upstream compatibility in mind. This fork should remain easy to turn into pull requests against upstream.
- Avoid introducing floating dependency pins when a stable version is available.
- Prefer documenting operational assumptions in the repo when deployment behavior is non-obvious.
- When changing shared XR components, assume the change affects site pages, demo pages, and the standalone tutorial unless proven otherwise.

## Testing Priorities

- First verify `/tutorial` for onboarding and skip behavior.
- Then verify at least one real site page under `/sites/`.
- For GitHub Pages changes, confirm both the `main` workflow run and the Pages publish step.
- For Quest-specific fixes, distinguish between production, preview branches, and stale cached builds before concluding that a change failed.

## Working Workflow

- Start with local validation using `npm run generate`.
- When the issue needs headset testing, prefer a published fork preview before changing `main`.
- Keep a stable preview branch available when it helps Quest testing. That branch may be reset to match `main` when needed.
- Treat fork `main` as the production-shaped verification step, not the first test step.
- Only open an upstream pull request after the change has been validated on the fork.

## Release Flow

1. Make the change on a branch.
2. Run `npm run generate`.
3. Test locally if the issue can be reproduced without the published site.
4. Push the branch and test the GitHub Pages preview on device.
5. Merge or promote the change to fork `main` once the preview is acceptable.
6. Confirm the `main` workflow run and Pages publish succeeded.
7. Re-test the published site on device if the change is XR-sensitive.
8. Open the upstream pull request when the fork is in a known-good state.
