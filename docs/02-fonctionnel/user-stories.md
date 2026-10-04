# User Stories

## Format
En tant que [utilisateur]
Je veux [action]
Afin de [valeur]

---

## Liste

### STEP-11 : Création des profils (patient, admin)
* **User Story** : *As a User, I want to Authenticate myself on the SaaS or the mobile App so that I can Access the corresponding information.*
* **Critères d'acceptation** :
  - [ ] Les rôles (Patient, Admin) sont disponibles et gérés sur le backend.
  - [ ] Les objets de données (`DataObjects`) nécessaires à la gestion de la session et de la connexion sont créés.

---

### STEP-12 : Connexion (Sign in)
* **User Story** : *As a User, I want to Authenticate myself on the SaaS or the mobile App so that I can access the platform.*
* **Critères d'acceptation** :
  - [ ] L'authentification est fonctionnelle pour un utilisateur avec le rôle **Patient**.
  - [ ] L'authentification est fonctionnelle pour un utilisateur avec le rôle **Admin**.

---

### STEP-13 : Déconnexion (Sign out)
* **User Story** : *As a User, I want to sign out of the SaaS or the mobile app so that I can protect my account and prevent any unauthorized access from my device.*
* **Critères d'acceptation** :
  - [ ] Déconnexion fonctionnelle côté **Patient** (App mobile).
  - [ ] Déconnexion fonctionnelle côté **Admin** (SaaS).
  - [ ] Implémentation de la méthode/endpoint de déconnexion (`Sign Out`) côté backend.

---

### STEP-14 : Suppression de compte
* **User Story** : *As a User, I want to Be able to delete my account so that I can Delete all my data from Digifeet.*
* **Critères d'acceptation** :
  - [ ] Action de suppression déclenchable par un administrateur pour un compte patient.
  - [ ] Endpoint dédié unique sur le backend pour traiter la suppression.
  - [ ] Déconnexion automatique immédiate (`Auto Sign Out`) après validation.
  - [ ] Impossibilité de se reconnecter avec les identifiants du compte supprimé.
  - [ ] Suppression effective et intégrale de toutes les données liées à l'utilisateur en base de données.

---

### STEP-15 : Page de connexion (Interface UI)
* **User Story** : *As a User, I want to Authenticate myself on the SaaS or the mobile App so that I can access the corresponding information.*
* **Critères d'acceptation** :
  - [ ] Présence de l'écran/page de connexion conforme aux maquettes graphiques.
  - [ ] Connexion de la page à l'API backend via l'endpoint de connexion.

---

### STEP-16 : Page de suppression de compte (Interface UI)
* **User Story** : *As a User, I want to have access to a suppression page on the SaaS and the mobile App so that I can choose to suppress the data of my account.*
* **Critères d'acceptation** :
  - [ ] Présence du bouton de suppression sur l'interface.
  - [ ] Appel à l'API de suppression déclenché lors du clic.
  - [ ] Présence d'un bouton de retour (« Flèche Retour »).
  - [ ] Présence d'une modale/message d'avertissement avec un bouton de confirmation avant exécution.

---

### STEP-17 : Bouton de déconnexion (Mobile)
* **User Story** : *As a patient, I want to press the sign out button of the mobile app so that I can protect my account and prevent any unauthorized access from my device.*
* **Critères d'acceptation** :
  - [ ] Bouton de déconnexion positionné en bas de la page Profil du patient.
  - [ ] Liaison du bouton avec l'API backend `Sign Out`.
  - [ ] Affichage d'un message d'avertissement exigeant une confirmation avant la déconnexion effective.

---

### STEP-18 : Connexion aux semelles connectées
* **User Story** : *As a User, I want to Connect my connected soles to my application so that I can Collect and see data related to my feet's health.*
* **Critères d'acceptation** :
  - [ ] Clic sur un bouton dédié pour démarrer l'appairage/connexion des semelles.
  - [ ] Information explicite fournie à l'utilisateur quant au succès ou à l'échec de la connexion.
  - [ ] Notification in-app en cas de déconnexion imprévue.
  - [ ] Possibilité de réessayer la connexion en cas d'échec sans provoquer de plantage (*crash*) de l'application.
  - [ ] Respect de l'accessibilité (ex. ne pas s'appuyer uniquement sur la couleur vert/rouge pour le statut succès/échec afin d'être inclusif pour les personnes daltoniennes).

---

### STEP-19 : Graphique des données en temps réel (Mobile)
* **User Story** : *As a Patient, I want to Monitor the data from my connected soles so that I can assess the state of my feet and act when necessary.*
* **Critères d'acceptation** :
  - [ ] Affichage des données sous forme de flux dynamique (un ou plusieurs graphiques).
  - [ ] Possibilité pour l'utilisateur de réinitialiser/effacer le graphique.
  - [ ] Tant que l'application est active et le matériel connecté, toutes les valeurs mesurées restent consultables sur le graphique.
  - [ ] Effacement automatique du graphique à la fermeture de l'application.

---

### STEP-20 : Refonte des graphiques (SaaS)
* **User Story** : *As a Practitioner, I want to view useful information on the SaaS so that I can quickly understand the data I need.*
* **Critères d'acceptation** :
  - [ ] Liste établie des graphiques existants à conserver.
  - [ ] Liste détaillée établie des graphiques à modifier.
  - [ ] Création des User Stories spécifiques pour chaque graphique à modifier.
  - [ ] Identification et suppression des graphiques obsolètes ou inutiles.

---

### STEP-21 : Page d'accueil (Mobile)
* **User Story** : *As a patient, I want to access the home page of the mobile app so that I can visualize my feet's real time state, risk assessment and sole connection state.*
* **Critères d'acceptation** :
  - [ ] Intégration du graphique en temps réel.
  - [ ] Intégration du composant d'évaluation des risques (*Risk assessment*).
  - [ ] Statut de connexion affiché clairement sur une ligne.
  - [ ] Conformité visuelle avec la maquette fournie.

---

### STEP-22 : Barre de navigation (Navbar)
* **User Story** : *As a User, I want to Access all my main pages/categories so that I can Access the entirety of the application.*
* **Critères d'acceptation** :
  - [ ] Présence des onglets principaux : **FAQ**, **Accueil (Home)**, **Profil**.
  - [ ] Contour carré aux bords arrondis marquant l'onglet actuellement sélectionné.
  - [ ] Couleur de fond de la barre : Bleu foncé / Violet (conforme au Design System).
  - [ ] Couleur des icônes et du marqueur de sélection : Jaune / Beige (conforme au Design System).

---

### STEP-23 : Base de données provisoire & Historique
* **User Story** : *As a user, I want to review past data from my connected soles so that I can (give accurate information to my practitioner / Review the data of my patient to prepare my next appointment).*
* **Critères d'acceptation** :
  - [ ] L'utilisateur (patient) peut interroger un endpoint API pour récupérer l'historique de ses données et événements.
  - [ ] Le praticien dispose des endpoints API pour ajouter, modifier ou supprimer des données de l'historique.

---

### STEP-24 : Étude d'architecture pour le stockage temps réel
* **User Story** : *As a maintener, I want to have an ordered data base so that I can navigate the data easily.*
* **Critères d'acceptation** :
  - [ ] Recherche et analyse comparative des différentes options de stockage.
  - [ ] Rédaction d'au moins 2 propositions d'architecture adaptées au temps réel.
  - [ ] Rédaction d'un document de synthèse (PowerPoint ou support d'ingénierie) présenté au Product Manager.

