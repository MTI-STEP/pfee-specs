# Use Cases

## UC01 - Consultation du tableau de bord patient
Acteur : Patient  
Description : Le patient consulte son état sensoriel et ses alertes sur l’application mobile.
Déclencheur : Le patient ouvre l’application.
Flux principal :
1. Le patient ouvre l’app.
2. L’application récupère les données récentes.
3. Le patient visualise les indicateurs de santé et les alertes.
4. Le patient applique les recommandations.

## UC02 - Alerte de surpression plantaire
Acteur : Patient Digifeet  
Description : Le système détecte une surpression et alerte le patient avant la plaie.
Déclencheur : Un capteur envoie une valeur de pression critique.
Flux principal :
1. Le dispositif mesure la pression.
2. Les données sont transmises au SaaS.
3. Une règle de seuil déclenche une alerte.
4. Le patient reçoit une notification.

## UC03 - Suivi et paramétrage par le praticien
Acteur : Praticien  
Description : Le praticien consulte un dashboard et ajuste les paramètres du dispositif.
Déclencheur : Le praticien se connecte au dashboard.
Flux principal :
1. Le praticien accède à la fiche patient.
2. Il consulte les données de capteurs, les tendances et le score IA.
3. Il modifie les paramètres adaptés au patient.
4. Il enregistre les réglages.

## UC04 - Historique et score de santé
Acteur : Praticien  
Description : Le praticien suit l’évolution des patients à l’aide d’un score de santé.
Déclencheur : Le praticien consulte le suivi périodique.
Flux principal :
1. Le système calcule un score basé sur les données.
2. Le score est affiché avec les tendances.
3. Le praticien peut comparer plusieurs périodes.