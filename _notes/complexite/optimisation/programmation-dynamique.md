---
layout: default
parent: "Optimisation"
parent: "Programmation dynamique"
nav_order: 4
published: false
---

# Programmation dynamique

## Objectif
Optimiser les calculs en évitant les répétitions grâce à la mémorisation des résultats intermédiaires.

## Explication
La programmation dynamique est utile lorsque le problème peut être décomposé en sous-problèmes qui se répètent. Elle permet de réduire la complexité en stockant les résultats déjà calculés.

{: .highlight}
> Par exemple, dans le calcul de la suite de Fibonacci, on peut utiliser :
> - **Mémoïsation** (top-down) : on stocke les résultats au fur et à mesure des appels récursifs.
> - **Tabulation** (bottom-up) : on construit une table de résultats à partir des cas de base.

## Pourquoi c’est utile
- Réduction drastique du temps d’exécution
- Exploitation efficace des dépendances internes du problème
- Applicable à de nombreux problèmes combinatoires

---

## Exemple

### Avant
```java
public class Fibonacci {
    public static int fib(int n) {
        if (n <= 1) {
            return n;
        }
        return fib(n - 1) + fib(n - 2);
    }

    public static void main(String[] args) {
        int n = 10; // Exemple : calculer le 10e terme
        System.out.println("Fibonacci(" + n + ") = " + fib(n));
    }
}
```

### Optimisation par mémoïsation (top-down)
```java
public class Fibonacci {
    static int[] memo;

    public static int fib(int n) {
        if (memo[n] != -1) return memo[n];
        if (n <= 1) return n;
        memo[n] = fib(n - 1) + fib(n - 2);
        return memo[n];
    }

    public static void main(String[] args) {
        int n = 10;
        memo = new int[n + 1];
        for (int i = 0; i <= n; i++) memo[i] = -1;
        System.out.println(fib(n));
    }
}
```

### Optimisation par tabulation (bottom-up)
```java
public class Fibonacci {
    public static int fib(int n) {
        if (n <= 1) return n;
        int[] dp = new int[n + 1];
        dp[0] = 0;
        dp[1] = 1;
        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }

    public static void main(String[] args) {
        System.out.println(fib(10));
    }
}
```
