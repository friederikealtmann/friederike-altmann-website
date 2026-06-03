# Friederike Altmann · Website

Static site built with **Eleventy 3** + **Tina CMS** (Tina Cloud).
Deployed on **Cloudflare Pages** (kostenlos).

**Domain** bei Hetzner registriert · DNS verweist auf Cloudflare Pages.

---

## Quick Setup (einmalig)

### 1. Lokale Dependencies installieren

```bash
npm install
```

### 2. Tina Cloud Account anlegen

1. Auf [app.tina.io](https://app.tina.io) registrieren (mit GitHub-Login)
2. **„New Project"** klicken
3. Repository **`lenapopenadesign/friederike-altmann-website`** auswählen
4. Branch: `main`
5. Tina generiert dann zwei Werte, die du brauchst:
   - `Client ID`
   - `Read-Only Token` (bzw. Read-Write Token)

### 3. Tina-Credentials hinterlegen

**Lokal:** `.env` Datei im Repo-Root anlegen (NICHT committen, ist gitignored):

```env
NEXT_PUBLIC_TINA_CLIENT_ID=<deine-client-id-von-tina>
TINA_TOKEN=<dein-token-von-tina>
```

**Auf Vercel:** Im Project-Settings → Environment Variables die gleichen zwei Variablen eintragen.

### 4. Local Dev starten

```bash
npm run dev
```

- Eleventy serviert die Seite auf `http://localhost:8080`
- Tina Admin UI ist erreichbar unter `http://localhost:8080/admin/index.html`
- Änderungen werden als Commits in deinem Git-Branch gespeichert

### 5. Production Build

```bash
npm run build
```

→ baut nach `_site/`. Lokales Vorschauen mit `npx serve _site` (separater Schritt).

**Cloudflare Pages** baut automatisch bei jedem Push auf `main` — kein lokaler Build nötig.

---

## Cloudflare Pages Deployment einrichten (einmalig)

### A. Cloudflare-Account anlegen (kostenlos)

1. [dash.cloudflare.com/sign-up](https://dash.cloudflare.com/sign-up) öffnen
2. Mit GitHub-Login registrieren (oder Email)
3. Account-Type: **Free**

### B. Pages-Projekt mit GitHub-Repo verbinden

1. Im Cloudflare Dashboard: **Workers & Pages** → **Create application** → **Pages** → **Connect to Git**
2. **GitHub Account verbinden** → den Account `lenapopenadesign` autorisieren
3. Repo wählen: `lenapopenadesign/friederike-altmann-website`
4. **Set up builds and deployments**:
   - Project name: `friederike-altmann` (wird Teil der URL: `friederike-altmann.pages.dev`)
   - Production branch: `main`
   - Framework preset: **None**
   - Build command: `npm run build`
   - Build output directory: `_site`
   - Root directory: (leer lassen)
   - Environment variables: (vorerst keine)
5. **Save and Deploy** — Cloudflare buildet das erste Mal (~1–2 Min)
6. URL erscheint: `https://friederike-altmann.pages.dev` → das ist die Live-URL

### C. Custom Domain (Friederikes echte Domain) verbinden

1. Im Pages-Projekt: **Custom domains** → **Set up a custom domain**
2. Domain eintippen: `friederikealtmann.de`
3. Cloudflare gibt dir DNS-Records, die du in **Hetzner DNS** eintragen musst:
   - Entweder einen **CNAME** auf `friederike-altmann.pages.dev` für `www`
   - UND für die Root-Domain (`friederikealtmann.de` ohne www) einen **A-Record** auf die Cloudflare-IP, die in der UI angezeigt wird

4. Im **Hetzner Cloud Console** (oder konsoleH falls Domain dort verwaltet wird):
   - **DNS** öffnen → die Domain bearbeiten → die Records hinzufügen
5. Cloudflare wartet auf DNS-Propagation (1–30 Min), dann **SSL-Zertifikat wird automatisch erzeugt**
6. Domain wird grün-tick in Cloudflare angezeigt → live

### D. Workflow danach

- Friederike editiert auf [app.tina.io](https://app.tina.io) → Tina committet auf GitHub
- Cloudflare Pages **detected den Push automatisch** → buildet → deployed → live in ~1–2 Min
- Du musst nichts manuell triggern

---

## Verzeichnis-Struktur

```
.
├── src/                      ← Eleventy Source
│   ├── index.njk             ← Landing (/)
│   ├── methode.njk           ← /methode/
│   ├── angebot.njk           ← /angebot/
│   ├── b2b.njk               ← /b2b/
│   ├── meine-geschichte.njk  ← /meine-geschichte/
│   ├── impressum.md          ← /impressum/ (Markdown body)
│   ├── datenschutz.md        ← /datenschutz/
│   ├── styles.css
│   ├── app.js
│   ├── assets/               ← Bilder, Logo, SVGs
│   ├── _includes/
│   │   ├── layouts/          ← base.njk, legal.njk
│   │   └── partials/         ← head, nav, footer, modal, cta-block
│   └── _data/                ← Globale Daten (von Tina editiert)
│       ├── site.json         ← Brand-Name, Kontaktdaten
│       ├── nav.json          ← Hauptnavigation
│       ├── footer.json       ← Footer-Links
│       ├── modal.json        ← Modal-Formular-Optionen
│       ├── testimonials.json ← Stimmen (Slider auto >3)
│       ├── faq.json          ← FAQ-Liste
│       └── topics.json       ← Themen-Tags
├── content/                  ← (optional, falls weitere Collections nötig)
├── tina/
│   └── config.ts             ← Tina-Schema
├── eleventy.config.js        ← Eleventy-Konfig
├── package.json
├── vercel.json               ← Build = npm run build, Output = _site
└── brand-kit/                ← Source Material (excluded from deploy)
```

---

## Was Tina aktuell editieren kann

Nach Login auf Tina Cloud sieht Friederike folgende Collections:

| Collection         | Was editierbar ist                                            |
|--------------------|--------------------------------------------------------------|
| **Site Settings**  | Brand-Name, Untertitel, CTA-Label, alle Kontaktdaten          |
| **Stimmen**        | Testimonial-Liste (Zitat / Name / Rolle) — beliebig viele    |
| **FAQ**            | Fragen + Antworten — beliebig viele                          |
| **Themen-Tags**    | Tag-Liste auf der Landing                                     |
| **Navigation**     | Label + URL pro Nav-Punkt                                     |
| **Footer**         | Label + URL pro Footer-Link                                   |
| **Seiten**         | Impressum + Datenschutz (Titel + Markdown-Body)               |

### Was noch HTML/Template ist (nicht via Tina editierbar)

Die Inhalte der komplexen Seiten (Methode-Sections, B2B-Hero, Angebot-Karten,
Über-mich-Story-Sections etc.) stehen aktuell als HTML in den `.njk`-Templates.

Falls du auch diese editierbar machen willst, können wir das schrittweise machen:
1. Inhalte aus dem Template ins YAML-Frontmatter ziehen
2. Tina-Schema dafür erweitern
3. Template ersetzt feste Strings durch `{{ frontmatter-variable }}`

---

## Standard-Workflow für Friederike

1. **Editieren:** [app.tina.io](https://app.tina.io) → Projekt → Collection → Änderungen
2. **Speichern:** Tina committet automatisch in den `main`-Branch (oder erstellt PR)
3. **Deploy:** Vercel pickt den Push auf und deployed in ~30 Sek

Sie braucht weder Git-Knowledge noch Code-Editor — alles läuft über die Tina-UI.

---

## Troubleshooting

**Build schlägt fehl mit "Missing TINA_TOKEN":**
→ Tina-Credentials auf Vercel als Environment Variables setzen (siehe oben).

**Lokaler `npm run dev` zeigt nichts:**
→ Erst `npm install`, dann `.env` mit Tina-Creds füllen.

**Eleventy-Build OK, aber Tina UI zeigt "Cannot connect":**
→ Tina Cloud Branch-Setting muss zum aktuellen Branch passen (`main`).

**Cloudflare Build schlägt fehl:**
→ Im Pages-Dashboard → letzter Deploy → **View build log** → meist sieht man den Fehler.
   Häufig: falsches Build-Command oder Node-Version. Build-Settings prüfen.

**Domain zeigt „Page not found":**
→ DNS-Records in Hetzner prüfen — müssen genau auf den von Cloudflare angegebenen
   Wert zeigen. DNS-Propagation kann bis zu 30 Min dauern.

**Tina commits triggern keinen Build:**
→ In Cloudflare Pages-Settings: **Production branch** muss `main` sein (oder
   der Branch, in den Tina committet).

**Alte Vercel-Deployments noch aktiv:**
→ Im Vercel-Dashboard kannst du das Project löschen — Cloudflare Pages übernimmt
   den Deploy jetzt vollständig.
