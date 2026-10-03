# Data Analytics & MLOps Project: Strategic Pokémon Analysis with PySpark

This project leverages Apache Spark (PySpark) to analyze, transform, and model combat statistics from the Pokémon ecosystem (Ultimate Pokémon Dataset 2025). The goal is to apply Data Engineering and Machine Learning (MLOps) best practices to extract latent knowledge about Game Design and propose a Teambuilding optimization algorithm.

## Tech Stack
* **Distributed Processing:** Apache Spark (PySpark SQL, PySpark MLlib)
* **Data Manipulation:** Python, Pandas
* **Data Visualization:** Matplotlib, Seaborn
* **Ingestion:** Kaggle API (`kagglehub`)

## Data Pipeline Structure

### 1. Ingestion and Quality Assurance
* Automated dataset download via Kaggle.
* Data cleanliness analysis: missing value detection, cardinality analysis (unique values) to map game metadata, and strict duplicate verification.

### 2. Data Engineering
* **Schema Definition:** Explicit data type casting to prevent Spark parsing errors.
* **Feature Engineering:** Creation of derived metrics like Body Mass Index (`bmi`), Attack/Defense ratio, and specialist type categorization (Physical, Special, Balanced).
* **Cluster Optimization:** Dataset caching via `persist(StorageLevel.MEMORY_ONLY)` to guarantee immediate RAM access during exploratory analysis and iterative machine learning phases.

### 3. Exploratory Data Analysis (EDA)
* **Univariate:** Global power (`base_stat_total`) distribution illustrating the bimodality of evolutionary stages and the statistical isolation of the Legendary class.
* **Bivariate:** Tracking stat inflation (Power Creep) across generations and highlighting the "hardcoded" negative correlation between base stats and Pokémon capture rates.
* **Multivariate:** Correlation matrices (`pairplots` and `heatmaps`) to study game balance, proving that overall power is almost perfectly correlated with base experience yield.

### 4. Advanced Transformations & Optimization
* **Window Functions:** Distributed windowing to rank Pokémon within their own generation or primary type.
* **Broadcast Hash Join:** Physical execution plan optimization by forcing a network cache (`broadcast()`) of a small dimension table (type profiles) to eliminate network Shuffle during joins.

### 5. Machine Learning & Algorithmic Optimization
* **Unsupervised Learning (K-Means & PCA):** Training a clustering model (K-Means) on standardized statistics to automatically identify latent combat archetypes 
(Tanks, Knights, Balanced, Mages). Principal Component Analysis (PCA) is used to extract, reduce, and visualize variance axes (Global Power Index vs. Specialization Orientation).
* **Constrained Optimization (Teambuilding):** Greedy selection algorithm based on Spark partitioning (`Window.partitionBy`) to generate the best possible 6-Pokémon team. 
The system enforces elemental diversity by strictly keeping only the absolute best representative of each primary type.

## How to Run the Project
1. Launch the execution environment (Google Colab or a PySpark-compatible cluster recommended).
2. Run the dependency installation cell: `!pip install pyspark kagglehub`.
3. Execute the notebook sequentially to automatically download the cached data and trigger the Spark session.


