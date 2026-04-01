# 確率の公理と性質

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python)](https://colab.research.google.com/)
[![R](https://img.shields.io/badge/R-4.3%2B-276DC3?logo=r)](https://colab.research.google.com/)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

数理統計学の基礎となる**コルモゴロフの確率の公理**と、そこから導出される重要な性質を、モンテカルロシミュレーションと可視化を通じて体験的に学ぶ Jupyter Notebook です。Python 版・R 版の両方を用意しています。

---

## 目次

- [背景と数理統計学的意義](#背景と数理統計学的意義)
- [コルモゴロフの公理の詳細](#コルモゴロフの公理の詳細)
- [公理から導出される性質](#公理から導出される性質)
- [デモの構成](#デモの構成)
- [環境と実行方法](#環境と実行方法)
- [使用ライブラリ](#使用ライブラリ)
- [ファイル構成](#ファイル構成)

---

## 背景と数理統計学的意義

### 確率論の公理化以前

20世紀初頭まで、確率の概念は「コインを投げたとき表が出る確率は 1/2」のような**頻度論的直観**や、「対称性から各事象は等確率」という**ラプラスの古典的定義**に基づいていました。しかしこれらの定義には次のような限界がありました：

- **頻度論的定義**：無限回試行という概念を用いており、循環論法になりやすい。また、反復不可能な事象（「明日雨が降る確率」など）に適用しにくい。
- **古典的定義**：「等確率」を前提とするため、等確率でない事象（歪んだコインなど）を扱えない。

### コルモゴロフによる公理化（1933年）

ソ連の数学者 **アンドレイ・コルモゴロフ（Andrei Kolmogorov）** は 1933 年の著書 *Grundbegriffe der Wahrscheinlichkeitsrechnung*（確率論の基礎概念）において、確率を **測度論（Measure Theory）** の枠組みで厳密に公理化しました。

この公理化の意義は：

1. **完全な厳密性**：直観や曖昧さに依存せず、3 つの公理のみから確率論全体を演繹的に構築できる。
2. **統一的な枠組み**：離散・連続・混合型の任意の確率空間を同一の枠組みで扱える。
3. **数理統計学の基礎**：推定論・検定論・ベイズ統計など、現代統計学のあらゆる理論がこの公理系の上に構築されている。

---

## コルモゴロフの公理の詳細

### 確率空間の定義

確率論の舞台は**確率空間**（Probability Space）$(\Omega, \mathcal{F}, P)$ の三つ組で定義されます。

| 記号 | 名称 | 意味 |
|------|------|------|
| $\Omega$ | 標本空間（Sample Space） | すべての起こりうる結果の集合 |
| $\mathcal{F}$ | $\sigma$-加法族（$\sigma$-algebra） | 確率を定義できる事象の集合族 |
| $P$ | 確率測度（Probability Measure） | 各事象に確率を割り当てる関数 |

> **サイコロの例**： $\Omega = \{1, 2, 3, 4, 5, 6\}$、$\mathcal{F} = 2^\Omega$ （べき集合）、 $P(\{k\}) = 1/6$

### 公理1：非負性（Non-negativity）

$$P(A) \geq 0 \quad \forall A \in \mathcal{F}$$

**直観的意味**：確率は負にならない。「ある事象が起こる可能性がマイナス」というのは意味をなさない。

**数理的含意**：確率測度は非負値測度（Non-negative measure）であり、これにより $P$ が距離・ノルムのような幾何学的性質を持つことが保証される。この性質は、後にチェビシェフの不等式・マルコフの不等式などの確率的不等式の証明に不可欠となる。

### 公理2：全確率（Normalization / Unitarity）

$$P(\Omega) = 1$$

**直観的意味**：標本空間全体（=何らかの結果が必ず起きる）の確率は 1 である。これは確率の「スケール」を定める規格化条件である。

**数理的含意**：この条件により確率測度は**有限測度**（Total Measure = 1）となる。一般の測度論における $\sigma$-有限測度とは異なり、確率測度は必ず全測度が 1 に正規化されている点が特徴的である。この条件から補事象の公式 $P(A^c) = 1 - P(A)$ が直ちに導かれる。

### 公理3：加法性（Countable Additivity / $\sigma$-additivity）

$$A \cap B = \emptyset \Rightarrow P(A \cup B) = P(A) + P(B)$$

より一般的には、**可算加法性**（$\sigma$-加法性）として：

$$P(A_1 \cup A_2 \cup \cdots) = \sum_{i=1}^{\infty} P(A_i) \qquad (A_i \cap A_j = \emptyset \text{ for } i \neq j)$$

**直観的意味**：互いに排反な（同時に起こりえない）事象の確率は足し合わせることができる。

**数理的含意**：この公理は確率論において最も強力かつ微妙な性質である。単なる有限加法性（Finite Additivity）ではなく**可算加法性**を要求することが測度論的確率論の核心であり、これにより：

- **連続性**：$A_n \nearrow A$ ならば $P(A_n) \to P(A)$（測度の上からの連続性）
- **大数の法則**（弱・強）の厳密な証明
- **中心極限定理**の証明

が可能となる。なお、有限加法性のみを仮定する「フィンレッティ流の主観確率論」も存在するが、コルモゴロフ流では可算加法性が標準的に採用される。

---

## 公理から導出される性質

以下の性質はすべて上記 3 公理の論理的帰結（定理）であり、追加の仮定を一切必要としません。

### 1. 空事象の確率

$$P(\emptyset) = 0$$

**証明**：$\Omega \cap \emptyset = \emptyset$ より公理3から $P(\Omega \cup \emptyset) = P(\Omega) + P(\emptyset)$。左辺は $P(\Omega) = 1$（公理2）なので $P(\emptyset) = 0$。$\blacksquare$

### 2. 補事象の確率

$$P(A^c) = 1 - P(A)$$

**証明**：$A \cap A^c = \emptyset$、$A \cup A^c = \Omega$ より公理3から $P(A) + P(A^c) = P(\Omega) = 1$。$\blacksquare$

**統計的応用**：仮説検定における $p$ 値の計算（$P(\text{棄却域}) = \alpha$）や、信頼区間（信頼係数 $1-\alpha$）の定義に直接使われる。

### 3. 単調性（Monotonicity）

$$A \subseteq B \Rightarrow P(A) \leq P(B)$$

**証明**：$B = A \cup (B \setminus A)$ かつ $A \cap (B \setminus A) = \emptyset$ より、$P(B) = P(A) + P(B \setminus A) \geq P(A)$（公理1より $P(B \setminus A) \geq 0$）。$\blacksquare$

**統計的応用**：検出力関数の単調性証明、信頼区間の包含関係の議論など。

### 4. 有界性

$$0 \leq P(A) \leq 1$$

**証明**：$\emptyset \subseteq A \subseteq \Omega$ より単調性から $P(\emptyset) \leq P(A) \leq P(\Omega)$、すなわち $0 \leq P(A) \leq 1$。$\blacksquare$

### 5. 包除原理（Inclusion-Exclusion Principle）

$$P(A \cup B) = P(A) + P(B) - P(A \cap B)$$

**証明**：$A \cup B = A \cup (B \setminus A)$（排反分解）より $P(A \cup B) = P(A) + P(B \setminus A)$。また $B = (A \cap B) \cup (B \setminus A)$ より $P(B \setminus A) = P(B) - P(A \cap B)$。代入すると公式が得られる。$\blacksquare$

**一般化**（$n$ 事象の包除原理）：

$$P(A_1 \cup \cdots \cup A_n) = \sum_i P(A_i) - \sum_{i<j} P(A_i \cap A_j) + \sum_{i<j<k} P(A_i \cap A_j \cap A_k) - \cdots$$

**統計的応用**：ボンフェローニ不等式（多重検定補正）はこの包除原理の上界・下界として導出される。

### 6. 大数の法則（Law of Large Numbers）との接続

大数の法則はコルモゴロフの公理系から厳密に証明される定理であり、確率の「頻度的解釈」を正当化します。

**弱大数の法則（Weak LLN）**：$X_1, X_2, \ldots$ が独立同分布で $E[X_i] = \mu < \infty$ ならば、

$$\bar{X}_n = \frac{1}{n}\sum_{i=1}^n X_i \xrightarrow{P} \mu \quad (n \to \infty)$$

**強大数の法則（Strong LLN、コルモゴロフ）**：さらに $E[|X_i|] < \infty$ ならば、

$$P(\bar{X}_n \to \mu \text{ as } n \to \infty) = 1$$

本デモでは、経験確率（相対頻度）$\hat{p}_n = \frac{1}{n}\sum_{i=1}^n \mathbf{1}_A(\omega_i)$ が真の確率 $P(A)$ に収束する様子を可視化することで、この定理を直感的に確認します。

---

## デモの構成

| セル | 内容 | 確認する性質 |
|------|------|------|
| 3 | 非負性のデモ | $P(A) \geq 0$ |
| 4 | 全確率のデモ | $P(\Omega) = 1$ |
| 5 | 加法性のデモ（排反） | $P(A \cup B) = P(A) + P(B)$ |
| 6-1 | 補事象 | $P(A^c) = 1 - P(A)$ |
| 6-2 | 包除原理 | $P(A \cup B) = P(A) + P(B) - P(A \cap B)$ |
| 6-3 | 単調性 | $A \subseteq B \Rightarrow P(A) \leq P(B)$ |
| 7 | 大数の法則 | 経験確率 $\xrightarrow{n\to\infty} P(A)$ |

### シミュレーション設計の方針

- **標本空間**：サイコロ投げ $\Omega = \{1,2,3,4,5,6\}$（各事象の理論値が $k/6$ と明快）
- **試行回数**：$10{,}000 \sim 50{,}000$ 回（大数の法則の収束が視覚的に明確になる規模）
- **再現性**：`set.seed(42)` / `np.random.seed(42)` により結果を固定
- **可視化**：棒グラフ・円グラフ・ベン図・収束グラフの 4 種類を用途に応じて使い分け

---

## 環境と実行方法

### Google Colab での実行（推奨）

**Python 版**

1. [Google Colab](https://colab.research.google.com/) を開く
2. `probability_axioms_demo.ipynb` をアップロード
3. 「ランタイム」→「すべてのセルを実行」

**R 版**

1. [Google Colab](https://colab.research.google.com/) を開く
2. `probability_axioms_demo_R.ipynb` をアップロード
3. 「ランタイム」→「ランタイムのタイプを変更」→ **R** を選択
4. 「ランタイム」→「すべてのセルを実行」

> **注意**：R 版はセル1でパッケージのインストールと日本語フォント（Noto Sans JP）のダウンロードを行います。初回実行時はネットワーク環境によって数分かかる場合があります。

### ローカル環境での実行

**Python 版**

```bash
pip install numpy matplotlib matplotlib-venn japanize-matplotlib jupyter
jupyter notebook probability_axioms_demo.ipynb
```

**R 版**

```r
install.packages(c("IRkernel", "ggplot2", "dplyr", "tidyr",
                   "patchwork", "ggvenn", "scales", "showtext"))
IRkernel::installspec()
```

```bash
jupyter notebook probability_axioms_demo_R.ipynb
```

---

## 使用ライブラリ

### Python 版

| ライブラリ | バージョン | 用途 |
|-----------|-----------|------|
| `numpy` | ≥ 1.24 | 乱数生成・配列演算 |
| `matplotlib` | ≥ 3.7 | グラフ描画 |
| `matplotlib-venn` | ≥ 0.11 | ベン図の描画 |
| `japanize-matplotlib` | ≥ 1.1 | 日本語フォント対応 |

### R 版

| パッケージ | バージョン | 用途 |
|-----------|-----------|------|
| `ggplot2` | ≥ 3.4 | グラフ描画（Grammar of Graphics） |
| `dplyr` | ≥ 1.1 | データ操作 |
| `tidyr` | ≥ 1.3 | データ整形（`pivot_longer` 等） |
| `patchwork` | ≥ 1.1 | 複数グラフの配置 |
| `ggvenn` | ≥ 0.1 | ベン図の描画 |
| `scales` | ≥ 1.2 | 軸ラベルの書式設定 |
| `showtext` | ≥ 0.9 | 日本語フォント対応 |

---

## ファイル構成

```
.
├── README.md
├── probability_axioms_demo.ipynb      # Python版ノートブック
└── probability_axioms_demo_R.ipynb    # R版ノートブック
```

---

## 参考文献

- Kolmogorov, A. N. (1933). *Grundbegriffe der Wahrscheinlichkeitsrechnung*. Springer.（英訳: *Foundations of the Theory of Probability*, Chelsea, 1956）
- 伊藤清 (1991). 『確率論』. 岩波書店.
- 測度と確率（東京大学出版会）
- Billingsley, P. (1995). *Probability and Measure* (3rd ed.). Wiley.
- Durrett, R. (2019). *Probability: Theory and Examples* (5th ed.). Cambridge University Press.

---

## ライセンス

MIT License © 2024
