---
layout: default
title: "Tables associatives"
parent: "Structures de données"
nav_order: 3
published: false
---

# Tables associatives

Une **table associative** (aussi appelée **map** ou **dictionnaire**) est une structure de données qui associe des **clés uniques** à des **valeurs**. Elle permet des accès rapides aux données via une clé. Il existe plusieurs implémentations possibles : certaines utilisent des **arbres** pour maintenir un ordre, tandis que d'autres, appelées **tables de hachage**, s'appuient sur une **fonction de hachage** pour calculer la position des clés. 

## Caractéristiques principales
- **Clés uniques** : chaque clé est associée à une seule valeur.
- **Accès rapide** : en moyenne O(1) pour insertion, recherche et suppression.
- **Fonction de hachage** : détermine la position de la clé dans la table.

## Types d'opérations principales
- **Insertion (put)** : ajoute ou remplace une paire clé-valeur.
- **Recherche (get)** : récupère la valeur associée à une clé.
- **Suppression (remove)** : supprime une paire clé-valeur.
- **Redimensionnement (resize)** : augmente la capacité pour réduire les collisions.

![Illustration d'une table associative](https://upload.wikimedia.org/wikipedia/commons/7/7d/Hash_table_3_1_1_0_1_0_0_SP.svg)


## Types de tables associatives

L'association entre une clé et une valeur peut être réalisée de plusieurs façons :

- **Table de hachage (*Hash Table*)** :
  - Utilise une fonction de hachage pour calculer un index à partir de la clé.
  - Avantages : accès en temps moyen O(1).
  - Inconvénients : collisions possibles, nécessite une bonne fonction de hachage.

- **Arbres (*Tree-based Maps*)** :
  - Utilise des structures d'arbres (par exemple, arbres binaires de recherche, arbres équilibrés comme AVL ou Rouge-Noir).
  - Avantages : maintien des clés triées, complexité O(log n).
  - Inconvénients : plus complexe à implémenter.

- **Listes chaînées ou tableaux (Structures linéaires)** :
  - Stocke les paires clé-valeur dans une liste ou un tableau.
  - Avantages : simple à implémenter.
  - Inconvénients : recherche en O(n), peu efficace pour de grandes tailles.

- **Structures hybrides** :
  - Combinaison de hachage et d'arbres pour optimiser les performances (ex. : HashMap avec arbres pour gérer les collisions).

Chaque méthode présente des compromis entre vitesse, mémoire et complexité d'implémentation.

---

## Tableau comparatif
| Structure            | Accès direct | Insertion rapide | Gestion des doublons |
|----------------------|--------------|------------------|-----------------------|
| Tableau             | Oui          | Non              | Non                   |
| Liste chaînée       | Non          | Oui              | Oui                   |
| Table associative   | Oui (par clé)| Oui              | Non                   |

---

## Opérations et complexité
| Opération   | Complexité moyenne | Complexité pire cas |
|-------------|---------------------|----------------------|
| Insertion (*put*)         | O(1)               | O(n) (si redimensionnement nécessaire)               |
| Recherche (*get* et *containsKey*)         | O(1)               | O(n)                |
| Suppression (*remove*)     | O(1)               | O(n)                |

---

## Cas d'utilisation
- Indexation en base de données
- Caches mémoire
- Dictionnaires