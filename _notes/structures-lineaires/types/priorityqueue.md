---
title: "java.util.PriorityQueue"
parent: "Structures linéaires"
layout: default
nav_order: 4
has_toc: false
published: false
---

# Classe `java.util.PriorityQueue`

## Description

**PriorityQueue** est une file qui ordonne ses éléments selon leur ordre naturel (s'ils implémentent `Comparable`) ou un `Comparator` fourni. Elle est implémentée avec un **tas binaire** (*binary heap*) stocké dans un tableau.


## Fonctionnement interne
 
Le **tas binaire** est une structure semi-ordonnée où le plus petit élément (ou le plus prioritaire selon le `Comparator`) se trouve toujours à la racine. Lorsqu’un élément est inséré, il est ajouté à la fin du tableau, puis « remonté » (*heapify up*) pour restaurer la propriété du tas. Lorsqu’on retire la tête (élément prioritaire), le dernier élément du tableau est déplacé à la racine, puis « descendu » (*heapify down*) pour rétablir l’ordre. Ces ajustements garantissent que la tête est toujours l’élément le plus prioritaire, avec des opérations d’insertion et de suppression en **O(log n)**. Ce fonctionnement est très efficace pour gérer des files où l’ordre de priorité est essentiel, mais il ne garantit pas un ordre global pour tous les éléments, seulement pour la tête.

{: .highlight}
> Comme `PriorityQueue` ne garantit l'ordre que pour la tête (élément le plus prioritaire), elle ne peut être utilisée comme queue à deux extrémités (**deque**). Elle implémente donc directement l'interface `Queue`, et non l'interface `Deque`.

## Forces et faiblesses

### Forces

- Permet de gérer des éléments avec **priorité**.
- Opérations de suppression et insertion efficaces (O(log n)).
- Idéale pour les algorithmes de graphes (Dijkstra, A*).

### Faiblesses

- Pas thread-safe.
- Ne garantit pas l'ordre global (seule la tête est prioritaire).
- Ne permet pas les éléments `null`.

## Quand l'utiliser ?
- Gestion de tâches avec priorité.
- Algorithmes comme Dijkstra.

## Complexité
| Opération | Complexité |
|-----------|------------|
| insertion | O(log n) |
| suppression tête | O(log n) |

## Exemple
```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.add(10);
pq.add(5);
pq.add(20);
System.out.println(pq.poll()); // 5
```

### À voir aussi
[Documentation Oracle PriorityQueue](https://docs.oracle.com/en/java/javase/25/docs/api/java.base/java/util/PriorityQueue.html)
