# 🦑 Atlas du Nautilus — The Nautilus Exploration

> _« Une carte interactive immersive inspirée de Jules Verne, propulsée par de l'IA générative et du web moderne. »_

![Carte interactive du Nautilus](img/cap_naut.png)

🌐 **Site en ligne :** [the-nautilus-exploration.netlify.app](https://the-nautilus-exploration.netlify.app)

---

## 🚀 Présentation

J'ai réalisé ce projet car, étant une femme très organisée, j'ai visualisé le trajet du Nautilus comme une carte mentale. Cette intuition m'a menée à extraire et structurer les données géographiques du roman _Vingt mille lieues sous les mers_ 🦑 de Jules Verne, puis à les enrichir progressivement avec de l'intelligence artificielle.

Le projet est né d'une question simple : _et si on pouvait suivre le Nautilus en temps réel sur une carte interactive, avec toutes les informations scientifiques, biologiques et historiques que Jules Verne a semées dans son roman ?_

À l'aide de JupyterLab, de Python et d'un modèle de langage local (Mistral 7B via Ollama), j'ai conçu une application qui reconstitue le voyage complet du Nautilus — 32 escales, deux langues, quatre fiches d'information par escale, générées en partie par une vraie IA générative.

---

## 🛠️ Fonctionnalités

🌍 **Carte interactive** retraçant les 32 escales du Nautilus sur les océans du monde

🌊 **Effets visuels océaniques** inspirés de la 3D, interface immersive

📱 **Interface responsive** adaptée aux mobiles et desktop

🇫🇷🇬🇧 **Affichage bilingue** français / anglais intégral

📖 **Fiche 1 — Extrait du livre** : extraits authentiques du roman de Jules Verne pour chaque escale

🐋 **Fiche 2 — Espèces marines** : 329 espèces détectées directement dans le texte du livre par algorithme NLP (regex + dictionnaire exhaustif INPN), classées par catégorie (cétacés, mollusques, échinodermes, algues...)

🔬 **Fiche 3 — Découvertes scientifiques du XIXe siècle** : textes générés par IA (Mistral 7B local) contextualisés par escale — savants de l'époque, disciplines, expéditions réelles

⚗️ **Fiche 4 — Comparaison 1866 / Aujourd'hui** : comparaison générée par IA entre ce que Jules Verne décrivait et la réalité scientifique et écologique de 2025

---

## 🤖 Architecture IA

Ce projet utilise une architecture **RAG simplifiée** (Retrieval Augmented Generation) :

1. Les textes des deux livres (`20000lieues_fr.txt` et `20000lieues_an.txt`) sont découpés en chapitres
2. Pour chaque escale, les passages correspondants sont extraits et fournis en contexte au modèle
3. **Mistral 7B** (via Ollama, exécuté localement sur GPU) génère les contenus des fiches 3 et 4
4. Les résultats sont sauvegardés en JSON statique (`fiche3_science_19c.json`, `fiche4_comparaison.json`)
5. Le HTML final est généré par le notebook et déployé sur Netlify — **zéro coût, zéro API externe**

```
Livres .txt  →  Script Python (Map_traduction.ipynb)
                      ↓
              Ollama / Mistral 7B (GPU local)
                      ↓
              fiche3_science_19c.json
              fiche4_comparaison.json
              especes_maritimes.json
                      ↓
              carte_nautilus_multilang.html  →  Netlify
```

---

## ⚙️ Installation & utilisation

### Prérequis

- Python 3.10+
- JupyterLab
- [Ollama](https://ollama.com) installé avec le modèle Mistral :

```bash
ollama pull mistral
```

### Cloner le repo

```bash
git clone https://github.com/mimiecmoua/nautilus-map.git
cd nautilus-map
```

### Installer les dépendances Python

```bash
pip install folium pandas
```

### Lancer le notebook

```bash
jupyter lab
```

Ouvrir `notebooks/Map_traduction.ipynb` et exécuter toutes les cellules (**Run All**).

> ⚠️ Ollama doit être actif (icône lama dans la barre des tâches Windows) lors de la première exécution pour générer les fiches 3 et 4. Les exécutions suivantes chargent directement les JSON sans rappeler le modèle.

### Déployer sur Netlify

Pousser les fichiers générés sur GitHub — Netlify déploie automatiquement.

---

## 🗂️ Structure du projet

```
nautilus-map/
├── notebooks/
│   ├── Map_traduction.ipynb          # Notebook principal
│   ├── especes_maritimes.json        # 329 espèces extraites du livre
│   ├── fiche3_science_19c.json       # Textes IA fiche 3
│   ├── fiche4_comparaison.json       # Textes IA fiche 4
│   └── data_texts/
│       ├── 20000lieues_fr.txt        # Roman en français
│       └── 20000lieues_an.txt        # Roman en anglais
├── img/                              # Images et assets
├── carte_nautilus_multilang.html     # Carte générée (déployée)
├── index.html                        # Page d'accueil
├── index2.html                       # Page carte
├── index3.html                       # Page mode d'emploi
├── README.md                         # Ce fichier
└── README_EN.md                      # Version anglaise
```

---

## 🛠️ Technologies utilisées

| Technologie             | Rôle                                     |
| ----------------------- | ---------------------------------------- |
| **Python 3**            | Langage principal                        |
| **JupyterLab**          | Environnement de développement           |
| **Folium**              | Cartographie interactive (Leaflet.js)    |
| **Pandas**              | Manipulation des données tabulaires      |
| **Ollama + Mistral 7B** | IA générative locale (fiches 3 & 4)      |
| **NLP regex + INPN**    | Extraction des espèces marines (fiche 2) |
| **Bootstrap 5**         | Interface modale et responsive           |
| **HTML / CSS / JS**     | Rendu final de la carte                  |
| **Netlify**             | Déploiement statique gratuit             |
| **GitHub**              | Versioning et intégration continue       |

---

## 📊 Chiffres clés

- 📍 **32 escales** reconstituées sur les océans du monde
- 🐋 **329 espèces marines** détectées dans le texte original de Jules Verne
- 📖 **2 langues** — français et anglais intégral
- 🤖 **64 textes générés par Mistral** (32 escales × 2 langues pour la fiche 4)
- 💰 **Coût de fonctionnement : 0 €** — 100 % local, 100 % open source

---

## 👩‍💻 Auteure

Ce projet a été imaginé, conçu et développé par **Émilie Clain — webOara**, ingénieure autodidacte en intelligence artificielle, développeuse web et passionnée par l'univers de Jules Verne.

💡 Elle aime transformer des idées audacieuses en expériences interactives accessibles, avec une touche de magie technologique.  
🎨 Entre deux lignes de code, elle explore l'art, la musique, l'histoire… et parfois même les fonds marins.

📫 Contact pro : [LinkedIn](https://www.linkedin.com/in/emilieclain)  
💻 Code open source : [GitHub](https://github.com/mimiecmoua/nautilus-map)  
🌐 Site : [weboara.com](https://weboara.com)

---

## 🏛️ Remerciements

Projet présenté à la **Société Jules Verne** — association dédiée à la promotion et à l'étude de l'œuvre de Jules Verne.

_« La science, mon ami, est faite d'erreurs, mais d'erreurs qu'il est bon de commettre, car elles mènent peu à peu à la vérité. »_ — Jules Verne

---

© 2025 WebOara — Émilie Clain | Licence MIT
