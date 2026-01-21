---
layout: default
title: Builder
parent: Patrons de création
nav_order: 2
published: true
---


## Description
Builder est un patron de création qui permet de construire des objets complexes étape par étape, tout en séparant clairement la construction de la représentation finale. Contrairement à d’autres patrons de création, Builder vise surtout à **éviter les constructeurs à rallonge** et à rendre le processus de création plus clair, flexible et lisible.

Le rôle du Builder est donc d'encapsuler la configuration d'un objet complexe en proposant une interface simple pour en assembler les parties.

{: .highlight}
La classe *Director* est parfois présentée dans les versions classiques du patron Builder (notamment dans le livre *Design Patterns* du GoF). Elle sert à orchestrer automatiquement les étapes de construction. **Elle n’est pas obligatoire** et n’est pas utilisée dans cette version moderne du patron, où le *client* contrôle lui-même les étapes.

## Quand l'utiliser ?
- Lorsque la création d’un objet nécessite **de nombreuses options** ou paramètres.
- Lorsque vous voulez éviter plusieurs constructeurs surchargés (*constructor telescoping*).
- Lorsque vous voulez rendre la construction d’objet **plus lisible** et progressive.
- Lorsque certaines étapes sont facultatives ou qu’un ordre spécifique n’est pas strictement requis.

## Avantages
- Le code client devient plus lisible et intuitif, surtout avec une interface *fluent*.
- Les objets complexes peuvent être construits sans exposer leur logique interne.
- Facilite l’ajout de nouveaux paramètres de construction sans casser l’existant.
- Évite les constructeurs surchargés et difficiles à maintenir.

## Inconvénients
- Nécessite une classe Builder supplémentaire.
- Peut être excessif pour des objets très simples.
- Le client doit appeler manuellement les étapes (ceci peut être mitigé par l'utilisation optionnelle d'un *Director*).

## Exemple

{: .highlight}
> Dans la version *classique* du patron Builder (telle que décrite par le *Gang of Four*), la méthode `getResult()` n’apparaît pas dans l’interface `Builder`. Elle est uniquement définie dans les *builders concrets*.  
>
> La raison est historique : en 1994, les langages ciblés (C++, Smalltalk…) ne permettaient pas d’exprimer facilement une méthode de retour typée dans une interface commune. Chaque builder pouvait produire un type de produit différent, ce qui empêchait de déclarer proprement `getResult()` au niveau abstrait.
>
> En Java (et dans plusieurs autres langages modernes, c’est différent : on peut (et souvent on devrait) placer `getResult()` dans l’interface `Builder`en utilisant des **génériques**.
>
> L'exemple ci-bas montre cette façon de faire, mais vous verrez aussi souvent des exemples où la méthode `getResult()` est uniquement dans l'implémentation de l'interface.


### Diagramme de classes
```mermaid
classDiagram
class Maison {
  -fenetres: int
  -portes: int
  -garage: boolean
  +getFenetres(): int
  +setFenetres(nb: int): void
  +getPortes(): int
  +setPortes(nb: int): void
  +hasGarage(): boolean
  +setGarage(garage: boolean): void
}

class Builder<T> {
  <<interface>>
  +reset(): void
  +setFenetres(nb: int): void
  +setPortes(nb: int): void
  +setGarage(garage: boolean): void
  +getResult(): T
}

class MaisonBuilder {
  -maison: Maison
  +getResult(): Maison
}

Builder <|.. MaisonBuilder
MaisonBuilder --> Maison : construit
```

### Code Java
```java
public class Maison {
    private int fenetres;
    private int portes;
    private boolean garage;

    public int getFenetres() {
        return this.fenetres;
    }

    public void setFenetres(int fenetres) {
        this.fenetres = fenetres;
    }

    public int getPortes() {
        return this.portes;
    }

    public void setPortes(int portes) {
        this.portes = portes;
    }

    public boolean hasGarage() {
        return this.garage;
    }

    public void setGarage(boolean garage) {
        this.garage = garage;
    }
}

public interface Builder<T> {
    void reset();
    void setFenetres(int nb);
    void setPortes(int nb);
    void setGarage(boolean garage);
    T getResult();
}

public class MaisonBuilder implements Builder<Maison> {
    private Maison maison;

    public MaisonBuilder() {
        this.maison = new Maison();
    }

    @Override
    public void reset() {
        this.maison = new Maison();
    }

    @Override
    public void setFenetres(int nb) {
        this.maison.setFenetres(nb);
    }

    @Override
    public void setPortes(int nb) {
        this.maison.setPortes(nb);
    }

    @Override
    public void setGarage(boolean garage) {
        this.maison.setGarage(garage);
    }

    @Override
    public Maison getResult() {
        return this.maison;
    }
}

public class Demo {
    public static void main(String[] args) {
        Builder<Maison> builder = new MaisonBuilder();

        builder.setFenetres(6);
        builder.setPortes(2);
        builder.setGarage(true);

        Maison maison = builder.getResult();
        builder.reset();

        System.out.println("Maison construite: " + maison.getFenetres() + " fenêtres");
    }
}
```

## Liens utiles
- [https://refactoring.guru/design-patterns/builder](https://refactoring.guru/design-patterns/builder)
- [https://en.wikipedia.org/wiki/Builder_pattern](https://en.wikipedia.org/wiki/Builder_pattern)
