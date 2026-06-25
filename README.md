# 🌷 お店のファン＆売上UP発見AIルーム
**〜 ブラウザ完結型の超本格・店舗データ分析AIツール 〜**

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)](https://developer.mozilla.org/ja/docs/Web/HTML)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)](https://developer.mozilla.org/ja/docs/Web/JavaScript)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![No Server](https://img.shields.io/badge/Data_Privacy-100%25_Local-success)](#)

「お店のファン＆売上UP発見AIルーム」は、エクセルやCSVのデータを読み込ませるだけで、**「どんなお客様がファンになりやすいか」「売上を上げる一番の鍵は何か」**をAI（機械学習・統計モデル）が自動で分析し、提案してくれるツールです。

🔗 **[デモを試す（GitHub PagesのURLをここに入力）](https://your-account.github.io/your-repo/)**

---

## ✨ アプリの特長

### 1. 🔒 サーバー送信ゼロ！完全ローカル＆セキュア
データは一切外部サーバーに送信されません。すべての計算（最尤推定・逆行列計算など）は**ブラウザのJavaScriptのみ**で完結しているため、顧客データや売上データが含まれる社外秘ファイルでも安心して分析できます。

### 2. 🤖 AIによる「目的」の自動判定
ユーザーが難しい設定をする必要はありません。一番右の列（目的変数）のデータをAIが自動で読み取り、最適な分析手法を適用します。
* **「1(はい) / 0(いいえ)」の場合** 👉 リピート確率などを予測する「ロジスティック回帰分析」
* **「金額 / 回数」の場合** 👉 売上金額などを予測する「重回帰分析」

### 3. 📊 直感的なUI × プロ仕様のガチ統計
「リピート倍率（オッズ比）」や「影響力」を分かりやすいポップなグラフで表示しつつ、専門家向けのエリアでは以下の本格的な統計指標を出力します。
* 回帰係数 (β) / 標準誤差 (SE) / p値 / 95%信頼区間
* オッズ比 (OR)
* 決定係数 (R²) / McFaddenの疑似R²
* モデルの予測精度グラフ（実測値 vs 予測値 / シグモイド曲線）

### 4. 📝 現場で使える充実の機能
* Excel特有のShift-JIS文字化けを自動回避（Encoding.js搭載）
* 「業種」をAIが自動推測し、明日から使える具体的なアクションプランを提案
* 美しいPDF保存 / 印刷用レイアウト（`@media print` に完全対応）
* X (Twitter) でのシェア機能

---

## 📖 使い方

1. **データの準備**
   Excelやスプレッドシートで以下のような表を作成し、`.csv` 形式で保存します。
   * **一番右の列**に、AIに予測してほしい「ゴール（目的変数）」を配置してください。
   * その他の列には、要因となりそうな項目（客単価、滞在時間、曜日のダミー変数など）を数値で入力します。

   *▼ 確率予測（0/1）のデータ例*
   | 客単価 | 滞在時間 | デザート注文(1=あり) | 次回来店したか(ゴール) |
   | :--- | :--- | :--- | :--- |
   | 1500 | 45 | 1 | 1 |
   | 800 | 20 | 0 | 0 |

2. **アップロード ＆ ワンタップ分析**
   画面からCSVファイルを読み込み、「🔮 ワンタップでAI分析をスタート！」を押すだけです。数秒で結果が出力されます。

---

## 🛠️ 技術スタックと裏側のロジック (For Developers)

このツールの最大の技術的挑戦は、**「Python (scikit-learn/statsmodels) や R言語に依存せず、純粋なフロントエンドJavaScriptだけで本格的な回帰分析を実装している点」**です。

* **フロントエンド**: HTML5, CSS3, Vanilla JavaScript
* **ライブラリ**: 
  * `Chart.js` (グラフ描画)
  * `PapaParse` (高速なCSVパース)
  * `encoding.js` (Shift-JIS等のバイナリ自動判定・UTF-8変換)
* **数学・統計アルゴリズムの自前実装**:
  * **ロジスティック回帰**: 勾配降下法（Gradient Descent）による重みの最適化
  * **ヘッセ行列と分散共分散行列**: ガウス・ジョルダン消去法による逆行列計算をJSで実装し、各変数の「標準誤差（Standard Error）」を算出
  * **p値の算出**: z値（Wald統計量）から、標準正規分布の累積分布関数（近似式）を用いてp値を正確に計算
  * **重回帰分析**: 最小二乗法 (OLS) による正規方程式を行列演算で解決

---

## 🚀 ローカル環境での動かし方

サーバー構築や `npm install` 等の環境構築は一切不要です。
リポジトリをクローンし、`index.html` をブラウザで開くだけで即座に動作します。

```bash
git clone https://github.com/your-account/your-repo.git
cd your-repo
# index.html をダブルクリック、またはブラウザにドラッグ＆ドロップして起動
