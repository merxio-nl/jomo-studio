# JOMO Studio

A founder-led digital studio brand — website strategy, design, and
development. This repository is the actively maintained JOMO Studio
website: a multilingual (EN/RU/NL) Astro site with a homepage, a Work
index, and per-project case studies.

See `docs/PROJECT.md` for verified project facts and development
history, and `docs/DECISIONS.md` for architecture decisions (including
how this project was extracted into its own repository — ADR-012).

## Tech stack

- [Astro](https://astro.build) (static output)
- Tailwind CSS v4, configured via the `@theme` block in
  `src/styles/global.css` (no separate `tailwind.config.*` file — v4
  doesn't need one)
- Astro Content Collections (schema-validated via Zod) for project/
  case-study data

## Languages

English (default, unprefixed route), Russian (`/ru/`), Dutch (`/nl/`).
Russian is the editorial source of truth for tone/facts; English and
Dutch are independent, natural localizations of the same content, not
literal translations — see `docs/DECISIONS.md` ADR-009.

## Project structure

```text
jomo-studio/
├── brand/                logo/wordmark/OG-card source assets — see brand/README.md
├── docs/                 PROJECT.md, WORKFLOW.md, DECISIONS.md
├── public/               static assets, served as-is (images, favicon, og-image.png)
├── src/
│   ├── components/       shared UI components
│   │   └── views/        full-page views, parameterized by lang (en/ru/nl)
│   ├── content/projects/ project data, one folder per locale (en/, ru/, nl/)
│   ├── i18n/              UI copy dictionary + locale helpers
│   ├── layouts/           Base.astro (document shell, fonts, metadata)
│   ├── pages/             EN routes; RU/NL routes live under pages/ru/, pages/nl/;
│   │                      also sitemap.xml.ts, robots.txt.ts, 404.astro
│   └── styles/            global.css (design tokens, base styles)
├── astro.config.mjs
├── package.json
└── tsconfig.json
```

## Local development

```bash
npm install
npm run dev          # start local dev server at localhost:4321
```

When running through Claude Code, start the dev server in background
mode (`astro dev --background`) and manage it with `astro dev stop`,
`astro dev status`, and `astro dev logs`.

## Build / check

| Command | Action |
| :--- | :--- |
| `npx astro check` | Type-check the project |
| `npm run build` | Build the production site to `./dist/` |
| `npm run preview` | Preview the build locally |

## Adding a project

Add matching `src/content/projects/en/<slug>.json`,
`src/content/projects/ru/<slug>.json`, and
`src/content/projects/nl/<slug>.json` entries (see `src/content.config.ts`
for the schema). Narrative fields (`problem`/`solution`/`outcome`) are
optional — leave them unset rather than inventing content for a project
that doesn't have a full case study yet. New projects automatically
appear in `sitemap.xml` — no extra step needed. See `docs/PROJECT.md`
for the truthfulness rules around case-study facts.

## Adding UI copy

Add the string to the `en`, `ru`, and `nl` blocks in `src/i18n/ui.ts`,
then reference it via `useTranslations(lang)`. Don't hardcode
user-facing text into components.

## Deployment

Deploys via Vercel, connected to this GitHub repository. Every feature
branch gets an automatic Preview deployment; nothing reaches production
until the repository owner explicitly approves merging to `main`. See
`docs/WORKFLOW.md` for the full collaboration/handoff process.

## Workflow

This repository follows an owner → ChatGPT (architect/reviewer) →
Claude Code (implementer) collaboration model, with GitHub as the shared
source of truth. See `CLAUDE.md` for agent-specific rules and
`docs/WORKFLOW.md` for the full process.
