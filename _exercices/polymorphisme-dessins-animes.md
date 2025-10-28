---
layout: default
title: "Polymorphisme en Java"
nav_order: 3
has_toc: false
published: true
---
# Exercice : Polymorphisme en Java

## Objectif

Pratiquer le polymorphisme en Java à l'aide d'une interface, d'une classe abstraite et de sous-classes concrètes.

## Contexte

Vous allez modéliser des personnages de dessins animés célèbres : Lisa Simpson, Eric Cartman et Stewie Griffin.

## Étapes

### 1. Créez une interface `PersonnageAnime`

Cette interface doit contenir les méthodes suivantes :

- `String getNom()`
- `void parler()`
- `void agir()`

### 2. Créez une classe abstraite `AbstractPersonnage` qui implémente `PersonnageAnime`

- Ajoutez un champ `nom` privé.
- Ajoutez un constructeur qui prend en paramètre le nom du personnage (`String`)
- Implémentez la méthode `getNom()` dans la classe abstraite.
  - Cette méthode doit retourner le nom du personnage.
- Implémentez la méthode `parler()` dans la classe abstraite. Cette méthode doit écrire
  - Cette méthode doit écrire sur la console `Bonjour, je suis {nom du personnage}!`
- Laissez la méthode `agir()` non implémentées (abstraite).

### 3. Créez trois classes concrètes qui étendent `AbstractPersonnage`

- `LisaSimpson`
- `EricCartman`
- `StewieGriffin`

Implémentez la méthode `agir()` dans chaque classe avec un comportement propre au personnage. Si vous les connaissez moins:

- Lisa

### 4. Dans une classe `Main`, créez une liste de `PersonnageAnime` contenant les trois personnages

- Créez une méthode
- Parcourez la liste et appelez les méthodes `parler()` et `agir()` sur chaque élément.

## Étape supplémentaire : interaction entre personnages

Ajoutez une méthode `interagirAvec(PersonnageAnime autre)` dans l'interface `PersonnageAnime`. Cette méthode doit permettre à un personnage d'interagir avec un autre personnage en affichant un message personnalisé.

### Exemple :

```java
public void interagirAvec(PersonnageAnime autre) {
    System.out.println(this.getNom() + " interagit avec " + autre.getNom());
}
```

Implémentez cette méthode dans chaque sous-classe (`LisaSimpson`, `EricCartman`, `StewieGriffin`) avec un message spécifique à leur personnalité.

Testez ensuite ces interactions dans une boucle où chaque personnage interagit avec les autres.
