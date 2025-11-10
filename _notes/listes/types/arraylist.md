---
layout: default
parent: "Types"
title: "ArrayList"
nav_order: 2
published: false
---

# ArrayList

Une ArrayList est une liste dynamique qui permet d'ajouter ou de supprimer des éléments facilement. Elle utilise un tableau sous-jacent et redimensionne automatiquement sa capacité.

```java
import java.util.ArrayList;

public class ExempleArrayList {
    public static void main(String[] args) {
        ArrayList<Integer> liste = new ArrayList<>();
        liste.add(10);
        liste.add(20);
        liste.add(30);
        for (int val : liste) {
            System.out.println(val);
        }
    }
}
```
