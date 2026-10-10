# Quanteliaのアーキテクチャ

## 目的

QuanteliaはCerune向けの独立した汎用数値計算ライブラリです。Neruneへの依存、機械学習固有の概念、WhitebaseやTint*の実装は持ち込みません。

```text
Nerune → Quantelia → Cerune

Whitebase: 実行結果・時間・Backendの比較
Tint*: Ceruneの変換過程の観測
```

WhitebaseやTint*はQuanteliaの必須依存ではありません。

## 責務

- Quantelia: Tensor、数値演算、shape、数値的な意味、再現可能な検証例。
- Cerune: 型・配列・所有・評価順・停止・IR・実行経路。
- Nerune: ニューラルネットワーク、Autograd、Optimizer、学習処理。
- Whitebase: ベンチマーク、Backendの可用性と性能・結果比較。
- Tint*: IR・MIR・SSA・生成成果物の観測。

## 初期API

`TensorF32`を`[f32]`のデータと`[i64]`のshapeで表します。当初の`from_data`は検証なしの仮APIであり、現状ではshapeの積と要素数の一致を保証しません。`numel`は次元の積を求め、整数オーバーフロー時にはCeruneの言語規則に従って停止します。

次に、不正次元・要素数不一致を回復可能なエラーとして扱う検証APIを設計します。公開構造体のフィールドを隠せない現行Ceruneでは、構築後にも不正値を作れるため、演算入口での検証も必要です。

## 計測の境界

Quanteliaの通常の演算は時計を参照しません。プログラム全体の計測はCerune CLI等のホスト、演算単位の比較はWhitebaseで扱います。コンパイル・準備・実行を混同せず、計測器の追加で演算結果を変えません。

## 依存と配布

現行Ceruneのimportは相対パスの`.ceru`です。Neruneへの取り込みは固定コミットのsubmodule等で実現できます。依存の複製を避け、パッケージ管理機能を先行して要求しません。
