---
layout: default
title: "Listes et tableaux"
parent: "Structures de données"
nav_order: 1
published: true
---

# Listes

En programmation orientée objet (POO), une **liste** est une structure de données qui permet de stocker une collection ordonnée d'objets. Chaque élément de la liste peut être accédé par son index, et la liste peut parfois, selon les implémentations, contenir des objets de types différents. Cependant, dans la pratique, les éléments sont très souvent du même type.

## Caractéristiques principales
- **Ordonnée** : les éléments sont stockés dans un ordre précis.
- **Indexée** : chaque élément peut être accédé via son index.
- **Mutable** : les listes peuvent être modifiées après leur création.

## Types de listes

Une liste peut, dans sa forme la plus simple, être représentée par un tableau. Il existe aussi des versions plus dynamiques appelées listes chaînées, qui peuvent être simples (chaînées dans un seul sens) ou doublement chaînées (navigables dans les deux sens).

| Type de liste            | Taille dynamique | Accès direct | Insertion rapide | Suppression rapide | Complexité mémoire |
|--------------------------|------------------|--------------|------------------|--------------------|--------------------|
| Tableau (Array)          | ❌               | ✅           | ❌               | ❌                 | Faible             |
| Liste chaînée            | ✅               | ❌           | ✅               | ✅                 | Élevée             |


## Opérations courantes sur les listes

| **Algorithme** | **Fonctionnalité**            | **Python**               | **Java**                     | **Description** |
|---------------|-------------------------------|--------------------------|------------------------------|-----------------|
| Ajout         | Ajouter un élément            | `append(objet)`          | `add(objet)`                 | Ajoute un élément à la fin de la liste. |
| Ajout         | Insérer à une position        | `insert(index, objet)`   | `add(index, objet)`          | Insère un élément à une position donnée. |
| Suppression   | Supprimer par index           | `pop(index)`             | `remove(index)`              | Supprime l’élément à l’index spécifié. |
| Tri           | Trier la liste                | `sort()`                 | `Collections.sort(liste)`    | Trie les éléments de la liste. |
| Recherche     | Vérifier la présence          | `objet in liste`         | `contains(objet)`            | Vérifie si un élément est présent dans la liste. |
| Recherche     | Trouver l’index d’un élément  | `index(objet)`           | `indexOf(objet)`             | Retourne l’index de la première occurrence. |
| Recherche & suppression   | Supprimer par valeur          | `remove(objet)`          | `remove(Object)`             | Supprime la première occurrence d’un élément. |
| Accès direct ou rehcherche <sup>1</sup>    | Accéder par index             | `list[index]`         | `get(index)`            | Accède à l'élément à une position donnée sans effectuer de recherche. |

<sup>1</sup> *Cela dépend du type de liste. Pour une liste indexée, c'est-à-dire une liste où l'on peut accéder à un élément car son index (un tableau, par exemple), l'accès est direct. Pour une liste sans index, comme une liste chaînée classique, l'opération s'apparente plutôt à une opération de recherche linéaire, car on doit itérer sur tous les éléments de la liste jusqu'à l'index désiré.*