---
layout: default
title: "Listes et tableaux"
parent: "Structures de données"
nav_order: 1
published: false
---

# Listes

## Types de listes

Les listes sont des structures de données linéaires permettant de stocker des collections d'éléments. Elles sont fondamentales en programmation et existent sous plusieurs formes : tableaux, listes dynamiques (ArrayList), et listes chaînées.

| Type de liste            | Taille dynamique | Accès direct | Insertion rapide | Suppression rapide | Complexité mémoire |
|--------------------------|------------------|--------------|------------------|--------------------|--------------------|
| Tableau (Array)          | ❌               | ✅           | ❌               | ❌                 | Faible             |
| ArrayList                | ✅               | ✅           | ⚠️               | ⚠️                 | Moyenne            |
| Liste chaînée (simple)   | ✅               | ❌           | ✅               | ✅                 | Élevée             |
| Liste chaînée (double)   | ✅               | ❌           | ✅               | ✅                 | Élevée             |


## Algorithmes sur les listes

Les algorithmes fondamentaux sur les listes incluent l'ajout, la suppression, la recherche et le tri. Leur efficacité dépend du type de liste utilisé.

| Algorithme  | Array | ArrayList | LinkedList Simple | LinkedList Double |
|------------|-------|-----------|--------------------|--------------------|
| Ajout      | ⚠️    | ✅        | ✅                 | ✅                 |
| Suppression| ⚠️    | ✅        | ✅                 | ✅                 |
| Recherche  | ✅    | ✅        | ✅ (linéaire)      | ✅ (linéaire)      |
| Tri        | ✅    | ✅        | ⚠️ (complexe)      | ⚠️ (complexe)      |