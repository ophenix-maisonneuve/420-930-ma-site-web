---
title: "List en Java"
parent: "Structures linéaires"
layout: default
nav_order: 3
has_toc: false
published: true
---

# Interface `java.util.List`

## Description

![Java Collections Framework](https://www.baeldung.com/wp-content/uploads/2020/04/java-collections-hierarchy.png)
*Source: Baeldung*

L'interface **List** en Java représente une collection ordonnée qui permet d’accéder aux éléments par leur position (index).Elle étend l'interface **Collection**, et plus spécifiquement l'interface **SequencedCollection**. Elle fournit des méthodes pour accéder aux éléments par index, insérer, supprimer, rechercher et parcourir.

## Quand l'utiliser ?

Une **List** est idéale lorsque l’ordre des éléments est important ou lorsque des opérations fréquentes d’insertion, de suppression ou de parcours séquentiel sont nécessaires. Contrairement à un **Set**, une liste autorise les doublons et conserve l’ordre d’insertion. Elle se distingue également d’une **Map**, qui associe des clés à des valeurs, car une liste ne gère que des éléments simples sans clé explicite.

### Scénarios d'utilisation propices

- **Maintenir un ordre précis** : lorsque l’ordre d’insertion ou un ordre logique est essentiel (ex. : étapes d’un processus).
- **Accès par position** : besoin de récupérer ou modifier un élément à un index spécifique.
- **Présence de doublons** : lorsque des éléments identiques doivent être autorisés (ex. : liste de participants où un nom peut apparaître plusieurs fois).
- **Parcours séquentiel** : itération dans un ordre déterminé (ex. : affichage chronologique).
- **Insertion et suppression dynamiques** : ajout ou retrait d’éléments à des positions spécifiques.
- **Collections de taille variable** : lorsque la taille n’est pas fixe et évolue au cours du programme.
- **Traitement ordonné avant tri** : préparation d’une liste pour appliquer un tri personnalisé ou naturel.

---

## Méthodes principales

| **Méthode** | **Description** |
|-------------|------------------|
| [add(E e)](https://docs.oracle.com/en/java/javase/25/docs/api/java.base/java/util/List.html)) | Ajoute un élément à la fin de la liste. |
| [add(int index, E element)](https://docs.oracle.com/en/java/javase/25/docs/api/java.base/java/util/List.html#add(int,Ee un élément à la position spécifiée (décale les éléments suivants). |
| [set(int index, E element)](https://docs.oracle.com/en/java/javase/25/docs/api/java.base/java/util/List.html)) | Remplace l’élément à l’index donné par un nouvel élément. |
| [remove(int index)](https://docs.oracle.com/en/java/javase/25/docs/api/java.base/java/util/List.html)) | Supprime l’élément à la position spécifiée. |
| [remove(Object o)](https://docs.oracle.com/en/java/javase/25/docs/api/java.base/java/util/List.html#remove(java.langpremière occurrence de l’objet spécifié (si présent). |
| [clear()](https://docs.oracle.com/en/java/javase/25/docs/api/java.base/java/util/List.html)) | Supprime tous les éléments de la liste. |
| [get(int index)](https://docs.oracle.com/en/java/javase/25/docs/api/java.base/java/util/List.html#get(intourne l’élément à la position spécifiée. |
| [contains(Object o)](https://docs.oracle.com/en/java/javase/25/docs/api/java.base/java/util/List.html#contains(javai la liste contient l’objet spécifié. |
| [indexOf(Object o)](https://docs.oracle.com/en/java/javase/25/docs/api/java.base/java/util/List.html#indexOf(java.langdex de la première occurrence de l’objet (ou -1 si absent). |
| [sort(Comparator<? super E> c)](https://docs.oracle.com/en/java/javase/25/docs/api/java.base/java/util/List.html)) | Trie la liste selon le comparateur fourni ; si `null`, utilise l’ordre naturel. |
| [size()](https://docs.oracle.com/en/java/javase/25/docs/api/java.base/java/util/List.html)) | Retourne le nombre d’éléments dans la liste. |


### En résumé

- Les méthodes `add`, `remove` et `set` modifient la liste.  
- Les méthodes `get`, `contains`, `indexOf` et `size` sont des opérations de lecture.  
- `sort` est utile pour organiser les éléments selon un ordre spécifique.

{: .highlight}
> Afin de permettre une réutilisation maximale, les Collections Java font beaucoup usage des types génériques. Pour plus d'information sur ce sujet, consultez la page suivante: [Génériques en Java](../notes/generiques-java)


## Utilitaires

- `Collections.sort(list)`
- `Collections.reverse(list)`
- `Collections.shuffle(list)`
- `Collections.synchronizedList(list)`
- `Arrays.asList(T... a)`

### Liens vers les implémentations

- [ArrayList](../notes/arraylist)
- [LinkedList](../notes/linkedlist)
- [CopyOnWriteArrayList](../notes/cowarraylist)
