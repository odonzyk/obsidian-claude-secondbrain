# 🧠 Obsidian + Claude Code — Second Brain

Eine vollständige deutsche Anleitung, um **Obsidian** und **Claude Code** zu einem
persönlichen **Second Brain** zu verbinden: Notizen in Markdown, ein KI-Assistent
direkt im Vault, automatische Verschlagwortung, Templates, Graph-Ansicht und Git-Backup.

Das Setup basiert auf einem real funktionierenden System und ist komplett nachbaubar —
ohne API-Key, ohne Cloud-Zwang, alles lokal.

## Was ist das?

- **Obsidian** ist die Notiz-App: lokale Markdown-Dateien, Wikilinks, Graph-Ansicht, Plugins.
- **Claude Code** ist Anthropics KI-Agent fürs Terminal — er kann Dateien lesen, schreiben und Kommandos ausführen.
- **Claudian** ist das Obsidian-Plugin, das beide verbindet: ein Claude-Chat direkt in Obsidian,
  der dein Vault kennt und bearbeiten kann. Mit dem Provider **„Claude Code"** nutzt es deine
  bestehende Claude-Code-Installation — **kein API-Key nötig**, dein normales Claude-Abo reicht.
- **obsidian-skills** bringen Claude bei, sauberes Obsidian-Markdown, Bases, Canvas & Co. zu erzeugen.

Das Ergebnis: Du wirfst rohe Gedanken in die `inbox/`, Claude destilliert sie zu Wissensnotizen,
verlinkt sie, pflegt Tagesnotizen und Dashboards — und merkt sich dauerhaften Kontext in `claude-memory/`.

## Voraussetzungen

| Komponente | Version (getestet) | Hinweis |
|------------|--------------------|---------|
| Linux | Ubuntu 24.04 / jede Distro mit Flatpak | Anleitung ist Linux-fokussiert |
| Claude Code CLI | aktuell | Claude-Abo (Pro/Max) oder API-Zugang |
| Obsidian | 1.12.7 (Flatpak, User-Install) | andere Installationswege funktionieren analog |
| Claudian Plugin | 2.0.25 | über Community Plugins |
| Node.js / npx | ≥ 18 | für `npx skills add` |
| Git | beliebig | für das Vault-Backup (optional, empfohlen) |

## 🚀 Schnellstart (5 Schritte)

### 1. Claude Code installieren

```bash
# Anleitung + Installer: https://claude.ai/code
curl -fsSL https://claude.ai/install.sh | bash
claude   # erster Start → Login mit deinem Claude-Konto
```

→ Details: [docs/01-claude-code-installation.md](docs/01-claude-code-installation.md)

### 2. Obsidian installieren und Vault anlegen

```bash
flatpak install --user flathub md.obsidian.Obsidian
```

Vault-Vorlage aus diesem Repo übernehmen:

```bash
cp -r vault-template/ ~/second-brain/
~/second-brain/start-obsidian.sh   # Obsidian starten, ~/second-brain als Vault öffnen
```

→ Details: [docs/02-obsidian-installation.md](docs/02-obsidian-installation.md)

### 3. Claudian-Plugin installieren

In Obsidian: **Settings → Community Plugins → Browse → „Claudian"** installieren und aktivieren.
Dann in den Claudian-Einstellungen den Provider auf **„Claude Code"** stellen
(CLI-Pfad herausfinden mit `which claude`).

→ Details: [docs/03-claudian-plugin.md](docs/03-claudian-plugin.md)

### 4. Claude konfigurieren

```bash
mkdir -p ~/.claude/commands
cp config-templates/claude/CLAUDE.md.template ~/.claude/CLAUDE.md      # dann anpassen!
cp config-templates/claude/settings.json ~/.claude/settings.json
cp config-templates/claude/commands/brain-sync.md ~/.claude/commands/
```

→ Details: [docs/04-claude-konfiguration.md](docs/04-claude-konfiguration.md)

### 5. Obsidian-Skills installieren

```bash
npx skills add obsidian-markdown obsidian-bases json-canvas obsidian-cli defuddle
```

→ Details: [docs/05-obsidian-skills.md](docs/05-obsidian-skills.md)

**Fertig!** Öffne Obsidian, starte den Claudian-Chat (rechte Seitenleiste) und frage:
*„Was steht in meiner Inbox?"*

## Vault-Struktur

```
~/second-brain/
├── CLAUDE.md            # Regeln, nach denen Claude im Vault arbeitet
├── .gitignore           # schützt Secrets, Sessions, Workspace-Dateien
├── start-obsidian.sh    # Obsidian-Starter (Flatpak)
├── inbox/               # Neue, unfilterte Notizen — hier landet alles zuerst
├── knowledge/           # Dauerhaftes, destilliertes Wissen
├── projects/            # Projektnotizen (mit Status im Frontmatter)
├── daily/               # Tagesnotizen
├── dashboards/          # Übersichten (Dataview-Queries)
├── claude-memory/       # Dauerhafter Kontext für Claude (Profil, Projekte, …)
└── templates/           # Notiz-Vorlagen (Wissen, Projekt, Tagesnotiz)
```

Der Workflow: **inbox → knowledge/projects** (Claude hilft beim Destillieren),
`claude-memory/` hält Claudes Langzeitgedächtnis kuratiert und versionierbar.

→ Details: [docs/06-vault-struktur.md](docs/06-vault-struktur.md)

## Die 5 obsidian-skills

| Skill | Was er kann |
|-------|-------------|
| `obsidian-markdown` | Sauberes Obsidian-Markdown: Wikilinks, Callouts, Embeds, Frontmatter |
| `obsidian-bases` | Obsidian Bases (Datenbank-Ansichten) erstellen und abfragen |
| `json-canvas` | Canvas-Dateien (`.canvas`) erzeugen — visuelle Boards per Chat |
| `obsidian-cli` | Obsidian per CLI steuern (Notizen öffnen, suchen, verwalten) |
| `defuddle` | Webseiten zu sauberem Markdown extrahieren — perfekt für die Inbox |

## Dokumentation

| Kapitel | Inhalt |
|---------|--------|
| [01 — Claude Code Installation](docs/01-claude-code-installation.md) | CLI installieren, Login, erster Start |
| [02 — Obsidian Installation](docs/02-obsidian-installation.md) | Flatpak-Install, Vault anlegen |
| [03 — Claudian Plugin](docs/03-claudian-plugin.md) | Plugin einrichten, Provider „Claude Code" |
| [04 — Claude Konfiguration](docs/04-claude-konfiguration.md) | `~/.claude/CLAUDE.md` + `settings.json` erklärt |
| [05 — Obsidian Skills](docs/05-obsidian-skills.md) | Alle 5 Skills installieren und nutzen |
| [06 — Vault-Struktur](docs/06-vault-struktur.md) | Ordner-Konzept, Templates, Graph-Farben |
| [07 — Git-Backup](docs/07-git-backup.md) | Vault versionieren und sichern |
| [08 — Troubleshooting](docs/08-troubleshooting.md) | Häufige Probleme und Lösungen |

## Sicherheit

- Die mitgelieferte [`.gitignore`](vault-template/.gitignore) schließt `.env`-Dateien, Keys,
  Zertifikate, Credentials und Claudian-Sessions vom Backup aus.
- Alle Konfigurations-Templates in diesem Repo enthalten **ausschließlich Platzhalter**
  (`<YOUR_USERNAME>`, `<YOUR_TOKEN>`, `/home/<USER>` …) — vor der Nutzung durch eigene Werte ersetzen.
- Grundregel: **Keine Credentials in Notizen oder in `CLAUDE.md`** — immer nur auf
  Speicherorte verweisen (z. B. `~/.git-credentials`).

## Lizenz

Private Nutzung — gerne forken und an das eigene Setup anpassen.
