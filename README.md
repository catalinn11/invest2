# 📈 Planul Meu de Investiții — dashboard + notificări gratuite

Dashboard personal de investiții (XTB, 500 RON/lună) găzduit gratuit pe GitHub Pages,
cu prețuri live la fiecare deschidere și notificări push săptămânale pe telefon.

## Ce face

- **Evidența investițiilor** — adaugi fiecare cumpărare (dată, simbol, unități, sumă în RON); datele se salvează local în browser (localStorage) + export/import JSON pentru backup.
- **Prețuri live** — la fiecare deschidere, pagina ia prețurile curente de la Yahoo Finance și cursul valutar (RON) de la Frankfurter și îți arată valoarea portofoliului și profitul/pierderea.
- **Plan lunar** — bară de progres 0–500 RON pentru luna curentă + alocarea recomandată (75% ETF / 25% acțiuni).
- **Countdown GTA VI** — zile rămase până la 19 noiembrie 2026 (catalizator TTWO).
- **Notificări push săptămânale** — GitHub Actions rulează automat lunea, ia prețurile și îți trimite notificare pe telefon prin [ntfy.sh](https://ntfy.sh) — gratuit, fără server.

## Instalare (5 minute)

1. Creează un cont GitHub (dacă nu ai) și un repository nou, de ex. `investitii` (public).
2. Urcă fișierele din acest folder în repository (inclusiv folderul ascuns `.github`).
3. În repo: **Settings → Pages → Source: Deploy from a branch → main → / (root)** → Save.
4. După ~1 minut, site-ul e live la `https://<username>.github.io/investitii/`. Salvează-l pe ecranul telefonului (Add to Home Screen) — arată ca o aplicație.

## Notificări pe telefon

1. Instalează aplicația **ntfy** (Android / iOS, gratuită).
2. În `.github/workflows/weekly-alert.yml`, schimbă `NTFY_TOPIC` cu un nume secret ales de tine (ex. `investitii-catalin-93kd2`).
3. În aplicația ntfy, abonează-te la același topic.
4. În repo: tab **Actions** → activează workflows → poți testa manual cu **Run workflow**.

GitHub Actions rulează workflow-ul în fiecare luni la ~09:00 ora României și trimite: prețurile curente, variația săptămânală, zilele până la GTA VI și memento-ul de investiție lunară.

## Important

- Datele portofoliului stau **doar în browserul tău** (localStorage). Fă export JSON periodic ca backup; dacă schimbi telefonul/browserul, faci import.
- Simboluri Yahoo utile: `TTWO` (Take-Two, NASDAQ), `IWDA.AS` (iShares MSCI World, EUR), `VUAA.L` (Vanguard S&P 500 Acc, USD), `EUNL.DE`, `SXR8.DE`.
- Acesta este un instrument educațional de evidență, nu consultanță financiară.
