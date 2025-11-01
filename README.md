# Détection d'Intrusion Réseau (NIDS) par Machine Learning

![Python](https://img.shields.io/badge/Python-3.9%2B-blue.svg)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

Ce projet utilise des techniques de Machine Learning pour construire un Système de Détection d'Intrusion Réseau (NIDS) efficace. L'objectif est de classifier le trafic réseau en distinguant le trafic "Bénin" (Benign) des attaques "FTP-BruteForce" et "SSH-Bruteforce".

Le notebook `Détection_d'Intrusion_Réseau_(NIDS)_par_Machine_Learning_.ipynb` présente l'ensemble du pipeline, de l'exploration des données à l'évaluation du modèle.

## 📊 Données

Le jeu de données utilisé est le fichier **02-14-2018.csv**, qui fait partie du dataset CIC-IDS-2018. Il contient les caractéristiques de flux réseau capturées lors d'une journée incluant des simulations d'attaques Brute Force.

* **Source :** [Kaggle - IDS Intrusion CSV](https://www.kaggle.com/datasets/solarmainframe/ids-intrusion-csv?select=02-14-2018.csv)
* **Taille :** 1 048 575 lignes x 80 colonnes
* **Classes Cibles :** `Benign`, `FTP-BruteForce`, `SSH-Bruteforce`

## 🛠️ Pipeline du Projet

Le notebook suit un pipeline complet :

1.  **Exploration des Données (EDA) :** Chargement et inspection des 1M+ lignes. Identification et comptage des valeurs manquantes (NaN) et infinies (Inf).
2.  **Nettoyage et Prétraitement :** Remplacement des valeurs infinies et NaN (résultant souvent de divisions par zéro dans la capture de flux) par 0.
3.  **Préparation (Preprocessing) :**
    * Encodage de la variable cible (`LabelEncoder`).
    * Séparation des données (70% entraînement, 30% test).
    * Standardisation des features (`StandardScaler`) pour normaliser les échelles, en évitant la fuite de données.
4.  **Modélisation :** Entraînement et comparaison de deux modèles :
    * **Régression Logistique** (comme baseline linéaire).
    * **Random Forest Classifier** (comme modèle d'ensemble).

## 📈 Résultats et Évaluation

Les deux modèles ont été évalués sur l'ensemble de test (plus de 314 000 échantillons). Le Random Forest a démontré une performance quasi parfaite, ce qui est idéal pour un cas d'usage en cybersécurité.

### Tableau Récapitulatif des Performances

| Modèle | Accuracy Globale | Faux Négatifs (Attaques -> "Bénin") | Faux Positifs ("Bénin" -> Attaque) | Erreurs inter-attaques |
| :--- | :--- | :--- | :--- | :--- |
| **Régression Logistique** | 99,97% | **1** (1 SSH classé Bénin) | **79** (73 Bénin -> FTP, 6 Bénin -> SSH) | 9 (SSH classé FTP) |
| **Random Forest** | **100,00%** (arrondi) | **0** | **0** | 9 (SSH classé FTP) |

### Conclusion

Le **Random Forest Classifier** s'est avéré être le modèle optimal. Il atteint une performance parfaite en n'identifiant **aucun Faux Négatif** (aucune attaque manquée) et **aucun Faux Positif** (aucune fausse alerte).

Dans un contexte de sécurité où manquer une seule attaque est le risque principal, la performance irréprochable du Random Forest en fait le choix idéal pour ce jeu de données.

## 🚀 Comment l'utiliser

1.  Clonez ce dépôt :
    ```bash
    git clone [https://github.com/VOTRE-NOM/VOTRE-REPO.git](https://github.com/VOTRE-NOM/VOTRE-REPO.git)
    cd VOTRE-REPO
    ```

2.  (Recommandé) Créez un environnement virtuel :
    ```bash
    python -m venv venv
    source venv/bin/activate  # Sur Windows: venv\Scripts\activate
    ```

3.  Installez les dépendances requises :
    ```bash
    pip install pandas numpy scikit-learn matplotlib seaborn jupyterlab
    ```

4.  Lancez Jupyter Lab (ou Notebook) et ouvrez le fichier `.ipynb` :
    ```bash
    jupyter lab
    ```

## 📄 Licence

Ce projet est sous licence MIT. Voir le fichier `LICENSE` pour plus de détails.
