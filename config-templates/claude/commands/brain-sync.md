Führe einen Second-Brain-Sync durch:

1. Lies `~/.claude/projects/<PROJECT_SLUG>/memory/MEMORY.md` und die darin verlinkten Memory-Dateien
   (Hinweis: `<PROJECT_SLUG>` ist der Verzeichnisname deines Haupt-Projekts unter `~/.claude/projects/`,
   z. B. `-home-<USER>-projekte` — einfach mit `ls ~/.claude/projects/` nachschauen)
2. Lies `~/second-brain/CLAUDE.md` für Vault-Konventionen
3. Prüfe `~/second-brain/` auf fehlende Notizen (git status, neue Ordner, leere Bereiche)
4. Lege im Second Brain fehlende Notizen an, falls es sinnvolle neue Einträge aus dem Auto-Memory gibt — frage vorher kurz nach (propose-then-commit)
5. Führe am Ende `cd ~/second-brain && git add -A && git commit -m "sync: $(date +%Y-%m-%d)" && git push` aus, wenn Änderungen vorhanden sind
6. Gib eine kurze Zusammenfassung: was geprüft, was angelegt, was gepusht
