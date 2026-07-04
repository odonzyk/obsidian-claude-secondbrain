# 08 — Troubleshooting

Häufige Probleme beim Setup und ihre Lösungen.

## Claudian findet die Claude-CLI nicht

**Symptom:** Chat startet nicht, Fehler wie „claude binary not found" / Spawn-Error.

**Ursache:** Obsidian läuft (besonders als Flatpak) in einer Sandbox mit eigenem `PATH`.

**Lösung:**

1. Pfad ermitteln: `which claude` → z. B. `/home/<USER>/.local/bin/claude`
2. In den Claudian-Settings den **absoluten CLI-Pfad** eintragen (nicht auf `PATH` verlassen)
3. Obsidian neu starten

Falls es weiter hakt (Flatpak-Sandbox blockiert das Binary):

```bash
flatpak override --user --filesystem=~/.local/bin:ro md.obsidian.Obsidian
```

## „Restricted Mode" verhindert Plugin-Installation

**Symptom:** Community Plugins lassen sich nicht durchsuchen/aktivieren.

**Lösung:** Settings → **Community Plugins** → „Turn on community plugins"
(= Restricted Mode ausschalten). Das ist Voraussetzung für Claudian und Dataview.

## Claude kennt die Vault-Regeln nicht

**Symptom:** Claude ignoriert Ordner-Konventionen, legt Notizen falsch ab.

**Checkliste:**

1. Liegt `CLAUDE.md` im **Vault-Root** (`~/second-brain/CLAUDE.md`)?
2. In Claudian: Option **„Load user settings"** aktiviert?
3. Bei CLI-Nutzung: Claude **im Vault-Verzeichnis** gestartet (`cd ~/second-brain && claude`)?

## `npx skills add` schlägt fehl

**Symptom:** Fehler bei der Skill-Installation.

**Checkliste:**

1. Node-Version prüfen: `node --version` → sollte ≥ 18 sein
2. Hinter Proxy/Firewall: npm-Registry erreichbar? (`npm ping`)
3. Einzeln installieren, um den Verursacher zu finden:
   `npx skills add obsidian-markdown` usw.

## Obsidian (Flatpak) sieht das Vault-Verzeichnis nicht

**Symptom:** „Open folder as vault" zeigt den Ordner nicht bzw. Zugriff verweigert.

**Lösung:** Flatpak-Dateizugriff erweitern:

```bash
flatpak override --user --filesystem=home md.obsidian.Obsidian
```

(oder gezielt `--filesystem=<pfad>`; grafisch geht das mit **Flatseal**.)

## Claudes Login ist abgelaufen

**Symptom:** Claudian-Chat bricht mit Auth-Fehler ab.

**Lösung:** Im Terminal neu einloggen — Claudian nutzt dieselbe Anmeldung:

```bash
claude
> /login
```

## Git-Push schlägt fehl (Vault-Backup)

**Checkliste:**

1. Remote korrekt? `git remote -v`
2. SSH-Key hinterlegt? `ssh -T git@github.com` → „Hi <YOUR_USERNAME>!"
3. Bei HTTPS + Token: Token abgelaufen? Scopes korrekt (`repo`)?

## Merge-Konflikte in `.obsidian/`

**Symptom:** Bei Sync zwischen zwei Rechnern kollidiert `workspace.json` o. Ä.

**Lösung:** Diese Dateien gehören nicht ins Repo — die mitgelieferte `.gitignore`
schließt sie aus. Falls sie schon getrackt sind:

```bash
git rm -r --cached .obsidian/workspace.json
git commit -m "chore: workspace state aus dem Tracking entfernen"
```

## Performance: Vault wird träge

- Graph-Ansicht: Filter nutzen (`showOrphans: false`, `hideUnresolved: true` — im Template gesetzt)
- Sehr große Anhänge (Videos, PDFs) besser außerhalb des Vaults lagern oder
  einen dedizierten `attachments/`-Ordner von Dataview-Queries ausnehmen

---

**Weitere Hilfe:** Claude Code Doku unter https://code.claude.com/docs •
Claudian-Repo auf GitHub (Issues) • Obsidian-Forum https://forum.obsidian.md
