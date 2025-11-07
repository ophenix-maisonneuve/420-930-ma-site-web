---
layout: default
parent: "Algorithmes"
title: "Recherche"
nav_order: 4
published: false
---

# Recherche dans les listes

La recherche permet de localiser un élément dans une structure. La recherche linéaire est universelle, tandis que la recherche binaire est efficace mais limitée aux structures avec accès direct et triées.

## Recherche linéaire
Applicable à toutes les structures.

### Dans un tableau
```java
for (int i = 0; i < array.length; i++) {
    if (array[i] == target) {
        return i;
    }
}
```
### Dans une liste chaînée
```java
Node current = head;
while (current != null) {
    if (current.getData() == target) {
        return true;
    }
    current = current.getNext();
}
return false;
```

## Recherche binaire
Fonctionne uniquement sur une liste triée, et n'offre un avantage de performance que pour les types de listes fournissant un accès direct par index.
```java
int left = 0, right = array.length - 1;
while (left <= right) {
    int mid = (left + right) / 2;
    if (array[mid] == target) {
        return mid;
    } else if (array[mid] < target) {
        left = mid + 1;
    } else {
        right = mid - 1;
    }
}
```

{: .warning}
Dans une liste chaînée ou doublement chaînée, la recherche binaire n'offre pas d'avantage de performance. En effet, la recherche binaire nécessite un accès direct à l’élément du milieu, ce qui est inefficace dans une liste chaînée (accès linéaire), car cela impliquerait de toujours itérer sur la liste jusqu'au centre. La recherche linéaire reste donc la méthode la plus adaptée pour les listes chaînées.

