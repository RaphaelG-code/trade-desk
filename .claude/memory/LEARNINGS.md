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

---

## LRN-006 — Ne jamais utiliser le tool Edit sur index.html

- **Date** : 2026-06-01
- **Découverte** : Le tool `Edit` (et `Write`) tronque la fin de `index.html` à cause d'un problème d'encodage UTF-8 sur les caractères `─` (U+2500) du commentaire `// ── INIT ───`. Le fichier est sauvegardé incomplet — sans `renderTop();render();`, `</script>`, `</body>`, `</html>`.
- **Impact** : L'app devient complètement non fonctionnelle (page blanche). Peut arriver silencieusement sans message d'erreur visible.
- **Solution** : Toujours modifier `index.html` via un **script Python** qui lit et écrit en **binaire** (`open(..., 'rb')` / `open(..., 'wb')`). Jamais via Edit/Write de Claude. Après toute modification, valider avec `node -e "new vm.Script(...)"`. Si tronqué : restaurer la fin depuis `git show HEAD:index.html`.
- **Source** : Session 2026-06-01, multiples occurrences de truncation

---

## LRN-007 — Variable `lot` non définie dans render()

- **Date** : 2026-06-01
- **Découverte** : Dans la fonction `render()`, le lot actif s'appelle `c.lot` (retourné par `calc()`), pas `lot`. Utiliser `lot` directement provoque `ReferenceError: lot is not defined`.
- **Impact** : Crash silencieux du dashboard (section offres vide, pas de message sauf dans Console).
- **Solution** : Toujours déclarer `const lot = c.lot;` en début de bloc avant d'utiliser `lot`, ou utiliser `c.lot` directement.
- **Source** : Session 2026-06-01, bug offersHtml

---

## LRN-008 — Mismatch de clés : capacité dans items vs pas dans offres acheteur

- **Date** : 2026-06-01
- **Découverte** : Les items de lot incluent la capacité dans le nom de modèle (ex: `"iPhone 16 Pro Max 256GB"`), mais les offres acheteurs (ex: Atelva) utilisent des noms courts sans capacité (ex: `"iPhone 16 Pro Max"`). La lookup directe par clé ne trouve rien.
- **Impact** : Les prix acheteurs ne s'affichent pas dans le tableau des offres.
- **Solution** : Fonction `normM(m)` = `m.replace(/\s+\d+GB$/i,'').trim()` + `lookupPrice(b,m,g)` qui essaie d'abord la clé complète, puis la clé sans capacité.
- **Source** : Session 2026-06-01, section offresHtml

---

## LRN-009 — Wrap try-catch sur les sections de render() critiques

- **Date** : 2026-06-01
- **Découverte** : Un crash dans une section de `render()` rend le dashboard entièrement vide sans message visible. L'onglet Paramètres continue de fonctionner car il est dans un `if` séparé qui s'exécute avant.
- **Impact** : Debugging très difficile sans Console ouverte.
- **Solution** : Wrapper les nouvelles sections de render() dans `try { ... } catch(e) { console.error(...); fallback=''; }` pendant le développement. Retirer le try-catch une fois la section stabilisée.
- **Source** : Session 2026-06-01
