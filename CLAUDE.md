# Orai: dabar vs pernai

## Kas tai

Vieno failo (`index.html`) orų palyginimo programėlė lietuvių kalba. Talpinama
per GitHub Pages (3inzo3.github.io), savininkas naudoja iPhone per „Add to
Home Screen“. **Pagrindinis tikslas — padėti analizuoti energijos vartojimą
pagal orus**, todėl visi palyginimai daromi lygiuojant savaitės dienas
(pirmadienis su pirmadieniu), ne kalendorines datas.

## Architektūra

- Grynas HTML/CSS/JS viename `index.html`, jokių bibliotekų ir build žingsnio.
- Duomenys: **Open-Meteo** (`api.open-meteo.com/v1/forecast` paskutinėms ~92 d.
  ir prognozei iki 16 d.; `archive-api.open-meteo.com` senesnėms datoms nuo
  1940 m., vėluoja ~5 d.). Užklausos kešuojamos `cache` (pagal URL) ir
  `dayCache` (miestas+data) objektuose sesijos ribose.
- Miestai: Vilnius, Klaipėda, Šiauliai, Ryga (`CITIES` masyvas).
- Tabai (`period`): `day`, `week`, `month`, `custom` (su `subMode`
  single/range), `year`.

## Svarbiausi sprendimai (nekeisti be priežasties)

- **Lygiavimas pagal ISO savaites**: „Diena“ = šiandien vs ta pati ISO savaitė
  ir savaitės diena pernai (`isoAlign()`); „Savaitė“ = einanti ISO savaitė nuo
  pirmadienio iki šiandien vs ta pati savaitė pernai; „Mėnuo“ = mėnuo nuo 1 d.
  iki šiandien vs pernai tas pats rėžis.
- **Šiandienos valandos** rodomos tik iki paskutinės sveikos valandos
  (22:32 → iki 22:00), be prognozės likusiai dienai.
- **Spalvos**: geltona (`--now`) = šis periodas, mėlyna (`--past`) =
  lyginamasis. Galioja visur: legendoje, juostose, krituliuose, grafiko
  linijose/stulpeliuose, kalendoriaus metuose.
- **Trumpos datos** kortelių žymose: `26-06-12` (pilna `2026-06-12` netelpa
  64px stulpelyje); pilnos datos antraštėje/legendoje.
- Krituliai: suma mm + paros vidurkis `(x.x/d.)` daugiadieniams periodams.
- „Metai“ tabas: 24 mėnesiai dviem stulpeliais — kairėje pernai, dešinėje
  šiemet; LT/LV šventės (kilnojamos skaičiuojamos: `easter()`, `nthSunday()`),
  ISO savaičių numeriai.
- Atnaujinimas: ⟳ mygtukas valo kešus; `visibilitychange`/`pageshow` atnaujina
  jei duomenys >30 min (iOS užšaldyto vaizdo problema).
- **meteo.lt buvo įdiegtas ir išimtas** (commit `a1633e4`) — savininkas norės
  testinio meteo.lt vs Open-Meteo palyginimo ateityje. Neaišku, ar
  api.meteo.lt leidžia CORS iš naršyklės — netikrinta.

## Darbo eiga

- Šaka: `pirmas-koregavimas` → PR į `main` (savininkas suliejimą daro pats,
  greitai). PR aprašymai ir commit žinutės — **lietuviškai**.
- Savininkas bendrauja lietuviškai, dažnai siunčia ekrano nuotraukas su
  pastabomis — žiūrėti atidžiai, jose būna ranka pažymėtos vietos.
- Prieš commit: ištraukti `<script>` bloką ir tikrinti `node --check`,
  logiką testuoti node skriptais su `TZ=Europe/Vilnius`.
- CSS pastaba: yra globali `[hidden]{display:none!important}` taisyklė, nes
  `display:flex` klasės kitaip nugali `hidden` atributą.

## Galimi ateities darbai (aptarta, nepadaryta)

- meteo.lt vs Open-Meteo testinis palyginimo puslapis.
- PWA: manifest.json + service worker (offline, tikra ikona).
- Slankiojantis tabo indikatorius, skeleton loaders, šviesi tema,
  localStorage duomenų kešas greitam atidarymui.
