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
