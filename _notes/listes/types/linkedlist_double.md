---
layout: default
parent: "Types"
title: "Liste doublement chaînée"
nav_order: 4
published: false
---

# LinkedList Double

Une liste chaînée double permet de naviguer dans les deux sens grâce à des pointeurs vers le nœud précédent et suivant.

```java
private class Node {
    private int data;
    private Node prev;
    private Node next;

    public Node(int d) {
        this.data = d;
    }

    public int getData() {
        return data;
    }

    public void setData(int data) {
        this.data = data;
    }

    public Node getPrev() {
        return prev;
    }

    public void setPrev(Node prev) {
        this.prev = prev;
    }

    public Node getNext() {
        return next;
    }

    public void setNext(Node next) {
        this.next = next;
    }
}

public class DoublyLinkedList {
    private Node head;

    // les méthodes pour les opérations seront ajoutées ici
    // ...
}
```
