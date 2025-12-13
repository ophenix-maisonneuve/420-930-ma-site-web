---
title: "java.util.concurrent.ConcurrentHashMap"
layout: default
parent: "java.util.Map"
nav_order: 3
published: false
---

# java.util.concurrent.ConcurrentHashMap

## Description
`ConcurrentHashMap` est une table de hachage **thread‑safe** offrant une **pleine concurrence en lecture** et une **forte concurrence en écriture**. Les **lectures** (dont `get`) sont en général **non bloquantes** et peuvent **chevaucher** des mises à jour (`put`, `remove`). Les itérateurs sont **faiblement cohérents** (ne lèvent pas `ConcurrentModificationException`).

## Fonctionnement interne
La structure **redimensionne** dynamiquement lorsque les collisions deviennent trop nombreuses (seuil lié au **facteur de charge ~0.75**). Les opérations de lecture n’emploient pas de verrou global; les mises à jour utilisent des mécanismes de concurrence fins pour préserver la **sécurité des threads** tout en maximisant le débit. Les **clés `null`** et les **valeurs `null`** **ne sont pas autorisées** (pour éviter l’ambiguïté entre « clé absente » et « valeur `null` » en environnement concurrent).

---

## Forces et faiblesses

### Forces
- **Lectures non bloquantes**; **itérateurs faiblement cohérents**.
- **Très bonnes performances** sous forte concurrence.
- Méthodes atomiques utiles: `putIfAbsent`, `replace`, `compute`, `merge`.

### Faiblesses
- **Ordre d’itération non garanti**.
- **Coût** des redimensionnements; éviter les tailles initiales trop faibles.
- Certaines méthodes d’agrégat (`size`, `containsValue`) reflètent des **états transitoires**.

---

## Quand l’utiliser ?
Lorsque **plusieurs threads** doivent lire et modifier simultanément une table associative **sans verrou global** (caches, index partagés, compteurs).

{: .warning}
> `ConcurrentHashMap` **n’autorise pas** les **clés/valeurs `null`**. Utilisez une **valeur sentinelle** ou encapsulez avec `Optional` si nécessaire.

---

## Complexité (indicative)

| **Opération**                          | **Complexité (attendue)** |
|----------------------------------------|----------------------------|
| `get`                                  | O(1) amorti               |
| `put`                                  | O(1) amorti               |
| `remove`                               | O(1) amorti               |
| `containsKey`                          | O(1) amorti               |
| `containsValue`                        | O(n)                      |
| `iterator()` (parcours faiblement cohérent) | O(n)                 |

---

## Exemple de code
```java
import java.util.concurrent.*;

public class DemoConcurrentHashMap {
    public static void main(String[] args) throws InterruptedException {
        ConcurrentHashMap<String, Integer> stock = new ConcurrentHashMap<>();

        Thread t1 = new Thread(new Runnable() {
            @Override
            public void run() {
                for (int i = 0; i < 1000; i++) {
                    stock.merge("article", 1, new java.util.function.BiFunction<Integer,Integer,Integer>() {
                        @Override
                        public Integer apply(Integer a, Integer b) {
                            return a + b;
                        }
                    });
                }
            }
        });

        Thread t2 = new Thread(new Runnable() {
            @Override
            public void run() {
                for (int i = 0; i < 1000; i++) {
                    stock.merge("article", 1, new java.util.function.BiFunction<Integer,Integer,Integer>() {
                        @Override
                        public Integer apply(Integer a, Integer b) {
                            return a + b;
                        }
                    });
                }
            }
        });

        t1.start();
        t2.start();
        t1.join();
        t2.join();

        System.out.println("Quantité totale: " + stock.get("article"));
    }
}
```

## Voir aussi
- [Documentation `ConcurrentHashMap` officielle](https://docs.oracle.com/en/java/javase/25/docs/api/java.base/java/util/concurrent/ConcurrentHashMap.html)
