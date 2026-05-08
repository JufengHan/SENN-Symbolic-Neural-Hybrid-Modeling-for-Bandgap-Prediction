[中文](README.zh-CN.md) | English

# 🌟 Perovskite Bandgap Modeling with EQL & Neural Networks

This project leverages the **EQL (Equation Learner) network** to obtain symbolic mathematical expressions as encoders, which guide neural networks in modeling the relationship between **perovskite material compositions and their bandgaps**.  
In addition, we implement **SENN (Symbolically Encoded Neural Network)** and other classical machine learning methods as baselines for comparison, providing insights into both accuracy and interpretability.

---

## 🌐 Online Web Demo

A web-based SENN bandgap prediction interface is available here:

👉 [SENN-Bandgap Web App](https://senn-bandgap-web-qu64kxosjmv7z5ndz4jgca.streamlit.app/)

Users can directly input the composition fractions and obtain the predicted perovskite bandgap without installing the package locally.

---

## 📂 Project Structure

<pre>
.
├── data/                # Dataset: perovskite compositions and bandgap values
│   ├── data.csv         # Dataset for EQL
│   ├── train.csv        # Training data for SENN and other models
│   └── text.csv         # Testing data for SENN and other models
├── EQL.py               # Training script for EQL network (produces symbolic encoders)
├── models/              # SENN training code and other ML baseline models
│   ├── senn.py
│   ├── rf.py            # Random Forest
│   ├── svr.py           # Support Vector Regression
│   ├── linear.py        # Linear Regression
│   └── gbdt.py          # Gradient Boosting
└── README.md
</pre>

---

## ⚙️ Environment Setup

First, create a virtual environment and install dependencies:

```bash
python -m venv .venv
source .venv/bin/activate    # On Windows: .venv\Scripts\activate
```

Key dependencies:

```text
numpy
pandas
scikit-learn
torch
DySymNet  # for symbolic regression
```

---

## 🚀 Usage

### 1. Train the EQL Encoder

```bash
python EQL.py
```

### 2. Train SENN and Other ML Models

Navigate into the `models/` directory and run the corresponding scripts:

```bash
python models/senn.py
python models/rf.py
python models/svr.py
python models/gbdt.py
```

---

## 📊 Outputs

Prediction results are stored as `.csv` files, including true and predicted bandgap values.

Evaluation metrics are stored as `.txt` files, including R², RMSE, MAE, and other metrics.

---

# SENN-Bandgap Quick Start

This project provides an installable SENN-based bandgap prediction package. Users can directly install the package via `pip` and predict the bandgap of perovskite compositions without retraining the model.

Users may also use the online web interface directly:

👉 [SENN-Bandgap Web App](https://senn-bandgap-web-qu64kxosjmv7z5ndz4jgca.streamlit.app/)

The input order is fixed as:

```text
[MA, FA, Cs, Br, Cl, I]
```

where `MA`, `FA`, and `Cs` denote A-site composition fractions, while `Br`, `Cl`, and `I` denote X-site composition fractions.

---

## Installation

```bash
pip install senn-bandgap
```

---

## Python Usage

Create a Python file, for example `predict.py`:

```python
from senn_bandgap import BandgapPredictor

predictor = BandgapPredictor()

bandgap = predictor.predict_one(
    MA=0.0,
    FA=1.0,
    Cs=0.0,
    Br=0.0,
    Cl=0.0,
    I=1.0,
)

print(f"Predicted bandgap: {bandgap:.6f} eV")
```

Run:

```bash
python predict.py
```

---

## Command-Line Usage

After installation, the predictor can also be used directly from the terminal:

```bash
senn-bandgap --MA 0 --FA 1 --Cs 0 --Br 0 --Cl 0 --I 1
```

Example output:

```text
Predicted bandgap: 1.520524 eV
```

Another example with mixed compositions:

```bash
senn-bandgap --MA 0 --FA 0.9 --Cs 0.1 --Br 0.2 --Cl 0 --I 0.8
```

---

## Input Requirements

The recommended composition constraints are:

```text
MA + FA + Cs ≈ 1
Br + Cl + I ≈ 1
```

The predicted bandgap is reported in:

```text
eV
```

---

## 📖 Research Significance

The EQL network generates symbolic expressions that act as encoders, helping neural networks capture underlying physical relations.

SENN and classical ML methods provide baselines to assess model performance in terms of both accuracy and interpretability.

This approach contributes to understanding the link between perovskite compositions and bandgap engineering, offering a data-driven pathway for new material design.
