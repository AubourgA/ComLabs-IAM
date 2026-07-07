# Domain Model 003 - Authentication

**Status** : Accepted  
**Version** : 2.0  
**Last Update** : 2026-07-06

---

# Objectif

Le domaine **Authentication** est responsable de vérifier qu'une Identity est bien celle qu'elle prétend être.

Il orchestre le processus d'authentification en utilisant les différents domaines de ComLabs IAM.

Authentication constitue le point d'entrée principal de toute demande de connexion.

---

# Définition

L'authentification est le processus permettant de vérifier l'identité d'un acteur avant de lui accorder un accès.

Ce processus repose sur plusieurs concepts du domaine :

- Login Identifier
- Credential
- Security Policy
- Identity

Authentication ne représente pas une donnée.

Il représente un processus métier.

---

# Responsabilités

Le domaine Authentication est responsable de :

- recevoir une demande d'authentification ;
- retrouver l'Identity concernée ;
- vérifier le Credential présenté ;
- appliquer les Security Policies ;
- décider si l'authentification est acceptée ou refusée ;
- déclencher l'ouverture d'une Session en cas de succès.

---

# Hors responsabilités

Le domaine Authentication n'est pas responsable de :

- stocker les Credentials ;
- gérer les Login Identifiers ;
- créer une Identity ;
- gérer les permissions ;
- gérer les rôles ;
- conserver les Sessions.

Ces responsabilités appartiennent à d'autres domaines.

---

# Cycle de vie

Une authentification débute lorsqu'un acteur tente d'accéder à une application cliente.

Le processus suit les étapes suivantes :

1. réception de la demande ;
2. recherche de l'Identity grâce au Login Identifier ;
3. récupération du Credential associé ;
4. application des Security Policies ;
5. validation ou refus de l'authentification ;
6. création d'une Session si l'authentification est validée.

Le processus se termine immédiatement après la décision.

Authentication ne conserve aucun état permanent.

---

# Relations

Authentication collabore avec :

- Identity
- Login Identifier
- Credential
- Security Policy
- Session

Authentication constitue le point de coordination entre ces domaines.

---

# Règles métier

Une Identity ne peut être authentifiée que si :

- elle existe ;
- elle est active ;
- un Login Identifier valide est présenté ;
- un Credential valide est fourni ;
- les Security Policies sont respectées.

En cas d'échec, aucune Session n'est créée.

---

# Processus métier

```mermaid
flowchart LR

A[Login Identifier]
B[Identity]
C[Credential]
D[Security Policy]
E[Authentication]
F[Session]

A --> E
E --> B
B --> C
E --> D
E --> F
```

---

# Décisions prises

- Authentication est un processus métier.
- Authentication ne possède aucun état permanent.
- Authentication orchestre plusieurs domaines.
- Authentication applique les Security Policies.
- Authentication décide de la création d'une Session.

---

# Évolutions prévues

Les futures versions pourront intégrer :

- authentification multifacteur ;
- Passkeys ;
- WebAuthn ;
- authentification fédérée ;
- OpenID Connect ;
- OAuth2.

Ces évolutions devront conserver le même principe : Authentication reste le coordinateur du processus.

---

# Conclusion

Authentication constitue le cœur opérationnel de ComLabs IAM.

Il relie les différents domaines sans en prendre la responsabilité.

Cette approche garantit une architecture modulaire dans laquelle chaque domaine conserve une responsabilité clairement définie.