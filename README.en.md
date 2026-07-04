🇩🇪 **[Deutsche Version](README.md)** | 🇬🇧 English version

# 🧠 Obsidian + Claude Code — Second Brain

A complete guide to connecting **Obsidian** and **Claude Code** into a personal
**Second Brain**: notes in Markdown, an AI assistant right inside your vault,
automatic tagging, templates, graph view, and Git backup.

This setup is based on a real, working system and is fully reproducible —
no API key, no cloud lock-in, everything runs locally.

> 📄 The detailed chapters in [`docs/`](docs/) are currently only available in German.
> This README gives you the full picture in English; use a translator for the deep-dive docs if needed.

## What is this?

- **Obsidian** is the note-taking app: local Markdown files, wikilinks, graph view, plugins.
- **Claude Code** is Anthropic's AI agent for the terminal — it can read files, write files, and run commands.
- **Claudian** is the Obsidian plugin that connects both: a Claude chat right inside Obsidian
  that knows your vault and can edit it. With the **"Claude Code"** provider it uses your
  existing Claude Code installation — **no API key needed**, your regular Claude subscription is enough.
- **obsidian-skills** teach Claude to produce clean Obsidian Markdown, Bases, Canvas, and more.

The result: you drop raw thoughts into `inbox/`, Claude distills them into knowledge notes,
links them, maintains daily notes and dashboards — and remembers durable context in `claude-memory/`.

## Prerequisites

| Component | Version (tested) | Note |
|-----------|-------------------|------|
| Linux | Ubuntu 24.04 / any distro with Flatpak | This guide is Linux-focused |
| Claude Code CLI | current | Claude subscription (Pro/Max) or API access |
| Obsidian | 1.12.7 (Flatpak, user install) | other installation methods work analogously |
| Claudian plugin | 2.0.25 | via Community Plugins |
| Node.js / npx | ≥ 18 | for `npx skills add` |
| Git | any | for vault backup (optional, recommended) |

## 🚀 Quickstart (5 steps)

### 1. Install Claude Code

```bash
# Guide + installer: https://claude.ai/code
curl -fsSL https://claude.ai/install.sh | bash
claude   # first start → log in with your Claude account
```

→ Details: [docs/01-claude-code-installation.md](docs/01-claude-code-installation.md) *(German)*

### 2. Install Obsidian and create the vault

```bash
flatpak install --user flathub md.obsidian.Obsidian
```

Copy the vault template from this repo:

```bash
cp -r vault-template/ ~/second-brain/
~/second-brain/start-obsidian.sh   # start Obsidian, open ~/second-brain as the vault
```

→ Details: [docs/02-obsidian-installation.md](docs/02-obsidian-installation.md) *(German)*

### 3. Install the Claudian plugin

In Obsidian: **Settings → Community Plugins → Browse → "Claudian"**, install and enable it.
Then, in the Claudian settings, set the provider to **"Claude Code"**
(find the CLI path with `which claude`).

→ Details: [docs/03-claudian-plugin.md](docs/03-claudian-plugin.md) *(German)*

### 4. Configure Claude

```bash
mkdir -p ~/.claude/commands
cp config-templates/claude/CLAUDE.md.template ~/.claude/CLAUDE.md      # then customize!
cp config-templates/claude/settings.json ~/.claude/settings.json
cp config-templates/claude/commands/brain-sync.md ~/.claude/commands/
```

→ Details: [docs/04-claude-konfiguration.md](docs/04-claude-konfiguration.md) *(German)*

### 5. Install the Obsidian skills

```bash
npx skills add obsidian-markdown obsidian-bases json-canvas obsidian-cli defuddle
```

→ Details: [docs/05-obsidian-skills.md](docs/05-obsidian-skills.md) *(German)*

**Done!** Open Obsidian, start the Claudian chat (right sidebar) and ask:
*"What's in my inbox?"*

## Vault structure

```
~/second-brain/
├── CLAUDE.md            # rules Claude follows while working in the vault
├── .gitignore           # protects secrets, sessions, workspace files
├── start-obsidian.sh    # Obsidian launcher (Flatpak)
├── inbox/               # new, unfiltered notes — everything lands here first
├── knowledge/           # durable, distilled knowledge
├── projects/            # project notes (with status in frontmatter)
├── daily/               # daily notes
├── dashboards/          # overviews (Dataview queries)
├── claude-memory/       # durable context for Claude (profile, projects, …)
└── templates/           # note templates (knowledge, project, daily)
```

The workflow: **inbox → knowledge/projects** (Claude helps distill),
`claude-memory/` keeps Claude's long-term memory curated and version-controlled.

→ Details: [docs/06-vault-struktur.md](docs/06-vault-struktur.md) *(German)*

## The 5 obsidian-skills

| Skill | What it does |
|-------|---------------|
| `obsidian-markdown` | Clean Obsidian Markdown: wikilinks, callouts, embeds, frontmatter |
| `obsidian-bases` | Create and query Obsidian Bases (database views) |
| `json-canvas` | Generate Canvas files (`.canvas`) — visual boards via chat |
| `obsidian-cli` | Control Obsidian from the CLI (open, search, manage notes) |
| `defuddle` | Extract web pages into clean Markdown — perfect for the inbox |

## Documentation

*(All chapter files below are currently written in German.)*

| Chapter | Content |
|---------|---------|
| [01 — Claude Code Installation](docs/01-claude-code-installation.md) | Install the CLI, log in, first run |
| [02 — Obsidian Installation](docs/02-obsidian-installation.md) | Flatpak install, create the vault |
| [03 — Claudian Plugin](docs/03-claudian-plugin.md) | Set up the plugin, "Claude Code" provider |
| [04 — Claude Configuration](docs/04-claude-konfiguration.md) | `~/.claude/CLAUDE.md` + `settings.json` explained |
| [05 — Obsidian Skills](docs/05-obsidian-skills.md) | Install and use all 5 skills |
| [06 — Vault Structure](docs/06-vault-struktur.md) | Folder concept, templates, graph colors |
| [07 — Git Backup](docs/07-git-backup.md) | Version and back up the vault |
| [08 — Troubleshooting](docs/08-troubleshooting.md) | Common problems and fixes |

## Security

- The included [`.gitignore`](vault-template/.gitignore) excludes `.env` files, keys,
  certificates, credentials, and Claudian sessions from the backup.
- All configuration templates in this repo contain **placeholders only**
  (`<YOUR_USERNAME>`, `<YOUR_TOKEN>`, `/home/<USER>` …) — replace them with your own values before use.
- Ground rule: **no credentials in notes or in `CLAUDE.md`** — always reference
  where the secret lives instead (e.g. `~/.git-credentials`).

## License

Personal use — feel free to fork and adapt it to your own setup.
