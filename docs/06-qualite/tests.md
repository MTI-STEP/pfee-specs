# Tests

La stratégie de test de Digi'Feet repose sur les principes de l'**Agile Software Testing**. Contrairement aux modèles traditionnels où les tests sont relégués à la fin du cycle, nos tests sont exécutés **en continu et en parallèle du développement**. L'objectif est de fournir un retour d'information rapide, de garantir l'alignement avec les besoins cliniques et de corriger les anomalies (bugs) au cours de la même itération (sprint).

## 1. Principes Fondamentaux
- **Tests Continus (Continuous Testing) :** Les tests accompagnent la rédaction du code. Une fonctionnalité n'est pas considérée comme "terminée" tant qu'elle n'est pas testée et validée.
- **Collaboration (Team Involvement) :** Les développeurs, testeurs, et professionnels de santé collaborent quotidiennement (Daily Scrums) pour valider les critères d'acceptation (User Stories).
- **Test-Driven Approach :** Utilisation des pratiques TDD (Test-Driven Development) et BDD (Behavior-Driven Development) pour guider le développement des règles cliniques.
- **Documentation Légère :** Privilégier des checklists (Definition of Done) et des cas de test clairs plutôt que de lourds documents figés.

## 2. Niveaux de Tests (Agile Testing Practices)

Pour garantir une couverture optimale en itérations courtes (Sprints), nous divisons nos tests en plusieurs catégories :

### 2.1. Tests Unitaires (Automatisés)
Testent les plus petits morceaux de l'application de manière isolée pour un feedback très rapide.
- **Backend (Spring Boot) :** Tests avec `JUnit` et `Mockito` pour la logique métier (ex: vérification stricte du calcul de surpression plantaire).
- **Frontend (React) :** Tests avec `Jest` / `React Testing Library` pour valider l'affichage conditionnel (ex: si le statut est `INSUFFICIENT`, l'UI affiche "N/A").

### 2.2. Tests d'Intégration et API (Automatisés)
Vérifient que les différents composants (Conteneurs) communiquent correctement.
- Vérification des endpoints REST de l'API.
- Validation des requêtes et de la persistance en base de données PostgreSQL.

### 2.3. Tests de Connectivité et Hardware (Spécifique Digi'Feet)
- **Mocking BLE :** Développement d'un script python simulant l'envoi de données FSR (Force Sensitive Resistor) par l'Arduino pour tester l'interface SaaS et l'application mobile sans dépendre physiquement de la semelle.
- **Tests d'intégration matérielle :** Pairage Bluetooth réel (sur environnements iOS/Android via Capacitor) et tests de pertes de paquets.

### 2.4. Tests Exploratoires et UAT (User Acceptance Testing)
Tests manuels centrés sur l'expérience utilisateur et les cas non prévus par l'automatisation.
- **Patient (Mobile) :** L'interface reste-t-elle simple et non surchargée ? L'alerte de surpression est-elle lisible et compréhensible immédiatement ?
- **Praticien (SaaS) :** Le praticien parvient-il à recalibrer les capteurs FSR en kPa rapidement lors d'une consultation ?
- Feedback direct des cliniciens partenaires (ex: Centre Hospitalier).

### 2.5. Tests Non-Fonctionnels (Sécurité & Performance)
- **Sécurité :** Vérification du chiffrement des données de santé (en transit via HTTPS et au repos) et de l'inviolabilité des tokens JWT.
- **Performance :** L'application mobile (et le backend) peuvent-ils traiter un flux de données continu d'une session de marche de 30 minutes sans crasher ni saturer la mémoire ?

## 3. Gestion des Données de Test (Test Data Management)
- Utilisation de **jeux de données fictifs et anonymisés** (mock data) pour simuler des journaux de capteurs (pression et température) représentant divers stades de pathologies diabétiques (ex: présence d'un hotspot thermique contralatéral de 2.2°C).
- Les jeux de données sont réutilisables d'un sprint à l'autre pour valider les régressions.

## 4. Gestion des Défauts (Defect Management)
- Tout bug trouvé durant un Sprint doit être **corrigé dans le même Sprint** pour maintenir un code propre (Clean Code) et assurer que le Produit Minimum Viable (MVP) reste potentiellement déployable.
