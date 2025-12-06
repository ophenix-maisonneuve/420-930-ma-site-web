---
layout: default
title: "Structures de données - semaine 3"
parent: "Structures de données"
nav_order: 3
published: false
---

## 2. Interfaces `Map` / `NavigableMap` et implémentation `TreeMap`
Votre implémentation du gestionnaire de classement fonctionne bien, mais vous regrettez de ne pas avoir de ***réelle*** gestion des ex-aequo. En effet, dans votre implémentation précédente, deux joueurs ayant le même score ne partageront pas le même rang, car le comparateur doit forcément prioriser un joueur par rapport à l'autre.

Vous décidez donc d'explorer une alternative : utiliser une implémentation table associative (`Map`) ordonnée utilisant un arbre rouge-noir en arrière-plan: `TreeMap`. Vous tentez d'évaluer si, pour votre scénario d'utilisation, cette structure pourrait mieux répondre au besoin.

### 2.1. Créez une nouvelle implémentation de l'interface `GestionnaireClassement` appelée `GestionnaireJoueursTreeMap`
Cette implémentation doit utiliser une `TreeMap` pour gérer le classement.
- Gardez une référence vers un nouveau `TreeMap<Integer, Set<Joueur>>` comme champ dans la classe.
  - La **clé** est le score du joueur
  - La **valeur** est un ensemble d'instances de `Joueur` ayant le même score.

### 2.2. Implémentez la méthode `ajouter(Joueur joueur)`
Cette méthode doit ajouter le joueur à la bonne position dans le classement.
- Quelle méthode de `TreeMap` doit être utilisée pour faire l'ajout ?
- Quelle est la complexité grand O de l'ajout dans un `TreeMap` ?
- Est-ce que la performance est meilleure qu'avec un `TreeSet` ? Pourquoi ?

### 2.3. Gérez le cas où on insère un nouveau score
Il peut arriver qu'aucun joueur n'ait le score à insérer. Dans ces cas, il faudra d'abord créer un nouveau `Set`, puis y insérer le joueur, et ensuite ajouter le score (clé) et le nouveau `Set` (valeur).
- Analysez les méthodes `computeIfAbsent` et `merge` de l'interface `Map`.
- Ces méthodes peuvent-elles vous être utiles ?
- Modifiez votre implémentation de la méthode `ajouter(Joueur joueur)` 
- Votre modifications change-t-elle la complexité grand O de cette méthode ?

### 2.3. Implémentez la méthode `afficher()`
Cette méthode doit afficher le classement tel qu'il est présentement stocké dans le `TreeMap`
- Comment pouvez-vous itérer sur la map ?
- Quel est l'ordre d'itération que vous observez ?
- Avez-vous besoin de modifier l'ordre naturel de `Joueur` ou d'utiliser un `Comparator` ? Pourquoi ?
- Quelle est la complexité grand O de la méthode `afficher()` ? Pourquoi ?

### 2.4. Implémentez la méthode `supprimer(Joueur joueur)`
Cette méthode doit supprimer un joueur du classement.
- Quelle méthode de `TreeMap` doit être utilisée pour faire la suppression ?
- Quelle est la complexité grand O de la suppression dans un `TreeMap` ?
- Est-ce que la performance est meilleure qu'avec un `TreeSet` ? Pourquoi ?

### 2.5. Implémentez la méthode `trouverRival(Joueur joueur)`
Cette méthode doit trouver le joueur ayant le score le plus rapproché du joueur passé en paramètre (soit plus haut ou plus bas).
- Pouvez-vous utiliser une méthode similaire à votre implémentation dans `GestionnaireClassementTreeSet` ?
- Implémentez la méthode de la façon la plus optimale
  - Quelle est la complexité grand O de votre implémentation ?


### 2.6. Implémentez la méthode `trouverRivaux(Joueur joueur, int ecart)`
Cette méthode doit trouver tous les joueurs se trouvant à l'intérieur de l'écart acceptable (soit au-dessus du joueur ou en-dessous).
- Pouvez-vous utiliser une méthode similaire à votre implémentation dans `GestionnaireClassementTreeSet` ?
- Implémentez la méthode de la façon la plus optimale
  - Quelle est la complexité grand O de votre implémentation ?

### 2.7. Implémentez les méthodes `meilleurs(int n)` et `pires(int n)`
Ces méthodes doivent respectivement retourner les n meilleurs ou pires joueurs.
- Analysez les méthodes `headSet` et `tailSet` de `TreeSet`.
  - Ces méthodes sont-elles utiles dans notre contexte? Pourquoi ?
- Proposez une implémentation la plus optimale possible pour chacune des deux méthodes.
  - Quelle est la complexité grand O de votre implémentation ?

## Questions de réflexion
- Dans quel(s) cas votre implémentation `GestionnaireClassementTreeSet` serait-elle avantageuse ?
- Dans quel(s) cas votre implémentation `GestionnaireClassementTreeMap` serait-elle avantegeuse ?

## 3. Bonus : Structure d'arbre avec concurrence (*thread-safety*)

### 3.1. `TreeSet` synchronisé avec un verrou
- 

### 3.2. Utilisation d'un `ConcurrentSkipListSet`
`ConcurrentSkipListSet` est une autre implémentation de `NavigableSet`. Il n'utilise pas