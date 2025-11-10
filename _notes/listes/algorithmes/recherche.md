---
layout: default
parent: "Algorithmes"
title: "Recherche"
nav_order: 4
published: true
---

# Recherche dans les listes

La recherche permet de localiser un élément dans une structure. La recherche linéaire est universelle, tandis que la recherche binaire est efficace mais limitée aux structures avec accès direct et triées.

## Recherche linéaire
Applicable à toutes les structures.

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



## Comparaison des méthodes de recherche

| Méthode             | Complexité moyenne | Complexité pire cas | Structure requise               | Avantages                          | Limitations                          |
|---------------------|--------------------|----------------------|----------------------------------|-------------------------------------|--------------------------------------|
| Recherche linéaire  | O(n)               | O(n)                 | Toutes                          | Simple, universelle                | Peu efficace sur grandes structures  |
| Recherche binaire   | O(log n)           | O(log n)             | Liste triée avec accès direct   | Très rapide sur grands ensembles   | Nécessite tri et accès par index     |

{: .warning}
Dans une liste chaînée ou doublement chaînée, la recherche binaire n'offre pas d'avantage de performance. En effet, la recherche binaire nécessite un accès direct à l’élément du milieu, ce qui est inefficace dans une liste chaînée (accès linéaire), car cela impliquerait de toujours itérer sur la liste jusqu'au centre. La recherche linéaire reste donc la méthode la plus adaptée pour les listes chaînées.

