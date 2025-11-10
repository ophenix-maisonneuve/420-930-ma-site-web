---
layout: default
parent: "Types"
title: "Liste chaînée"
nav_order: 3
published: true
---

# Liste chaînée

Une liste chaînée (aussi appelée liste chaînée simple) est composée de nœuds où chaque nœud pointe vers le suivant. Elle permet des insertions et suppressions rapides.

```java
class Node {
    private int data;
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

    public Node getNext() {
        return next;
    }

    public void setNext(Node next) {
        this.next = next;
    }
}

class LinkedList {
    private Node head;

    // les méthodes pour les opérations seront ajoutées ici
    // ...
}
```
