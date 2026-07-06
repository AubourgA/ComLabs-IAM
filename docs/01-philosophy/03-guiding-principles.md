# Guiding Principles

**Status** : Accepted  
**Version** : 1.0  
**Last Update** : 2026-07-06

---

# Introduction

Ce document définit les règles fondamentales qui guident le développement de ComLabs IAM.

Ces règles sont plus strictes que les principes de conception.

Elles représentent les limites à ne pas franchir.

---

# Règle 1 - ComLabs IAM ne connaît pas le métier des applications clientes

ComLabs IAM ne doit jamais contenir de logique liée à une application métier.

Il ne connaît pas :

- les laboratoires ;
- les prélèvements ;
- les essais ;
- les matériaux ;
- la R&D ;
- la facturation ;
- les clients métier.

Ces données appartiennent aux applications clientes.

---

# Règle 2 - Une Identity ne stocke pas directement les informations d'authentification

Une Identity ne contient pas directement :

- un mot de passe ;
- un token ;
- une session ;
- un rôle applicatif technique.

Ces éléments appartiennent à des concepts séparés.

---

# Règle 3 - Un Login Identifier n'authentifie jamais

Le Login Identifier sert uniquement à retrouver une Identity.

Il ne prouve jamais que l'utilisateur est bien cette Identity.

La preuve est apportée par un Credential.

---

# Règle 4 - Un Credential ne décide pas des règles de sécurité

Un Credential représente un moyen de preuve.

Il ne décide pas :

- de sa durée de validité ;
- de son expiration ;
- de son historique ;
- de sa complexité ;
- de son renouvellement.

Ces règles appartiennent aux Security Policies.

---

# Règle 5 - Les applications clientes ne gèrent jamais les mots de passe

Une application cliente ne doit jamais :

- stocker un mot de passe ;
- vérifier un mot de passe ;
- réinitialiser directement un mot de passe ;
- gérer la politique de mot de passe.

Elle délègue ces responsabilités à ComLabs IAM.

---

# Règle 6 - Les Security Policies sont globales

Par défaut, les Security Policies s'appliquent à toutes les applications clientes.

L'objectif est de garantir une homogénéité des règles de sécurité.

Les exceptions ne seront envisagées que dans une version future.

---

# Règle 7 - Une information possède une seule source officielle

Une information ne doit jamais être dupliquée inutilement.

Chaque donnée importante doit avoir une source de vérité clairement identifiée.

---

# Règle 8 - Les décisions importantes doivent être documentées

Toute décision structurante doit être décrite dans une ADR.

Une décision ne doit jamais exister uniquement dans le code.

---

# Règle 9 - Le modèle métier reste indépendant de la technique

Les documents du Domain Model ne doivent pas dépendre de :

- Symfony ;
- Doctrine ;
- PostgreSQL ;
- JWT ;
- Redis ;
- Docker.

Ces éléments appartiennent à l'architecture technique.

---

# Règle 10 - Le code vient après la conception

Une fonctionnalité ne doit pas être développée avant que son concept métier soit compris et documenté.

Cette règle protège la cohérence du projet.

---

# Conclusion

Ces règles constituent le cadre de conception de ComLabs IAM.

Elles doivent être respectées dans toutes les évolutions futures du produit.