---
date: 2026-10-26
type: reunion
personnes: []
projet:
statut: fait
tags:
  - reunion
---

- [ ] Calcul PFTN noel 6 OCCA CAMPUS 📅 2026-10-30 
- [ ] Voir avec Thierry les extractions des affiches horaires 📅 2026-10-30 

A sonder semaine 4 ARC


# Page d'accueil


Refaire : 

- Infos générales sur le SA
	- Dates
	- Calendrier des principaux travaux (WE de coupure PMP VC
	- Global annuel et semaine de base
		- Nb de JS N, U et réserve
		- Distance totale commerciale
		- Distance totale W
		- KM Caisse commerciaux
		- KM Caisse W
		- Distance + KM-C Totale
	- Liste des roulements (lettre et nom)

- Rediriger vers Sharepoint

-- Sharepoint
f" 
Source travaux -> Conséquences de charge études week-ends
Source travaux -> Exports Orion des Contextes et mise à jour à chaque modif de semaine
Source travaux -> Lien avec le COPIL Travaux (regénérer ou maj)


---

Features rewrite


0. General : Rewrite of input data structure

Given the new features needed, we will streamline and enhance the input data and folder structure.

The structure is now : 
Unless specified, all files are direct tool (ORION Mainly or TCAP) extracted and structured files.

`data/input/[Service Annuel name]{SAyyyy}/`
	`service_description.xlsx`
	`contextes_travaux/`
		`contextes_services/`
			`Contextes_Services_{SAyy}.xlsx`
		`scenarios_travaux/`
			`A structured but handmade ORION list of work scenarios by line axis and a list of trains , finishes on .xlsx`
	`legacy_travaux_synthese/`
		`{one excel macro file .xlsm built by a coworker, hand made file already analyzed, the basis for tcap travaux analysis`
	`tcap`
		`{A list of all TCAP raw and official data -no copy>paste}`
	`sous_services/`
		`{sous_service_name}/`
			`projets_ressources_description.xlsx`
			`projets_ressources/`
				`{project_name}/`
					`grilles_adc/`
						`ER_PMP.xlsx` # Grille roulement for a depot called PMP
						`ER_RBT.xlsx` # Grille roulement for a depot called RBT
						`ER_TRA.xlsx` # Grille roulement for a depot called TRA
						`for idx, weekday in [(01,LU), (02,MA), (03,ME), (04,JE), (05,VE), (06,SA), (07,DI)] for pln in {N, U (, V)} file = {SAYY}_{idx}_LIGNE_{pln}_{weekday}.xlsx` # 7 files for each line
					
					`roulements_rames/`
						`RM_LIGNE_N.xlsx` or `RM_LIGNES_NV`
						`RM_LIGNE_U.xlsx`
						
			`/voyages/`
				`Voy_Ligne_N.xlsx`
				`Voy_Ligne_U.xlsx`
				`(Voy_Ligne_V.xlsx)`


1. Main Landing Page "Pilotage"/"Vue d'ensemble"

Replace the current page by a totally new page that will keep a filter band with Service Annuel, Sous Service Annuel, Version de roulements, Passenger line "Ligne", Dépôt, Roulement, weekdays filters.
Enhance the UI/UX of all these filters, especially the one for roulement.

We will need new KPIs, remove the old ones which UI seems not to match with the rest of the app that has been implemented later on.

This page should features KPIs that as a Smooth Modern but clever UI/UX product specialist will design and craft.
but i need


On the whole service annuel
- Total Kilometers of all roulement rames
- Total number of JS

On a BASE WEEK info
- Total (Weekly) number of commercial  trains (Voyages) 
- Total (weekly) number of Journee Service (JS)


On charts by weekdays (mostly bar chart but you can rewrite it)
- Number of voyages per weekday and per axis - with a toggle to enable all type, commercial only, technical only
- Number of JS per weekday and separated info by line (JS are tagged by passenger line "Ligne")

And that's it.

2. Comparison Page "Pilotage/Comparaison"

The comparison tool must allow to compare objects that are bound to resources_projects
Keep the current Comparison KPIs and if you have updated the whole UI , just update the UI here to be in the same configuration.

3. Offres & agents / Journee Service

Keep the current page and KPI, if necessary update/enhance UI

4. O & A / Analyse avancées
Keep the current page and KPI, if necessary update/enhance UI

5. O & A / Robustesse
Keep the current page and KPI, if necessary update/enhance UI

6. O & A / Roulements

-> This page will be redefined for the ensemble roulement. Here are some KPI to inspire you : 




OK Page JS : create an ER analysis tool

Page Scenarios travaux

Calendar of application
Definition of km and nb of impacted days per scenario
Even with limitation


-> Create Budget Page
Create base week from projet
Extrapolate on whole year
Remove KM and JS From travaux scenario application



---


Data source rewrite

The main data used by this app are 





| Object name                | Acronym, short name | Object<br>source       | Object attributes<br>(can be challenged) | Existing ? | Definition/details                                                                                                                                                                                                                                                        |
| -------------------------- | ------------------- | ---------------------- | ---------------------------------------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Service Annuel (SA)        | SA{yyyy}            | Generated at DB Reset  |                                          | Yes        | Period of time that defines the work done by the transport planner. Transport plans are made for a specific SA most of the times.<br>It is linked to a year (2027 for example) and spans from the second Sunday of December Year Y-1 to the second Saturday of December Y |
| Sous-service (SSA)         | SA{yyyy}_{SSA_name} | Reading files from ETL |                                          | No         |                                                                                                                                                                                                                                                                           |
| Version de roulement (PVR) | PVR_name            | Reading files from ETL |                                          |            |                                                                                                                                                                                                                                                                           |



- General data 
	- Service annuel of application (SA, Source : from app generation, with each service annuel we should derive a year of application : 2026; 2027; 2028; 2029)
		- has a main year (2027)
		- a calculated name "SA" + Main Year
		- Starts on the second sunday of december of MainYear-1
		- Ends on second Saturday of Decembre of MainYear
	- Subservices of application (SSA)
		- Can be the whole service annuel or pieces of this one. It is only used to have a different train timetable if necessary (for example, we open a new line mid year thus we have different train voyages object times or list of sillons)
		- To 
	- Resources usage project (PVR). One year of application can hold several service annuel projects, one of these projects can be marked as "main" and other as projects or variants, the user can define which service annuel is the main one, a default one is issued from the ETL. (Source : from app generation)
	- Train Passenger lines operating names. We should have the names of lines N, U, V for the moment. (Source : from app generation with checking of ETL folder names)
	- General physical infrastructure 
		- SNCF RESEAU - Gaia tool
			- Objects : 
				- TIVS (railway track unit objects ("tronçon d'itinéraire de voie") from which we can derive (geojson here but we do not serve tiles or geodata for the moment : "C:\Users\9606807G\workspace\repos\ppu_nu\unified_project\data\input\_referentiel\reseau\tiv_geo\Export_RAI_TRONCON_VOIE_TOUS.geojson")
					- UIC Code line (can be used in dropdowns or filter pr by code line)
					- Tracks of these lines (with junctions between tracks and lines)
					- You can store this object in a geotable with the direct columns
							- Note that the attributes PK (column `PK_DEBUT_R` and `PK_FIN_R`) are in the form "xxx+yyy" which means xxx + yyy/1000 most of the time.. but not always. Here is a code snippet that helps reads this kind of pk `C:\Users\9606807G\workspace\repos\confluo\confluo\utils\pk_sncf.py` keep sncf format for display but for calculations use a float version derived from this small util i've made long time ago for another project
					
				- Points Remarquables (PR) : list of specific points on the railway network that is used to waypoint train `C:\Users\9606807G\workspace\repos\ppu_nu\unified_project\data\input\_referentiel\reseau\points_remarquables\Points Remarquables PR-GaiaVe-DataSniffeur-20261027-210635.xlsx`
				- PR of type Batiment Voyageur "CH=00" or "CH=BV" are the main passenger stations
					- Same PK /PK SNCF logic here
		- ORION network objects 
			- "Lieux" : a translation of physical waypoints, this is the main object used to track the voyage object that we will use later (source `C:\Users\9606807G\workspace\repos\ppu_nu\unified_project\data\input\_referentiel\orion\lieux\DEFINITIONS_LIEUX_ORION.xlsx`)
			- Note that most of Orion Lieux have a correspondant PR
	



This general data is meant to be the same across the years.

Then we have usage data, the core of the app


- List of Voyage (example here `C:\Users\9606807G\workspace\repos\ppu_nu\unified_project\data\input\voyages\SA2027\base\SA27_Voy_LN_PH1.xlsx`)
	- Be careful, this may contains duplicates; it holds a list of waypoints with duplicated info from a single voyage, you should split that into two tables and eliminate duplicates of a voyage and its waypoints
	- A voyage is linked to a main service annuel of application

- Roulement Materiel Data
	- From `./data/input/roulements_rames/{service_annuel}/{service_annuel_version}/{service_annuel_nickname}_RM_LIGNE_{passenger_line_name}_PC.xlsx` 
	- This gives data of the roulement itself
		- A roulement holds a line of roulement which indicates for each 7 weekdays the different activities a line of roulement (which we can assimilate to a physical train machine [two lines of roulement doing the same activities at the same times the same weekday are likely two physical train attached togeter that operates as a "UM2"  a long train made of two elements])
		- A line of roulement for a specific day holds some task of "tache vehicule" which can be maintenance activities (types CEBOR or MAINTENANCE DELOCALISEE), some rest times, some parking times, some voyage time (actually travelling with or without passengers, with reference to the voyage table), some operations times (security operations such as VAE, PAQ, TT) etc. This is used to understand how a machine resource is used across a week that is supposed to begin again and again across 52 weeks of a service annuel
		- A roulement materiel is linked to a service annuel version


- Journee Service (usage of train driver resources)
	- in data/resources folder
	- Already well mapped : it gives the detail of activities from train drivers
	- These activities can hold voyages, and can be linked through sillon number to a a voyage (may be a version of this voyage depending on the weekday of application)
	- This is linked to a service annuel version

- Ensemble Roulement (ER, how train drivers are used accross a weekly schedules "roulement")
	- This is a grid that explains how that for a train driver "depot", we create some "roulements" that will hold specific number of lines ("ligne de roulement") which is basically a train driver. For example, the roulement 144P of PMP depot holds around 20 lines, so 20 drivers have their schedule for the whole year. They know that on depending on their position (train driver Allan is given the first week the line number 1 of the "Ensemble roulement" of roulement 144P of PMP, he will the first monday of the year do the JS R111 then the tuesday the R122 and so on, then on the next week he moves to line 2, and so on)
		- Some train drivers do not have a roulement and are on "Facultatif" service, where they take the "rest" of JS that should be covered when a roulement line holder is for example on holiday or sick etc. All the JS of a roulement are meant to be put in an ensemble roulement or a "AF" ensemble roulement , which are JS that cannot be put in a grid of ensemble roulement , the AF can be considered as "separate" ER but is still affiliate to the main roulement. we have for instance 144P and the AF144P
		- In an ensemble roulement, we can have
			- a JS (linked to the JS table)
			- a "(d)" or a "d" : which means the train driver is meant to cover another JS that is leftover from another line or another roulement : it is called a "disponibility"
			- a "(D)" : which is a specific type of disponibility where we usually put some rest of type "RM", we can call it "RM", the case is important
			- a "RP" which the mandatory rest "Repos Périodique" 
			- A list of average kpis that measure how well we chain the JS to ensure maximal occupation for train drivers while having work life balance (rest on week ends for example)
		- This is not yet used by a feature in the app , but you can as a product engineer, HR / Finance advisor on how we use the train driver think about feature that we could implement before i give you specific ones






---


