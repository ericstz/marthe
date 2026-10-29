# 🏠 Hub — Ma base de travail

> Vault Obsidian · Dernière réorganisation : 2026-05-31

---

## 🚀 Accès rapides

| Zone | Description |
|------|-------------|
| [[00-dailies/\|📅 Notes quotidiennes]] | Une note par jour de travail |
| [[01-meetings/\|🤝 Réunions & échanges]] | CR de réunions, entretiens, échanges téléphoniques |
| [[02-contacts/\|👥 Contacts]] | Fiches personnes avec historique auto |
| [[03-projects/\|📁 Projets]] | Suivi de projets transverses |
| [[04-processes/\|⚙️ Processus]] | Documentation des processus métier |
| [[05-learnings/\|🎓 Formations]] | Notes de formations et apprentissages |
| [[06-references/\|📚 Références]] | Docs, acronymes, infos à garder |
| [[07-archives/\|🗄️ Archives]] | Tout l'historique antérieur |

---

## 📋 Mes tâches

### Aujourd'hui

```tasks
not done
due today
sort by priority
```

### En retard

```tasks
not done
due before today
sort by due
```

### Toutes taches

```tasks
not done
sort by due
```

---

## 📅 Réunions récentes

```dataview
TABLE date AS "Date", personnes AS "Participants", projet AS "Projet"
FROM "01-meetings"
WHERE date >= date(today) - dur(7 days)
SORT date DESC
LIMIT 10
```

---

## 📝 Notes récentes

```dataview
TABLE file.mtime AS "Modifié"
FROM "00-dailies" OR "01-meetings"
SORT file.mtime DESC
LIMIT 5
```

---

## 📖 Guide d'utilisation — Quel flux suivre ?

### Chaque matin

1. Créer une **note quotidienne** dans `00-dailies/` (Cmd+P → "Templater: Create daily")
   - Nommer : `YYYY-MM-DD` (ex: `2026-06-01`)
   - Le template se remplit automatiquement avec tes tâches du jour
2. Parcourir la section **"À faire aujourd'hui"** générée par Tasks
3. Parcourir la section **"Réunions du jour"** générée par Dataview

### Pour une réunion

1. Créer une note dans `01-meetings/`
2. Nommer : `YYYY-MM-DD nom-réunion` (ex: `2026-06-01 hebdo-encadrement`)
3. Remplir : participants (champ `personnes:`), projet si applicable
4. Ajouter les actions avec `- [ ] Action 📅 YYYY-MM-DD` → apparaîtront dans Tasks

### Pour une tâche rapide

- Ajouter directement dans ta note du jour : `- [ ] Ma tâche 📅 2026-06-05`
- Ou dans la note de réunion concernée
- La date d'échéance `📅` est **obligatoire** pour apparaître dans les vues Tasks

### Pour un échange (mail / Teams / téléphone)

- Dans ta note du jour, section **"Échanges du jour"**
- Si c'est important : créer une note dans `01-meetings/` avec `type: echange`

### Pour une demande hiérarchie

- Retrouver via la vue Tasks ou la recherche Obsidian (Cmd+F)
- Chercher par nom de contact, mot-clé, ou tag

---

## 🏷️ Conventions de tags

| Tag | Usage |
|-----|-------|
| `#daily` | Note quotidienne |
| `#reunion` | Compte-rendu de réunion |
| `#echange` | Mail / Teams / Téléphone |
| `#contact` | Fiche contact |
| `#projet/nom` | Notes liées à un projet |
| `#processus` | Documentation processus |
| `#formation` | Notes de formation |
| `#important` | À retrouver facilement |
| `#hierarchie` | Demande / info de la hiérarchie |

---

## 📁 Règles de nommage

| Type | Format | Exemple |
|------|--------|---------|
| Note quotidienne | `YYYY-MM-DD` | `2026-06-01` |
| Réunion | `YYYY-MM-DD nom-réunion` | `2026-06-01 hebdo-encadrement` |
| Contact | `Prénom Nom` | `Jean Dupont` |
| Projet | `nom-projet` | `budget-technicentre` |
| Processus | `nom-processus` | `processus-cef` |
| Formation | `YYYY-MM-DD nom-formation` | `2026-06-01 formation-excel` |

---

## 🔧 Plugins actifs

| Plugin | Rôle |
|--------|------|
| **Templater** | Création automatique de notes depuis templates |
| **Tasks** | Gestion des tâches avec échéances |
| **Dataview** | Vues dynamiques (réunions, contacts, projets) |
| **Calendar** | Navigation calendaire des notes quotidiennes |
| **Smart Composer** | Assistant IA sur les notes |

---

*Archives de l'ancienne base : [[07-archives/archive-2026-05-31/\|Archive 2026-05-31]]*
