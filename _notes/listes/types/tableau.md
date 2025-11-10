---
layout: default
parent: "Listes et tableaux"
title: "Tableau"
nav_order: 1
published: true
---

# Tableau (Array)

Un tableau est une structure de données à taille fixe où chaque élément est accessible directement par son index. Il est efficace pour les accès rapides mais coûteux pour les insertions et suppressions.

```java
public class MonTableau {
    public static void main(String[] args) {
        int[] tableau = new int[5];
        tableau[0] = 10;
        tableau[1] = 20;
        tableau[2] = 30;
        for (int i = 0; i < tableau.length; i++) {
            System.out.println(tableau[i]);
        }
    }
}
```

## Opérations sur les tableaux

### Ajout

<details markdown="1">
<summary markdown="span">**Ajout simple (écrasement)**</summary>

Voici une insertion simple, où l'on écrase potentiellement l'élément qui était déjà présent à l'index donné.Dans un tableau, l'ajout nécessite souvent de décaler les éléments ou de recréer le tableau si sa taille est fixe.
```java
int[] array = new int[5];
array[0] = 10; // ajout en début
array[2] = 30; // ajout au milieu
array[4] = 50; // ajout en fin
```
</details>

<details markdown="1">
<summary markdown="span">**Ajout avec redimensionnement**</summary>
Dans bien des cas, on veut plutôt ajouter aux éléments déjà existants, ce qui demande plutôt de décaler les éléments ou même de recréer le tableau

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
</details>

### Suppression

<details markdown="1">
<summary markdown="span">**Suppression simple (sans redimensionnement)**</summary>

```java
int[] array = {10, 20, 30, 40};
// Suppression au milieu (index 1)
for (int i = 1; i < array.length - 1; i++) {
    array[i] = array[i + 1];
}
```
</details>

<details markdown="1">
<summary markdown="span">**Suppression avec redimensionnement**</summary>

```java
int[] original = {10, 20, 30, 40};
int newValue = 25;
int deleteIndex = 3;

// Création d'un nouveau tableau avec une taille réduite
int[] resized = new int[original.length - 1];

// Copier les éléments avant l'index à supprimer
for (int i = 0; i < deleteIndex; i++) {
    resized[i] = original[i];
}

// Décaler les éléments restants
for (int i = deleteIndex + 1; i < original.length; i++) {
    resized[i - 1] = original[i];
}
```
</details>


### Tri

</details>

<details markdown="1">
<summary markdown="span">**Tri par insertion**</summary>

Le tri par insertion fonctionne en construisant progressivement une liste triée en insérant chaque nouvel élément à sa position correcte.

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
</details>

</details>

<details markdown="1">
<summary markdown="span">**Tri à bulles**</summary>

Le tri à bulles compare chaque paire d'éléments adjacents et les échange si nécessaire, répétant ce processus jusqu'à ce que la liste soit triée.

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
</details>

</details>

<details markdown="1">
<summary markdown="span">**Tri rapide (*Quick Sort*)**</summary>

Le tri rapide est un algorithme de tri efficace basé sur le principe du diviser pour régner. Il choisit un pivot et partitionne le tableau autour de ce pivot.

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
</details>

</details>

<details markdown="1">
<summary markdown="span">**Tri par fusion (*Merge Sort*)**</summary>

Le tri par fusion divise la liste en deux moitiés, trie chaque moitié récursivement, puis fusionne les deux listes triées.

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
</details>


### Recherche

</details>

<details markdown="1">
<summary markdown="span">**Recherche linéaire**</summary>
```java
for (int i = 0; i < array.length; i++) {
    if (array[i] == target) {
        return i;
    }
}
```
</deatils>

</details>

<details markdown="1">
<summary markdown="span">**Recherche binaire**</summary>

```java
int left = 0, right = array.length - 1;
while (left <= right) {
    int mid = (left + right) / 2;
    if (array[mid] == target) {
        return mid;
    } else if (array[mid] < target) {
        left = mid + 1;
    } else {
        right = mid - 1;
    }
}
```
</details>
