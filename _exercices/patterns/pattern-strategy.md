---
layout: default
title: "Strategy"
parent: "Patrons de conception"
nav_order: 2
has_toc: false
published: false
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
ou
```bash
mvn clean compile exec:java
```
ou directement à partir de votre IDE.

Familiarisez-vous avec le menu, qui vous permet déjà d'ajouter des éléments dans la liste.

## Questions

