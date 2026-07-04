# 01 — Claude Code CLI installieren

Claude Code ist Anthropics KI-Agent fürs Terminal. Er ist die Grundlage des gesamten Setups:
Das Claudian-Plugin in Obsidian nutzt später **deine lokale Claude-Code-Installation** als
Provider — dadurch brauchst du keinen API-Key.

## Voraussetzungen

- Ein Claude-Konto mit **Pro- oder Max-Abo** (empfohlen) oder API-Zugang
- Linux, macOS oder Windows (diese Anleitung: Linux)

## Installation

Offizielle Seite: **https://claude.ai/code**

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

Der Installer legt die CLI typischerweise unter `~/.local/bin/claude` ab.
Prüfen:

```bash
which claude
claude --version
```

Falls `which claude` nichts findet: `~/.local/bin` muss im `PATH` sein —

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

> 📌 **Merke dir die Ausgabe von `which claude`** — den Pfad brauchst du später
> in den Claudian-Plugin-Einstellungen (Kapitel 03).

## Erster Start und Login

```bash
claude
```

Beim ersten Start öffnet sich der Login-Flow im Browser — mit dem Claude-Konto anmelden.
Danach ist die CLI einsatzbereit. Kurz testen:

```
> Sag Hallo auf Deutsch
```

## Nützliche Grundbefehle

| Befehl | Wirkung |
|--------|---------|
| `claude` | Interaktive Session im aktuellen Verzeichnis starten |
| `claude "Frage…"` | Einmalige Frage stellen |
| `/model` | Modell wechseln (in der Session) |
| `/login` | Neu einloggen |
| `/config` | Einstellungen anzeigen/ändern |

## Wichtig für das Second Brain

Claude Code lädt beim Start automatisch:

1. `~/.claude/CLAUDE.md` — deine **globalen Regeln** (Kapitel 04)
2. `CLAUDE.md` **im aktuellen Verzeichnis** — d. h. wenn du Claude im Vault
   (`~/second-brain/`) startest, kennt es automatisch deine Vault-Regeln

Genau dieses Verhalten nutzt das Second Brain: Die Regeln, wie Notizen strukturiert,
verlinkt und committet werden, stehen in `CLAUDE.md`-Dateien — nicht in Prompts.

## Weiter

→ [02 — Obsidian Installation](02-obsidian-installation.md)
