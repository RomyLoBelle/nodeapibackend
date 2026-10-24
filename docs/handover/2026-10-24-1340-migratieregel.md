# 24-10-2026 13:40 — Migratieregel Supabase-connector

Gemaakt door het coördinatie-gesprek (`session_01LWu1YE1imtvwJxBeiMM95Y`).

## Wat er veranderde

- `CLAUDE.md` → "Regels die ALTIJD gelden", regel 6: **Migraties en de Supabase-connector**.
  - Bij een `drop`, `delete` of `truncate` vraagt de connector om Romy's bevestiging. In een cloud-sessie komt die vraag nooit bij haar aan, en hij verloopt na 60 s.
  - Daarom: schrijf zonder die woorden, of lever een `.sql`-bestand voor de SQL Editor en controleer het daarna zelf.
- Dezelfde regel staat in AutomatingHQ (#1268) en RomyHQ (#813).

Geen code, geen env-vars, geen databasewijziging.

## Voor Romy

Niets te doen.
