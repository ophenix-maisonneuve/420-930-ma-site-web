---
layout: default
title: "Strategy"
parent: "Patrons de conception"
nav_order: 2
has_toc: false
published: true
---

# Exercice : J'ai mon Voyage (partie 2) - Strategy

Tellement satisfaite de votre travail pour améliorer la qualité du code de son application de gestion, l'agence de voyages ***J'ai mon Voyage*** fait de nouveau appel à vos services. Cette fois, elle aimerait ajouter la possibilité de produire le libellé de ses billets dans plusieurs langues différentes.

## Objectifs

- Comprendre le fonctionnement du patron de conception *Strategy*
- Reconnaître les cas d'utilisation propices pour le patron *Strategy*

## Contexte

À partir du code développé dans le cours pour l'application de gestion de l'agence de voyages, utiliser le patron de conception *Strategy* pour permettre la création du libellé du billet en français, en anglais, et éventuellement en plusieurs autres langues. Le changement de langue se fait via l'interface en ligne de commande interactive.

## Étapes préparatoires

### 1. Clonez le dépôt de l'exercice

```bash
git clone git@github.com:ophenix-420-930-ma-24636/patrons-agence-voyages.git
```
ou
```bash
git clone https://github.com/ophenix-420-930-ma-24636/patrons-agence-voyages.git
```

### 2. Lancez le projet Java
```bash
mvn clean package
java -jar target/patrons-agence-voyages-1.0-SNAPSHOT.jar
```
ou directement à partir de votre IDE.

Familiarisez-vous avec le menu, qui vous permet déjà d'ajouter des itinéraires.

## Questions

### 1. Créez l'interface de votre *Strategy*
- Pour quelle fonctionnalité tente-t-on d'ajouter des comportements différents ? 
- Quelle classe existante effectue présentement cette fonctionnalité ?
   - *Cette classe pourrait devenir l'une des implémentations de votre **Strategy*** ?
- Créez une interface nommée `BilletStrategy` qui définit le contrat de votre *Strategy*
- Faites en sorte que la classe existante implémente maintenant votre nouvelle interface `BilletStrategy` (vous pouvez la renommer au besoin pour que son nom soit cohérent).
- Créez une nouvelle implémentation de `BilletStrategy` qui crée le libellé en anglais dans le format suivant :
   - *[<code du type de vol>] Ticket from <ville d'origine> to <ville de destination> [<code du type de vol>]*

### 2. Étudiez la méthode `main()` de la classe `Launcher`
- Cette classe respecte-t-elle les principes SOLID ? Pourquoi ?
   - *La bonne réponse est : votre enseignant était un peu paresseux pour cette classe "jetable"... :)*
   - S'il y a des infractions SOLID, où sont-elles ?
- À quel endroit la langue est-elle sélectionnée ?
- Pourriez-vous vous servir de cet endroit pour changer dynamiquement la langue en vous servant de votre *Strategy* ?
   - Si oui, implémentez ce changement
   - Sinon, pourquoi ?

### 3. Planifiez les prochaines évolutions
- Lorsque l'agence de voyages voudra ajouter une langue supplémentaire (par exemple l'espagnol), quelles seront les étapes à réaliser ?
- Hormis la classe `Launcher`, est-ce que le code existant aura à être modifié ? 
- Quel(s) principe(s) SOLID le patron *Strategy* favorise-t-il ?
