# API Spec

Ce document décrit les endpoints de l'API backend (Spring Boot) qui permettent aux clients (SaaS et Mobile) de communiquer avec les bases de données. L'API utilise les standards REST et le format JSON pour l'échange de données.

## Base URL
`/api/v1`

## Conventions générales
- **Authentification :** Toutes les routes (sauf `/auth/login`) nécessitent un token JWT valide passé dans le header : `Authorization: Bearer <token>`.
- **Formats de retour :** Les succès retournent des statuts `20X`. Les erreurs retournent des statuts `40X` ou `50X` avec un objet d'erreur standard : `{ "error": "message", "code": HTTP_STATUS }`.

---

## 1. Utilisateurs & Authentification (`/auth`)

| Méthode | Endpoint | Description | Rôle requis |
| :--- | :--- | :--- | :--- |
| **POST** | `/auth/login` | Authentifie un utilisateur (Praticien ou Patient) et retourne un JWT. | Aucun |
| **POST** | `/auth/logout` | Invalide le token de session actuel. | Utilisateur |

---

## 2. Patients (`/patients`)

| Méthode | Endpoint | Description (SCRUD) | Payload / Query | Rôle requis |
| :--- | :--- | :--- | :--- | :--- |
| **GET** | `/patients` | **S**earch : Récupère la liste des patients rattachés au praticien. | `?practitionerId={id}` | Praticien |
| **POST** | `/patients` | **C**reate : Crée un nouveau profil Patient. | `{ "firstName": "...", "lastName": "...", "age": 55, ... }` | Praticien |
| **GET** | `/patients/{id}` | **R**ead : Récupère la fiche détaillée d'un patient. | - | Praticien / Patient(soi-même) |
| **PUT** | `/patients/{id}` | **U**pdate : Met à jour les informations cliniques d'un patient. | `{ "weightInKg": 82.5, "notes": "...", ... }` | Praticien |
| **DELETE** | `/patients/{id}` | **D**elete : Supprime le compte d'un patient. | - | Admin |

---

## 3. Praticiens (`/practitioners`)

| Méthode | Endpoint | Description (SCRUD) | Payload / Query | Rôle requis |
| :--- | :--- | :--- | :--- | :--- |
| **GET** | `/practitioners/{id}` | **R**ead : Récupère les informations du praticien connecté. | - | Praticien |
| **PUT** | `/practitioners/{id}` | **U**pdate : Met à jour les informations du praticien. | `{ "mail": "nouveau@mail.com" }` | Praticien |
| **DELETE** | `/practitioners/{id}` | **D**elete : Supprime le compte d'un practicien. | - | Admin |

---

## 4. Historique Clinique des Pieds (`/patients/{id}/feet-history`)

Gestion des antécédents et scores SINBAD pour le pied d'un patient.

| Méthode | Endpoint | Description (SCRUD) | Payload / Query | Rôle requis |
| :--- | :--- | :--- | :--- | :--- |
| **GET** | `/patients/{id}/feet-history` | **S**earch : Liste l'historique clinique des pieds du patient. | - | Praticien |
| **POST** | `/patients/{id}/feet-history` | **C**reate : Ajoute une nouvelle évaluation (ex: score Sinbad). | `{ "type": "...", "sinbadScore": 3, "depth": 1.5, ... }` | Praticien |
| **GET** | `/patients/{id}/feet-history/{historyId}` | **R**ead : Détail d'une évaluation spécifique. | - | Praticien |
| **PUT** | `/patients/{id}/feet-history/{historyId}` | **U**pdate : Modifie une évaluation existante. | `{ ... }` | Praticien |

---

## 5. Alertes Cliniques (`/patients/{id}/alerts`)

Alertes générées lors d'une surpression ou d'une anomalie thermique (hotspot).

| Méthode | Endpoint | Description (SCRUD) | Payload / Query | Rôle requis |
| :--- | :--- | :--- | :--- | :--- |
| **GET** | `/patients/{id}/alerts` | **S**earch : Récupère l'historique des alertes du patient. | `?severity=HIGH&limit=20` | Praticien / Patient |
| **POST** | `/patients/{id}/alerts` | **C**reate : Enregistre une nouvelle alerte détectée par le backend. | (Interne / Automatisé) | Système |
| **GET** | `/patients/{id}/alerts/{alertId}` | **R**ead : Récupère les détails d'une alerte spécifique. | - | Praticien / Patient |
| **PUT** | `/patients/{id}/alerts/{alertId}` | **U**pdate : Met à jour le statut d'une alerte (ex: marquée comme "lue" ou "acquittée"). | `{ "status": "READ" }` | Praticien / Patient |

---

## 6. Données Télémétriques / Capteurs (`/patients/{id}/sensor-data`)

Manipulation des données continues (Db B) provenant des semelles. Étant donné le volume, ces données sont principalement créées (par batch) et lues (par plages temporelles). Les updates et deletes manuels sont très rares.

| Méthode | Endpoint | Description (SCRUD) | Payload / Query | Rôle requis |
| :--- | :--- | :--- | :--- | :--- |
| **GET** | `/patients/{id}/sensor-data` | **S**earch : Récupère les données des capteurs sur une période. | `?startTs=1690000&endTs=1693000` | Praticien |
| **POST** | `/patients/{id}/sensor-data` | **C**reate : Enregistre un lot de données brutes envoyées par le client BLE. | `[ { "dateTime": "...", "left": {...}, "right": {...} } ]` | Système / App |
