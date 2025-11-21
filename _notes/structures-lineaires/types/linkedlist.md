---
title: "LinkedList"
layout: default
parent: "Interface List"
nav_order: 2
---

# LinkedList

![Diagramme ArrayList vs LinkedList](https://media.geeksforgeeks.org/wp-content/uploads/20220817143838/ArrayList-vs-LinkedList.png)
*Source: GeeksforGeeks*

## Description

`LinkedList` est une implémentation basée sur une liste chaînée double. Chaque élément est stocké dans un noeud qui contient une référence vers l'élément précédent et suivant. Cette structure permet des insertions et suppressions rapides en tête ou en queue (O(1)), car il suffit de mettre à jour quelques références. Cependant, l'accès par index est coûteux (O(n)), car il faut parcourir la liste depuis le début ou la fin.

## Fonctionnement interne

En interne, `LinkedList` consomme plus de mémoire qu'un tableau car chaque noeud stocke deux références supplémentaires. Elle est idéale pour des scénarios où les insertions et suppressions sont fréquentes, mais les accès aléatoires rares.

---

## Forces et faiblesses

### Forces
- **Insertion et suppression rapides en tête ou en milieu** : pas de décalage des éléments comme dans `ArrayList`.
- **Structure chaînée** : idéale pour des réorganisations fréquentes ou des listes très dynamiques.
- **Navigation bidirectionnelle** : grâce au double chaînage (avant/arrière).

### Faiblesses
- **Accès par index lent** : nécessite un parcours séquentiel (complexité O(n)).
- **Surcharge mémoire élevée** : chaque élément stocke des références supplémentaires (précédent et suivant).
- **Moins efficace pour parcours pur** : moins rapide que `ArrayList` pour itérations simples.
- **Non thread-safe** : nécessite une synchronisation explicite en contexte concurrent.

---

## Quand l'utiliser ?

`LinkedList` est appropriée lorsque la liste subit des **insertions et suppressions fréquentes** à des positions variées, et que l’accès direct par index n’est pas une priorité. Elle est particulièrement utile pour des **collections dynamiques** où la structure évolue souvent.

### Cas d’utilisation propices

- **Insertions fréquentes en tête ou en milieu** : lorsque la structure change régulièrement.
- **Collections très dynamiques** : ajout et suppression d’éléments à des positions variées.
- **Scénarios où l’accès par index est rare** : la liste est parcourue séquentiellement plutôt qu’aléatoirement.
- **Traitement par réorganisation** : lorsque les éléments doivent être déplacés ou réordonnés sans coût élevé de décalage.

---

✅ **À retenir** : Pour des insertions/suppressions rapides en tête ou en milieu, `LinkedList` est adaptée. Pour des accès rapides par index et des ajouts en fin, préférez `ArrayList`.  
**Pour les files et piles**, utilisez plutôt l’interface `Deque` avec une implémentation comme `ArrayDeque`, qui est optimisée pour ces usages.


## Complexité

| Opération       | Complexité |
|-----------------|------------|
| Accès par index | O(n) |
| Insertion début/fin  | O(1) |
| Insertion milieu| O(n) |
| Suppression début/fin     | O(1) |
| Suppression milieu     | O(n) |

## Utilitaires

- `Collections.sort(list)`

## Exemple de code

```java
import java.util.*;

public class DemoLinkedList {
    public static void main(String[] args) {
        List<String> noms = new LinkedList<>();
        noms.add("Alice");
        noms.add("Bob");
        noms.add("Charlie");

        Collections.reverse(noms);
        System.out.println("Liste inversée : " + noms);
    }
}
```
