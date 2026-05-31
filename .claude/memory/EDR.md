# EDR.md — Registre des Décisions Architecturales

> Format : ID · Date · Contexte · Problème · Décision · Alternatives rejetées · Conséquences

---

## EDR-001 — Framework frontend

- **Date** : 2026-05-31
- **Contexte** : App existante = monofichier vanilla JS. Besoin de migrer vers une architecture maintenable et scalable. Projet potentiellement commercialisable à terme.
- **Problème** : Quel framework choisir pour garantir évolutivité, lisibilité du code, et recrutement futur ?
- **Décision** : **React (Vite)**
- **Alternatives rejetées** :
  - Svelte : plus léger, mais écosystème plus petit, moins adapté si recrutement futur
  - Vanilla JS modulaire : zéro dépendance, mais pas de réactivité, difficile à scale
- **Conséquences** : Nécessite Node.js pour développer. Courbe d'apprentissage initiale. Standard industrie → recrutement facilité.

---

## EDR-002 — Base de données

- **Date** : 2026-05-31
- **Contexte** : Données actuellement en localStorage (éphémère, mono-device, non partageable). Raphael utilise déjà Firebase sur 2 autres projets Neora.
- **Problème** : Comment rendre les données durables, partageables et multi-session ?
- **Décision** : **Firebase Firestore**
- **Alternatives rejetées** :
  - Supabase (PostgreSQL) : meilleure structure relationnelle, mais crée un compte supplémentaire
  - Backend custom Node.js : contrôle total, mais délai de mise en place important
- **Conséquences** : Centralisation de l'infra Neora sur Firebase. Structure NoSQL à anticiper dans le modèle de données.

---

## EDR-003 — Structure des fichiers

- **Date** : 2026-05-31
- **Contexte** : Migration depuis un monofichier. Besoin d'une structure qui reflète les domaines métier et facilite l'évolution feature par feature.
- **Problème** : Comment organiser le code pour qu'il reste lisible et maintenable à mesure que le projet grandit ?
- **Décision** : **Feature-based** (`src/features/lots`, `pricing`, `negotiation`, `settings`, `dashboard`)
- **Alternatives rejetées** :
  - Structure par type (`components/`, `pages/`, `utils/`) : plus simple au départ mais difficile à naviguer quand le projet grandit
- **Conséquences** : Chaque feature est autonome. Ajouter une feature = ajouter un dossier. Logique métier dans `logic.js`, jamais dans les composants UI.

---

## EDR-004 — Langue du code

- **Date** : 2026-05-31
- **Contexte** : App actuelle mélange français et anglais dans les noms de variables et classes CSS.
- **Problème** : Quelle langue utiliser pour le code afin de maximiser la cohérence et la lisibilité ?
- **Décision** : **Code en anglais, interface utilisateur en français**
- **Alternatives rejetées** :
  - Tout en français : crée des frictions avec les frameworks, la doc et les conventions
  - Tout en anglais (UI compris) : perd le contexte métier dans l'interface
- **Conséquences** : `LotDashboard`, `PricingTable` dans le code — "Tableau de marge", "Lot actif" dans l'UI.

---

## EDR-005 — Remplacement de localStorage

- **Date** : 2026-05-31
- **Contexte** : Données de lots, territoires, acheteurs et prix de référence stockées en localStorage. Éphémères, non partageables.
- **Problème** : Comment migrer vers une persistence robuste sans tout reconstruire d'un coup ?
- **Décision** : **Migration vers Firebase Firestore** (cohérent avec EDR-002)
- **Alternatives rejetées** : Conserver localStorage en parallèle pendant la migration (risque de désynchronisation)
- **Conséquences** : Toutes les interactions données passent par `src/api/`. Jamais d'appel Firebase direct depuis un composant.
