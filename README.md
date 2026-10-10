# Quantelia

日本語 | [English](README.en.md)

Quanteliaは、[Cerune](https://github.com/Hokutaka/Cerune)向けの実験的な汎用数値計算ライブラリです。

**Numerical computing you can observe.**

計算結果だけでなく、計算の規則・数値的な挙動・実行経路を理解し、検証できることを目指します。

現在は初期開発段階です。小さなTensor表現から始め、基本演算・線形代数・統計処理を段階的に追加します。

## 設計原則

### 汎用性と独立性

Quanteliaは機械学習専用ではありません。[Nerune](https://github.com/Hokutaka/Nerune)などから利用できますが、Neruneの存在や型・学習処理・依存関係を知りません。

ニューラルネットワーク、Autograd、Optimizer、学習ループはQuanteliaの責務に含めません。

### 観測可能な数値計算

- 入力・出力の型、shape、演算の規則を明確にします。
- 浮動小数点の丸め、演算順序、誤差、境界条件を検証できるようにします。
- 同じソースについて、Ceruneが提供するIR・VM・生成経路と照合できる小さな例を用意します。
- 観測の有無によって計算の意味を変えず、観測と計算への介入を分けます。

### 計算と計測の分離

Quanteliaは数値演算とその契約を提供します。

実行時間、繰り返し計測、バックエンド間の性能・結果比較は、必要に応じてCeruneの実行基盤や[Whitebase](https://github.com/Hokutaka/Whitebase)などの外部ツールで扱います。時間計測や特定の実行バックエンドはQuanteliaの必須依存としません。

### 小さく段階的に

実装済みの範囲、未実装の機能、将来の構想を明確に区別します。演算を追加するときは、期待結果・失敗条件・可能な実行経路での比較を一組として確認します。

## 現在の範囲

最初は`f32`のTensorを一次元のデータ配列とshapeで表すことから始めます。APIと内部表現は実験段階で変更される可能性があります。

今後の候補:

- shapeと要素数の整合性検証
- 要素ごとの四則演算・集約
- ベクトル・行列演算
- 基本統計
- 数値的な挙動の検証例

Tensorの所有・値コピー・評価順・停止の意味はCeruneの言語仕様に従います。

## 試す

Ceruneをインストールしたうえで、リポジトリのルートから実行します。

```sh
cerune check examples/basic_tensor.ceru
cerune run examples/basic_tensor.ceru
```

## 関連プロジェクト

- [Cerune](https://github.com/Hokutaka/Cerune): 言語・型・中間表現・実行経路
- [Nerune](https://github.com/Hokutaka/Nerune): Quanteliaを利用できる機械学習ライブラリ
- [Whitebase](https://github.com/Hokutaka/Whitebase): 計測・比較・検証
- [Tint*](https://github.com/Hokutaka/Tint-St): コンパイル過程の観測

## 名前

Quanteliaは、数量・定量を表す「Quant」と椿の「Camellia」を組み合わせた造語です。

## License

MIT License
