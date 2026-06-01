# BLOCKERS.md — Registre des Blockers

> Format : ID · Date · Problème · Cause racine · Solution · Temps perdu

---

## BLK-001 — Troncature de index.html par les tools Edit/Write

- **Date** : 2026-06-01
- **Problème** : Après modification via tool Edit/Write, index.html était tronqué — la fin du fichier (renderTop();render(); + balises fermantes) disparaissait. L'app devenait complètement non fonctionnelle.
- **Cause racine** : Encodage UTF-8 des caractères `─` (U+2500) dans le commentaire `// ── INIT ───` en fin de fichier. Le tool Edit écrit en UTF-8 mais la gestion des multi-byte chars tronque le fichier.
- **Solution** : Modifier index.html uniquement via scripts Python (lecture/écriture binaire). Restauration : `git show HEAD:index.html` pour récupérer la fin. Validation post-modif : `node -e "new vm.Script(...)"`.
- **Temps perdu** : ~2h de debugging

---

<!-- Template :

## BLK-00X — [Titre court]

- **Date** : YYYY-MM-DD
- **Problème** : ...
- **Cause racine** : ...
- **Solution** : ...
- **Temps perdu** : ...

-->
