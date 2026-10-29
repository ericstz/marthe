---
date: 2026-03-26
type: formation
formateur: []
tags:
  - formation
  - rprod
  - acr
---


# 🎓 <% tp.file.cursor() %>

**Date** : 26/03/2026
**Formateur** : 
**Durée** : 

## 📝 Notes clés

Dans l'organisation, on garde la lignée de construction PdT -> Km -> Rendement kilométrique -> Nb de JS.

A partir de ce nb de JS, ma productivité ADC me permet de définir le nombre d'ADC.


---
Type d'effectifs : 

- EU : paire de pieds, agents en tant que tel
	- Au figeage/budget = tous nos agents qui nous rattachés, y compris ceux détachés/mis a dispo
	- En réalisé = ressources utilisables (y compris ceux qui me sont rattachés en utilisation, détachés d'ailleurs)
	- Comment se fait la jointure ?
- ED : Effectifs corrigés des temps partiels et des ILD

Effectif calculé = ![[Pasted image 20260326101436.png]]

Sur la définition du $K_i$ , on peut le calculer en évolution mensuelle (- mais comment , Ok on prend en compte les absences, mais pourquoi on l'évalue à 2)

$$
K_i^m \ = \ \frac{jours_m}{jours_m  -  jours_{absence}}
$$

Exemple, à 30 jours mensuels, on a environ 15 jours d'absence (RP, CA...).
On considère un "bon" Ki comme inférieur à 2.


Pour prendre en compte des effets d'expérience, (notamment, un jeune TB1 qui n'est pas disponible sur certaines )

Info pour saisie Guepard : il faut être au plus "juste" partout.  Pas d'intégration des grèves en théorie.

Noter : dans les relations PROD/GEF-RH, on garde dans Guepard une source en EU.

Le management du R Production se fait sur la traduction opérationnelle du budget/figeage pour faire accoster les deux.

Dans les exercices budgétaires on distingue de JS dimensionnantes / JS FACultatives 

Dans le calcul de la productivité, dans le quotient, au dénominateur les effets temps partiels et les effets ARC/assistants DPX.



--


Exercice 

Sur des agents sédentaires :  (ex en 3x8 = $365 * 3 =1095$ postes à couvrir)
Ensuite, on récupère les jours d'utilisation autre (JF, DELE, Réunions/GT... )
Et enfin, les absences (règlementaires liée au régime de travail : ici 118RP+28CA+14RU et les RF(au calcul selon l'année, 8 -10 à général) et une part de Maladie provisionnée, souvent au prorata historique)
172 jours d'indispos.

On a donc pour un agent, environ 188 jours travaillés possibles.
On a 1095 jours-postes à trouver donc 5.82 agents nécessaires => 6 agents nécessaires pour un 3x8

- Coté ADC, les différents postes d'inutilisation (I, i, d, NUF)
- Les postes de formations, les familles : JFC; Extensions de compétences (EM, Système); Etude de lignes; Formations diverses (FE, sureté, prise de parole, tournée..)
- Autres postes 
	- Visites médicales (VMT, VAS)
- Familles d'absence (RP, RM -compensateurs-, RF, CA, MA, AA : VT, AH(pour réunion syndicale) )

#todo #ordo #fredericM Suivi fin des utilisations/inutilisations ?


![[Pasted image 20260326142847.png]]


--
-  **Saisie et lecture GUEPARD**

![[Pasted image 20260326143623.png]]

-> Budget calé à la V1 du budget en juillet
-> Prévisionnel mis à jour chaque mois 
-> Réalisé depuis Pacific ?



- [x] ⏳ 2026-05-01 #todo #fredericM #ordo cranter sur le suivi de notre utilisation lors des points avec Frederic ✅ 2026-10-14
- [ ]  ⏳ 2026-06-01 #todo #ordo #kpi Faire un Sankey de l'utilisation de nos ADC sur ce modèle là : 

![[Pasted image 20260326144347.png]]
![[Pasted image 20260326144359.png]]
![[Pasted image 20260326144429.png]]

⚠️Attention ici : on a décompté les postes à assurer



$$

K_{as} = \frac{N \ Postes}{N \ JS}

$$

## 🔑 Points à retenir
- Différents effectifs (EC, EU, ED, ES, ESFP)
- Coefficients ($K_i$, $K_d$ (1 pour TN), $K_{as}$ (on ne parle plus de $K_c$ ), et on n'est plus censé parler de 7e)
- Logique générale sur l'enchainement Figeage->Budget->PrépaService->Production
- Calcul des 
	- postes de conduite = une journée calendaire portant au moins 1' de journée de services
	- Le décompte se fait par ligne de grille également, deux cases avec 1' de JS = 2 postes
	- Pour cela, le Kas = Nb de Postes/ Nb de JS; le nombre de RHR de jours fait baisser le Kas, les bascules de nuit le font baisser
- Pour info, le 7e = Nb de postes de conduite + i/I/d 


## 🔗 Ressources
- [SAPP-Complément Production 1.pdf](https://sncf-my.sharepoint.com/:b:/r/personal/9606807g_commun_ad_sncf_fr/Documents/Documents/NU/06%20-%20Formations/Compl%C3%A9ments%20production/SAPP-Compl%C3%A9ment%20%20Production%201.pdf?csf=1&web=1&e=cM0nHd) 
- 

## ✅ Actions post-formation
- [x] Action 📅 2026-04-09 ✅ 2026-05-31


