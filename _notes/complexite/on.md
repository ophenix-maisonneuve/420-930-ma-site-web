---
layout: default
parent: "Complexité des algorithmes"
title: "Complexité O(n) - Linéaire
nav_order: 3
published: true
---

# Complexité O(n) - Linéaire

Un algorithme en O(n) parcourt tous les éléments une seule fois.

## Exemple
```java
public class ExempleOn {
    public static boolean contains(int[] array, int target) {
        for (int i = 0; i < array.length; i++) {
            if (array[i] == target) return true;
        }
        return false;
    }
}
```

## Allure de la courbe

![Complexité O(n)](../assets/images/complexite-on.png)
