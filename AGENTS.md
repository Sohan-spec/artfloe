# Documentation project instructions

## Repository role

Thally has three distinct repositories. `thallylabs/thally` is the only
authored source for the open-source runtime and toolchain,
`thallylabs/starter` is this complete customer-ready template, and
`thallylabs/thally-cloud` is the private control plane.

The sole production architecture authority is
[`thally-cloud/ARCHITECTURE.md`](https://github.com/thallylabs/thally-cloud/blob/main/ARCHITECTURE.md).
That repository is private; this file defines only starter-local ownership and
workflow rules. Do not create another architecture document here.

Runtime-owned files in this repository are a generated snapshot, not a second
implementation. Never hand-apply a runtime fix here. Run the **Sync Thally
runtime** workflow, review its generated pull request, and let CI prove that
the snapshot matches the exact runtime commit in `starter-release.json`.

Before placing a feature, trace the actual creation or request path in code and
identify the deployed artifact. Do not infer ownership from repository names
or an outdated planning document.

Package versions, scaffold releases, managed site releases, and Cloud platform
releases are separate identities. A starter synchronization does not itself
upgrade an existing site or move a production release pointer.

## Project boundaries

- Pages are MDX files in `src/content/`.
- Navigation and portable product features are configured in `docs.json`.
- Site identity and versioned brand defaults live in `src/data/site.ts`.
- `starter-release.json` and runtime-owned paths listed in it are
  machine-managed; do not hand-edit them.
- Runtime changes belong in `thallylabs/thally` and arrive here only through
  the generated synchronization pull request.
- Starter-owned seed content and portable defaults are authored here. Paid
  service internals remain in `thallylabs/thally-cloud`.
- Never place credentials in source files. Use `.env.local` locally and secret
  storage in the deployment platform.

## Writing standards

- Address the reader as “you” and use active voice.
- Lead with the outcome, then state prerequisites and the shortest working path.
- Use sentence-case headings and concise paragraphs.
- Format commands, files, configuration keys, and code with backticks.
- Tell readers what success looks like and link the next useful task.
- Keep advanced or optional paths outside the primary workflow.

## Content model

- Every page needs `title` and `description` frontmatter.
- Keep page slugs stable once published.
- Add pages to `docs.json`; do not leave useful pages orphaned.
- Update `openapi.yaml` when API behavior changes.
- Run `npm ci --ignore-scripts --prefix .github/thally-tooling`, then
  `.github/thally-tooling/node_modules/.bin/thally check --ci .`, `npm test`,
  and `npm run build` before publishing.

## Product context

ArtFloe is the product. The app repo is ArtFlow-CloudFlare (Flask + Modal GPU).
This folder is the public docs site only.

Document what the code does now. Do not describe Stripe, Clerk, SAM 3,
Real-ESRGAN upscale, or GET `/predict` as shipped. Do not copy secret values
into pages. Env *names* may appear in operator guides (`guides/run-locally`,
`guides/deploy`) when the reader must set them; never paste values.

### Canonical terms (use these everywhere)

| Concept | Term |
|---------|------|
| Built-in look | catalog style |
| User-uploaded look | custom style |
| One `/predict` run | generation |
| Monthly count | quota (not credits) |
| Keeping people photoreal | person preservation |
| Browser mix of preserve layers | subject blend |
| Razorpay or Dodo | gateway |
| Plans | Free / Pro / Max (`plan_tier`: `free` / `pro` / `max`) |

Pages live under Diátaxis folders: `quickstart` (tutorial), `guides/` (how-to),
`reference/` (facts), `concepts/` (why). Do not mix those types on one page.

<!-- BEGIN:nextjs-agent-rules -->

# This is NOT the Next.js you know

This version has breaking changes — APIs, conventions, and file structure may all differ from your training data. Read the relevant guide in `node_modules/next/dist/docs/` (resolved from this file's directory; in monorepos the `next` package may not be visible from the repo root) before writing any code. Heed deprecation notices.

This block is written and re-added by `next dev` — verify at `node_modules/next/dist/server/lib/generate-agent-files.js`. Removing it from a diff only re-creates the uncommitted change; committing it with your work keeps the tree clean.

<!-- END:nextjs-agent-rules -->
