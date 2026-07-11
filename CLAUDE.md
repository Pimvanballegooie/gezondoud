# VindJeFysio Netwerk — gezondoud.net

Deze repo is één "spoke" in een hub-and-spoke netwerk van gespecialiseerde fysiotherapie-subsites. De hub is vindjefysio.net; spokes zijn o.a. rugnek, enkelvoet, beenklachten, kansrijkopgroeien, mentaalgezond, chronischezorg, armklachten, neuroklachten en deze (gezondoud).

## Architectuur
- Statische HTML/CSS/vanilla JS op GitHub Pages, custom domein via CNAME.
- Gedeelde Supabase-backend, project islujznszevdynguhjdc, met anon key in de frontend.
- Gedeelde tabellen: therapeuten, praktijken, therapeut_subcategorieen, therapeut_praktijken, subcategorieen, categorieen.
- Elke spoke deelt dezelfde structuur en bestanden: index.html, therapeut-aanmelden.html, mijn-profiel.html, therapeuten.html, privacy.html, protocollen.html (gegenereerd), sync_protocollen.py, .github/workflows/sync.yml, protocollen-config.json.

## Belangrijke conventies
- therapeut-aanmelden.html linkt ALTIJD relatief/lokaal binnen de eigen subsite (nooit naar vindjefysio.net).
- Praktijk/locatie-aanmelden loopt WEL centraal via vindjefysio.net/aanmelden.html?via=<domein>.
- Mails lopen via info@vindjefysio.net.
- Therapeut-registratie zet aangemeld_via op het eigen subsite-domein en actief=false (wacht op goedkeuring).
- Deze site: palet primair #3D8B6E (groen), light #EBF5EF, dark #2E6B54, navy #1F4A42, accent #E8A13A. Structuur = acht losse kaarten (géén netwerk-eis zoals het Lage Rugnetwerk bij rugnek), deels gebieden en deels thema's, categorie 2 "Ouderen" in Supabase: Kwetsbaarheid en mobiliteit (11), Valpreventie en balans (12), Dementie en bewegen (13), Herstel na ziekenhuisopname (14), Voorbereiding op operatie (15), Revalidatie na operatie (16), Sport, bewegen en overbelasting (17), Ouderen met levenslange beperking (18). Elk domein = precies 1 subcategorie, dus geen geneste chips-per-domein en geen domein+thema-combinatiefilter zoals in rugnek.

## Sync-pipeline
- sync_protocollen.py haalt protocollen op uit publiek gedeelde Google Docs (export-link, geen API-key), zet markdown om naar HTML, genereert protocollen/<id>-makkelijk.html (patiënt) en -complex.html (therapeut) + protocollen.html + sitemap.xml.
- De workflow git-add regel moet zijn: git add protocollen/ protocollen.html sitemap.xml (op één regel).
- Google Docs moeten op "iedereen met de link kan bekijken" staan.
- Zones: kwetsbaarheid, valpreventie, dementie, herstel-ziekenhuis, voorbereiding-operatie, revalidatie-operatie, sport-bewegen, levenslange-beperking (één op één met de acht kaarten, geen aparte thema-zone).
