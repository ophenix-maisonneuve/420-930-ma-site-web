---
layout: default
parent: "Complexité des algorithmes"
title: "Complexité O(log n) - Logarithmique"
nav_order: 2
published: true
---

# Complexité O(log n) - Logarithmique

Un algorithme en O(log n) divise le problème à chaque étape. Exemple typique : recherche dichotomique.

## Exemple
```java
public class ExempleOlogn {
    public static boolean binarySearch(int[] array, int target) {
        int left = 0, right = array.length - 1;
        while (left <= right) {
            int mid = (left + right) / 2;
            if (array[mid] == target) return true;
            else if (array[mid] < target) left = mid + 1;
            else right = mid - 1;
        }
        return false;
    }
}
```

## Allure de la courbe

![Complexité O(log n)](../assets/images/complexite-ologn.png)