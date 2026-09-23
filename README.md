# learning_iLQR

iLQRは最適制御問題を解く方法であり、軌道計画にもNMPCのようなオンライン制御にも使うことが出来る。

iLQR : iterative Linear Quadratic Regulator (反復線形二次レギュレータ)

## 学習ステップ

- Step1からStep10でiLQRを有限ホライゾン軌道最適化として理解する
- Step 11で完成したiLQRを各制御周期で繰り返し、NMPC化する

### 基礎編

* [x] **Step 1：rolloutと総コスト**<br>
  入力列 $U$ から状態軌道 $X$ を順方向計算し、総コスト $J$ を求める。

* [x] **Step 2：有限時間離散LQR**<br>
  Bellmanの最適性原理からRiccati再帰を導き、ゲイン列を求める。初期状態から順方向計算して、最適な状態・入力軌道を構成する。

* [x] **Step 3：iLQRの一反復の全体像**<br>
  基準軌道のrollout、局所近似、backward pass、forward pass、ラインサーチという一反復の流れを理解する。

* [x] **Step 4：動力学の局所一次近似とQ関数と局所二次近似** <br>
  基準軌道の周辺で動力学を一次近似、コストと価値関数を二次近似し、$Q_x,Q_u,Q_{xx},Q_{uu},Q_{ux}$ を構成する。

* [x] **Step 5：backward pass**<br>
  終端から逆向きに計算し、入力修正則

  $$
  \delta u_k=d_k+K_k\delta x_k
  $$

  と価値関数の微分 $V_x,V_{xx}$ を求める。

* [ ] **Step 6：forward pass** <- 現在値<br>
  backward passで得た修正則を使って非線形モデルをrolloutし、ラインサーチによってコストが減少する新しい軌道を求める。

* [ ] **Step 7：非線形ばねでiLQRを完成**<br>
  Step 1〜6を組み合わせ、入力列の改善を反復するiLQRを実装する。C/GMRESとの違いも確認する。

### 応用編

* [ ] **Step 8：数値安定化**<br>
  $Q_{uu}$ の正定値性、正則化、Cholesky分解、予測コスト減少量を扱う。

* [ ] **Step 9：モデルの発展**<br>
  非線形ばねから振子、Cart-Pole、SimpleCarへ適用対象を広げる。

* [ ] **Step 10：制約付きiLQR**<br>
  入力上下限、バリア関数、Box-constrained iLQR、Augmented Lagrangianを学ぶ。

* [ ] **Step 11：iLQRによるNMPC**<br>
  warm startを用いて各制御周期でiLQRを解き、最初の入力だけを制御対象に与える。
