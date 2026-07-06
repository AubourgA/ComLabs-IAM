# Architecture Handbook

**Version** : 1.0

---

# Introduction

Ce document définit les principes d'architecture utilisés pour concevoir **ComLabs IAM**.

Son objectif n'est pas de décrire le fonctionnement du produit.

Il définit la manière dont le produit doit être conçu.

Toutes les décisions d'architecture doivent respecter les principes présentés dans ce document.

---

# Notre philosophie

Nous considérons que :

> Une architecture solide est plus importante qu'une implémentation rapide.

Le code évoluera.

Les frameworks évolueront.

Les technologies évolueront.

Le modèle métier, lui, doit rester stable.

Notre objectif est donc de construire un modèle métier robuste, indépendant de toute technologie.

---

# Les principes fondamentaux

## Le métier avant la technique

La première étape d'un développement consiste toujours à comprendre le métier.

Aucune décision technique ne doit être prise avant d'avoir identifié les concepts métier.

Le code est une conséquence du métier.

---

## Le domaine avant la classe

Nous ne concevons jamais une classe directement.

Nous concevons d'abord un domaine.

Puis les concepts de ce domaine.

Puis seulement les objets qui le composent.

---

## Une responsabilité unique

Chaque domaine possède une responsabilité clairement définie.

Un domaine ne doit jamais réaliser plusieurs métiers.

Cette règle s'applique également aux classes.

---

## Une décision documentée

Toute décision importante doit être documentée dans un ADR.

Aucune décision structurante ne doit uniquement exister dans le code.

---

## Un concept = un document

Chaque concept métier possède son propre document.

Exemple :

- Identity
- Credential
- Session
- Client
- Authentication

Cette règle permet d'éviter les documents trop volumineux.

---

## Une information = un seul endroit

Une information ne doit jamais être dupliquée.

Chaque information possède une source officielle.

Cette règle évite les incohérences.

---

# Domain Driven Design

ComLabs IAM est conçu selon les principes du Domain Driven Design (DDD).

Les domaines représentent les responsabilités métier du système.

Les technologies utilisées pour les implémenter sont secondaires.

Le modèle métier constitue le cœur du projet.

---

# Organisation des domaines

Chaque domaine est indépendant.

Chaque domaine possède :

- sa responsabilité ;
- son langage métier ;
- ses règles ;
- ses objets.

Les domaines communiquent entre eux sans partager leur logique interne.

---

# Les couches

Chaque domaine sera organisé selon les couches suivantes.

```text
Domain

↓

Application

↓

Infrastructure

↓

Presentation
```

Chaque couche possède une responsabilité unique.

Une couche ne doit jamais dépendre d'une couche située au-dessus.

---

# Les règles métier

Les règles métier appartiennent au domaine.

Elles ne doivent jamais être implémentées dans :

- les contrôleurs ;
- les repositories ;
- les services techniques.

---

# Les Policies

Les comportements du système sont pilotés par des Policies.

Une Policy représente une règle métier configurable.

Les Policies ne réalisent aucune opération.

Elles définissent uniquement le comportement attendu.

---

# Les événements métier

Lorsqu'un événement important se produit, le domaine publie un Domain Event.

Exemples :

- Identity Created
- Password Changed
- Session Opened
- User Locked

Les autres domaines réagissent à ces événements.

Ils ne doivent jamais accéder directement aux objets internes d'un autre domaine.

---

# Les Value Objects

Les concepts sans identité propre seront modélisés sous forme de Value Objects.

Exemples possibles :

- Email Address
- Password Hash
- Phone Number

Un Value Object est immuable.

---

# Les Entités

Les objets possédant une identité propre sont des Entités.

Exemples :

- Identity
- Client
- Session

Une Entité possède un identifiant stable.

---

# Les Aggregates

Les Aggregates permettent de protéger la cohérence des règles métier.

Un Aggregate contrôle toujours les modifications de ses objets internes.

Les Aggregates seront identifiés progressivement pendant la conception.

Ils ne seront jamais créés sans justification métier.

---

# Les Services

Un Service existe lorsqu'une opération :

- n'appartient à aucune Entité ;
- n'appartient à aucun Value Object.

Les Services doivent rester rares.

Le modèle métier doit toujours être privilégié.

---

# Les Repositories

Les Repositories appartiennent au domaine.

Ils représentent uniquement l'accès aux Aggregates.

Ils ne contiennent aucune logique métier.

---

# Les Domain Events

Les Domain Events permettent de découpler les domaines.

Ils représentent des faits métier.

Ils ne représentent jamais des commandes.

---

# Les ADR

Chaque décision d'architecture importante possède son ADR.

Les ADR racontent l'histoire du projet.

Ils expliquent :

- le contexte ;
- les alternatives ;
- la décision ;
- les conséquences.

---

# Les technologies

Symfony, PostgreSQL, JWT, Redis, Docker...

Toutes ces technologies sont considérées comme des détails d'implémentation.

Elles peuvent évoluer sans remettre en cause le modèle métier.

---

# Notre manière de travailler

Chaque nouvelle fonctionnalité suit toujours le même processus.

```text
Besoin

↓

Réflexion métier

↓

Documentation

↓

Domain Model

↓

Architecture

↓

ADR

↓

Implémentation

↓

Tests
```

Le code est toujours la dernière étape.

---

# Notre objectif

Construire un moteur IAM :

- robuste ;
- modulaire ;
- évolutif ;
- maintenable ;
- indépendant des applications qui l'utilisent.

Chaque décision prise doit aller dans cette direction.

---

# Conclusion

L'Architecture Handbook constitue la référence principale pour toutes les décisions d'architecture de ComLabs IAM.

En cas de doute, ce document fait foi.

L'objectif n'est pas seulement de développer un logiciel.

L'objectif est de construire une architecture capable d'évoluer pendant de nombreuses années.