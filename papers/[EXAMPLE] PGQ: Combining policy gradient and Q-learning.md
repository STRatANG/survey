# PGQ: Combining policy gradient and Q-learning

<img src='../tmb/PGQ: Combining policy gradient and Q-learning.png' width=750px />

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

## まとめ

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

<!-- #### 定理・証明していること（汎用的で重要なものであれば） -->

## 次に読むべき論文
- Nachum et al. (2017) [Bridging the Gap Between Value and Policy Based Reinforcement Learning](https://arxiv.org/abs/1702.08892)

## コメント

#### @sotetsuk: 8/10
- 方策勾配法はナイーブな定式化では探索をすることができずに方策が決定論的になりがちだが、探索を促すエントロピー正則化を使った方策勾配法がある意味でより自然な定式化かもしれない、という示唆とも捉えることができて面白い。
- Eq.4からπとVだけを使って（妥当な）Qを計算しているのがPGQのポイントだと思った。
