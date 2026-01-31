---
layout: default
title: "State et Command"
parent: "Patrons de conception"
nav_order: 5
has_toc: false
published: false
---

# Exercice : Machine distributrice : Patrons *State* et *Command*

Cette fois, c'est assez : la machine distributrice du campus vous a encore volé 2$! Vous décidez d'écrire à la compagnie qui fabrique cette machine distributrice afin de leur enseigner comment ils auraient dû programmer leur machine afin qu'elle cesse de voler l'argent des étudiants (à moins que ce soit fait exprès... c'est un complot!)

Après avoir analysé la machine, vous constatez le fonctionnement suivant: 

Selon l'état de la machine (paiement, choix, distribution, panne), les boutons ne produisent pas les mêmes actions 
Votre mandat : **la moitié du groupe** implémente la solution avec **State**, **l’autre moitié** avec **Command**. Les deux versions doivent passer **les mêmes scénarios d’acceptation**.

---

## Objectifs

- Comprendre et appliquer les patrons **State** *et* **Command** dans un contexte réaliste.  
- Reconnaître **où placer la variabilité** : *dans les états* (State) vs *dans les actions* (Command).  
- Comparer les avantages/inconvénients de chaque approche sur un même problème.

---

## Contexte

Vous partez d’une classe Java (ci‑dessous) : elle ne vous force ni particulièrement vers *State* ni particulièrement vers *Command*.  
- **Option A — State** : encapsulez les **modes** de la machine (EnAttentePaiement, PaiementValidé, etc.).  
- **Option B — Command** : encapsulez les **actions** des boutons (ChoisirProduit, Distribuer, Annuler…), et réassignez dynamiquement ces commandes selon le contexte.

---

## Étapes préparatoires

### 1. Créez votre projet Java
- Projet Maven/Gradle ou projet simple dans votre IDE favori.  
- Version Java : 25 (ou celle utilisée en cours).

### 2. Copiez la classe de départ (ci‑dessous)
- Placez‑la dans votre projet (`src/main/java/...`).  
- Vous pouvez créer une sous‑classe selon vos besoins (voir Options A/B).

### 3. Configurez un mini catalogue (pour tester)
- Définissez au moins un produit, son prix et un stock positif.  
- Testez les boutons : insertion, choix, annulation, demande de distribution.

---

## Scénarios d’acceptation (exemples)
1. Insertion 100 → Choix “Café” (prix 150) → Message: “Crédit insuffisant”.  
2. Insertion 100 → Insertion 50 → Choix “Café” → Distribuer → *stock décrémenté* et *solde débité*.  
3. Insertion 200 → Annuler → *rendu 200*, retour à l’état initial.  
4. Produit en rupture → message d’erreur adapté, sans débiter.

## Option A — Implémentation *State*

**Intention** : le **comportement** de la machine varie selon son **état interne**.

### A1. Créez l’interface d’état
Définissez une interface `EtatMachine` contenant les mêmes événements que les *hooks* :
```java
public interface EtatMachine {
    void onChoixProduit(MachineDistributrice m, String codeProduit);
    void onAnnulation(MachineDistributrice m);
    void onDemandeDistribution(MachineDistributrice m);
}
```

### A2. Implémentez les états concrets
- `EnAttentePaiement`
- `PaiementValide`
- `ChoixProduit`
- `Distribution`
- `HorsService` (optionnel mais utile)

Chaque état :
- vérifie les préconditions (`prixAtteint`, `produitDisponible`),  
- appelle les services utilitaires si nécessaire (`debiterSoldePour`, `debiterStock`, `rendreMonnaie`),  
- peut mettre à jour le message (`setDernierMessage`),  
- change d’état quand cela a du sens (ex. vers `Distribution` puis retour vers `EnAttentePaiement`).

### A3. Reliez la classe de départ à vos états
Créez une **sous‑classe** de `MachineDistributrice` (ex. `MachineDistributriceState`) contenant :
- un champ `private EtatMachine etatCourant;`
- un constructeur qui assigne l’état initial (`EnAttentePaiement`)
- des redirections des hooks, par exemple :
```java
@Override
protected void onChoixProduit(String code) {
    this.etatCourant.onChoixProduit(this, code);
}
@Override
protected void onAnnulation() {
    this.etatCourant.onAnnulation(this);
}
@Override
protected void onDemandeDistribution() {
    this.etatCourant.onDemandeDistribution(this);
}
```
- des **méthodes de transition** (ex. `setEtat(EtatMachine nouvelEtat)`).

---

## Option B — Implémentation *Command*

**Intention** : les **actions** des boutons sont encapsulées dans des **Commandes** réassignables.

### B1. Créez l’interface Commande
```java
public interface Commande {
    void executer(MachineDistributrice m);
}
```
Éventuellement des sous‑types paramétrés :
- `CommandeChoisirProduit(String code)`
- `CommandeDistribuer()`
- `CommandeAnnuler()`
- `CommandeInsertion(int montant)`

### B2. Implémentations de commandes
- **Commandes “réelles”** : débitent solde/stock, distribuent, rendent monnaie, etc.  
- **Commandes “neutres”** : affichent un message si l’action n’est pas autorisée (“Insérez d’abord de l’argent”, “Choix invalide”, etc.).

### B3. Reliez la classe de départ à vos commandes
Créez une sous‑classe `MachineDistributriceCommand` qui :
- déclare des **emplacements** pour les commandes actives (par ex. `commandeChoix`, `commandeDistribuer`, `commandeAnnuler`),  
- redirige les hooks vers les commandes, par exemple :
```java
@Override
protected void onChoixProduit(String code) {
    if (this.commandeChoix != null) {
        // si vous optez pour une commande paramétrable
        // this.commandeChoix.setCode(code);
        this.commandeChoix.executer(this);
    }
}
@Override
protected void onAnnulation() {
    if (this.commandeAnnuler != null) {
        this.commandeAnnuler.executer(this);
    }
}
@Override
protected void onDemandeDistribution() {
    if (this.commandeDistribuer != null) {
        this.commandeDistribuer.executer(this);
    }
}
```
- réassigne dynamiquement les commandes en fonction du contexte (solde, choix courant, disponibilité du produit, mode maintenance, etc.).  
  Exemple : tant que le prix n’est pas atteint, `commandeDistribuer` pointe vers une **CommandeMessage** (“Crédit insuffisant”). Une fois le prix atteint, elle pointe vers **CommandeDistribuer**.

---

## Critères de réussite (pour les deux options)

- Les scénarios d’acceptation s'exécutent correctement (distribution, annulation, ruptures, crédits).  
- Aucune cascade de `if/switch` géante : la variabilité est portée par les **états** ou par les **commandes**.  
- Code clair, cohérent avec le patron choisi, et respectant les principes SOLID.  

---

## Questions de réflexion

1. Où réside **la variabilité** dans votre solution ?  
   - *State* : dans les **modes**.  
   - *Command* : dans les **actions** configurées par les boutons.  
2. Quel patron vous semble **le plus simple à faire évoluer** (nouveau mode vs nouvelle action) ?  
3. Comment respecter au mieux **OCP** et **SRP** dans votre version ?  
4. Quelles **faiblesses** potentielles voyez‑vous dans l’autre approche ?

---

## Classe Java de départ

```java
import java.util.HashMap;
import java.util.Map;

public class MachineDistributrice {

    // Données "métier" minimales et neutres
    private int soldeCents;
    private String dernierMessage;
    private Map<String, Integer> stock;     // codeProduit -> quantité
    private Map<String, Integer> prixCents; // codeProduit -> prix en cents

    public MachineDistributrice() {
        this.soldeCents = 0;
        this.dernierMessage = "";
        this.stock = new HashMap<String, Integer>();
        this.prixCents = new HashMap<String, Integer>();
    }

    // --- API "neutre" : événements/boutons ---
    public void appuyerBoutonInsertion(int montantCents) {
        if (montantCents > 0) {
            this.soldeCents = this.soldeCents + montantCents;
            this.setDernierMessage("Crédit: " + this.soldeCents + " cents");
        } else {
            this.setDernierMessage("Montant invalide");
        }
        // STATE: l'état pourra décider d'une transition ici.
        // COMMAND: ce bouton pourrait déléguer à une Commande d'insertion.
    }

    public void appuyerBoutonChoix(String codeProduit) {
        this.setDernierMessage("Choix demandé: " + codeProduit);
        this.onChoixProduit(codeProduit);
    }

    public void appuyerBoutonAnnuler() {
        if (this.soldeCents > 0) {
            int rendu = this.soldeCents;
            this.soldeCents = 0;
            this.setDernierMessage("Annulé. Rendu: " + rendu + " cents");
        } else {
            this.setDernierMessage("Rien à annuler");
        }
        this.onAnnulation();
    }

    public void appuyerBoutonDistribuer() {
        this.setDernierMessage("Demande de distribution");
        this.onDemandeDistribution();
    }

    // --- Hooks "neutres" à rediriger dans vos solutions ---
    protected void onChoixProduit(String codeProduit) {
        // Intention: point d'extension pour State/Command.
    }

    protected void onAnnulation() {
        // Intention: point d'extension pour State/Command.
    }

    protected void onDemandeDistribution() {
        // Intention: point d'extension pour State/Command.
    }

    // --- Services utilitaires communs (réutilisables par vos patrons) ---
    public boolean produitDisponible(String codeProduit) {
        Integer qte = this.stock.get(codeProduit);
        if (qte == null) {
            return false;
        }
        return qte > 0;
    }

    public boolean prixAtteint(String codeProduit) {
        Integer prix = this.prixCents.get(codeProduit);
        if (prix == null) {
            return false;
        }
        return this.soldeCents >= prix;
    }

    public boolean debiterStock(String codeProduit) {
        Integer qte = this.stock.get(codeProduit);
        if (qte == null) {
            return false;
        }
        if (qte <= 0) {
            return false;
        }
        this.stock.put(codeProduit, qte - 1);
        return true;
    }

    public boolean debiterSoldePour(String codeProduit) {
        Integer prix = this.prixCents.get(codeProduit);
        if (prix == null) {
            return false;
        }
        if (this.soldeCents < prix) {
            return false;
        }
        this.soldeCents = this.soldeCents - prix;
        return true;
    }

    public void rendreMonnaie() {
        if (this.soldeCents > 0) {
            int rendu = this.soldeCents;
            this.soldeCents = 0;
            this.setDernierMessage("Monnaie rendue: " + rendu + " cents");
        } else {
            this.setDernierMessage("Aucune monnaie à rendre");
        }
    }

    // --- Gestion du catalogue (pour config de tests) ---
    public void definirPrix(String codeProduit, int prixEnCents) {
        if (codeProduit != null && prixEnCents >= 0) {
            this.prixCents.put(codeProduit, prixEnCents);
        }
    }

    public void definirStock(String codeProduit, int quantite) {
        if (codeProduit != null && quantite >= 0) {
            this.stock.put(codeProduit, quantite);
        }
    }

    // --- Afficheur & accès aux données ---
    public String getDernierMessage() {
        return this.dernierMessage;
    }

    public void setDernierMessage(String message) {
        if (message != null) {
            this.dernierMessage = message;
        }
    }

    public int getSoldeCents() {
        return this.soldeCents;
    }

    public Map<String, Integer> getStockSnapshot() {
        return new HashMap<String, Integer>(this.stock);
    }

    public Map<String, Integer> getPrixSnapshot() {
        return new HashMap<String, Integer>(this.prixCents);
    }
}
```

----

## Pistes d'amélioration (facultatif)

- **Command** : ajoutez un **historique** et implémentez “Annuler” (si pertinent).  
- **State** : ajoutez un **mode Maintenance** ou **HorsService** propre.  
- **Observer** : branchez une **tour de contrôle** (capteur externe) qui notifie la machine, pour déclencher un changement de mode ou de mapping de commandes.

---

