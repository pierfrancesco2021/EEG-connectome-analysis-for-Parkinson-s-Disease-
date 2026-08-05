# EEG-connectome-analysis-for-Parkinson-s-Disease-

# Explainable Multi-Band Model for Enhanced EEG Signal Interpretation: Addressing Functional Connectivity Alteration in Parkinson’s Disease

> **Authors**: Donato Romano, Michele Magarelli, Pierfrancesco Novielli, Federica Cuna, Domenico Diacono, Pierpaolo Di Bitonto, Alfonso Monaco, Nicola Amoroso, Roberto De Blasi, Giancarlo Logroscino, Roberto Bellotti, Sabina Tangaro

## 📊 Graphical Abstract

![Graphical Abstract](eeg_upscayl_4x_realesrgan-x4plus.png)

## 📝 Abstract

Parkinson's disease (PD) is a neurodegenerative disorder characterized by the degeneration of dopaminergic neurons, leading to a variety of motor and non-motor symptoms. This study presents a novel explainable machine learning framework that integrates complex network analysis with multi-band EEG connectomes to detect and interpret functional connectivity alterations in PD.

We analyzed electroencephalographic signals from **31 subjects** (15 PD patients, 16 healthy controls), decomposing the spectral content into five frequency sub-bands (δ, θ, α, β, γ) to create a connectome for each rhythm. Seven key network features—degree, clustering coefficient, betweenness centrality, eigenvector centrality, information centrality, closeness centrality, and edge betweenness centrality—were extracted and fed into an XGBoost classifier.

**Key Results**:
- 🧠 **Full Connectome**: AUC = 0.84 ± 0.05, Accuracy = 0.80 ± 0.05
- 🧠 **Theta Band (Best Individual)**: AUC = 0.82 ± 0.03, Accuracy = 0.75 ± 0.03
- 🔍 **Multi-Connectome**: AUC = 0.72 ± 0.04

The SHAP algorithm identified **C4 (right primary motor cortex)**, **P3 (left parietal lobe)**, and the **F3-T7 frontal-temporal connection** as the most discriminative features, with alterations most pronounced in theta and delta bands. This framework enables **personalized connectome analysis**, offering new perspectives on the neural mechanisms underlying Parkinson's disease.

---

## 🔬 Methods Overview

### Workflow


### Key Steps

1. **Preprocessing** (EEGLAB/MATLAB):
   - Noisy channel removal (kurtosis-based, z-score > 3)
   - Band-pass filtering (0.5-100 Hz)
   - ICA-based artifact removal using ICLabel
   - Common average reference
   - Epoch rejection (±100 µV threshold)

2. **Connectome Construction**:
   - **Nodes**: 32 EEG electrodes
   - **Edges**: Spearman's rank correlation coefficient
   - Weighted networks (no threshold applied)
   - Applied to complete signal and five frequency bands

3. **Network Features Extracted**:
   - Degree
   - Clustering coefficient
   - Betweenness centrality
   - Eigenvector centrality
   - Information centrality
   - Closeness centrality
   - Edge betweenness centrality

4. **Classification**:
   - **Algorithm**: XGBoost (Extreme Gradient Boosting)
   - **Validation**: 10-fold cross-validation repeated 20 times
   - **Comparison**: Random Forest, SVM, MLP

5. **Explainability**:
   - **Method**: SHAP (SHapley Additive exPlanations)
   - **Analysis**: Global feature importance + personalized waterfall plots

---

## 📈 Results

### Full Connectome Classification Performance

| Metric | Value |
|--------|-------|
| **AUC-ROC** | 0.84 ± 0.05 |
| **Accuracy** | 0.80 ± 0.05 |
| **Sensitivity** | 0.74 ± 0.07 |
| **Specificity** | 0.86 ± 0.07 |
| **Precision** | 0.84 ± 0.07 |

### Band-Specific Performance

| Frequency Band | AUC-ROC | Accuracy | Precision |
|----------------|---------|----------|-----------|
| **θ (Theta)** | **0.82 ± 0.03** | **0.75 ± 0.03** | **0.76 ± 0.04** |
| α (Alpha) | 0.77 ± 0.04 | 0.70 ± 0.04 | 0.68 ± 0.05 |
| γ (Gamma) | 0.76 ± 0.05 | 0.67 ± 0.06 | 0.66 ± 0.07 |
| δ (Delta) | 0.69 ± 0.04 | 0.65 ± 0.05 | 0.64 ± 0.06 |
| β (Beta) | 0.62 ± 0.05 | 0.57 ± 0.08 | 0.56 ± 0.05 |

### Multi-Connectome Performance

| Metric | Value |
|--------|-------|
| AUC-ROC | 0.72 ± 0.04 |
| Accuracy | 0.67 ± 0.06 |
| Precision | 0.68 ± 0.07 |

---

## 🔑 Key Findings

### 1. Theta Band Dominance
The theta rhythm (4-8 Hz) demonstrated the highest discriminative power, consistent with known cognitive and memory-related impairments in PD. This band is crucial for distinguishing between healthy individuals and PD patients.

### 2. Critical Brain Regions
- **C4 (Right Primary Motor Cortex)**: Shows increased degree centrality in PD patients, indicating compensatory reorganization in motor networks
- **P3 (Left Parietal Lobe)**: Associated with cognitive deficits in PD
- **F3-T7 Connection**: Frontal-temporal connectivity, particularly impaired in theta and delta bands, suggesting disruption in cognitive processing pathways

### 3. Personalized Analysis
SHAP waterfall plots reveal individual-specific feature contributions, enabling:
- Personalized identification of affected neural circuits
- Tailored therapeutic strategies
- Patient-specific monitoring of disease progression

### 4. Robust Indicators
C4 degree and F3-T7 derivation emerge as common important features across both full and multi-connectome analyses, underscoring their significance as robust biomarkers.

---

## 📁 Dataset

This study uses the **San Diego Parkinson's EEG Dataset** (OpenNeuro accession: **ds002778**):

| Group | N | Age (years) | Gender |
|-------|---|-------------|--------|
| **PD Patients** | 15 | 62.6 ± 8.3 | 8F, 7M |
| **Healthy Controls** | 16 | 63.5 ± 9.6 | 9F, 7M |

- **EEG System**: 32-channel Biosemi
- **Sampling Rate**: 512 Hz
- **Duration**: ≥ 3 minutes resting-state
- **Condition**: Eyes open (fixating on a cross)
- **Medication**: PD patients off-medication (≥ 12 hours)

---

## 🚀 Getting Started

### Prerequisites

```bash
Python >= 3.8
MATLAB (for EEGLAB preprocessing)
