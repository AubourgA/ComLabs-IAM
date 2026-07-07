# Session

## Objectif

Le domaine **Session** représente un état d'authentification actif entre une **Identity** et ComLabs IAM.

Une session est créée après une authentification réussie et permet à une Identity d'accéder à un ou plusieurs Clients autorisés sans devoir se réauthentifier à chaque requête.

Le domaine Session est responsable de la gestion du cycle de vie d'une connexion authentifiée.

---

## Définition

Une **Session** est un état temporaire attestant qu'une Identity a été authentifiée avec succès.

Une Session est toujours associée à :

- une Identity ;
- un Client ;
- un Device ;
- une date de création ;
- une date d'expiration ;
- un état.

Le domaine Session ne décide jamais si une session est autorisée ou non.

Cette responsabilité appartient au domaine **Security Policy**.

---

## Responsabilités

Le domaine Session est responsable de :

- créer une session après une authentification valide ;
- gérer le cycle de vie d'une session ;
- expirer une session ;
- révoquer une session ;
- fermer une session lors d'une déconnexion ;
- relier une session à une Identity ;
- relier une session à un Client ;
- relier une session à un Device ;
- exposer l'état courant d'une session ;
- émettre les événements destinés au domaine Audit.

---

## Ce que le domaine Session ne fait pas

Le domaine Session n'est pas responsable de :

- vérifier les identifiants de connexion ;
- décider si une authentification est valide ;
- déterminer le nombre maximal de Sessions autorisées ;
- déterminer le nombre maximal de Devices autorisés ;
- décider si un Device est de confiance ;
- imposer une authentification multifacteur (MFA) ;
- gérer le Remember Me ;
- définir la durée de vie d'une Session ;
- définir les règles d'expiration pour inactivité.

Toutes ces règles sont définies par le domaine **Security Policy**.

---

## Cycle de vie

Une Session suit l'un des cycles suivants :

```text
Créée
   │
   ▼
Active
   │
   ├──────────────┐
   ▼              ▼
Expirée      Révoquée
   │              │
   └──────┬───────┘
          ▼
       Fermée
```

---

## États d'une Session

| État | Description |
|------|-------------|
| **Active** | La session est valide et peut être utilisée. |
| **Expirée** | La durée de vie ou le délai d'inactivité est dépassé. |
| **Révoquée** | La session a été invalidée avant son expiration. |
| **Fermée** | La session a été clôturée suite à une déconnexion normale. |

Une Session expirée ou révoquée ne peut jamais redevenir active.

---

## Relations

### Identity

Une Identity peut posséder une ou plusieurs Sessions selon les règles définies par **Security Policy**.

Le domaine Session est capable de gérer plusieurs Sessions simultanées mais ne décide jamais si cela est autorisé.

---

### Client

Une Session est toujours créée pour un Client.

Exemples :

- ComLabs Labo
- ComLabs Sampling
- ComLabs R&D
- ComLabs Materials

---

### Device

Une Session est toujours créée depuis un Device.

Le Device représente l'environnement utilisé pour se connecter.

Exemples :

- poste de travail ;
- navigateur ;
- téléphone ;
- tablette ;
- terminal d'entreprise.

Le domaine Session connaît le Device utilisé mais ne définit jamais la manière dont celui-ci est identifié.

Cette responsabilité appartient au domaine **Device**.

---

### Security Policy

Le domaine Security Policy décide si une Session peut être :

- créée ;
- renouvelée ;
- maintenue ;
- révoquée.

Exemples de règles :

- nombre maximal de Sessions ;
- nombre maximal de Devices ;
- durée de vie d'une Session ;
- expiration par inactivité ;
- Remember Me ;
- durée de confiance d'un Device ;
- MFA obligatoire ;
- fermeture des Sessions après changement de mot de passe.

Le domaine Session applique ces décisions sans les définir.

---

### Authentication

Le processus est le suivant :

```text
Authentication
        │
        ▼
Security Policy
        │
        ▼
Création de la Session
        │
        ▼
Audit
```

Authentication vérifie l'identité.

Security Policy décide si une Session peut être créée.

Session représente ensuite l'état d'authentification.

---

### Audit

Tous les événements importants concernant une Session doivent être enregistrés.

Exemples :

- session.created
- session.expired
- session.revoked
- session.closed
- session.replaced
- session.rejected_by_policy

---

## Règles métier

### Règle 1

Une Session appartient toujours à une seule Identity.

### Règle 2

Une Session appartient toujours à un seul Client.

### Règle 3

Une Session est toujours associée à un Device.

### Règle 4

Une Session expirée ne peut jamais redevenir active.

Une nouvelle authentification est nécessaire.

### Règle 5

Une Session révoquée ne peut jamais être réactivée.

### Règle 6

Toutes les limitations concernant les Sessions sont définies par **Security Policy**.

### Règle 7

Chaque changement d'état significatif doit produire un événement d'audit.

---

## Exemple

Un utilisateur se connecte à ComLabs Labo depuis son poste de travail.

Authentication valide son identité.

Security Policy vérifie :

- si le compte est actif ;
- si le Device est autorisé ;
- si le nombre maximal de Sessions est respecté ;
- si une authentification multifacteur est nécessaire.

Si toutes les règles sont satisfaites, une Session est créée.

Cette Session est liée :

- à l'Identity ;
- au Client ;
- au Device.

Enfin, un événement `session.created` est enregistré dans Audit.

---

## Décision de conception

Le domaine **Session** est volontairement simple.

Il représente une connexion authentifiée et gère uniquement son cycle de vie.

Toutes les règles de sécurité concernant les Sessions appartiennent exclusivement au domaine **Security Policy**.

Cette séparation garantit un modèle métier clair, flexible et évolutif.