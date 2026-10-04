# Composants (C4 - Niveau 3)

## Vue d'ensemble

Cette vue détaille la structure interne du conteneur "Serveur A (API Spring Boot)". Elle identifie les principaux modules (composants) responsables de la logique métier, du traitement des données et de l'accès à la base de données PostgreSQL.

## Composants de l'API (Backend Spring Boot)

### 1. Contrôleurs (REST Endpoints)
- **`AuthController` :** Gère la sécurité, les inscriptions, les connexions (SaaS et Mobile), les déconnexions et la génération/validation des tokens (JWT).
- **`PatientController` :** Gère les opérations CRUD liées aux patients (création de profil, suppression de compte).
- **`TelemetryController` :** Point d'entrée pour la réception (via des requêtes HTTP/JSON du client SaaS) et la consultation des données historiques de pression et de température.
- **`AlertController` :** Gère la récupération et le statut des alertes (ex: notifier la vue par l'utilisateur).

### 2. Services Métier (Logique métier)
- **`ClinicalRulesService` :** Applique les règles de gestion décrites dans les spécifications. Calcule les indicateurs cliniques :
  - Peak Plantar Pressure (PPP)
  - Pressure-Time Integral (PTI)
  - Alertes de température (hotspot contralatéral).
- **`HealthScoreService` :** Service dédié au calcul (ou au relayage) de l'algorithme d'IA interne permettant de générer le "Score de Santé" (Mobilité, Charge, Posture, Risque) basé sur le cumul des données.
- **`ExportService` :** Génère les fichiers d'export (CSV standard et CSV+ clinique) demandés par les praticiens via le SaaS.

### 3. Couche d'accès aux données (Repositories Spring Data JPA)
- **`UserRepository` :** Interagit avec PostgreSQL pour stocker et lire les informations d'authentification (Admins/Praticiens et Patients).
- **`DeviceConfigRepository` :** Stocke les configurations matérielles spécifiques à chaque patient (paramètres de calibration FSR vers kPa, baseline de température).
- **`SensorDataRepository` :** Insère et interroge d'importants volumes de données chronologiques liées aux capteurs.
- **`AlertRepository` :** Enregistre l'historique des alertes déclenchées.

### 4. Sécurité & Configuration
- **`SecurityConfig` :** Implémente la protection des routes API, assurant que seuls les praticiens authentifiés peuvent configurer les seuils, et que les patients n'ont accès qu'à leurs propres données chiffrées.
