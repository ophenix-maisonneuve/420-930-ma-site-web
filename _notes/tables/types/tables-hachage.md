---
layout: default
parent: "Tables associatives"
title: "Tables de hachage"
nav_order: 2
published: true
---

# Tables de hachage
Une **table de hachage** est une **table associative** qui utilise une **fonction de hachage** pour transformer les **clés** en indices. Dans cette page, nous présentons une implémentation pédagogique nommée **`TableHachage`** avec :

- **Chaînage séparé** (chaque seau est une **liste simplement chaînée** d’entrées),
- **Facteur de charge** `0,75`,
- **Redimensionnement ×2** quand `taille / capacité > 0,75`,
- **Clé `null` interdite**, **valeur `null` autorisée**.

![Table de hachage avec chaînage séparé — Princeton Algorithms](https://algs4.cs.princeton.edu/34hash/images/separate-chaining.png)


> **Complexités (moyenne)** : `put/get/remove` en **`O(1)` amorti**  
> **Pire cas** : `O(n)` si les collisions se concentrent anormalement.

---

## Structure (rappel)

```java
// Schéma simplifié utilisé dans tous les extraits ci-dessous.
private static class Entry {
    private final String key;
    private Object value;
    private Entry next;

    Entry(String key, Object value, Entry next) {
        this.key = key;
        this.value = value;
        this.next = next;
    }

    public String getKey() { return key; }
    public Object getValue() { return value; }
    public void setValue(Object value) { this.value = value; }
    public Entry getNext() { return next; }
    public void setNext(Entry next) { this.next = next; }
}
private Entry[] table; // tableau de seaux
private int size; // nombre de paires (clé, valeur)
private final float loadFactor; // ex. 0.75f
```

---

## Fonctions utilitaires

<details>
<summary><strong>indexFor(key) — transformer le hash en index de seau</strong></summary>

```java
/** Calcule l'index de seau pour une clé donnée. */
private int indexFor(String key) {
    int h = key.hashCode();
    // Masque le bit de signe pour éviter les indices négatifs puis modulo capacité
    return (h & 0x7fffffff) % table.length;
}
```
</details>

<details>
<summary><strong>findEntry(key) — retrouver le maillon (si présent)</strong></summary>

```java
/** Retourne l'entrée (maillon) associée à la clé, ou null si absente. */
private Entry findEntry(String key) {
    if (key == null) {
        throw new NullPointerException("La clé ne peut pas être nulle");
    }

    int index = indexFor(key);
    for (Entry e = table[index]; e != null; e = e.getNext()) {
        if (key.equals(e.getKey())) {
            return e;
        }
    }
    return null;
}
```
</details>

---

## Ajout / Mise à jour

<details>
<summary><strong>put(key, value) — insérer ou mettre à jour (O(1) amorti)</strong></summary>

```java
/**
 * Insère la paire (key, value) ou met à jour si la clé existe déjà.
 * @return l'ancienne valeur si mise à jour, sinon null (nouvelle entrée).
 */
public Object put(String key, Object value) {
    if (key == null) {
        throw new NullPointerException("La clé ne peut pas être nulle");
    }

    // 1) Redimensionnement éventuel (préventif) pour maintenir le load factor
    if (needsResize()) {
        resize();
    }

    // 2) Index du seau
    int index = indexFor(key);

    // 3) Parcourir la chaîne : si la clé existe → mise à jour
    for (Entry e = table[index]; e != null; e = e.getNext()) {
        if (key.equals(e.getKey())) {
            Object old = e.getValue();
            e.setValue(value);
            return old;
        }
    }

    // 4) Sinon, insertion en tête de chaîne (O(1))
    table[index] = new Entry(key, value, table[index]);
    size++;
    return null;
}

/** Vrai si une insertion supplémentaire dépasserait le facteur de charge. */
private boolean needsResize() {
    return size + 1 > (int)(table.length * loadFactor);
}
```
</details>

---

## Suppression

<details>
<summary><strong>remove(key) — retirer une paire (O(1) amorti)</strong></summary>

```java
/**
 * Supprime la paire (key, ?) si présente.
 * @return l'ancienne valeur si supprimée, sinon null.
 */
public Object remove(String key) {
    if (key == null) throw new NullPointerException("La clé ne peut pas être nulle");
    int index = indexFor(key);

    Entry prev = null;
    Entry curr = table[index];

    while (curr != null) {
        if (key.equals(curr.key)) {
            // D'un coup de pointeur, on "saute" le maillon courant
            if (prev == null) {
                table[index] = curr.getNext(); // suppression en tête
            } else {
                prev.setNext(curr.getNext();    // suppression au milieu/fin
            }
            size--;
            return curr.value;
        }
        prev = curr;
        curr = curr.getNext();
    }
    return null; // clé absente
}
```
</details>

---

## Recherche par clé

<details>
<summary><strong>get(key) — retrouver la valeur (O(1) amorti)</strong></summary>

```java
/** Retourne la valeur associée à la clé, ou null si absente. */
public Object get(String key) {
    Entry e = findEntry(key);
    return (e == null) ? null : e.getValue();
}
```
</details>

<details>
<summary><strong>containsKey(key) — la clé est‑elle présente ?</strong></summary>

```java
/** Vrai si la clé est présente, même si la valeur associée est null. */
public boolean containsKey(String key) {
    return findEntry(key) != null;
}
```
</details>

---

# Tables de hachage

<details>
<summary><strong>resize() — doubler la capacité et re‑hacher toutes les entrées (O(n))</strong></summary>

```java
/** Double la capacité et re-hache toutes les entrées. Coût linéaire, mais rare. */
private void resize() {
    Entry[] old = this.table;
    Entry[] neu = new Entry[old.length * 2];
    this.table = neu;

    // Ré-insertion de tous les maillons dans le nouveau tableau de seaux
    for (Entry head : old) {
        Entry e = head;
        while (e != null) {
            Entry next = e.getNext(); // préserver la suite avant de relinker
            int idx = (e.getKey().hashCode() & 0x7fffffff) % neu.length;
            e.setNext(neu[idx]);
            neu[idx] = e;
            e = next;
        }
    }
}
```
</details>

---

## Parcours (exposition minimale)

<details>
<summary><strong>toString() — parcourir toutes les entrées pour afficher (O(n))</strong></summary>

```java
@Override
public String toString() {
    StringBuilder sb = new StringBuilder();
    sb.append("{");
    boolean first = true;
    for (Entry bucket : table) {
        for (Entry e = bucket; e != null; e = e.getNext()) {
            if (!first) {
        sb.append(", ");
    }
            first = false;
            sb.append(e.getKey()).append("=").append(String.valueOf(e.getValue()));
        }
    }
    sb.append("}");
    return sb.toString();
}
```
</details>

---

## Résumé des complexités

| Opération                      | Moyenne         | Pire cas |
|---                             |---              |---|
| `put(key, value)`              | `O(1)` amorti   | `O(n)` |
| `get(key)` / `containsKey(key)`| `O(1)` amorti   | `O(n)` |
| `remove(key)`                  | `O(1)` amorti   | `O(n)` |
| `resize()` (re‑hachage)        | —               | `O(n)` |
| Parcours complet               | `O(n)`          | `O(n)` |

{: .highlight}
> Les performances moyennes reposent sur un **bon hachage** des clés et un **facteur de charge maîtrisé** (ex. `0,75`) qui limite la longueur moyenne des chaînes.