---
layout: default
parent: "Types"
title: "Tableau"
nav_order: 1
published: false
---

# Tableau (Array)

Un tableau est une structure de données à taille fixe où chaque élément est accessible directement par son index. Il est efficace pour les accès rapides mais coûteux pour les insertions et suppressions.

```java
public class MonTableau {
    public static void main(String[] args) {
        int[] tableau = new int[5];
        tableau[0] = 10;
        tableau[1] = 20;
        tableau[2] = 30;
        for (int i = 0; i < tableau.length; i++) {
            System.out.println(tableau[i]);
        }
    }
}
```
