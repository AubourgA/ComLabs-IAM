# Domain Model 001 - Identity

**Status** : Accepted  
**Version** : 2.0  
**Last Update** : 2026-07-06

---

# Objectif

Le domaine **Identity** constitue le cœur de ComLabs IAM.

Il représente une identité numérique unique capable d'être reconnue et authentifiée par le système.

Son objectif est de fournir une représentation stable d'un acteur indépendamment des applications qui l'utilisent et des mécanismes d'authentification employés.

---

# Définition

Une **Identity** est la représentation numérique d'un acteur pouvant interagir avec ComLabs IAM.

Une Identity ne représente pas un compte de connexion.

Elle représente une identité persistante pouvant être utilisée par une ou plusieurs applications.

Une Identity peut représenter :

- une personne ;
- une application ;
- un service ;
- un processus automatisé.

---

# Responsabilités

Le domaine Identity est responsable de :

- représenter une identité numérique ;
- garantir l'unicité de cette identité ;
- servir de point de référence aux autres domaines ;
- exister indépendamment des applications clientes.

---

# Hors responsabilités

Le domaine Identity n'est pas responsable de :

- authentifier une identité ;
- gérer les mots de passe ;
- gérer les sessions ;
- gérer les permissions ;
- appliquer les politiques de sécurité.

Ces responsabilités appartiennent à d'autres domaines.

---

# Cycle de vie

Une Identity est créée lors du processus de provisioning.

Une fois créée, elle peut :

- évoluer ;
- être désactivée ;
- être réactivée.

Une Identity n'est jamais recréée pour représenter la même entité.

Son identifiant interne reste stable pendant toute sa durée de vie.

---

# Relations

Le domaine Identity collabore avec :

- Login Identifier
- Credential
- Authentication
- Session
- Authorization
- Client

Il constitue le point central du modèle métier.

---

# Règles métier

Une Identity possède un identifiant interne unique.

Une Identity peut être associée à plusieurs Login Identifiers.

Une Identity peut posséder plusieurs Credentials.

Une Identity peut ouvrir plusieurs Sessions.

Une Identity ne connaît jamais directement les applications métier.

---

# Décisions prises

- Identity est le concept central de ComLabs IAM.
- Une Identity est indépendante des applications clientes.
- Une Identity est indépendante des méthodes d'authentification.
- Une Identity est indépendante des politiques de sécurité.
- Une Identity représente un acteur numérique et non un utilisateur au sens applicatif.

---

# Évolutions prévues

Les futures versions pourront permettre de représenter :

- des comptes de service ;
- des applications clientes ;
- des processus automatisés ;
- des identités fédérées.

Ces évolutions ne devront jamais remettre en cause la définition fondamentale d'une Identity.

---

# Conclusion

Le domaine Identity constitue la pierre angulaire de ComLabs IAM.

Tous les autres domaines gravitent autour de ce concept sans jamais en modifier la responsabilité.

La stabilité de ce domaine garantit la pérennité de l'ensemble de l'architecture.