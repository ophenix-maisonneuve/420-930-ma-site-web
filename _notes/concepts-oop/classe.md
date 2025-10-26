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
public class Vehicule {
    // Champs (fields)
    
    // private: accessible uniquement dans cette classe
    private String marque;
    
    // protected: accessible par cette classe, ses sous-classes et les classes du même package
    protected int vitesseMaximale;

    // public: accessible de partout
    // static: accessible sans instance de cette classe
    public static int compteur = 0;

    // Constructeur (constructor)
    public Hero(String marque, int vitesseMaximale) {
        // ici, this est obligatoire pour lever l'ambiguité
        this.marque = marque;
        this.vitesseMaximale = vitesseMaximale;
        compteur++;
    }

    // Méthodes (method)
    public void demarrer() {
        // ici, this est optionnel, car il n'y a pas d'ambiguité
        System.out.println(this.marque + " démarre.");
    }

    protected void accelerer() {
        System.out.println(this.marque + " accélère.");
    }

    private void verifierSysteme() {
        System.out.println("Vérification du système interne de " + this.nom);
    }
}
```

<details>

<summary>Équivalent Python</summary>


```python
class Vehicule:
    compteur = 0  # Champ public statique

    def __init__(self, marque, vitesse_maximale):
        self.__marque = marque         # Champ privé
        self._vitesse_maximale = vitesse_maximale  # Champ protégé
        Vehicule.compteur += 1

    def demarrer(self):
        print(f"{self.__marque} démarre.")

    def _accelerer(self):
        print(f"{self.__marque} accélère.")

    def __verifier_systeme(self):
        print("Vérification du système interne.")
```

</details>
