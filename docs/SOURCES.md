# Sources officielles et choix du laboratoire

Pages primaires consultées le **12 octobre 2026**. Les tutoriels, scénarios, contrats et barèmes sont des créations pédagogiques originales de PilotCrew. Les pages ci-dessous documentent les outils ou principes utilisés ; elles ne décrivent pas notre mock PSP.

| Source primaire | Usage dans le cours |
|---|---|
| [React — Managing State](https://react.dev/learn/managing-state) | Choix de la source d’état et partage de données entre composants. |
| [React — Synchronizing with Effects](https://react.dev/learn/synchronizing-with-effects) | Séparer actions utilisateur et synchronisation avec une ressource externe. |
| [React — useEffect](https://react.dev/reference/react/useEffect) | Nettoyage des effets, dépendances et protection contre les réponses tardives. |
| [TypeScript — Narrowing](https://www.typescriptlang.org/docs/handbook/2/narrowing.html) | Union discriminée et contrôle des variantes de l’interface. |
| [Vite — Getting Started](https://vite.dev/guide/) | Préparer un projet React/TypeScript et vérifier la version de Node compatible. |
| [Vite — server.proxy](https://vite.dev/config/server-options.html#server-proxy) | Proxy de développement pour appeler /api ; ce réglage ne constitue pas un déploiement. |
| [W3C WAI — Forms Tutorial](https://www.w3.org/WAI/tutorials/forms/) | Libellés, regroupement des choix, instructions et erreurs accessibles. |
| [Vitest — Getting Started](https://vitest.dev/guide/) | Exécution des tests frontend et intégration au projet Vite. |
| [Testing Library — About Queries](https://testing-library.com/docs/queries/about/) | Rechercher par rôle et nom accessible ; choisir les assertions asynchrones. |

Les versions et noms d’API pouvant évoluer, l’encadrant vérifie les liens et la combinaison exacte avant une nouvelle promotion. Java 21 et Spring Boot 4.1.1 sont fixés pour ce cursus ; les versions JavaScript sont celles du package-lock.json validé. La version de JUnit est gérée par le parent Spring Boot ; le cours ne prescrit pas de mélanger une ancienne configuration de tests avec Boot 4.

La répartition Java / React, les interfaces de paiement, l’intégration et la rigueur sont des thèmes issus de [l’annonce de référence](https://consultant.jean-michel.io/annonces/31738). Le choix Spring Boot, TypeScript, Vite, tests et protocole HMAC local appartient à la conception pédagogique. Aucune source ne transforme les 27 heures de ce parcours en expérience senior.
