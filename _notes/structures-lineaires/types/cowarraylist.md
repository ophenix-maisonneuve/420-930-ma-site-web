---
title: "CopyOnWriteArrayList"
layout: default
parent: "Interface List"
nav_order: 3
---

# CopyOnWriteArrayList

![CopyOnWriteArrayList Diagram](https://www.baeldung.com/wp-content/uploads/2020/04/java-copyonwritearraylist.png)
*Source: Baeldung*

## Description

`CopyOnWriteArrayList` est une implémentation thread-safe qui repose sur le principe de copie lors de l'écriture. Chaque fois qu'une modification (ajout, suppression) est effectuée, un nouveau tableau est créé et les éléments existants sont copiés. Cela garantit que les itérations ne rencontrent jamais de `ConcurrentModificationException`, car elles travaillent sur une version immuable.

## Fonctionnement interne

Cette approche est très efficace pour des scénarios où les lectures sont beaucoup plus fréquentes que les écritures. Cependant, elle est coûteuse en mémoire et en temps pour des modifications fréquentes, car chaque écriture implique une copie complète du tableau.

## Complexité

| Opération       | Complexité |
|-----------------|------------|
| Lecture         | O(1) |
| Écriture        | O(n) (copie complète) |

## Forces

- Thread-safe sans verrou explicite.

## Faiblesses

- Coûteux pour modifications fréquentes.

## Utilitaires

- Compatible avec `Collections.sort()`.

## Exemple de code

```java
import java.util.*;
import java.util.concurrent.CopyOnWriteArrayList;

public class DemoCOWArrayList {
    public static void main(String[] args) {
        List<String> noms = new CopyOnWriteArrayList<>();
        noms.add("Alice");
        noms.add("Bob");

        for (String nom : noms) {
            System.out.println(nom);
        }
    }
}
```
