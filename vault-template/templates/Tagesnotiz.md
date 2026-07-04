---
date: {{date:YYYY-MM-DD}}
tags: [daily]
---
# {{date:DD.MM.YYYY}}

## 🎯 Fokus heute

## ✅ Erledigt
- [x] 

## 📋 Offen
- [ ] 

## 🚀 Aktive Projekte (heute relevant)

```dataview
TABLE status, tags
FROM "projects"
WHERE status = "aktiv"
SORT file.name ASC
```

## 📝 Notizen

## 🔗 Links
- [[dashboards/Projekt-Dashboard]] — Gesamtübersicht
- Gestern: [[{{date-1d:YYYY-MM-DD}}]]
- Morgen: [[{{date+1d:YYYY-MM-DD}}]]
