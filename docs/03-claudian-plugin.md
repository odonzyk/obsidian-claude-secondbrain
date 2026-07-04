# 03 — Claudian-Plugin: Claude direkt in Obsidian

**Claudian** verbindet Obsidian mit Claude: ein Chat-Panel in der Seitenleiste, das dein
Vault lesen und bearbeiten kann. Mit dem Provider **„Claude Code"** nutzt es deine lokale
CLI-Installation — **kein API-Key nötig**, dein Claude-Abo reicht.

Getestet mit Claudian **v2.0.25**.

## Installation

1. Obsidian → **Settings → Community Plugins**
2. **Restricted Mode ausschalten** (falls noch aktiv)
3. **Browse** → nach **„Claudian"** suchen → **Install** → **Enable**

(In `config-templates/obsidian/community-plugins.json` siehst du die aktivierten Plugins
dieses Setups: `realclaudian` und `dataview`.)

## Provider auf „Claude Code" stellen

1. **Settings → Claudian**
2. **Provider / Settings Provider**: **Claude Code** auswählen
3. **CLI-Pfad** setzen — den Pfad findest du mit:

   ```bash
   which claude
   # z. B. /home/<USER>/.local/bin/claude
   ```

   > ⚠️ **Flatpak-Besonderheit:** Obsidian läuft in einer Sandbox und findet `claude`
   > evtl. nicht automatisch über den `PATH`. Trage deshalb den **absoluten Pfad** ein.

4. Optional sinnvolle Einstellungen (siehe Template unten):
   - **Safe Mode:** `acceptEdits` — Claude darf Notizen direkt bearbeiten
   - **Load user settings:** an — deine `~/.claude/`-Konfiguration (CLAUDE.md, Skills) wird geladen
   - **Locale:** `de`
   - **Chat-Position:** rechte Seitenleiste

## Settings-Template

`config-templates/obsidian/claudian-settings.json` enthält alle Einstellungen des
Referenz-Setups mit Platzhaltern. Claudian v2.x speichert seine Einstellungen **im Vault**
unter `.claudian/claudian-settings.json`:

```bash
mkdir -p ~/second-brain/.claudian
cp config-templates/obsidian/claudian-settings.json ~/second-brain/.claudian/claudian-settings.json
```

Danach im Template ersetzen:

- `<YOUR_DEVICE_ID>` → deine Geräte-ID. Am einfachsten: Plugin einmal starten und den
  CLI-Pfad in der UI setzen — Claudian legt den `device:<uuid>`-Eintrag selbst an.
  (Die UUID findest du danach in `.claudian/claudian-settings.json` unter `cliPathsByHost`.)
- `/home/<USER>/.local/bin/claude` → deine Ausgabe von `which claude`

> 📁 **Abgrenzung:** `.obsidian/plugins/claudian/data.json` enthält nur den
> **Session-Zustand** (offene Tabs/Conversations) — keine Einstellungen. Die Datei ist
> in der mitgelieferten `.gitignore` ausgeschlossen und muss nicht kopiert werden.
> Chat-Verläufe liegen unter `.claudian/sessions/` (ebenfalls gitignored).

## Erster Test

1. Claudian-Icon in der rechten Seitenleiste öffnen
2. Fragen: *„Welche Ordner hat dieses Vault und was steht in der CLAUDE.md?"*

Wenn Claude die Vault-Struktur beschreibt, ist alles korrekt verbunden. 🎉

## Weiter

→ [04 — Claude Konfiguration](04-claude-konfiguration.md)
