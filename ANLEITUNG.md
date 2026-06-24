# Anleitung: Website selbst weiterentwickeln mit Claude Code

Liebe Friederike,

deine Website hat zwei „Eingänge" für Änderungen:

| Was möchtest du ändern? | Wo? |
|---|---|
| **Texte** (Headlines, Absätze, FAQ, Stimmen) | Tina CMS → https://friederikealtmann.de/admin/ |
| **Bilder** (austauschen, Bildausschnitt) | Tina CMS |
| **Kontakt-Daten, Navigation, Footer** | Tina CMS |
| **Design** (Farben, Abstände, Schriftgrößen) | Claude Code |
| **Neue Sektionen, neue Seiten, Layout** | Claude Code |
| **Funktionen** (z.B. neue Buttons, Slider) | Claude Code |

**Tina** ist der einfache Editor für deinen Alltag — Texte und Bilder ändern, ohne Code zu sehen.

**Claude Code** ist ein KI-Assistent, der direkt deinen Website-Code anpassen kann. Du sagst in normalem Deutsch was du willst („mach die Headline kleiner", „füge eine neue Sektion hinzu", „ändere die Hintergrundfarbe von X"), Claude Code schreibt den Code. Du musst kein Programmieren können.

---

## Voraussetzungen

Du brauchst:

1. **Einen Mac oder PC** (Linux geht auch)
2. **Einen GitHub-Account** (kostenlos) — dort liegt der Code deiner Website
3. **Einen Anthropic-Account** für Claude Code (kostenpflichtig — siehe https://claude.com/pricing)
4. **Claude Code installiert** auf deinem Rechner

---

## Setup (einmalig, ~30 Minuten)

### Schritt 1 — GitHub-Account einrichten

Falls du noch keinen hast:

1. Auf https://github.com gehen
2. **„Sign up"** → mit deiner Mail registrieren
3. E-Mail bestätigen
4. **Username** wählen (z.B. `friederikealtmann` oder Vorname-Nachname)

### Schritt 2 — Zugriff zum Repository

Dein Website-Code liegt unter: **https://github.com/friederikealtmann/friederike-altmann-website**

Lena muss dich als **Collaborator** oder **Owner** der Organisation `friederikealtmann` einladen. Sobald die Einladung in deiner GitHub-Inbox steht: akzeptieren.

### Schritt 3 — Claude Code installieren

1. Auf https://claude.com/code gehen
2. Den **Installer für dein Betriebssystem** (Mac oder Windows) herunterladen
3. Installieren (wie jede andere App)
4. App starten → mit deinem Anthropic-Account einloggen

### Schritt 4 — Repository auf deinen Rechner kopieren

Öffne **Claude Code** und sag ihm:

> „Klon das Repository `https://github.com/friederikealtmann/friederike-altmann-website` in meinen Documents-Ordner."

Claude Code macht das für dich. Beim ersten Mal fragt es nach deinem **GitHub-Login** — einmal eingeben und du wirst nicht wieder gefragt.

Alternativ über die GitHub Desktop App oder Terminal — aber Claude Code kann's einfach machen.

---

## Tägliche Nutzung

### Vorgehen für jede Änderung

1. **Claude Code öffnen** und das Projekt-Verzeichnis auswählen (z.B. `~/Documents/friederike-altmann-website`)
2. Im Chat **in normalem Deutsch** beschreiben was du willst
3. Claude Code macht die Änderung und zeigt dir das Ergebnis
4. Wenn's passt: bitte Claude Code es zu **„pushen"** (auf GitHub hochladen)
5. **2 Minuten warten** — automatischer Deploy aktualisiert die Website

### Beispiele für gute Prompts

> „Mach die Hero-Headline auf der Startseite 20% kleiner."

> „Füge auf der Methode-Seite eine neue Sektion am Ende ein mit der Überschrift „Häufige Fragen" und einer Liste von 3 Fragen."

> „Ändere die Farbe der Buttons von Safran zu einem dunkleren Gelb."

> „Auf Mobile soll die Navigation nicht mehr als Hamburger angezeigt werden, sondern direkt sichtbar bleiben."

> „Erstelle eine neue Seite `/workshops/` mit folgendem Inhalt: …"

### Tipps für die Zusammenarbeit mit Claude Code

- **Sei konkret**: „kleiner" → „20% kleiner" oder „auf 32px"
- **Sag wo**: „die Headline" → „die Hero-Headline auf der Startseite"
- **Vorschau anschauen**: Claude Code kann die Seite lokal bei dir öffnen bevor sie live geht
- **Bei Unsicherheit fragen**: „Was sind die Optionen für X?"
- **Schritt für Schritt**: Lieber eine Änderung pro Prompt als 10 auf einmal

---

## Wichtige Konzepte

### Was passiert bei einer Änderung?

```
Du sagst Claude Code was du willst
    ↓
Claude Code ändert Code auf deinem Rechner
    ↓
Claude Code „pusht" (lädt hoch) auf GitHub
    ↓
GitHub Actions startet automatisch
    ↓
Eleventy baut die Website neu
    ↓
Hochgeladen per SFTP auf Hetzner
    ↓
~2 Min später: live auf friederikealtmann.de
```

### Was wenn was kaputt geht?

Jede Änderung wird in GitHub gespeichert (als „Commit"). Du kannst jederzeit zu einer vorherigen Version zurück:

> „Mach den letzten Commit rückgängig."

Oder:

> „Stell die Version von gestern Mittag wieder her."

### Tina CMS vs. Claude Code — wann was?

| Szenario | Tool |
|---|---|
| „Ich will den Hero-Text ändern" | **Tina** (1 Klick) |
| „Ich brauche ein neues Testimonial" | **Tina** |
| „Das Bild soll oben rechts beschnitten sein" | **Tina** |
| „Die Headline soll größer/kleiner sein" | **Claude Code** |
| „Ich brauche eine ganz neue Sektion" | **Claude Code** |
| „Die Buttons sollen rund statt eckig sein" | **Claude Code** |
| „Auf Mobile soll X anders aussehen" | **Claude Code** |
| „Ich brauche eine neue Unterseite" | **Claude Code** |

---

## Hosting & Domain (zur Info)

- **Domain**: friederikealtmann.de
- **Hosting**: Hetzner Webhosting (über konsoleH verwaltbar: https://konsoleh.your-server.de)
- **Mail**: Google Workspace mit Adresse post@friederikealtmann.de
- **Kontaktformular**: FormSubmit — Mails landen direkt in post@friederikealtmann.de
- **CDN/SSL**: Let's Encrypt Cert wird automatisch von Hetzner erneuert

---

## Wenn du nicht weiterkommst

Claude Code selbst ist ein guter erster Anlaufpunkt — frag direkt im Chat:

> „Ich verstehe nicht warum X nicht funktioniert. Was muss ich tun?"

Wenn's komplizierter wird:
- **Lena** kennt das Projekt und kann reinschauen
- **Tina CMS Support**: https://tina.io/docs
- **Claude Code Docs**: https://docs.claude.com/en/docs/claude-code/overview

---

## Sicherheitshinweise

- **GitHub-Passwort** nie weitergeben. 2-Faktor-Authentifizierung aktivieren.
- **Anthropic API-Keys** nie in Tina oder im Code speichern. Claude Code regelt das selbst.
- **GitHub Secrets** (FTP-Passwort, Tina-Token, FormSubmit) sind verschlüsselt im Repo. Bitte nicht ändern ohne zu wissen was du tust.

---

Viel Erfolg und Spaß beim Weiterentwickeln!  
*Stand: Juni 2026*
