---
date: <% tp.date.now("YYYY-MM-DD") %>
type: contact
tags:
  - contact
---

# 👤 <% tp.file.cursor(1) %>

**Service** : 
**Poste** : 
**Mail** : 
**Téléphone** : 
**Localisation** : 

## 📋 Historique des échanges

```dataview
TABLE date AS "Date", type AS "Type", file.link AS "Note"
FROM "01-meetings" OR "00-dailies" OR "06-references"
WHERE contains(personnes, this.file.name)
SORT date DESC
```

## 🗒️ Notes personnelles

- 
