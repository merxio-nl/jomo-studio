# CLAUDE.md

## Role

Claude Code is the primary implementation agent for this repository. It works
directly in the codebase to execute tasks specified by the product/technical
architect (ChatGPT) and approved by the repository owner, who makes final
product decisions. GitHub is the shared source of truth between ChatGPT and
Claude Code.

## This repository

This repository contains **only JOMO Studio** — the active, live product.
There is no legacy version and no nested project directory: `brand/`,
`src/`, `public/`, `docs/`, and this file all live at the repository root.
If you're about to create a new top-level directory for something
JOMO-related, put it at root — do not recreate a `v2/`-style nested
namespace. (JOMO was extracted from a prior monorepo,
`merxio-nl/PORTFOLIO`, where it lived under `v2/` alongside an unrelated
legacy site — see `docs/DECISIONS.md` ADR-012. That structure no longer
applies here.)

## Before implementation

- Read `docs/PROJECT.md`, `docs/WORKFLOW.md`, and `docs/DECISIONS.md` (and any
  other relevant project documentation) before starting implementation work.
- Confirm the task matches an already-approved decision or specification. If
  it doesn't, flag the gap rather than deciding unilaterally.

## Content integrity

- Preserve truthful copy. Do not invent metrics, testimonials, client
  outcomes, or capabilities that aren't real — see the per-project facts
  in `docs/PROJECT.md` and the case-study content under
  `src/content/projects/`.
- Avoid AI-slop: generic agency language, hollow claims, and copy that
  doesn't sound like it was written by the actual person running the
  studio. This applies in English, Russian, and Dutch alike.
- Russian is the approved editorial source for the site's voice. English
  and Dutch are independent, natural localizations of the same facts —
  not literal translations of each other.

## Tool requirements

- Use **Context7 MCP** whenever current external library/framework/API
  documentation matters (setup, config, version-specific syntax, migrations).
  Prefer it over relying on training data or web search for library docs.
- Use **Playwright MCP** for browser/UI verification whenever a change is
  visual, interactive, or affects rendered output (layout, responsiveness,
  navigation, console errors).
- Check `git status` before starting work and again after finishing, to
  confirm the change set matches intent and nothing unrelated was touched.

## Git and change discipline

- Never commit directly to `main` for implementation work unless explicitly
  instructed by the repository owner.
- Never push, merge, deploy, delete files, or perform other destructive Git
  operations (force-push, reset --hard, branch deletion, etc.) unless
  explicitly instructed.
- Do not silently change product requirements or architecture. Surface any
  such need for a decision instead of assuming one.
- Major architecture or technology-stack decisions (framework migrations,
  new build tooling, replacing an already-accepted stack) require explicit
  repository-owner approval before implementation. Proposing and explaining
  a change is fine; implementing it without that approval is not. The
  established Astro + Tailwind + Content Collections stack should not be
  rolled back or replaced within a refinement/polish task — only within a
  task that explicitly scopes that decision.
- Prefer small, reviewable changes over large or speculative ones.
- Project-specific assets (brand material, images, content) belong in the
  directory that already matches their kind (`brand/`, `public/`,
  `src/content/`) — don't introduce new top-level asset folders without a
  clear reason.

## Repository/PR handoff to ChatGPT

For implementation tasks that produce repository changes, follow this
sequence (see `docs/WORKFLOW.md` for full detail):

1. Work on a dedicated feature branch.
2. Verify the implementation before reporting completion.
3. Only after explicit owner authorization to publish the work, commit and
   push the feature branch.
4. Create a GitHub Pull Request when GitHub CLI/API access is available,
   using the PR description structure defined in `docs/WORKFLOW.md`
   (Summary, Files changed, Verification, Issues/limitations, Decisions
   needed, Review focus). The PR is the primary handoff artifact to
   ChatGPT, not a separate report.
5. The deployment model is Preview → owner review → explicit merge
   approval: every feature branch gets an automatic Vercel Preview;
   nothing reaches production until the owner explicitly approves merging
   to `main`.
6. Creating a report or recommending a next step never authorizes
   merge/deploy — that authorization comes from the repository owner only.
- Do not create a continuously modified `STATUS.md` or similar log for
  routine task reports, and do not store chat transcripts in the
  repository.

## Reporting

After each implementation task (whether or not a PR is created), report in
chat:

1. Files changed.
2. Verification performed (tests run, Playwright checks, manual review).
3. Unresolved issues or open questions.
4. Recommended next step.
