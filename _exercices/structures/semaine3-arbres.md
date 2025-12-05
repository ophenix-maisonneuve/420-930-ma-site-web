---
layout: default
title: "Structures de données - semaine 3"
parent: "Structures de données"
nav_order: 3
published: false
---

# Exercice : Structures de données – Arbres

## Contexte
Bienvenue à nouveau dans **Le Lobby des Braves** ! Cette semaine, vous devez enrichir votre application en ajoutant un **classement des joueurs** basé sur leur **score**. Le classement doit être **trié automatiquement** et **sans doublons**. Pour y parvenir, vous utiliserez une structure en **arbre** : `TreeSet` (implémentation de `NavigableSet`).

## Objectifs
Implémenter un classement des joueurs à l’aide d’un `TreeSet` et travailler avec l’API `NavigableSet` afin de :
- Modifier l'**ordre naturel** (`Comparable`) pour la classe `Joueur` : **score décroissant**, puis **pseudo croissant** (bris d'égalité).
- Écrire un **`Comparator`** personnalisé pour trier plutôt par **score**, puis par **ancienneté d’inscription** en cas d'égalité.
- Utiliser les opérations de **navigation** d’un `NavigableSet` (`first`, `last`, `higher`, `lower`, `subSet`, `headSet`, `tailSet`).
- Comparer `TreeSet` et `TreeMap` lorsque de nombreux joueurs partagent le **même score**.

---

## Étapes préparatoires

### 1. Clonez (ou mettez à jour) le dépôt de l’exercice
```bash
git clone git@github.com:ophenix-420-930-ma-24636/lobby-braves.git
```
Ou, si vous avez déjà cloné le dépôt :
```bash
git pull
```

Si vous travaillez sur une autre branche:
```bash
git checkout <votre branche>
git fetch
git merge origin/main
```

### 2. Lancez le projet Java
```bash
mvn clean package
java -jar target/lobby-braves-1.0-SNAPSHOT.jar
```
Ou :
```bash
mvn clean compile exec:java
```
Ou directement à partir de votre IDE.

### 3. Analysez l’interface `GestionnaireClassement`
Cette interface définit plusieurs méthodes utiles pour les classements qu'il faudra implémenter :
```java
public interface GestionnaireClassement {
    void ajouter(Joueur joueur);
    void supprimer(Joueur joueur);
    //void rafraichir();
    Set<Joueur> pires(int n);
    Set<Joueur> meilleurs(int n);
    Set<Joueur> trouverRivaux(Joueur joueur, int ecart);
    Joueur trouverRival(Joueur joueur);
    void afficher();
}
```
---

## 1. Interface `NavigableSet` et implémentation `TreeSet`
Étant donné la nature hiérarchique d'un classement, vous décidez d'abord d'utiliser un `TreeSet` pour maintenir l'ordre dans le gestionnaire de classement. Cette structure utilise un arbre rouge-noir afin de s'assurer que l'arbre demeure équilibré, et garantit donc les opérations en O(log n).

### 1.1. Créez une nouvelle implémentation de l'interface `GestionnaireClassement` appelée `GestionnaireJoueursTreeSet`
Cette implémentation doit utiliser un `TreeSet` pour gérer l'arbre de classement.
- Gardez une référence vers un nouveau `TreeSet<Joueur>` comme champ dans la classe.
- Ne fournissez pas de `Comparator` lors de la création du `TreeSet`.

### 1.2. Implémentez la méthode `ajouter(Joueur joueur)`
Cette méthode doit ajouter le joueur à la bonne position dans le classement.
- Quelle méthode de `TreeSet` doit être utilisée pour faire l'ajout ?
- Pouvez-vous résumer les principales étapes effectuées par l'arbre rouge-noir sous-jacent lors de l'insertion ?
  - ***Indice :** Vous pouvez consulter les [notes de cours](../notes/arbre-rouge-noir)
- Quelle est la complexité grand O de l'ajout dans un `TreeSet` (donc dans un arbre rouge-noir) ? Pourquoi ?

### 1.3. Implémentez la méthode `afficher()`
Cette méthode doit afficher le classement tel qu'il est présentement stocké dans le `TreeSet`
- Comment pouvez-vous itérer sur l'arbre ?
- Quel est l'ordre d'itération que vous observez ?
- Quelle interface permet aux objets de type `Joueur` d'être triés même en l'absence d'un `Comparator` ?
- Quelle méthode de la classe `Joueur` définit l'ordre naturel de tri ?
- Quelle est la complexité grand O de la méthode `afficher()` ? Pourquoi ?

### 1.4. Modifiez l'ordre naturel de la classe `Joueur`
L’ordre naturel doit maintenant trier **d’abord par score décroissant**, puis **par pseudo croissant** (ordre alphabétique).
- Pourquoi l'ajout d'un deuxième critère de comparaison en plus du score (le pseudo) était-il nécessaire ?
- Observez le changement de comportement de la méthode `afficher()` que vous avez implémentée précédemment.
- Ce changement a-t-il modifié la complexité grand O de la méthode `afficher()` ? Pourquoi ?

### 1.5. Modifiez le score d'un joueur qui est déjà présent dans le classement
Observez ce qui se passe maintenant si on tente de modifier le score d'un joueur 
Dans la méthode `afficher`, ajoutez le code temporaire suivant **avant** l'affichage (il sera enlevé par la suite):
```java
// remplacez ici le nom de la variable par le nom que vous avez donné à votre TreeMap
this.classement.first().setScore(0);
```
- Lancer à nouveau l'affichage. Qu'observez-vous ?
- Que se passera-t-il si une classe appelante modifie le score des instances de `Joueur` qui sont traitées par `GestionnaireClassement`
- Modifiez votre code de façon à le protéger de ce comportement
  - *En d'autres mots, assurez-vous que les joueurs fournis à / retournés par `GestionnaireClassement` ne peuvent pas être modifiés à l'externe*

***N'oubliez pas d'enlever le code temporaire!***

### 1.6. Insérez un joueur qui est déjà présent dans le classement
Observez ce qui se passe maintenant si l'on tente d'ajouter deux fois le même joueur (même pseudo) mais avec des scores différents.
- Dans la méthode `ajouter(Joueur joueur)`, ajoutez du code temporaire qui effectue les opérations suivantes après l'ajout initial :
  - Modifier le score du joueur
  - Ajouter à nouveau le joueur dans le `TreeSet`
- Par exemple :
```java
// implémentation initiale
this.classement.add(joueur);

// code temporaire à ajouter
joueur.setScore(123456); // nouveau score
this.classement.add(joueur);
```
- Qu'observez-vous ? Pourquoi ?
- Proposez une modification possible à la méthode `ajouter(Joueur)` qui permettrait d'éviter ce scénario et implémentez-la.
- Ce changement a-t-il modifié la complexité grand O de la méthode `ajouter(Joueur)` ? Pourquoi ? 

***N'oubliez pas d'enlever le code temporaire!***

### 1.7. Utilisez un `Comparator` plutôt que l'ordre naturel
L'un des problèmes introduits par le changement d'ordre naturel de la classe `Joueur` et une incohérence entre une égalité logique (méthode `equals`) et la comparaison (méthode `compareTo`). Afin de demeurer cohérent, il est préférable que si `equals` entre deux instances retourne `true`, `compareTo` entre ces deux mêmes instances retourne `0`. Afin de régler ce problème:
- Changez l'implémentation de `Joueur.compareTo(Joueur joueur)` pour qu'elle soit cohérente avec l'implémentation de `equals` (normalement, on compare `Joueur.pseudo`)
- Ajoutez à votre `TreeSet` un `Comparator` qui trie de la façon suivante :
  - D'abord, tri sur le score (du plus grand au plus petit)
  - Ensuite, en cas d'égalité, donne priorité au joueur le plus ancien (champ `Joueur.inscription`)

### 1.8. Implémentez la méthode `supprimer(Joueur joueur)`
Cette méthode doit supprimer un joueur du classement.
- Quelle méthode de `TreeSet` doit être utilisée pour faire la suppression ?
- Pouvez-vous résumer les principales étapes effectuées par l'arbre rouge-noir sous-jacent lors de la suppression ?
  - ***Indice :** Vous pouvez consulter les [notes de cours](../notes/arbre-rouge-noir)
- Quelle est la complexité grand O de la suppression dans un `TreeSet` (donc dans un arbre rouge-noir) ? Pourquoi ?

### 1.9. Implémentez la méthode `trouverRival(Joueur joueur)`
Cette méthode doit trouver le joueur ayant le score le plus rapproché du joueur passé en paramètre (soit plus haut ou plus bas).
- Pouvez-vous implémenter cette méthode à l'aide d'un `for-each` ou d'un `Iterator` ? 
  - Si oui, quelle serait alors la complexité grand O de votre implémentation ?
  - Si non, pourquoi ?
- Existe-t-il des méthodes de `TreeSet` (ou de son interface `NavigableSet`) qui peuvent être utilisées ici ?
  - Si oui, lesquelles ?
  - Si non, pourquoi ?
- Implémentez la méthode de la façon la plus optimale
  - Quelle est la complexité grand O de votre implémentation ?


### 1.10. Implémentez la méthode `trouverRivaux(Joueur joueur, int ecart)`
Cette méthode doit trouver tous les joueurs se trouvant à l'intérieur de l'écart acceptable (soit au-dessus du joueur ou en-dessous).
- Pouvez-vous implémenter cette méthode à l'aide d'un `for-each` ou d'un `Iterator` ? 
  - Si oui, quelle serait alors la complexité grand O de votre implémentation ?
  - Si non, pourquoi ?
- Existe-t-il une méthode de `TreeSet` (ou de son interface `NavigableSet`) qui peut être utilisées ici ?
  - Si oui, laquelle ?
  - Si non, pourquoi ?
- Implémentez la méthode de la façon la plus optimale
  - Quelle est la complexité grand O de votre implémentation ?

### 1.11. Implémentez les méthodes `meilleurs(int n)` et `pires(int n)`
On veut maintenant mettre un place un *Wall of Fame* pour les meilleurs joueurs et un `*Wall of Shame* pour les pires joueurs (c'est de goût discutable, mais bon... Nous ne sommes pas les patrons!) Nous avons donc besoin de méthodes qui doivent, respectivement, retourner les n meilleurs ou pires joueurs.
- Analysez les méthodes `headSet` et `tailSet` de `TreeSet`.
  - Ces méthodes sont-elles utiles dans notre contexte? Pourquoi ?
- Proposez une implémentation la plus optimale possible pour chacune des deux méthodes.
  - Quelle est la complexité grand O de votre implémentation ?

## 2. Interfaces `Map` / `NavigableMap` et implémentation `TreeMap`
Votre implémentation du gestionnaire de classement fonctionne bien, mais vous regrettez de ne pas avoir de ***réelle** gestion des ex-aequo. En effet, dans votre implémentation précédente, deux joueurs ayant le même score ne partageront pas le même rang, car le comparateur doit forcément prioriser un joueur par rapport à l'autre.

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


