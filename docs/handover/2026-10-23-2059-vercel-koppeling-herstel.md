# Vercel rolde de backend sinds 22-06 niet meer uit (23-10-2026)

## Wat er aan de hand was

- De laatste uitrol van nodeapibackend in Vercel is commit `b220955` (#30, 22-06-2026).
  Daarna kwam er geen enkele uitrol meer, en Vercel reageerde niet meer op PR's
  (geen bot-reactie vanaf #31 op 28-06).
- Daardoor stond de lekreparatie #39 (open test- en debugroutes weg) wél op `main`,
  maar NIET live. De oude routes antwoordden nog zonder inlog.
- Oorzaak (zo goed als zeker): de Vercel-koppeling was gemaakt toen de repo nog op het
  persoonlijke account `RBlancoSaa` stond. Na de verhuizing naar de organisatie
  `RomyLoBelle` kwam er niets meer binnen bij Vercel. AutomatingHQ (zelfde Vercel-team)
  is wel aan `RomyLoBelle` gekoppeld en rolt gewoon uit.

## Wat er veranderde

- Romy heeft op 23-10 de GitHub-app van Vercel bij de organisatie `RomyLoBelle`
  nagekeken (All repositories). Dat alleen hielp niet: de eerste push op deze PR
  kreeg geen reactie van Vercel.
- Daarna in Vercel → nodeapibackend → Settings → Git: **Disconnect** en opnieuw
  **Connect** met het GitHub-account `RomyLoBelle` (niet `RBlancoSaa`).
- Dit bestand is de eerste wijziging daarna: de PR test of Vercel weer reageert
  (preview + bot-reactie), en de merge rolt `main` uit, inclusief #39.
- Geen code, geen database, geen env-vars.

## Controle na de uitrol

- GET `/api/inspect-pdf` op de productie-URL moet 404 geven (route bestaat niet meer).
- De echte routes (login, tenants, voorstellen, referentielijst) moeten blijven werken.

## Voor Romy

- Zet de externe cron uit die elke 5 minuten `/api/process-steinweg-queue` aanroept
  (dienst onbekend, bijv. cron-job.org). Na de uitrol krijgt hij een 404.
- Lukt de uitrol niet: in Vercel → nodeapibackend → Settings → Git eenmaal
  **Disconnect** en opnieuw **Connect** met de organisatie `RomyLoBelle`.
