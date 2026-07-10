# Domain Model 009 - Device

**Status** : Accepted  
**Version** : 1.0  
**Last Update** : 2026-07-10

---

# Objectif

Le domaine **Device** représente un environnement de connexion utilisé par une **Identity** pour accéder à ComLabs IAM.

Son objectif est de fournir les informations nécessaires à l'évaluation des politiques de sécurité lors d'une authentification.

Le domaine Device ne prend aucune décision de sécurité.

Il décrit uniquement le contexte dans lequel une connexion est réalisée.

---

# Définition

Un **Device** représente un environnement de connexion connu par ComLabs IAM.

Il ne représente pas nécessairement un ordinateur, un téléphone ou un navigateur.

Il représente un environnement permettant à une Identity d'établir une connexion avec ComLabs IAM.

Un Device est associé à une Identity et peut être utilisé lors de plusieurs Sessions successives.

---

# Responsabilités

Le domaine Device est responsable de :

- représenter un environnement de connexion ;
- maintenir les informations connues sur un Device ;
- déterminer si un Device est connu ou inconnu ;
- indiquer si un Device est considéré comme fiable ;
- fournir les informations nécessaires au domaine Security Policy ;
- conserver l'historique des environnements de connexion d'une Identity.

---

# Hors responsabilités

Le domaine Device n'est pas responsable de :

- authentifier une Identity ;
- créer une Session ;
- décider si une connexion est autorisée ;
- imposer une authentification multifacteur (MFA) ;
- limiter le nombre de Devices autorisés ;
- appliquer les Security Policies.

Toutes ces décisions appartiennent au domaine **Security Policy**.

---

# Cycle de vie

Un Device suit le cycle de vie suivant :

```text
Découvert
    │
    ▼
Connu
    │
    ├──────────────┐
    ▼              ▼
Fiable         Oublié
```

### Découvert

Le Device est détecté pour la première fois.

Son traitement dépend des règles définies par Security Policy.

---

### Connu

Le Device est enregistré dans ComLabs IAM.

Il peut être utilisé lors de futures connexions.

---

### Fiable

Le Device est reconnu comme environnement de confiance.

Les conditions permettant de déclarer un Device fiable sont définies exclusivement par Security Policy.

---

### Oublié

Le Device n'est plus considéré comme connu.

Il ne sera plus reconnu lors des connexions suivantes.

L'historique peut néanmoins être conservé à des fins d'audit.

---

# Relations

## Identity

Une Identity possède un ensemble de Devices connus.

Chaque Device appartient à une seule Identity.

Un même poste de travail utilisé par plusieurs personnes donnera donc naissance à plusieurs Devices, chacun étant associé à une Identity différente.

---

## Authentication

Authentication vérifie l'identité.

Une fois l'identité authentifiée, le domaine Device permet de déterminer dans quel environnement cette authentification est réalisée.

---

## Security Policy

Le domaine Device fournit des informations.

Le domaine Security Policy prend les décisions.

Exemples :

- Device connu ;
- Device inconnu ;
- Device fiable.

À partir de ces informations, Security Policy peut décider :

- d'autoriser la connexion ;
- d'exiger une authentification multifacteur ;
- de refuser la connexion ;
- d'enregistrer un nouveau Device.

---

## Session

Une Session est toujours créée depuis un Device.

Un Device peut être à l'origine de plusieurs Sessions successives.

Le Device existe indépendamment des Sessions.

---

## Audit

Toutes les opérations importantes concernant un Device doivent être enregistrées.

Exemples :

- device.discovered
- device.recognized
- device.trusted
- device.forgotten

---

# Règles métier

## Règle 1

Chaque Device appartient à une seule Identity.

---

## Règle 2

Une Identity peut posséder plusieurs Devices.

Le nombre maximal de Devices autorisés est défini par Security Policy.

---

## Règle 3

Un Device ne prend jamais de décision.

Il fournit uniquement des informations sur l'environnement de connexion.

---

## Règle 4

La reconnaissance d'un Device précède l'évaluation des Security Policies.

Le domaine Device ne fait que décrire le contexte de connexion.

---

## Règle 5

Un Device peut être reconnu comme fiable.

Les critères permettant cette reconnaissance appartiennent exclusivement au domaine Security Policy.

---

## Règle 6

Un Device oublié n'est plus reconnu lors des connexions suivantes.

Il pourra être redécouvert comme un nouveau Device.

---

# Gouvernance

La création, la reconnaissance et l'oubli d'un Device sont pilotés par les politiques de sécurité de ComLabs IAM.

Le domaine Device reste indépendant de ces règles.

Cette séparation garantit une évolution des politiques de sécurité sans modifier le domaine Device.

---

# Exemple

Une Identity s'authentifie avec succès.

Le processus est le suivant :

```text
Identity
      │
      ▼
Authentication
      │
      ▼
Reconnaissance du Device
      │
      ▼
Security Policy
      │
      ▼
Authorization
      │
      ▼
Création de la Session
      │
      ▼
Audit
```

Le domaine Device ne décide jamais si la connexion est autorisée.

Il fournit uniquement les informations nécessaires au domaine Security Policy.

---

# Principes

## Device représente un environnement de connexion

Le domaine Device ne représente pas un équipement physique.

Il représente un environnement de connexion associé à une Identity.

---

## Device ne prend aucune décision

Toutes les décisions sont prises par Security Policy.

Le domaine Device fournit uniquement des informations.

---

## Device est persistant

Un Device existe indépendamment des Sessions.

Une même Identity peut réutiliser le même Device lors de plusieurs connexions successives.

---

## Device est indépendant des technologies

Le domaine Device ne définit pas la manière dont un environnement est identifié.

Cette identification pourra être réalisée par différentes stratégies :

- empreinte de navigateur ;
- identifiant fourni par l'application cliente ;
- certificat machine ;
- agent d'entreprise ;
- toute autre stratégie future.

Le domaine Device reste indépendant de ces choix techniques.

---

# Décisions prises

- Un Device représente un environnement de connexion.
- Un Device appartient à une seule Identity.
- Une Identity peut posséder plusieurs Devices.
- Un Device ne prend jamais de décision de sécurité.
- Les décisions concernant les Devices appartiennent exclusivement à Security Policy.
- Un Device est persistant et indépendant des Sessions.
- La méthode d'identification d'un Device reste indépendante du modèle métier.

---

# Évolutions prévues

Les futures versions pourront enrichir le domaine Device avec :

- classification des Devices ;
- niveau de confiance ;
- historique des connexions ;
- informations de sécurité complémentaires ;
- détection de comportements inhabituels.

Ces évolutions devront respecter les principes définis par le présent domaine.

---

# Conclusion

Le domaine **Device** représente les environnements de connexion connus d'une Identity.

Il constitue une source d'information essentielle pour l'évaluation des politiques de sécurité tout en restant totalement indépendant des mécanismes de décision.

Cette séparation permet à ComLabs IAM de faire évoluer ses stratégies de sécurité sans modifier le modèle métier du domaine Device.