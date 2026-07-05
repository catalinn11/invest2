# orbit. — planul meu de investiții

Dashboard personal de investiții (XTB, 500 RON/lună, strategie 80% ETF / 20% acțiuni),
găzduit gratuit pe GitHub Pages, cu bază de date cloud, prețuri live și notificări push săptămânale.

## Ce face

- **Inelul lunii** — arcul albastru (nucleu ETF, 400 RON) și cel auriu (satelit acțiuni, 100 RON) se umplu pe măsură ce investești luna curentă.
- **Evidența investițiilor** — fiecare cumpărare cu dată, simbol, unități, sumă; valoare de piață și profit/pierdere live (Yahoo Finance + curs RON de la Frankfurter).
- **Bază de date cloud (opțional, recomandat)** — Firebase Firestore: aceleași date pe telefon și calculator, nu mai depinzi de localStorage.
- **Notificări push săptămânale** — GitHub Actions + ntfy.sh îți trimit lunea recomandarea: ~100 RON ETF + ~25 RON TTWO, cu prețuri și context.
- **Countdown GTA VI** — 19 noiembrie 2026, catalizatorul TTWO.

## 1. Publicare pe GitHub Pages (5 min)

1. Creează un cont GitHub și un repository public, ex. `investitii`.
2. Urcă toate fișierele din acest folder (inclusiv folderul ascuns `.github`).
3. Repo → **Settings → Pages → Source: Deploy from a branch → main → / (root)** → Save.
4. Site-ul e live la `https://<username>.github.io/investitii/`. Pe telefon: deschide-l și **Add to Home Screen** — arată ca o aplicație.

## 2. Baza de date — Firebase Firestore (5 min, o singură dată)

1. Mergi la [console.firebase.google.com](https://console.firebase.google.com) → **Add project** (nume oricare, Analytics poate rămâne oprit).
2. În proiect: **Build → Firestore Database → Create database → Start in production mode** → alege regiunea `europe-west`.
3. Tab **Rules**, înlocuiește cu regulile de mai jos și apasă Publish:
   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /portfolios/{id} {
         allow read, write: if true;
       }
     }
   }
   ```
   (Oricine ar ști codul tău de sincronizare ar putea citi datele — folosește un cod lung și greu de ghicit, ca o parolă. Nu pune date sensibile, sunt doar tranzacțiile tale.)
4. **Project settings (rotița) → General → Your apps → </> (Web)** → înregistrează aplicația → copiază obiectul `firebaseConfig`.
5. Deschide `index.html`, caută `const FIREBASE_CONFIG = null;` și înlocuiește cu config-ul tău:
   ```js
   const FIREBASE_CONFIG = {
     apiKey: "AIza…",
     authDomain: "proiectul-tau.firebaseapp.com",
     projectId: "proiectul-tau"
   };
   ```
6. Urcă `index.html` actualizat pe GitHub. În aplicație: **☁️ Sincronizare cloud** → alege un cod secret (ex. `catalin-orbit-93kd2`) → Conectează. Introdu același cod pe telefon și pe calculator — datele se sincronizează automat (badge-ul verde din colț confirmă).

## 3. Notificări pe telefon (5 min)

1. Instalează aplicația **ntfy** (Android/iOS, gratuită).
2. În `.github/workflows/weekly-alert.yml` schimbă `NTFY_TOPIC` cu un nume secret ales de tine.
3. În aplicația ntfy abonează-te la același topic.
4. Repo → tab **Actions** → activează workflows → testează cu **Run workflow**.

În fiecare luni (~09:00 ora României) primești push: recomandarea săptămânii (80/20), prețurile, variația și zilele până la GTA VI.

## Simboluri utile (Yahoo)

`TTWO` · `IWDA.AS` (iShares MSCI World, EUR) · `VUAA.L` (Vanguard S&P 500 Acc) · `VWCE.DE` (Vanguard All-World) · `EUNL.DE` · `SXR8.DE`

## Important

Instrument educațional de evidență, nu consultanță financiară. Fă export JSON periodic ca backup suplimentar.
