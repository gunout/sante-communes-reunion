# 🇫🇷 Santé Financière Communale — La Réunion

> **Analyse interactive des comptes des 24 communes de La Réunion (2000-2025)**

[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Live-brightgreen?style=for-the-badge&logo=github)](https://gunout.github.io/sante-communes-reunion/)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)](https://developer.mozilla.org/fr/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)](https://developer.mozilla.org/fr/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/fr/docs/Web/JavaScript)
[![Chart.js](https://img.shields.io/badge/Chart.js-FF6384?style=for-the-badge&logo=chart.js&logoColor=white)](https://www.chartjs.org/)
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![License MIT](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](LICENSE)
[![Données DGFiP](https://img.shields.io/badge/Donn%C3%A9es-DGFiP%20%2B%20OFGL-blue?style=for-the-badge)](https://www.data.economie.gouv.fr/)

---

## 📊 Aperçu

Cette application web présente une **analyse financière complète** des 24 communes de La Réunion sur la période **2000-2025**, à partir de données officielles de la DGFiP et de l'OFGL.

### Fonctionnalités principales

- 🏛️ **Analyse par commune** : cartes de stats, 5 graphiques interactifs, insights automatiques, tableau détaillé
- 📊 **Comparaison multi-communes** : radar comparatif (2-3 communes), carte heatmap, tableau triable
- 📥 **Export CSV** des données comparatives
- 🇫🇷 **Charte graphique** bleu-blanc-rouge

### Aperçu de l'interface

| Accueil par commune | Comparaison |
|---|---|
| Sélecteur, stats, graphiques, insights | Radar, carte, tableau triable |

---

## 🚀 Accès à l'application

**Lien direct** : [https://gunout.github.io/sante-communes-reunion/](https://gunout.github.io/sante-communes-reunion/)

Ou en local :
```bash
git clone https://github.com/gunout/sante-communes-reunion.git
cd sante-communes-reunion
python3 -m http.server 8009
```
Puis ouvrir **http://localhost:8009/**

---

## 📁 Structure du projet

```
sante-communes-reunion/
├── index.html                              # Application complète (SPA)
├── processed/
│   └── reunion_24_communes_data_complet.json   # Données consolidées 2000-2025
├── LICENSE
└── README.md
```

---

## 📊 Données

### Sources officielles

| Source | Période | Contenu |
|---|---|---|
| **DGFiP** (miroir cquest) | 2000-2018 | Comptes individuels des communes |
| **OFGL** (data.ofgl.fr) | 2018-2025 | Comptes consolidés des communes |

### Couverture

- **24 communes** de La Réunion (codes INSEE 97401 à 97424)
- **26 années** (2000 à 2025)
- **624 enregistrements** au total

### Indicateurs disponibles

| Indicateur | Description |
|---|---|
| `population` | Population municipale |
| `recettes_fonctionnement` | Recettes réelles de fonctionnement |
| `depenses_fonctionnement` | Dépenses réelles de fonctionnement |
| `impots_locaux` | Produits des impôts et taxes |
| `dotations_etat` | Dotation Globale de Fonctionnement |
| `personnel` | Charges de personnel |
| `achats` | Achats et charges externes |
| `investissement` | Dépenses d'équipement |
| `dette` | Encours de dette |
| `epargne_brute` | Épargne brute (excédent) |

### Structure du JSON

```json
{
  "meta": {
    "source": "DGFiP + OFGL",
    "departement": "La Réunion (974)",
    "nb_communes": 24,
    "periode": "2000-2025",
    "total_enregistrements": 624,
    "unite": "euros"
  },
  "communes": {
    "97408": {
      "code_insee": "97408",
      "nom": "La Possession",
      "donnees": [
        {
          "annee": 2000,
          "population": 22014,
          "recettes_fonctionnement": 17759000,
          "depenses_fonctionnement": 16107000,
          "dette": 14510000
        }
      ]
    }
  }
}
```

---

## 🛠️ Technologies

| Technologie | Usage |
|---|---|
| **HTML5** | Structure |
| **CSS3** | Design responsive bleu-blanc-rouge |
| **JavaScript (ES5)** | Logique applicative |
| **Chart.js 4.4** | Graphiques interactifs |
| **Python 3** | Traitement des données brutes |

---

## 🔄 Régénérer les données

### 1. Télécharger les sources brutes

**DGFiP (cquest)** :
```bash
mkdir -p data/raw/cquest
cd data/raw/cquest
for year in {2000..2018}; do
  curl -O "http://data.cquest.org/dgfip_comptes_collectivites/communes/${year}.csv"
done
```

**OFGL** :
```bash
cd data/raw
curl -O "https://data.ofgl.fr/api/explore/v2.1/catalog/datasets/ofgl-base-communes-consolidee/exports/json"
```

### 2. Traiter les données

```bash
python3 scripts/process.py      # CSV cquest → JSON 2000-2018
python3 scripts/merge_ofgl.py   # Fusion + OFGL 2018-2025
```

### 3. Copier le JSON final

```bash
cp data/processed/reunion_24_communes_data_complet.json processed/
```

---

## 🎯 Utilisation

### Onglet 🏛️ Accueil par commune

1. Cliquez sur une commune dans la grille
2. Consultez les **cartes de statistiques** (population, recettes, dépenses, dette, épargne)
3. Explorez les **graphiques** :
   - Évolution des recettes/dépenses (2000-2025)
   - Structure des recettes (impôts, dotations, autres)
   - Structure des dépenses (personnel, achats, charges)
   - Investissement annuel
   - Dette et épargne
4. Lisez les **insights** et le **diagnostic** automatique
5. Consultez le **tableau détaillé** année par année

### Onglet 📊 Comparaison

**Radar comparatif** :
1. Cochez 2 ou 3 communes
2. Le radar se met à jour automatiquement
3. Comparez les profils financiers normalisés (0-100)

**Carte heatmap** :
1. Sélectionnez un indicateur dans la liste
2. Les 24 communes se colorent selon la valeur
3. Survolez pour voir les détails
4. Cliquez pour accéder à la fiche de la commune

**Tableau comparatif** :
1. Triez par colonne (clic sur l'en-tête)
2. Les 3 premières communes ont des médailles 🥇🥈🥉
3. Cliquez sur une ligne pour accéder à la fiche
4. Exportez en CSV (compatible Excel)

---

## 📈 Exemples de résultats

### La Possession (97408)

| Année | Population | Recettes | Dépenses | Dette |
|---|---|---|---|---|
| 2000 | 22 014 | 17,76 M€ | 16,11 M€ | 14,51 M€ |
| 2010 | 27 520 | 33,71 M€ | 33,99 M€ | 22,96 M€ |
| 2020 | — | — | — | — |
| 2025 | 33 106 | 57,07 M€ | 60,38 M€ | 59,44 M€ |

**Évolution 2000-2025** : +221% de recettes

---

## 🎨 Charte graphique

| Couleur | Hex | Usage |
|---|---|---|
| 🔵 Bleu France | `#0055A4` | Couleur principale |
| ⚪ Blanc | `#FFFFFF` | Fond |
| 🔴 Rouge Marianne | `#EF4135` | Accents, alertes |

---

## 📝 License

Ce projet est sous licence **MIT**. Voir [LICENSE](LICENSE) pour plus de détails.

---

## 👤 Auteur

**Gunout** — [@gunout](https://github.com/gunout)

---

## 🙏 Remerciements

- **DGFiP** pour les comptes individuels des communes
- **Christian Quest** pour le miroir [data.cquest.org](http://data.cquest.org)
- **OFGL** pour les données consolidées récentes
- **Chart.js** pour la bibliothèque de graphiques

---

## 🔗 Liens utiles

- [Application live](https://gunout.github.io/sante-communes-reunion/)
- [DGFiP — Comptes des communes](https://www.data.economie.gouv.fr/)
- [OFGL — data.ofgl.fr](https://data.ofgl.fr/)
- [INSEE — Populations légales](https://www.insee.fr/)
- [Préfecture de La Réunion](https://www.reunion.gouv.fr/)

---

<div align="center">

**🇫🇷 Fait avec ❤️ pour La Réunion 🇷🇪**

⭐ Si ce projet vous plaît, n'hésitez pas à lui donner une étoile !

</div>

---

<div align="center">

### 🇫🇷 Gunout · 2026

![Made in France](https://img.shields.io/badge/Made_in-France-002395?style=flat-square&labelColor=FFFFFF&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA5MDAgNjAwIj48cmVjdCB3aWR0aD0iOTAwIiBoZWlnaHQ9IjYwMCIgZmlsbD0iIzAwMjM5NSIvPjxyZWN0IHdpZHRoPSI5MDAiIGhlaWdodD0iNDAwIiB5PSIxMDAiIGZpbGw9IiNmZmYiLz48cmVjdCB3aWR0aD0iOTAwIiBoZWlnaHQ9IjIwMCIgeT0iNDAwIiBmaWxsPSIjZWQyOTM5Ii8+PC9zdmc+)
![GitHub](https://img.shields.io/badge/GitHub-gunout-181717?style=flat-square&logo=github&logoColor=white)
![Year](https://img.shields.io/badge/2026-ED2939?style=flat-square&labelColor=FFFFFF)

<sub>© 2026 <strong>Gunout</strong> — Tous droits réservés.</sub>

</div>
