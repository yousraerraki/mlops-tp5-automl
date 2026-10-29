# Modele manuel ou modele AutoML ? (TP05)

| Critere                    | Manuel (rf 500/16)          | AutoML (FLAML 90 s)               |
|----------------------------|-----------------------------|-----------------------------------|
| Famille de modele          | foret aleatoire             | XGBoost (XGBClassifier)           |
| F1 sur le jeu de test      | 0.8669                      | 0.8582                            |
| Temps de recherche machine | 1.3 s (entrainement unique) | 90.1 s (duree_recherche_s)        |
| Temps humain (estimation)  | ~ 2 a 3 h (reglage au TP2)  | ~ 5 min (ecrire le script)        |
| Latence mediane (ms)       | 70.4 (69.9 / 70.8)          | 20.7 (20.6 / 20.7)                |
| Latence p95 (ms)           | 93.8 (93.2 / 94.4)          | 40.3 (39.1 / 41.4)                |
| Taille du fichier (Mo)     | 13.37                       | 0.29                              |
| Explicabilite              | importance des variables, 500 arbres, profondeur 16 | importance des variables, 333 arbres de 4 feuilles max |

## Decision (5 lignes) : quel modele mettre en production, et pourquoi ?

1. Nous mettons en production le modele AutoML (fraude-automl, XGBoost).
2. Son F1 (0.8582) est a moins d'un point de celui du modele manuel (0.8669).
3. Il est 46 fois plus leger (0.29 Mo contre 13.37 Mo) : image Docker plus petite, demarrage plus rapide.
4. Il repond environ 3,4 fois plus vite (mediane 20.7 ms contre 70.4 ms, p95 40.3 ms contre 93.8 ms).
5. L'explicabilite reste comparable ; le modele manuel reste dans le registre comme solution de repli.
