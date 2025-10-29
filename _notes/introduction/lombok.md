---
layout: default
title: "Librairie Lombok"
parent: "Introduction à Java et ses outils"
nav_order: 8
published: false
---

# 📚 Introduction à Lombok pour Java

## Qu'est-ce que Lombok ?

[Lombok](https://projectlombok.org/) est une bibliothèque Java qui permet de **réduire le code boilerplate** (code répétitif et souvent inutilement verbeux) en utilisant des **annotations**. Elle s'intègre facilement dans les projets Java via Maven ou Gradle et fonctionne avec la plupart des IDE modernes comme IntelliJ IDEA et Eclipse.

---

## 🚀 Pourquoi utiliser Lombok ?

En Java "vanilla" (sans Lombok), il est courant d'écrire manuellement des méthodes comme :

- `getters` et `setters`
- `constructeurs`
- `toString()`
- `equals()` et `hashCode()`

Cela peut rendre le code long, difficile à lire et à maintenir. Lombok automatise ces tâches grâce à des annotations simples.

---

## ✅ Annotations les plus utiles

### `@Getter` / `@Setter`
Génère automatiquement les accesseurs et mutateurs.
```java
@Getter @Setter
public class Student {
    private String name;
    private int age;
}
```

### `@Data`
Combine `@Getter`, `@Setter`, `@ToString`, `@EqualsAndHashCode`, etc.
```java
@Data
public class Book {
    private String title;
    private String author;
}
```

### `@NoArgsConstructor` / `@AllArgsConstructor`
Génère des constructeurs sans et avec tous les arguments.
```java
@NoArgsConstructor
@AllArgsConstructor
public class Course {
    private String name;
    private int credits;
}
```

### `@RequiredArgsConstructor`
Génère un constructeur avec les champs `final` ou annotés `@NonNull`.
```java
@RequiredArgsConstructor
public class User {
    private final String username;
    @NonNull private String email;
}
```

### `@ToString`
Génère une méthode `toString()`.
```java
@ToString
public class Point {
    private int x;
    private int y;
}
```

### `@EqualsAndHashCode`
Génère les méthodes `equals()` et `hashCode()`.
```java
@EqualsAndHashCode
public class Employee {
    private int id;
    private String name;
}
```

### `@Builder`
Implémente le pattern Builder.
```java
@Builder
public class Car {
    private String brand;
    private int year;
}
```

### `@SneakyThrows`
Permet de lancer des exceptions sans les déclarer.
```java
@SneakyThrows
public void readFile(String path) {
    Files.readAllLines(Paths.get(path));
}
```

### `@NonNull`
Ajoute une vérification de nullité.
```java
public class Account {
    public Account(@NonNull String id) {
        this.id = id;
    }
    private String id;
}
```

---

## 📦 Installation avec Maven

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.30</version>
    <scope>provided</scope>
</dependency>
```

---

## 🔗 Ressources utiles

- [Documentation officielle](https://projectlombok.org/features/all)
- [Tutoriel vidéo YouTube](https://www.youtube.com/results?search_query=lombok+java+tutorial)
- [Exemples sur GitHub](https://github.com/search?q=lombok+java+examples)

---

## ⚠️ Inconvénients et points à surveiller

- **Dépendance à une bibliothèque externe** : peut poser problème dans certains environnements de build.
- **Moins de visibilité** sur le code généré automatiquement.
- **Problèmes de compatibilité** avec certains outils ou IDE.
- **Debugging plus complexe** : les méthodes générées ne sont pas visibles dans le code source.

---

*Notes de cours préparées par Olivier Phénix, Enseignant aux adultes.*
