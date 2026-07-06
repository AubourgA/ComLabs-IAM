# Documentation Handbook

**Version** : 1.0

---

# Introduction

Ce document définit les règles de rédaction et d'organisation de la documentation de **ComLabs IAM**.

Son objectif est de garantir une documentation :

- claire ;
- homogène ;
- évolutive ;
- facilement maintenable.

Chaque nouveau document créé dans le projet doit respecter les conventions décrites dans ce guide.

---

# Objectifs

La documentation doit permettre à toute personne de comprendre :

- pourquoi le projet existe ;
- comment il est organisé ;
- comment il fonctionne ;
- pourquoi certaines décisions ont été prises ;
- comment contribuer au projet.

La documentation est considérée comme une partie intégrante du produit.

---

# Philosophie

Avant d'écrire du code, nous écrivons la documentation.

Avant de prendre une décision technique, nous la documentons.

Avant de créer une classe, nous définissons le concept métier qu'elle représente.

Le code est une conséquence du modèle métier.

La documentation est la mémoire du projet.

---

# Les différents niveaux de documentation

La documentation est organisée en plusieurs niveaux.

Chaque information possède une place unique.

Une même information ne doit jamais être dupliquée dans plusieurs documents.

---

# 1. Philosophy

Le dossier **01-philosophy** décrit les valeurs du projet.

On y trouve :

- pourquoi le projet existe ;
- les grands principes de conception ;
- les règles qui ne changeront jamais.

Il ne contient jamais :

- de code ;
- de détails techniques ;
- de choix d'implémentation.

---

# 2. Product

Le dossier **02-product** décrit le produit.

On y retrouve :

- la vision ;
- le périmètre ;
- la roadmap ;
- le glossaire.

Ce dossier est destiné aussi bien aux développeurs qu'aux décideurs.

---

# 3. Domain Model

Le dossier **03-domain-model** décrit les concepts métier.

Chaque document représente un concept unique.

Exemple :

- Identity
- Credential
- Session
- Client
- Role

Un document ne décrit jamais plusieurs concepts.

Le modèle métier est indépendant de toute technologie.

Les documents de ce dossier ne doivent jamais parler :

- de Symfony ;
- de Doctrine ;
- de PostgreSQL ;
- de JWT ;
- d'implémentation technique.

---

# 4. Architecture

Le dossier **04-architecture** décrit la structure globale du système.

Il contient :

- les diagrammes ;
- les vues d'ensemble ;
- les interactions entre domaines.

Il ne décrit jamais les détails d'implémentation.

---

# 5. Decisions

Le dossier **05-decisions** contient les Architecture Decision Records (ADR).

Chaque ADR répond à une seule question :

> Pourquoi cette décision a-t-elle été prise ?

Une ADR ne décrit jamais :

- le fonctionnement du système ;
- les concepts métier.

Elle documente uniquement une décision.

---

# 6. Technical Design

Le dossier **06-technical-design** décrit les choix techniques.

Exemples :

- choix de Symfony ;
- structure de la base de données ;
- stockage des mots de passe ;
- JWT ;
- OpenID Connect ;
- infrastructure.

Ce dossier peut évoluer régulièrement.

---

# 7. Development Guide

Le dossier **07-development-guide** décrit les conventions de développement.

On y retrouve :

- conventions de nommage ;
- workflow Git ;
- stratégie de tests ;
- bonnes pratiques.

---

# 8. Sprints

Chaque Sprint possède son propre document.

Chaque Sprint contient :

- les objectifs ;
- les décisions prises ;
- les documents créés ;
- les prochaines étapes.

L'objectif est de conserver l'historique de la conception du projet.

---

# Les modèles de documents

Tous les documents doivent respecter les modèles présents dans le dossier **templates**.

Cela garantit une documentation homogène.

---

# Les règles de rédaction

## Une responsabilité par document

Chaque document décrit un seul sujet.

Exemple :

Identity

Credential

Session

Password Policy

Authentication

Chaque concept possède son propre document.

---

## Ne jamais mélanger métier et technique

Le modèle métier décrit uniquement les concepts.

Les détails techniques sont documentés dans Technical Design.

---

## Les ADR décrivent uniquement les décisions

Une ADR répond toujours à :

Pourquoi ?

Jamais :

Comment ?

---

## Les diagrammes

Les diagrammes utilisent exclusivement Mermaid.

Ils doivent être simples et lisibles.

---

## Le Markdown

Tous les documents sont écrits en Markdown.

Aucun format propriétaire n'est utilisé.

---

# Cycle de vie d'un document

Chaque document suit le cycle suivant :

Draft

↓

Review

↓

Accepted

↓

Deprecated

↓

Archived

Le statut doit apparaître en haut du document.

---

# Numérotation

Les documents sont numérotés afin de faciliter leur lecture.

Exemple :

01-identity.md

02-login-identifier.md

03-credential.md

La numérotation ne représente pas une priorité.

Elle représente uniquement un ordre de lecture recommandé.

---

# Diagrammes

Les diagrammes sont réalisés avec Mermaid.

Les diagrammes doivent privilégier :

- la simplicité ;
- la lisibilité ;
- la compréhension métier.

---

# Principe fondamental

Une information ne doit exister qu'à un seul endroit.

Si une information est répétée dans plusieurs documents, la documentation deviendra incohérente avec le temps.

Chaque information possède un document de référence.

---

# Conclusion

La documentation constitue une partie essentielle de ComLabs IAM.

Elle évolue au même rythme que le code.

Toute évolution du projet doit être documentée avant son implémentation.

Cette discipline garantit une architecture cohérente, maintenable et compréhensible sur le long terme.