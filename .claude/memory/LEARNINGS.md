# LEARNINGS.md — Registre des Apprentissages

> Format : ID · Date · Découverte · Impact · Source

---

## LRN-001 — Architecture actuelle : monofichier total

- **Date** : 2026-05-31
- **Découverte** : L'app entière tient dans un seul `index.html` (~620 lignes). HTML, CSS inline (`<style>`), JS inline (`<script>`). Aucun fichier séparé, aucune dépendance npm, aucun build.
- **Impact** : Migration vers React = repartir d'une base propre plutôt que refactoriser progressivement. Le comportement et la logique de l'app actuelle servent de spec fonctionnelle.
- **Source** : Analyse directe du repo GitHub `RaphaelG-code/trade-desk`

---

## LRN-002 — Sémantique couleur cohérente et réutilisable

- **Date** : 2026-05-31
- **Découverte** : Le système de couleurs sémantiques actuel (`.g` = vert/bon, `.a` = amber/attention, `.o` = orange/warning, `.r` = rouge/danger, `.n` = neutre) est cohérent et bien appliqué dans toute l'app (cards, badges, banners, texte).
- **Impact** : Ce système est à conserver tel quel dans React sous forme de classes CSS utilitaires ou variables. Ne pas réinventer.
- **Source** : Analyse CSS inline de `index.html`

---

## LRN-003 — Domaines métier bien identifiés dans l'app existante

- **Date** : 2026-05-31
- **Découverte** : L'app actuelle organise naturellement ses fonctionnalités autour de 5 domaines : lots, pricing (VMR, thresholds, profit table), negotiation (proposals, buy price), settings (territories, buyers, reference prices), dashboard.
- **Impact** : Ces domaines deviennent directement les features dans la structure React. Pas besoin de réfléchir à la découpe — elle existe déjà dans l'app actuelle.
- **Source** : Analyse HTML/JS de `index.html`

---

## LRN-004 — Données de référence actuellement hardcodées

- **Date** : 2026-05-31
- **Découverte** : `DEFAULT_TERRITORIES`, `DEFAULT_BUYERS`, `DEFAULT_REF` sont des constantes JS directement dans le fichier. Les prix de référence incluent des prix par fournisseur (`sg_A`, `bb_B`, `fnc_B`, `ty_A`…) et par grade (A/B/C/D).
- **Impact** : Ces données doivent migrer vers Firestore. La structure des objets existants est un bon point de départ pour le schéma de base de données.
- **Source** : Analyse JS de `index.html`

---

## LRN-005 — Rendu entièrement dynamique via innerHTML

- **Date** : 2026-05-31
- **Découverte** : Toute l'UI est reconstruite via `innerHTML` sur `#main` à chaque changement d'onglet. Pas de composants, pas de state management — tout est re-rendu à chaque fois.
- **Impact** : En React, ce pattern devient du state + composants réactifs. La logique de rendu actuelle = spec pour les composants à construire.
- **Source** : Analyse JS de `index.html`
