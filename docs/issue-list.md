# Lambertville XR Issue List

Last updated: 2026-03-13

## Immediate

### 1. Remove `polyfill.io` from production HTML

Priority: P0

Why it matters:
- This is the clearest direct browser-side security risk in the current project.

Suggested issue title:
- `security: remove polyfill.io script from Nuxt head config`

Scope:
- Remove the external script from `nuxt.config.ts`.
- Replace with a trusted alternative only if needed.
- Smoke test the site after removal.

Acceptance criteria:
- No `polyfill.io` reference remains in the repository.
- The site still builds and loads in supported browsers.

### 2. Fix broken prerender targets in static export

Priority: P1

Suggested issue title:
- `build: eliminate generate warnings for /storymap and malformed credits links`

Scope:
- Resolve `/storymap` so it is not treated as a broken internal prerender route.
- Fix malformed external links in `pages/credits.vue`.

Acceptance criteria:
- `npm run generate` finishes without the current broken-route warnings.

## Near Term

### 3. Update GitHub Pages workflow to a maintained baseline

Priority: P1

Suggested issue title:
- `ci: modernize GitHub Pages workflow for Node 20 and npm ci`

Scope:
- Update `actions/checkout` and `actions/setup-node`.
- Use Node 20.
- Use `npm ci`.
- Confirm deploy still publishes `.output/public`.

Acceptance criteria:
- Workflow runs successfully from `main`.
- Build behavior matches local validation.

### 4. Make deployment base URL match the intended hosting model

Priority: P1

Suggested issue title:
- `deploy: document custom-domain root hosting and optional preview base URL mode`

Scope:
- Document that production is served from `flowingtogether.lambertvillenj.org` at the domain root.
- Keep production `NUXT_APP_BASE_URL=/`.
- Document repo-subpath builds as an optional preview mode for forks.

Acceptance criteria:
- Generated asset URLs work on the production custom domain.
- Hosting assumptions are documented in README.

### 5. Add a pinned Node version file

Priority: P2

Suggested issue title:
- `dx: add pinned Node version and align README setup instructions`

Scope:
- Add `.nvmrc` or `.node-version`.
- Update README prerequisites and install/build instructions.

Acceptance criteria:
- Developers can reproduce the expected runtime locally without guessing.

## Dependency Refresh

### 6. Replace `@nuxthq/ui-edge@latest` with a stable release

Priority: P2

Suggested issue title:
- `deps: replace ui-edge latest dependency with a stable pinned release`

Scope:
- Update `package.json`.
- Refresh lockfile.
- Verify build output.

Acceptance criteria:
- No production dependency uses a floating edge `latest` source.

### 7. Upgrade Nuxt and related build dependencies

Priority: P2

Suggested issue title:
- `deps: upgrade Nuxt, Nitro, Vite, and related build stack`

Scope:
- Update direct Nuxt and build-time dependencies.
- Regenerate lockfile.
- Re-test static generation.

Acceptance criteria:
- Audit findings are materially reduced from the current 64 total.
- The app still installs, builds, and generates successfully.

### 8. Review A-Frame and AR-related dependency risk

Priority: P2

Suggested issue title:
- `deps: evaluate aframe and AR package upgrade path`

Scope:
- Review the impact of upgrading `aframe`, `@ar-js-org/ar.js`, and related packages.
- Document compatibility risk if upgrades are deferred.

Acceptance criteria:
- There is a documented decision to upgrade now or accept a temporary exception.

## Documentation and Content

### 9. Normalize canonical host references

Priority: P3

Suggested issue title:
- `docs: align README, env defaults, and metadata with one canonical site URL`

Scope:
- Update README host references.
- Update `env-defaults.sh`.
- Update metadata defaults in `nuxt.config.ts`.

Acceptance criteria:
- Repo docs and generated metadata point at one intended host.

### 10. Add a lightweight maintenance checklist

Priority: P3

Suggested issue title:
- `docs: add periodic maintenance checklist for dependencies and deployment`

Scope:
- Add a short checklist for dependency review, build verification, and Pages validation.

Acceptance criteria:
- The repo includes a simple recurring maintenance process.

## Optional Follow-Up

### 11. Compare fork network hosting decisions

Priority: P3

Suggested issue title:
- `project: document roles of origin, upstream, and canonical source repo`

Scope:
- Document the relationship between `rianders`, `lambertvillenj`, and `RutgersGRID`.
- Clarify which repo receives PRs and which host is considered canonical.

Acceptance criteria:
- Contributors know where to branch, where to open PRs, and where deployment is expected.
