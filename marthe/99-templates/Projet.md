---
date: <% tp.date.now("YYYY-MM-DD") %>
type: projet
statut: en-cours
tags:
  - projet
---

# 📁 <% tp.file.cursor(1) %>

**Date de début** : <% tp.date.now("DD/MM/YYYY") %>
**Date cible** : 
**Porteur** : 
**Parties prenantes** : 

## 🎯 Objectif

> En une phrase : quel est le résultat attendu ?

## 📋 Tâches

```tasks
not done
tags include #projet/<% tp.file.cursor(2) %>
sort by due
```

## 🗓️ Réunions liées

```dataview
LIST
FROM "01-meetings"
WHERE projet = this.file.name
SORT date DESC
```

## 📝 Notes et avancements

- 

## 📎 Documents / Références

- 
