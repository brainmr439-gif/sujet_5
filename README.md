# Détection de fraude dans les transactions de mobile money

Projet du cours d'Intelligence Artificielle (M2 MIAGE, UFHB), sujet 5.
Auteurs : YAPI YAPO PAUL EMMANUEL / POE JEAN-PHILLIPE ARNAUD

Détection de fraude sur le jeu synthétique PaySim : détection d'anomalies
(Isolation Forest), classification (Random Forest, AdaBoost), réseau de neurones
PyTorch, réglage du seuil d'alerte selon les coûts, simulation en flux.

## Résultats principaux

- Fraude = 0,129 % des transactions, présente uniquement dans TRANSFER et CASH_OUT.
- Random Forest : meilleur modèle dans les deux scénarios (PR-AUC 1,000 avec les ratios,
  0,914 avec les variables brutes).
- Seuil réglé selon les coûts : coût total réduit de 39 à 90 % par rapport au seuil 0,5
  (validation sur une moitié du test non utilisée pour choisir le seuil).
- Simulation en flux : 6,5 ms par transaction en moyenne, 29 fraudes sur 30 bloquées.

Détails et limites : voir le rapport.

## Structure

```
data/                    # PaySim (non versionné, voir ci-dessous)
notebooks/
  environnement.ipynb   # tout le pipeline, dans l'ordre
figures/                 # figures du rapport
resultats_modeles.csv    # tableau de comparaison des modèles
informations.txt
```

## Installation

```bash
python -m venv .venv
source .venv/bin/activate        # Windows : .venv\Scripts\activate
pip install -r informations.txt
```

## Données

1. Télécharger PaySim sur Kaggle : « Synthetic Financial Datasets For Fraud Detection ».
2. Placer le fichier `PS_20174392719_1491204439457_log.csv` dans `data/`.

## Exécution

Ouvrir `notebooks/environnement.ipynb` et exécuter toutes les cellules dans l'ordre
(Kernel > Restart & Run All). Durée totale : environ 30 à 45 minutes sur un poste
standard (l'entraînement des forêts aléatoires est la partie la plus longue).
Graines aléatoires fixées à 42.

## Notes de reproductibilité

- Découpage temporel : 80 % des premiers `step` pour l'entraînement, le reste pour le test.
- Les temps de latence dépendent de la machine ; les autres résultats sont reproductibles.
- Les jeux de variables « B » (avant transaction) et « D » (brut) sont définis dans le notebook.