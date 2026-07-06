# ComLabs IAM Documentation

Bienvenue dans la documentation officielle de **ComLabs IAM**.

Cette documentation décrit l'ensemble de l'architecture, du modèle métier, des choix techniques et des décisions de conception du projet.

L'objectif est de fournir une documentation claire, maintenable et évolutive permettant à tout développeur de comprendre le fonctionnement de ComLabs IAM sans devoir commencer par lire le code.

---

# Qu'est-ce que ComLabs IAM ?

ComLabs IAM (Identity & Access Management) est un fournisseur d'identité (Identity Provider) destiné à centraliser la gestion des identités, l'authentification et l'autorisation de plusieurs applications.

Le projet est développé selon une approche **Domain Driven Design (DDD)** afin de garantir une architecture modulaire, évolutive et indépendante des applications clientes.

---

# Philosophie

Le projet repose sur quelques principes fondamentaux :

- Une seule identité pour plusieurs applications.
- Une seule source de vérité.
- Une authentification centralisée.
- Une architecture orientée domaine.
- Un moteur piloté par des politiques de sécurité (Policy Driven).
- Une séparation stricte entre métier, architecture et technique.

---

# Structure de la documentation

```
docs/
│
├── README.md
│
├── 01-philosophy/
│
├── 02-product/
│
├── 03-domain-model/
│
├── 04-architecture/
│
├── 05-decisions/
│
├── 06-technical-design/
│
├── 07-development-guide/
│
├── 08-sprints/
│
├── handbook/
│
└── templates/
```

---

# Contenu

## 01 - Philosophy

Décrit les valeurs fondamentales du projet.

Ce dossier répond à la question :

> Pourquoi ComLabs IAM existe-t-il ?

---

## 02 - Product

Décrit le produit.

On y retrouve :

- la vision ;
- le périmètre ;
- la roadmap ;
- le glossaire.

---

## 03 - Domain Model

Le cœur du projet.

Chaque document décrit un concept métier.

Exemples :

- Identity
- Credential
- Session
- Client
- Authentication
- Authorization

---

## 04 - Architecture

Décrit l'architecture générale du système.

Diagrammes.

Relations entre domaines.

Interactions.

---

## 05 - Decisions

Contient les Architecture Decision Records (ADR).

Chaque ADR explique une décision importante prise pendant la conception du projet.

---

## 06 - Technical Design

Décrit les choix techniques.

Symfony.

Doctrine.

JWT.

Base de données.

API.

Infrastructure.

---

## 07 - Development Guide

Documentation destinée aux développeurs.

Conventions.

Organisation du code.

Workflow Git.

Tests.

---

## 08 - Sprints

Historique du développement.

Chaque Sprint documente :

- les objectifs ;
- les décisions prises ;
- les documents créés ;
- les prochaines étapes.

---

## Handbook

Décrit la manière dont cette documentation est organisée.

Il constitue le guide de référence pour maintenir une documentation homogène.

---

## Templates

Contient les modèles utilisés pour créer tous les documents du projet.

---

# Lecture recommandée

Pour découvrir ComLabs IAM, il est recommandé de lire les documents dans l'ordre suivant :

1. Philosophy
2. Product
3. Domain Model
4. Architecture
5. Decisions
6. Technical Design

---

# Organisation du projet

Cette documentation est volontairement indépendante du code source.

Les concepts métier sont définis avant leur implémentation.

Les décisions d'architecture sont documentées avant leur développement.

Cette approche garantit une meilleure maintenabilité du projet et facilite son évolution.

---

# Licence

Cette documentation fait partie intégrante du projet ComLabs IAM.V