---
layout: default
title: "Structures de données - semaine 1"
parent: "Structures de données"
nav_order: 1
published: true
---

# Exercice : Structures de données - Listes

## Contexte
Bienvenue au **Lobby des Braves**! Vous devez créer une application qui gère les joueurs inscrits au jeu de rôle en ligne. Cette semaine, nous allons nous concentrer sur la gestion de la liste des joueurs inscrits.

## Objectifs
Implémenter la gestion des joueurs dans une liste en utilisant le **pattern Strategy** pour permettre de changer d'implémentation (ArrayList, LinkedList) sans modifier la logique métier.

![Diagramme Liste](https://media.geeksforgeeks.org/wp-content/uploads/20230703105736/ArrayList-in-Java.png)
_Source: GeeksforGeeks_

## Étapes préparatoires

### 1. Clonez le dépôt de l'exercice

```bash
git clone git@github.com:ophenix-420-930-ma-24636/lobby-braves.git
```
ou
```bash
git clone https://github.com/ophenix-420-930-ma-24636/lobby-braves.git
```

### 2. Lancez le projet Java
```bash
mvn clean package
java -jar target/lobby-braves-1.0-SNAPSHOT.jar
```
ou
```bash
mvn clean compile exec:java
```
ou directement à partir de votre IDE.

Familiarisez-vous avec le menu, qui vous affichera toutes les opérations que nous devrons être en mesure d'exécuter lorsque l'application sera complétée. Pour l'instant, la plupart des options lanceront une `UnsupportedOperationException` ou ne feront simplement rien. Au fur et à mesure du développement, les options commenceront à fonctionner.

## Étapes

### 1. Analysez l'interface `GestionnaireJoueurs` et son implémentation fournie `GestionnaireJoueursListeChainee`
- L'implémentation `GestionnaireJoueursListeChainee` fait-elle usage des structures fournies par Java ?
   - Si oui, lesquelles ?
   - Si non, comment gère-t-elle la liste ?

### 2. Créez une autre implémentation de l'interface `GestionnaireJoueurs` appelée `GestionnaireJoueursLinkedList`
- Cette implémentation doit utiliser une `LinkedList` pour gérer la liste au lieu d'une gestion manuelle.

### 3. Implémentez la méthode `ajouter` dans `GestionnaireJoueursLinkedList`

### 4. Implémentez la méthode `supprimer` dans `GestionnaireJoueursLinkedList`

### 5. Analysez la méthode `afficher` dans `GestionnaireJoueursLinkedList`
Cette méthode doit parcourir la liste dans son ordre actuel (sans faire de tri).
- Quelle méthode devriez-vous ré-implémenter dans la classe `Joueur` pour rendre l'affichage plus lisible ?
   - Implémentez cette méthode.
- Dans quel ordre les joueurs sont-ils affichés ?
- Existe-t-il une façon simple d'inverser cet ordre ?
   - Utiliser cette façon de faire pour permettre l'affichage en ordre inverse.

### 6. Implémentez la méthode `trier` dans `GestionnaireJoueursLinkedList`
- Quel algorithme de tri est utilisé lors de l'appel à `List.sort()` ?
- Est-il possible de forcer un algorithme différent ? Pourquoi ?
- Comment la méthode `List.sort()` est-elle capable de déterminer sur quel(s) champ(s) de la classe `Joueur` se baser pour établir l'ordre?

## Bonus
- Ajoutez une **stratégie thread-safe** avec `CopyOnWriteArrayListStrategy`.
- Expliquez les avantages et inconvénients.

## Bonus
- Ajouter un remove avec une regex

## Bonus
- Trier dans un ordre différent avec un Comparator

