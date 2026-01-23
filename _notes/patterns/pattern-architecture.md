---
layout: default
title: Patrons architecturaux
parent: Patrons de conception
nav_order: 1
---

# Patrons architecturaux

Les patrons architecturaux définissent l’organisation globale d’un système logiciel, sa structure à grande échelle et la manière dont ses composantes interagissent. Leur objectif est de guider la construction d’architectures robustes, évolutives et cohérentes. Ces patrons ont donc une portée plus large (ou plus haut-niveau) que les patrons comportementaux, structurels et de création, car ils dictent l'organisation d'une composante complète ou même d'un système complet. Autrement dit, une application ou un système construits suivant un patron architectural peut très bien aussi renfermer l'utilisation de plusieurs autres patrons de conception plus granulaires.

## Cas d'utilisation
Les patrons architecturaux répondent à des problématiques de structuration d’application, de séparation des responsabilités et de gestion de la complexité d’ensemble. Ils améliorent la modularité, facilitent les tests et assurent une évolution plus prévisible du système. Ils peuvent intervenir à différents *niveaux* de l'architecture d'une application ou d'un système.

**Niveaux?**

En développement logiciel, *architecture* peut désigner à la fois :
- **la structure interne d’une application** : organisation des couches, dépendances, responsabilités
- **la structure d’un système distribué** : frontières entre services, communication, déploiement, données, observabilité

Ces deux préoccupations sont complémentaires mais n’opèrent pas à la même échelle. On parle donc de niveaux d’architecture.

### Niveau *système* (macro‑architecture)
Définit **comment plusieurs applications/services coopèrent** pour former un produit complet.

**Définit :**
- **Frontières et responsabilités** : groupement de fonctionnalités selon la logique métier (*business logic*), par exemple *Catalogue*, *Recommandations*, etc.
- **Communication** entre processus, c'est-à-dire comment les différents services échangent des données, par exemple *APIs*, *messages*, *fichiers*, *flux ("streams")*).
- **Données** : appartenance par service, c'est-à-dire quel service gère quelle entité métier, et comment assurer la synchronisation et la cohérence.
- **Déploiement** : indépendance, pipelines, scalabilité, résilience.

**Exemples courants :**
- [Microservices](../patterns/pattern-microservices)
- Monolithe (modulaire ou non)
- SOA (*Service-Oriented Architecture*)
- Architecture événementielle
- Architecture à n‑tiers (*n-tier architecture*) : couches déployées séparément

{: .highlight}
> Une *macro‑architecture* n'impose **rien** quant à l’organisation interne de chaque service. Chaque service peut employer indépendamment MVC, *Hexagonal*, *Clean Architecture*, ou n'importe quelle autre modèle d'architecture interne.

### Niveau *application* (architecture interne)
Définit **comment organiser le code à l’intérieur d’un service** pour garantir clarté, testabilité et séparation des responsabilités.

**Définit :**
- **Les couches** (présentation, application, domaine, infrastructure)
- **Les dépendances** (direction, inversion, interfaces, *adapters*)
- **Les contrats internes** (DTO, *ports*)

**Exemples courants :**
- [MVC](../patterns/pattern-mvc) ;
- *Hexagonal* (*Ports & Adapters*) ;
- *Clean Architecture* ;
- MVVM.

{: .highlight}
> L'*architecture interne* organise la logique interne d’un processus. Elle ne décide pas *comment* plusieurs processus coopèrent.
