# Dépannage — jr-02-react

Relever la première erreur, la commande, la version et le contexte. Une correction conserve le comportement demandé et ajoute ou rejoue une preuve ; retirer une assertion ne répare pas le problème.

| Symptôme | Cause plausible | Diagnostic discriminant | Résolution attendue |
|---|---|---|---|
| Le catalogue est remplacé par la page HTML | /api est servi par Vite sans proxy correct | Observer URL, Content-Type et corps dans Réseau | Corriger server.proxy et utiliser une URL relative cohérente. |
| HTTP 500 est traité comme un catalogue | Le code ne vérifie pas response.ok | Contrôler le statut avant response.json et le traitement du résultat | Traduire les réponses non 2xx vers un état d’erreur explicite. |
| Deux commandes sont créées au montage | Le POST est placé dans un effet | Comparer l’événement de soumission aux requêtes Réseau | Déplacer la création dans onSubmit ; garder le chargement dans un effet nettoyé. |
| Un résultat ancien remplace le nouveau | Les requêtes concurrentes ne sont pas distinguées | Résoudre deux promesses dans l’ordre inverse | Ignorer une réponse obsolète et nettoyer la requête active. |
| Le montant affiché diverge du serveur | La confirmation réutilise l’aperçu du panier | Renvoyer un total distinct depuis le double API du test | Afficher la commande de réponse et traiter la différence explicitement. |
| Le test ne trouve pas le champ par son nom | Le label n’est pas relié à l’input | Inspecter nom accessible et attributs htmlFor/id | Employer une association HTML correcte ; ne pas remplacer par un sélecteur fragile. |
| Le build passe mais aucun test ne tourne | Le script build ne lance pas Vitest | Lire scripts et le nombre de tests du rapport | Exécuter séparément la suite et la construction TypeScript/Vite. |

Si un port est occupé, identifier le processus avant de l’arrêter. Ne jamais arrêter globalement toutes les JVM ou tous les processus Node d’un poste partagé. Si une commande dépend d’un fichier demandé dans l’atelier, le construire d’abord : les dépôts élèves sont des supports, pas des solutions prêtes à lancer.
