---
layout: default
parent: "Algorithmes"
title: "Tri"
nav_order: 3
published: false
---

# Tri dans les structures de données

Le tri est une opération fondamentale qui permet de réorganiser les éléments d'une structure de données selon un ordre défini (croissant ou décroissant). Il existe plusieurs algorithmes de tri, chacun ayant ses avantages selon le type de structure et la taille des données.

---

## Tri par insertion

Le tri par insertion fonctionne en construisant progressivement une liste triée en insérant chaque nouvel élément à sa position correcte.

### Exemple sur un tableau
```java
public void insertionSort(int[] arr) {
    for (int i = 1; i < arr.length; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}
```

### Exemple sur une liste chaînée
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

---

## Tri à bulles

Le tri à bulles compare chaque paire d'éléments adjacents et les échange si nécessaire, répétant ce processus jusqu'à ce que la liste soit triée.

### Exemple sur un tableau
```java
public void bubbleSort(int[] arr) {
    int n = arr.length;
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}
```

### Exemple sur une liste chaînée
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

---

## Tri rapide (*Quick Sort*)

Le tri rapide est un algorithme de tri efficace basé sur le principe du diviser pour régner. Il choisit un pivot et partitionne le tableau autour de ce pivot.

### Exemple sur un tableau
```java
public void quickSort(int[] arr, int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

private int partition(int[] arr, int low, int high) {
    int pivot = arr[high];
    int i = (low - 1);
    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
    }
    int temp = arr[i + 1];
    arr[i + 1] = arr[high];
    arr[high] = temp;
    return i + 1;
}
```

### Exemple sur une liste chaînée
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

---

## Tri par fusion (*Merge Sort*)

Le tri par fusion divise la liste en deux moitiés, trie chaque moitié récursivement, puis fusionne les deux listes triées.

### Exemple sur un tableau
```java
public void mergeSort(int[] array, int left, int right) {
    if (left < right) {
        int middle = (left + right) / 2;

        // Recursively sort first and second halves
        mergeSort(array, left, middle);
        mergeSort(array, middle + 1, right);

        // Merge the sorted halves
        merge(array, left, middle, right);
    }
}

private void merge(int[] array, int left, int middle, int right) {
    int leftSize = middle - left + 1;
    int rightSize = right - middle;

    int[] leftArray = new int[leftSize];
    int[] rightArray = new int[rightSize];

    // Copy data to temporary arrays
    for (int i = 0; i < leftSize; i++) {
        leftArray[i] = array[left + i];
    }
    for (int j = 0; j < rightSize; j++) {
        rightArray[j] = array[middle + 1 + j];
    }

    int i = 0, j = 0;
    int k = left;

    // Merge the temporary arrays
    while (i < leftSize && j < rightSize) {
        if (leftArray[i] <= rightArray[j]) {
            array[k++] = leftArray[i++];
        } else {
            array[k++] = rightArray[j++];
        }
    }

    // Copy remaining elements of leftArray
    while (i < leftSize) {
        array[k++] = leftArray[i++];
    }

    // Copy remaining elements of rightArray
    while (j < rightSize) {
        array[k++] = rightArray[j++];
    }
}
```

### Exemple sur une liste chaînée
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

## Complexité

| Algorithme de tri | Complexité moyenne | Complexité pire cas |
|-------------------|--------------------|----------------------|
| Tri par insertion | O(n²)              | O(n²)                |
| Tri à bulles      | O(n²)              | O(n²)                |
| Tri rapide        | O(n log n)         | O(n²)                |
| Tri fusion        | O(n log n)         | O(n log n)           |
