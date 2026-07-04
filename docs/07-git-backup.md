# 07 — Git-Backup des Vaults

Das Vault sind nur Textdateien — Git ist das perfekte Backup: Versionshistorie für jede
Notiz, Sync zwischen Rechnern, und Claude kann committen/pushen gleich mit erledigen.

## Repo initialisieren

```bash
cd ~/second-brain
git init -b main
git add -A
git commit -m "init: Second Brain Vault"
```

Die mitgelieferte `.gitignore` ist dabei entscheidend — sie schließt aus:

| Muster | Warum |
|--------|-------|
| `.obsidian/workspace.json`, Caches | ständig wechselnder UI-Zustand — nur Merge-Konflikte |
| `.obsidian/plugins/*/data.json` | Plugin-Session-State (z. B. offene Claudian-Tabs) |
| `.claudian/sessions/` | Chat-Verläufe — können private Inhalte enthalten |
| `.env`, `*.key`, `*.pem`, `*.crt`, `*.p12` | Secrets und Zertifikate |
| `*credentials*`, `*token*`, `*password*`, `*secret*` | Sicherheitsnetz gegen versehentlich abgelegte Secrets |
| `.claude/`, `.agents/`, `.trash/` | lokale Arbeitsverzeichnisse |

## Remote einrichten — Hosting-Optionen

Ein **privates** Repo ist Pflicht — im Vault steht dein Leben.

### Option A: GitHub (einfachster Weg)

```bash
# Privates Repo auf https://github.com/new anlegen (ohne README), dann:
git remote add origin git@github.com:<YOUR_USERNAME>/second-brain.git
git push -u origin main
```

### Option B: Selbst gehostetes Gitea/Forgejo

Volle Datenhoheit — das Vault verlässt dein Netz nie:

```bash
git remote add origin https://<YOUR_USERNAME>:<YOUR_TOKEN>@git.<YOUR_GITEA_DOMAIN>/<YOUR_USERNAME>/second-brain.git
git push -u origin main
```

> 💡 Token nicht in der Remote-URL lassen? Besser: `git config credential.helper store`
> und den Token einmalig eingeben — er landet dann in `~/.git-credentials` (außerhalb des Vaults).

### Option C: Nur lokal / anderes Medium

Auch ohne Remote lohnt sich Git (Historie!). Backup dann z. B. per `rsync`/Syncthing
auf ein NAS — aber `.git/` mitsichern.

## Claude committet für dich

Die Vault-`CLAUDE.md` enthält einen **Commit-Reminder**: Claude fragt am Ende jeder
Session, ob es die Änderungen committen soll, und committet Neues in `knowledge/`,
`projects/` und `claude-memory/` selbstständig (nach Bestätigung).

Zusätzlich gibt es den Slash-Command **`/brain-sync`** (Kapitel 04): Auto-Memory
abgleichen → fehlende Notizen vorschlagen → committen → pushen, alles in einem Schritt.

## Sicherheits-Checkliste vor dem ersten Push

- [ ] `git status` — tauchen `.env`, Keys oder `sessions/` auf? → `.gitignore` prüfen
- [ ] `grep -ri "password\|token\|secret" ~/second-brain --include="*.md" | grep -v template` — Treffer prüfen
- [ ] Repo-Sichtbarkeit auf **privat** gestellt?

## Weiter

→ [08 — Troubleshooting](08-troubleshooting.md)
