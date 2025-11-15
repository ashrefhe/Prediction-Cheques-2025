# Prédiction et Analyse des Chèques – Attijari Bank

Ce projet propose une pipeline complète allant de la simulation des données bancaires à la visualisation BI, en passant par l’ingénierie de features, la modélisation prédictive (valeurs continues) et la création de dashboards interactifs.

---

## 🏗️ Étapes du projet

### 1. Simulation et Préparation des Données
- Génération des clients, comptes et opérations bancaires (2022-2024) avec répartition réaliste par typologie (entreprise, particulier, étudiant...).
- Simulation des transactions dont les chèques : montants, fréquences, villes, eligibility client-chéquier, gestion des soldes.
- Structuration de la base sur PostgreSQL : tables dimensionnelles (`dimclients`, `dimcomptes`, `dimdate`), table factuelle (`factoperations`), et type d’opérations (DDL SQL inclus).

### 2. ETL et Data Warehouse
- Nettoyage, jointures et agrégation des données massives simulées (>67M opérations).
- Chargement progressif dans le data warehouse PostgreSQL via `pandas/sqlalchemy` par chunks pour performance et robustesse.
- Vérification d’intégrité et contrôles d’export.

### 3. Feature Engineering et Extraction
- Imputation des valeurs manquantes, normalisation, gestion des outliers.
- Création de variables temps, volatilité, ratios, moyennes mobiles, tendances interannuelles, ratios chèques/virements.
- Sélection intelligente des features pour entraînement et prédiction (ex : `trendnbcheques2022_2023`, `cvnbcheques`, `montantmoyenparcheque2023`, etc.).
- Pipeline Python modulaire et extensible — voir `prediction.ipynb` pour le détail.

### 4. Modélisation Prédictive (Valeurs Continues)
- Les modèles sont entraînés sur les données **2022 et 2023** pour prédire **2024**, afin de comparer les résultats aux valeurs réelles et évaluer la performance des modèles.
- Après évaluation, les modèles sont utilisés pour prédire **2025** : nombre et montant total des chèques par client, avec intervalles de confiance.
- Modèles utilisés : Poisson, Ridge, Lasso, ElasticNet, RandomForest, GradientBoosting.
- Validation croisée temporelle, tuning hyperparamètres avec `GridSearchCV`, gestion de l’overfitting.
- Analyse de l’importance des variables pour extraire les drivers principaux.

### 5. Visualisation et Business Intelligence
- Dashboards interactifs Power BI à partir des exports modélisés et agrégés :
  - Vue globale, drill-down par ville, ancienneté des clients, type de clientèle, volume chèque.
  - Analyse comparative annuelle et prévisions 2025.
  - Visualisation des réseaux d’agences, température des opérations, contribution par segment.
- Captures d’écran incluses dans `/screenshots`.

---

## 📂 Structure du dépôt

| Dossier/Fichier               | Rôle |
|-------------------------------|------|
| `data_warehouse.ipynb`        | Création, peuplement, et tests Data Warehouse/Postgres |
| `comptes.ipynb`               | Simulation des comptes bancaires |
| `clientsdata.ipynb`           | Simulation et gestion des clients |
| `operations.ipynb`            | Génération massive des opérations de paiement |
| `prediction.ipynb`            | Pipeline feature engineering et modélisation prédictive |
| `feature_prediction.ipynb`    | Extraction et sélection avancée de features |
| `ETL.ipynb`                   | Nettoyage, fusion, transformation pilotée |
| `/screenshots`                | Captures d’écran des dashboards BI |

---

## ⚙️ Mode d’emploi

1. Simuler les jeux de données selon vos besoins ou télécharger les CSV générés.  
2. Exécuter `data_warehouse.ipynb` pour monter le schéma relationnel sous PostgreSQL.  
3. Nettoyer, préparer et agréger les données avec le notebook `ETL.ipynb`.  
4. Lancer la modélisation prédictive selon les valeurs cibles continues (`prediction.ipynb`).  
5. Comparer les prédictions de 2024 avec les valeurs réelles pour évaluer la performance des modèles.  
6. Exporter les agrégats nécessaires pour reporting et intégrer/actualiser les dashboards Power BI.  
7. Personnaliser ou étendre chaque étape : simulation, extraction, dashboarding.

---

## 📊 Visualisations Power BI

- Vue d’ensemble du volume et du montant des chèques par ville, client, agence et année.  
- Prévisions et objectifs pour 2025.  
- Analyse des tendances, volatilité et segmentation clientèle.  
- Modèle étoile complet des entités.

---

## 👤 Auteur et contact

Projet développé par **Ashref Hemriti**, pour démonstration d’une pipeline analytique bancaire & BI sur données simulées de chèques – 2025.
