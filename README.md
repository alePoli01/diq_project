# End-to-End Data Quality & Preparation Pipeline

## 📌 Overview
This repository contains a comprehensive Data Preparation and Quality Pipeline developed as part of the Data and Information Quality coursework. The project demonstrates the ability to take a raw, dirty dataset and systematically transform it into a clean, highly reliable dataset ready for downstream machine learning or analytical tasks. 

The pipeline handles complex data quality issues—such as missing values, multivariate outliers, and fuzzy duplicates—using advanced machine learning and record linkage techniques. By the end of the pipeline, the dataset achieved **100% completeness** and zero duplicate records.

## 🛠️ Tech Stack & Libraries
* **Data Manipulation:** `pandas`, `numpy`, `re`
* **Profiling & EDA:** `ydata-profiling`, `seaborn`, `matplotlib`
* **Machine Learning:** `scikit-learn` (Isolation Forest, Random Forest)
* **Dimensionality Reduction & NLP:** `umap-learn`, `sentence-transformers`, `hdbscan`, `scipy`
* **Data Matching:** `recordlinkage`

## 🏗️ Pipeline Architecture
To maintain a modular and scalable workflow, the pipeline is decoupled into dedicated Jupyter notebooks. 

| Step | Phase | Notebook | Description |
| :--- | :--- | :--- | :--- |
| **1** | **Initial Assessment** | `diq_dataq.ipynb` | Baseline evaluation of data integrity, schema definitions, and completeness ratios. |
| **2** | **Data Profiling** | `diq_datap.ipynb` | Automated EDA using `ydata-profiling` to map data distributions and variance. |
| **3** | **Data Wrangling** | `diq_dataw.ipynb` | String standardization, regex-based address parsing, and feature decomposition. |
| **4** | **Data Clustering** | `diq_datac.ipynb` | Text embedding via SentenceTransformers, reduced with **UMAP**, and clustered with **HDBSCAN** to consolidate high-cardinality categorical features. |
| **5** | **Missing Values** | `diq_datam.ipynb` | ML-driven imputation. Used **Random Forest** models to predict and fill missing values based on the combined information of other features. |
| **6** | **Outlier Detection** | `diq_datao.ipynb` | Rule-based checks for discrete variables and **Isolation Forests** for detecting multivariate outliers in continuous features. |
| **7** | **Deduplication** | `diq_datad.ipynb` | Exact matching combined with probabilistic record linkage (**Jaro-Winkler** distance) to identify and remove fuzzy duplicates. |
| **8** | **Final Assessment** | `diq_dataq_final.ipynb` | Verification of the final data state, achieving the desired quality metrics. |

## 🧠 Key Methodologies Highlighted

* **Machine Learning-Driven Imputation:** Instead of relying on simple mean/mode filling, Random Forest Regressors and Classifiers were trained on the dataset to intelligently estimate missing values for structural features.
* **Multivariate Outlier Detection:** Applied an Isolation Forest algorithm to the joint distribution of continuous area metrics (e.g., *Superficie Vendita* and *Superficie Altri Usi*) to flag and handle complex, multi-dimensional anomalies without relying on rigid standard deviation thresholds.
* **Semantic Dimensionality Reduction:** Transformed messy, high-cardinality categorical text (2,100+ unique values) into semantic embeddings. Applied UMAP for dimensionality reduction and HDBSCAN for density-based clustering, successfully consolidating the feature into 230 clean categories.
* **Probabilistic Record Linkage:** Implemented blocking and fuzzy string matching (Jaro-Winkler) via the `recordlinkage` library to detect near-duplicates that standard `.duplicated()` checks would miss due to typos or minor formatting variations.
