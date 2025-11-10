---
layout: default
parent: "Listes et tableaux"
title: "Liste chaînée"
nav_order: 3
published: true
---

# Liste chaînée

## Structure

### Simple

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

### Double

Une liste doublement chaînée(ou liste chaînée double) permet de naviguer dans les deux sens grâce à des références vers le nœud précédent et suivant.

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

## Opérations sur les listes chaînées

### Ajout

#### Ajout dans une liste chaînée
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

#### Ajout dans une liste doublement chaînée
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

### Suppression

#### Suppression dans une liste chaînée
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

#### Suppression dans une liste doublement chaînée
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

### Tri

#### Tri par insertion

Le tri par insertion fonctionne en construisant progressivement une liste triée en insérant chaque nouvel élément à sa position correcte.

```java
public Node insertionSort(Node head) {
    Node sorted = null;
    Node current = head;
    while (current != null) {
        Node next = current.next;
        sorted = sortedInsert(sorted, current);
        current = next;
    }
    return sorted;
}

private Node sortedInsert(Node head, Node newNode) {
    if (head == null || head.getData() >= newNode.getData()) {
        newNode.next = head;
        return newNode;
    }
    Node current = head;
    while (current.getNext() != null && current.getNext().getData() < newNode.getData()) {
        current = current.next;
    }
    newNode.next = current.next;
    current.next = newNode;
    return head;
}
```
#### Tri à bulles

Le tri à bulles compare chaque paire d'éléments adjacents et les échange si nécessaire, répétant ce processus jusqu'à ce que la liste soit triée.

```java
public void bubbleSort(Node head) {
    boolean swapped;
    Node ptr1;
    Node lptr = null;
    do {
        swapped = false;
        ptr1 = head;
        while (ptr1.next != lptr) {
            if (ptr1.data > ptr1.next.data) {
                int temp = ptr1.data;
                ptr1.data = ptr1.next.data;
                ptr1.next.data = temp;
                swapped = true;
            }
            ptr1 = ptr1.next;
        }
        lptr = ptr1;
    } while (swapped);
}
```

#### Tri rapide (*Quick Sort*)

Le tri rapide est un algorithme de tri efficace basé sur le principe du diviser pour régner. Il choisit un pivot et partitionne le tableau autour de ce pivot.

```java
class Node {
    int data;
    Node next;
    Node(int d) { data = d; next = null; }
}

public Node quickSort(Node head) {
    if (head == null || head.next == null) return head;
    Node pivot = head;
    Node lesser = null, greater = null;
    Node current = head.next;
    while (current != null) {
        Node next = current.next;
        if (current.data < pivot.data) {
            current.next = lesser;
            lesser = current;
        } else {
            current.next = greater;
            greater = current;
        }
        current = next;
    }
    lesser = quickSort(lesser);
    greater = quickSort(greater);
    return concatenate(lesser, pivot, greater);
}

private Node concatenate(Node lesser, Node pivot, Node greater) {
    Node head = lesser;
    if (lesser == null) head = pivot;
    else {
        Node temp = lesser;
        while (temp.next != null) temp = temp.next;
        temp.next = pivot;
    }
    pivot.next = greater;
    return head;
}
```

#### Tri par fusion (*Merge Sort*)

Le tri par fusion divise la liste en deux moitiés, trie chaque moitié récursivement, puis fusionne les deux listes triées.

```java
public Node mergeSort(Node head) {
    if (head == null || head.getNext() == null) {
         return head;
    }

    Node middle = getMiddle(head);
    Node nextOfMiddle = middle.getNext();
    middle.setNext(null);

    Node left = mergeSort(head);
    Node right = mergeSort(nextOfMiddle);

    return sortedMerge(left, right);
}

private Node getMiddle(Node head) {
    if (head == null) {
        return head;
    }

    Node slow = head;
    Node fast = head.getNext();

    while (fast != null && fast.getNext() != null) {
        slow = slow.getNext();
        fast = fast.getNext().getNext();
    }

    return slow;
}

private Node sortedMerge(Node a, Node b) {
    if (a == null) {
         return b;
    }
    if (b == null) {
        return a;
    } 

    Node result;
    if (a.getData() <= b.getData()) {
        result = a;
        result.setNext(sortedMerge(a.getNext(), b));
    } else {
        result = b;
        result.setNext(sortedMerge(a, b.getNext()));
    }

    return result;
}
```


### Recherche

#### Recherche linéaire
Applicable à toutes les structures.

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
{: .warning}
>Dans une liste chaînée ou doublement chaînée, la recherche binaire n'offre pas d'avantage de performance et n'est donc pas applicable. En effet, la recherche binaire nécessite un accès direct à l’élément du milieu, ce qui est inefficace dans une liste chaînée (accès linéaire), car cela impliquerait de toujours itérer sur la liste jusqu'au centre. La recherche linéaire reste donc la méthode la plus adaptée pour les listes chaînées.

