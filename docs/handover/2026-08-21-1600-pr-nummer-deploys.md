# 2026-08-21 16:00 — PR-nummer vooraan deploytitels (zelfde afspraak als AHQ)

Romy wil in de Vercel-deploylijst het PR-nummer vooraan élke deploy (preview
én productie), net als in AutomatingHQ (#1214 daar) en Romy-HQ (#57).

## Wat er veranderd is

- **`.github/workflows/pr-nummer-prefix.yml`** (nieuw, 1-op-1 uit AHQ):
  zet bij aanmaken/bewerken van een PR automatisch `#<nr> — ` vóór de
  PR-titel (idempotent, alleen voor PR's uit deze repo zelf).
- **`CLAUDE.md`** (Git workflow): afspraak toegevoegd — PR direct na de eerste
  push openen (draft mag), daarna elke commit-subject met `#<nr> — ` beginnen;
  alleen de allereerste push blijft nummerloos. Repo-instellingen-blok
  bijgewerkt: squash-default = "Pull request title" + verwijzing naar de
  bestaande `ci.yml`-check (de oude regel "geen GitHub Actions-CI" klopte
  niet meer).

## ⚠️ Handmatige actie voor Romy (admin, GitHub UI)

*Settings → Pull Requests* → **Allow squash merging → Default commit message =
"Pull request title"** — zonder die instelling pakt een squash van een
één-commit-PR de commit-subject i.p.v. de PR-titel → geen nummer op de
productie-deploy. (In AHQ staat dit al goed; check het hier even.)

## Getest

Docs + workflow-yaml; geen app-code geraakt.

## Open punten

Geen.
