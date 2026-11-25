# Classification de spams par méthode bayésienne naïve

Implémentation d'un filtre anti-spam en Python sur le jeu de données **Ling-spam** (960 e-mails prétraités, dictionnaire de 2 500 mots), comparant un modèle bayésien naïf codé *from scratch* à `GaussianNB` de `scikit-learn`.

## Objectif du projet
* Construire une matrice creuse binaire (présence/absence de chaque mot du dictionnaire).
* Implémenter un classifieur bayésien naïf avec **lissage de Laplace** et passage au **logarithme (`np.log`)** pour éviter l'*underflow* numérique.
* Évaluer les performances sur les 260 e-mails de test (matrice de confusion, *accuracy*, *F1-score*) et comparer avec `GaussianNB`.

## Données
* **Jeu d'entraînement :** 700 e-mails (350 spams, 350 normaux) — `train-features.txt`, `train-labels.txt`
* **Jeu de test :** 260 e-mails (130 spams, 130 normaux) — `test-features.txt`, `test-labels.txt`
* **Vocabulaire :** 2 500 mots (e-mails prétraités : suppression des mots outils, chiffres et ponctuation, lemmatisation/racinisation).

## Résultats principaux (sur 260 e-mails de test)

| Modèle | Accuracy | F1-score | Vrais Négatifs (VN) | Faux Positifs (FP) | Faux Négatifs (FN) | Vrais Positifs (VP) |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Naive Bayes (from scratch)** | **98,08 %** | **0,9811** | 125 | 5 | 0 | 130 |
| **GaussianNB (`scikit-learn`)** | 96,92 % | 0,9697 | 124 | 6 | 2 | 128 |

Le modèle implémenté à la main obtient de meilleurs résultats (5 erreurs contre 8 pour `GaussianNB`, et aucun spam manqué), car il modélise directement des variables binaires de présence de mots avec lissage de Laplace, tandis que `GaussianNB` suppose une distribution continue gaussienne.
