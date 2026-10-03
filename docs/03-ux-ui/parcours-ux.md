# Parcours UX (optionnel)

Expérience utilisateur détaillée, points de friction, améliorations possibles.

```mermaid

flowchart TD
    A@{ shape: stadium, label: "Ecran de connexion" } --> B{Choix du type de compte}
    style A fill:#f9f

    B -->|Client| C[Dashboard patient]
    B -->|Professionnel| D[Liste patients]

    C --> G{Choix de la tab}

    G --> |FAQ|H{Question rechcerchée trouvée}
    G --> |Accueil|E{Notification sur le journal d'alerte ?}
    G --> |Profil|I[Consulter ses données et le contact de son professionnel de santé]

    E --> |Oui|F[Ouverture du journal]

    H --> |Oui|J[Visualisation de la reponse]

    I --> K{Se deconnecter ?}

    K --> |Oui|A
```
