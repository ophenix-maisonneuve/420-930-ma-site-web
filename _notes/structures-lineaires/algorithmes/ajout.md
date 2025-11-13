---
layout: default
parent: "Algorithmes"
title: "Ajout"
nav_order: 1
published: true
---

# Ajout dans les listes

L'ajout est une opération fondamentale dans les structures de données linéaires. Elle permet d'insérer un nouvel élément à une position donnée : au début, au milieu ou à la fin. Le comportement et la complexité de cette opération varient selon le type de liste utilisé.




## Complexité

| Structure              | Ajout en tête | Ajout en fin | Ajout à une position |
|------------------------|---------------|--------------|-----------------------|
| Tableau                | O(n)          | O(1) ou O(n) si tableau plein| O(n)                  |
| Liste chaînée simple   | O(1)          | O(n) ou O(1) si *tail*       | O(n)                  |
| Liste chaînée double   | O(1)          | O(n) ou O(1) si *tail*         | O(n)                  |

{: .highlight}

>Dans un tableau, l’ajout en fin est généralement O(1) si la capacité est suffisante. Toutefois, si le tableau est plein, il faut créer un nouveau tableau plus grand et copier les éléments, ce qui entraîne une complexité O(n).
>Dans une liste chaînée (simple ou double), l’ajout en fin est O(n) par défaut, car il faut parcourir la liste pour atteindre le dernier nœud. Cependant, si une référence vers le dernier nœud (tail) est maintenue, l’ajout en fin peut être effectué en O(1).