# Exercice : Polymorphisme avec des personnages de dessins animés

## Objectif
Pratiquer le polymorphisme en Java à l'aide d'une interface, d'une classe abstraite et de sous-classes concrètes.

## Contexte
Vous allez modéliser des personnages de dessins animés célèbres : Homer Simpson, Eric Cartman et Lisa Simpson.

## Étapes

### 1. Créez une interface `PersonnageAnime`
Cette interface doit contenir les méthodes suivantes :
- `String getNom()`
- `void parler()`
- `void agir()`

### 2. Créez une classe abstraite `PersonnageAbstrait` qui implémente `PersonnageAnime`
- Ajoutez un champ `nom` protégé.
- Implémentez la méthode `getNom()` dans la classe abstraite.
- Laissez les méthodes `parler()` et `agir()` non implémentées (abstraites).

### 3. Créez trois classes concrètes qui étendent `PersonnageAbstrait`
- `HomerSimpson`
- `EricCartman`
- `LisaSimpson`

Implémentez les méthodes `parler()` et `agir()` dans chaque classe avec un comportement propre au personnage.

### 4. Dans une classe `Main`, créez une liste de `PersonnageAnime` contenant les trois personnages
- Parcourez la liste et appelez les méthodes `parler()` et `agir()` sur chaque élément.

## Étape supplémentaire : interaction entre personnages

Ajoutez une méthode `interagirAvec(PersonnageAnime autre)` dans l'interface `PersonnageAnime`. Cette méthode doit permettre à un personnage d'interagir avec un autre personnage en affichant un message personnalisé.

### Exemple attendu :

```java
public void interagirAvec(PersonnageAnime autre) {
    System.out.println(this.getNom() + " interagit avec " + autre.getNom());
}
```

Implémentez cette méthode dans chaque sous-classe (`HomerSimpson`, `EricCartman`, `LisaSimpson`) avec un message spécifique à leur personnalité.

Testez ensuite ces interactions dans une boucle où chaque personnage interagit avec les autres.
