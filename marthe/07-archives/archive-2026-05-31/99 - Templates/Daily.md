---
date: <%= today %>
type: daily
tags:
  - daily
---

# <%= tp.date.now("dddd DD MMMM YYYY") %>

<< [[<%= yesterday %>|Hier]] | [[<%= tomorrow %>|Demain]] >>

---

## 📋 To do du jour
```tasks
not done
due on <%= today %>
```

## 📅 Réunions du jour

```dataview
TABLE personnes AS "Participants", projet AS "Projet"
FROM "01-Reunions"
WHERE date = date("<%= today %>")
SORT file.ctime ASC

```

## 📞 Échanges (mails, Teams, tel)

## 📝 Notes du jour

## ✅ To do créées aujourd'hui

```tasks
not done  
created on <%= today %>
```
## 📋 To do demain

```tasks
not done  
due on <%= tomorrow %>
```

## 📋 To do de la semaine

```tasks
not done  
due after <%= lastDay %>  
due before <%= nextWeek %>  
sort by due
```

