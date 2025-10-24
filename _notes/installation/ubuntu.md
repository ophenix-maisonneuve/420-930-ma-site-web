---
layout: default
title: "Ubuntu 24.04"
nav_order: 1
parent: "Installation de l'environnement"
---

# Installation sur Ubuntu 24.04

## Java JDK 25
```bash
sudo apt update
sudo apt install openjdk-25-jdk
java -version
```

## Maven
```bash
sudo apt install mave --no-install-recommends 
mvn -version
```

## Visual Studio Code
```bash
sudo snap install code --classic
```
