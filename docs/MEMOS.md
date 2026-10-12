# Mémos 02 — Une interface expose un état

## Données métier et état de l’écran

Une commande est un fait métier fourni par l’API. Le texte saisi, l’onglet ouvert ou le message d’attente sont des états d’interface. Dans notre page, le catalogue vient du serveur ; la quantité en cours de saisie vient du formulaire ; la confirmation vient de la réponse de création. Les dupliquer sans règle de synchronisation crée des contradictions.

Une union discriminée comme `idle | submitting | confirmed | error` oblige à traiter une variante identifiée. Elle peut porter les données utiles à cette variante, par exemple la commande dans `confirmed`. Un état structuré ne dispense pas de tester les transitions, mais rend les situations incohérentes plus visibles à la compilation. [TypeScript](https://www.typescriptlang.org/docs/handbook/2/narrowing.html).

## Props, événements et état partagé

Placer l’état au niveau qui en a besoin, puis fournir aux composants leurs données et callbacks. Un composant Quantité n’a pas à connaître le dépôt mémoire Java. La page orchestre le formulaire et la confirmation. Un petit fil rouge n’exige pas de gestionnaire d’état global supplémentaire. [Organisation de l’état React](https://react.dev/learn/managing-state).

## Un type ne valide pas le réseau

`response.json()` donne une valeur obtenue à l’exécution. Une assertion `as Order` persuade le compilateur ; elle ne vérifie ni `amountMinor` ni `currency`. Le module API doit savoir reconnaître les données minimales attendues et signaler une réponse non conforme. Le cours évalue ce contrôle à la frontière, pas la construction d’un moteur de validation générique.

## Action et synchronisation

La soumission suit une intention précise de l’utilisateur : elle appartient au gestionnaire du formulaire. Un effet sert notamment à synchroniser la page avec le chargement du catalogue et doit prévoir son nettoyage. Un montage répété en développement révèle certains effets mal nettoyés ; déplacer une création de commande dans un effet peut déclencher une action métier inattendue. [Effets React](https://react.dev/learn/synchronizing-with-effects).

## Le temps fait partie du comportement

Une requête peut arriver après une autre. L’écran doit reconnaître quel résultat est encore pertinent. Annuler une lecture peut libérer une ressource, mais annuler l’attente du navigateur ne prouve pas qu’une écriture serveur n’a pas eu lieu. C’est pourquoi l’échec réseau d’un POST doit être décrit avec soin et n’entraîne pas automatiquement une nouvelle création.

## Accessibilité et preuves

Un champ associé à son label, une erreur reliée au champ et un bouton sémantique rendent le parcours repérable. La même structure aide les tests à chercher ce qu’une personne peut nommer. Une capture ne prouve pas le clavier ; un test DOM ne remplace pas toute la validation assistive. Dans le cours, consigner les contrôles réellement réalisés. [W3C WAI](https://www.w3.org/WAI/tutorials/forms/).

## Questions de compréhension

1. Qu’est-ce qui change si la réponse arrive deux secondes après le changement de produit ?
2. Pourquoi l’aperçu du montant n’est-il pas envoyé comme montant de commande ?
3. Quand un HTTP 404 passe-t-il dans la branche succès d’une promesse fetch mal gérée ?
4. Quel code décide le libellé du message et quel code décide le total ?
5. Pourquoi désactiver un bouton n’est-il pas une garantie d’idempotence serveur ?
