
# Classe abstraite : VehiculeAction

## Définition
Une **classe abstraite** peut contenir des méthodes implémentées et des méthodes abstraites. Elle sert de base pour d'autres classes.

## Exemple en Java
```java
public abstract class AbstractVehicule implements Vehicule {
    protected String marque;

    public VehiculeAction(String marque) {
        this.marque = marque;
    }

    public void arreter() {
        System.out.println(marque + " s'arrête.");
    }

    public abstract void demarrer();
}
```

```java
public class Voiture extends AbstractVehicule {
    private String marque;

    public Voiture(String marque) {
        this.marque = marque;
    }

    @Override
    public void demarrer() {
        System.out.println(marque + " démarre doucement.");
    }
}
```

```java
public class Camion extends AbstractVehicule {
    private String marque;

    public Camion(String marque) {
        this.marque = marque;
    }

    @Override
    public void demarrer() {
        System.out.println(marque + " démarre dans un nuage de fumée.");
    }
}
```

<details>
<summary>💡 Équivalent Python</summary>

```python
class VehiculeAction(Vehicule):
    def __init__(self, marque):
        self._marque = marque

    def arreter(self):
        print(f"{self._marque} s'arrête.")

    @abstractmethod
    def demarrer(self):
        pass
```

</details>
