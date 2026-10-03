# Critères d'acceptation

### US01 : Création des profils (patient, admin)
  - [ ] Les rôles (Patient, Admin) sont disponibles et gérés sur le backend.
  - [ ] Les objets de données (`DataObjects`) nécessaires à la gestion de la session et de la connexion sont créés.

### US02 : Connexion (Sign in)
  - [ ] L'authentification est fonctionnelle pour un utilisateur avec le rôle **Patient**.
  - [ ] L'authentification est fonctionnelle pour un utilisateur avec le rôle **Admin**.

### US03 : Déconnexion (Sign out)
  - [ ] Déconnexion fonctionnelle côté **Patient** (App mobile).
  - [ ] Déconnexion fonctionnelle côté **Admin** (SaaS).
  - [ ] Implémentation de la méthode/endpoint de déconnexion (`Sign Out`) côté backend.

### US04 : Suppression de compte
  - [ ] Action de suppression déclenchable par un administrateur pour un compte patient.
  - [ ] Endpoint dédié unique sur le backend pour traiter la suppression.
  - [ ] Déconnexion automatique immédiate (`Auto Sign Out`) après validation.
  - [ ] Impossibilité de se reconnecter avec les identifiants du compte supprimé.
  - [ ] Suppression effective et intégrale de toutes les données liées à l'utilisateur en base de données

### US05 : Page de connexion (Interface UI)
  - [ ] Présence de l'écran/page de connexion conforme aux maquettes graphiques.
  - [ ] Connexion de la page à l'API backend via l'endpoint de connexion.

### US06 : Page de suppression de compte (Interface UI)
  - [ ] Présence du bouton de suppression sur l'interface.
  - [ ] Appel à l'API de suppression déclenché lors du clic.
  - [ ] Présence d'un bouton de retour (« Flèche Retour »).
  - [ ] Présence d'une modale/message d'avertissement avec un bouton de confirmation avant exécution.

### US07 : Bouton de déconnexion (Mobile)
  - [ ] Bouton de déconnexion positionné en bas de la page Profil du patient.
  - [ ] Liaison du bouton avec l'API backend `Sign Out`.
  - [ ] Affichage d'un message d'avertissement exigeant une confirmation avant la déconnexion effective.

### US08 : Connexion aux semelles connectées
  - [ ] Clic sur un bouton dédié pour démarrer l'appairage/connexion des semelles.
  - [ ] Information explicite fournie à l'utilisateur quant au succès ou à l'échec de la connexion.
  - [ ] Notification in-app en cas de déconnexion imprévue.
  - [ ] Possibilité de réessayer la connexion en cas d'échec sans provoquer de plantage (*crash*) de l'application.
  - [ ] Respect de l'accessibilité (ex. ne pas s'appuyer uniquement sur la couleur vert/rouge pour le statut succès/échec afin d'être inclusif pour les personnes daltoniennes).

### US09 : Graphique des données en temps réel (Mobile)
  - [ ] Affichage des données sous forme de flux dynamique (un ou plusieurs graphiques).
  - [ ] Possibilité pour l'utilisateur de réinitialiser/effacer le graphique.
  - [ ] Tant que l'application est active et le matériel connecté, toutes les valeurs mesurées restent consultables sur le graphique.
  - [ ] Effacement automatique du graphique à la fermeture de l'application.

### US10 : Refonte des graphiques (SaaS)
  - [ ] Liste établie des graphiques existants à conserver.
  - [ ] Liste détaillée établie des graphiques à modifier.
  - [ ] Création des User Stories spécifiques pour chaque graphique à modifier.
  - [ ] Identification et suppression des graphiques obsolètes ou inutiles.

### US11 : Page d'accueil (Mobile)
  - [ ] Intégration du graphique en temps réel.
  - [ ] Intégration du composant d'évaluation des risques (*Risk assessment*).
  - [ ] Statut de connexion affiché clairement sur une ligne.
  - [ ] Conformité visuelle avec la maquette fournie.

### US12 : Barre de navigation (Navbar)
  - [ ] Présence des onglets principaux : **FAQ**, **Accueil (Home)**, **Profil**.
  - [ ] Contour carré aux bords arrondis marquant l'onglet actuellement sélectionné.
  - [ ] Couleur de fond de la barre : Bleu foncé / Violet (conforme au Design System).
  - [ ] Couleur des icônes et du marqueur de sélection : Jaune / Beige (conforme au Design System).

### US13 : Base de données provisoire & Historique
  - [ ] L'utilisateur (patient) peut interroger un endpoint API pour récupérer l'historique de ses données et événements.
  - [ ] Le praticien dispose des endpoints API pour ajouter, modifier ou supprimer des données de l'historique.

### US14 : Étude d'architecture pour le stockage temps réel
  - [ ] Recherche et analyse comparative des différentes options de stockage.
  - [ ] Rédaction d'au moins 2 propositions d'architecture adaptées au temps réel.
  - [ ] Rédaction d'un document de synthèse (PowerPoint ou support d'ingénierie) présenté au Product Manager.
