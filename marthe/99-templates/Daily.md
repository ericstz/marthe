---
date: <% tp.date.now("YYYY-MM-DD") %>
type: daily
tags:
  - daily
---
<%* await tp.file.rename(tp.date.now("YYYY-MM-DD")) %>
# <% tp.date.now("YYYY-MM-DD") %>

<< [[<% tp.date.now("YYYY-MM-DD", -1) %>|Hier]] | [[<% tp.date.now("YYYY-MM-DD", 1) %>|Demain]] >>

---

## 📋 À faire aujourd'hui

```tasks
not done
due on <% tp.date.now("YYYY-MM-DD") %>
```

---

## 📅 Réunions du jour

```dataview
TABLE personnes AS "Participants", projet AS "Projet"
FROM "01-meetings"
WHERE date = date("<% tp.date.now("YYYY-MM-DD") %>")
SORT file.ctime ASC
```

---

## 📞 Échanges du jour
> Mails, Teams, appels téléphoniques reçus ou passés

- 

---

## 📝 Notes libres


---

## ✅ Tâches créées aujourd'hui

```tasks
not done
created on <% tp.date.now("YYYY-MM-DD") %>
```

---

## 📋 À faire demain

```tasks
not done
due on <% tp.date.now("YYYY-MM-DD", 1) %>
```

---

## 📋 À faire cette semaine

```tasks
not done
due after <% tp.date.now("YYYY-MM-DD", -1) %>
due before <% tp.date.now("YYYY-MM-DD", 7) %>
sort by due
```
