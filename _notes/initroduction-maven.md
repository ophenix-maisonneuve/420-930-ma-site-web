---
layout: default
title: "Introduction à Maven"
nav_order: 4
---

# Introduction à Maven

Apache Maven est un outil de gestion de projet et d'automatisation de la construction pour les projets Java. Il permet de compiler, tester, empaqueter et déployer des applications de manière standardisée.

---

## Cycle de vie de Maven

Maven fonctionne selon un **cycle de vie** composé de plusieurs **phases** :

1. **validate** : vérifie que le projet est correct.
2. **compile** : compile le code source.
3. **test** : exécute les tests unitaires.
4. **package** : crée un fichier JAR ou WAR.
5. **verify** : vérifie que l'artefact généré est valide.
6. **install** : installe l'artefact généré dans le dépôt local.
7. **deploy** : déploie l'artefact dans un dépôt distant.

---

## Structure du fichier `pom.xml`

Le fichier `pom.xml` est le cœur du projet Maven. Voici les sections importantes :

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.exemple</groupId>
    <artifactId>mon-projet</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging>

    <dependencies>
        <!-- Dépendances ici -->
    </dependencies>

    <build>
        <plugins>
            <!-- Plugins ici -->
        </plugins>
    </build>
</project>
```

---

## Plugins Maven

Les plugins Maven sont des modules permettent d'étendre les fonctionnalités du cycle de vie de construction. Ils sont utilisés pour compiler du code, exécuter des tests, créer des fichiers JAR, déployer des artefacts, etc. On peut rattacher l'exécution d'un plugin à l'une des phases du cycle de vie de Maven, ce qui permet d'ajouter des fonctionnalités et de personnaliser la construction.

## Exemple 1 : Créer un fichier `.jar`

### Structure du projet :
```
mon-projet/
├── pom.xml
└── src/
    └── main/
        └── java/
            └── com/
                └── exemple/
                    └── App.java
```

Structure minimale du `pom.xml` :

```xml
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.exemple</groupId>
  <artifactId>mon-projet</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>jar</packaging>

  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-jar-plugin</artifactId>
        <version>3.4.2</version>
        <configuration>
          <archive>
            <manifest>
              <mainClass>com.exemple.Main</mainClass>
            </manifest>
          </archive>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

Classe Java :

```java
package com.exemple;

public class Main {
    public static void main(String[] args) {
        System.out.println("Bonjour Maven !");
    }
}
```

Compilation :
```bash
mvn package
```
Le fichier `.jar` sera généré dans le dossier `target/mon-projet-1.0-SNAPSHOT.jar`.

Exécution :
```bash
java -jar target/mon-projet-1.0-SNAPSHOT.jar
```

---

## Exemple 2 : Exécuter le programme avec `exec:java`

### Ajouter le plugin dans `pom.xml` :
```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.codehaus.mojo</groupId>
      <artifactId>exec-maven-plugin</artifactId>
      <version>3.6.2</version>
      <configuration>
        <mainClass>com.exemple.App</mainClass>
      </configuration>
    </plugin>
  </plugins>
</build>
```

### Commande pour exécuter :
```bash
mvn compile
mvn exec:java
```

Cela exécutera la méthode `main()` de la classe `App`.

---

## Références utiles

- [Documentation officielle de Maven](https://maven.apache.org/guides/index.html)
- [Guide Maven par Baeldung](https://www.baeldung.com/maven)
- [Tutoriel Maven par OpenClassrooms](https://openclassrooms.com/fr/courses/26832-apprenez-a-programmer-en-java/26838-utilisez-maven-pour-gerer-vos-projets)
