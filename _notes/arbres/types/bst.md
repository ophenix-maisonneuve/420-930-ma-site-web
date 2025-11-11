---
layout: default
title: "Arbre binaire de recherche"
parent: "Arbres"
nav_order: 2
published: true
---

# Arbre binaire de recherche (Binary Search Tree)

## Structure

Un **arbre binaire de recherche (BST)** est une structure de données dans laquelle chaque nœud possède au plus deux enfants : un enfant gauche et un enfant droit. Les valeurs dans l'arbre sont organisées de manière à ce que pour chaque nœud :

- Les valeurs dans le sous-arbre gauche sont inférieures à la valeur du nœud.
- Les valeurs dans le sous-arbre droit sont supérieures à la valeur du nœud.

```java
class Node {
    private int value;
    private Node left;
    private Node right;

    public Node(int value) {
        this.value = value;
        this.left = null;
        this.right = null;
    }

    public int getValue() {
        return value;
    }

    public void setValue(int value) {
        this.value = value;
    }

    public Node getLeft() {
        return left;
    }

    public void setLeft(Node left) {
        this.left = left;
    }

    public Node getRight() {
        return right;
    }

    public void setRight(Node right) {
        this.right = right;
    }
}
```

## Opérations sur les arbres binaires

### Insertion

```java
public Node insert(Node root, int value) {
    if (root == null) {
        return new Node(value);
    }
    if (value < root.getValue()) {
        root.setLeft(insert(root.getLeft(), value));
    } else if (value > root.getValue()) {
        root.setRight(insert(root.getRight(), value));
    }
    return root;
}
```

### Recherche

```java
public boolean search(Node root, int value) {
    if (root == null) {
        return false;
    }
    if (value == root.getValue()) {
        return true;
    }
    if (value < root.getValue()) {
        return search(root.getLeft(), value);
    } else {
        return search(root.getRight(), value);
    }
}
```

### Suppression

```java
public Node delete(Node root, int value) {
    if (root == null) {
        return null;
    }
    if (value < root.getValue()) {
        root.setLeft(delete(root.getLeft(), value));
    } else if (value > root.getValue()) {
        root.setRight(delete(root.getRight(), value));
    } else {
        if (root.getLeft() == null) {
            return root.getRight();
        } else if (root.getRight() == null) {
            return root.getLeft();
        }
        Node minNode = findMin(root.getRight());
        root.setValue(minNode.getValue());
        root.setRight(delete(root.getRight(), minNode.getValue()));
    }
    return root;
}

private Node findMin(Node node) {
    while (node.getLeft() != null) {
        node = node.getLeft();
    }
    return node;
}
```

### Parcours

```java
public void inorder(Node root) {
    if (root != null) {
        inorder(root.getLeft());
        System.out.print(root.getValue() + " ");
        inorder(root.getRight());
    }
}

public void preorder(Node root) {
    if (root != null) {
        System.out.print(root.getValue() + " ");
        preorder(root.getLeft());
        preorder(root.getRight());
    }
}

public void postorder(Node root) {
    if (root != null) {
        postorder(root.getLeft());
        postorder(root.getRight());
        System.out.print(root.getValue() + " ");
    }
}
```

---

## Complexité des opérations

| Opération   | Complexité moyenne | Complexité pire cas |
|-------------|---------------------|----------------------|
| Insertion   | O(log n)            | O(n)                 |
| Recherche   | O(log n)            | O(n)                 |
| Suppression | O(log n)            | O(n)                 |
| Parcours    | O(n)                | O(n)                 |

{: .highlight}
> La complexité dépend de l'équilibre de l'arbre. Un arbre parfaitement équilibré permet des opérations en O(log n), tandis qu'un arbre dégénéré (ressemblant à une liste) entraîne des performances en O(n).