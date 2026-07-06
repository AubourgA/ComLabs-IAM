# Product Scope

**Status** : Accepted
**Version** : 1.0

---

# Objectif

Ce document définit le périmètre fonctionnel de ComLabs IAM.

Il précise ce que le produit prend en charge et ce qui relève des applications clientes.

---

# Ce que ComLabs IAM fait

## Gestion des identités

- création d'identités ;
- modification ;
- désactivation ;
- suppression logique.

---

## Authentification

- login ;
- logout ;
- renouvellement des tokens ;
- vérification des Credentials.

---

## Gestion des Credentials

- mot de passe ;
- futurs Credentials (Passkeys, OTP, etc.).

---

## Gestion des applications clientes

- enregistrement des applications ;
- gestion des Clients ;
- autorisation d'accès.

---

## Gestion des sessions

- ouverture ;
- fermeture ;
- révocation.

---

## Gestion des politiques de sécurité

- Password Policy ;
- Authentication Policy ;
- Session Policy ;
- Lockout Policy ;
- MFA Policy.

---

## Journalisation

- authentifications ;
- erreurs ;
- événements de sécurité ;
- audit.

---

# Ce que ComLabs IAM ne fait pas

ComLabs IAM ne gère pas :

- les clients métier ;
- les laboratoires ;
- les prélèvements ;
- les essais ;
- les matériaux ;
- la R&D ;
- les commandes ;
- la facturation ;
- les ERP ;
- les CRM.

Ces informations appartiennent aux applications clientes.

---

# Principe fondamental

ComLabs IAM fournit les services d'identité.

Les applications clientes fournissent les services métier.