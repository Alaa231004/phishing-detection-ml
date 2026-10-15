# 🔐 Phishing URL Detection — Machine Learning

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10+-blue?style=for-the-badge&logo=python&logoColor=white" alt="Python"/>
  <img src="https://img.shields.io/badge/Scikit--learn-Machine%20Learning-orange?style=for-the-badge&logo=scikit-learn&logoColor=white" alt="Scikit-learn"/>
  <img src="https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white" alt="Jupyter"/>
  <img src="https://img.shields.io/badge/Domain-Cybersecurity-red?style=for-the-badge&logo=securityscorecard&logoColor=white" alt="Cybersecurity"/>
</p>

<p align="center">
  <strong>A Machine Learning Approach to Phishing URL Detection</strong>
  <br/>
  Détection automatique des URL malveillantes à l'aide d'algorithmes de Machine Learning.
</p>

---

## 📌 Table des matières

- [À propos du projet](#-à-propos-du-projet)
- [Objectifs](#-objectifs)
- [Dataset](#-dataset)
- [Méthodologie](#-méthodologie)
- [Sélection des caractéristiques](#-sélection-des-caractéristiques)
- [Modèles de Machine Learning](#-modèles-de-machine-learning)
- [Résultats expérimentaux](#-résultats-expérimentaux)
- [Meilleur modèle](#-meilleur-modèle)
- [Structure du projet](#-structure-du-projet)
- [Installation et exécution](#-installation-et-exécution)
- [Technologies utilisées](#-technologies-utilisées)
- [Perspectives](#-perspectives)
- [Équipe du projet](#-équipe-du-projet)

---

## 🎯 À propos du projet

Le phishing est une cyberattaque qui consiste à tromper les utilisateurs en les redirigeant vers des sites frauduleux afin de dérober des informations sensibles, notamment des identifiants, des mots de passe ou des données financières.

Ce projet vise à développer un système de classification basé sur le **Machine Learning** capable de distinguer les URL légitimes des URL de phishing à partir de leurs caractéristiques.

L'approche repose sur l'analyse des données, l'extraction et la sélection de caractéristiques pertinentes, l'entraînement de plusieurs algorithmes et la comparaison de leurs performances.

### Objectifs

- Développer un modèle de classification binaire des URL.
- Explorer et préparer le dataset avant l'entraînement.
- Identifier les caractéristiques les plus pertinentes pour la détection.
- Comparer plusieurs algorithmes de Machine Learning.
- Évaluer les modèles à l'aide de métriques de classification.
- Identifier le modèle offrant le meilleur compromis entre précision et détection des URL malveillantes.

---

## 📊 Dataset

Le projet utilise un dataset de détection du phishing contenant des caractéristiques décrivant les URL et les pages web.

| Propriété | Description |
|---|---|
| Nombre d'observations | 11 430 URL |
| Nombre de colonnes initiales | 88 |
| Type de problème | Classification binaire |
| Classe 0 | URL légitime |
| Classe 1 | URL de phishing |
| Nombre de caractéristiques sélectionnées | 20 |
| Valeurs manquantes | Aucune, selon l'analyse initiale |

### Source des données

Le dataset utilisé est disponible sur Kaggle :

[Web Page Phishing Detection Dataset](https://www.kaggle.com/datasets/shashwatwork/web-page-phishing-detection-dataset)

Les données doivent être téléchargées séparément et placées dans le répertoire prévu à cet effet.

---

## ⚙️ Méthodologie

Le projet suit un pipeline de Machine Learning structuré en plusieurs étapes.

```text
Dataset
   │
   ▼
Exploration et analyse des données (EDA)
   │
   ▼
Nettoyage et traitement des valeurs aberrantes
   │
   ▼
Feature Engineering
   │
   ▼
Sélection des caractéristiques
   │
   ▼
Normalisation des données
   │
   ▼
Entraînement et comparaison des modèles
   │
   ▼
Évaluation des performances
   │
   ▼
Sélection du meilleur modèle
```

### 1. Exploration des données

- Analyse des statistiques descriptives.
- Étude de la distribution des variables.
- Visualisation des corrélations.
- Recherche des valeurs aberrantes.
- Génération d'un rapport exploratoire avec `ydata-profiling`.

### 2. Prétraitement des données

- Vérification de la qualité des données.
- Encodage de la variable cible.
- Traitement des valeurs aberrantes par la méthode IQR et clipping.
- Préparation des variables pour l'entraînement.

### 3. Feature Engineering

Des caractéristiques supplémentaires peuvent être construites à partir de la structure des URL, notamment :

- Longueur totale de l'URL.
- Nombre de chiffres.
- Nombre de caractères spéciaux.
- Présence du protocole HTTPS.

### 4. Sélection des caractéristiques

La sélection vise à réduire la dimensionnalité des données et à conserver les variables les plus informatives.

Les méthodes utilisées dans le pipeline comprennent :

- Analyse des corrélations.
- `VarianceThreshold`.
- `SelectKBest` avec le test statistique `f_classif`.

### 5. Normalisation

`StandardScaler` est utilisé pour standardiser les variables numériques lorsque cela est nécessaire.

Le scaler doit être ajusté uniquement sur les données d'entraînement afin d'éviter toute fuite d'information (*data leakage*).

---

## 🏆 Sélection des caractéristiques

Les 20 caractéristiques retenues dans le pipeline présenté couvrent plusieurs aspects des URL et des pages web.

| Caractéristique | Description |
|---|---|
| `length_url` | Longueur totale de l'URL |
| `length_hostname` | Longueur du nom d'hôte |
| `nb_dots` | Nombre de points |
| `nb_slash` | Nombre de barres obliques |
| `nb_www` | Présence de « www » |
| `ratio_digits_url` | Proportion de chiffres dans l'URL |
| `length_words_raw` | Longueur des mots extraits |
| `longest_words_raw` | Longueur du mot le plus long |
| `longest_word_path` | Longueur du mot le plus long dans le chemin |
| `avg_word_path` | Longueur moyenne des mots du chemin |
| `nb_hyperlinks` | Nombre de liens hypertextes |
| `ratio_intHyperlinks` | Proportion de liens internes |
| `ratio_extErrors` | Ratio d'erreurs sur les liens externes |
| `domain_registration_length` | Durée d'enregistrement du domaine |
| `domain_age` | Âge du domaine |
| `google_index` | Indicateur d'indexation |
| `page_rank` | Indicateur de popularité du domaine |
| `url_length` | Longueur calculée de l'URL |
| `num_digits` | Nombre de chiffres |
| `num_special` | Nombre de caractères spéciaux |

Les caractéristiques réellement utilisées par le modèle doivent être confirmées à partir du notebook final.

---

## 🤖 Modèles de Machine Learning

Quatre algorithmes sont comparés dans le cadre de cette étude.

### 1. K-Nearest Neighbors (KNN)

Algorithme de classification fondé sur la proximité entre les observations. La classe d'une URL est déterminée à partir des classes de ses voisins les plus proches.

### 2. Support Vector Machine (SVM)

Algorithme qui recherche une frontière de séparation entre les classes. Le noyau RBF permet de modéliser des relations non linéaires entre les caractéristiques.

### 3. Arbre de décision

Modèle qui construit des règles de classification successives. Il présente l'avantage de faciliter l'interprétation des décisions.

### 4. Naive Bayes

Algorithme probabiliste basé sur le théorème de Bayes, avec une hypothèse d'indépendance conditionnelle entre les caractéristiques.

---

## 📈 Résultats expérimentaux

Les résultats ci-dessous correspondent aux métriques communiquées dans le rapport du projet.

| Modèle | Accuracy | Précision | Recall | F1-Score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| KNN (k = 15) | 95,10 % | 94,64 % | 95,48 % | 95,06 % | 98,61 % |
| **SVM (RBF)** | **95,80 %** | **95,43 %** | **96,10 %** | **95,76 %** | **99,01 %** |
| Arbre de décision | 92,39 % | 91,45 % | 93,53 % | 92,38 % | 96,43 % |
| Naive Bayes | 83,42 % | 84,50 % | 83,42 % | 83,38 % | 93,98 % |

### Interprétation

- **Accuracy** : proportion totale de prédictions correctes.
- **Précision** : proportion des URL prédites comme phishing qui sont effectivement des URL de phishing.
- **Recall** : proportion des URL de phishing effectivement détectées.
- **F1-Score** : moyenne harmonique de la précision et du recall.
- **ROC-AUC** : capacité du modèle à distinguer les deux classes sur différents seuils de décision.

Ces métriques doivent être calculées sur le même jeu de test pour permettre une comparaison cohérente.

---

## 🥇 Meilleur modèle

Selon les résultats communiqués, le **SVM avec noyau RBF** obtient les meilleures performances globales parmi les quatre modèles évalués.

| Indicateur | Résultat |
|---|---:|
| Accuracy | 95,80 % |
| Précision | 95,43 % |
| Recall | 96,10 % |
| F1-Score | 95,76 % |
| ROC-AUC | 99,01 % |

Son recall de 96,10 % indique qu'il détecte une grande partie des URL de phishing présentes dans le jeu de test.

Cependant, un modèle de détection ne garantit pas l'identification de toutes les URL malveillantes. Une validation supplémentaire sur des données récentes et indépendantes serait nécessaire avant une utilisation en production.

---

## 📁 Structure du projet

```text
phishing-url-detection/
│
├── data/
│   └── README_data.md
│
├── notebooks/
│   └── Phishing_ML.ipynb
│
├── models/
│   └── README.md
│
├── rapport/
│   └── Rapport_Phishing_ML.docx
│
├── requirements.txt
├── .gitignore
└── README.md
```

Cette structure constitue une proposition d'organisation. Adaptez les noms et les chemins aux fichiers réellement présents dans votre repository.

**Important :** le dataset, les modèles volumineux et les fichiers sensibles ne doivent pas être publiés sans vérification des droits de partage. Le dossier `models/` peut rester vide au départ ou contenir un fichier `README.md`.

---

## 🚀 Installation et exécution

### 1. Cloner le repository

```bash
git clone https://github.com/VOTRE_USERNAME/phishing-url-detection.git
cd phishing-url-detection
```

Remplacez `VOTRE_USERNAME` par le nom de votre compte GitHub.

### 2. Créer un environnement virtuel

```bash
python -m venv .venv
```

Sous Windows :

```bash
.venv\Scripts\activate
```

Sous Linux ou macOS :

```bash
source .venv/bin/activate
```

### 3. Installer les dépendances

Si le fichier `requirements.txt` est disponible :

```bash
pip install -r requirements.txt
```

Sinon, les bibliothèques principales peuvent être installées avec :

```bash
pip install pandas numpy scikit-learn matplotlib seaborn ydata-profiling jupyter
```

### 4. Préparer le dataset

Téléchargez le dataset depuis Kaggle et placez le fichier CSV à l'emplacement attendu par le notebook.

Vérifiez le chemin du fichier dans les cellules de chargement des données avant de lancer l'analyse.

### 5. Exécuter le notebook

```bash
jupyter notebook
```

Ouvrez ensuite `notebooks/Phishing_ML.ipynb` et exécutez les cellules dans l'ordre.

---

## 🛠️ Technologies utilisées

| Technologie | Utilisation |
|---|---|
| Python | Langage de programmation |
| Pandas | Manipulation des données |
| NumPy | Calcul numérique |
| Scikit-learn | Prétraitement, classification et évaluation |
| Matplotlib | Visualisation des données |
| Seaborn | Visualisation statistique |
| Jupyter Notebook | Expérimentation et documentation |
| ydata-profiling | Exploration automatisée des données |
| Git et GitHub | Gestion de versions et partage du projet |

---

## 🔭 Perspectives d'amélioration

Plusieurs évolutions peuvent être envisagées :

- **Ensemble Learning :** comparer Random Forest, XGBoost et d'autres méthodes d'ensemble.
- **Deep Learning :** étudier des modèles capables d'analyser directement la séquence de caractères des URL.
- **API REST :** exposer le modèle via une API pour recevoir une URL et retourner une prédiction.
- **Interface web :** développer une interface simple pour tester des URL.
- **Évaluation en conditions réelles :** tester le modèle sur des URL récentes et inconnues.
- **Explicabilité :** identifier les caractéristiques qui influencent le plus les prédictions.
- **Déploiement :** conteneuriser l'application avec Docker et préparer son déploiement.

---

## 👥 Équipe du projet

Projet réalisé en groupe dans le cadre du cours de **Machine Learning en sécurité informatique** à l'École des Sciences de l'Information (ESI), Rabat.

- **Membres :** à compléter avec les noms des membres du groupe.
- **Encadrement :** à compléter si nécessaire.
- **Année universitaire :** à compléter.

---

<p align="center">
  <strong>Phishing URL Detection</strong>
  <br/>
  Machine Learning for Cybersecurity
</p>
