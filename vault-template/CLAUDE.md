# Claude Code — Second Brain Vault

Dieses Verzeichnis ist dein persönliches Second Brain als Obsidian-Vault.

## Vault-Struktur

- `inbox/` — Neue, unfilterte Notizen
- `knowledge/` — Dauerhaftes Wissen
- `projects/` — Projektnotizen
- `daily/` — Tagesnotizen
- `dashboards/` — Übersichts-Notizen (z. B. Projekt-Dashboard mit Dataview)
- `claude-memory/` — Gedächtnisnotizen für Claude

## Konventionen

- Wikilinks verwenden: `[[Notizname]]`
- Tags: `#tag` in Notizen
- Frontmatter bei strukturierten Notizen:
  ```yaml
  ---
  date: YYYY-MM-DD
  tags: [tag1, tag2]
  ---
  ```

## Claude-Memory (immer lesen!)

Diese Dateien enthalten wichtigen Kontext über dich und deine Projekte.
**Bei jeder Session in diesem Vault diese Dateien zuerst lesen** (lege sie nach und nach an):

- [[claude-memory/00-Profil-und-Konventionen]] — Sprache, Git-Workflow, persönliche Konventionen
- [[claude-memory/01-Infrastruktur]] — Deine Rechner, Server, Dienste (nur unkritische Infos!)
- [[claude-memory/02-AI-Tools-und-Skills]] — AI-Tools, Skills-Cheatsheet
- [[claude-memory/03-Aktive-Projekte]] — Laufende Projekte
- [[claude-memory/04-Tech-Stack-und-Design]] — Bevorzugter Tech-Stack, Design-Prinzipien

## Auto-Memory ↔ Vault (Spiegelungs-Konvention)

Zwei getrennte Gedächtnis-Ebenen, bewusst **nicht** 1:1:

- **Auto-Memory** (`~/.claude/projects/<PROJECT_SLUG>/memory/`) — automatisch von Claude
  während der Session gepflegt, roh/vollständig, lädt selbst in jede Session.
- **Dieses Vault** — kuratiert, destilliert, **nur per Vorschlag** befüllt.

**Regel:** Am Ende **inhaltsreicher** Sessions schlägt Claude **aktiv** vor, relevante
Erkenntnisse hierher zu spiegeln — „Diese Punkte würde ich ins Second Brain übernehmen — ok?"
mit Liste + Zielordner. **Propose-then-commit, NIE ungefragt.** Kein Auto-Dump und kein
Hintergrund-Hook — Kuratierung braucht Urteil, der Mensch entscheidet.

## Templates

Templates für neue Notizen befinden sich in `templates/`:

- [[templates/Wissensnotiz]] — Für dauerhaftes Wissen
- [[templates/Projektnotiz]] — Für neue Projekte
- [[templates/Tagesnotiz]] — Für Daily Notes

In Obsidian: Settings → Core Plugins → Templates → Ordner: `templates`

## Sicherheit

- Dieses Vault ist rein lokal — kein Obsidian Sync, kein Publish
- Keine sensiblen Credentials in Notizen ablegen
- `.env`-Dateien gehören NICHT in dieses Vault

## Git Commit-Reminder (WICHTIG!)

**Mindestens einmal täglich nach Nutzung:**

- Am Ende jeder Session: „Soll ich die Änderungen im Second Brain committen?"
- Auch bei kleineren Änderungen (neue Notizen, Tag-Updates, Graph-Anpassungen)
- Immer vor längerer Pause (Ende des Arbeitstages)

**Automatisch committen bei:**

- Neuen Dateien in `knowledge/`, `projects/`, `claude-memory/`
- Änderungen an Dokumentations-Notizen
- Graph-Farb-Gruppen-Updates (`.obsidian/graph.json`)
- Memory-Dateien-Updates
