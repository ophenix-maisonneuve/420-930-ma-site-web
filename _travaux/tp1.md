---
layout: default
title: "Travail pratique 1"
nav_order: 1
published: true
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


## Fonctionnalités à développer

### Interface commune (fournie): `Catalogue`

```java
void ajouter(Chanson chanson);
Chanson rechercher(int duree);
void afficher(Ordre ordre);
void supprimer(int duree);
```

### Liste doublement chaînée `CatalogueListeDoublementChainee`

- `ajouter(chanson)` : Ajoute une chanson en fin de liste
- `rechercher(duree)` : Retourne la première chanson correspondant à la durée de façon séquentielle.
- `afficher(duree)` : Trie (vous devrez choisir le type de tri) et affiche dans l'ordre demandé.
- `supprimer(duree)` : Supprime **la première** chanson trouvée qui correspond à la durée.

### Arbre binaire de recherche (BST) `CatalogueBST`

- `ajouter(chanson)` : Ajoute une chanson selon les règles d'un arbre BST.
- `rechercher(duree)` : Retourne la première chanson correspondant à la durée demandée.
- `afficher(duree)` : Tri naturel via parcours in-order (et ordre inverse) et affiche dans l'ordre demandé.
- `supprimer(duree)` : Supprimer **la première** chanson trouvée qui correspond à la durée.

## Analyse de complexité

Dans la section **Analyse de la complexité** du fichier `README.md` (ou, si vous préférez, dans un fichier Word ou PDF), vous devez :

- Pour chacune des deux structures (liste doublement chaînée et arbre de recherche binaire), comparer la complexité des algorithmes utilisés pour l'implémentation des méthodes suivantes:
  - `ajouter(chanson)` : Algorithmes d'ajout/insertion
  - `recherche(duree)` : Algorithmes de recherche
  - `afficher(ordre)` : Algorithmes de tri ou de parcours (dans le cas d'un arbre déjà trié)
  - `supprimer(duree)` : Algorithmes de suppression
- En fonction de l'analyse de la complexité ci-haut, justifier quelle structure devrait être privilégiée pour l'application de gestionnaire musical.

## Journal de développement

Dans la section **Journal de développement** du fichier `README.md` (ou, si vous préférez, dans un fichier Word ou PDF), vous devez décrire :

- Les étapes de votre travail
- Les décisions prises, en particulier par rapport aux choix d'algorithmes (ex.: tri dans la liste)
- Les difficultés rencontrées
- Les tests effectués

---

## Code fourni

Le code de base est disponible dans le dépôt Git suivant: [tp1-gestionnaire-musical](https://github.com/ophenix-420-930-ma-24636/tp1-gestionnaire-musical)

### `Chanson.java`

Classe complète représentant une chanson avec titre, artiste et durée.

### `Catalogue.java`

Interface définissant les opérations de base à implémenter.

### `Noeud.java`

Classes représentant un nœud de la liste doublement chaînée et de l’arbre BST, respectivement.

### `CatalogueListeDoublementChainee.java`

Classe à compléter pour l’implémentation de la liste doublement chaînée.

### `CatalogueBST.java`

Classe à compléter pour l’implémentation du BST.

### `Main.java`

Classe principale qui vous fournit un menu simple permettant d'interagir avec l'application. Lorsque votre càde sera complété, tout devrait fonctionner à partir de cette classe.

---

## Évaluation


| Critère                                                                       | Points |
| ------------------------------------------------------------------------------|--------|
| Implémentation et bon fonctionnement de la méthode`ajouter(chanson)`          | 3      |
| Implémentation et bon fonctionnement de la méthode`rechercher(duree)`         | 3      |
| Implémentation et bon fonctionnement de la méthode`afficher(ordre)`           | 4      |
| Implémentation et bon fonctionnement de la méthode`supprimer(duree)`          | 4      |
| Analyse de la complexité et choix des algorithmes                             | 3      |
| Journal de réflexion (documentation des étapes, décisions, tests effectués)   | 3      |
| **Total**                                                                     | **20** |

---

## À remettre

- Un fichier **.zip** de votre projet, comprenant:
  - Tout le projet Java (code, fichier pom.xml, etc).
  - L'analyse de la complexité (dans le fichier `README.md` ou un document Word ou PDF dans le sous-répertoire `docs`)
  - Le journal de développement (dans le fichier `README.md` ou un document Word ou PDF dans le sous-répertoire `docs`)
- Le travail est à remettre sur Léa (Omnivox) dans la section "Travaux - Énoncés et remises"
- Le travail peut être fait en équipes de **deux** ou **trois** personnes (une seule remise pour l'équipe)
- Le projet doit pouvoir être exécuté de la façon suivante:

```bash
mvn clean package
java -jar <nom du fichier>.jar
```

À vous de jouer ! 🎧
