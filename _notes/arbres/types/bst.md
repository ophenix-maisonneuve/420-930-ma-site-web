---
layout: default
parent: "Arbres"
title: "Arbre binaire de recherche"
nav_order: 3
published: true
---

# Arbre binaire de recherche

## Structure

Un arbre binaire de recherche est composé de nœuds contenant une valeur, un pointeur vers le nœud gauche et un pointeur vers le nœud droit.

```java
class Node {
    int value;
    Node left, right;

    public Node(int value) {
        this.value = value;
        left = right = null;
    }
}

class BinarySearchTree {
    Node root;

    public BinarySearchTree() {
        root = null;
    }

    // Les méthodes seront ajoutées ici
}
```
```

## Opérations sur les arbres binaires

### Insertion

<details markdown="1">
<summary markdown="span">**Insertion récursive**</summary>

```java
Node insert(Node root, int value) {
    if (root == null) {
        return new Node(value);
    }
    if (value < root.value) {
        root.left = insert(root.left, value);
    } else if (value > root.value) {
        root.right = insert(root.right, value);
    }
    return root;
}
```
</details>

### Suppression

<details markdown="1">
<summary markdown="span">**Suppression d'un nœud**</summary>

```java
Node delete(Node root, int value) {
    if (root == null) return root;
    if (value < root.value) {
        root.left = delete(root.left, value);
    } else if (value > root.value) {
        root.right = delete(root.right, value);
    } else {
        if (root.left == null) return root.right;
        else if (root.right == null) return root.left;

        Node minNode = findMin(root.right);
        root.value = minNode.value;
        root.right = delete(root.right, minNode.value);
    }
    return root;
}

Node findMin(Node node) {
    while (node.left != null) node = node.left;
    return node;
}
```
</details>

### Recherche

<details markdown="1">
<summary markdown="span">**Recherche récursive**</summary>

```java
boolean search(Node root, int value) {
    if (root == null) return false;
    if (value == root.value) return true;
    if (value < root.value) return search(root.left, value);
    else return search(root.right, value);
}
```
</details>

### Parcours

<details markdown="1">
<summary markdown="span">**Parcours infixe (in-order)**</summary>

```java
void inOrder(Node root) {
    if (root != null) {
        inOrder(root.left);
        System.out.print(root.value + " ");
        inOrder(root.right);
    }
}
```
</details>

<details markdown="1">
<summary markdown="span">**Parcours préfixe (pre-order)**</summary>

```java
void preOrder(Node root) {
    if (root != null) {
        System.out.print(root.value + " ");
        preOrder(root.left);
        preOrder(root.right);
    }
}
```
</details>

<details markdown="1">
<summary markdown="span">**Parcours suffixe (post-order)**</summary>

```java
void postOrder(Node root) {
    if (root != null) {
        postOrder(root.left);
        postOrder(root.right);
        System.out.print(root.value + " ");
    }
}
```
</details>
