# Domain Model 008 - Authorization

**Status** : Accepted  
**Version** : 1.0  
**Last Update** : 2026-07-08

---

# Objectif

Le domaine **Authorization** détermine si une **Identity** est autorisée à accéder à une ressource protégée.

Dans ComLabs IAM, la principale ressource protégée est un **Client**.

Authorization intervient après une authentification réussie et avant l'autorisation d'accès à l'application.

---

# Définition

L'autorisation consiste à vérifier qu'une Identity authentifiée possède les droits nécessaires pour accéder à une ressource.

L'authentification répond à la question :

> **Qui êtes-vous ?**

L'autorisation répond à la question :

> **Que pouvez-vous faire ?**

Ces deux concepts sont indépendants et complémentaires.

---

# Responsabilités

Le domaine Authorization est responsable de :

- déterminer si une Identity peut accéder à un Client ;
- vérifier les autorisations applicables ;
- collaborer avec Security Policy lorsque des règles de sécurité influencent l'autorisation ;
- transmettre le résultat de la décision au Client ;
- produire les événements nécessaires au domaine Audit.

---

# Hors responsabilités

Le domaine Authorization n'est pas responsable de :

- authentifier une Identity ;
- créer une Session ;
- gérer les Credentials ;
- définir les rôles ;
- définir les permissions métier propres aux applications.

Ces responsabilités appartiennent aux autres domaines.

---

# Cycle de vie

Le domaine Authorization intervient après une authentification réussie.

```text
Authentication
        │
        ▼
Authorization
        │
        ├──────────────┐
        ▼              ▼
Accès autorisé   Accès refusé
```

---

# Relations

## Identity

Authorization prend une décision pour une Identity authentifiée.

Une Identity ne peut être autorisée que si son authentification est valide.

---

## Authentication

Authorization ne peut intervenir qu'après une authentification réussie.

---

## Session

Une Session valide est nécessaire pour demander une autorisation.

---

## Client

Le Client représente la ressource principale protégée par ComLabs IAM.

Authorization décide si une Identity peut accéder à ce Client.

---

## Role

Authorization exploite les rôles attribués à une Identity afin de prendre sa décision.

Le domaine Role définit les rôles mais ne prend pas les décisions d'autorisation.

---

## Permission

Authorization peut utiliser les Permissions afin d'affiner ses décisions.

Le domaine Permission définit les permissions disponibles.

---

## Security Policy

Security Policy peut imposer des contraintes complémentaires.

Par exemple :

- compte désactivé ;
- accès temporairement interdit ;
- restrictions horaires ;
- authentification multifacteur obligatoire.

Authorization applique ces décisions sans les définir.

---

## Audit

Chaque décision importante prise par Authorization doit être enregistrée.

Exemples :

- authorization.granted
- authorization.denied
- authorization.rejected_by_policy

---

# Règles métier

## Règle 1

Une Identity doit être authentifiée avant toute autorisation.

---

## Règle 2

Une Identity ne peut accéder qu'aux Clients pour lesquels elle possède une autorisation.

---

## Règle 3

Authorization décide uniquement de l'accès au Client.

Les actions métier réalisées dans le Client restent sous la responsabilité de l'application.

---

## Règle 4

Les modifications d'autorisation prennent effet lors de la prochaine création d'une Session.

Les Sessions déjà actives conservent leurs autorisations jusqu'à leur expiration ou leur fermeture.

---

## Règle 5

Toutes les décisions d'autorisation doivent être auditables.

---

# Gouvernance

Les règles d'autorisation sont administrées par les administrateurs de ComLabs IAM.

Les droits accordés à une Identity peuvent évoluer au cours de son cycle de vie.

Toute modification est enregistrée et appliquée conformément aux règles du domaine Security Policy.

---

# Exemple

Une Identity souhaite accéder à **ComLabs Labo**.

Le processus est le suivant :

```text
Identity
      │
      ▼
Authentication
      │
      ▼
Authorization
      │
      ├──────────────┐
      ▼              ▼
Accès autorisé   Accès refusé
```

Si l'accès est autorisé, le Client ouvre une nouvelle Session.

L'application ComLabs Labo reste ensuite responsable des autorisations métier propres à son domaine.

---

# Principes

## Authorization protège les Clients

Le rôle principal du domaine Authorization est de contrôler l'accès aux applications enregistrées dans ComLabs IAM.

---

## Authorization ne gère pas les règles métier

Le domaine Authorization ne décide jamais si un utilisateur peut créer une éprouvette, modifier un chantier ou supprimer une facture.

Ces décisions appartiennent exclusivement aux applications clientes.

---

## Authorization est indépendant du métier

Le domaine Authorization ne possède aucune connaissance des fonctionnalités des applications.

Il prend uniquement des décisions d'accès.

---

## Authorization est centralisé

Toutes les décisions d'accès aux Clients sont prises par ComLabs IAM afin de garantir un comportement homogène dans l'ensemble de l'écosystème.

---

# Décisions prises

- Authorization intervient uniquement après une authentification réussie.
- Authorization décide de l'accès aux Clients.
- Les applications clientes restent responsables de leurs autorisations métier.
- Les modifications d'autorisation prennent effet à la prochaine Session.
- Toutes les décisions d'autorisation sont auditables.

---

# Évolutions prévues

Les futures versions pourront enrichir le domaine Authorization avec :

- autorisation contextuelle ;
- contrôle d'accès basé sur les risques ;
- autorisation adaptative ;
- délégation d'autorisation ;
- règles dynamiques.

Ces évolutions devront respecter les principes définis par le présent domaine.

---

# Conclusion

Le domaine **Authorization** garantit qu'une Identity authentifiée peut uniquement accéder aux Clients pour lesquels elle possède les autorisations nécessaires.

En limitant sa responsabilité au contrôle d'accès aux applications, Authorization reste indépendant des règles métier propres à chaque Client.

Cette séparation assure une architecture claire, évolutive et conforme aux principes de conception de ComLabs IAM.