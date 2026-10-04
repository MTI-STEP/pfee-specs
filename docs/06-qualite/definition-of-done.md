# Definition of Done

## 1. Grille de Contrôle Générale (Applicable à toute User Story)

Une *User Story* (US) est considérée comme **Done** uniquement si l'ensemble des critères suivants sont validés :

### A. Qualité du Code & Revue
- **Standards de code respectés** : Le code suit les conventions établies par l'équipe (ESLint pour le JS/TS, Checkstyle pour Java).
- **Pas de warning critique** : La compilation et le build s'exécutent sans warnings ni erreurs critiques.
- **Revue de code (Pull Request)** : Au moins **1 pair-review** effectuée et approuvée par un autre membre de l'équipe (sur 4).
- **Pas de code mort / de débogage** : Les `console.log`, `System.out.println`, commentaires inutiles ou code temporaire ont été supprimés.

### B. Tests & Couverture
- **Tests unitaires passés** : Tous les tests unitaires existants et nouveaux réussissent à 100%.
- **Seuil de couverture minimal** :
  - Backend Spring Boot : $\ge 70\%$ de couverture sur les services et contrôleurs.
- **Tests de non-régression** : Aucun bug identifié sur les fonctionnalités existantes impactées.

### C. Git
- **Branche mise à jour** : La branche de fonctionnalité est merged sans conflit avec la branche principale `developpement`.

### D. Documentation & Agilité
- [ ] **Critères d'acceptation (PO/Équipe)** : Tous les critères décrits dans la User Story sont satisfaits.
- [ ] **Documentation technique** : Mise à jour du [Google Drive de documentation](https://drive.google.com/drive/folders/1YkQH3waGJEB6i7TFJhBOgM7wXiRyeIJW) si des changements de configuration ou de variables d'environnement ont eu lieu.
- [ ] **Ticket mis à jour** : Le ticket Jira est renseigné avec le lien de la PR et passé à l'état "Done".

---

## 2. Critères Spécifiques par Brique Technique

### 🍃 Backend — Java Spring Boot
- [ ] **API Documentation (OpenAPI / Swagger)** : Les endpoints modifiés ou créés sont annotés et documentés dans la spécification OpenAPI.
- [ ] **Gestion des erreurs & HTTP Status** : Les codes de retour HTTP (200, 201, 400, 401, 404, 500) et les payloads d'erreur suivent la norme du projet.
- [ ] **Base de données / Migrations** :
  - Les scripts de migration de BDD (postgreSQL) sont rédigés et testés.
  - Pas de modifications destructives directes sans rollback prévu.
- [ ] **Sécurité** : Les contrôles d'accès (Spring Security / JWT / Rôles) sont appliqués sur les nouveaux endpoints.

### ⚛️ Frontend Client — React (Application Lourde / Web)
- [ ] **Composants & Modularité** : Respect de la structure en composants (DRY, séparation logique/affichage).
- [ ] **Expérience utilisateur (UX) & Erreurs** :
  - Les états de chargement (*spinners/skeletons*) et la gestion des erreurs API sont affichés à l'utilisateur.
- [ ] **Rendu & Responsive** : L'interface s'affiche correctement selon la résolution cible de l'application.

### 📱 Frontend Mobile — React Native
- [ ] **Test Multi-Plateforme** :
  - [ ] Testé et validé sur **Android** (Émulateur ou appareil physique).
- [ ] **Gestion du Réseau & Mode Hors-Ligne** : L'application gère proprement la perte de connexion ou les timeouts réseau.
- [ ] **Performances** : Pas de ralentissements flagrants, re-renders intempestifs ou fuites de mémoire.
- [ ] **Périphériques & Permissions** : Les permissions mobiles (bluetooth, Permanent Notification) sont sollicitées correctement avec explication claire.

---

## 3. Engagements de l'Équipe

1. **Responsabilité partagée** : Toute l'équipe est collectivement garante du respect de cette DoD.
2. **Revue de PR sous 72h** : Pour éviter les goulots d'étranglement, chaque membre s'engage à repasser sur les Pull Requests ouvertes dans les jours qui suivent.
3. **Amélioration continue** : La DoD peut être révisée lors des réunions de rétrospective si des critères s'avèrent trop stricts ou insuffisants.