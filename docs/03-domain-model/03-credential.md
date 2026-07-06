# Domain Model 004 - Credential

**Status** : Accepted  
**Version** : 2.0  
**Last Update** : 2026-07-06

---

# Objectif

Le domaine **Credential** représente les moyens utilisés par une Identity pour prouver son identité lors d'une authentification.

Son objectif est de séparer clairement l'identité numérique de la preuve utilisée pour l'authentifier.

---

# Définition

Un **Credential** est un moyen de preuve associé à une Identity.

Il permet à ComLabs IAM de vérifier qu'une Identity est bien celle qu'elle prétend être.

Exemples :

- Password
- Passkey
- OTP
- Certificate
- API Key

---

# Responsabilités

Le domaine Credential est responsable de :

- représenter un moyen d'authentification ;
- être associé à une Identity ;
- permettre la vérification d'une preuve d'identité ;
- pouvoir être renouvelé ou remplacé.

---

# Hors responsabilités

Le domaine Credential n'est pas responsable de :

- retrouver une Identity ;
- décider si une authentification est autorisée ;
- gérer les sessions ;
- gérer les rôles ;
- gérer les permissions ;
- définir les règles de sécurité.

Ces responsabilités appartiennent à d'autres domaines.

---

# Cycle de vie

Un Credential est créé lorsqu'une Identity reçoit un moyen d'authentification.

Dans la première version de ComLabs IAM, le premier Credential sera généralement un mot de passe.

Ce Credential peut ensuite être :

- renouvelé ;
- remplacé ;
- invalidé ;
- archivé.

Un Credential ne doit jamais être considéré comme éternel.

---

# Relations

Credential collabore avec :

- Identity
- Authentication
- Security Policy

Credential est utilisé par Authentication pour vérifier une tentative de connexion.

---

# Règles métier

Une Identity peut posséder plusieurs Credentials.

Un Credential appartient à une seule Identity.

Un Credential peut être actif ou inactif.

Un Credential ne décide jamais de ses propres règles de validité.

Les règles de complexité, d'expiration, de renouvellement ou d'historique appartiennent aux Security Policies.

---

# Password Credential

La première version de ComLabs IAM implémentera le **Password Credential**.

Le mot de passe est considéré comme un type de Credential, et non comme le centre du système.

Le modèle doit rester ouvert à d'autres types de Credentials dans les futures versions.

---

# Historique

Pour le Password Credential, ComLabs IAM devra empêcher la réutilisation des derniers mots de passe.

La règle retenue pour la première version est :

> Les trois derniers mots de passe ne peuvent pas être réutilisés.

Cette règle appartient à la Password Policy.

---

# Décisions prises

- Le mot de passe est un Credential parmi d'autres.
- Une Identity peut posséder plusieurs Credentials.
- La première version implémente uniquement le Password Credential.
- Le changement de mot de passe est piloté par une Policy.
- Les trois derniers mots de passe ne doivent pas être réutilisés.
- Le modèle doit permettre d'ajouter d'autres Credentials plus tard.

---

# Évolutions prévues

Les futures versions pourront ajouter :

- Passkeys ;
- OTP ;
- MFA ;
- certificats ;
- clés API ;
- authentification biométrique ;
- authentification fédérée.

Ces évolutions ne devront pas modifier le concept fondamental de Credential.

---

# Conclusion

Credential est le domaine qui porte les moyens de preuve d'une Identity.

Cette séparation entre Identity, Login Identifier et Credential permet à ComLabs IAM de rester flexible, évolutif et compatible avec plusieurs méthodes d'authentification.