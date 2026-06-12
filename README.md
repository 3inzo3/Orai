# Orai 🌤

Orų palyginimo programėlė: rodo, kiek šiltesnis ar šaltesnis dabartinis oras, palyginti su praeitimi.

## Funkcijos

- **Laikotarpiai:** diena, savaitė (7 d.) arba mėnuo (30 d.)
- **Palyginimo režimai:**
  - su tuo pačiu laikotarpiu **pernai**
  - su paskutinių **5 metų vidurkiu**
  - su **pasirinktomis datomis** – dviem kalendoriaus laukeliais pasirenkate, kurią dieną su kuria lyginti
- **Temperatūros grafikas** – paros vidurkių kreivės (šiemet vs palyginamasis laikotarpis) savaitės ir mėnesio režimuose
- **Miestų valdymas** – pridėkite bet kurį pasaulio miestą per paiešką, pašalinkite nereikalingus (✕). Sąrašas išsaugomas naršyklėje
- Kritulių kiekio palyginimas, temperatūros skirtumo ženkliukas (šilčiau / šalčiau)

## Naudojimas

Tai vieno failo statinis puslapis – jokio diegimo nereikia:

- atidarykite `index.html` naršyklėje, arba
- įjunkite GitHub Pages šiai repozitorijai (Settings → Pages → branch `main`).

## Duomenys

[Open-Meteo](https://open-meteo.com) nemokami API (be rakto):

- `api.open-meteo.com/v1/forecast` – paskutinių ~3 mėn. duomenys
- `archive-api.open-meteo.com/v1/archive` – istoriniai duomenys
- `geocoding-api.open-meteo.com/v1/search` – miestų paieška
