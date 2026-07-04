# 06 — Vault-Struktur: Ordner, CLAUDE.md, Templates, Graph

Die Vorlage `vault-template/` ist ein komplettes, sofort nutzbares Vault-Gerüst.
Dieses Kapitel erklärt das Konzept dahinter.

## Ordner-Konzept

```
~/second-brain/
├── inbox/           # ALLES landet zuerst hier — ungefiltert, schnell
├── knowledge/       # destilliertes, dauerhaftes Wissen
├── projects/        # eine Notiz pro Projekt, Status im Frontmatter
├── daily/           # Tagesnotizen (YYYY-MM-DD.md)
├── dashboards/      # Übersichts-Notizen mit Dataview-Queries
├── claude-memory/   # Claudes kuratiertes Langzeitgedächtnis
└── templates/       # Notiz-Vorlagen
```

**Der zentrale Workflow — inbox → knowledge:**

1. Gedanken, Links, Zwischenergebnisse schnell in `inbox/` kippen (niedrige Hürde!)
2. Regelmäßig (oder per Zuruf) destilliert Claude: fasst zusammen, ergänzt Frontmatter
   und Tags, verlinkt verwandte Notizen und verschiebt nach `knowledge/` oder `projects/`
3. `inbox/` bleibt dadurch leer — das Vault wächst kuratiert statt chaotisch

**`claude-memory/` — das Besondere an diesem Setup:**

Hier pflegt Claude dauerhaften Kontext als normale, versionierte Markdown-Notizen:

- `00-Profil-und-Konventionen.md` — wer du bist, wie du arbeitest
- `01-Infrastruktur.md` — deine Umgebung (nur Unkritisches!)
- `02-AI-Tools-und-Skills.md` — dein Tooling
- `03-Aktive-Projekte.md` — woran du gerade arbeitest
- `04-Tech-Stack-und-Design.md` — deine technischen Vorlieben

Die Vault-`CLAUDE.md` weist Claude an, diese Dateien zu Session-Beginn zu lesen.
Vorteil gegenüber unsichtbarem Auto-Memory: **du siehst, editierst und versionierst**,
was Claude über dich weiß.

## Die CLAUDE.md im Vault

`vault-template/CLAUDE.md` definiert die Spielregeln, sobald Claude im Vault arbeitet:

- **Struktur & Konventionen** — welche Ordner wofür, Wikilinks, Tags, Frontmatter
- **Memory-Regel** — welche `claude-memory/`-Dateien immer zuerst gelesen werden
- **Spiegelungs-Konvention** — Erkenntnisse aus Sessions werden nur **per Vorschlag**
  („propose-then-commit") ins Vault übernommen, nie ungefragt
- **Sicherheit** — keine Credentials in Notizen, keine `.env`-Dateien im Vault
- **Commit-Reminder** — Claude erinnert ans tägliche Git-Backup

## Templates

Drei Vorlagen in `templates/` (in Obsidian: Core Plugin **Templates** aktivieren,
Template-Ordner auf `templates` setzen):

| Template | Zweck | Besonderheit |
|----------|-------|--------------|
| `Wissensnotiz.md` | dauerhaftes Wissen | Frontmatter mit `source:` für die Quelle |
| `Projektnotiz.md` | neues Projekt | `status: aktiv` → erscheint in Dashboards |
| `Tagesnotiz.md` | Daily Note | Obsidian-Datumsvariablen + Dataview-Query auf aktive Projekte |

## Graph-Ansicht mit Farb-Gruppen

`config-templates/obsidian/graph.json` bringt 13 Farb-Gruppen mit — Notizen werden in der
Graph-Ansicht nach Tags eingefärbt, z. B.:

| Tag | Farbe |
|-----|-------|
| `#claude-memory` | Koralle |
| `#infrastruktur` | Türkis |
| `#projekt` / `#projekte` | Pink |
| `#devops` | Grün |
| `#wissen` | Grau |
| `#daily` | Violett |
| `#dashboard` | Dunkelrot |
| Fallback (alle Dateien) | Mittelgrau |

```bash
cp config-templates/obsidian/graph.json ~/second-brain/.obsidian/graph.json
```

**Konvention:** Neue Themen-Tags bekommen sofort eine eigene Farbe (kein Weiß) —
die Vault-`CLAUDE.md` weist Claude an, das automatisch zu pflegen.

## Weiter

→ [07 — Git-Backup](07-git-backup.md)
