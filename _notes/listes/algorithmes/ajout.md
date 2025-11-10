---
layout: default
parent: "Algorithmes"
title: "Ajout"
nav_order: 1
published: true
---

# Ajout dans les listes

L'ajout est une opération fondamentale dans les structures de données linéaires. Elle permet d'insérer un nouvel élément à une position donnée : au début, au milieu ou à la fin. Le comportement et la complexité de cette opération varient selon le type de liste utilisé.

## Ajout dans un tableau simple
Voici une insertion simple, où l'on écrase potentiellement l'élément qui était déjà présent à l'index donné.Dans un tableau, l'ajout nécessite souvent de décaler les éléments ou de recréer le tableau si sa taille est fixe.
```java
int[] array = new int[5];
array[0] = 10; // ajout en début
array[2] = 30; // ajout au milieu
array[4] = 50; // ajout en fin
```

Dans bien des cas, on veut plutôt ajouter aux éléments déjà existants, ce qui demande plusôt de décaler les éléments ou même de recréer le tableau
```java
int[] original = {10, 20, 30, 40, 50};
int newValue = 25;
int insertIndex = 2;

// Création d'un nouveau tableau avec une taille augmentée
int[] resized = new int[original.length + 1];

// Copier les éléments avant l'index d'insertion
for (int i = 0; i < insertIndex; i++) {
    resized[i] = original[i];
}

// Insérer la nouvelle valeur
resized[insertIndex] = newValue;

// Décaler les éléments restants
for (int i = insertIndex; i < original.length; i++) {
    resized[i + 1] = original[i];
}
```

## Ajout dans une liste chaînée
On crée un nouveau nœud et on ajuste les pointeurs.
```java
public void addFront(int data) {
    Node newNode = new Node(data);
    newNode.setNext(head);
    head = newNode;
}

public void addEnd(int data) {
    Node newNode = new Node(data);
    if (head == null) {
        head = newNode;
        return;
    }
    Node current = head;
    while (current.getNext() != null) {
        current = current.getNext();
    }
    current.setNext(newNode);
}
```

## Ajout dans une liste doublement chaînée
Permet d'insérer dans les deux directions.
```java
public void addFront(int data) {
    Node newNode = new Node(data);
    newNode.setNext(head);
    if (head != null) {
        head.setPrev(newNode);
    }
    head = newNode;
}

public void addEnd(int data) {
    Node newNode = new Node(data);
    if (head == null) {
        head = newNode;
        return;
    }
    Node current = head;
    while (current.getNext() != null) {
        current = current.getNext();
    }
    current.setNext(newNode);
    newNode.setPrev(current);
}
```

## Complexité

| Structure              | Ajout en tête | Ajout en fin | Ajout à une position |
|------------------------|---------------|--------------|-----------------------|
| Tableau                | O(n)          | O(1) ou O(n) si tableau plein| O(n)                  |
| Liste chaînée simple   | O(1)          | O(n) ou O(1) si *tail*       | O(n)                  |
| Liste chaînée double   | O(1)          | O(n) ou O(1) si *tail*         | O(n)                  |

{. :highlight}

>Dans un tableau, l’ajout en fin est généralement O(1) si la capacité est suffisante. Toutefois, si le tableau est plein, il faut créer un nouveau tableau plus grand et copier les éléments, ce qui entraîne une complexité O(n).
>Dans une liste chaînée (simple ou double), l’ajout en fin est O(n) par défaut, car il faut parcourir la liste pour atteindre le dernier nœud. Cependant, si une référence vers le dernier nœud (tail) est maintenue, l’ajout en fin peut être effectué en O(1).