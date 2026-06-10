# 🚀 Projet Data Engineering Azure – Architecture Medallion (Bronze / Silver / Gold)

## 📌 Présentation du projet

Dans le cadre de la modernisation du système décisionnel d'une entreprise du secteur retail, ce projet consiste à concevoir et implémenter une plateforme Data Engineering complète sur Microsoft Azure.

L'objectif est de construire un pipeline automatisé capable d'ingérer, stocker, transformer et analyser des données provenant de différentes sources afin de produire des indicateurs métier exploitables pour la prise de décision.

L'architecture mise en œuvre repose sur le modèle Medallion (Bronze, Silver, Gold) et utilise Azure Data Factory pour l'orchestration, Azure Data Lake Storage Gen2 pour le stockage et Azure Databricks pour les traitements analytiques.

---

# 🎯 Objectifs

Ce projet permet de :

* Comprendre l'écosystème Azure dédié à la Data Engineering.
* Mettre en place un pipeline d'ingestion de données automatisé.
* Structurer un Data Lake selon l'architecture Medallion.
* Nettoyer et transformer les données avec Apache Spark.
* Produire des jeux de données analytiques optimisés.
* Concevoir un tableau de bord décisionnel sous Power BI.
* Intégrer plusieurs services cloud dans une architecture cohérente.

---

# 🏗️ Architecture du projet

Sources de données :

* Azure SQL Database

  * Products
  * Stores
  * Transactions

* API JSON publique

  * Customers

Pipeline de traitement :

Azure SQL Database / API JSON

⬇

Azure Data Factory

⬇

ADLS Gen2 Bronze Layer (Parquet)

⬇

Azure Databricks

⬇

Silver Layer (Delta)

⬇

Gold Layer (Delta)

⬇

Export CSV

⬇

Power BI Dashboard

---

# 🛠️ Technologies utilisées

| Technologie                  | Rôle                             |
| ---------------------------- | -------------------------------- |
| Azure SQL Database           | Base de données transactionnelle |
| Azure Data Lake Storage Gen2 | Stockage des données             |
| Azure Data Factory           | Orchestration et ingestion       |
| Azure Databricks             | Traitement et transformation     |
| Apache Spark / PySpark       | Calcul distribué                 |
| Delta Lake                   | Stockage optimisé Silver et Gold |
| Parquet                      | Format de stockage Bronze        |
| Power BI                     | Visualisation et reporting       |
| GitHub API (JSON)            | Source de données clients        |

---

# 📂 Structure du Data Lake

## Bronze Layer

Zone contenant les données brutes provenant des différentes sources.

bronze/

├── transactions/

├── products/

├── stores/

└── customers/

Format : Parquet

---

## Silver Layer

Zone contenant les données nettoyées et enrichies.

Traitements réalisés :

* Conversion des types de données
* Suppression des doublons
* Contrôle qualité
* Jointures entre les tables
* Création des indicateurs calculés

Exemple :

total_amount = quantity × price

Format : Delta Lake

---

## Gold Layer

Zone destinée à l'analyse métier.

Agrégations réalisées :

* Quantité vendue
* Chiffre d'affaires
* Nombre de transactions
* Valeur moyenne des transactions

Format : Delta Lake

---

# 📋 Déroulement du projet

## Phase 0 : Étude des services Azure

Documentation détaillée des services :

* Azure SQL Database
* Azure Data Lake Storage Gen2
* Azure Data Factory
* Azure Databricks Community Edition

---

## Phase 1 : Préparation des données

### Création de la base Azure SQL

Tables :

* Products
* Stores
* Transactions

Relations :

* Transactions → Products
* Transactions → Stores

### Import des données

Insertion de données de test dans les différentes tables.

### Ajout d'une source JSON

Utilisation d'une API publique GitHub contenant les données clients.

---

## Phase 2 : Création du Data Lake

### Création du Storage Account

Configuration :

* Hierarchical Namespace activé
* Azure Data Lake Storage Gen2

### Création des couches

* Bronze
* Silver
* Gold

---

## Phase 3 : Orchestration avec Azure Data Factory

### Pipeline d'ingestion

Mise en place de quatre Copy Activities :

1. Products → Bronze
2. Stores → Bronze
3. Transactions → Bronze
4. Customers API → Bronze

Format de sortie :

Parquet

---

## Phase 4 : Azure Databricks

### Configuration

* Création du cluster Spark
* Création des notebooks
* Connexion au Data Lake

### Vérification

Lecture des données Bronze depuis Databricks.

---

## Phase 5 : Traitement Silver

### Chargement des données

Création des DataFrames :

* products_df
* stores_df
* transactions_df
* customers_df

### Nettoyage

* Gestion des valeurs nulles
* Conversion des types
* Suppression des doublons

### Transformation

Jointure des différentes tables.

Création de l'indicateur :

total_amount = quantity * price

### Sauvegarde

Écriture dans la couche Silver au format Delta.

---

## Phase 6 : Traitement Gold

### Lecture de Silver

Chargement des données nettoyées.

### Agrégation métier

Calcul :

* Revenue
* Quantity Sold
* Number of Transactions
* Average Transaction Value

### Sauvegarde

Écriture dans la couche Gold au format Delta.

---

# 📊 Tableau de bord Power BI

Les données Gold sont exportées au format CSV puis importées dans Power BI.

Visualisations réalisées :

### Sales by Date

Analyse temporelle des ventes.

### Sales by Product

Classement des produits les plus vendus.

### Sales by Category

Répartition du chiffre d'affaires par catégorie.

### Quantity Sold

Volume total des ventes.

### Average Transaction Value

Valeur moyenne des transactions.

---

# 📈 Résultats obtenus

Grâce à cette architecture :

* Centralisation des données retail.
* Automatisation complète du pipeline.
* Réduction des traitements manuels.
* Amélioration de la qualité des données.
* Mise à disposition d'indicateurs fiables pour l'analyse métier.

---

# 👨‍💻 Compétences développées

* Azure SQL Database
* Azure Data Factory
* Azure Data Lake Storage Gen2
* Azure Databricks
* Apache Spark / PySpark
* Delta Lake
* Data Warehousing
* Architecture Medallion
* ETL / ELT
* Power BI
* Cloud Data Engineering

---

# 📚 Auteur

Projet réalisé dans le cadre d'une formation Data Engineering Azure.

Auteur : [Votre Nom]

Date : Juin 2026
