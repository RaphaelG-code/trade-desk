# CONTEXT.md — État Actuel du Projet

> Mis à jour à chaque session. Source de vérité sur où en est le projet maintenant.

---

## Priorités actuelles

1. Trancher les décisions ouvertes (CSS, Auth, Hébergement)
2. Scaffolding du projet React + Firebase
3. Migration feature par feature depuis `index.html`

---

## En cours

- Rien de codé à ce jour — phase de structuration et décisions d'architecture

---

## En attente (décisions à prendre avant d'agir)

| Sujet | Options | Bloque quoi |
|---|---|---|
| CSS | Modules vs Tailwind | Scaffolding React |
| Auth | Oui (Firebase Auth) vs Non | Architecture Firestore |
| Hébergement | Firebase Hosting vs autre | Déploiement |

---

## Équipe / Rôles

| Personne | Rôle |
|---|---|
| Raphael | Product owner, décideur, utilisateur final |
| Claude | Développeur, architecte, documentaliste |

---

## Stack validée

| Couche | Choix |
|---|---|
| Frontend | React (Vite) |
| Backend / DB | Firebase Firestore |
| Style | À décider |
| Hébergement | À décider |

---

## Repo GitHub

`https://github.com/RaphaelG-code/trade-desk`
Branche principale : `main`
État actuel du repo : monofichier `index.html` (app vanilla JS originale)

---

## Périmètre du projet (rappel)

- **Core** : Trading desk (lots, pricing, négociation, settings)
- **Secondaire** : Marketing collateral (présentations, one-pagers)
- **Long terme** : Base de pricing intelligence (historique des prix, marges)
