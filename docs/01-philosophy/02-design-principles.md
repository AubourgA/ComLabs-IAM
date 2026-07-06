# Design Principles

**Status** : Accepted  
**Version** : 1.0  
**Last Update** : 2026-07-06

---

# Introduction

Ce document définit les grands principes de conception de ComLabs IAM.

Ces principes guident les choix métier, fonctionnels et architecturaux du projet.

Ils doivent être respectés pendant toute la durée de vie du produit.

---

# Principe 1 - Identity First

ComLabs IAM est centré sur le concept d'Identity.

Le système ne gère pas simplement des utilisateurs.

Il gère des identités numériques capables d'accéder à plusieurs applications.

Une Identity peut représenter :

- une personne ;
- une application ;
- un service ;
- un robot ;
- un script automatisé.

---

# Principe 2 - Une identité, plusieurs applications

Une même Identity peut être utilisée par plusieurs applications clientes.

L'utilisateur ne doit pas posséder un compte différent pour chaque application.

ComLabs IAM devient la source centrale d'identité.

---

# Principe 3 - Les applications ne stockent jamais les mots de passe

Aucune application cliente ne doit gérer ou stocker les mots de passe des utilisateurs.

Les applications délèguent l'authentification à ComLabs IAM.

Cette règle améliore la sécurité et évite la duplication des mécanismes d'authentification.

---

# Principe 4 - Séparation des responsabilités

Chaque concept possède une responsabilité claire.

Exemples :

- Identity représente l'identité numérique.
- Login Identifier permet de retrouver une Identity.
- Credential permet de prouver l'identité.
- Security Policy définit les règles de sécurité.
- Session représente une connexion active.
- Client représente une application connectée.

Aucun concept ne doit mélanger plusieurs responsabilités.

---

# Principe 5 - Le mot de passe n'est qu'un Credential

Le mot de passe n'est pas le centre du système.

Il est uniquement un type de Credential parmi d'autres.

ComLabs IAM doit pouvoir évoluer vers :

- Passkeys ;
- OTP ;
- certificats ;
- clés API ;
- MFA ;
- autres mécanismes futurs.

---

# Principe 6 - Policy Driven

Le comportement de sécurité de ComLabs IAM est piloté par des Security Policies.

Les règles ne doivent pas être codées directement dans les domaines métier.

Les politiques permettent de faire évoluer les règles de sécurité sans remettre en cause l'architecture.

---

# Principe 7 - DDD First

ComLabs IAM est conçu en partant du modèle métier.

Avant d'écrire du code, les concepts sont définis dans la documentation.

Le code est une conséquence du modèle métier.

---

# Principe 8 - Documentation First

Toute décision importante doit être documentée.

La documentation fait partie du produit.

Elle doit permettre de comprendre :

- pourquoi le projet existe ;
- comment il est conçu ;
- pourquoi certaines décisions ont été prises ;
- comment il doit évoluer.

---

# Principe 9 - Réutilisabilité

ComLabs IAM doit pouvoir être utilisé par plusieurs applications.

Il ne doit pas être conçu uniquement pour une application spécifique.

Toute dépendance au métier d'une application cliente doit être évitée.

---

# Principe 10 - Évolutivité

Le système doit être conçu pour évoluer progressivement.

Les futures versions pourront ajouter :

- OpenID Connect ;
- MFA ;
- Passkeys ;
- gestion avancée des sessions ;
- fédération d'identité ;
- audit avancé.

Ces évolutions ne doivent pas remettre en cause le cœur du modèle métier.

---

# Conclusion

Ces principes constituent la base de conception de ComLabs IAM.

Ils doivent guider toutes les décisions futures.

En cas de doute, une décision doit toujours être évaluée par rapport à ces principes.