# CONTEXT.md — État Actuel du Projet

> Mis à jour à chaque session.

---

## Priorités actuelles

1. **Sprint 5** : Calcul bid automatique basé sur les offres reçues (Passe 2)
   - `maxBid = revenueOptimisé / (1 + targetMargin)`
   - Affichage dans le dashboard lot : bid suggéré en ILS + USD/EUR
2. **Sprint 6** (après) : Recommendation meilleur acheteur / split optimal (Passe 3)
3. **Décisions ouvertes avant migration React** : CSS (Modules vs Tailwind) · Auth · Hébergement

---

## État de l'app (index.html actuel)

| Feature | Statut |
|---|---|
| Gestion lots (création, statut) | ✅ Opérationnel |
| Dashboard VMR par territoire | ✅ Opérationnel |
| Seuils de rentabilité (ideal/max/extreme) | ✅ Opérationnel |
| Négociation + calcul profit | ✅ Opérationnel |
| Référentiel Smartphones : VMR + grades | ✅ Implémenté (2026-06-01) |
| Section Offres Reçues : tableau par acheteur | ✅ Implémenté (2026-06-01) |
| Multi-devise USD/EUR dans Offres Reçues | ✅ Implémenté (2026-06-10) |
| Tableau offres collapsible + sticky | ✅ Implémenté (2026-06-10) |
| Sélecteur devise lors ajout acheteur | ✅ Implémenté (2026-06-10) |
| Smartgrade HK injecté dans LOT-2026-003 | ✅ Injecté (2026-06-10) |
| Calcul bid depuis offres reçues | ⏳ À faire (Sprint 5) |
| Recommendation meilleur acheteur / split | ⏳ À faire (Sprint 6) |

---

## Lots actifs

| Lot | Type | Statut | Note |
|---|---|---|---|
| LOT-2026-001 | Standard | 💬 Pricing acheteurs | Lot d'origine |
| LOT-2026-002 | Écrans | 💬 Pricing acheteurs | 12 510 écrans LCD/OLED |
| LOT-2026-003 | Standard | 📩 Offres reçues | 964 pcs · Atelva 144 480 € · Smartgrade HK (80+ prix) |

---

## Règle technique critique

**Modifier index.html = script Python binaire uniquement.**
```python
with open('index.html', 'rb') as f: content = f.read()
html = content.decode('utf-8', errors='replace')
# ... modifications ...
with open('index.html', 'wb') as f: f.write(html.encode('utf-8', errors='replace'))
```
Puis valider : `node -e "const fs=require('fs');const vm=require('vm');new vm.Script(fs.readFileSync('index.html','utf8').slice(fs.readFileSync('index.html','utf8').indexOf('<script>')+8,fs.readFileSync('index.html','utf8').lastIndexOf('</script>')));console.log('OK')"`

---

## Stack validée

| Couche | Choix |
|---|---|
| Actuel | Vanilla JS monofichier (index.html) — 4 372 lignes |
| Cible frontend | React (Vite) |
| Cible backend | Firebase Firestore |
| Style | À décider (CSS Modules vs Tailwind) |

---

## Repo GitHub
`https://github.com/RaphaelG-code/trade-desk` — branche `main`
