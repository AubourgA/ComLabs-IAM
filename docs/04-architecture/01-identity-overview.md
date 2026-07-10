# Architecture 001 - Identity Overview

**Status** : Accepted  
**Version** : 1.0  
**Last Update** : 2026-07-10

---

# Vision

ComLabs IAM est un **Identity Provider** dont la mission est de fournir un service centralisé d'authentification et de gestion des identités pour l'ensemble de l'écosystème ComLabs.

Il constitue le point d'entrée de confiance entre les utilisateurs et les applications de l'entreprise.

Son objectif n'est pas de remplacer les applications métiers mais de leur fournir un mécanisme commun, sécurisé et homogène pour identifier les utilisateurs, contrôler l'accès aux applications et appliquer les politiques de sécurité de l'organisation.

Toutes les applications de l'écosystème délèguent ces responsabilités à ComLabs IAM.

---

# Objectifs

ComLabs IAM poursuit plusieurs objectifs majeurs :

- centraliser l'authentification des utilisateurs ;
- centraliser les politiques de sécurité ;
- garantir un comportement homogène entre toutes les applications ;
- assurer la traçabilité des événements de sécurité ;
- découpler la gestion des identités des applications métiers ;
- permettre l'évolution indépendante des applications et du système d'identité.

Le système est conçu pour rester indépendant des domaines métiers qu'il protège.

---

# Positionnement

ComLabs IAM ne constitue pas une application métier.

Il fournit des services d'identité utilisés par les autres applications.

Les applications clientes restent propriétaires de leur logique fonctionnelle.

ComLabs IAM intervient uniquement dans les domaines suivants :

- gestion des identités ;
- authentification ;
- gestion des environnements de connexion ;
- application des politiques de sécurité ;
- autorisation d'accès aux applications ;
- gestion des sessions ;
- audit des événements de sécurité.

---

# Ce que ComLabs IAM ne fait pas

ComLabs IAM ne possède aucune connaissance du métier des applications.

Il ne connaît pas :

- les éprouvettes béton ;
- les essais laboratoire ;
- les chantiers ;
- les prélèvements ;
- les factures ;
- les commandes ;
- les workflows métiers.

Ces responsabilités appartiennent exclusivement aux applications clientes.

Cette séparation constitue l'un des principes fondateurs de l'architecture.

---

# Les acteurs

L'architecture fait intervenir deux catégories principales d'acteurs.

## Les Identities

Une Identity représente une personne physique connue par ComLabs IAM.

Une Identity peut :

- s'authentifier ;
- ouvrir des Sessions ;
- utiliser plusieurs Clients ;
- posséder plusieurs Devices.

---

## Les Clients

Un Client représente une application de confiance enregistrée auprès de ComLabs IAM.

Exemples :

- ComLabs Labo
- ComLabs Sampling
- ComLabs R&D
- ComLabs Materials

Une application ne peut utiliser ComLabs IAM qu'après avoir été enregistrée comme Client.

Le Client constitue le point d'entrée des demandes d'authentification.

---

# Les responsabilités de ComLabs IAM

ComLabs IAM est responsable de :

- vérifier l'identité d'un utilisateur ;
- reconnaître son environnement de connexion ;
- appliquer les politiques de sécurité ;
- autoriser ou refuser l'accès à une application ;
- créer une Session ;
- conserver une trace des événements de sécurité.

Chaque responsabilité est portée par un domaine métier indépendant.

---

# Les domaines métier

Le cœur fonctionnel de ComLabs IAM est composé des domaines suivants.

```text
Identity

Login Identifier

Credential

Authentication

Device

Security Policy

Authorization

Session

Client

Audit
```

Chaque domaine possède une responsabilité unique.

Aucun domaine ne doit contenir les responsabilités d'un autre.

Cette séparation permet de limiter le couplage et de faciliter les évolutions futures.

---

# Philosophie de conception

L'ensemble de l'architecture repose sur plusieurs principes fondamentaux.

## Une responsabilité par domaine

Chaque domaine répond à une seule question métier.

Exemple :

```text
Identity
    Qui est la personne ?

Authentication
    Est-elle bien celle qu'elle prétend être ?

Device
    Depuis quel environnement se connecte-t-elle ?

Security Policy
    Les règles autorisent-elles cette connexion ?

Authorization
    Peut-elle accéder à cette application ?

Session
    Comment conserver son état de connexion ?

Audit
    Que s'est-il passé ?
```

Chaque domaine possède une responsabilité clairement identifiée.

---

## Les domaines collaborent sans se remplacer

Les domaines communiquent entre eux mais restent indépendants.

Par exemple :

Authentication ne connaît pas les règles de sécurité.

Device ne décide jamais si une connexion est autorisée.

Security Policy ne crée jamais de Session.

Audit n'intervient jamais dans les décisions.

Chaque domaine apporte uniquement les informations qui relèvent de sa responsabilité.

---

## Les décisions sont centralisées

Toutes les décisions de sécurité sont prises par ComLabs IAM.

Les applications clientes ne doivent jamais implémenter leurs propres mécanismes d'authentification.

Cette centralisation garantit un comportement homogène dans tout l'écosystème.

---

## Les applications restent autonomes

Une fois l'accès accordé par ComLabs IAM, chaque application reste responsable de son propre métier.

Par exemple :

ComLabs IAM décide :

```text
Jean peut accéder à ComLabs Labo.
```

Puis :

ComLabs Labo décide :

```text
Jean peut créer une éprouvette.

Jean peut modifier un essai.

Jean peut consulter un rapport.
```

Les rôles et les permissions métier appartiennent exclusivement aux applications clientes.

---

# Principes architecturaux

L'architecture de ComLabs IAM repose sur les principes suivants :

- séparation des responsabilités ;
- faible couplage entre les domaines ;
- forte cohésion des modèles métier ;
- indépendance vis-à-vis des technologies ;
- indépendance vis-à-vis des applications clientes ;
- évolutivité des politiques de sécurité ;
- traçabilité complète des événements.

Ces principes guident toutes les décisions de conception du projet.

---

# Conclusion

ComLabs IAM constitue le socle de confiance de l'écosystème ComLabs.

Son rôle est de gérer les identités, sécuriser les accès aux applications et garantir une politique de sécurité homogène.

Il ne remplace jamais les applications métiers.

Il leur fournit un service d'identité centralisé, fiable et indépendant.

Les chapitres suivants détaillent la manière dont les différents domaines collaborent pour atteindre cet objectif.