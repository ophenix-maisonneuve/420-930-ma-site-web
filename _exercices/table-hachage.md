---
layout: default
title: "Table de hachage"
nav_order: 8
has_toc: false
published: false
---

# Exercice : Implémentation d’une table de hachage

## Objectifs

- Comprendre le fonctionnement d’une **table associative** reposant sur une **fonction de hachage** (table de hachage).
- Implémenter les opérations de base : **ajout/mise à jour** (`ajouter`), **suppression** (`supprimer`), **recherche** (`contient`), **affichage par seau** (`afficherParSeau`).
- Observer la gestion des **collisions par chaînage séparé**.

{: .highlight}
> En moyenne, avec une bonne fonction de hachage et un facteur de charge maîtrisé, `ajouter/contient/supprimer` sont proches de **O(1)** amorti ; le **pire cas** est **O(n)** lorsque les collisions s’accumulent.

---

## Contexte

On vous fournit une classe `TableHachage` où :
- `ajouter(String cle, Object valeur)` et `toString()` sont **déjà implémentées** ;
- `contient(String cle)`, `afficherParSeau()` et `supprimer(String cle)` sont **à implémenter** et lèvent `UnsupportedOperationException`.

---

## Étapes préparatoires

### 1. Clonez le dépôt de l'exercice

```bash
git clone git@github.com:ophenix-420-930-ma-24636/table-hachage.git
```
ou
```bash
git clone https://github.com/ophenix-420-930-ma-24636/table-hachage.git
```

### 2. Lancez le projet Java
```bash
mvn clean package
java -jar target/table-hachage-1.0-SNAPSHOT.jar
```
ou
```bash
mvn exec:java
```
ou directement à partir de votre IDE.

Familiarisez-vous avec le menu, qui vous permet déjà d'ajouter des éléments dans la table.

---

## Questions

### 1. Étudiez les classes `Entry` et `TableHachage`
- Expliquez le rôle de `indexFor(String cle)`.
- À quoi sert le masquage du bit de signe ?
- À quoi sert l'opérateur **modulo** avec la taille de la table

### 2. Étudiez la classe `TableHachage`
- Expliquez comment `ajouter` distingue **mise à jour** vs **insertion**.

### 3. Implémentez la suppression dans la table.
- Implémentez `Object supprimer(String cle)` qui **retourne l’ancienne valeur** si supprimée, sinon `null`.
   - Gérez les cas : **tête**, **milieu/fin** de chaîne, **clé absente**.
- Quelle est la complexité grand O de la suppression dans la majorité des cas ? Dans le pire cas ?

{: .astuce}
> Pour l'implémentation, utilisez deux pointeurs `prev` / `curr` et mettez à jour le lien avec `setNext`.

### 4. Implémentez la recherche dans la table.
- Implémentez la méthode  `boolean contient(String cle)` :
- Validez depuis le menu : cas présent/absent et valeur `null`.

{: .astuce}
> Avant de vous lancer dans une implémentation compliquée, observez bien les méthodes déjà fournies. L'une d'elles peut être réutilisée ici...

### 5. Exercice Bonus: Redimensionnement
- Ajoutez `resize()` (×2 quand `size > table.length * loadFactor`) et appelez‑le dans `ajouter`.

---

## Ressources
- Diagramme de **chaînage séparé** : https://algs4.cs.princeton.edu/34hash/images/separate-chaining.png
- Synthèse **Hash table** (définitions, complexités) : https://en.wikipedia.org/wiki/Hash_table
