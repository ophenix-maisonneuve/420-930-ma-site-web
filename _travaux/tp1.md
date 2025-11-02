---
layout: default
title: "Travail pratique 1"
nav_order: 1
published: false
---

# Travail pratique 1 : Gestion de chansons par durée avec deux structures de données

## Mise en situation
Vous avez obtenu le poste de DJ au Centre Bell pour les matchs des Canadiens de Montréal. Vous êtes responsable de la musique diffusée lors des pauses (publicités, arrêts de jeu, temps morts, etc.). Vous disposez d’une bibliothèque d’extraits musicaux de durées variées, mais vous n’avez aucun moyen rapide de retrouver une chanson correspondant à la durée exacte d’une pause. Vous décidez donc d’implémenter vous-même cette fonctionnalité pour vous aider dans votre travail.

## Objectifs pédagogiques
- Implémenter deux structures de données : une liste doublement chaînée et un arbre binaire de recherche (BST)
- Utiliser une interface commune pour abstraire les opérations
- Comparer les performances des deux structures
- Comprendre la complexité algorithmique (notation Grand O)
- Documenter les étapes de développement

## Structures à implémenter

### 1. Liste chaînée
- Ajout en fin de liste
- Recherche séquentielle
- Tri (vous devrez choisir le type de tri)

### 2. Arbre binaire de recherche (BST)
- Ajout selon les règles d'un arbre BST
- Recherche dans l'arbre
- Tri naturel via parcours in-order (et ordre inverse)

## Fonctionnalités à développer

### Interface commune : `Catalogue`
```java
void ajouter(Chanson chanson);
Chanson rechercher(int duree);
void supprimer(int duree);
void afficher(Ordre ordre);
```

### Implémentations :
- `CatalogueListeDoublementChainee` : basée sur une liste doublement chaînée
- `CatalogueBST` : basée sur un arbre binaire de recherche

## Analyse de complexité
Dans la section **Analyse de la complexité** du fichier `README.md`, vous devez :
- Pour chacune des deux structures (liste doublement chaînée et arbre de recherche binaire), comparer la complexité des algorithmes utilisés pour l'implémentation des méthodes suivantes:
 - `ajouter(chanson)` : Algorithmes d'ajout/insertion
 - `recherche(duree)` : Algorithmes de recherche
 - `afficher(ordre)` : Algorithmes de tri ou de parcours (dans le cas d'un arbre déjà trié)
- En fonction de l'analyse de la complexité ci-haut, justifier quelle structure devrait être privilégiée pour l'application de gestionnaire musical.

## Journal de développement
Dans la section **Journal de développement** du fichier `README.md`, vous devez décrire :
- Les étapes de votre travail
- Les décisions prises, en particulier par rapport aux choix d'algorithmes (ex.: tri dans la liste)
- Les difficultés rencontrées
- Les tests effectués

## Évaluation
| Critère | Points |
|--------|--------|
| Implémentation de la méthode `ajouter(chanson)` | 3 |
| Implémentation de la méthode `rechercher(duree)` | 3 |
| Implémentation de la méthode `afficher(ordre)` | 4 |
| Implémentation de la méthode `supprimer(duree)` | 4 |
| Analyse de la complexité et choix des algorithmes | 3 |
| Qualité du code et documentation | 3 |

## Code fourni

### `Chanson.java`
Classe complète représentant une chanson avec titre, artiste et durée.

### `Catalogue.java`
Interface définissant les opérations de base à implémenter.

### `Noeud.java`
Classes sreprésentant un nœud de la liste doublement chaînée et de l’arbre BST, respectivement.

### `CatalogueListeDoublementChainee.java`
Classe à compléter pour l’implémentation de la liste doublement chaînée.

### `CatalogueBST.java`
Classe à compléter pour l’implémentation du BST.

### `Main.java`
Classe principale qui vous fournit un menu simple permettant d'interagir avec l'application. Lorsque votre càde sera complété, tout devrait fonctionner à partir de cette classe.

---

À vous de jouer ! 🎧
