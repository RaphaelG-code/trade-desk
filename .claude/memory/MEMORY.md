# MEMORY.md — Trade Desk Index

> Index principal du système mémoire. Ne contient pas le détail — consulter les fichiers liés.
> Chargé automatiquement à chaque session Claude Code.

---

## 📍 État du projet
→ Voir [CONTEXT.md](CONTEXT.md) pour les priorités, ce qui est en cours, ce qui est en attente.

**En un mot :** App vanilla JS monofichier opérationnelle. Référentiel smartphones refait (VMR + grades). Section "Offres Reçues" ajoutée dans le dashboard lot. Prochaine étape : calcul bid basé sur les offres.

---

## ⚠️ RÈGLES CRITIQUES (lire en premier)
→ Voir [BLOCKERS.md](BLOCKERS.md) pour le détail.

| Règle | Pourquoi |
|---|---|
| **Ne JAMAIS utiliser Edit/Write sur index.html** | Tronque le fichier → app morte. Toujours via script Python binaire. |
| **Valider après chaque modif** : `node -e "new vm.Script(...)"` | Détecte troncature et erreurs de syntaxe immédiatement |
| **Si tronqué** : `git show HEAD:index.html` pour restaurer la fin | Récupération rapide |

---

## 🏗 Décisions d'architecture
→ Voir [EDR.md](EDR.md) pour le détail.

| ID | Sujet | Décision |
|---|---|---|
| EDR-001 | Framework frontend | React (Vite) — migration future |
| EDR-002 | Base de données | Firebase Firestore |
| EDR-003 | Structure fichiers | Feature-based |
| EDR-004 | Langue du code | Anglais / UI français |
| EDR-005 | Remplacement localStorage | Firebase Firestore |

**Décisions ouvertes :** CSS (Modules vs Tailwind) · Auth · Hébergement

---

## 📚 Apprentissages clés
→ Voir [LEARNINGS.md](LEARNINGS.md) pour le détail complet.

| ID | Règle critique |
|---|---|
| **LRN-006** | ⚠️ Ne jamais Edit/Write sur index.html — script Python binaire uniquement |
| **LRN-007** | Dans render(), le lot actif = `c.lot`, pas `lot` |
| **LRN-008** | Clés buyer offers : modèle sans capacité → utiliser `normM()` + `lookupPrice()` |
| **LRN-009** | Wrapper nouvelles sections render() dans try-catch pendant le dev |
| LRN-001 | App = 1 fichier, vanilla JS, 0 dépendance |
| LRN-002 | Sémantique couleur `.g/.a/.o/.r` → à conserver |
| LRN-003 | Domaines métier existants = bons noms de features React |

---

## 🚧 Blockers
→ Voir [BLOCKERS.md](BLOCKERS.md) pour le détail.

| ID | Statut | Sujet |
|---|---|---|
| BLK-001 | ✅ Résolu | Troncature index.html via Edit/Write |

---

## 📋 Dernières itérations
→ Voir [ITERATION_LOG.md](ITERATION_LOG.md) pour le journal complet.

| Date | Réalisé |
|---|---|
| 2026-06-01 | Référentiel smartphones (VMR+grades) · Section Offres Reçues · Lots migrés · Bugs résolus |
| 2026-05-31 | Analyse repo · Décisions archi · CLAUDE.md · Système mémoire |

---

## 🔗 Fichiers du système mémoire
- [EDR.md](EDR.md) — Décisions architecturales
- [LEARNINGS.md](LEARNINGS.md) — Apprentissages (dont règles critiques)
- [BLOCKERS.md](BLOCKERS.md) — Blockers
- [ITERATION_LOG.md](ITERATION_LOG.md) — Journal des sessions
- [CONTEXT.md](CONTEXT.md) — État actuel du projet
