---
title: "ArrayList"
layout: default
parent: "Interface List"
nav_order: 1
---

# ArrayList

![Diagramme ArrayList vs LinkedList](https://media.geeksforgeeks.org/wp-content/uploads/20220817143838/ArrayList-vs-LinkedList.png)
*Source: GeeksforGeeks*

## Description
`ArrayList` est une implémentation basée sur un tableau dynamique. Lorsqu'on ajoute des éléments, la capacité initiale est augmentée automatiquement (généralement doublée) lorsque le tableau est plein. Cela permet un accès direct par index grâce à la structure contiguë en mémoire, ce qui rend les opérations de lecture très rapides (O(1)). Cependant, les insertions ou suppressions au milieu nécessitent un décalage des éléments, ce qui entraîne un coût O(n).

## Fonctionnement interne
En interne, `ArrayList` utilise un tableau d'objets. Lorsqu'une redimension est nécessaire, un nouveau tableau est créé et les éléments existants sont copiés, ce qui peut être coûteux en termes de performance pour des listes très grandes. Cette implémentation est idéale pour des scénarios où les accès sont fréquents et les modifications rares.

## Complexité
| Opération       | Complexité |
|-----------------|------------|
| Accès par index | O(1) |
| Insertion (générale)| O(n) |
| Insertion (fin)   | O(1) amorti |
| Suppression (générale)    | O(n) |
| Suppression (fin)    | O(1) amorti |

## Forces
- Accès rapide.
- Bonne performance pour ajout et suppression en fin.

## Faiblesses
- Coûteux pour insertion/suppression au début ou au milieu.

## Utilitaires
- `Collections.sort(list)`
- `Collections.reverse(list)`
- `Collections.shuffle(list)`

## Exemple de code
```java
import java.util.*;

public class DemoArrayList {
    public static void main(String[] args) {
        List<String> noms = new ArrayList<>();
        noms.add("Alice");
        noms.add("Bob");
        noms.add("Charlie");

        Collections.sort(noms);
        System.out.println("Tri naturel : " + noms);
    }
}
```
