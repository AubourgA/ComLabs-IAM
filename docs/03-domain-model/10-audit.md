# Domain Model 010 - Audit

**Status** : Accepted  
**Version** : 1.0  
**Last Update** : 2026-07-10

---

# Objectif

Le domaine **Audit** constitue la mémoire des événements de sécurité survenus dans ComLabs IAM.

Son objectif est de fournir une vision fidèle, chronologique et exploitable de toutes les opérations ayant un impact sur la sécurité du système.

L'Audit permet de comprendre ce qui s'est produit, à quel moment, par qui, depuis quel environnement et avec quel résultat.

---

# Définition

Un **Audit** représente un événement de sécurité enregistré par ComLabs IAM.

Il ne décrit pas le fonctionnement interne du système.

Il décrit les événements significatifs liés à l'identité, à l'authentification, aux Devices, aux Sessions, aux Clients et aux politiques de sécurité.

Chaque événement constitue un fait historique.

Une fois enregistré, il ne peut plus être modifié.

---

# Responsabilités

Le domaine Audit est responsable de :

- enregistrer les événements de sécurité ;
- conserver l'historique des événements ;
- garantir l'intégrité des informations enregistrées ;
- permettre la consultation des événements par les personnes autorisées ;
- fournir les informations nécessaires aux analyses de sécurité ;
- permettre l'archivage des événements anciens.

---

# Hors responsabilités

Le domaine Audit n'est pas responsable de :

- authentifier une Identity ;
- créer une Session ;
- prendre une décision de sécurité ;
- appliquer une Security Policy ;
- détecter automatiquement une fraude ;
- gérer les autorisations des utilisateurs.

Le domaine Audit observe les événements mais ne participe jamais aux décisions du système.

---

# Cycle de vie

Un événement d'audit suit le cycle suivant :

```text
Créé
   │
   ▼
Consultable
   │
   ▼
Archivé
```

Un événement d'audit n'est jamais modifié.

Il conserve son intégrité pendant toute sa durée de vie.

---

# Relations

## Identity

Les événements produits par une Identity sont enregistrés dans l'Audit.

---

## Authentication

Toutes les authentifications significatives peuvent produire un événement.

Exemples :

- connexion réussie ;
- échec d'authentification ;
- verrouillage d'un compte.

---

## Device

Les opérations liées aux Devices peuvent produire des événements.

Exemples :

- nouveau Device détecté ;
- Device reconnu ;
- Device oublié ;
- Device déclaré fiable.

---

## Security Policy

Les décisions importantes prises par Security Policy peuvent être enregistrées.

Exemples :

- accès refusé ;
- MFA exigé ;
- Session refusée ;
- Device refusé.

---

## Authorization

Les décisions d'autorisation peuvent produire des événements.

Exemples :

- accès autorisé ;
- accès refusé.

---

## Session

Toutes les évolutions importantes d'une Session peuvent être enregistrées.

Exemples :

- Session créée ;
- Session expirée ;
- Session révoquée ;
- Session fermée.

---

## Client

Les demandes provenant des Clients peuvent produire des événements.

Exemples :

- demande d'authentification ;
- Client désactivé ;
- tentative d'accès à un Client désactivé.

---

# Règles métier

## Règle 1

Tout événement de sécurité significatif doit pouvoir être audité.

---

## Règle 2

Les succès comme les échecs doivent être enregistrés.

L'analyse des échecs est essentielle pour améliorer la sécurité du système.

---

## Règle 3

Un événement d'audit est immuable.

Une fois enregistré, il ne peut jamais être modifié.

---

## Règle 4

Un événement d'audit n'est jamais supprimé.

Les événements anciens peuvent être archivés mais restent conservés.

---

## Règle 5

L'Audit ne possède aucune connaissance du métier des applications clientes.

Il enregistre uniquement les événements concernant ComLabs IAM.

Les événements métier restent sous la responsabilité des applications.

---

## Règle 6

La consultation des audits est réservée aux utilisateurs autorisés.

Cette autorisation est définie par les règles d'administration de ComLabs IAM.

---

# Gouvernance

Les événements d'audit sont consultables uniquement par les administrateurs disposant des autorisations nécessaires.

Exemples :

- Responsable Informatique ;
- Responsable Sécurité ;
- Auditeur.

La politique de conservation et d'archivage est définie par l'organisation.

---

# Informations enregistrées

Selon le type d'événement, un Audit peut notamment contenir :

- la date et l'heure ;
- l'Identity concernée ;
- le Client concerné ;
- le Device concerné ;
- l'adresse IP (si disponible) ;
- le résultat de l'opération ;
- la raison de l'échec éventuel ;
- les informations nécessaires à l'analyse de sécurité.

La structure exacte dépend de la nature de l'événement.

---

# Exemple

Une Identity tente de se connecter à ComLabs Labo.

Le processus est le suivant :

```text
Identity
      │
      ▼
Authentication
      │
      ▼
Device
      │
      ▼
Security Policy
      │
      ▼
Authorization
      │
      ▼
Session
      │
      ▼
Audit
```

Si la connexion réussit :

```text
authentication.success
device.recognized
authorization.granted
session.created
```

Si la connexion échoue :

```text
authentication.failed
authorization.denied
```

Ces événements sont enregistrés afin de conserver une trace fidèle du comportement du système.

---

# Principes

## Audit est un observateur

Le domaine Audit ne prend aucune décision.

Il observe les événements produits par les autres domaines.

---

## Audit est immuable

Un événement enregistré ne peut jamais être modifié.

Cette propriété garantit l'intégrité des informations.

---

## Audit est indépendant

Le domaine Audit ne possède aucune connaissance du fonctionnement métier des applications clientes.

Il reste exclusivement centré sur les événements de sécurité de ComLabs IAM.

---

## Audit est exploitable

Les informations enregistrées doivent permettre :

- l'analyse des incidents ;
- la recherche d'événements ;
- l'amélioration continue des politiques de sécurité ;
- les contrôles de conformité.

---

# Décisions prises

- Tous les événements de sécurité significatifs sont auditables.
- Les succès comme les échecs sont enregistrés.
- Un événement d'audit est immuable.
- Les événements ne sont jamais supprimés.
- Les événements anciens peuvent être archivés.
- L'Audit ne connaît pas le métier des applications clientes.
- Le domaine Audit est un observateur et ne prend aucune décision.

---

# Évolutions prévues

Les futures versions pourront enrichir le domaine Audit avec :

- catégorisation des événements ;
- recherche avancée ;
- tableaux de bord de sécurité ;
- indicateurs statistiques ;
- détection de comportements anormaux ;
- intégration avec des plateformes de supervision.

Ces évolutions devront respecter les principes définis par le présent domaine.

---

# Conclusion

Le domaine **Audit** constitue la mémoire de ComLabs IAM.

Il enregistre les événements de sécurité produits par les autres domaines afin de garantir la traçabilité, la conformité et l'analyse des activités du système.

En restant totalement indépendant des mécanismes de décision, le domaine Audit respecte le principe de responsabilité unique et complète naturellement l'architecture de ComLabs IAM.