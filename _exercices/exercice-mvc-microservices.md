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

Vous disposez de **deux projets Spring Boot 3.5.9 (Maven)**. Les **contrôleurs REST sont fournis** pour vous éviter d’apprendre REST : vous vous concentrez sur la **logique interne** des services.

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
# Catalogue (squelette)
git clone git@github.com:VOTRE-ORG/catalogue-service-student.git
# ou
git clone https://github.com/VOTRE-ORG/catalogue-service-student.git

# Recommandations (squelette)
git clone git@github.com:VOTRE-ORG/recommendations-service-student.git
# ou
git clone https://github.com/VOTRE-ORG/recommendations-service-student.git
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

### 1.1. Étudiez la structure interne de **catalogue-service**

- Où se situent **Modèle / Service / Dépôt** dans le projet ?
- Quelles responsabilités sont associées à **chaque couche** ?
- Quelle est la **structure de données** minimale d’un `Film` (champ obligatoires) ?
- Où et comment effectuer la **conversion Entité → DTO** ?

### 1.2. Complétez la **persistance** du Catalogue (version squelette)

- Implémentez un **dépôt en mémoire** `FilmRepository` et sa **configuration**.
- Préchargez au démarrage **au moins 5 films** variés (genre, popularité).
- Implémentez :
  - `findAll()`
  - `findByGenre(String genre)`
  - `findById(Integer id)`

> **Question de complexité** : Quelle est la complexité **grand O** des opérations de lecture dans votre dépôt en mémoire ? Justifiez.

### 1.3. Implémentez la **logique métier** du Catalogue

- Dans `FilmService`, implémentez un **tri décroissant par popularité** pour `findByGenre`.
- Assurez-vous que les **id inexistants** renvoient une **réponse vide** (ou `null` côté service, DTO `null` mappé en 404 par le contrôleur si déjà prévu).
- Rédigez **2 tests unitaires** minimum (par ex. : *filtrage par genre*, *tri par popularité*).

## 2. Service de recommandations (`recommendations-service`)

### 2.1. Étudiez la structure interne de **recommendations-service**

- Où se trouvent **`RecommendationEngine`** (algorithme) et **`CatalogueClient`** (client vers l’autre service) ?
- Quels sont les **DTO** échangés ? Sont-ils **proprement découplés** du modèle interne du Catalogue ? Pourquoi est-ce souhaitable ?

### 2.2. Implémentez l’algorithme de **recommandation**

- Dans `RecommendationEngine`, implémentez `recommend(String genre)` :
  - Récupère la **liste** du Catalogue,
  - Trie par **popularité décroissante**,
  - Retourne le **Top 3**.
- Que se passe-t-il si **le genre est vide** ou non fourni ? Proposez un **comportement** raisonnable et justifiez (ex. Top 3 global).

### 2.3. Gérez l’**indisponibilité** du Catalogue (résilience minimale)

- Simulez une panne (éteindre Catalogue).
- Quel **message** renvoie Recommandations ?
- Quels **comportements alternatifs** proposez-vous (ex. 503 explicite, top « fallback » à partir d’un cache, message pédagogique) ?
- Décrivez comment vous **documenteriez** ce comportement pour un autre client (contrat).

### 2.4. Variante **sans REST** (optionnelle)

- Remplacez `CatalogueClient` par un **chargeur de fichier** `films.json` local (même structure que le DTO).
- Comparez les **avantages / limites** de cette approche (simplicité, couplage, réalisme microservices).

---

## Exercice Bonus

### A. **Contrôles de validité** côté Recommandations

- Genre inconnu → que faire ?
- Valeurs de popularité **hors bornes** (négatives, >100) → les ignorer ? les normaliser ?
- Documentez votre **stratégie** et testez-la.

### B. **Extension Top N**

- Rendez **N configurable** (paramètre de requête `limit`, valeur par défaut = 3).
- Ajoutez des tests pour `limit=1`, `limit>taille`, `limit≤0`.

### C. **Cache local** minimal

- Mettez en place un **cache en mémoire** (structure Java) avec **expiration simple** (ex. 60 s) pour éviter d’appeler Catalogue à chaque requête.
- Mesurez (manuellement) la **différence de comportement** en éteignant Catalogue pendant que le cache est encore valide.

---

## Pistes de réflexion

- **Niveaux** d’architecture : qu’est-ce qui, dans cet exercice, illustre clairement que **MVC** (interne) et **microservices** (système) ne se situent **pas au même niveau** ?
- **Frontières métier** : la coupe « Catalogue / Recommandations » vous paraît-elle **naturelle** ? Pourquoi ? Quelles autres coupes seraient possibles ?
- **Données par service** : que changerait une **base partagée** entre les deux services ? Quels **risques** (couplage, verrouillage, migrations) ?
- **Évolution** : si l’on remplaçait Recommandations par un **service statistique** (moyenne de popularité par genre), qu’est-ce que cela changerait dans le **contrat** et dans les **dépendances** ?
- **Tests d’intégration** : proposez un scénario de **test bout-en-bout** (Catalogue allumé, Recommandations qui appelle, vérification du Top N).
