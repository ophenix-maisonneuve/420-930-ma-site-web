---
title: "LinkedList"
layout: default
parent: "Interface List"
nav_order: 2
---

# LinkedList

![Diagramme ArrayList vs LinkedList](https://media.geeksforgeeks.org/wp-content/uploads/20220817143838/ArrayList-vs-LinkedList.png)
*Source: GeeksforGeeks*

## Description

`LinkedList` est une implémentation basée sur une liste chaînée double. Chaque élément est stocké dans un noeud qui contient une référence vers l'élément précédent et suivant. Cette structure permet des insertions et suppressions rapides en tête ou en queue (O(1)), car il suffit de mettre à jour quelques références. Cependant, l'accès par index est coûteux (O(n)), car il faut parcourir la liste depuis le début ou la fin.

## Fonctionnement interne

En interne, `LinkedList` consomme plus de mémoire qu'un tableau car chaque noeud stocke deux références supplémentaires. Elle est idéale pour des scénarios où les insertions et suppressions sont fréquentes, mais les accès aléatoires rares.

## Complexité

| Opération       | Complexité |
|-----------------|------------|
| Accès par index | O(n) |
| Insertion tête/queue  | O(1) |
| Insertion milieu| O(n) |
| Suppression tête/queue     | O(1) |
| Suppression milieu     | O(n) |

## Forces

- Insertions/suppressions rapides en tête et en queue (début et fin de liste).

## Faiblesses

- Accès par index lent.

## Utilitaires

- `Collections.sort(list)`

## Exemple de code

```java
import java.util.*;

public class DemoLinkedList {
    public static void main(String[] args) {
        List<String> noms = new LinkedList<>();
        noms.add("Alice");
        noms.add("Bob");
        noms.add("Charlie");

        Collections.reverse(noms);
        System.out.println("Liste inversée : " + noms);
    }
}
```
