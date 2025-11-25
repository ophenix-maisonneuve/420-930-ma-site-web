---
title: "java.util.ArrayList"
layout: default
parent: "java.util.List"
nav_order: 2
published: true
---

# java.util.ArrayList

![Diagramme ArrayList](../assets/images/arraylist.png)

## Description

`ArrayList` est une implémentation basée sur un tableau dynamique. Lorsqu'on ajoute des éléments, la capacité initiale est augmentée automatiquement (généralement doublée) lorsque le tableau est plein. Cela permet un accès direct par index grâce à la structure contiguë en mémoire, ce qui rend les opérations de lecture très rapides (O(1)). Cependant, les insertions ou suppressions au milieu nécessitent un décalage des éléments, ce qui entraîne un coût O(n).

## Fonctionnement interne

En interne, `ArrayList` utilise un tableau d'objets. Lorsqu'une redimension est nécessaire, un nouveau tableau est créé et les éléments existants sont copiés, ce qui peut être coûteux en termes de performance pour des listes très grandes. Cette implémentation est idéale pour des scénarios où les accès sont fréquents et les modifications rares.

---

## Forces et faiblesses

### Forces
- **Accès rapide par index** : temps constant en moyenne pour `get(int index)` et `set(int index)`.
- **Bonne performance en lecture** : idéal pour parcourir ou lire des éléments séquentiellement.
- **Souplesse de taille** : la capacité s’ajuste automatiquement (pas besoin de taille fixe).
- **Compatibilité avec les API Java** : largement utilisée et bien intégrée dans les bibliothèques standard.

### Faiblesses
- **Insertion/suppression coûteuse en milieu de liste** : nécessite un décalage des éléments (complexité O(n)).
- **Consommation mémoire** : réserve une capacité supérieure à la taille réelle pour anticiper les ajouts.
- **Pas optimisée pour les opérations en tête** : `add(0, element)` ou `remove(0)` sont très coûteuses.
- **Non thread-safe** : nécessite une synchronisation explicite pour un usage concurrent.

---

## Quand l'utiliser ?

`ArrayList` est le choix privilégié lorsque la priorité est la **rapidité d’accès par index** et la **performance en lecture**, plutôt que des insertions fréquentes en milieu ou en tête de liste. Elle est particulièrement adaptée aux scénarios où la liste est principalement **consultée** ou **modifiée en fin de liste**.

### Cas d’utilisation propices

- **Accès direct aux éléments** : besoin fréquent de récupérer des éléments par leur index.
- **Parcours rapide** : itération séquentielle sur une grande collection.
- **Ajouts en fin de liste** : opérations `add(E e)` fréquentes sans contraintes de position.
- **Collections principalement en lecture** : peu de modifications après la construction initiale.
- **Pré-tri et traitement ordonné** : lorsque la liste doit être triée ou manipulée avant affichage.
- **Scénarios où la mémoire est acceptable** : lorsque la surcharge liée à la capacité n’est pas critique.

{: .astuce}

> Si votre application nécessite des accès rapides et des ajouts en fin de liste, `ArrayList` est généralement le meilleur choix. Pour des insertions fréquentes en tête ou en milieu, préférez `LinkedList`.

## Complexité

| Opération       | Complexité |
|-----------------|------------|
| Accès par index | O(1) |
| Insertion début/milieu | O(n) |
| Insertion fin   | O(1) amorti |
| Suppression début/milieu    | O(n) |
| Suppression fin    | O(1) amorti |

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

## Voir aussi

- [java.util.ArrayList](https://docs.oracle.com/en/java/javase/25/docs/api/java.base/java/util/ArrayList.html)

{: .highlight}
> Comme toutes les autres Collections, `ArrayList` fonctionne principalement avec des types génériques. Pour plus d'information sur ce sujet, consultez la page suivante: [Génériques en Java](../notes/generiques-java)
