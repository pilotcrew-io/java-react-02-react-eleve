# Évaluation — jr-02-react · 20 points

| Critère | Points | Preuve attendue |
|---|---:|---|
| Composants, types et états cohérents | 3 | Structure expliquée ; pas de succès et erreur simultanés ; contrôle minimal de la réponse JSON. |
| Formulaire et confirmation issus du contrat | 4 | POST sans montant, saisie contrôlée, total et référence de réponse serveur. |
| Chargement, vide, erreur et reprise | 4 | Captures ou tests des quatre situations, saisie conservée lors d’échec. |
| Clavier, libellés et annonces utiles | 3 | Parcours manuel décrit et tests par rôle/nom accessible. |
| Tests de comportement et réponse obsolète | 4 | Au moins six cas réels, promesses contrôlées et aucune attente arbitraire. |
| Build, journal et revue | 2 | Build TypeScript/Vite, versions, explication du flux et limites de POST commande. |
| **Total** | **20** | |
## Règles de restitution

Un fichier présent n’obtient pas à lui seul tous les points : montrer son comportement et pouvoir l’expliquer. Les cas négatifs sont aussi importants que le nominal. Le code rendu ne contient aucune vraie donnée bancaire ou identité PSP ; tous les scénarios restent locaux et fictifs.

Associer chaque preuve à la version remise. Le journal mentionne l’acquis repris du lab précédent et toute base fournie par l’encadrant. Une revue locale est recevable lorsqu’aucun dépôt distant n’est utilisé. Ne pas créer de fausse URL de commit, de pull request ou de rapport.

En cas de panne d’outillage documentée, l’encadrant distingue les critères vérifiés sur un poste de secours, les contrôles relus mais non exécutés et les preuves reportées. Un test navigateur non exécuté ne reçoit pas l’étiquette « E2E réussi ». Une reprise de preuve peut être organisée ; le résultat obtenu reste daté et attribué au bon environnement.

Pour valider la séance, le formateur dispose d’un ensemble fonctionnel sur les objectifs obligatoires, de tests pertinents, d’un diagnostic expliqué et de limites honnêtes. Une extension ne compense pas un montant client accepté, une duplication masquée ou un faux succès affiché.

## Questions d’oral

1. Distinguer état serveur et état du formulaire.
2. Expliquer pourquoi un type TypeScript ne valide pas un JSON.
3. Expliquer une réponse tardive et le nettoyage choisi.
