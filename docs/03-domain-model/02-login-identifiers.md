# Domain Model 002 - Login Identifier

**Status** : Accepted  
**Version** : 2.0  
**Last Update** : 2026-07-06

---

# Objectif

Le domaine **Login Identifier** permet de retrouver une **Identity** lors d'une tentative d'authentification.

Il constitue le point d'entrée du processus d'authentification.

Son objectif est d'identifier une Identity avant toute vérification d'un Credential.

---

# Définition

Un **Login Identifier** est une information unique permettant d'identifier une Identity.

Il ne représente pas une preuve d'identité.

Il représente uniquement un moyen de retrouver une Identity dans ComLabs IAM.

Exemples :

- Username
- Email
- Employee Number
- Phone Number

---

# Responsabilités

Le domaine Login Identifier est responsable de :

- identifier une Identity ;
- garantir l'unicité de chaque identifiant selon son type ;
- permettre la recherche rapide d'une Identity.

---

# Hors responsabilités

Le domaine Login Identifier n'est pas responsable de :

- vérifier un mot de passe ;
- authentifier une Identity ;
- gérer les sessions ;
- appliquer les politiques de sécurité ;
- gérer les permissions.

Ces responsabilités appartiennent à d'autres domaines.

---

# Cycle de vie

Un Login Identifier est créé lors de la création d'une Identity.

Il peut ensuite :

- être modifié ;
- être remplacé ;
- être désactivé.

Une Identity peut conserver plusieurs Login Identifiers au cours de son existence.

---

# Relations

Le domaine Login Identifier collabore principalement avec :

- Identity
- Authentication

Il ne dépend pas des Credentials.

Il ne dépend pas des Sessions.

---

# Règles métier

Chaque Login Identifier appartient à une seule Identity.

Une Identity peut posséder plusieurs Login Identifiers.

Le moteur ComLabs IAM supporte plusieurs types de Login Identifier.

Les règles déterminant quels types sont autorisés pour la connexion appartiennent au domaine **Security Policy**.

Le Login Identifier ne décide jamais s'il peut être utilisé pour authentifier une Identity.

---

# Types de Login Identifier

La première version de ComLabs IAM prévoit les types suivants :

- Username
- Email
- Employee Number
- Phone Number

Le modèle est volontairement extensible afin de permettre l'ajout de nouveaux types sans remettre en cause l'architecture.

---

# Décisions prises

- Le Login Identifier est indépendant de l'Identity.
- Le Login Identifier est indépendant du Credential.
- Une Identity peut posséder plusieurs Login Identifiers.
- Les règles d'utilisation des Login Identifiers sont définies par les Security Policies.
- Le moteur est conçu pour accepter plusieurs types de Login Identifier.

---

# Évolutions prévues

Les futures versions pourront ajouter :

- LDAP Identifier
- Azure Active Directory Identifier
- OpenID Identifier
- Identifiants personnalisés

Ces évolutions devront conserver le même principe : un Login Identifier sert uniquement à retrouver une Identity.

---

# Conclusion

Le domaine Login Identifier constitue la première étape du processus d'authentification.

Il permet de localiser une Identity sans jamais intervenir dans la vérification des Credentials.

Cette séparation garantit un modèle métier flexible, évolutif et indépendant des méthodes d'authentification.ok