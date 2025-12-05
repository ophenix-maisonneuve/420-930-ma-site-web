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

### 3. Créez/inspectez l’interface `GestionnaireClassement`
Créez une interface afin de définir les opérations indispensables au classement.
```java
public interface GestionnaireClassement {
    void ajouter(Joueur joueur);
    void supprimer(Joueur joueur);
    Joueur meilleur();
    Joueur pire();
    void afficher();
}
```
{: .highlight}
> Cette interface servira de **contrat** pour votre gestionnaire basé sur un arbre.

---

## 1. Ordre naturel (`Comparable`) pour `Joueur`
### 1.1. Créez/complétez la classe `Joueur` avec `Comparable<Joueur>`
L’ordre naturel doit trier **d’abord par score décroissant**, puis **par pseudo croissant**.
- Pourquoi la cohérence entre `compareTo` et `equals` est-elle importante dans un `TreeSet` ?
- Que se passe-t-il si deux joueurs ont **le même score** et **le même pseudo** ?

```java
public class Joueur implements Comparable<Joueur> {
    private String pseudo;
    private int score;
    private java.time.Instant inscription;

    public Joueur(String pseudo, int score, java.time.Instant inscription) {
        this.pseudo = pseudo;
        this.score = score;
        this.inscription = inscription;
    }

    public String getPseudo() {
        return this.pseudo;
    }

    public void setPseudo(String pseudo) {
        this.pseudo = pseudo;
    }

    public int getScore() {
        return this.score;
    }

    public void setScore(int score) {
        this.score = score;
    }

    public java.time.Instant getInscription() {
        return this.inscription;
    }

    public void setInscription(java.time.Instant inscription) {
        this.inscription = inscription;
    }

    @Override
    public int compareTo(Joueur autre) {
        int cmpScore = Integer.compare(autre.getScore(), this.getScore()); // décroissant
        if (cmpScore != 0) {
            return cmpScore;
        }
        return this.getPseudo().compareTo(autre.getPseudo()); // croissant
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) {
            return true;
        }
        if (obj == null || getClass() != obj.getClass()) {
            return false;
        }
        Joueur autre = (Joueur) obj;
        return this.pseudo.equals(autre.pseudo);
    }

    @Override
    public int hashCode() {
        return java.util.Objects.hash(this.pseudo);
    }

    @Override
    public String toString() {
        return "Joueur{" +
               "pseudo='" + this.pseudo + '\'' +
               ", score=" + this.score +
               ", inscription=" + this.inscription +
               '}';
    }
}
```
{: .astuce}
> Si `compareTo` retourne **0**, l’élément est considéré **doublon** par le `TreeSet`.

### 1.2. Testez l’ajout et l’affichage
Créez un `TreeSet<Joueur>`, ajoutez quelques joueurs et affichez-les.
- Dans **quel ordre** les joueurs sont-ils affichés ?
- Que se passe-t-il si vous modifiez le **score** d’un joueur **déjà présent** dans le set ?

---

## 2. `GestionnaireClassementTreeSet`
### 2.1. Créez la classe et stockez un `NavigableSet<Joueur>`
La classe doit utiliser un `TreeSet`.
```java
public class GestionnaireClassementTreeSet implements GestionnaireClassement {
    private final java.util.NavigableSet<Joueur> classement = new java.util.TreeSet<>();

    @Override
    public void ajouter(Joueur joueur) {
        this.classement.add(joueur);
    }

    @Override
    public void supprimer(Joueur joueur) {
        this.classement.remove(joueur);
    }

    @Override
    public Joueur meilleur() {
        return this.classement.first();
    }

    @Override
    public Joueur pire() {
        return this.classement.last();
    }

    @Override
    public void afficher() {
        for (Joueur j : this.classement) {
            System.out.println(j);
        }
    }
}
```
- Quelle est la **complexité grand O** de `add`, `remove` et `contains` dans un `TreeSet` ?
- Pourquoi `first()` et `last()` sont-ils en général **O(1)** ?

### 2.2. Ajoutez deux méthodes utilitaires
Implémentez :
- `topN(int n)` pour retourner les **n meilleurs**.
- `entreScores(int minInclus, int maxInclus)` pour obtenir une **fenêtre de scores**.

```java
public java.util.Set<Joueur> topN(int n) {
    java.util.Set<Joueur> resultat = new java.util.LinkedHashSet<>();
    int compteur = 0;
    for (Joueur j : this.classement) {
        resultat.add(j);
        compteur = compteur + 1;
        if (compteur >= n) {
            break;
        }
    }
    return resultat;
}

public java.util.Set<Joueur> entreScores(int minInclus, int maxInclus) {
    Joueur borneHaute = new Joueur("__borne_haute__", maxInclus, java.time.Instant.EPOCH);
    Joueur borneBasse = new Joueur("__borne_basse__", minInclus, java.time.Instant.EPOCH);
    return this.classement.subSet(borneHaute, true, borneBasse, true);
}
```
{: .astuce}
> L’ordre est **décroissant** par score : la **borne haute** correspond au **score le plus élevé** et la **borne basse** au **score le plus faible**.

---

## 3. `Comparator` alternatif : ancienneté puis score
### 3.1. Créez `ComparatorAnciennetePuisScore`
Le tri doit privilégier l’**inscription la plus ancienne** en premier, puis le **score décroissant**, puis le **pseudo**.
```java
public class ComparatorAnciennetePuisScore implements java.util.Comparator<Joueur> {
    @Override
    public int compare(Joueur j1, Joueur j2) {
        int cmpInscription = j1.getInscription().compareTo(j2.getInscription()); // plus ancien en premier
        if (cmpInscription != 0) {
            return cmpInscription;
        }
        int cmpScore = Integer.compare(j2.getScore(), j1.getScore()); // score décroissant
        if (cmpScore != 0) {
            return cmpScore;
        }
        return j1.getPseudo().compareTo(j2.getPseudo());
    }
}
```

### 3.2. Instanciez un `TreeSet` avec ce comparator
```java
java.util.NavigableSet<Joueur> classementParAnciennete = new java.util.TreeSet<>(new ComparatorAnciennetePuisScore());
```
- En présence d’un `Comparator`, pourquoi la notion de **doublon** dépend-elle de `compare` et non de `equals` ?

---

## 4. Navigation dans le classement (`NavigableSet`)
### 4.1. Rival direct
Pour un joueur donné, récupérez son **rival direct** au-dessus et en dessous.
- Quelle méthode utiliser pour le joueur juste **au-dessus** ?
- Quelle méthode utiliser pour le joueur juste **en dessous** ?
- Quels sont les **cas limites** ?

### 4.2. Top 5 et fenêtres
- Extraire un **top 5** : vaut-il mieux **itérer** ou utiliser une **vue** du set (p. ex. `headSet`) ? Pourquoi ?
- Extraire une **fenêtre de scores** (par ex. 1200–1500) avec `subSet` en conservant l’ordre **décroissant**.

---

## 5. Tests et validation
### 5.1. Génération et vérifications
- Générez **100 joueurs** (pseudos distincts), scores aléatoires **[800, 2000]**, inscriptions réparties sur **2 ans**.
- Vérifiez : aucun **doublon**, ordre **décroissant** par score, **pseudo** en brise-égalité.

### 5.2. Mesures simples
- Comparez le temps d’ajout dans `TreeSet` avec une approche `ArrayList` + `sort` après **chaque insertion**.
- Discutez des résultats observés.

---

## 6. Bonus
### 6.1. Deux classements simultanés
Maintenez **deux** `TreeSet` :
- Un par **score** (ordre naturel).
- Un par **ancienneté** (via `ComparatorAnciennetePuisScore`).

Comment éviter la **duplication** coûteuse de données ?

### 6.2. Vue immuable
Exposez le classement via `Collections.unmodifiableNavigableSet(...)`.

### 6.3. Export CSV
Exportez le **top 100** en CSV pour intégration à un tableau de bord.

---

## Questions de réflexion
- Pourquoi `TreeSet` rejette-t-il certains ajouts quand `compareTo` ou `compare` retourne **0** ?
- Que se passe-t-il si l’ordre de tri change **dynamiquement** (score mis à jour) pendant que l’élément est **déjà présent** dans le set ? Quelle procédure faut-il suivre ?
- Dans quels cas un `TreeMap<Integer, java.util.Set<Joueur>>` est-il **plus adapté** qu’un `TreeSet<Joueur>` ?
