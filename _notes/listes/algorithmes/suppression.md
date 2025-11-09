---
layout: default
parent: "Algorithmes"
title: "Suppression"
nav_order: 2
published: false
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
