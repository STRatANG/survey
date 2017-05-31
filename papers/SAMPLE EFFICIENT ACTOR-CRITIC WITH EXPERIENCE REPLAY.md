# SAMPLE EFFICIENT ACTOR-CRITIC WITH EXPERIENCE REPLAY

<!-----------------------------------------------------------------
# サムネイル
------------------------------------------------------------------->
<!-- <img src='../tmb/template.png' width=750px /> -->


<!-----------------------------------------------------------------
# 関連情報記述欄

論文リンク・出版年以外はoptional

-------
EXAMPLE
-------

- 論文リンク: https://arxiv.org/abs/1611.01626
- 出版年: 2017
- ジャーナル・カンファレンス: ICLR
- 著者: Brendan O'Donoghue, Remi Munos, Koray Kavukcuoglu, Volodymyr Mnih
- 所属: DeepMind
- 関連リンク:
- [openreview](https://openreview.net/forum?id=B1kJ6H9ex)
- タグ:
- :q-learning:
- :policy gradient:
- :atari:
- :neural network:
------------------------------------------------------------------->
- 論文リンク: https://arxiv.org/abs/1611.01224
- 出版年: 2017
- ジャーナル・カンファレンス: ICLR
- 著者: Ziyu Wang, Victor Bapst, Nicolas Heess, Volodymyr Mnih, Remi Munos, Koray Kavukcuoglu, Nando de Freitas
- 所属: DeepMind, CIFAR, Oxford University
<!--
- 関連リンク:
-
-->
- タグ:
- :actor-critic:
- :experience replay:
- :sample efficiency:
- :policy gradient:
- :atari:
- :mujoco:
- :neural network:


<!-----------------------------------------------------------------
# 論文内容まとめ記述欄

概要以外はoptional

-------
EXAMPLE
-------

#### 概要
エントロピー正則化付きの方策勾配法とQ学習を組み合わせた新しいアルゴリズムPGQを提案し、DQNやA3Cに対する優位性をAtariドメインで実験的に示した。

#### 目的
方策勾配法は方策オン型で経験再生を使えずサンプル効率が悪いため、Q学習（方策オフ型）と組み合わせてこれを解決したい。

#### 貢献（新規性・差分）
1. エントロピー正則化付きの方策勾配法の推定している方策πが、πに基づくアドバンテージ関数Aによって表せることを示した (Sec.3.1, 3.2, Eq.4)
2. 上記の関係を用いてPGQを提案・評価した (Sec.4., 5.)
3. Actor-critic法 (e.g., ベースライン付きの方策勾配法) の更新則と行動価値ベースの手法（e.g., SARSA, Q学習）の更新則が（特殊な場合に）等価であることを示した (Sec. 3.3)

#### 手法
PGQはまず、エントロピー正則化付きの方策勾配法で推定しているπと、この方策に基づくアドバンテージAの関係 (Eq.4) を使って、方策勾配法の推定しているπとVから、πに基づくQを計算する。このQがベルマン最適方程式に従うよう正則化をかけた方策勾配法の目的関数を最適化する。この正則加項部分の最適化をQ学習と同じく経験再生を使って行う。

#### 結果

##### 1. Atariドメインでの評価
Atariの50以上のゲームにおいて、得られた報酬に基づくスコアによる評価を行い、DQNとA3Cと比較を行った。
50以上のゲームにおける平均スコアだけでなくスコアの中央値でも人間のスコアを上回り、PGQとDQNとA3Cの3アルゴリズム中最下位になったのは1つのゲームだけだった。
----------------------------------------------------------------->
## まとめ

#### 概要
Actor-critic法(A3C)にExperience Replayを組み合わせたアルゴリズムACERを提案し、A3Cに対する優位性をAtari、Mujocoドメインで実験的に示した。

<!-- #### 目的 -->

#### 貢献（新規性・差分）
- 適切な処理によって勾配の分散を抑えれば, A3CにおいてもExperience Replayが機能することを示した。

#### 手法
  アルゴリズム全体としては、ACERはA3CでOn-policyの学習を行いつつ、それによってサンプルされたデータを使ってExperience Replay（Off-policyの学習）を行う。
このExperience Replay部分において、Sample Efficiency向上のために以下の工夫を行っている。
  まず、Sample Efficiencyを向上するためにImportance Samplingの概念を取り入れている。
Experience ReplayでImportance Samplingを行うと、通常であれば勾配の分散が非常に大きくなってしまい好ましくないが、
ACERではImportance Weightをマージ[Degris 2012]した上でクリッピングを施し、さらにQ^πの推定にRetrace(λ)[Munos 2016]を用いることでこれを回避している.
  また、Trust Region Policy Optimization[Schulman 2015]を応用したEfficient Trust Region Policy Optimizationを用い、
更新後の方策がそれまでの方策の平均から離れすぎないよう更新を制限している。

#### 結果

##### 1. Atariドメインでの評価
Atariの全ゲームを用いて、ACER、A3C、Prioritized Double DQN[Schaul 2016]（以下DDQN）等のサンプル効率、計算量効率を比較。
サンプル効率において大まかにDDQN = ACER（8 replay）> ACER（1 replay）> A3C。
計算量効率において大まかにDDQN = ACER（1 replay）= A3C > ACER（8 replay）。

##### 2. Mujocoドメインでの評価
Walker2d、Fish、Cartpole、Humanoid、Reacher3、Cheetahにて、ACER、A3C、Truncated Importance Sampling（以下TIS）のサンプル効率を比較。
Cartpole以外でACERがもっとも良い結果。
CartpoleにおいてもEfficient Trust Region Policy Optimization付きのTISに僅差の2位。

<!-- #### 定理・証明していること（汎用的で重要なものであれば） -->

<!--
## 次に読むべき論文
-
-->


<!-----------------------------------------------------------------
# コメント欄

コメントの他に
- コメント記述者: @XXX
- 点数: X/10（論文が必読に値するかどうかを10点満点で書く）
を書く。

コメントは記述者・点数が分かればあとはフォーマットは自由
返信なども可（例: そうかもしれないですね by @XXX）

-------
EXAMPLE
-------

#### @sotetsuk: 8/10
- 方策勾配法はナイーブな定式化では探索をすることができずに方策が決定論的になりがちだが、探索を促すエントロピー正則化を使った方策勾配法がある意味でより自然な定式化かもしれない、という示唆とも捉えることができて面白い。
- Eq.4からπとVだけを使って（妥当な）Qを計算しているのがPGQのポイントだと思った。
- そうかもしれないですね by @XXX
----------------------------------------------------------------->
## コメント

<!-- 1人目 -->
#### @yoshito.ogawa: 6/10
- 近年提案された重要な概念を利用しており, それらへのクリックリファレンスとして読むのも有用と思われる。

<!-- 2人目 -->
<!--
#### @XXX: X/10
-
-->

<!-- 3人目 -->
<!--
#### @XXX: X/10
-
-->
