IchHave2Cassel!

# Maquette de charge

## Définitions

- Service annuel :
objet unique, liée à une unique année calendaire, ayant un nom ("SA"+YYYY : SA2027, SA28...) et un commentaire

ServiceAnnuel
	id : uuid as string
	name: string
	year : int
	service_start: datetime
	service_end : datetime

Exemple : 
	uuid
	SA2027
	2027
	13/12/2026
	12/12/2027



CalendrierAnnuel
	 id : uuid as string
	 service_annuel_id : uuid as string

Cette table doit peut etre servir à stocker les différents jours fériés et leur jour calendaire d'application. Ex, via le paquet python jours ([jours-feries-france · PyPI](https://pypi.org/project/jours-feries-france/)), on veut dire, via saisie utilisateur OU import d'un fichier excel que le 8 mai 2027 doit être circulé comme un dimanche et que la veille du 8 mai, le 7 mai, est un typé comme un vendredi (ou comme son jour naturel)
Mais je n'ai pas d'idée précise de l'architecture.


- Ligne : 
Objet décrivant une ligne de transport au sens du voyageur. Ce programme traitera des lignes N, U et V du réseau Transilien et possédant un ou plusieurs axes et deux "catégories statistiques", une pour les trains commerciaux, et une pour les trains techniques (ou aussi appelés vides voyageurs) ex de valeur  : Catégorie statistique N commercial "TBM", N technique : "UBM", U commercial "TBQ", U technique : "UBQ" par exemple

Ligne
	id: uuid as string
	name: string
	categorie_statistique_commercial: string 
	categorie_statistique_technique: string
	
Exemple : 
	uuid
	N
	TBM
	UBM



- Axe
Un axe est une branche géographique d'une ligne et correspond à un service voyageur associé à cette branche.

Axe
	id : uuid as string
	code: string
	name : string

Exemple : 
	uuid
	N4
	Rambouillet


- Résidence
Une résidence est un regroupement de conducteurs et conductrices : les Journees de Service et les roulements sont liées à une résidence.


Residence
	id : uuid as string
	name: string
	


- Roulement
Un roulement est un assemblage ordonné de journées de service, disposant d'une grille.
Une grille est un enchainement de plusieurs lignes de roulement sur une semaine de 7 jours. Nous définirons la grille plus 


- JourneeService :
Définit le travail unitaire sur un jour calendaire le plus souvent, qu'un conducteur de travail doit réaliser. Elle est liée à un service annuel, à un ou plusieurs axes, est liée à un jour de semaine (lu, ma, ..di), a une heure de début de service appelée "prise de service" et une heure de fin de service. Elle comprend une ou plusieurs activités qui ont eux même des horaires distincts


JourneeService
	id: uuid as string
	service_annuel_id : foreign key vers service_annuel
	name : string
	ps_start: time without timezone
	fs_end : time without timezone
	is_passe_minuit : boolean
	lieu_ps : string
	lieu_fs: string
	distance_km : float nullable
	duration_minutes: float nullable
	nb_taxis: int nullable
	taxis_duration_minutes: float nullable
	has_rhr: boolean
	has_imbrication: boolean
	week_day : int
	residence_id: uuid as string
	roulement_id: uuid as string
	
	

We also need some tables to link Journees Service to Activites, to Axes and a way to know 


- Activite :
Une activité est un élément unitaire d'une journée de service. Il peut s'agit d'un voyage, d'une activité de sécurité comme la mise en stationnement d'un train, d'une activité de voyage non productive comme se déplacer dans un autre train ou un taxi, ou simplement attendre lorsqu'on est en réserve;

Activite
	id: uuid as string
	name: string
	type: Enum among (Déplacement de; Réserve; Opérateur; Déplacement vers )
	duration_minutes: boolean nullable
	comment: string nullable
	is_voyage: boolean 
	sillon_voyage : string nullable



- Voyage

- Sillon

- Utilisations


+Toutes les tables à créer pour les jointures, faciliter l'architecture, sauvegarder les résultats, ou toute autre table nécessaire aux fonctionnalités ci dessous


## Fonctionnalités


### 1 Calcul, sauvegarde et consultation d'un budget d'un service_annuel


#### 1.1 Consulter un budget


L'utilisateur doit disposer d'une fonctionnalité dont la finalité est d'obtenir la charge à réaliser sur un service annuel en nombre de JS et en nombre de kilomètres à parcourir. Ceux ci sont à décliner 

Par filtres temporaires : 

- par semaine calendaire type  : nb de JS et de KM par jour callendaire
	- (traduction directe des données excel)
- Par mois 
	- données excel + conversion via nombre de jours calendaire par mois
- Par un couple de dates bornants au besoin de l'utilisateur
- Par service annuel

Par filtre spatiaux ou d'entités

- Par résidence 
- Par roulement
- Par axe
- Par ligne


Par caractère Régulier ou Facultatif

Afficher le détail des calculs : charge du service (données importées) et la liste des évènements d'ajustement saisis par l'utilisateur (voir ci dessous)

#### 1.2 Construire un budget

La construction d'un budget se fait via les fonctionnalités suivantes


- Définir un service annuel et le calendrier du typage des jours fériés 
	- L'utilisateur doit pouvoir créer un service annuel en choisissant une année calendaire ou doit pouvoir choisir un service annuel existant. 
	- L'utilisateur doit pouvoir lister les services annuels déja créés et voir si ceux ci sont complets, à savoir ont déja un "typage des jours fériés réalisés"
	- L'utilisateur doit pouvoir créer, modifier, supprimer un typage des jours fériés d'un service annuel
		- Via la sélection dans un tableau, qui affiche tous les jours fériés, les veilles de ces jours fériés et les lendemain de ces jours fériés : le jour calendaire par défaut lié au calendrier est par défaut renseigné, et l'utilisateur peut modifier ce jour de façon ergonomique et peut télécharger un fichier csv simple qui lui permettra de recharger de façon ultérieure la saisie qu'il aura faite manuellement
-
- Importer les données Excel de base des indicateurs "OCARINA" qui permettent de définir pour un service annuel et une ligne donnée, la charge en JourneesService, Activite, Roulement associée à un jour calendaire et à une ligne
	- Cet import se fait via l'ETL client de l'application appelable par l'interface utilisateur ou réalisé via ligne de commande avant lancement de l'application utilisateur
	- A noter : les fichiers OCARINA ont pour chaque ligne excel une activité, si plusieurs activités apppartiennent à une Journée de Service, les infos de la Journee de Service sont dupliquées dans le fichier excel, idem pour le roulement.

(cela suppose de sauvegarder la date d'un import de fichier ressource, soit via l'interface , en spécifiant un dossier qui doit contenir des fichiers respecant la nomenclature :"Indicateurs OCARINA base SA2026 N MARDI.xlsx" pour charge d'un MARDI sur le SA2026  et la ligne "N" )


- Ajouter des contraintes en ressource à un budget
	- Il s'agit des journées supplémentaire ou journées à supprimer pour causes multiples
		- Causes : Travaux; Evolution d'offre; Réserve Froid/Redoux; Autres ajustements
	- L'utilisateur, sur un service annuel, doit pouvoir saisir et sauvegarder un ensemble de contraintes comme
		- Le nombre de JS ou de KM (convertis en JS ou en KM selon la moyenne issue des imports ou ETL qui donne le nb moyen de km par js) liés à un évènement dont la cause est ci dessus
			- L'utilisateur peut saisir un "évènement contrainte", choisir le type de cause; saisir 
				- le nom de l'évènement
				- un commentaire facultatif
				- soit un nombre de JS, soit un nombre de KM (en positif : on ajoute ou en négatif, on retire)
				- puis appliquer ce nombre 
					- soit par jour calendaire avec une date de début et une date de fin parmi ceux du service annuel
					- soit par mois
			- Plus tard, l'utilisateur pourra importer une réduction kilométrique liée aux chantiers et travaux du service quand ceux ci seront intégrés à l'application, il pourra alors choisir un ou plusieurs chantiers dont on connait la réduction de charge en kilomètres à appliquer par mois
	


- A partir des données en base, si un import ou un ETL a déja été fait, l'utilisateur doit calculer un budget 
	- Je ne sais pas s'il faut sauvegarder quelque chose du budget pour le récupérer ou juste relancer le calcul, à mon sens, le calcul ne sera pas long et donc peut etre relancé à chaque fois sur la base de données enregistrées ou réimportées
	- Un budget est un objet que l'on peut consulter selon la fonctionnalité 1.1
		- Il peut etre exporté en fichier excel qui dispose de plusieurs onglets : 
			- Onglet Récapitulatif calendaire qui donne par jour calendaire et par type FAC/Régulier (les journées de type Réserve sont considérées FAC) le nombre de JS par jour et le nombre de kilomètres par jour
			- Onglet Récapitulatif mensuel
				- Pour chaque mois donne le total réel sur le mois de service annuel du nombre total de JS et de total de km, ainsi que la moyenne "Nombre de JS par jour" et "NOmbre de KM par jour" calculés ainsi : total JS mensuel/nb de jours du mois, total km mensuel / nb de jours du mois




### 2 Comparaison entre plusieurs services annuels des budgets


### 3 Analyse des journées de service d'un service annuel

#### 3.1 Analyse des journées de service et des roulements

- Résumé du nombre de Journées par Jour calendaire 
- Liste et détail des journées (activités) des Journees de Service
- répartition des journées selon les nombres de tours de chaque axe
- Répartition des journées selon le temps de conduite effectif (formule à venir)
- répartition des journées selon l'amplitude
- Répartition des journées selon la présence de l'heure de début (prise de service) dans une plage horaire d'extreme matinée (entre 2h du matin et 6h du matin) ou fin en extreme soirée (entre 21h et 2h du matin en passe minuit)

#### 3.2 Analyse des grilles de roulement (à venir)


### 4 Affichage de l'offre de trains d'un service annuel (à venir, déja existant dans la base actuelle)


### 5 Affichage des travaux du service annuel (à venir, en partie déja existant dans la base actuelle)


### 6 Affichage des ressources à disposition (à venir)

#### 6.1 Construction de l'Adéquation Charges - Ressource (à venir)


