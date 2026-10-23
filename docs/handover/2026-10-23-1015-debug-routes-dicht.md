# Open test- en debugroutes weg (PR #39)

## Wat er openstond

Uit de securityscan van 23-10-2026 (RomyHQ, AHQ en nodeapibackend). Zonder
inlog bereikbaar op `nodeapibackend.vercel.app`:

- `GET /api/test-send-email?to=<adres>`: verstuurde mail vanuit de Gmail van
  Tiaro naar elk adres, en liet zien welke env-vars er zijn en welke scopes het
  token heeft. Bij de controle op 23-10 is per ongeluk één testmail naar het
  vaste adres `RECIPIENT_EMAIL` (easybestanden@tiarotransport.nl) gegaan.
- `GET /api/upload-from-inbox`: las de Tiaro-inbox leeg en markeerde mails als
  gelezen. De mailverwerking zit sinds 15-05-2026 in de AHQ-harvester, die
  gelezen mails overslaat.
- `GET /api/inspect-pdf?file=…`: gaf transportopdrachten uit de bucket terug.
- `test-gmail-auth`, `test-steinweg`, `process-steinweg-queue` en
  `generate-easy-files` (die laatste had ook een niet-gedefinieerde variabele).

## Wat er veranderde

`index.js`: de routes en imports zijn weg. De handler-bestanden staan nog in
`api/`, maar zijn niet meer bereikbaar (Vercel stuurt alles naar `index.js`).

Gecontroleerd: RomyHQ en AHQ roepen geen van deze routes aan. Alleen
`/api/verwerk-pdf-upload` (de dropbox) wordt gebruikt, en die blijft.
`node --check index.js` is groen.

Geen DB-migraties, geen env-wijzigingen. Akkoord van Romy: *"ja ga maar live
met alles"*.

## Open punten

- De bucket `referentielijsten` is publiek en bevat ook factuur- en
  ritarchieven, het adresboek en klantgegevens. Privé maken raakt lezers in
  RomyHQ en AHQ; eerst die lezers op een signed URL zetten.
- `npm audit`: 13 kwetsbaarheden (1 kritiek, 9 hoog), o.a. `xlsx`, `adm-zip`,
  `nodemailer`.
- `node_modules/` (3.716 bestanden) staat in git.
- CLAUDE.md is verouderd (Gmail-flow staat uit sinds 15-05; KWE, Easyfresh en
  DFDS-body bestaan wel).
- Afbouwplan: nodeapi laten opgaan in AHQ (zie het plan van 23-10).
