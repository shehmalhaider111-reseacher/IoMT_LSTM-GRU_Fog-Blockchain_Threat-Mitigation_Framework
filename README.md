# IoMT LSTM-GRU Fog-Blockchain Threat Mitigation Framework

Official implementation and reproducibility repository for an edge-centric **Healthcare Internet of Medical Things (IoMT)** threat detection and mitigation framework.

The framework combines a hybrid **LSTM–GRU deep learning model** for multiclass IoMT threat detection with fog-based latency and resource profiling and policy-driven threat mitigation mechanisms. The repository provides the complete experimental pipeline, including data preprocessing, multi-seed model training, fog resource profiling, ablation studies with explainable AI (XAI), and external cross-dataset validation.

---

## 📁 Repository Structure

* **`data_preprocessing.py`**
  Loads and preprocesses the raw IoMT traffic data, including data cleaning, missing-value handling, categorical encoding, Random Forest-based feature importance analysis, feature selection, MinMax normalization, and generation of fixed-length sliding-window sequences.

* **`lstm_gru_fog_threat_blockchain_model.py`**
  Main implementation of the hybrid LSTM–GRU architecture for multiclass IoMT threat detection. The script also includes multi-seed execution, fog-node latency and resource profiling, scalability experiments, and policy-driven threat mitigation.

* **`ablation_study_xai.py`**
  Performs ablation experiments comparing standalone LSTM, standalone GRU, and the hybrid LSTM–GRU model. SHAP-based feature attribution is also generated for model interpretability.

* **`external_validation.py`**
  Performs external cross-dataset validation using the **WUSTL-EHMS-2020** dataset to evaluate the generalization capability of the proposed detection framework on an independent dataset.

* **`requirements.txt`**
  Contains the Python dependencies required to run the experimental pipeline.

---

## ⚙️ Environment Setup

Clone the repository and install the required dependencies:

```bash
git clone https://github.com/shehmalhaider111-reseacher/IoMT_LSTM-GRU_Fog-Blockchain_Threat-Mitigation_Framework.git
cd IoMT_LSTM-GRU_Fog-Blockchain_Threat-Mitigation_Framework
pip install -r requirements.txt
```

### System Environment

The framework was developed and evaluated using the following environment:

* **Python:** 3.9+
* **TensorFlow:** 2.x
* **Operating System:** Linux
* **Architecture:** x86_64
* **Fog-node CPU:** 2 CPU cores
* **Fog-node memory:** 4 GB RAM
* **Communication capacity:** 100 Mbps
* **Resource monitoring:** `psutil`

---

## 🔁 Multi-Seed Reproduction

To evaluate the stability of the proposed model under different random initializations, the experiments are executed using three independent random seeds:

**42, 100, and 2024**

In `lstm_gru_fog_threat_blockchain_model.py`, select the required seed:

```python
# Select the target seed sequentially:

CURRENT_SEED = 42       # Run 1: Primary experiment
# CURRENT_SEED = 100    # Run 2: Consistency evaluation
# CURRENT_SEED = 2024   # Run 3: Additional evaluation
```

Execute the model for each seed:

```bash
python lstm_gru_fog_threat_blockchain_model.py
```

### Generated Model Files

The corresponding trained model is saved for each seed:

```text
lstm_gru_seed_42.keras
lstm_gru_seed_100.keras
lstm_gru_seed_2024.keras
```

The multiple runs allow the experimental results to be examined across different random initializations.

---

## 🔬 Experimental Pipeline

### 1. Data Preprocessing

The preprocessing pipeline performs the following steps:

1. Loads the CICIoMT2024 traffic data.
2. Cleans the raw traffic records.
3. Handles missing values.
4. Encodes categorical variables and attack labels.
5. Uses Random Forest feature importance for feature selection.
6. Reduces the feature set from **44 to 29 features**.
7. Applies MinMax normalization using the training data.
8. Generates fixed-length sliding-window sequences with a sequence length of **10 timesteps**.

Run the preprocessing script:

```bash
python data_preprocessing.py
```

---

### 2. Hybrid LSTM–GRU Threat Detection

The proposed hybrid LSTM–GRU model performs multiclass classification of **18 IoMT traffic classes**.

The model learns temporal patterns in network traffic using the combined representation capability of LSTM and GRU layers.

Run:

```bash
python lstm_gru_fog_threat_blockchain_model.py
```

The same script also performs fog-node profiling and evaluates the behavior of the framework under different numbers of simulated IoMT devices.

---

### 3. Fog Computing Resource and Latency Profiling

The framework evaluates fog-node performance under increasing device loads.

The simulated fog-node configuration is:

| Resource          | Configuration |
| ----------------- | ------------: |
| CPU               |       2 cores |
| Memory            |      4 GB RAM |
| Network capacity  |      100 Mbps |
| Simulated devices |         10–50 |

CPU utilization and process-level memory consumption are monitored using the `psutil` library.

The profiling experiments are used to examine latency and resource behavior as the number of connected IoMT devices increases.

---

### 4. Policy-Driven Threat Mitigation

After threat detection, the framework applies predefined policy-driven mitigation mechanisms according to the detected threat category.

The mitigation component demonstrates how detected threats can be handled at the fog/edge level to support timely response within the IoMT environment.

---

### 5. External Cross-Dataset Validation

External validation is performed using the **WUSTL-EHMS-2020** dataset.

The purpose of this experiment is to evaluate the generalization capability of the proposed detection framework on an independent dataset that was not used during the primary CICIoMT2024 training process.

Run:

```bash
python external_validation.py
```

The external validation provides an additional evaluation of the model beyond the primary dataset.

---

### 6. Ablation Study and XAI

The ablation study evaluates the contribution of the hybrid architecture by comparing:

* Standalone LSTM
* Standalone GRU
* Hybrid LSTM–GRU

SHAP-based feature attribution is additionally used to analyze the contribution of input features to model predictions.

Run:

```bash
python ablation_study_xai.py
```

---

## 📊 Datasets

### Primary Dataset

The primary experiments use the **CICIoMT2024** dataset for IoMT network threat detection.

The experimental configuration uses:

* **18 traffic/attack classes**
* **44 initial features**
* **29 selected features**
* **10-timestep sliding sequences**

### External Validation Dataset

The **WUSTL-EHMS-2020** dataset is used for independent external validation.

It is used separately from the primary training data to assess cross-dataset generalization.

---

## 🏗️ Framework Overview

The overall experimental workflow is:

```text
                 CICIoMT2024 Traffic
                         │
                         ▼
              Data Preprocessing
                         │
                         ▼
              Feature Selection
                    44 → 29
                         │
                         ▼
               MinMax Normalization
                         │
                         ▼
             Sliding-Window Sequences
                    10 Timesteps
                         │
                         ▼
                Hybrid LSTM–GRU
                         │
                         ▼
                 Threat Detection
                         │
                         ▼
              Fog-Level Processing
                  │              │
                  ▼              ▼
              Latency       Resource
              Profiling      Profiling
                  │              │
                  └──────┬───────┘
                         ▼
              Threat Mitigation
                         │
                         ▼
             External Validation
               WUSTL-EHMS-2020
```

---

## 📌 Reproducibility

This repository provides the main components required to reproduce the reported experiments:

* Raw-data preprocessing pipeline
* Feature selection procedure
* MinMax normalization
* Sliding-window sequence generation
* Hybrid LSTM–GRU model
* Multi-seed execution
* Fog-node resource configuration
* Latency and scalability profiling
* Policy-driven threat mitigation
* LSTM vs. GRU vs. LSTM–GRU ablation study
* SHAP-based feature attribution
* WUSTL-EHMS-2020 external validation
* Python dependency specification

For reproducibility, execute the scripts according to the experimental stages described above.

---

## 📄 License

This project is licensed under the **MIT License**. See the `LICENSE` file for details.
