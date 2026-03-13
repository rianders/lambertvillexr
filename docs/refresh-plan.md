# Lambertville XR Refresh Plan

Last updated: 2026-03-13

## Goals

- Restore confidence that the repo can be developed, built, and deployed reliably.
- Remove known security exposure that affects the published site.
- Bring the fork and deployment setup into a maintainable state for future pull requests.
- Reduce technical drift in the Nuxt and GitHub Pages toolchain.

## Current State Summary

- Local `main`, `origin/main`, and `upstream/main` are aligned at `7a937ef1b220e6db0a4fc74c6156c02d3d25fa3a`.
- `origin` points to `rianders/lambertvillexr`.
- `upstream` points to `lambertvillenj/lambertvillexr`.
- The project still installs and generates successfully.
- The repo uses an early Nuxt 3 stack and an old GitHub Pages workflow.
- `npm audit` reports 64 vulnerabilities: 8 low, 18 moderate, 34 high, 4 critical.

## Phase 1: Immediate Risk Reduction

### 1. Remove `polyfill.io`

Reason:
- The project loads `https://polyfill.io/v3/polyfill.min.js` from `nuxt.config.ts`.
- That third-party domain is no longer considered trustworthy and should not remain in production.

Actions:
- Remove the script entirely if it is not required.
- If a polyfill is still needed, replace it with a maintained and trusted alternative.
- Rebuild and smoke test the site after removal.

Definition of done:
- No `polyfill.io` references remain in the repo.
- The site builds and loads without runtime regressions in supported browsers.

### 2. Fix broken static generation output

Reason:
- `npm run generate` completes but reports broken prerender targets for `/storymap` and a malformed credits link.

Actions:
- Replace the local `/storymap` redirect route with a plain external link pattern, or explicitly exclude it from prerendering.
- Fix malformed Creative Commons links in `pages/credits.vue`.

Definition of done:
- `npm run generate` finishes without broken-route warnings from the current site content.

## Phase 2: Build and Deployment Stabilization

### 3. Modernize GitHub Pages workflow

Reason:
- CI still uses Node 16 and `npm install`.
- Deployment base path is hardcoded to `/`, which is fragile for GitHub Pages forks and repo-name-based hosting.

Actions:
- Move to current GitHub Actions versions.
- Move CI to Node 20 LTS.
- Use `npm ci` in CI.
- Make `NUXT_APP_BASE_URL` repo-aware or document that deployment requires a custom domain root.

Definition of done:
- CI uses current maintained actions and Node 20.
- Deployment behavior is documented and reproducible for the chosen hosting model.

### 4. Pin the local runtime expectations

Reason:
- The repo has no `.nvmrc`, `.node-version`, or equivalent version pin.
- Local Node 20 works, but the current dependency tree still emits engine warnings.

Actions:
- Add a Node version file.
- Update README setup instructions to match the pinned version and actual build steps.

Definition of done:
- Developers can see the expected Node version without reading workflow YAML.

## Phase 3: Dependency Refresh

### 5. Replace moving-edge dependencies with stable pins

Reason:
- `@nuxthq/ui` is currently sourced from `ui-edge@latest`, which makes future refreshes less predictable.

Actions:
- Switch to a stable package release and pin it explicitly.
- Regenerate the lockfile and run a full build.

Definition of done:
- No production dependency is sourced from a floating `latest` edge channel.

### 6. Upgrade the Nuxt stack as a planned batch

Reason:
- Most audit findings come from the old Nuxt, Nitro, Vite, and supporting build stack.
- Incremental patching is likely to be noisy and harder to verify than one coordinated upgrade pass.

Actions:
- Upgrade Nuxt, Nitro, Vite-related modules, and other direct dependencies together.
- Regenerate the lockfile.
- Re-run install, generate, and manual smoke checks.

Definition of done:
- Audit results are materially reduced.
- The site still builds, prerenders, and serves correctly.

## Phase 4: Documentation and Cleanup

### 7. Resolve host and metadata inconsistencies

Reason:
- README, env defaults, and runtime metadata reference different canonical hosts.

Actions:
- Pick the canonical deployment URL.
- Update README, `env-defaults.sh`, and `nuxt.config.ts` defaults to match.

Definition of done:
- Documentation and generated metadata reference the same intended host.

### 8. Add a lightweight maintenance checklist

Reason:
- The project sat for a long time without a clear refresh process.

Actions:
- Add a short checklist covering dependency review, Pages verification, and basic smoke tests.

Definition of done:
- The next refresh cycle is easier and less ad hoc.

## Recommended Execution Order

1. Remove `polyfill.io`.
2. Fix prerender warnings and malformed links.
3. Modernize CI and deployment config.
4. Pin Node version and refresh README.
5. Replace edge dependency pins.
6. Upgrade the Nuxt dependency stack.
7. Normalize host metadata and docs.

## Validation Checklist

- `npm ci`
- `npm run generate`
- Verify homepage, credits page, and at least one site route locally
- Verify generated asset paths under the chosen Pages base URL
- Confirm GitHub Pages deployment succeeds from `main`
