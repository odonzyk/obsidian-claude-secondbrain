# 02 — Obsidian installieren und Vault anlegen

## Obsidian via Flatpak installieren (User-Install)

```bash
# Falls Flatpak/Flathub noch nicht eingerichtet:
sudo apt install flatpak
flatpak remote-add --user --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo

# Obsidian installieren (User-Install, kein sudo nötig):
flatpak install --user flathub md.obsidian.Obsidian
```

Getestet mit Obsidian **1.12.7**. Start:

```bash
flatpak run md.obsidian.Obsidian
```

> 💡 Andere Installationswege (AppImage, deb, Snap) funktionieren genauso —
> nur die Startbefehle und Sandbox-Pfade unterscheiden sich (siehe Kapitel 08).

## Vault aus der Vorlage anlegen

Die Vorlage aus diesem Repo enthält die komplette Ordnerstruktur, die Vault-Regeln
für Claude (`CLAUDE.md`), eine `.gitignore` und drei Notiz-Templates:

```bash
cp -r vault-template/ ~/second-brain/
```

Danach in Obsidian: **„Open folder as vault"** → `~/second-brain` auswählen.

> ⚠️ **Flatpak-Hinweis:** Die Flatpak-Version darf standardmäßig aufs Home-Verzeichnis
> zugreifen. Falls dein Vault woanders liegt, Zugriff mit Flatseal oder
> `flatpak override --user --filesystem=<pfad> md.obsidian.Obsidian` erlauben.

## Start-Skript

Die Vorlage enthält `start-obsidian.sh`:

```bash
~/second-brain/start-obsidian.sh
```

Es ruft einfach `flatpak run md.obsidian.Obsidian` auf — praktisch für
Desktop-Verknüpfungen oder den Autostart.

## Empfohlene Grundeinstellungen

In den Obsidian-Settings (die Vorlage `config-templates/obsidian/app.json` enthält diese Werte):

| Einstellung | Wert | Warum |
|-------------|------|-------|
| **Restricted Mode** | aus | nötig für Community Plugins (Claudian, Dataview) |
| **Default view mode** | Source | Markdown-Quelltext sehen — hilfreich, wenn Claude Dateien ändert |
| **Core Plugin „Templates"** | an, Ordner `templates` | für die mitgelieferten Notiz-Vorlagen |

Optional kannst du die Configs aus `config-templates/obsidian/` direkt übernehmen:

```bash
cp config-templates/obsidian/app.json ~/second-brain/.obsidian/app.json
cp config-templates/obsidian/graph.json ~/second-brain/.obsidian/graph.json
```

(`graph.json` bringt die 13 Farb-Gruppen für die Graph-Ansicht mit — siehe Kapitel 06.)

## Weiter

→ [03 — Claudian Plugin](03-claudian-plugin.md)
