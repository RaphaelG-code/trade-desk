# CLAUDE.md — Trade Desk

## WHY
Outil interne de Neora Resources pour analyser des lots de matériel télécom/IT, calculer les marges, préparer les offres d'achat et documenter les décisions commerciales. Fait partie d'un écosystème plus large incluant le marketing collateral et les outils de sourcing.

## WHAT

### Aujourd'hui
Single-page app vanilla JS/HTML/CSS (monofichier `index.html`) avec localStorage. Fonctionnalités actives :
- Gestion de lots (création, suivi, statut)
- Dashboard par lot : KPIs, VMR, seuils de rentabilité
- Simulation de négociation (acheteurs, prix, devises ILS/EUR/USD)
- Paramètres : territoires, acheteurs, prix de référence par modèle/grade

### Direction cible
Migration vers une application React modulaire + Firebase (Firestore).
Structure orientée feature. L'app a vocation à devenir un outil professionnel potentiellement commercialisable.

Périmètre étendu du projet :
- Outil de trading desk (core)
- Marketing collateral (présentations, one-pagers, capability decks)
- Base de pricing intelligence (historique des prix, marges, lots)

## HOW

### Stack
- **Frontend** : React (Vite)
- **Backend/DB** : Firebase (Firestore)
- **Style** : CSS Modules ou Tailwind (à décider avant d'initier)
- **Hébergement** : à définir (Firebase Hosting en option naturelle)

### Structure des fichiers
```
src/
  features/
    lots/          ← gestion des lots
    pricing/       ← VMR, seuils, profit table, logique de marge
    negotiation/   ← propositions, acheteurs, prix d'achat
    settings/      ← territoires, acheteurs, référence
    dashboard/     ← vue principale
  shared/          ← composants et utils réutilisables
  api/             ← toute interaction Firebase centralisée ici
archive/           ← fichiers obsolètes datés, jamais supprimés
```

### Conventions
- Code en **anglais**, interface utilisateur en **français**
- Logique métier dans `features/[domain]/logic.js`, jamais dans les composants
- Toute interaction Firebase passe par `api/` — jamais directement depuis un composant
- Nommage : `camelCase` pour les variables/fonctions, `PascalCase` pour les composants React

## RÈGLES

1. **Prix de référence** : jamais modifié sans prix substitutif fourni par Raphael ou décision commune. Zéro modification unilatérale.
2. **Pas de code sans go** : ne jamais coder sans demande explicite ou validation de Raphael.
3. **Toute décision = validation préalable** : technique, stratégique, structurelle, architecturale — présenter les options, attendre le go.
4. **Toujours des alternatives avec tradeoffs** avant toute recommandation.
5. **Documenter dans MEMORY.md** : toute update, décision, blocage ou apprentissage → tracé immédiatement.
6. **Archiver, ne jamais supprimer** : fichier obsolète → `archive/YYYY-MM-DD_nom-fichier`.
7. **Commit systématique** : tout changement validé = commit Git avec message clair.
8. **Jamais de données métier hardcodées** : prix, modèles, territoires viennent de Firestore.
9. **Jamais de suppression Firestore** sans confirmation explicite de Raphael.
10. **Jamais de données commerciales exposées** côté public (marges, prix d'achat).
11. **Début de session** : toujours lire CLAUDE.md + MEMORY.md avant de travailler.

## ARCHITECTURE

### Décisions prises
| Décision | Choix | Raison |
|---|---|---|
| Framework | React (Vite) | Evolutivité, standard industrie, potentiel commercial |
| Base de données | Firebase Firestore | Déjà utilisé sur 2 autres projets Neora |
| Structure | Feature-based | Scalable, aligné avec les domaines métier |
| Langue code | Anglais | Standard technique universel |
| Persistence | Firestore (remplace localStorage) | Données partagées, durables, multi-session |

### Décisions ouvertes (à trancher avant de coder)
- Style : CSS Modules vs Tailwind
- Hébergement : Firebase Hosting vs autre
- Auth : avec ou sans login utilisateur

### À ne pas réinventer
- La sémantique couleur actuelle (g/a/o/r = vert/amber/orange/rouge) est bonne → la conserver
- Les domaines métier existants (lots, pricing, négociation, settings) sont bons → les garder comme features
