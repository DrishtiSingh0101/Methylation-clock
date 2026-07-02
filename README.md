# 🧬 Methylation Clock for Breast Cancer (TCGA-BRCA)

## Project Overview

DNA methylation is one of the most well-studied epigenetic modifications associated with aging. Specific CpG sites across the genome undergo predictable methylation changes as humans age, enabling the development of **epigenetic (DNA methylation) clocks** that estimate biological age from methylation data.

In this project, I built an **ElasticNet-based epigenetic clock** using **normal breast tissue methylation data** from **TCGA-BRCA** and applied the trained model to **breast cancer tumor samples** to investigate **epigenetic age acceleration**.

The project was developed entirely in Python using publicly available TCGA DNA methylation datasets.

---

# Objectives

- Build an epigenetic clock using normal breast tissue methylation profiles.
- Identify CpG sites significantly associated with chronological age.
- Train an ElasticNet regression model to predict biological age.
- Validate the clock on unseen normal samples.
- Apply the trained clock to breast cancer tumors.
- Quantify epigenetic age acceleration in tumors.

---

# Key Results

- 🧬 Built an ElasticNet-based epigenetic clock using 75 TCGA-BRCA normal samples.
- 📈 Achieved MAE ≈ 5.1 years and R² ≈ 0.88 on held-out normal samples.
- 🎯 Applied the clock to 283 TCGA-BRCA tumor samples.
- ⏳ Observed a median epigenetic age acceleration of ~6 years in tumors.
- 📊 Found a significant difference in age acceleration between normal and tumor tissues (Mann–Whitney p ≈ 0.05).

# Dataset

Source:
- The Cancer Genome Atlas (TCGA)
- TCGA-BRCA

Platform:
- Illumina Human Methylation 450K Array

Workflow:
- SeSAMe Methylation Beta Estimation

Data Used:

### Normal Samples
- 75 breast normal samples
- DNA methylation beta values
- Clinical age information

### Tumor Samples
- 283 breast tumor samples
- DNA methylation beta values
- Clinical age information

---

# Project Workflow

```text
Download TCGA Data
        │
        ▼
Create CpG × Sample Beta Matrix
        │
        ▼
Quality Control
    • Remove missing CpGs
    • Beta value distribution
    • PCA
        │
        ▼
Identify Age-associated CpGs
    • Pearson Correlation
    • P-value
    • FDR correction
        │
        ▼
Candidate CpG Selection
    • FDR < 0.05
    • |r| > 0.5
        │
        ▼
Train ElasticNet Clock
        │
        ▼
Validate on Held-out Normal Samples
        │
        ▼
Predict Tumor Epigenetic Age
        │
        ▼
Calculate Age Acceleration
        │
        ▼
Compare Normal vs Tumor
```

---

# Methods

## Data Preparation

- Downloaded TCGA DNA methylation beta values
- Mapped methylation files to TCGA sample IDs
- Integrated clinical age information
- Constructed CpG × Sample methylation matrix

---

## Quality Control

Performed:

- Removal of missing CpGs
- Beta value distribution visualization
- Principal Component Analysis (PCA)

Purpose:

- Detect outlier samples
- Explore global methylation patterns
- Assess biological variability

---

## Age-associated CpG Discovery

For every CpG:

- Pearson correlation with chronological age
- P-value calculation
- Benjamini-Hochberg FDR correction

Candidate CpGs were selected using:

- FDR < 0.05
- |Correlation| > 0.5

---

## Epigenetic Clock Development

Machine Learning Model:

- ElasticNetCV

Training:

- 80% Training Set
- 20% Test Set

Evaluation Metrics:

- Mean Absolute Error (MAE)
- R² Score
- Pearson Correlation

---

## Tumor Analysis

The trained clock was directly applied to tumor samples.

Predicted biological age was calculated for each tumor.

Age acceleration was computed as:

Age Acceleration = Predicted DNAm Age − Chronological Age

---

# Results

## Normal Tissue Clock Performance

| Metric | Value |
|---------|------:|
| Samples | 75 |
| Candidate CpGs | 421 |
| MAE | ~5.1 years |
| R² | ~0.88 |

The trained model accurately predicted chronological age in unseen normal breast samples.

---

## Tumor Analysis

Samples:

- 283 Breast Tumors

Mean Epigenetic Age Acceleration:

+5.6 years

Median Age Acceleration:

+6.0 years

Statistical Test:

Mann–Whitney U Test

p-value ≈ 0.05

The tumor samples exhibited significantly higher epigenetic age acceleration compared to normal breast tissue.

---

# Visualizations

The notebook generates:

- Beta value distribution
- PCA plots
- Age-associated CpG volcano plot
- CpG methylation vs age scatter plots
- Actual vs Predicted Age
- Tumor age acceleration histogram
- Normal vs Tumor age acceleration violin plot

---

# Repository Structure

```
Methylation-clock/
│
├── notebooks/
│   └── Methylation_clock.ipynb
│
├── data/
│   ├── Normal_metadata/
│   ├── Tumor_metadata/
│   └── README.md
│
├── results/
│   ├── plots/
│   └── tables/
│
├── README.md
├── requirements.txt
└── .gitignore
```

---

# Requirements

Python 3.11+

Main packages:

- pandas
- numpy
- scipy
- matplotlib
- seaborn
- scikit-learn
- statsmodels
- joblib

Install dependencies:

```bash
pip install -r requirements.txt
```

---

# Reproducing the Analysis

1. Download TCGA BRCA methylation data from the GDC Data Portal.
2. Place the downloaded methylation beta files in the appropriate data directory.
3. Download the corresponding metadata and clinical files.
4. Open the notebook:

```
notebooks/Methylation_clock.ipynb
```

5. Execute the notebook sequentially.

---

# Future Improvements

- Feature selection performed only on the training set to eliminate information leakage.
- Cross-validation using independent cohorts.
- Evaluate additional regression models (LASSO, XGBoost, Random Forest).
- Compare with established epigenetic clocks (Horvath, Hannum, PhenoAge, GrimAge).
- Investigate subtype-specific epigenetic aging.
- Integrate mutation and clinical data for downstream analyses.

---

# Key Learnings

Through this project I gained practical experience in:

- DNA methylation data processing
- TCGA data acquisition
- Epigenetic clock development
- Feature selection using correlation and FDR
- ElasticNet regression
- Biological age prediction
- Cancer epigenetics
- Statistical testing
- Data visualization
- Machine learning for genomics

---

# References

- Horvath S. (2013). DNA methylation age of human tissues and cell types. Genome Biology.
- The Cancer Genome Atlas (TCGA)
- Genomic Data Commons (GDC)
