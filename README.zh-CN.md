中文 | [English](README.md)

# 🌟 基于 EQL 与神经网络的钙钛矿带隙建模

本项目利用 **EQL（Equation Learner）网络** 获取符号数学表达式，并将这些表达式作为编码器，用于引导神经网络建模 **钙钛矿材料组分与带隙之间的关系**。  
此外，本项目还实现了 **SENN（Symbolically Encoded Neural Network，符号编码神经网络）** 以及其他经典机器学习方法作为对比基线，从而同时分析模型的预测精度与可解释性。

---

## 📂 项目结构

<pre>
.
├── data/                # 数据集：钙钛矿组分与带隙数值
│   ├── data.csv         # 用于 EQL 的数据集
│   ├── train.csv        # 用于 SENN 和其他模型的训练数据
│   └── text.csv         # 用于 SENN 和其他模型的测试数据
├── EQL.py               # EQL 网络训练脚本，用于生成符号编码器
├── models/              # SENN 训练代码和其他机器学习基线模型
│   ├── senn.py
│   ├── rf.py            # 随机森林
│   ├── svr.py           # 支持向量回归
│   ├── linear.py        # 线性回归
│   └── gbdt.py          # 梯度提升树
└── README.md
</pre>

---

## ⚙️ 环境配置

首先，创建虚拟环境并安装依赖：

```bash
python -m venv .venv
source .venv/bin/activate    # Windows 系统使用：.venv\Scripts\activate
```

主要依赖包括：

```text
numpy
pandas
scikit-learn
torch
DySymNet  # 用于符号回归
```

---

## 🚀 使用方法

### 1. 训练 EQL 编码器

```bash
python EQL.py
```

### 2. 训练 SENN 和其他机器学习模型

进入 `models/` 目录，运行对应脚本：

```bash
python models/senn.py
python models/rf.py
python models/svr.py
python models/gbdt.py
```

---

## 📊 输出结果

预测结果会保存为 `.csv` 文件，其中包含真实带隙值与预测带隙值。

评价指标会保存为 `.txt` 文件，其中包括 R²、RMSE、MAE 等指标。

---

# SENN-Bandgap 快速使用

本项目已经提供了一个可直接安装使用的 SENN 带隙预测工具包。用户无需重新训练模型，只需要通过 `pip` 安装，即可输入钙钛矿组分并预测带隙。

模型输入顺序固定为：

```text
[MA, FA, Cs, Br, Cl, I]
```

其中 `MA`、`FA` 和 `Cs` 表示 A 位点组分比例，`Br`、`Cl` 和 `I` 表示 X 位点组分比例。

---

## 安装

```bash
pip install senn-bandgap
```

---

## Python 文件使用示例

新建一个 Python 文件，例如 `predict.py`：

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

运行：

```bash
python predict.py
```

---

## 命令行使用示例

安装后，也可以直接在终端中使用预测器：

```bash
senn-bandgap --MA 0 --FA 1 --Cs 0 --Br 0 --Cl 0 --I 1
```

示例输出：

```text
Predicted bandgap: 1.520524 eV
```

也可以输入混合组分：

```bash
senn-bandgap --MA 0 --FA 0.9 --Cs 0.1 --Br 0.2 --Cl 0 --I 0.8
```

---

## 输入要求

建议输入组分满足：

```text
MA + FA + Cs ≈ 1
Br + Cl + I ≈ 1
```

预测带隙的单位为：

```text
eV
```

## 🌐 在线网页演示

我们提供了一个基于 SENN 的钙钛矿带隙在线预测界面：

👉 [SENN-Bandgap 在线预测网页](https://senn-bandgap-web-qu64kxosjmv7z5ndz4jgca.streamlit.app/)

用户无需在本地安装 Python 包，即可直接输入钙钛矿组分比例，并获得对应的带隙预测结果。

## 📖 研究意义

EQL 网络能够生成符号表达式，并将其作为编码器，帮助神经网络捕捉潜在的物理关系。

SENN 和经典机器学习方法提供了对比基线，可用于从预测精度和可解释性两个角度评估模型表现。

该方法有助于理解钙钛矿组分与带隙调控之间的关系，为新材料设计提供数据驱动的研究路径。
