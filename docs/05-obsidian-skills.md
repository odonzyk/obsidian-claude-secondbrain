# 05 — Obsidian-Skills für Claude installieren

**Skills** sind Wissenspakete, die Claude Code beibringen, wie es bestimmte Aufgaben richtig
erledigt — hier: sauber mit Obsidian-Formaten umzugehen. Ohne die Skills schreibt Claude
zwar Markdown, aber nicht unbedingt *Obsidian*-Markdown (Wikilinks, Callouts, Bases, Canvas …).

## Installation

Alle fünf Skills mit einem Befehl (benötigt Node.js ≥ 18):

```bash
npx skills add obsidian-markdown obsidian-bases json-canvas obsidian-cli defuddle
```

Der Befehl installiert die Skills in dein Claude-Code-Setup. Prüfen kannst du das
in einer Claude-Session — die Skills erscheinen in der Skill-Liste, oder du fragst einfach:
*„Welche Obsidian-Skills hast du?"*

> 💡 Am besten im Vault-Verzeichnis (`cd ~/second-brain`) ausführen, dann liegen die
> Skills beim Vault-Projekt. Eine `skills-lock.json` im Vault-Root hält die Versionen fest.

## Die 5 Skills im Detail

### `obsidian-markdown`

Der wichtigste Skill: Obsidian-spezifisches Markdown korrekt erzeugen.

- Wikilinks `[[Notiz]]`, `[[Notiz|Alias]]`, `[[Notiz#Überschrift]]`
- Embeds `![[Bild.png]]`, Callouts `> [!note]`, `> [!warning]`
- YAML-Frontmatter (`date`, `tags`, Properties)
- Interne Link-Konventionen, die die Graph-Ansicht sauber halten

### `obsidian-bases`

Obsidian **Bases** — die eingebauten Datenbank-Ansichten (`.base`-Dateien).
Claude kann damit z. B. eine Projekt-Übersicht als filterbare Tabelle über alle
Notizen mit `status: aktiv` bauen.

### `json-canvas`

Erzeugt **Canvas-Dateien** (`.canvas`, JSON Canvas Format) — visuelle Boards mit Karten,
Gruppen und Verbindungen. Praktisch für Brainstorming: *„Mach mir ein Canvas aus den
Kernpunkten dieser Notiz."*

### `obsidian-cli`

Steuert Obsidian von der Kommandozeile: Notizen öffnen, suchen, erstellen.
Damit kann Claude z. B. nach einem Sync direkt die richtige Notiz in Obsidian aufmachen.

### `defuddle`

Extrahiert **Webseiten zu sauberem Markdown** (ohne Werbung, Navigation, Cookie-Banner).
Der perfekte Inbox-Zulieferer: *„Lies diesen Artikel und leg ihn als Wissensnotiz ab: <URL>"*

## Typische Workflows mit den Skills

| Aufgabe | Prompt-Beispiel |
|---------|-----------------|
| Artikel archivieren | „Hol dir <URL> mit defuddle und leg eine Wissensnotiz in knowledge/ an" |
| Inbox aufräumen | „Destilliere alle Notizen in inbox/ und sortiere sie ein — Vorschlag zuerst" |
| Projektübersicht | „Bau mir eine Base über alle Projekte mit Status und letzter Änderung" |
| Mindmap | „Erstelle ein Canvas zu [[Mein Thema]] mit den wichtigsten Unterpunkten" |

## Weiter

→ [06 — Vault-Struktur](06-vault-struktur.md)
