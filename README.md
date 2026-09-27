<div align="center">
# 🚀 Amazon ML Challenge 2026



## Business Entity Resolution

**Building a scalable machine learning pipeline for matching noisy business records across multiple data sources.**

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white)
![Machine Learning](https://img.shields.io/badge/Machine%20Learning-Entity%20Resolution-orange)
![Amazon ML Challenge](https://img.shields.io/badge/Amazon-ML%20Challenge%202026-FF9900?logo=amazon&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-success)

</div>

---

## 📌 About the Challenge

This repository contains our solution and experiments for the **Amazon ML Challenge 2026 – Business Entity Resolution Challenge**.

Real-world business information often comes from different sources with inconsistent names, addresses, formatting, abbreviations, missing fields, and other noise.

The objective is to determine which records across multiple datasets represent the **same real-world business entity**.

The challenge provides three independent sources:

- **Source 1 (S1)** — deduplicated reference entities
- **Source 2 (S2)** — candidate business records
- **Source 3 (S3)** — candidate business records

For every Source 1 entity, the system attempts to identify all corresponding entities from Sources 2 and 3.

---

## 🧠 Our Approach

Our solution follows a multi-stage Entity Resolution pipeline:

```text
                    ┌─────────────────────┐
                    │   Raw Business Data │
                    │    S1 / S2 / S3     │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │   Preprocessing &   │
                    │    Normalization    │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Candidate Generation│
                    │     / Blocking      │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Feature Engineering │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │   ML-Based Entity   │
                    │      Matching       │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Validation & Final  │
                    │     Resolution      │
                    └──────────┬──────────┘
                               │
                               ▼
              ┌──────────────────────────────┐
              │     Final Submission Files   │
              │                              │
              │ • matching_results.tsv       │
              │ • candidate_pairs.tsv        │
              └──────────────────────────────┘
```

### 1. 🧹 Data Preprocessing

Business records are cleaned and normalized before comparison.

The pipeline handles variations such as:

- capitalization
- punctuation
- whitespace
- business-name variations
- address inconsistencies
- missing information
- noisy textual fields

### 2. 🔎 Candidate Generation

Comparing every Source 1 entity against every record in Sources 2 and 3 would be computationally expensive.

Candidate generation or **blocking** reduces the search space by identifying plausible matches before the more expensive matching stages.

### 3. ⚙️ Feature Engineering

Candidate pairs are transformed into useful similarity features representing signals such as:

- business-name similarity
- address similarity
- token overlap
- geographical information
- numerical/address components
- exact and partial matches
- blocking information

### 4. 🤖 Machine Learning

The generated features are used to estimate whether two records represent the same real-world business.

The system is designed around the challenge's precision-heavy evaluation objective.

### 5. 🎯 Entity Resolution

Model predictions are converted into final entity relationships while attempting to avoid incorrect merges between unrelated businesses.

---

## 📊 Evaluation Metric

The challenge uses the **Macro F₀.₅ Score**.

```text
F₀.₅ = (1.25 × Precision × Recall)
       ──────────────────────────
        (0.25 × Precision + Recall)
```

Unlike the standard F1 score, **F₀.₅ gives greater importance to precision**.

This is especially important for Entity Resolution because incorrectly merging two different businesses can be more damaging than missing a possible match.

---

## 📂 Repository Structure

This repository contains multiple development branches representing different iterations of our solution.

```text
amazon-ml-2026/
│
├── dataset/                    # Competition datasets
├── docs/                       # Documentation
├── notebooks/                  # Experiments / analysis
├── scripts/                    # Utility & benchmark scripts
├── src/                        # Core ML pipeline
├── tests/                      # Tests and validation
├── artifacts/                  # Generated artifacts
│
├── version1                    # First solution iteration
│
└── version2                    # Final / improved solution iteration
```

> Large competition datasets and generated artifacts may be excluded from normal Git tracking because of their size.

---

## 🌿 Development Branches

Development was separated into branches so different architectures and experiments could be developed independently.

| Branch | Purpose |
|---|---|
| `main` | Stable repository / project overview |
| `version1` | Version 1 submission and experiments |
| `version2` | Version 2 submission and improved pipeline |
| `training-pipeline` | Model training workflow |
| `Multithreaded-arch` | Parallel / multithreaded architecture experiments |
| `refactored-arch` | Refactored implementation |

This branch-based workflow allowed experimentation without disrupting other implementations.

---

## 📦 Submission Files

The final challenge submission requires two primary TSV outputs:

### `matching_results.tsv`

Contains the final predicted matches for each Source 1 entity.

### `candidate_pairs.tsv`

Contains the candidate entities generated during the blocking/candidate-generation stage.

The expected submission package follows the general structure:

```text
submission/
│
├── output/
│   ├── matching_results.tsv
│   └── candidate_pairs.tsv
│
├── code/
│   └── business_entity_resolution/
│       ├── src/
│       ├── README.md
│       └── requirements.txt
│
└── Documentation_template.md
```

---

## 🛠️ Technologies

The project primarily uses:

- **Python**
- **Pandas**
- **NumPy**
- **Scikit-learn**
- Machine Learning classification
- String similarity techniques
- Candidate blocking
- Feature engineering
- Entity resolution algorithms
- Git & GitHub

Individual experimental branches may use additional libraries.

---

## 💡 Key Challenges

### Large-Scale Matching

Millions of records make exhaustive pairwise comparison impractical. Efficient candidate generation is therefore essential.

### Noisy Business Information

The same business can appear differently across independent datasets.

For example:

```text
Amazon Technologies Inc.
Amazon Technologies, Inc
AMAZON TECHNOLOGIES
```

A robust Entity Resolution system needs to recognize that formatting differences do not necessarily represent different businesses.

### Precision vs Recall

Aggressive matching may improve recall while creating false positives.

Because the competition uses **F₀.₅**, the pipeline must carefully balance candidate recovery with high-confidence matching.

---

## 🏁 Final Goal

The project aims to build an Entity Resolution pipeline that is:

**Scalable** ⚡  
Capable of processing millions of business records.

**Accurate** 🎯  
Designed to minimize incorrect entity merges.

**Reproducible** 🔁  
Structured so experiments and submission pipelines can be recreated.

**Modular** 🧩  
Separates preprocessing, blocking, feature engineering, modeling, inference, and validation.

---

## 👥 Contributors

This project was developed collaboratively for the **Amazon ML Challenge 2026**.

Thanks to everyone who contributed to the architecture, experimentation, implementation, testing, and submission process.

---

<div align="center">

### ⭐ Amazon ML Challenge 2026

**Business Entity Resolution • Machine Learning • Large-Scale Record Matching**

Built with Python 🐍 and a lot of experimentation 🚀

</div>
