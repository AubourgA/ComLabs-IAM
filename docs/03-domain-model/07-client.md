# Domain Model 007 - Client

**Status** : Accepted  
**Version** : 1.0  
**Last Update** : 2026-07-08

---

# Objectif

Le domaine **Client** représente une application de confiance enregistrée auprès de ComLabs IAM.

Il permet d'identifier les applications autorisées à utiliser les services proposés par ComLabs IAM, tels que l'authentification, l'autorisation ou toute autre fonctionnalité de gestion des identités.

Le domaine Client constitue le lien entre l'écosystème applicatif et ComLabs IAM.

---

# Définition

Un **Client** représente une application enregistrée dans ComLabs IAM et reconnue comme digne de confiance.

L'existence d'une application ne signifie pas qu'elle peut utiliser ComLabs IAM.

Une application devient un Client uniquement après son enregistrement et sa validation par un administrateur autorisé.

Le Client représente ainsi la relation de confiance établie entre une application et ComLabs IAM.

---

# Responsabilités

Le domaine Client est responsable de :

- représenter une application autorisée à utiliser ComLabs IAM ;
- identifier de manière unique chaque application enregistrée ;
- maintenir les informations propres à une application ;
- permettre l'activation ou la désactivation d'un Client ;
- servir de point d'entrée aux demandes d'authentification et d'autorisation provenant des applications.

---

# Hors responsabilités

Le domaine Client n'est pas responsable de :

- authentifier une Identity ;
- créer une Session ;
- gérer les Credentials ;
- appliquer les Security Policies ;
- déterminer les Permissions d'une Identity ;
- gérer les rôles des utilisateurs.

Ces responsabilités appartiennent aux autres domaines du modèle métier.

---

# Cycle de vie

Un Client suit le cycle de vie suivant :

```text
Créé
   │
   ▼
Actif
   │
   ├──────────────┐
   ▼              ▼
Suspendu      Désactivé
```

### Créé

Le Client est enregistré dans ComLabs IAM.

Il n'est pas encore nécessairement utilisable.

### Actif

Le Client est autorisé à utiliser les services proposés par ComLabs IAM.

### Suspendu

Le Client est temporairement indisponible.

Cette suspension peut être liée à une maintenance ou à une décision administrative.

### Désactivé

Le Client n'est plus autorisé à utiliser ComLabs IAM.

Aucune nouvelle authentification ne peut être initiée.

---

# Relations

## Identity

Une Identity peut accéder à plusieurs Clients.

Chaque Client peut être utilisé par plusieurs Identities.

Le domaine Client ne gère pas les droits des utilisateurs.

---

## Authentication

Toutes les demandes d'authentification proviennent d'un Client.

Authentication vérifie l'identité de l'utilisateur avant d'autoriser l'accès au Client.

---

## Session

Une Session est toujours créée pour un Client.

Le Client représente l'application au sein de laquelle la Session sera utilisée.

---

## Authorization

Après authentification, Authorization détermine les actions que l'Identity est autorisée à réaliser au sein du Client.

Le domaine Client ne prend aucune décision d'autorisation.

---

## Security Policy

Le domaine Security Policy définit les règles applicables aux Clients.

Par exemple :

- autorisation ou interdiction d'accès ;
- périodes de maintenance ;
- restrictions d'utilisation ;
- autres politiques applicables aux applications.

Le domaine Client applique ces décisions sans les définir.

---

## Audit

Toutes les opérations importantes réalisées par un Client doivent être enregistrées.

Exemples :

- demande d'authentification ;
- activation ;
- désactivation ;
- suspension ;
- tentative d'accès refusée.

---

# Règles métier

## Règle 1

Une application doit être enregistrée dans ComLabs IAM avant de pouvoir utiliser ses services.

Une application inconnue ne peut jamais initier une authentification.

---

## Règle 2

Chaque environnement applicatif est représenté par un Client distinct.

Exemple :

```text
ComLabs Labo DEV

ComLabs Labo PREPROD

ComLabs Labo PROD
```

Ces trois environnements sont considérés comme trois Clients indépendants.

---

## Règle 3

Chaque Client possède son propre cycle de vie.

L'activation, la suspension ou la désactivation d'un Client n'affecte pas les autres Clients.

---

## Règle 4

L'enregistrement d'un Client est réalisé par un administrateur autorisé.

Le développement d'une application et son enregistrement dans ComLabs IAM sont deux processus distincts.

---

## Règle 5

Le domaine Client représente une relation de confiance.

L'existence d'une application ne suffit pas.

Seules les applications explicitement enregistrées sont reconnues par ComLabs IAM.

---

# Gouvernance

Le développement d'une application relève de l'équipe de développement.

L'enregistrement d'un Client dans ComLabs IAM relève de l'administration de l'IAM.

Cette séparation garantit que seules les applications approuvées peuvent utiliser les services de ComLabs IAM.

---

# Exemple

Le directeur demande la création d'une nouvelle application nommée **ComLabs Planning**.

L'équipe de développement réalise l'application.

Une fois celle-ci validée, un administrateur ComLabs IAM enregistre un nouveau Client.

À partir de ce moment, l'application devient autorisée à utiliser les services proposés par ComLabs IAM.

---

# Principes

## Le Client représente une application de confiance

Le domaine Client ne représente pas l'application elle-même.

Il représente la relation de confiance entre cette application et ComLabs IAM.

---

## Les applications sont indépendantes

Chaque application possède son propre Client.

Les environnements de développement, de préproduction et de production sont considérés comme des Clients distincts.

---

## Les Clients sont administrés

L'enregistrement, l'activation et la désactivation d'un Client relèvent exclusivement de l'administration de ComLabs IAM.

---

## Les Clients ne prennent aucune décision de sécurité

Les règles de sécurité appartiennent exclusivement au domaine Security Policy.

Le Client applique ces règles sans les définir.

---

# Décisions prises

- Un Client représente une application de confiance enregistrée dans ComLabs IAM.
- Une application doit être enregistrée avant d'utiliser les services de ComLabs IAM.
- Les environnements DEV, PREPROD et PROD sont représentés par des Clients distincts.
- L'enregistrement d'un Client est une responsabilité de l'administration IAM.
- Le domaine Client ne contient aucune règle de sécurité.

---

# Évolutions prévues

Les futures versions pourront enrichir le domaine Client avec des informations complémentaires, notamment :

- classification des applications ;
- informations de contact ;
- propriétaire métier ;
- propriétaire technique ;
- historique des changements ;
- métadonnées applicatives.

Ces évolutions devront respecter les principes définis par le présent domaine.

---

# Conclusion

Le domaine **Client** constitue le point d'entrée des applications dans l'écosystème ComLabs IAM.

Il représente une application de confiance autorisée à consommer les services proposés par le moteur d'identité.

En séparant clairement le développement des applications de leur enregistrement dans ComLabs IAM, le domaine Client garantit une administration maîtrisée, une sécurité homogène et une architecture évolutive.