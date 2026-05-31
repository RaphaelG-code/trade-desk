# MEMORY.md — Trade Desk Index

> Index principal du système mémoire. Ne contient pas le détail — consulter les fichiers liés.
> Chargé automatiquement à chaque session Claude Code. Objectif : charger le minimum, consulter à la demande.

---

## 📍 État du projet
→ Voir [CONTEXT.md](CONTEXT.md) pour les priorités, ce qui est en cours, ce qui est en attente.

**En un mot :** Migration d'un monofichier `index.html` (vanilla JS + localStorage) vers React + Firebase.
Stack validée, architecture validée. Aucune ligne de React écrite à ce jour.

---

## 🏗 Décisions d'architecture
→ Voir [EDR.md](EDR.md) pour le détail complet (contexte, alternatives rejetées, conséquences).

| ID | Sujet | Décision |
|---|---|---|
| EDR-001 | Framework frontend | React (Vite) |
| EDR-002 | Base de données | Firebase Firestore |
| EDR-003 | Structure fichiers | Feature-based (`features/lots`, `pricing`, etc.) |
| EDR-004 | Langue du code | Anglais (UI en français) |
| EDR-005 | Remplacement localStorage | Firebase Firestore |

**Décisions ouvertes :** CSS (Modules vs Tailwind) · Auth (oui/non) · Hébergement

---

## 📚 Apprentissages
→ Voir [LEARNINGS.md](LEARNINGS.md) pour le détail.

| ID | Découverte clé |
|---|---|
| LRN-001 | App actuelle = 1 fichier, vanilla JS, 0 dépendance externe sauf Google Fonts |
| LRN-002 | Sémantique couleur `.g/.a/.o/.r` cohérente → à conserver dans React |
| LRN-003 | Domaines métier bien définis dans l'app actuelle → bons noms de features |

---

## 🚧 Blockers
→ Voir [BLOCKERS.md](BLOCKERS.md) pour le détail.

Aucun blocker actif.

---

## 📋 Dernières itérations
→ Voir [ITERATION_LOG.md](ITERATION_LOG.md) pour le journal complet.

| Date | Réalisé |
|---|---|
| 2026-05-31 | Analyse repo · Décisions d'archi · Création CLAUDE.md + système mémoire |

---

## 🔗 Fichiers du système mémoire
- [EDR.md](EDR.md) — Décisions architecturales
- [LEARNINGS.md](LEARNINGS.md) — Apprentissages
- [BLOCKERS.md](BLOCKERS.md) — Blockers
- [ITERATION_LOG.md](ITERATION_LOG.md) — Journal des itérations
- [CONTEXT.md](CONTEXT.md) — État actuel du projet
