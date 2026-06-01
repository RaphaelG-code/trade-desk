# CONTEXT.md — État Actuel du Projet

> Mis à jour à chaque session.

---

## Priorités actuelles

1. Valider l'affichage Atelva complet dans Offres Reçues (LOT-2026-003)
2. Passe 2 : calcul du bid basé sur les offres reçues (max bid = revenu optimisé ÷ (1 + marge cible))
3. Passe 3 : recommendation meilleur acheteur / split optimal
4. Décisions ouvertes : CSS, Auth, Hébergement (avant migration React)

---

## État de l'app (index.html actuel)

| Feature | Statut |
|---|---|
| Gestion lots (création, statut) | ✅ Opérationnel |
| Dashboard VMR par territoire | ✅ Opérationnel |
| Seuils de rentabilité (ideal/max/extreme) | ✅ Opérationnel |
| Négociation + calcul profit | ✅ Opérationnel |
| Référentiel Smartphones : VMR + grades | ✅ Implémenté (2026-06-01) |
| Section Offres Reçues + bouton + acheteur | ✅ Implémenté (2026-06-01) |
| Atelva pré-rempli dans LOT-2026-003 | ✅ Injecté (clé sans capacité, lookup normalisé) |
| Calcul bid depuis offres reçues | ⏳ À faire (Passe 2) |
| Recommendation meilleur acheteur | ⏳ À faire (Passe 3) |

---

## Lots actifs

| Lot | Type | Statut | Note |
|---|---|---|---|
| LOT-2026-001 | Standard | 💬 Pricing acheteurs | Lot d'origine |
| LOT-2026-002 | Écrans | 💬 Pricing acheteurs | 12 510 écrans LCD/OLED |
| LOT-2026-003 | Standard | 📩 Offre reçue | 964 pcs · Offre Atelva 144 480 EUR |

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
| Actuel | Vanilla JS monofichier (index.html) |
| Cible frontend | React (Vite) |
| Cible backend | Firebase Firestore |
| Style | À décider |

---

## Repo GitHub
`https://github.com/RaphaelG-code/trade-desk` — branche `main`
