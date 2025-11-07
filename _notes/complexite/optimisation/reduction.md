---
layout: default
parent: "Optimisation"
title: "Réduction du problème"
nav_order: 3
published: false
---


# Réduction du problème

## Objectif
Reformuler un problème complexe en sous-problèmes plus simples.

## Explication
Réduire un problème permet de mieux structurer la solution et de préparer l’utilisation de l'une des autres méthodes sur chacun des sous-problèmes:

- Structure de données mieux adaptée
- Algorithme plus performant
- Programmation dynamique

## Exemple

### Avant (calcul récursif naïf du nombre de chemins dans une grille)
```java
public class GridPaths {
    public static int countPaths(int m, int n) {
        if (m == 1 || n == 1) return 1;
        return countPaths(m - 1, n) + countPaths(m, n - 1);
    }
}
```

### Après (réduction en tableau 2D)
```java
public class GridPaths {
    public static int countPaths(int m, int n) {
        int[][] dp = new int[m][n];
        for (int i = 0; i < m; i++) {
             dp[i][0] = 1;
        }
        for (int j = 0; j < n; j++) {
             dp[0][j] = 1;
        }
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
        return dp[m - 1][n - 1];
    }
}
```
