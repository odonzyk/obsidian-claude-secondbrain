# 04 — Claude konfigurieren: CLAUDE.md und settings.json

Claude Code wird über Dateien im Verzeichnis `~/.claude/` gesteuert. Für das Second Brain
sind drei Dateien relevant — Templates liegen in `config-templates/claude/`.

## Überblick

| Datei | Zweck | Ins Git-Backup? |
|-------|-------|-----------------|
| `~/.claude/CLAUDE.md` | Globale Verhaltensregeln (jede Session) | ja |
| `~/.claude/settings.json` | Technische Einstellungen (Permissions, Effort) | ja |
| `~/.claude/settings.local.json` | **Secrets** (Env-Vars, Tokens) | **NEIN — niemals!** |
| `~/.claude/commands/*.md` | Eigene Slash-Commands | ja |

## 1. Globale CLAUDE.md

```bash
cp config-templates/claude/CLAUDE.md.template ~/.claude/CLAUDE.md
```

Danach **anpassen** — das Template enthält Platzhalter (`<YOUR_NAME>`, `<YOUR_USERNAME>`,
`/home/<USER>`, `git.<YOUR_GITEA_DOMAIN>` …). Die Abschnitte:

- **§1 Sprache** — Claude antwortet immer auf Deutsch (anpassbar)
- **§2 Dotfiles-Backup** — optional: Claude fragt nach Config-Änderungen, ob es sie ins Dotfiles-Repo committen soll
- **§3 Keine AI-Identität in Commits** — verhindert `Co-Authored-By: Claude` & Co.
- **§4 Read-only Commands** — welche harmlosen Befehle Claude ohne Nachfrage ausführen darf
- **§5 Private Infrastruktur** — NUR unkritische Infos; **niemals Tokens/Passwörter im Klartext**
- **§6 Second Brain** — sagt Claude, wo das Vault liegt und welche Memory-Dateien es bei Bedarf liest

> 💡 **Prinzip:** `~/.claude/CLAUDE.md` gilt global für jede Session. Die `CLAUDE.md`
> **im Vault** (aus `vault-template/`) gilt zusätzlich, sobald Claude im Vault arbeitet —
> auch über das Claudian-Plugin (Option „Load user settings").

## 2. settings.json

```bash
cp config-templates/claude/settings.json ~/.claude/settings.json
```

Das Template ist bewusst minimal:

```json
{
  "permissions": {
    "allow": ["Agent", "Task", "Bash(python3 -m json.tool)"],
    "defaultMode": "auto"
  },
  "effortLevel": "xhigh",
  "tui": "fullscreen"
}
```

| Option | Bedeutung |
|--------|-----------|
| `permissions.allow` | Tools/Kommandos, die nie eine Bestätigungs-Nachfrage auslösen |
| `permissions.defaultMode` | `auto` = Claude fragt nur bei potenziell riskanten Aktionen |
| `effortLevel` | Denk-Aufwand des Modells (`low` … `xhigh`) — für Wissensarbeit lohnt sich `xhigh` |
| `tui` | `fullscreen` = Terminal-UI im Vollbildmodus |

Weitere nützliche Optionen (bei Bedarf ergänzen): `model` (Standard-Modell festlegen),
`statusLine` (eigene Statuszeile), `enabledPlugins` (Claude-Code-Plugins/Skills-Marketplaces).

## 3. settings.local.json — nur für Secrets

```bash
cp config-templates/claude/settings.local.json.example ~/.claude/settings.local.json
```

Hier gehören Umgebungsvariablen mit echten Werten hinein (API-Tokens etc.):

```json
{
  "env": {
    "EXAMPLE_API_TOKEN": "<YOUR_TOKEN>"
  }
}
```

> ⚠️ Diese Datei enthält Klartext-Secrets. Sie gehört **niemals** in ein Git-Repo —
> auch nicht ins private Dotfiles-Backup, außer das Repo ist wirklich abgesichert.

## 4. Slash-Command /brain-sync

```bash
mkdir -p ~/.claude/commands
cp config-templates/claude/commands/brain-sync.md ~/.claude/commands/brain-sync.md
```

Danach steht in jeder Claude-Session `/brain-sync` zur Verfügung: Claude liest sein
Auto-Memory, gleicht es mit dem Vault ab, schlägt fehlende Notizen vor (propose-then-commit)
und committet/pusht das Vault. Im Template den Platzhalter `<PROJECT_SLUG>` ersetzen
(nachschauen mit `ls ~/.claude/projects/`).

## Weiter

→ [05 — Obsidian Skills](05-obsidian-skills.md)
