# Domain Model 005 - Security Policy

**Status** : Accepted  
**Version** : 2.1  
**Last Update** : 2026-07-07

---

# Objectif

Le domaine **Security Policy** définit les règles de sécurité applicables à l'ensemble de ComLabs IAM.

Il permet de centraliser les comportements de sécurité afin de garantir une politique homogène pour toutes les applications utilisant le moteur IAM.

L'objectif est de séparer les règles de sécurité de leur implémentation.

---

# Définition

Une **Security Policy** représente un ensemble cohérent de règles métier qui déterminent le comportement de sécurité de ComLabs IAM.

Une Security Policy ne réalise aucune action.

Elle décrit les règles que les autres domaines doivent appliquer.

---

# Responsabilités

Le domaine Security Policy est responsable de :

- définir les règles de sécurité du système ;
- centraliser les exigences de sécurité ;
- garantir un comportement homogène pour toutes les applications ;
- permettre l'évolution des règles sans modifier le modèle métier.
- définir les règles de sécurité applicables aux Sessions et aux Devices ;

---

# Hors responsabilités

Le domaine Security Policy n'est pas responsable de :

- authentifier une Identity ;
- créer une Session ;
- gérer les Login Identifiers ;
- stocker les Credentials ;
- gérer les Permissions.

Ces responsabilités appartiennent aux autres domaines.

---

# Cycle de vie

Une Security Policy est définie par les administrateurs de ComLabs IAM.

Lorsqu'une nouvelle version est validée, elle devient la politique active.

Les nouvelles opérations utilisent immédiatement cette version.

Les opérations déjà en cours poursuivent leur cycle normal, sauf si une politique impose explicitement leur interruption.

---

# Relations

Le domaine Security Policy collabore avec :

- Authentication
- Credential
- Session
- Device
- Identity

Ces domaines appliquent les règles définies par la Security Policy.

La Security Policy ne dépend d'aucun d'eux.

---

# Règles métier

Une seule politique de sécurité est active à un instant donné.

Cette politique est commune à toutes les applications utilisant ComLabs IAM.

Les règles sont définies une seule fois afin de garantir une sécurité homogène dans toute l'organisation.

Les politiques sont indépendantes les unes des autres.

Une modification d'une politique ne doit pas remettre en cause les autres.

---

# Gouvernance

Les Security Policies sont administrées par des utilisateurs disposant des autorisations nécessaires.

Dans la plupart des organisations, cette responsabilité revient au responsable informatique.

La validation interne des changements relève de l'organisation de chaque entreprise et ne fait pas partie du modèle métier.

---

# Les politiques spécialisées

Le domaine Security Policy constitue le point d'entrée des différentes politiques spécialisées.

La première version prévoit notamment :

- Password Policy
- Authentication Policy
- Session Policy
- Lockout Policy
- Multi-Factor Authentication Policy

Chaque politique possède une responsabilité unique.

---
# Gestion des Sessions et des Devices

Le domaine **Security Policy** définit les règles qui gouvernent la création, le maintien et la révocation des Sessions.

Le domaine **Session** applique ces décisions mais ne les prend jamais.

De la même manière, le domaine **Security Policy** exploite les informations fournies par le domaine **Device** afin de déterminer si une connexion est autorisée.

Cette séparation garantit une responsabilité claire entre les domaines.

## Exemples de règles

Une Security Policy peut notamment définir :

- le nombre maximal de Sessions simultanées ;
- le nombre maximal de Devices autorisés ;
- la durée de vie maximale d'une Session ;
- le délai d'expiration par inactivité ;
- l'activation du Remember Me ;
- les règles applicables aux Devices de confiance ;
- le comportement lors d'une connexion depuis un nouveau Device ;
- l'obligation d'une authentification multifacteur (MFA) ;
- la fermeture automatique des Sessions lors d'un changement de mot de passe ;
- la fermeture automatique des Sessions lors de la désactivation d'une Identity.

Le domaine Session applique ces décisions sans jamais les définir.

---
# Principes

## Les règles sont centralisées

Toutes les règles de sécurité sont définies dans ComLabs IAM.

Les applications clientes ne doivent jamais implémenter leurs propres règles d'authentification.

Cette séparation permet de modifier les politiques de sécurité sans impacter le fonctionnement interne des domaines métier.

---

## Les règles sont configurables

Le comportement du moteur est piloté par les politiques de sécurité.

Les domaines métier appliquent les politiques actives sans connaître leur mode de configuration.

---

## Les règles sont indépendantes

Chaque politique traite un sujet unique.

Cette séparation facilite les évolutions et limite les impacts lors des modifications.

---

## Les règles sont évolutives

De nouvelles politiques pourront être ajoutées sans remettre en cause les concepts existants.

Le moteur est conçu pour accompagner l'évolution des besoins de sécurité.

---

# Décisions prises

- Les règles de sécurité sont centralisées.
- Une seule politique globale est active pour toute l'organisation.
- Les applications clientes appliquent les politiques définies par ComLabs IAM.
- Les politiques spécialisées sont indépendantes.
- Les domaines métier ne définissent jamais leurs propres règles de sécurité.
- Toutes les contraintes liées aux Sessions et aux Devices sont pilotées par Security Policy.
- Le moteur adopte une architecture orientée Policy Driven.

---

# Évolutions prévues


Les futures versions pourront intégrer de nouvelles politiques, notamment :

- Session Policy (extensions)
- Risk Policy
- Geolocation Policy
- Trusted Network Policy
- Adaptive Authentication Policy

Ces évolutions devront respecter les principes définis par le domaine Security Policy.

---

# Conclusion

Le domaine Security Policy constitue le référentiel de sécurité de ComLabs IAM.

Il définit les règles qui gouvernent le comportement du moteur sans intervenir directement dans les processus d'authentification ou d'autorisation.

Cette séparation permet de construire un système cohérent, évolutif et facilement maintenable.