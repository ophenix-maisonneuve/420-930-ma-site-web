---
layout: default
title: "Adapter"
parent: "Patrons de conception"
nav_order: 2
has_toc: false
published: false
---

# Exercice : J'ai mon Voyage (partie 3) - Adapter

Décidément, vous avez vraiment fait sensation auprès de l'agence de voyages  ***J'ai mon Voyage***! L'agence fait à nouveau appel à vos services pour modifier son application de gestion. Cette fois, elle vous demande d'y intégrer **CashBox3000**, une librairie tierce qui facilite supposément la gestion de la petite caisse.

## Objectifs

- Comprendre le fonctionnement du patron de conception *Adapter*
- Reconnaître les cas d'utilisation propices pour le patron *Adapter*

## Contexte

À partir du code développé dans le cours pour l'application de gestion de l'agence de voyages, utiliser le patron de conception *Adapter* pour permettre l'intégration de la librairie tierce **CashBox3000**. Le but sera d'intégrer cette librairie en minimisant les changements de code dans la classe appelante (la classe `GestionnaireAgenceVoyages`). Idéalement, on voudrait que cette classe continue à faire les mêmes appels de méthodes, mais utilise de façon sous-jacente la nouvelle librairie...

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
ou
```bash
mvn clean compile exec:java
```
ou directement à partir de votre IDE.

Familiarisez-vous avec le menu, qui vous permet déjà d'ajouter des itinéraires.

## Questions

### 1. Analysez la classe CashBox3000
- Quelles sont les principales différences entre cette classe et la gestion de petite caisse utilisée présentement (`ServicePetiteCaisse`) ?
- Si vous désirez minimiser les changements dans `GestionnaireAgenceVoyages`, que sera votre cible (*target*) et que sera votre classe adaptée (*adaptee*) dans le contexte d'un *adapter* ?


### 2. Choisissez la variante du patron *adapter*
- Adaptation par héritage (*class adapter*) ?
   - Quelles étapes devriez-vous réaliser pour utiliser l'adaptation par héritage (*class adapter*) ?
   - Quels seraient les avantages et inconvénients d'utiliser cette variante ?
- Adaptation par implémentation (*class adapter*) ?
   - Quelles étapes devriez-vous réaliser pour utiliser l'adaptation par héritage (*class adapter*) ?
   - Quels seraient les avantages et inconvénients d'utiliser cette variante ?
