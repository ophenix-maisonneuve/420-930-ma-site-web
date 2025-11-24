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
Implémenter la gestion des joueurs dans plusieurs types de listes différentes afin de déterminer les forces et les faiblesses de chaque implémentation.


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

Familiarisez-vous avec le menu, qui vous affichera les opérations que nous devrons être en mesure d'exécuter lorsque l'application sera complétée. Pour l'instant, la plupart des options lanceront une `UnsupportedOperationException` ou ne feront simplement rien. Au fur et à mesure du développement, les options commenceront à fonctionner.

### 3. Analysez l'interface `GestionnaireJoueurs` et son implémentation fournie `GestionnaireJoueursListeChainee`
- L'implémentation `GestionnaireJoueursListeChainee` fait-elle usage des Collections fournies par Java ?
   - Si oui, lesquelles ?
   - Si non, comment gère-t-elle la liste ?

{: .highlight}
> Certaines opérations ne sont pas implémentées de manière optimale dans cette version.

## 1. LinkedList

### 1.1. Créez une nouvelle implémentation de l'interface `GestionnaireJoueurs` appelée `GestionnaireJoueursLinkedList`
Cette implémentation doit utiliser une `LinkedList` pour gérer la liste au lieu d'une gestion manuelle.
- Gardez une référence vers une nouvelle `LinkedList` comme champ dans la classe.
- Toutes les opérations des questions suivantes manipuleront cette liste.
- Changez l'initialisation du champ `Lobby.gestionnaireJoueurs` pour qu'il utilise votre nouvelle implémentation.
```java
private GestionnaireJoueurs gestionnaireJoueurs = new GestionnaireJoueursLinkedList();
```

### 1.2. Implémentez la méthode `ajouter(Joueur)` dans `GestionnaireJoueursLinkedList`
Le joueur doit être ajouté à la fin de la liste.
- Quel est le comportement par défaut de la méthode `add()` sur une `List` ? 
- Si vous aviez voulu insérer ailleurs qu'à la fin, comment auriez-vous pu faire ?

### 1.3. Implémentez la méthode `supprimer(Joueur)` dans `GestionnaireJoueursLinkedList`
Cette méthode doit supprimer un `Joueur` s'il possède le même pseudo que l'instance de `Joueur` passé en paramètre.
- Est-ce qu'un appel à `List.remove(joueur)` fonctionne ? Pourquoi ?
- Modifiez le code de la classe `Joueur` pour que l'appel à `List.remove(joueur)` fonctionne correctement
  - ***Indice:** il s'agit d'une méthode à ré-implémenter dans la classe `Joueur`*


### 1.4. Implémentez la méthode `afficher()` dans `GestionnaireJoueursLinkedList`
Cette méthode doit parcourir la liste dans son ordre actuel (sans faire de tri) et afficher le joueur en utilisant `System.out.println(joueur)`
- Utilisez un `Iterator` pour itérer sur la liste et afficher les informations de chaque joueur.
- Est-ce que les informations sur les joueurs apparaissent dans un format lisible ?
- Modifiez le code de la classe `Joueur` pour que l'information affichée soit lisible et utilisable.
  - ***Indice:** il s'agit d'une méthode à ré-implémenter dans la classe `Joueur`*
- Dans quel ordre les joueurs sont-ils affichés ?


### 1.5. Implémentez la méthode `trier(Ordre)` dans `GestionnaireJoueursLinkedList`
- Quel algorithme de tri est utilisé lors de l'appel à `List.sort()` ?
- Est-il possible de forcer un algorithme différent ? Pourquoi ?
- Comment la méthode `List.sort()` est-elle capable de déterminer sur quel(s) champ(s) de la classe `Joueur` se baser pour établir l'ordre?
- Existe-t-il une façon simple de trier la liste en ordre décroissant plutôt qu'en ordre croissant ?
  - ***Indice:** il suffit d'appeler une méthode utilitaire `Collections.<quelque chose>` après avoir fait le tri.*
- Utiliser cette façon de faire pour implémenter le tri en ordre inverse lorsque le paramètre `Ordre.INVERSE` est passé à la méthode `trier`

