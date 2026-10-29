---
date: 2026-06-04
type: processus
tags:
  - processus
---

# ⚙️ 

**Dernière mise à jour** : 04/06/2026
**Propriétaire** : 
**Domaine** : 

## 📋 Description

Nous allons calculer la charge et les effectifs nécessaires pour couvrir la charge traction conduite.
La charge est issue de la conception des journées de service (JS) ADC prévue au service annuel (SA A+1) de l'année prochaine , au budget, et intuitée pour le service annuel sur prochain (SA A+2), c'est le figeage.

La charge est faite sur tous les produits (lignes) : La ligne N, la ligne U et la ligne V pour le SA2028.


A la charge prévue en conception, on ajoute des ajustements : 

- Réaffectation des réserves communes (en général, liées à la ligne N) à d'autres lignes (ligne U?)


Pour ce faire, ce qui est fait aujourd'hui via de nombreux fichiers excel sera fait via une app locale en Python + PSQL (Docker local qui tourne sur postgres:password@localhost:5435/budget_ppu) à créer (budget_ppu n'existe pas mais le serveur oui) et une interface web JS la plus adaptée (React ? Vite?).
Cette interface doit avoir les codes UI de la SNCF le plus possible [Documentation / Introduction - Documentation ⋅ Storybook](https://wcs.dev.sncf/?path=/docs/documentation-introduction--documentation), les logos des lignes N&U Transilien IDFM la famille de polices Avenir

## 🔄 Étapes


### 0 Objets et définitions

- Service annuel -cf ci dessous
	- nom
	- date de début
	- date de fin
	- année correspondante
	- nombres de lundi, mardi, mercredi, jeudi, vendredi, samedi, dimanche

- Résidence traction


- Roulement

- Journée de Service


- Activité de JS


- Voyage




### 1 Estimation et vérification de la charge

A partir des fichiers Orion BASE extraits de l'application.

Ligne N (Lu, Ma, Me, Je, Ve, Sa, Di) SA27
Ligne U idem sur la base de la conception SA27.

Et la base ligne V au SA28.


Concrètement, on obtient alors pour la charge pour une semaine type pour une ligne.

Pour la déployer sur un service annuel, il faut connaitre le nombre de Lundi, mardi, mercredi, jeudi, vendredi, samedi et dimanches de l'année.

Aux jours calendaires en tant que tel, on va considérer les jours fériés, les veilles de jours fériés, les lendemains de jours fériés éventuellement, et peut etre les considérer qu'on va rouler comme un "dimanche". Par exemple, le 14 juillet 2027 est un mercredi, mais nous allons rouler comme un dimanche. Il y a donc un "mercredi" de moins sur le SA2027 et un dimanche de plus.

Le processus est d'abord de créer le service annuel A en récupérant les jours calendaires entre le début et la fin du service de l'année A.

```rule
Un service annuel est un ensemble de jours calendaires définis par la période entre le dimanche du 2e week end du mois de décembre A-1 et le samedi du 2e week end du mois de décemnbre de l'année A. 
```

#### FEATURE 1.1 : L'application doit importer en base de données en initialisation les services annuels de l'année en cours, l'année A-1, l'année A+1 et l'année A+2
En initialisant cette application, nous devons importer dans la base de données Postgresql par défaut les services annuels en considérant chaque jour férié francais (via la librairie etalab jours_feries) comme un dimanche.

On pourra ensuite consulter dans une page paramétrage / Service Annuel
le nom du service annuel (SAYYYY: SA2027 par exemple), ses dates de début/fin,
son nombre de jours calendaires considérés (nombre de Lundi, Mardi, etc..., ainsi que consulter la liste des jours fériés, la liste des jours fériés et des jours autour)

J'aimerai aussi pouvoir modifier cette attribution des jours fériés en changeant, si je le souhaite, un des dimanche automatiquement attribué pour un  jour férié spécifique par un autre jour de semaine, et de même pour la veille ou le lendemain de ce jour;

j'aimerai pouvoir le sauvegarder en base de données.

Cela ne sera effacé que si nous réinitialisons la base de données, via un commande poetry ou via l'interface web.


- Structure des fichiers Orion BASE.

Il  y a un fichier par jour par ligne.
Ceux ci contiennent des informations sur les résidences, les journées de service, les activités au sein de ces journées de service et certaines de ces activités sont des voyages.

Ces journées sont applicables sur un certain service annuel et sur un jour calendaire.
L'ensemble des JS sur une semaine type est appelé un SOCLE.

#### FEATURE 1.2 : L'application doit importer en base de données les journées de service (avec les résidences et les activités de celles ci)

En se basant notamment sur l'archive etl, importe les fichiers BASE selon le jour présent dans le titre et la ligne puis affecte les à tous les services annuels à partir de celui présent dans le titre du fichier (SA et SA+1)


#### FEATURE 1.3 : Je peux consulter la liste des JS et les décomptes par semaine calendaire, puis dans le service annuel des JS et des kilomètres associées aux JS

J'aimerai avoir des tableaux et des filtres 



Features à venir : 

- Pouvoir créer le budget (budget exprimé en JS et en km via des métriques calculées via le socle)
	- Ensuite, on ajoute les évolutions d'offre d'un SA à l'autre
	- Les  différentes réserves spécifiues (froid)
	-  les JS de marches d'essai
	-  les effets travaux qui réduisent les KM donc les JS associées 
	- On définit ainsi la vraie charge à couvrir sur un service annuel exprimée en nombre de JS et en nombre de km
- Ensuite on va définir la trame budgétaire des ressources : combien de conducteurs va t on mettre en face de cette charge
- On va pouvoir analyser aussi la charge en regardant le nombre de JS par résidence, par jour
	- Ces analyses se font uniquement sur les socles de JS hebdomadaires
	- Regarder pour chaque JS comment elle est composée : ses amplitudes horaires, ses lieux de prise de service PS et de fin de service FS
	- Si elle a un RHR
	- Catégoriser les JS selon les heures de PS/FS ou amplitude
	- Catégorier les JS selon le nombre de voyages qu'elle comprend (notamment de tours des différents axes N2, N4, N5, N6, N8 et U3 et V)
	- Comparer les services annuels entre eux (combien de JS en plus/moins d'un SA a l'autre, par ligne par résidence par jour ou au global)
	- Comparer des variantes de projet de service annuels entre eux 
- Ajouter les travaux qui réduisent les kilomètres à parcourir et donc in fine le nb de JS via la conversion km/js moyen
- Visualiser dans le temps ces travaux sur des gantt et par axe
- Estimer la perte de km lié à chaque chantier, et puis de façon globale puis de façon mensuelle
- Pouvoir faire de nombreux exports excel à différentes étapes





### 2 Suivi budget Traction

D
