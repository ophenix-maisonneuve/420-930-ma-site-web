---
layout: default
title: "Classe, champs, méthodes"
parent: "Concepts de programmation orientée objet"
nav_order: 2
---

# Classe

En Java, une **classe** est un modèle qui définit les propriétés (champs) et les comportements (méthodes) d'un objet.

## Définitions

- **Classe** : structure qui regroupe des champs et des méthodes.
- **Champ (field)** : variable définie dans une classe.
- **Méthode (method)** : fonction définie dans une classe.

## Visibilité

- `private` : accessible uniquement dans la classe.
- `protected` : accessible dans la classe et ses sous-classes, ainsi que les classes dans le même package
- `public` : accessible depuis n'importe quelle classe.

## Mot-clé static
Le mot-clé static permet de définir des champs et des méthodes accessibles sans avoir créer une instance de la classe. Ces champs/méthodes appartiennent à la classe elle-même, et non à une instance en particulier
- **Champ (field)** : le champ appartient à la classe, et non à une instance en particulier
- **Méthode (method)** : la méthode appartient à la classe, et peut donc être appelée sans instance comme ceci: Classe.methode(...)

Si aucun modificateur de visibilité n'est utilisé, Java utilise la visibilité par défaut (*default*), qui permet uniquement l'accès par les autres classes du même package.

## Exemple

```java
public class Hero {
    // Champs (fields)
    
    // private: accessible uniquement dans cette classe
    private String nom;
    
    // protected: accessible par cette classe, ses sous-classes et les classes du même package
    protected int force;

    // public: accessible de partout
    // static: accessible sans instance de cette classe
    public static int compteur;

    // Constructeur (constructor)
    public Hero(String nom, int force) {
        // ici, this est obligatoire pour lever l'ambiguité
        this.nom = nom;
        this.force = force;
    }

    // Méthodes (method)
    public void combattre() {
        // ici, this est optionnel, car il n'y a pas d'ambiguité
        System.out.println(nom + " combat avec une force de " + this.force);
    }

    protected void seReposer() {
        System.out.println(this.nom + " se repose.");
    }

    private void penser() {
        System.out.println(this.nom + " médite en silence.");
    }
}
```

<details>
<summary>Équivalent Python</summary>

```python
class Hero:
    compteur = 0  # Champ public et statique

    def __init__(self, nom, force):
        self.__nom = nom          # Champ privé
        self._force = force       # Champ protégé

    def combattre(self):         # Méthode publique
        print(f"{self.__nom} combat avec une force de {self._force}")

    def _se_reposer(self):       # Méthode protégée
        print(f"{self.__nom} se repose.")

    def __penser(self):          # Méthode privée
        print(f"{self.__nom} médite en silence.")
```

</details>
