---
title: "Interface List"
parent: "Structures linéaires"
layout: default
nav_order: 3
has_toc: false
published: true
---

# Interface List

![Java Collections Framework](https://www.baeldung.com/wp-content/uploads/2020/04/java-collections-hierarchy.png)
*Source: Baeldung*

L'interface **List** en Java définit une collection ordonnée qui peut contenir des éléments en double. Elle étend l'interface **Collection** et fournit des méthodes pour accéder aux éléments par index, insérer, supprimer et parcourir.

## Méthodes clés

- `add(E e)` : ajoute un élément.
- `get(int index)` : récupère un élément par index.
- `remove(int index)` : supprime un élément.
- `size()` : retourne la taille.
- `contains(Object o)` : vérifie la présence.

## Complexité générale

| Opération       | Complexité |
|-----------------|------------|
| Accès par index | O(1) pour ArrayList, O(n) pour LinkedList |
| Insertion début   | O(n) pour ArrayList, O(1) pour LinkedList |
| Insertion fin   | O(1) amorti pour ArrayList, O(1) pour LinkedList |
| Insertion milieu| O(n) pour ArrayList, O(n) pour LinkedList |
| Suppression début   | O(n) pour ArrayList, O(1) pour LinkedList |
| Suppression fin   | O(1) amorti pour ArrayList, O(1) pour LinkedList |
| Suppression milieu| O(n) pour ArrayList, O(n) pour LinkedList |

## Utilitaires

- `Collections.sort(list)`
- `Collections.reverse(list)`
- `Collections.shuffle(list)`
- `Collections.synchronizedList(list)`
- `Arrays.asList(T... a)`

### Liens vers les implémentations

- [ArrayList](../notes/arraylist)
- [LinkedList](../notes/linkedlist)
- [CopyOnWriteArrayList](../notes/cowarraylist)
