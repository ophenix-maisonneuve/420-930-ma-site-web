---
layout: default
title: "Installation de l'environnement"
nav_order: 1
has_toc: true
---
# Installation et personnalisation de l'environnement

Vous trouverez ici toute l'information pour installer et personnaliser votre environnement de développement.

## Installation de Java, Maven et Visual Studio Code

*Si vous utilisez la machine virtuelle du cours, ces étapes ont déjà été effectuées*

- [Ubuntu 24.04](ubuntu.md)
- [Windows 11](windows.md)
- [macOS](macos.md)

## Installation des extensions Java dans Visual Studio Code

*Si vous utilisez la machine virtuelle du cours, ces étapes ont déjà été effectuées*

### 1. Ouvrir Visual Studio Code

Lancez **VS Code** depuis le menu Démarrer ou un raccourci.

---

### 2. Accéder au gestionnaire d’extensions

Cliquez sur l’icône des **extensions** dans la barre latérale gauche ou utilisez le raccourci `Ctrl+Shift+X`.

---

### 3. Rechercher le Java Extension Pack

Dans la barre de recherche, tapez :

```
Java Extension Pack
```

Vous verrez un résultat comme celui-ci :

---

### 4. Installer l'ensemble d'extensions

Cliquez sur **Install** pour installer l'ensemble complet. Il inclut :

- Language Support for Java™ by Red Hat
- Debugger for Java
- Test Runner for Java
- Maven for Java
- Project Manager for Java
- Visual Studio IntelliCode

---

### 5. Redémarrer VS Code (si nécessaire)

Après l’installation, redémarrez VS Code pour que toutes les extensions soient bien chargées.

## Installation des additions invités VirtualBox (Guest Additions)


### 1. Mettre à jour le système

```bash
sudo apt update && sudo apt upgrade -y
```

### 2. Installer les paquets nécessaires

```bash
sudo apt install build-essential dkms linux-headers-$(uname -r) -y
```

### 3. Insérer l’image ISO des Guest Additions

Dans le menu de VirtualBox :

- Aller dans **Périphériques > Insérer l’image CD des Additions Invité...**

Cela montera un CD dans `/media/<utilisateur>/VBox_GAs_...`

### 4. Exécuter le script d’installation

```bash
sudo sh /media/$USER/VBox_GAs_*/VBoxLinuxAdditions.run
```

### 5. Redémarrer la machine virtuelle

```bash
sudo reboot
```

---

### 6. Vérification

Après redémarrage, vérifier que :

- Le redimensionnement automatique de l’écran fonctionne
- Le presse-papiers partagé est actif (si activé dans les paramètres)

## Personnalisation de l'apparence de Ubuntu MATE
