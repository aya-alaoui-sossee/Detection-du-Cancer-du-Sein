# Breast Cancer Detection with Ensemble Learning

*[Version française plus bas](#détection-du-cancer-du-sein-par-méthodes-ensemblistes)*

A student project (Euromed University of Fez) comparing ensemble learning methods for classifying breast tumours as benign or malignant from tabular cytology features.

## Data

Two public versions of the Wisconsin breast cancer data are used:

| Notebook | Dataset | Samples | Features used |
|---|---|---|---|
| `bagging_comparison.ipynb` | Wisconsin Diagnostic (WDBC), loaded with `sklearn.datasets.load_breast_cancer` | 569 | 30 |
| `stacking_model.ipynb` | Wisconsin Breast Cancer (Original), UCI | 699 | 5 (clump thickness, marginal adhesion, single epithelial cell size, bare nuclei, normal nucleoli) |

## Methods

**Bagging and majority voting** (`bagging_comparison.ipynb`)
- Models: Bagging with a KNN base learner (10 estimators), Random Forest, and an RBF SVC with standardisation
- 70/30 train/test split; confusion matrices, ROC curves, precision, recall, F1, specificity and balanced accuracy for each model
- A majority vote of the three models gives the final prediction

**Stacking** (`stacking_model.ipynb`)
- Preprocessing: missing values (`?`) imputed with the column mean, then Min-Max normalisation
- Base models: KNN (k=5), a small neural network (32-16-1, Keras) and a decision tree
- Meta-model: Gaussian Naive Bayes trained on the base models' predictions

## Results

| Method | Test set | Accuracy |
|---|---|---|
| Majority vote (Bagging-KNN + Random Forest + SVC) | WDBC, 171 samples | 97.7% |
| Stacking (KNN + ANN + Decision Tree → Naive Bayes) | Original Wisconsin, 28 samples | 96.4% |

Balanced accuracy of the individual models in the bagging notebook: Bagging-KNN 0.95, Random Forest 0.96, SVC 0.97.

## Limitations

- The two notebooks use different versions of the dataset, so their numbers are not directly comparable.
- The stacking meta-model is evaluated on only 28 samples, so its accuracy estimate is noisy.
- No cross-validation or external validation set.

## Run it

```bash
pip install -r requirements.txt
jupyter notebook notebooks/
```

The notebooks download the UCI data directly, so an internet connection is needed.

## Tech

Python, pandas, NumPy, scikit-learn, TensorFlow/Keras, SciPy, Matplotlib, Seaborn

---

# Détection du cancer du sein par méthodes ensemblistes

Projet étudiant (Université Euromed de Fès) qui compare des méthodes d'apprentissage ensembliste pour classer des tumeurs du sein en bénignes ou malignes à partir de données cytologiques tabulaires.

## Données

Deux versions publiques du jeu de données Wisconsin sont utilisées :

| Notebook | Jeu de données | Échantillons | Variables utilisées |
|---|---|---|---|
| `bagging_comparison.ipynb` | Wisconsin Diagnostic (WDBC), via `sklearn.datasets.load_breast_cancer` | 569 | 30 |
| `stacking_model.ipynb` | Wisconsin Breast Cancer (Original), UCI | 699 | 5 (épaisseur de la masse, adhérence marginale, taille des cellules épithéliales, noyaux nus, nucléoles normaux) |

## Méthodes

**Bagging et vote majoritaire** (`bagging_comparison.ipynb`)
- Modèles : Bagging avec KNN comme apprenant de base (10 estimateurs), Random Forest et SVC (noyau RBF) avec standardisation
- Découpage 70/30 ; matrices de confusion, courbes ROC, précision, rappel, F1, spécificité et accuracy équilibrée pour chaque modèle
- Un vote majoritaire des trois modèles donne la prédiction finale

**Stacking** (`stacking_model.ipynb`)
- Prétraitement : valeurs manquantes (`?`) remplacées par la moyenne, puis normalisation Min-Max
- Modèles de base : KNN (k=5), un petit réseau de neurones (32-16-1, Keras) et un arbre de décision
- Méta-modèle : Naive Bayes gaussien entraîné sur les prédictions des modèles de base

## Résultats

| Méthode | Jeu de test | Accuracy |
|---|---|---|
| Vote majoritaire (Bagging-KNN + Random Forest + SVC) | WDBC, 171 échantillons | 97,7 % |
| Stacking (KNN + ANN + arbre de décision → Naive Bayes) | Wisconsin original, 28 échantillons | 96,4 % |

Accuracy équilibrée des modèles individuels (notebook bagging) : Bagging-KNN 0,95, Random Forest 0,96, SVC 0,97.

## Limites

- Les deux notebooks utilisent des versions différentes du jeu de données : les résultats ne sont pas directement comparables.
- Le méta-modèle du stacking est évalué sur seulement 28 échantillons, l'estimation est donc peu stable.
- Pas de validation croisée ni de validation externe.

## Exécution

```bash
pip install -r requirements.txt
jupyter notebook notebooks/
```

Les notebooks téléchargent les données UCI directement : une connexion internet est nécessaire.

## Technologies

Python, pandas, NumPy, scikit-learn, TensorFlow/Keras, SciPy, Matplotlib, Seaborn
