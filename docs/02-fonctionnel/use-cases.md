# Use Cases

## Cas d'Usage : Acteur "Praticien"

### UC-PRAT-01 : Consultation globale et tri des patiens
- **Acteur Principal :** Praticien
- **Acteurs Secondaires :** Aucun
- **Objectif :** Permettre au praticien d'avoir une vue synthétique de l'ensemble de ses patients suivis, avec une indication visuelle des niveaux de risque afin de prioriser ses actions.
- **Déclencheur :** Le praticien se connecte au portail web DigiFeet.
- **Préconditions :**
  1. Le praticien possède un compte actif et authentifié.
  2. Au moins un patient est attribué à son profil.
- **Flux Principal (Scénario nominal) :**
  1. Le praticien accède à la page d'accueil.
  2. Le système récupère et affiche la liste des patients attribués au praticien.
  3. Pour chaque patient, le système affiche les indicateurs clés : nom, prénom, `pourcentage de risque`, statut d'alerte récent et date de dernière synchronisation.
  4. Le praticien filtre ou trie la liste par niveau de risque (ex: Risque Élevé, Risque Modéré, Stable).
  5. Le praticien sélectionne une fiche patient pour l'analyser en détail ([vers UC-PRAT-02](#UC-PRAT-02-:-Analyse-détaillée-d'une-fiche-patient-&-cartographie-des-pressions)).
- **Flux Alternatifs & d'Exception :**
  - *FA 1.1 - Aucun patient assigné :* Le système affiche un message d'information "Aucun patient assigné à votre compte" avec un bouton pour contacter l'administrateur.
  - *FE 1.1 - Erreur de connexion API :* Si le backend est indisponible, un message d'erreur s'affiche avec la possibilité de rafraîchir la page.
- **Postconditions :** Le praticien identifie immédiatement les patients prioritaires et accède au dossier sélectionné.


### UC-PRAT-02 : Analyse détaillée d'une fiche patient & cartographie des anomalies
- **Acteur Principal :** Praticien
- **Acteurs Secondaires :** Backend / Bouchon IoT
- **Objectif :** Analyser l'historique des pressions plantaires, la cartographie thermique et l'évolution temporelle du score de santé d'un patient.
- **Déclencheur :** Le praticien clique sur un patient dans le tableau de bord ([UC-PRAT-01](UC-PRAT-01-:-Consultation-globale-et-tri-des-patiens)).
- **Préconditions :** Le praticien est connecté et sur la fiche du patient ciblé.
- **Flux Principal (Scénario nominal) :**
  1. Le praticien accède au détail du dossier patient.
  2. Le système interroge la base de données et affiche l'historique des `métriques enregistrées`.
  3. Le système génère une cartographie visuelle (heatmap) de la plante des pieds indiquant les zones de surpression cumulée.
  4. Le praticien choisit l'intervalle de temps d'analyse (ex: 24 heures, 7 jours, 1 mois).
  5. Le système réactualise la cartographie, les graphiques et `le pourcentage de risque`.
  6. Le praticien consulte le journal des alertes passées.
- **Flux Alternatifs & d'Exception :**
  - *FA 2.1 - Données insuffisantes :* Si aucune donnée n'a été transmise sur la période sélectionnée, le système affiche "Aucune donnée disponible pour cette plage de dates" tout en indiquant la date du dernier relevé connu.
- **Postconditions :** Le praticien dispose d'un diagnostic visuel et chiffré du risque de plaie plantaire.

### UC-PRAT-03 : Paramétrage personnalisé des seuils d'alerte
> IMPORTANT
>
> Check this use case again should the Practitioner be adjusting the thresholds?
>Et trouver les valeurs par default dans le notion donner par gabriel
- **Acteur Principal :** Praticien
- **Acteurs Secondaires :** Patient, Dispositif / Bouchon IoT
- **Objectif :** Ajuster les seuils de pression et les temps d'exposition tolérés en fonction de la pathologie spécifique du patient.
- **Déclencheur :** Le praticien sélectionne l'option "Modifier le paramétrage" dans la fiche du patient.
- **Préconditions :** Le praticien est identifié et consulte la fiche du patient concerné.
- **Flux Principal (Scénario nominal) :**
  1. Le système affiche les réglages actuels de déclenchement des alertes (valeurs par défaut `[à préciser]`).
  2. Le praticien modifie la valeur du seuil de surpression critique ainsi que la durée d'exposition tolérée.
  3. Le praticien valide la saisie.
  4. Le système contrôle la cohérence physique et médicale des valeurs.
  5. Le système enregistre la configuration et transmet les paramètres à jour au profil du dispositif / simulateur DigiFeet.
  6. Une confirmation visuelle "Paramètres mis à jour avec succès" est affichée.
- **Flux Alternatifs & d'Exception :**
  - *FE 3.1 - Saisie incohérente :* Le praticien entre une valeur hors limites (ex: valeur négative). Le système bloque l'enregistrement et signale le champ invalide.
- **Postconditions :** Les règles d'alerte du patient sont mises à jour dans le système.


### UC-PRAT-04 : Génération et exportation du rapport de suivi
- **Acteur Principal :** Praticien
- **Acteurs Secondaires :** Aucun
- **Objectif :** Éditer un compte-rendu synthétique de l'évolution du patient pour le dossier médical.
- **Déclencheur :** Le praticien clique sur "Générer un rapport".
- **Préconditions :** Le praticien consulte la fiche d'un patient.
- **Flux Principal (Scénario nominal) :**
  1. Le praticien sélectionne la période couverte par le rapport.
  2. Le praticien coche les éléments à intégrer (graphiques, historique des alertes, score de risue).
  3. Le système génère le document au format CSV.
  4. Le téléchargement s'exécute automatiquement sur le poste du praticien.
- **Postconditions :** Le rapport est disponible au format CSV pour impression ou archivage.

---

## Cas d'Usage : Acteur "Patient"

### UC-PAT-01 : Consultation du tableau de bord de santé et conseils
- **Acteur Principal :** Patient
- **Acteurs Secondaires :** Aucun
- **Objectif :** Prendre connaissance de son état de santé plantaire quotidien et lire les recommandations de prévention sur son smartphone.
- **Déclencheur :** Le patient ouvre l'application mobile DigiFeet Mobile.
- **Préconditions :** Le patient est authentifié dans l'application.
- **Flux Principal (Scénario nominal) :**
  1. Le patient lance l'application mobile DigiFeet Mobile.
  2. L'application récupere les dernières données du dispositif DigiFeet
  2. L'application demande une évaluation de santé calculée par le backend.
  3. L'application affiche un indicateur visuel simplifié (code couleur / score) représentant le niveau de risque actuel.
  4. L'application affiche la liste des conseils préventifs personnalisés (ex: inspection visuelle du pied, pause recommandée).
  5. Le patient consulte ses indicateurs.
- **Flux Alternatifs & d'Exception :**
  - *FA 1.1 - Absence de réseau mobile :* L'application affiche les données de la dernière évaluation de santé connue avec la mention "Mode hors-ligne" ainsi que les metriques en temps réel du patient.
- **Postconditions :** Le patient est sensibilisé à son état de santé quotidien.


### UC-PAT-02 : Réception et gestion d'une alerte de surpression en temps réel
- **Acteur Principal :** Patient
- **Acteurs Secondaires :** Bouchon IoT / Dispositif, Backend
- **Objectif :** Réagir immédiatement à un signalement de surpression afin d'éviter la formation d'une plaie.
- **Déclencheur :** Le dispositif ou le simulateur enregistre un dépassement du seuil `[à préciser]`.
- **Préconditions :** Le dispositif DigiFeet est sous tension et appairé à l'application mobile DigiFeet Mobile.
- **Flux Principal (Scénario nominal) :**
  1. Les capteurs transmettent les valeurs de pression en temps réel.
  2. Le moteur de règles évalue que la pression dépasse le seuil `[à préciser]` sur la durée maximale autorisée.
  4. Le patient reçoit la notification push indiquant la zone du pied sous contrainte.
  5. Le patient ouvre la notification et consulte la consigne de décharge (ex: "Veuillez vous asseoir ou décharger le pied droit").
  6. Le patient modifie sa posture. La pression diminue et le système enregistre le retour à la normale.
- **Flux Alternatifs & d'Exception :**
  - *FE 2.1 - Surpression prolongée sans réaction :* Si la surpression persiste après 5 minutes, le système re-notifie avec une intensité supérieure et consigne un événement critique destiné au praticien.
- **Postconditions :** L'événement de surpression est consigné et l'action corrective du patient est encouragée.


### UC-PAT-03 : Synchronisation des données du dispositif connecté
- **Acteur Principal :** Patient
- **Acteurs Secondaires :** Bouchon IoT / Dispositif, Backend
- **Objectif :** Transmettre les mesures collectées par le dispositif vers la plateforme cloud.
- **Déclencheur :** Automatique à intervalle régulier `[à définir]` ou déclenché manuellement par le patient.
- **Préconditions :** La connexion sans fil du smartphone est active et le dispositif DigiFeet est à proximité.
- **Flux Principal (Scénario nominal) :**
  1. L'application mobile établit la communication avec le dispositif DigiFeet.
  2. L'application extrait les relevés de capteurs en attente.
  3. L'application transmet ces données via API sécurisée au serveur distant.
  4. L'application confirme au patient "Synchronisation terminée".
- **Flux Alternatifs & d'Exception :**
  - *FE 3.1 - Échec de transmission :* En cas d'absence de réseau, les données sont conservées en mémoire locale sur l'application mobile et transmises dès le rétablissement du réseau.
- **Postconditions :** Les données de capteurs sont sauvegardées en BDD et prêtes pour l'analyse par le praticien.


## Cas d'Usage : Acteur "Administrateur / Technicien"

### UC-ADM-01 : Gestion des utilisateurs et appairage Praticien-Patient
>IMPORTANT
> Est ce que le practitien peut créer un profil patient? (je crois que oui)
> Est ce que le practitien peut se créer un profil poractitien ou il faut qu'il passe par un admin?
- **Acteur Principal :** Administrateur / Technicien
- **Acteurs Secondaires :** Praticien, Patient
- **Objectif :** Créer les comptes d'accès et définir le périmètre de suivi médical en associant chaque patient à son praticien référent.
- **Déclencheur :** Demande de création d'accès par un établissement de santé client.
- **Préconditions :** L'administrateur est authentifié avec le rôle d'administration.
- **Flux Principal (Scénario nominal) :**
  1. L'administrateur accède au module de gestion des comptes.
  2. Il crée le compte du praticien ou du patient.
  3. Il associe le profil du patient au praticien responsable.
  4. Le système génère et envoie les identifiants temporaires par e-mail.
- **Postconditions :** L'association est effective et sécurise le cloisonnement des données médicales.


### UC-ADM-02 : Configuration et exécution du bouchon / simulateur IoT
> IMPORTANT
> On as toujours pas le bouchons fait par adrient :\
- **Acteur Principal :** Administrateur / Développeur / Technicien
- **Acteurs Secondaires :** Bouchon IoT, Backend
- **Objectif :** Simuler l'émission de flux de données capteurs pour valider l'architecture technique, tester les alertes et alimenter les maquettes en l'absence de matériel physique.
- **Déclencheur :** Préparation d'une démonstration de sprint ou session de test de montée en charge.
- **Préconditions :** Le composant simulateur/bouchon `[probablement du python]` est déployé et connecté à l'API du backend.
- **Flux Principal (Scénario nominal) :**
  1. Le technicien accède à l'outil de pilotage du simulateur `[probablement du python]`.
  2. Il sélectionne un scénario de test (ex: "Patient au repos", "Marche prolongée avec surpression au talon", "Défaillance de capteur").
  3. Il règle la fréquence d'envoi des paquets de données.
  4. Il lance la simulation.
  5. Le bouchon génère des trames de données de test et les envoie aux endpoints API / MQTT du backend.
  6. Le technicien contrôle sur le portail web et l'app mobile que les graphiques et alertes réagissent conformément aux attentes.
  7. Le technicien stoppe le bouchon.
- **Flux Alternatifs & d'Exception :**
  - *FE 2.1 - API Backend inaccessible :* Le simulateur journalise une erreur HTTP/Timeout et stoppe l'émission.
- **Postconditions :** L'architecture technique et le pipeline de traitement des données ont été validés sans dépendre du matériel réel.
