---
layout: default
title: "Principes SOLID"
nav_order: 10
has_toc: false
published: false
---

# Exercice: Analyse et correctifs SOLID

## Objectifs

- Comprendre les principes SOLID
- Analyser des cas où ils sont enfreints et les conséquences
- Proposer des correctifs appropriés

## Contexte

On vous propose ci-bas différents extraits d'une application fictive qui implémente un jeu de type *Escape Room* en ligne. Chacun des extraits enfreint l'un des principes SOLID.

## 1. SRP - Principe de responsabilité unique

```java
public class GameManager {
    private int score;
    private int secondsRemaining;

    public GameManager() {
        this.score = 0;
        this.secondsRemaining = 900; // 15 minutes
    }

    public int getScore() {
        return this.score;
    }

    public int getSecondsRemaining() {
        return this.secondsRemaining;
    }

    // Démarrer la partie + démarrer le chronomètre + logger
    public void startGame() {
        System.out.println("Partie démarrée.");
        this.secondsRemaining = 900;
    }

    // Gérer une énigme, donner un indice, augmenter score, logger
    public void solvePuzzle(String puzzleId, String answer) {
        if (answer != null && answer.length() > 0) {
            this.score = this.score + 100;
            System.out.println("Enigme " + puzzleId + " complétée -> +100 points");
        } else {
            System.out.println("Mauvaise réponse.");
        }
    }

    // Gestion du timer (décrément + logs)
    public void tick() {
        this.secondsRemaining = this.secondsRemaining - 1;
        if (this.secondsRemaining % 60 == 0) {
            System.out.println("Temps restant: " + this.secondsRemaining + "s");
        }
        if (this.secondsRemaining <= 0) {
            System.out.println("Game over.");
        }
    }

    // Donner un indice ET pénaliser le score
    public String giveHint(String puzzleId) {
        this.score = this.score - 20;
        return "Indice pour " + puzzleId + ": regardez le tableau!";
    }
}
```
1. Pourquoi le code ci-haut enfreint le principe de responsabilité unique ?
1. Proposez une nouvelle version du code qui corrige le problème.


## 2. OCP - Principe ouvert/fermé

```java
public class DifficultyCalculator {
    public int computeSecondsForPuzzle(String puzzleType) {
        if ("TEXT".equals(puzzleType)) {
            return 300;
        } else if ("LOGIC".equals(puzzleType)) {
            return 420;
        } else if ("MAZE".equals(puzzleType)) {
            return 600;
        } else {
            return 240;
        }
    }
}
```

1. Pourquoi le code ci-haut enfreint le principe ouvert/fermé ?
  1. **Indice** : Si on désirait ajouter un nouveau type d'énigme, comment devrait-on procéder ?
1. Proposez une nouvelle version du code qui corrige le problème.


## 3. LSP - Principe de substitution de Liskov

```java

// Contrat implicite : attempt() ne lance pas d'exception et retourne false si l'entrée est invalide (null)
public class PuzzleBase {
    public boolean attempt(String input) {
        if (input == null) {
            return false;
        }
        return input.length() >= 1;
    }
}

public class LaserMazePuzzle extends PuzzleBase {
    @Override
    public boolean attempt(String input) {
        if (input == null) {
            throw new IllegalArgumentException("LaserMaze requires a START command.");
        }
        if (!"START".equals(input)) {
            throw new UnsupportedOperationException("Invalid command for LaserMaze.");
        }
        return true;
    }
}

// Code client écrit contre le type de base
public class PuzzleRunner {
    public boolean run(PuzzleBase puzzle, String input) {
        return puzzle.attempt(input); // suppose aucune exception
    }
}
```

1. Que se passera-t-il si l'entrée (`input`) est `null` dans les cas suivants :
  1. Si `puzzle` est de type `PuzzleBase` ?
  1. Si `puzzle` est de type `LaserMazePuzzle` ?
1. En fonction de vos réponses ci-haut, le principe de substitution de Liskov est-il respecté ? Pourquoi ?
1. Si le principe n'est pas respecté, proposez une nouvelle version du code qui corrige le problème.


### 4. ISP - Principe de ségrégation des interfaces

```java
/**
 * Interface qui définit une console de jeu utilisable pour jouer au escape room
 * Par exemple : terminal de texte, PC Windows, iPhone, etc
 */
public interface GameConsole {
    void displayText(String text);
    void playSound(String soundFile);
    void vibrate(int intensity);
    void showMap(String roomId);
    void recordVideo(String filePath);
}

/**
 * Implémentation la plus basique d'une console de jeu : un terminal texte
 */
public class TextTerminal implements GameConsole {
    public void displayText(String text) {
        System.out.println(text);
    }

    public void playSound(String soundFile) {
        throw new UnsupportedOperationException("Le son n'est pas pris en charge.");
    }

    public void vibrate(int intensity) {
        throw new UnsupportedOperationException("La vibration n'est pas prise en charge.");
    }

    public void showMap(String roomId) {
        throw new UnsupportedOperationException("Les maps complexes ne sont pas prises en charge.");
    }

    public void recordVideo(String filePath) {
        throw new UnsupportedOperationException("La vidéo n'est pas prise en charge.");
    }
}
```

1. Pourquoi le code ci-haut enfreint le principe de ségrégation des interfaces ?
  1. **Indice** : Est-il réellement utile d'implémenter les méthodes `playSound`, `vibrate`, `showMap` et `recordVideo` pour un terminal de texte ?
1. Proposez une nouvelle version du code qui corrige le problème.

### 4. ISP - Principe de ségrégation des interfaces

```java
/**
 * Interface qui définit une console de jeu utilisable pour jouer au escape room
 * Par exemple : terminal de texte, PC Windows, iPhone, etc
 */
public interface GameConsole {
    void displayText(String text);
    void playSound(String soundFile);
    void vibrate(int intensity);
    void showMap(String roomId);
    void recordVideo(String filePath);
}

/**
 * Implémentation la plus basique d'une console de jeu : un terminal texte
 */
public class TextTerminal implements GameConsole {
    public void displayText(String text) {
        System.out.println(text);
    }

    public void playSound(String soundFile) {
        throw new UnsupportedOperationException("Le son n'est pas pris en charge.");
    }

    public void vibrate(int intensity) {
        throw new UnsupportedOperationException("La vibration n'est pas prise en charge.");
    }

    public void showMap(String roomId) {
        throw new UnsupportedOperationException("Les maps complexes ne sont pas prises en charge.");
    }

    public void recordVideo(String filePath) {
        throw new UnsupportedOperationException("La vidéo n'est pas prise en charge.");
    }
}
```

1. Pourquoi le code ci-haut enfreint le principe de ségrégation des interfaces ?
  1. **Indice** : Est-il réellement utile d'implémenter les méthodes `playSound`, `vibrate`, `showMap` et `recordVideo` pour un terminal de texte ?
1. Proposez une nouvelle version du code qui corrige le problème.