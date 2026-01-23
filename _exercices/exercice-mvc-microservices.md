---
layout: default
title: "Patrons architecturaux - MVC & microservices"
nav_order: 12
has_toc: false
published: false
---
# Exercice : Recommandations de films (MVC + microservices)

## Objectifs

- Comprendre la **différence de niveau** entre l’architecture **interne** (MVC) et l’architecture **système** (microservices).
- Implémenter la **logique métier** d’un service **Catalogue** (MVC) et d’un service **Recommandations** (non-MVC).
- Expérimenter la **collaboration entre services** dans un modèle microservices
- Mettre en place des **tests simples** et raisonner sur la **résilience** (comportement si l’autre service est indisponible).

## Contexte

Vous disposez de **deux projets Maven** utilisant Spring Boot pour gérer, entre autres, la communication via services REST. Les contrôleurs REST sont déjà fournis et n'ont pas à être modifiés afin de pouvoir se concentrer sur l'implémentation et l'architecture des services.

- **catalogue-service** (pattern **MVC** à l’interne)Expose une liste de films avec `id`, `titre`, `genre`, `popularite`.Le dépôt **en mémoire** est à compléter (version squelette).Endpoints (déjà câblés) :

  - `GET /films`
  - `GET /films?genre=Action`
  - `GET /films/{id}`
- **recommendations-service** (pattern **non‑MVC**, “service layer only”)Calcule un **Top N** (N=3) par *genre* en **appelant** le service Catalogue (client fourni) ou en **lisant** un fichier `films.json` (variante).Endpoint (déjà câblé) :

  - `GET /recommendations?genre=Action`

> Le but est de **vivre** l’architecture : un service peut être MVC, un autre non, **et pourtant** ils coopèrent proprement.

## Étapes préparatoires

### 1. Clonez les dépôts de l’exercice

> Utilisez l’une des deux URLs (SSH ou HTTPS) lorsque vous recevrez vos dépôts.
> *(Remplacez les placeholders ci-dessous par les vraies URLs de votre classe.)*

```bash
# Catalogue
git clone <repo ici>
# ou
git clone <repo ici>

# Recommandations
git clone <repo ici>
# ou
git clone <repo ici>
```

### 2. Lancez chaque projet Java

Dans **chaque** dépôt (un terminal par service) :

```bash
mvn clean package
mvn spring-boot:run
```

- **Catalogue** démarre par défaut sur **:8080**
- **Recommandations** démarre par défaut sur **:8081**

> Si besoin, vous pouvez surcharger l’URL du Catalogue côté Recommandations avec :
> `-Dspring-boot.run.jvmArguments="-DCATALOGUE_URL=http://localhost:8080"`

### 3. Familiarisez-vous avec les contrôleurs fournis

- **Ne modifiez pas** les contrôleurs : ils servent à **isoler l’architecture** des détails REST.
- Concentrez-vous sur les **services** (métier) et la **persistance** (dépôt en mémoire).

---

## 1. Service de catalogue (`catalogue-service`)

On désire implémenter un service ayant la responsabilité d'organiser un catalogue de films et pouvant, par exemple, servir de base à une plate-forme de diffusion (*streaming*).

### 1.1. Étudiez la structure interne de **catalogue-service**

- Pour chaque rôle du MVC (modèle, vue et contrôleur), identifiez la ou les classes correspondantes:

  - **Modèle** : quelles classes représentent les entités métier, leur manipulation et leur persistance ?
  - **Vue** : quelles classes sont responsables de la préparation / présentation de la réponse au client ?
  - **Contrôleur** : Quelle classe reçoit les requêtes, les aiguille vers la logique métier et retourne la réponse correspondante ?

### 1.2. Complétez la **persistance** du Catalogue

- Implémentez un **dépôt en mémoire** `FilmRepository` et sa **configuration**.
- Préchargez au démarrage **au moins 5 films** variés (genre, popularité).
- Implémentez :
  - `findAll()`
  - `findByGenre(String genre)`
  - `findById(Integer id)`

> **Question de complexité** : Quelle est la complexité **grand O** des opérations de lecture dans votre dépôt en mémoire ? Justifiez.

### 1.3. Implémentez la **logique métier** du catalogue

On suppose que la première version de notre catalogue de films s'adresse à des enfants. Ainsi, on voudra s'assurer que, même s'il est possible que notre base de données contienne des films qui ne sont pas destinés aux enfants, notre implémentation de service empêche les enfants d'avoir accès aux films de genre `Horreur` et `Adulte` .

- Créez une implémentation de `FilmService` nommée `FilmServiceEnfants`.
- Dans `FilmServiceEnfants`, implémentez les méthodes requises par l'interface `FilmService`
  - Assurez-vous que toutes les méthodes excluent les films appartenant aux genres `Horreur` et `Adulte` des résultats
- - Assurez-vous que les **id inexistants** renvoient une **réponse vide** ou `null`
- Dans le contexte du MVC, pourquoi est-il important que cette logique d'exclusion appartienne à la classe `FilmService` plutôt...
  - ... qu'à la classe `FilmController` ?
  - ... qu'à la classe `FilmMapper` ou `FilmDto` ?

### 1.4. Implémentez la logique de conversion dans `FilmMapper`

* À quoi sert la distinction entre un objet `Film` et un objet `FilmDto` dans le contexte du MVC ?

## 2. Service de recommandations (`recommendations-service`)

On désire maintenant ajouter à notre service de catalogue la possibilité de faire des recommandations basées sur la popularité de certains films.

### 2.1. Comparez deux architectures possibles

Quels seraient les avantages et les inconvénients des solutions suivantes...

- Ajouter la fonctionnalité de recommandations directement dans le service de catalogue ?
  - Pensez, entre autres, à la complexité liée aux bases de données et à la communication entre les services...
- Ajouter la fonctionnalité de recommandations dans un service séparé (donc un projet complètement distinct) ?
  - Pensez, entre autres, à l'ajout de nouvelles fonctionnalités au fil du temps, à la facilité de déploiement et à la possibilité d'utiliser des langages ou technologies différentes pour différents services...

Laquelle des architectures ci-haut correspond à une architecture par microservices ? Pourquoi ?

### 2.2. Implémentez l’algorithme de **recommandation**

- Dans `RecommendationEngine`, implémentez `recommend(String genre)` :
  - Récupère la **liste** du Catalogue,
  - Trie par **popularité décroissante**,
  - Retourne le **Top 3**.
- Que se passe-t-il si **le genre est vide** ou non fourni ? Proposez un **comportement** raisonnable et justifiez.

### 2.3. Gérez l’**indisponibilité** du service de catalogue

Simulez une panne en éteignant le service de catalogue.

- Quel **message** renvoie le service de recommandations ?
- Quel comportement pourriez-vous implémenter pour gérer le cas où le catalogue est en panne de façon plus gracieuse ?
- Décrivez comment vous **documenteriez** ce comportement pour un autre client (contrat).

## Pistes de réflexion

- **Niveaux** d’architecture : qu’est-ce qui, dans cet exercice, illustre clairement que **MVC** (interne) et **microservices** (système) ne se situent **pas au même niveau** ?
- **Frontières métier** : la séparation Catalogue vs Recommandations vous paraît-elle **naturelle** ? Pourquoi ? Aurait-on pu séparer autrement ?
- **Données par service** : que changerait une **base partagée** entre les deux services ? Quels seraient les risques et les avantages ?
- **Évolution** : si l’on remplaçait Recommandations par un **service statistique** (moyenne de popularité par genre), qu’est-ce que cela changerait dans le **contrat** et dans les **dépendances** ?
