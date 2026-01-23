---
layout: default
title: Patrons architecturaux
parent: Patrons de conception
nav_order: 1
---

# Patrons architecturaux

Les patrons architecturaux définissent l’organisation globale d’un système logiciel, sa structure à grande échelle et la manière dont ses composantes interagissent. Leur objectif est de guider la construction d’architectures robustes, évolutives et cohérentes.

## Cas d'utilisation
Ces patrons répondent à des problématiques de structuration d’application, de séparation des responsabilités et de gestion de la complexité d’ensemble. Ils améliorent la modularité, facilitent les tests et assurent une évolution plus prévisible du système. Ils peuvent intervenir à différents *niveaux* de l'architecture d'une application ou d'un système.

**Niveaux?**
En développement logiciel, *architecture* peut désigner à la fois :
- **la structure interne d’une application** : organisation des couches, dépendances, responsabilités
- **la structure d’un système distribué** : frontières entre services, communication, déploiement, données, observabilité

Ces deux préoccupations sont complémentaires mais n’opèrent pas à la même échelle. On parle donc de niveaux d’architecture.

### Niveau *système* (macro‑architecture)
Définit **comment plusieurs applications/services coopèrent** pour former un produit complet.

**Caractéristiques clés :**
- **Frontières et responsabilités** par *capabilité métier* (ex. *Catalogue*, *Recommandations*).
- **Communication** entre processus (APIs, messages, fichiers, *streams*).
- **Données** : ownership par service, synchronisation/consistance.
- **Déploiement** : indépendance, pipelines, scalabilité, résilience.

**Exemples courants :**
- [Microservices](../patterns/pattern-microservices) ;
- Monolithe *modulaire*
- SOA
- Architecture événementielle
- *n‑tier* (couches déployées séparément)

{: .highlight}
> Une *macro‑architecture* ne présuppose **rien** de l’organisation interne de chaque service. Un service peut employer MVC, *Hexagonal*, *Clean Architecture*, ou une simple couche fonctionnelle.

### Niveau *application* (architecture interne)
Définit **comment organiser le code à l’intérieur d’un service** pour garantir clarté, testabilité et séparation des responsabilités.

**Caractéristiques :**
- **Couches** (présentation, application, domaine, infrastructure).
- **Dépendances** (direction, inversion, interfaces, *adapters*).
- **Contrats internes** (DTO, *ports*). 

**Exemples courants :**
- [MVC](../patterns/pattern-mvc) ;
- *Hexagonal* (*Ports & Adapters*) ;
- *Clean Architecture* ;
- MVVM.

{: .highlight}
> L'*architecture interne* organise la logique interne d’un processus. Elle ne décide pas *comment* plusieurs processus coopèrent.
