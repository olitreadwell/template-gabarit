# canada-ca/template-gabarit context
> refreshed 2026-09-05 | upstream default: main @ 0926777

## Identity & policies
- upstream: canada-ca/template-gabarit, default branch main, language: JavaScript (markdown + link-check tooling) — a bilingual (en/fr) template repo for Government of Canada open-source projects.
- English-first: yes/no — repo is deliberately bilingual; maintain BOTH languages in any edit. English variants (AU/UK/USA/CA/NZ spellings) are not typos.
- CLA/DCO: none found (no CLA bot, no DCO in CONTRIBUTING). CONTRIBUTING is minimal; suggests discussing via Issues first.
- AI-assisted PR policy: unstated (no ban, no disclosure requirement). org canada-ca has no .github defaults.
- signed commits required: no.
- PR template: PRESENT `.github/PULL_REQUEST_TEMPLATE/general.md` — fill verbatim (What does this MR do / General checklist / Related issues). This repo uses GitLab-era "MR" language.
- external tracker: github.

## Conventions (verified)
- branch naming: no dominant human pattern; recent merged PRs are all dependabot. Human historical branches: e.g. `code-conduct`, `master`. Use `fix/<kebab>`.
- commit style: dependabot conventional `chore(deps): ...`; human history uses imperative plain (e.g. "adding issue/pr templates", "fix: Remove duplicate option file reading"). Prefer imperative, conventional-commit-style `fix(...)` is seen in history ("fix: Remove duplicate option file reading").
- test command: `npm test` = `npm run lint` (markdownlint) + `npm run link-check`. CI: markdownlint.yml + link-check.yml (GitHub Actions). Both green on current main.
- how outside PRs get merged: effectively only dependabot merges in recent months; repo is low-activity (stars ~23) but CI is maintained. No recent evidence of human PR merges.

## Maintainer picture
- Low-activity maintenance (dependabot commits only for months). gcharest / shawnthompson / delisma historically active. No in-flight maintainer PRs.

## Issue-area health
- 7 open issues, ALL stale (2019-2022), mostly no maintainer acceptance: #182 (crown copyright, 2022), #142 (purpose of link-check.js/package files, 2022), #23 (include cSpell, 2020, enhancement), #10 (fr code-of-conduct, 2021), #9 (commit message templates, 2021), #7 (probot config, 2019), #4 (Canada mark in license, 2019, question).
- No maintainer-engaged open issue survives the filters -> use repo-audit matrix for a self-found, verifiable gap.

## Gap ledger (dedupe — READ FIRST, never re-pick)
- 2026-09-05 self-found gap (audit: clean code / docs / tests-ci) — the repo's markdown quality tooling silently EXCLUDES the `.github/` markdown templates: markdownlint runs `**/*.md` without `-d` and link-check.js globs `**/*.md` without `dot:true`, so `.github/ISSUE_TEMPLATE/*.md` (and the PR template) are never linted or link-checked. Verified: `npx markdownlint -d "**/*.md"` reports 2 real MD001 heading-increment errors in bug.md + feature.md that `npm run lint` currently misses; globs skip dot-dirs by default (fast-glob/npm-glob dot:false). Dedupe: no upstream issue/PR (open/closed/merged) addresses lint/link coverage of .github templates or MD001 in them. — status: proposed (will attempt same cycle)

## Mined gaps (discovered, not yet attempted)
- 2026-09-05 tests-ci/clean-code: add `-d` to markdownlint glob and `dot:true` to link-check.js glob so issue + PR templates are covered; fix the 2 MD001 heading-increment errors they surface (top-level `###` -> `##` in bug.md + feature.md). Repro: `npm run lint` exits 0 while `npx markdownlint -d "**/*.md"` exits 1 with 2 errors. Expected: all checks cover `.github/**/*.md` and pass. — status: proposed
