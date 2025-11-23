---
layout: default
title: "Structures de données - semaine 1"
parent: "Structures de données"
nav_order: 2
published: false
---

### 2. ArrayList

### 2.1. Créez une nouvelle implémentation de l'interface `GestionnaireJoueurs` appelée `GestionnaireJoueursArrayList`
Cette implémentation doit utiliser une `ArrayList` pour gérer la liste au lieu d'une gestion manuelle.
- Gardez une référence vers une nouvelle `ArrayList` comme champ dans la classe.
- Toutes les opérations des questions suivantes manipuleront cette liste.
- Théoriquement, avec cette nouvelle implémentation, quelles opérations devraient être...
  - Plus performantes qu'avec `GestionnaireJoueursLinkedList` ?
  - Moins performantes qu'avec `GestionnaireJoueursLinkedList` ?
  - D'une performance à peu près égale par rapport à `GestionnaireJoueursLinkedList` ?

### 3. Concurrence (*thread-safety*)


## Bonus
- Ajoutez une **stratégie thread-safe** avec `CopyOnWriteArrayListStrategy`.
- Expliquez les avantages et inconvénients.

## Bonus
- Ajouter un remove avec une regex

## Bonus
- Trier dans un ordre différent avec un Comparator