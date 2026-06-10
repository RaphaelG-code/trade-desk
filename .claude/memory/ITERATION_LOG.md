# ITERATION_LOG.md — Journal des Itérations

> Format : Date · Objectif · Réalisé · Décisions prises · Prochaine étape

---

## 2026-05-31 — Session fondatrice

- **Objectif** : Analyser l'existant et poser les fondations du projet structuré.
- **Réalisé** :
  - Analyse complète du repo GitHub `RaphaelG-code/trade-desk` (architecture, patterns, features, naming)
  - Décisions d'architecture prises en collaboration (stack, structure, langue, backend)
  - Création de `CLAUDE.md` à la racine du projet
  - Création du système mémoire `.claude/memory/` (6 fichiers)
- **Décisions prises** :
  - Framework : React (Vite)
  - Backend : Firebase Firestore
  - Structure : feature-based
  - Langue code : anglais / UI : français
  - Voir EDR-001 à EDR-005 pour le détail
- **Décisions ouvertes** :
  - CSS : Modules vs Tailwind
  - Auth : oui/non
  - Hébergement : Firebase Hosting vs autre
- **Prochaine étape** : Trancher les décisions ouvertes puis scaffolding du projet React.

---

<!-- Template pour ajout futur :

## YYYY-MM-DD — [Titre de la session]

- **Objectif** : Ce qu'on voulait accomplir.
- **Réalisé** : Ce qui a effectivement été fait.
- **Décisions prises** : Décisions importantes prises pendant la session (avec lien EDR si applicable).
- **Décisions ouvertes** : Ce qui reste à trancher.
- **Prochaine étape** : Action concrète suivante.

-->

---

## 2026-06-01 — Refonte référentiel + section Offres Reçues

- **Objectif** : Ajouter prix par grade dans le référentiel smartphones + section "Offres Reçues" dans le dashboard lot avec colonnes dynamiques par acheteur.
- **Réalisé** :
  - DEFAULT_REF smartphones : `prices:{fr,dxb}` → `vmr:{fr,dxb}` + `prices:{}` (grade market prices)
  - Migration état existant : vmr conversion + buyerOffers sur tous les lots
  - Référentiel Smartphones : nouveau tableau VMR + 8 colonnes grades (A+/A/A'/B+/B/C+/C/Faulty)
  - Section "Offres Reçues" dans dashboard lot : tableau modèle×grade×acheteur, meilleur prix ★, total estimé
  - Bouton "+" pour ajouter acheteur existant ou nouveau
  - Offre Atelva (41 prix A+/B+) injectée dans LOT-2026-003
  - Lots-2026-002 et 003 injectés comme migrations automatiques dans index.html
- **Décisions prises** :
  - Référentiel = VMR + prix marché moyen par grade (PAS les prix par acheteur)
  - Prix par acheteur = dans la page du lot uniquement (éphémères, marché change chaque semaine)
  - Clés buyer offers = `model_gradeKey` avec fallback `model_sans_capacité_gradeKey`
- **Blockers rencontrés** :
  - BLK-001 : troncature répétée de index.html via Edit/Write → réglé par scripts Python binaires
  - LRN-007 : `lot` vs `c.lot` dans render() → réglé par `const lot = c.lot`
  - LRN-008 : mismatch clés avec/sans capacité → réglé par `normM()` + `lookupPrice()`
- **Prochaine étape** : Valider l'affichage Atelva complet → puis Passe 2 (dashboard : calcul bid basé sur offres).

---

## 2026-06-10 — Sprint 4 : Multi-devise + UX Offres Reçues + Smartgrade HK

- **Objectif** : Multi-devise USD/EUR dans les offres acheteurs, injection offre Smartgrade HK, amélioration UX tableau offres.
- **Réalisé** :
  - Multi-devise dans la section Offres Reçues : header affiche €/$ par acheteur, colonne "Meilleur" affiche la bonne devise, totaux par acheteur respectent la devise
  - Correction Smartgrade : devise EUR → USD (Smartgrade opère en USD)
  - Sélecteur devise (EUR/USD) lors de l'ajout d'un acheteur dans Offres Reçues
  - Auto-propagation de la devise lors de la sélection d'un acheteur existant (dropdown)
  - Injection offre Smartgrade HK dans LOT-2026-003 (80+ prix C+/C pour iPhones et Samsung)
  - Tableau offres : ligne "Ajouter acheteur" déplacée en haut de section
  - Tableau offres : collapsible — 5 premières lignes visibles, expand/collapse pour le reste
  - Tableau offres : header sticky (top) + totaux sticky (bottom)
  - Buy price thresholds (Ideal/Max/Extreme) : affichage en $ (USD) au lieu de €
  - Correction `sgIls` : Smartgrade calculé en `sg * S.rUsd` (était `rEur`)
  - Migration initiale : `S.buyers` et `lot.buyerOffers` reçoivent devise par défaut si absente
- **Décisions prises** :
  - Devise stockée par acheteur (dans `buyer`) ET par offre (dans `buyerOffer`)
  - Seuils d'achat affichés en USD (aligné usage réel)
- **Prochaine étape** : Sprint 5 — Calcul bid automatique depuis les offres reçues (Passe 2).
