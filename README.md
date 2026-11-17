# Quantum-Enhanced Dimensionality Reduction Using QUMAP for Breast Cancer Data

> **Academic research project | Quantum Machine Learning | Dimensionality Reduction | Medical Data Analysis**

This repository documents an academic research project investigating classical, quantum-inspired, and hybrid dimensionality-reduction approaches for the Wisconsin Diagnostic Breast Cancer dataset. The central research direction is to study whether quantum-state-fidelity-based similarity can be incorporated into UMAP-style manifold learning while preserving meaningful local neighbourhood relationships.

**Repository status:** Documentation-first research repository. Source code, notebooks, trained models, and generated datasets are intentionally not included in this repository at this stage.

---

## Table of Contents

- [1. Project Overview](#1-project-overview)
- [2. Research Problem](#2-research-problem)
- [3. Research Objectives](#3-research-objectives)
- [4. Dataset](#4-dataset)
- [5. Methods Under Investigation](#5-methods-under-investigation)
- [6. Enhanced QUMAP Research Direction](#6-enhanced-qumap-research-direction)
- [7. Experimental Evaluation](#7-experimental-evaluation)
- [8. Patient Similarity Network Analysis](#8-patient-similarity-network-analysis)
- [9. Current Progress](#9-current-progress)
- [10. Planned Work](#10-planned-work)
- [11. Technology Stack](#11-technology-stack)
- [12. Repository Structure](#12-repository-structure)
- [13. Data and Reproducibility](#13-data-and-reproducibility)
- [14. Research Limitations](#14-research-limitations)
- [15. References](#15-references)
- [16. Disclaimer](#16-disclaimer)

---

## 1. Project Overview

High-dimensional datasets can increase computational cost and make it difficult to identify meaningful patterns. Dimensionality reduction maps data into a smaller representation while attempting to preserve useful information or relationships.

This project studies dimensionality reduction from both classical and quantum-computing perspectives. It compares established classical methods with quantum-inspired or quantum-circuit-based counterparts, using breast cancer diagnostic data as the experimental case study.

The primary research focus is **QUMAP (Quantum Uniform Manifold Approximation and Projection)** and the investigation of a hybrid distance strategy that combines fidelity-based similarity with classical Euclidean distance.

The broader project also considers reducing both the number of features and the number of training samples to investigate their potential impact on quantum-machine-learning resource requirements.

## 2. Research Problem

The project aims to develop and evaluate a systematic framework for comparing classical and quantum data-reduction techniques, and to identify suitable approaches for efficient Quantum Machine Learning under data and resource constraints.

A specific research question is:

> How does a quantum-state-fidelity-based similarity measure affect the local-neighbourhood structure learned by UMAP, and can a hybrid similarity strategy improve the resulting low-dimensional representation of breast cancer data?

The research does not assume that quantum methods will outperform classical methods. Their representation quality, computational requirements, and downstream usefulness must be evaluated experimentally.

## 3. Research Objectives

The project is organized around three objectives.

### Objective 1 — Feature / Column Reduction

Compare classical and quantum or quantum-inspired dimensionality-reduction methods:

| Classical method | Quantum counterpart / research implementation |
|---|---|
| Principal Component Analysis (PCA) | Quantum PCA (QPCA) / QPCA-inspired implementation |
| Uniform Manifold Approximation and Projection (UMAP) | Quantum-inspired UMAP (QUMAP) |
| Classical Autoencoder (AE) | Quantum Autoencoder (QAE) |

The purpose is to compare reduced representations in terms of information preservation, neighbourhood structure, classification performance, and computational cost.

### Objective 2 — Quantum Optimization and Sample / Row Reduction

Investigate data encoding and quantum-circuit design considerations, including gate selection and optimization. The proposed sample-reduction study considers training-data proportions of:

`100% → 70% → 50% → 30% → 20% → 10%`

This objective is intended to study the effect of reducing the number of training samples on resource requirements and model performance. It should be considered ongoing/planned unless supported by completed experiment results.

### Objective 3 — Quantum Machine Learning Classification

Use reduced or optimized data for Quantum Machine Learning (QML), compare quantum and classical classifiers, and study predictive performance and generalization for benign-versus-malignant classification.

## 4. Dataset

The case study uses the **Wisconsin Diagnostic Breast Cancer (WDBC) dataset**, also referred to in the project materials as the Breast Cancer Wisconsin dataset.

| Property | Description |
|---|---|
| Samples | 569 |
| Numerical input features | 30 |
| Task | Binary classification |
| Target classes | Benign (B) and Malignant (M) |
| Current feature-reduction target | 10 dimensions in the documented experiments |

The 30 numerical features describe characteristics of cell nuclei computed from digitized images of fine needle aspirates of breast masses.

The project materials describe an initial transformation from a `569 × 30` feature matrix to a lower-dimensional representation such as `569 × 10`.

**Data handling:** The raw dataset is not committed in this documentation-only repository. Refer to the dataset's original distribution and terms before downloading or redistributing it. Do not upload private, identifiable, or otherwise restricted patient information.

## 5. Methods Under Investigation

### 5.1 Classical methods

- **PCA:** Linear dimensionality reduction based on principal directions of variance.
- **UMAP:** Nonlinear manifold learning designed to represent local-neighbourhood relationships.
- **Autoencoder:** Neural-network-based representation learning through reconstruction.

UMAP is used as an important classical reference because preserving local relationships is a central requirement of this research.

### 5.2 Quantum and quantum-inspired methods

- **QPCA / QPCA-inspired reduction:** Quantum principal-component-analysis concepts are considered in the comparative study. Any classical simulation or density-matrix-inspired implementation must be clearly distinguished from execution of a quantum algorithm on quantum hardware.
- **QUMAP:** A UMAP-style workflow in which data-point similarity is calculated using a quantum-state-inspired fidelity measure.
- **Quantum Autoencoder:** A quantum-circuit-based compression experiment using Qiskit and simulation tools, as documented in the research notebook.

The terms *quantum*, *quantum-inspired*, and *classically simulated* are not interchangeable. The implementation and execution environment must be stated precisely for each experiment.

## 6. Enhanced QUMAP Research Direction

The original QUMAP experiment uses a fidelity-based distance derived from normalized feature representations:

\[
F(x,y)=|\langle \psi_x \mid \psi_y \rangle|^2
\]

\[
D_Q(x,y)=1-F(x,y)
\]

The project investigates a hybrid distance that combines the fidelity-based distance with a normalized Euclidean distance:

\[
D_H(x,y)=\alpha D_Q(x,y)+(1-\alpha)D_E(x,y)
\]

where:

- \(D_H\) is the hybrid distance;
- \(D_Q\) is the fidelity-based distance;
- \(D_E\) is the normalized Euclidean distance; and
- \(\alpha\) controls the relative contribution of the two terms.

The notebook includes experiments with different values of \(\alpha\), including 0.25, 0.50, and 0.75. These experiments are intended to assess the effect of the weighting on embedding structure and downstream performance.

The hybrid formulation is a research direction under evaluation, not a claim of quantum computational advantage. The exact state encoding, normalization, distance construction, and UMAP integration should be documented alongside any future reproducible implementation.

## 7. Experimental Evaluation

The research materials describe evaluation at multiple levels.

### Representation quality

- Trustworthiness, to assess preservation of local neighbourhood relationships.
- Silhouette score, to assess separation of labelled groups in an embedding.
- Visual inspection of two-dimensional embeddings.
- Neighbourhood overlap and class-consistency analysis.

### Downstream classification

- Accuracy.
- Precision.
- Recall.
- F1-score.
- Confusion matrix.
- Benign and malignant class-wise performance.

The notebook contains classification experiments using classical models including RBF-SVM and Logistic Regression. The final classifier and split must be stated for each result; scores from different runs, splits, embedding dimensions, or classifiers must not be combined as if they came from one experiment.

### Robustness and computational cost

The research notebook also includes experiments involving multiple random seeds, stratified cross-validation, and runtime measurements. For a rigorous comparison, preprocessing and dimensionality-reduction steps must be fitted only on the training portion of each split or fold.

## 8. Patient Similarity Network Analysis

An additional analysis constructs patient-similarity graphs from the learned representations. The notebook documents graphs derived from:

1. Classical UMAP.
2. Original QUMAP.
3. Enhanced QUMAP.

The graph analysis uses NetworkX and examines:

- Number of nodes and edges.
- Average degree and weighted degree.
- Graph density.
- Connected components.
- Average clustering coefficient.
- Degree distributions.
- Highly connected nodes (patient hubs).
- Overlap between hub sets from different representations.

These measures describe graph structure. They do not, by themselves, establish clinical importance or validate a diagnostic biomarker. Any clinical interpretation requires separate validation.

## 9. Current Progress

Based on the project presentation materials and the supplied Jupyter Notebook, the work documented so far includes:

- Selection of the Wisconsin Diagnostic Breast Cancer dataset.
- Data preprocessing and standardization.
- Classical and quantum/quantum-inspired dimensionality-reduction comparisons.
- PCA and QPCA-inspired experiments.
- UMAP and fidelity-based QUMAP experiments.
- Classical and quantum autoencoder experiments.
- Investigation of weaker neighbourhood-preservation results in the original QUMAP experiment.
- Hybrid fidelity–Euclidean distance experiments for Enhanced QUMAP.
- Evaluation using embedding-quality and classification metrics.
- Experiments involving random seeds and stratified cross-validation.
- Two-dimensional embedding comparisons.
- Patient-similarity adjacency matrices and graph-theoretic analysis.

The project presentation dated 10 October 2026 describes the enhanced-QUMAP-to-QML classification pipeline as planned work. The notebook contains subsequent experimental development, but the repository does not yet publish the source notebook or a fully reproducible implementation.

**Important:** Numerical results should be published in a dedicated results document only after each value has been traced to its exact notebook cell, dataset split, embedding dimension, classifier, and validation protocol.

## 10. Planned Work

The following items are suitable next steps for completing and strengthening the research:

1. Consolidate the experimental configurations and maintain a single source of truth for reported metrics.
2. Document the exact quantum-state encoding and fidelity calculation.
3. Validate the hybrid distance normalization and the selection of \(\alpha\) without test-set leakage.
4. Reproduce results using leakage-safe stratified cross-validation.
5. Complete and document the proposed training-sample reduction study.
6. Integrate the reduced representations with a clearly specified QML classifier.
7. Compare quantum and classical classification under the same data splits and evaluation protocol.
8. Report runtime and resource requirements with sufficient implementation detail.
9. Validate patient-similarity graph findings and avoid unsupported clinical interpretations.
10. Prepare a reproducible code release when the implementation is ready for public distribution.

## 11. Technology Stack

The supplied notebook and project materials refer to the following tools and libraries:

| Area | Tools |
|---|---|
| Programming language | Python |
| Interactive research | Jupyter Notebook |
| Numerical computing | NumPy |
| Data processing | Pandas |
| Classical machine learning | Scikit-learn |
| Manifold learning | UMAP (`umap-learn`) |
| Deep learning | TensorFlow / Keras |
| Quantum computing | Qiskit |
| Visualization | Matplotlib |
| Graph analysis | NetworkX |
| Spreadsheet exports | OpenPyXL |

Exact package versions and a tested environment file should be added when the code is prepared for release.

## 12. Repository Structure

This repository is intentionally organized as an academic documentation repository. A suggested structure is:

```text
quantum-enhanced-qumap-breast-cancer/
│
├── README.md
├── CITATION.cff
├── LICENSE
├── CONTRIBUTING.md
├── CHANGELOG.md
│
├── docs/
│   ├── PROJECT_OVERVIEW.md
│   ├── METHODOLOGY.md
│   ├── EXPERIMENTAL_PROTOCOL.md
│   ├── RESULTS.md
│   ├── RESEARCH_PLAN.md
│   └── REFERENCES.md
│
├── figures/
│   └── README.md
│
└── .gitignore
```

Only files that have been reviewed and are ready for public release should be added. No source code is required for the initial documentation-only repository.

## 13. Data and Reproducibility

This repository currently provides research documentation rather than an executable software package.

To make future results reproducible, a code release should include:

- The notebook or modular source implementation.
- A dependency specification with tested versions.
- Dataset acquisition instructions and source citation.
- Fixed random seeds and explicit train/test split definitions.
- Experimental configuration files.
- Scripts for generating tables and figures.
- A record of hardware, simulator, and execution settings.
- A clear separation between simulated quantum experiments and hardware execution.

Do not claim that results are independently reproducible until the required code, data instructions, environment, and experiment configuration are available.

## 14. Research Limitations

- Results are specific to the dataset and experimental configurations used; broader generalization requires additional datasets and validation.
- Fidelity-based calculations performed with classical numerical operations are quantum-inspired simulations, not evidence of quantum hardware speedup.
- Quantum-circuit simulation and execution on quantum hardware have different resource and noise characteristics.
- Embedding quality and classification accuracy measure different properties and should be reported separately.
- Patient-similarity graph metrics are descriptive and do not establish clinical validity.
- A quantum advantage claim requires a fair comparison, explicit resource accounting, and evidence beyond a single accuracy result.

## 15. References

The following references are listed in the project's Panel Review 2 materials. Bibliographic details should be checked against the publisher record before formal publication.

1. V. Fernandes et al., “Analyzing data reduction techniques: An experimental perspective,” *Applied Sciences*, vol. 14, no. 8, Art. no. 3436, 2024. https://doi.org/10.3390/app14083436
2. S. Genç, “Feature selection using quantum feature maps: Performance analysis of classical and quantum models on the breast cancer dataset,” *International Journal of Data Science and Applications*, vol. 8, no. 1, pp. 28–44, 2025.
3. S. K. Sheoran, V. Yadav, and R. K. Sheoran, “Robust evaluation of classical and quantum machine learning under noise, imbalance, feature reduction and explainability,” *Scientific Reports*, vol. 15, Art. no. 45714, 2025. https://doi.org/10.1038/s41598-025-28412-9
4. S. R. Sihare, “Dimensionality reduction for data analysis with quantum feature learning,” *WIREs Data Mining and Knowledge Discovery*, vol. 15, Art. no. e1568, 2025. https://doi.org/10.1002/widm.1568
5. L. McInnes, J. Healy, and J. Melville, “UMAP: Uniform manifold approximation and projection for dimension reduction,” 2018. https://doi.org/10.48550/arXiv.1802.03426
6. X. Zhang et al., “Quantum-enhanced t-stochastic neighbor embedding for high-dimensional data visualization,” *Physical Review Research*, vol. 8, Art. no. 023265, 2026. https://doi.org/10.1103/w8b9-7zt9

## 16. Disclaimer

This repository documents an academic research project. It is not a clinical diagnostic tool and must not be used to make medical decisions. The experiments are research investigations on a public benchmark dataset and do not establish clinical effectiveness.

---

**Project title:** Quantum-Enhanced Dimensionality Reduction Using QUMAP for Breast Cancer Data  
**Research area:** Quantum Machine Learning and Data Reduction  
**Institutional context:** Amrita School of Computing  
**Repository type:** Academic research documentation
