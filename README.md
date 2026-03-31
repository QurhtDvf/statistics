# 📐 数理統計学

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=white)](https://www.python.org/)
[![R](https://img.shields.io/badge/R-4.0%2B-276DC3?logo=r&logoColor=white)](https://www.r-project.org/)
[![Jupyter Notebook](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter&logoColor=white)](https://jupyter.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Google Colab](https://img.shields.io/badge/Open%20in-Colab-F9AB00?logo=googlecolab&logoColor=white)](https://colab.research.google.com/)

> **「データから真実を推論する」**——この一文が、数理統計学の存在意義をすべて言い表しています。  
> 本ドキュメントでは、数理統計学とは何か、どのように発展してきたか、そして現代の機械学習・大規模言語モデル（LLM）とどう関連しているかを体系的に解説します。

---

## 目次

1. [数理統計学とは何か](#1-数理統計学とは何か)
2. [数理統計学の歴史](#2-数理統計学の歴史)
3. [機械学習・LLMとの関係](#3-機械学習llmへの接続)
4. [参考文献](#7-参考文献)

---

## 1. 数理統計学とは何か

### 1.1 定義と立ち位置

**数理統計学**（Mathematical Statistics） とは、**確率論**を基盤として「不完全なデータから母集団の性質を科学的・論理的に推論する」ための理論体系です。

```
確率論（Probability Theory）
    ↓  演繹的：既知のモデル → データの振る舞いを予測
数理統計学（Mathematical Statistics）
    ↓  帰納的：観測されたデータ → 未知のモデル・母数を推定
データサイエンス／機械学習（Data Science / ML）
    ↓  拡張：高次元・非線形・大規模データへの適用
大規模言語モデル（LLM）
       自然言語という「データ」から世界の構造を学習
```

確率論が「コインを投げたとき表が出る確率は 0.5 である、では10回投げると何回表が出るか？」と問うのに対し、数理統計学は「10回投げて7回表が出た、このコインは公平か？」と問います。方向が逆なのです。

### 1.2 数理統計学の3本柱

数理統計学は大きく以下の3領域に分類されます。

| 領域 | 問い | 代表的手法 |
|------|------|-----------|
| **記述統計 (Descriptive Statistics)** | データをどう要約するか | 平均・分散・分位数・相関係数 |
| **推測統計 (Inferential Statistics)** | 標本から母集団をどう推定するか | 点推定・区間推定・仮説検定 |
| **ベイズ統計 (Bayesian Statistics)** | 事前知識とデータをどう統合するか | ベイズ推定・MCMC・変分推論 |

### 1.3 数理統計学が解く問題の構造

すべての統計的推論は、次の構造を持っています。

$$
\underbrace{X_1, X_2, \ldots, X_n}_{\text{観測データ（標本）}} \sim \underbrace{p(x \mid \theta)}_{\text{未知の確率モデル}}
$$

目標は、観測データ $\{X_i\}$ から未知パラメータ $\theta$ を推定することです。

点推定では推定量 $\hat{\theta}$ を構成し、その性質（不偏性・一致性・有効性）を評価します。

$$
\hat{\theta}_{\text{MLE}} = \arg\max_{\theta} \sum_{i=1}^{n} \log p(x_i \mid \theta) \quad \text{（最尤推定）}
$$

区間推定では信頼区間を構成します。

$$
P\!\left(\hat{\theta}_L \leq \theta \leq \hat{\theta}_U\right) = 1 - \alpha
$$

**仮説検定**では帰無仮説 $H_0$ の棄却・採択を、第一種過誤の確率（有意水準 $\alpha$）を制御しながら判断します。

### 1.4 数理統計学が扱う主要概念

```
数理統計学
├── 確率分布論
│   ├── 正規分布・t分布・χ²分布・F分布
│   ├── 指数型分布族（Exponential Family）
│   └── 十分統計量（Sufficient Statistic）
├── 推定理論
│   ├── 最尤推定（MLE）
│   ├── ベイズ推定（MAP・事後分布）
│   ├── クラメール・ラオ下界（CRLB）
│   └── 不偏性・一致性・有効性
├── 仮説検定
│   ├── ネイマン・ピアソン理論
│   ├── 尤度比検定
│   └── p値・検出力・効果量
└── 漸近理論
    ├── 大数の法則（LLN）
    ├── 中心極限定理（CLT）
    └── デルタ法
```

---

## 2. 数理統計学の歴史

数理統計学の歴史は、単なる「計算技術の歴史」ではありません。それは「データから何がわかるか」という問いそのものの深化の歴史であり、現代AIへと直線的につながっています。

### 2.1 黎明期：確率論の誕生（17〜18世紀）

| 年代 | 人物・出来事 | 内容 |
|------|-------------|------|
| 1654 | **パスカル & フェルマー** | ギャンブル問題の書簡往復 → 確率論の誕生 |
| 1713 | **ヤコブ・ベルヌーイ** | 『推測術（Ars Conjectandi）』— 大数の法則の初証明 |
| 1763 | **トーマス・ベイズ** | 「逆確率」の論文 → ベイズの定理 $P(\theta\|x) \propto P(x\|\theta)P(\theta)$ |
| 1812 | **ピエール＝シモン・ラプラス** | 『確率の解析理論』— 中心極限定理の先駆、確率論の体系化 |

> 🔗 **LLMとの関係**：ベイズの定理は、LLMが次のトークンを予測する際の条件付き確率 $P(\text{次の単語} \mid \text{これまでの文脈})$ の理論的根拠そのものです。

---

### 2.2 統計学の制度化：記述から推測へ（19世紀）

| 年代 | 人物・出来事 | 内容 |
|------|-------------|------|
| 1809 | **カール・フリードリヒ・ガウス** | 最小二乗法の体系化。誤差の正規分布モデル $\varepsilon \sim \mathcal{N}(0, \sigma^2)$ |
| 1835 | **アドルフ・ケトレー** | 社会統計に正規分布を応用。「平均的人間（l'homme moyen）」の概念 |
| 1869 | **フランシス・ゴルトン** | 回帰（Regression）の発見。親子の身長の関係を研究 |
| 1896 | **カール・ピアソン** | 相関係数 $r$、$\chi^2$ 検定、モーメント法を体系化 |

ガウスが定式化した**最小二乗法（OLS: Ordinary Least Squares）**は、

$$
\hat{\boldsymbol{\beta}} = \arg\min_{\boldsymbol{\beta}} \|\mathbf{y} - \mathbf{X}\boldsymbol{\beta}\|^2 = (\mathbf{X}^\top \mathbf{X})^{-1}\mathbf{X}^\top \mathbf{y}
$$

という形で、現代の線形回帰・ニューラルネットワークの勾配降下法の直系の祖先です。

> 🔗 **機械学習との関係**：線形回帰はすべての教師あり学習の原型です。ニューラルネットワークの損失関数最小化は、最小二乗法の非線形・高次元拡張と見なせます。

---

### 2.3 推測統計学の確立：フィッシャー革命（1910〜1930年代）

20世紀初頭、**ロナルド・A・フィッシャー（Ronald A. Fisher）** は統計学を根本から変革しました。

| 業績 | 内容 | 現代への影響 |
|------|------|-------------|
| **最尤推定（MLE, 1922）** | $\hat{\theta} = \arg\max_\theta \mathcal{L}(\theta; \mathbf{x})$ | 深層学習の損失関数設計の原理 |
| **十分統計量（1922）** | データの情報を損なわない圧縮 | 情報ボトルネック理論・表現学習へ |
| **フィッシャー情報量（1925）** | $\mathcal{I}(\theta) = -E\!\left[\frac{\partial^2 \log p}{\partial \theta^2}\right]$ | クラメール・ラオ下界、自然勾配法 |
| **分散分析（ANOVA, 1925）** | グループ間差異の検定 | 実験計画・A/Bテスト |
| **実験計画法（1935）** | 無作為化・反復・ブロック化の原理 | 機械学習の交差検証・ランダム化の設計 |

フィッシャー情報量は、モデルのパラメータ推定の理論的限界を与えます。

$$
\text{Var}(\hat{\theta}) \geq \frac{1}{\mathcal{I}(\theta)} \quad \text{（クラメール・ラオ下界）}
$$

> 🔗 **深層学習への接続**：自然勾配降下法（Natural Gradient Descent）はフィッシャー情報行列を使って損失関数の曲率を補正します。Transformer の学習安定化技術はこの延長線上にあります。

---

### 2.4 ネイマン・ピアソン理論と検定の形式化（1930年代）

**イェジー・ネイマン**と**エゴン・ピアソン**は、フィッシャーの「有意性検定」を批判し、仮説検定に厳密な数学的枠組みを与えました。

$$
H_0: \theta = \theta_0 \quad \text{vs} \quad H_1: \theta \neq \theta_0
$$

| 概念 | 記号 | 意味 |
|------|------|------|
| 第一種過誤（偽陽性） | $\alpha = P(\text{棄却} \mid H_0 \text{が真})$ | 有意水準として制御 |
| 第二種過誤（偽陰性） | $\beta = P(\text{採択} \mid H_1 \text{が真})$ | 小さいほど検出力が高い |
| 検出力 | $1-\beta$ | モデル評価指標と同根 |

> 🔗 **機械学習への接続**：機械学習の**精度（Precision）・再現率（Recall）・ROC曲線**は、第一種過誤・第二種過誤のトレードオフをそのまま引き継いでいます。分類器の評価理論は、ネイマン・ピアソン理論の直接的な応用です。

---

### 2.5 情報理論との融合（1940〜50年代）

| 年代 | 人物・出来事 | 内容 |
|------|-------------|------|
| 1948 | **クロード・シャノン** | 情報エントロピー $H = -\sum p_i \log p_i$ の定義。情報理論の創設 |
| 1951 | **ソロモン・クルバック** | KLダイバージェンス（相対エントロピー）の導入 |
| 1954 | **アブラハム・ワルド** | 統計的決定理論の完成 |

シャノンのエントロピーとKLダイバージェンスは、統計学と情報理論を結びつける橋梁になりました。

$$
D_{\text{KL}}(P \| Q) = \sum_x P(x) \log \frac{P(x)}{Q(x)}
$$

> 🔗 **LLMへの接続**：LLMの学習における交差エントロピー損失（Cross-Entropy Loss）は、
> $$\mathcal{L} = -\sum_{t} \log P_\theta(w_t \mid w_1, \ldots, w_{t-1})$$
> であり、これはモデル分布 $P_\theta$ と真のデータ分布 $P_{\text{data}}$ の KLダイバージェンスを最小化することと等価です。LLMが「次の単語を予測する」訓練は、情報理論と統計学の直接の産物です。

---

### 2.6 ベイズ統計の復興と計算統計学（1950〜90年代）

長年、ベイズ統計は「事前分布の主観性」という批判から傍流に置かれていました。しかし計算機の発展とともに状況は一変します。

| 年代 | 出来事 | 内容 |
|------|--------|------|
| 1953 | **メトロポリス法** | マルコフ連鎖モンテカルロ（MCMC）の原型 |
| 1977 | **EM アルゴリズム（Dempster et al.）** | 潜在変数モデルの最尤推定。混合ガウス分布、HMM |
| 1983 | **ギブスサンプラー** | 高次元ベイズ推定の実用化 |
| 1990s | **変分推論（Variational Inference）** | 事後分布の近似。計算コストの大幅削減 |

EMアルゴリズムは次の反復で最尤推定を実現します。

$$
\text{E-step:} \quad Q(\theta \mid \theta^{(t)}) = E_{\mathbf{Z}|\mathbf{X},\theta^{(t)}}[\log p(\mathbf{X}, \mathbf{Z} \mid \theta)]
$$
$$
\text{M-step:} \quad \theta^{(t+1)} = \arg\max_\theta\, Q(\theta \mid \theta^{(t)})
$$

> 🔗 **深層生成モデルへの接続**：**変分オートエンコーダ（VAE）** の ELBO（証拠下界）最大化は変分推論の深層学習への直接拡張です。**拡散モデル（Diffusion Models）** の訓練もベイズ推論の枠組みで理解できます。

---

### 2.7 機械学習との融合（1990〜2010年代）

この時代、統計学と計算機科学は急速に融合しました。

| 年代 | 出来事 | 統計学との接続 |
|------|--------|--------------|
| 1995 | **サポートベクターマシン（SVM）** | 構造的リスク最小化、マージン最大化 |
| 1997 | **LSTM（Hochreiter & Schmidhuber）** | 系列データの確率モデル |
| 2001 | **ランダムフォレスト（Breiman）** | ブートストラップ集約（Bagging）＋アンサンブル学習 |
| 2006 | **深層信念ネットワーク（Hinton）** | 制限ボルツマンマシン、確率的グラフィカルモデル |
| 2012 | **AlexNet（Krizhevsky et al.）** | 深層学習の実用化。確率的勾配降下法（SGD）の大規模適用 |

**確率的勾配降下法（SGD）** は、大数の法則の応用です。

$$
\nabla_\theta \mathcal{L}(\theta) = \frac{1}{N}\sum_{i=1}^N \nabla_\theta \ell(x_i, \theta) \approx \frac{1}{|B|}\sum_{i \in B} \nabla_\theta \ell(x_i, \theta)
$$

ミニバッチ $B$ による勾配の推定は、母集団の勾配を標本で推定する行為にほかなりません。

---

### 2.8 大規模言語モデルの時代（2017年〜現在）

| 年代 | 出来事 | 統計学との接続 |
|------|--------|--------------|
| 2017 | **Transformer（Vaswani et al.）** | Attention = 条件付き確率の重み付き集約 |
| 2018 | **BERT / GPT** | 自己回帰モデル・マスク言語モデル（確率分布の推定） |
| 2020 | **GPT-3（175B パラメータ）** | スケール則（べき乗則）の実証 |
| 2022 | **ChatGPT / InstructGPT** | RLHF：強化学習＋ベイズ的報酬モデル |
| 2023〜 | **GPT-4, Claude, Gemini** | 多モーダル・推論強化・エージェント化 |

---

## 3. 機械学習・LLMとの関係

### 3.1 対応関係の全体図

数理統計学の概念が機械学習・LLMにどう対応するかを一覧で示します。

| 数理統計学の概念 | 機械学習・LLMでの対応物 |
|----------------|----------------------|
| 母集団 $p(x)$ | **真のデータ分布**（学習データの生成源） |
| 標本 $\{x_i\}_{i=1}^n$ | **訓練データセット** |
| パラメータ推定 $\hat{\theta}$ | **モデルの重み学習**（$\arg\min \mathcal{L}$） |
| 最尤推定（MLE） | **交差エントロピー最小化**（分類・言語モデル） |
| 最小二乗法（OLS） | **MSE 最小化**（回帰・拡散モデルのノイズ予測） |
| 過学習・汎化誤差 | **バイアス・バリアンストレードオフ** |
| 正則化（Ridge/Lasso） | **Weight Decay / L1・L2 正則化** |
| 交差検証（CV） | **ホールドアウト検証・k-fold CV** |
| ベイズ推定 | **事前分布＝重み初期化・正則化の確率的解釈** |
| KLダイバージェンス | **VAE の ELBO・RLHF の KL ペナルティ** |
| 中心極限定理 | **SGD の収束保証・バッチ正規化の理論的根拠** |
| 十分統計量 | **表現学習（Representation Learning）** |
| フィッシャー情報量 | **自然勾配法（Natural Gradient）** |

### 3.2 LLMの確率的本質

LLMは本質的に**条件付き確率分布の推定器**です。

$$
P_\theta(w_1, w_2, \ldots, w_T) = \prod_{t=1}^{T} P_\theta(w_t \mid w_1, \ldots, w_{t-1})
$$

この自己回帰分解は、確率の連鎖律（Chain Rule of Probability）そのものです。Transformerはこの条件付き分布を Attention 機構によって近似します。

$$
\text{Attention}(Q, K, V) = \text{softmax}\!\left(\frac{QK^\top}{\sqrt{d_k}}\right)V
$$

softmax は多項分布のパラメータを出力する**正規化関数**であり、これもまた統計学の指数型分布族の枠組みで理解できます。

### 3.3 RLHF（人間フィードバックによる強化学習）と統計学

ChatGPT などに使われる **RLHF（Reinforcement Learning from Human Feedback）** は、次の統計的枠組みで構成されます。

```
Step 1: 教師あり学習（SFT）
    → 最尤推定：P_θ(y|x) の最大化

Step 2: 報酬モデルの学習
    → ブラッドリー・テリーモデル（Bradley-Terry Model）
       P(y_A ≻ y_B) = σ(r(y_A) - r(y_B))
       （ロジスティック回帰の一種）

Step 3: PPO による方策最適化
    → KL 制約付き最大化：
       max_θ E[r(y)] - β · D_KL(π_θ || π_ref)
```

KLダイバージェンスによる制約は、モデルが事前分布（参照方策）から大きく外れないようにするベイズ的正則化と解釈できます。

### 3.4 スケール則（Scaling Laws）と統計的推定

Kaplan et al. (2020) が実証した**スケール則**は、統計学の漸近理論の現代的展開です。

$$
\mathcal{L}(N) \sim N^{-\alpha}, \quad \mathcal{L}(D) \sim D^{-\beta}, \quad \mathcal{L}(C) \sim C^{-\gamma}
$$

ここで $N$ はパラメータ数、$D$ はデータ量、$C$ は計算量です。これは、標本サイズ $n$ の増加に伴う推定誤差の収束率（$O(1/\sqrt{n})$）のパラメトリック拡張と見なすことができます。

---

## 4. 参考文献

**数理統計学の基礎**
- 竹内啓 (2014)『数理統計学 — データ解析の方法』東洋経済新報社
- Casella, G. & Berger, R.L. (2002). *Statistical Inference* (2nd ed.). Duxbury Press.
- Fisher, R.A. (1922). On the mathematical foundations of theoretical statistics. *Phil. Trans. R. Soc. A*, 222, 309–368.

**情報理論・ベイズ統計**
- Shannon, C.E. (1948). A mathematical theory of communication. *Bell System Technical Journal*, 27(3), 379–423.
- Bishop, C.M. (2006). *Pattern Recognition and Machine Learning*. Springer.
- 久保拓弥 (2012)『データ解析のための統計モデリング入門』岩波書店

**機械学習・深層学習**
- Goodfellow, I., Bengio, Y. & Courville, A. (2016). *Deep Learning*. MIT Press.
- Kaplan, J. et al. (2020). Scaling Laws for Neural Language Models. *arXiv:2001.08361*.

**LLM・RLHF**
- Vaswani, A. et al. (2017). Attention Is All You Need. *NeurIPS 2017*.
- Ouyang, L. et al. (2022). Training language models to follow instructions with human feedback. *NeurIPS 2022*.

---

## 📝 ライセンス

MIT License — 教育目的での自由な利用・改変を歓迎します。
