---
layout: default
title: "State et Command"
parent: "Patrons de conception"
nav_order: 5
has_toc: false
published: false
---

# Exercice : Machine distributrice : Patrons *State* et *Command*

Cette fois, c'est assez : la machine distributrice du campus vous a encore volé 2$! Vous décidez d'écrire à la compagnie qui fabrique cette machine distributrice afin de leur enseigner comment ils auraient dû la programmer afin qu'elle cesse de voler l'argent des étudiants (à moins que ce soit fait exprès... c'est un complot!)

Après avoir analysé la machine, vous constatez les éléments suivants :

- 4 boutons
   - Insérer : ajoute des crédits à partir d'une carte de crédit ou d'une carte de points par incréments de 1$ (100 crédits)
   - Choisir : sélectionne un produit en passant son code de produit
   - Distribuer : officialise l'achat, distribue le produit, décrémente les stocks de la machine, débite le solde de l'utilisateur et retourne les crédits en trop à l'utilisateur
   - Annuler : annule la sélection et retourne les crédits à l'utilisateur
- Un petit écran LCD où le dernier message généré par la machine est affiché à l'utilisateur (messages de statut ou d'erreurs, par exemple).

Les conditions suivantes doivent être respectées :
- La distribution doit être permise seulement si le solde est suffisant ET si le produit est en stock.
- Si une distribution est demandée alors que le solde est insuffisant OU que le produit n'est pas en stock, un message d'erreur doit s'afficher et la distribution doit être bloquée.
- L'annulation est permise à tout moment avant la distribution.
---

## Objectifs

- Comprendre et appliquer les patrons ***State*** et ***Command*** dans un contexte réaliste.  
- Reconnaître où placer la variabilité : dans les états (*State*) ou dans les actions (*Command*).  
- Comparer les avantages/inconvénients de chaque approche sur un même problème.

---

## Contexte

Vous partez d’un squelette de code Java (voir ci-dessous). 
- **Option A — State** : encapsulez les **états** de la machine (EnAttentePaiement, PaiementValidé, etc.), et gérez les conditions selon l'état actuel.
- **Option B — Command** : encapsulez les **actions** des boutons (ChoisirProduit, Distribuer, Annuler, etc.), et réassignez les commandes pour respecter les conditions. 

---

## Étapes préparatoires

### 1. Clonez le dépôt de l'exercice

```bash
git clone git@github.com:ophenix-420-930-ma-24636/patrons-machine-distributrice.git
```
ou
```bash
git clone https://github.com/ophenix-420-930-ma-24636/patrons-machine-distributrice.git
```

---

## Option A — Implémentation *State*

Le comportement de la machine varie selon son état interne.

### A1. Analysez le code fourni
- Selon le patron `State`, quelle classe représente le **Contexte** ?
- En observant l'interface `State`, quelles sont les transitions possibles entre les états ?

### A2. Implémentez les états concrets
Créez une implémentation d'état par état possible :
- `Pret` : Lorsque la machine est prête à accepter un nouveau choix
- `ProduitChoisi` : Lorsqu'un choix a été fait par l'utilisateur
- `Distribution` : Lorsque le produit est en cours de distribution

Chaque état :  
- appelle l'API publique de `MachineDistributrice` (`insertion`, `choixProduit`, etc.)
- appelle les services utilitaires si nécessaire (`debiterSoldePour`, `debiterStock`, `rendreMonnaie`),  
- peut mettre à jour le message (`setDernierMessage`),  
- change d’état quand cela a du sens (ex. vers `Distribution` puis retour vers `EnAttentePaiement`).

De plus, l'état `ChoixProduit` doit s'assurer que les conditions sont remplies avant de permettre une distribution.

### A3. Reliez la classe de départ à vos états
Ajoutez dans la classe `MachineDistributrice` :
- un champ `private State etatCourant;`
- un constructeur qui assigne l’état initial (`Pret`)
- des méthodes de transition (ex. `setEtat(State nouvelEtat)`).
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

---

## Option B — Implémentation *Command*

Le comportement des boutons est encapsulé dans des **Commandes** réassignables.

### B1. Analysez le code fourni
- Selon le patron `Command`, quelle classe représente le ***Invoker*** (ou ***Sender***) ?
- Quelle classe assigne les actions à l'***Invoker*** ?
   - Sur quels critères les actions sont elles (ré-)assignées ?
- Selon le patron `Command`, quelle classe représente le ***Receiver*** ?


### B2. Implémentations de commandes
Créez les implémentations de commandes manquantes (`CommandeMessage` a déjà été implémentée):
- `CommandeChoisirProduit(String code)`
- `CommandeDistribuer()`
- `CommandeAnnuler()`
- `CommandeInsertion()`

*N'oubliez pas que, selon le patron **Command**, la commande doit être construite avec le **Receiver** en paramètre de façon à garder sa référence*

Chaque commande :  
- appelle l'API publique de `MachineDistributrice` (`insertion`, `choixProduit`, etc.)
- appelle les services utilitaires si nécessaire (`debiterSoldePour`, `debiterStock`, `rendreMonnaie`),  
- peut mettre à jour le message (`setDernierMessage`),  

### B3. Reliez la classe de départ à vos commandes
Dans `PanneauControle.configurerCommandes`, assignez les bonnes implémentations de commandes aux boutons en validant les conditions lorsque nécessaire. Par exemple, le bouton **Distribuer** ne devra débloquer la commande `CommandeDistribuer` que si l'item choisi est en stock ET que le solde est suffisant. Sinon, il devra utiliser une `CommandeMessage` pour afficher un message d'erreur à l'utilisateur.

```java
    this.boutonDistribuer.setAction(() -> {
        // TODO ici, on doit s'assurer que les conditions sont respectées avant de permettre au bouton "Distribuer" de lancer l'action effectuant la distribution
        configurerCommandes(machine);
    });
```

---

## Questions de réflexion

1. Où réside la variabilité dans chacune des solutions ?  
2. Quel patron vous semble le plus simple à faire évoluer (nouveau mode vs nouvelle action) ?  
3. Comment respecter au mieux ***OCP*** et ***SRP*** dans votre version ?  
4. Quelles faiblesses potentielles voyez‑vous dans chacune des approches ?

---


