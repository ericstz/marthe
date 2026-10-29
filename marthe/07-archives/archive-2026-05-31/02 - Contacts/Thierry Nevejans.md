---
date: 2026-04-09
type: contact
tags:
  - contact
---
# 👤 <% tp.file.cursor() %>

**Service** : 
**Poste** : 
**Mail** : 
**Téléphone** : 

## 📋 Historique des échanges
```dataview
TABLE date AS "Date", type AS "Type"
FROM "01-Reunions" OR "00-Daily" OR "06-References"
WHERE contains(personnes, this.file.name)
SORT date DESC
```


# Impact avec SVCO

Obligation à être transféré au 13/12 puis recherche à être immédiatement transféré.
