# 📊 母集団・標本・観測値

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=white)](https://www.python.org/)
[![R](https://img.shields.io/badge/R-4.0%2B-276DC3?logo=r&logoColor=white)](https://www.r-project.org/)
[![Jupyter Notebook](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter&logoColor=white)](https://jupyter.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Google Colab](https://img.shields.io/badge/Open%20in-Colab-F9AB00?logo=googlecolab&logoColor=white)](https://colab.research.google.com/)

> 数理統計学の根幹をなす「母集団・標本・観測値」を、シミュレーションと豊富な可視化で直感的に理解するための教材リポジトリです。Python版・R版の両方を収録しています。

---

## 📁 ファイル構成

```
.
├── statistics_demo.ipynb        # Python版（NumPy / matplotlib / scipy）
├── statistics_demo_R.ipynb      # R版（ggplot2 / dplyr / patchwork）
├── images/
│   ├── download-4.png
│   ├── population_vs_sample.png
│   ├── sampling_distribution.png
│   └── standard_error_relation.png
└── README.md
```

---

## 🖼️ 生成されるビジュアライゼーション

### 1. 母集団の分布
J国の成人男性の身長（N=10,000人、μ=171cm、σ=6cm）を正規分布で生成し、ヒストグラムとして可視化します。

![母集団の分布](image/download-4.png)

---

### 2. 母集団 vs 標本の比較
母集団から n=50 人を無作為抽出した標本と、母集団全体を並べて比較します。標本平均（x̄）が母平均（μ）に近いことを視覚的に確認できます。

![母集団 vs 標本](images/population_vs_sample.png)

---

### 3. 標本平均の標本分布（各1000回抽出）
標本サイズ n を 5, 10, 30, 50, 100, 500 と変えながら、各サイズで1000回の抽出を繰り返し、標本平均のヒストグラムを描きます。**nが大きいほど分布が狭くなる**＝推定精度が高くなることが一目瞭然です。

![標本平均の分布](images/sampling_distribution.png)

---

### 4. 標準誤差と標本サイズ・母集団・標本・観測値の関係
実測の標準誤差と理論値 σ/√n が一致することを示すグラフと、母集団→標本→観測値の概念図をあわせて表示します。

![標準誤差の関係](images/standard_error_relation.png)

---

## 🧮 数理統計学的解説

### 1. 母集団（Population）

**母集団**とは、研究・推測の対象となる個体すべての集合 $\mathcal{U}$ です。母集団のサイズを $N$ で表します。

母集団全体の確率分布が既知であれば、そのパラメータ（母数）として以下が定義されます。

$$
\mu = \frac{1}{N}\sum_{i=1}^{N} x_i \quad \text{（母平均）}
$$

$$
\sigma^2 = \frac{1}{N}\sum_{i=1}^{N}(x_i - \mu)^2 \quad \text{（母分散）}
$$

本教材では $\mu = 171\,\text{cm}$、$\sigma = 6\,\text{cm}$ の正規分布 $\mathcal{N}(\mu, \sigma^2)$ を母集団として使用しています。現実の統計分析では**母数は未知**であり、標本から推定するのが統計学の根本的な目標です。

---

### 2. 標本（Sample）

母集団の規模が大きい場合、全数調査は費用・時間・実行可能性の観点から困難です。そこで母集団から **無作為抽出（random sampling）** によって $n$ 個の個体を選び出した部分集合を**標本**といいます。

$$
\{X_1, X_2, \ldots, X_n\} \subseteq \mathcal{U}, \quad n \ll N
$$

無作為抽出の条件は次の2つです。

| 条件 | 内容 |
|------|------|
| **等確率性** | 各個体が同じ確率 $1/N$ で選ばれる |
| **独立性** | ある個体の選出が他の個体の選出に影響しない（復元抽出の場合） |

標本から計算される統計量（標本平均 $\bar{X}$、標本分散 $S^2$）は、母数の**推定量（estimator）**として機能します。

$$
\bar{X} = \frac{1}{n}\sum_{i=1}^{n} X_i
$$

$$
S^2 = \frac{1}{n-1}\sum_{i=1}^{n}(X_i - \bar{X})^2 \quad \text{（不偏分散）}
$$

$S^2$ の分母が $n-1$（自由度）である理由は、$\bar{X}$ を使って $\mu$ を代替することで1次元の情報が失われるためです（ベッセルの補正）。

---

### 3. 観測値（Observation）

**観測値**は、抽出された各標本個体に対して実際に計測・記録された具体的な数値です。$i$ 番目の観測値を $x_i$（実現値）として区別する場合もあります。

$$
\text{観測値} = \{x_1, x_2, \ldots, x_n\} = \{175.2,\; 168.7,\; 182.1,\; \ldots\}
$$

確率変数 $X_i$ は抽出前の「値が決まる前の状態」を表し、観測値 $x_i$ は実際に観測された後の「実現した値」を表す、という確率論上の区別が重要です。

---

### 4. 標本平均の標本分布と中心極限定理

標本平均 $\bar{X}$ は標本ごとに異なる値をとる確率変数です。その確率分布を**標本分布（sampling distribution）**といいます。

母集団の分布によらず、標本サイズ $n$ が十分大きければ、**中心極限定理（Central Limit Theorem; CLT）**により次が成り立ちます。

$$
\bar{X} \xrightarrow{d} \mathcal{N}\!\left(\mu,\; \frac{\sigma^2}{n}\right) \quad \text{as } n \to \infty
$$

これを言い換えると、

$$
Z = \frac{\bar{X} - \mu}{\sigma / \sqrt{n}} \xrightarrow{d} \mathcal{N}(0, 1)
$$

本教材のシミュレーションでは、$n=5$ の場合でも平均 171cm 付近に分布が集中し始め、$n=500$ ではほぼ点状に集中する様子が確認できます。

---

### 5. 標準誤差（Standard Error; SE）

標本平均の標準偏差を**標準誤差**といい、推定の「精度」を表す指標です。

$$
\text{SE} = \frac{\sigma}{\sqrt{n}}
$$

| 標本サイズ $n$ | 理論的な SE（σ=6） |
|:--------------:|:-----------------:|
| 5              | 2.68 cm           |
| 10             | 1.90 cm           |
| 30             | 1.10 cm           |
| 50             | 0.85 cm           |
| 100            | 0.60 cm           |
| 500            | 0.27 cm           |

SEは $\sqrt{n}$ に反比例して減少するため、精度を2倍にするには**標本サイズを4倍**にする必要があります。これは調査設計において重要なトレードオフです。

---

### 6. 推定の枠組み：点推定と区間推定

#### 点推定（Point Estimation）
標本統計量を用いて母数を1つの値で推定します。標本平均 $\bar{X}$ は母平均 $\mu$ の**不偏推定量（unbiased estimator）**です。

$$
E[\bar{X}] = \mu
$$

#### 区間推定（Interval Estimation）
母平均の 95% 信頼区間（CI）は次のように計算されます。

$$
\bar{X} \pm 1.96 \cdot \frac{S}{\sqrt{n}}
$$

この区間は「同じ手順で区間を繰り返し構成した場合、長期的に 95% の区間が真の母平均 μ を含む」ことを意味します（頻度論的解釈）。

---

### 7. 概念の階層まとめ

```
母集団 (Population)
│  N = 10,000 人、μ = 171 cm、σ = 6 cm
│
│  ← 無作為抽出 (Random Sampling)
▼
標本 (Sample)
│  n = 50 人、x̄ = 171.4 cm、S = 5.9 cm
│
│  ← 各個体を測定 (Observation)
▼
観測値 (Observations)
   175.2, 168.7, 182.1, 170.3, ...
```

| 概念 | 記号 | 性質 |
|------|------|------|
| 母平均 | $\mu$ | 固定された定数（未知） |
| 母標準偏差 | $\sigma$ | 固定された定数（未知） |
| 標本平均 | $\bar{X}$ | 標本ごとに変わる確率変数 |
| 標本標準偏差 | $S$ | 標本ごとに変わる確率変数 |
| 標準誤差 | $\text{SE} = \sigma/\sqrt{n}$ | 推定精度の指標 |

---

## 🚀 使い方

### Python版（Jupyter / Google Colab）

```bash
git clone https://github.com/yourname/statistics-demo.git
cd statistics-demo
pip install numpy matplotlib pandas scipy japanize-matplotlib
jupyter notebook statistics_demo.ipynb
```

または、Google Colab でそのまま開くことができます。

### R版（Jupyter / RStudio）

```r
install.packages(c("ggplot2", "dplyr", "tidyr", "patchwork"))
```

Jupyter で R カーネルを使う場合は `IRkernel` をインストールしてください。

```r
install.packages("IRkernel")
IRkernel::installspec()
```

---

## 📦 使用ライブラリ

**Python**

| ライブラリ | 用途 |
|------------|------|
| `numpy` | 乱数生成・数値計算 |
| `matplotlib` | グラフ描画 |
| `scipy.stats` | 統計関数 |
| `pandas` | データ集計 |
| `japanize-matplotlib` | 日本語フォント対応 |

**R**

| パッケージ | 用途 |
|------------|------|
| `ggplot2` | グラフ描画 |
| `dplyr` | データ操作 |
| `tidyr` | データ整形 |
| `patchwork` | 複数プロット結合 |

---

## 📚 参考文献

- 竹内啓 (2014)『数理統計学 — データ解析の方法』東洋経済新報社
- Casella, G. & Berger, R.L. (2002). *Statistical Inference* (2nd ed.). Duxbury Press.
- 久保拓弥 (2012)『データ解析のための統計モデリング入門』岩波書店

---

## 📝 ライセンス

MIT License — 教育目的での自由な利用・改変を歓迎します。
