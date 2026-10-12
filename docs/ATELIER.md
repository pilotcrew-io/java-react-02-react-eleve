# Lab 02 — Une interface de commande accessible

**4 h 30 · dominante React.** La commande de l’API doit devenir compréhensible pour une personne qui ne lit ni JSON ni logs. Construire un écran simple qui indique ce qui est demandé, ce qui est en cours et ce qui a réellement été confirmé par le serveur.

## 1. Définir les états avant les composants — 20 min

Dessiner six vues : chargement du catalogue, catalogue vide, erreur de chargement, formulaire prêt, création en cours, confirmation. Ajouter le cas d’échec de création avec un message et une action possible. Écrire le texte exact de chaque bouton. Une personne au clavier doit pouvoir choisir la quantité, soumettre et comprendre le résultat.

Séparer l’état de chargement du catalogue de l’état de création d’une commande. Éviter une collection de booléens qui permettrait d’afficher simultanément « confirmation » et « échec ». Dans le journal, donner un exemple d’état impossible et la façon dont votre structure l’empêche.

## 2. Préparer React, TypeScript et Vite — 40 min

Créer `frontend/` avec un projet React/TypeScript adapté aux versions validées par l’encadrant. Conserver `package-lock.json`. Prévoir les scripts `dev`, `build` avec vérification TypeScript, et `test` avec Vitest. Organiser au minimum un module de contrat, un module d’accès API, le composant de page et des composants de formulaire/confirmation.

Configurer le serveur Vite sur `127.0.0.1:5173` et son proxy `/api` vers `http://127.0.0.1:8080`. Le frontend appelle des URLs relatives comme `/api/products`. Vérifier l’adresse réelle des requêtes dans l’onglet Réseau. Le proxy simplifie uniquement le développement local.

Décrire `Product`, `Order` et une réponse d’erreur. Un type TypeScript ne transforme pas magiquement un JSON en donnée valide : dans le module API, vérifier la présence et le type des champs indispensables avant de considérer la réponse comme utilisable. Centraliser les erreurs HTTP et prévoir un message de secours pour une réponse qui n’est pas du JSON.

```bash
npm --prefix frontend install
npm --prefix frontend run dev
```

Ces commandes s’exécutent après création des fichiers du projet ; la copie élève seule n’est pas une application installable.

## 3. Charger sans masquer les problèmes — 50 min

Faire charger le catalogue par un effet lié au composant de page. Afficher un texte d’attente, puis soit les produits, soit un message vide, soit une erreur avec bouton « Réessayer le chargement ». Vérifier `response.ok` avant d’utiliser un résultat comme succès. Ne pas substituer silencieusement un produit codé en dur lorsqu’une requête échoue.

Prévoir le nettoyage au démontage et protéger l’état contre une réponse devenue obsolète. Vous pouvez employer un AbortController et un marqueur de requête active ; l’idée à prouver est que le résultat d’une ancienne demande n’écrase pas la plus récente. Un abandon n’est pas présenté comme une panne utilisateur.

Dans les tests, fournir une réponse vide et un rejet contrôlé, puis une réponse réussie après nouvelle tentative. En manipulation manuelle, arrêter brièvement votre API, observer le message, la relancer et utiliser le bouton prévu. Le rechargement complet de la page ne remplace pas le comportement demandé.

## 4. Créer une commande compréhensible — 60 min

Construire un formulaire HTML contrôlé. Utiliser un libellé lié au champ de quantité, un groupe sémantique si plusieurs produits sont proposés, un bouton submit et une indication « quantité entière de 1 à 5 ». L’utilisateur voit un aperçu du total calculé depuis le catalogue chargé. Cet aperçu n’est pas transmis comme prix : le JSON envoyé reste uniquement `{productId, quantity}`.

Déclencher POST `/api/orders` dans l’action de soumission, jamais dans un effet de montage. Pendant la demande, indiquer « Création en cours » et empêcher une nouvelle soumission de ce formulaire. À la réponse 201, afficher la référence et le montant **retournés par le serveur**. Pour une erreur 400, relier l’explication au champ concerné quand c’est possible ; pour une panne réseau, conserver la saisie et indiquer que la création n’a pas pu être confirmée.

Le POST de création de commande du lab 01 n’est pas idempotent : une réponse perdue peut cacher une commande créée. Pour ce lab, afficher cette incertitude et demander une nouvelle action explicite, sans boucle de retry automatique. Le lab suivant traite une clé de reprise pour une tentative de paiement.

## 5. Vérifier accessibilité et courses de réponses — 65 min

Parcourir l’écran avec Tab, Maj+Tab, Entrée et Espace selon les contrôles. Le focus doit rester visible ; les libellés doivent permettre d’identifier les champs. Employer une zone de statut pour le résultat asynchrone et une zone d’alerte pour une erreur qui exige une action, sans annoncer chaque rendu en boucle. Quand une erreur de champ apparaît, rendre son lien avec le champ compréhensible (`aria-describedby`, et `aria-invalid` si pertinent).

Écrire au moins six tests de comportement : attente puis catalogue, catalogue vide, échec puis reprise, quantité invalide, soumission nominale avec confirmation serveur, et réponse ancienne ignorée. Le test nominal intercepte la requête et vérifie qu’aucun montant n’est envoyé. Un test peut renvoyer un total volontairement distinct de l’aperçu ; l’écran doit respecter le retour serveur et signaler la différence si l’utilisateur doit en tenir compte.

Choisir les éléments par rôle et nom accessible. Ne vérifier ni le nom d’une fonction interne ni la position d’un `div`. Pour le cas de réponse tardive, contrôler deux promesses : la deuxième réponse arrive d’abord ; résoudre ensuite la première et vérifier que l’écran garde la seconde. Aucun délai arbitraire n’est nécessaire pour cette preuve.

## 6. Construire, relire et expliquer — 35 min

```bash
npm --prefix frontend run test -- --run
npm --prefix frontend run build
```

Le build doit vérifier TypeScript puis créer les fichiers distribuables. Un build Vite réussi ne vérifie pas que `/api` sera correctement routé sur un hébergement : cette séance reste locale. Le pair observe le navigateur réel pendant que l’élève décrit une donnée qui descend par props et une action qui remonte par callback.

Rendre captures des états nominal et erreur, rapport de tests, extrait de requête sans prix client, contrôle au clavier et journal. Arrêter les deux serveurs. L’extension hors temps est un thème visuel plus riche ; elle ne remplace pas l’état vide ou une erreur exploitable.

## Déroulé minuté — 270 minutes

| Plage | Activité | Durée |
|---|---|---:|
| 00:00–00:20 | Décrire les états utilisateur et le parcours au clavier | 20 min |
| 00:20–01:00 | Créer le projet Vite, les types et la décomposition des composants | 40 min |
| 01:00–01:50 | Charger le catalogue et gérer chargement, vide, erreur et nouvelle tentative | 50 min |
| 01:50–02:50 | Créer le formulaire contrôlé et une confirmation issue du serveur | 60 min |
| 02:50–03:55 | Traiter accessibilité, réponse tardive et tests de comportement | 65 min |
| 03:55–04:30 | Construire le frontend, faire relire le parcours et réunir les preuves | 35 min |

## Contrat commun du fil rouge

La boutique **PilotCrew Démo** ne vend rien. Elle présente le produit `demo-ticket`, libellé « Atelier fictif », à `unitAmountMinor: 2500`, devise `EUR`, `fictional: true`. Une quantité entière de **1 à 5** produit une commande dont le montant est calculé par le serveur. Dans cette simulation EUR seulement, 2500 unités mineures s’affichent 25,00 € fictifs. Aucun autre nombre de décimales ni aucune conversion de devise n’est traité.

| Objet | Champs publics attendus |
|---|---|
| Product | `id`, `label`, `unitAmountMinor`, `currency`, `fictional` |
| Order | `id`, `productId`, `quantity`, `amountMinor`, `currency`, `fictional` |
| Payment | `id`, `orderId`, `amountMinor`, `currency`, `method`, `status`, `fictional` |

Le corps de création de commande accepte uniquement `productId` et `quantity`. Le corps de création de paiement accepte uniquement `method`. Un montant, une devise ou un statut ajoutés par le client ne doivent jamais devenir une autorité : **ce contrat les refuse en 400**. Le code utilise les identifiants retournés, jamais un identifiant d’exemple comme s’il existait déjà.

| Route | Résultat contractuel |
|---|---|
| `GET /api/products` | 200, tableau de produits fictifs |
| `POST /api/orders` | 201, commande créée et en-tête Location |
| `GET /api/orders/{id}` | 200, commande ; 404 si référence absente |
| `POST /api/orders/{id}/payments` | À partir du lab 03 : 202, tentative PENDING ; Idempotency-Key obligatoire |
| `GET /api/payments/{id}` | À partir du lab 03 : 200, état serveur ; 404 si référence absente |
| `POST /api/webhooks/mock-psp` | À partir du lab 04 : réception d’un événement signé par le simulateur local |

Les erreurs structurées emploient `application/problem+json` et au moins `type`, `title`, `status`, `detail`, `code`. `code` est une extension de ce projet. Le texte est destiné à l’utilisateur ; aucune pile d’exception ne sort dans la réponse. Les codes HTTP du cours sont des choix de contrat précis ; ils ne décrivent pas toutes les API de paiement existantes.

Toutes les données métier sont en mémoire dans une JVM : un redémarrage les efface. Cette limite est visible dans la documentation et dans les scénarios. Le cours ne met en place ni identité client, ni base durable, ni gestion de stock, ni remboursement, ni autorisation financière réelle.
