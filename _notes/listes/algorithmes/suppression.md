---
layout: default
parent: "Algorithmes"
title: "Suppression"
nav_order: 2
published: true
---

# Suppression dans les listes

La suppression consiste à retirer un élément d'une structure de données. Elle peut se faire au début, au milieu ou à la fin. Selon la structure, cela implique des décalages ou des mises à jour de références.

## Suppression dans un tableau
```java
int[] array = {10, 20, 30, 40};
// Suppression au milieu (index 1)
for (int i = 1; i < array.length - 1; i++) {
    array[i] = array[i + 1];
}
```

## Suppression dans une liste chaînée
```java
void deleteFront() {
    if (head != null) {
        head = head.getNext();
    }
}

void deleteEnd() {
    if (head == null || head.getNext() == null) {
        head = null;
        return;
    }

    Node current = head;
    while (current.getNext().getNext() != null) {
         current = current.getNext();
    }
    current.setNext(null);
}
```

## Suppression dans une liste doublement chaînée
```java
void deleteFront() {
    if (head == null) {
        return;
    }

    head = head.getNext();
    if (head != null) {
            head.setPrev(null);
    }
}

void deleteEnd() {
    if (head == null) {
          return;
    }

    Node current = head;
    while (current.getNext() != null) {
         current = current.getNext();
    }
    if (current.getPrev() != null) {
         current.getPrev().setNext(null);
    } else {
        head = null;
    }
}

```
## Complexité

| Structure              | Suppression en tête | Suppression en fin | Suppression à une position |
|------------------------|---------------------|---------------------|-----------------------------|
| Tableau                | O(n)                | O(1) ou O(n)        | O(n)                        |
| Liste chaînée simple   | O(1)                | O(n)                | O(n)                        |
| Liste chaînée double   | O(1)                | O(1) ou O(n)        | O(n)                        |

{: .highlight}
>La complexité de la suppression en fin dépend de l’implémentation.
>
>Dans un tableau, si on ne fait que remplacer le dernier élément sans réduire la taille du tableau, la complexité est O(1). Toutefois, si on veut réduire la taille du tableau pour n'avoir aucun élément vide, on devra recopier le tableau, entraînant une complexité O(n).
>Dans une liste chaînée simple, même si une référence au dernier nœud (tail) est maintenue, il est nécessaire de retrouver l’avant-dernier nœud pour mettre à jour son pointeur, ce qui implique un parcours complet de la liste (O(n)).
>Dans une liste chaînée double, si une référence au dernier nœud est maintenue, on peut accéder directement à son prédécesseur et le détacher sans parcourir la liste (O(1)).