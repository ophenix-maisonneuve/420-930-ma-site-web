---
layout: default
parent: "Complexité des algorithmes"
title: "Complexité O(2<sup>n</sup>) - Exponentielle"
nav_order: 5
published: true
---

# Complexité O(2<sup>n</sup>) - Exponentielle

Les algorithmes en O(2<sup>n</sup>) doublent le nombre d'opérations à chaque ajout d'entrée. Exemple : génération de tous les sous-ensembles.

## Exemple
```java
public class ExempleO2n {
    public static void generateSubsets(int[] array, int index, int[] subset) {
        if (index == array.length) {
            // Affiche le sous-ensemble
            for (int i = 0; i < subset.length; i++) {
                System.out.print(subset[i] + " ");
            }
            System.out.println();
            return;
        }
        subset[index] = 0;
        generateSubsets(array, index + 1, subset);
        subset[index] = array[index];
        generateSubsets(array, index + 1, subset);
    }
}
```

## Allure de la courbe

![Complexité O(2<sup>n</sup>)](../assets/images/complexite-o2n.png)
