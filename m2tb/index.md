# WebGLではじめるGPGPU入門

![カバー](./cover.png)

## 著者

* tama
  * GitHub: [@ttk1](https://github.com/ttk1)
  * Twitter: [@mscle11](https://twitter.com/mscle11)
* Happinessfield
  * GitHub: [@yasuda0102](https://github.com/yasuda0102)
  * Twitter: [@Happinessfield](https://twitter.com/Happinessfield)

## 概要

* 2ヶ月前まで、「WebGLなんもわからん」状態だった著者が、プライベートの時間を全て注ぎ込んで書き上げました
* WebGLはいいぞい
* 初出イベント
  * [技術書典7 2019-09-22](https://techbookfest.org/event/tbf07/circle/5088651352473600)
* 価格
  * ￥1,000
* ページ数
  * 102p
* 電子版/通販
  * 未定...

## 問い合わせ先

本書の内容に関する問い合わせは、メールもしくはTwitterで受け付けています。

* Mail: [tama@ttk1.net](mailto:tama@ttk1.net)
* Twitter: [@mscle11](https://twitter.com/mscle11)

## 目次

* まえがき
* 第1章 はじめに
  * なぜWebGLなのか
  * 物理エンジンとGPGPU
  * 本書の構成
* 第2章 WebGL入門
  * WebGLとは
  * WebGLの特徴
  * グラフィックスパイプライン
  * OpenGL Shading Language（GLSL）
  * プログラムの流れ
  * 環境構築
* 第3章 GPGPU
  * GPGPUとは何か？
  * なぜ計算が高速なのか？
  * WebGLでGPGPUをやるために必要な知識
  * Transform Feedbackを用いた計算サンプル
* 第4章 物理エンジン: 多体問題
  * 多体問題とは何か？
  * WebGLプログラムの実装
  * 計算のためのシェーダの実装
  * 考察
* あとがき

## サンプルコード

本書で紹介したコードはこちらからダウンロードできます

* 第2章
  * [sample01.html](https://github.com/ttk1/tamas-workshop/tree/master/m2tb/demo/sample01.html)
    * [デモ](./demo/sample01.html)
  * [WebGLTemplate](https://github.com/ttk1/WebGLTemplate)
    * 環境構築の節で作った、WebGLプロジェクトのたたき台
* 第3章
  * [Transform Feedbackを用いた計算サンプル](https://github.com/ttk1/TransformFeedbackSample)
    * [デモ](./demo/sample02.html)
* 第4章
  * [多体問題の実装例](https://github.com/ttk1/n-body)
    * [デモ（高負荷に注意）](./demo/sample03.html)

### 注意

* デモを動作させるには、少なくともWebGL 2.0に対応した環境が必要です
  * [Can I use webgl2?](https://caniuse.com/#search=webgl2)
* サンプルコードには修正を入れており、本の記述とは異なる箇所があります

## 補足

### 88ページ、3. 型付き配列をテクスチャとしてVRAMに転送する

`pTex, vTex, aTex, mTex`のテクスチャの大きさは、(N, 1)となるという説明が抜けていました。
イメージとしては、1次元配列`P, V, A, M`を横方向に細長い2次元配列に変換していると考えるとよいでしょう。

実際に横方向に細長いテクスチャを作成している箇所は、`createTexture()`関数の51-52行目の`gl.texImage2D()`メソッドです。
このメソッドがテクスチャ領域の確保とVRAMへのデータの転送を行うために必要です。以下に`gl.texImage2D()`メソッドの引数を示します。

- 第1引数
  - テクスチャの種類を指定します。ここでは`gl.TEXTURE_2D`を指定しています。これは2次元テクスチャであることを意味しています。
- 第2引数
  - ミップマップのレベルを指定します。今回はミップマップを使用しないため、ここでは`0`を指定しています。
- 第3引数
  - テクスチャの色成分を指定します。ここでは呼び出し元から渡ってきた`iformat`を指定しています。
- 第4引数
  - テクスチャの横幅を指定します。ここでは呼び出し元から渡ってきた`list, dimension`を使って横幅を求めています。
- 第5引数
  - テクスチャの縦幅を指定します。ここでは`1`固定です。
- 第6引数
  - ボーダーの幅を指定します。この引数は`0`を指定しなければなりません。
- 第7引数
  - テクスチャのピクセル(テクセル)のフォーマットを指定します。ここでは呼び出し元から渡ってきた`format`を指定しています。
- 第8引数
  - テクセルデータのデータタイプを指定します。ここでは呼び出し元から渡ってきた`type`を指定しています。
- 第9引数
  - テクスチャデータを指定します。ここでは呼び出し元から渡ってきた`list`を指定します。

なお、`iformat, format, type`についてですが、`iformat`によって、`format, type`は決まります。
[WebGL 2.0 APIクイックリファレンスガイド](https://www.khronos.org/files/webgl20-reference-guide.pdf)の5ページに書かれています。
例えば、`iformat`に`gl.RGBA32F`を指定すると、`format`は`gl.RGBA`, `type`は`gl.FLOAT`にしなければなりません。

## 訂正

### 25ページ、リスト 2.6 の 13-15 行目

```glsl
// float 値を 1 つだけ指定
mat2 d = mat2(1.0); // = mat2(1.0 * 2.0 + 3.0 * 3.0, 2.0 * 2.0 + 4.0 * 3.0,
                    //        1.0 * 4.0 + 3.0 * 5.0, 2.0 * 4.0 + 4.0 * 5.0)
```

となっていますが、正しくは

```glsl
// float 値を 1 つだけ指定
mat2 d = mat2(1.0); // = mat2(1.0, 0.0,
                    //        0.0, 1.0)
```

でした。

## おまけ

* [多体問題の実装例（GPGPUじゃない版）](https://github.com/ttk1/n-body-js)
  * [デモ（高負荷に注意）](./demo/sample04.html)
* [多体問題の実装例をマウスでぐりぐり動くようにしたもの](https://github.com/ttk1/n-body-3d)
  * [デモ（高負荷に注意）](./demo/sample05.html)
* [著者がWebGLの練習で作ったもの](https://wglp.ttk1.dev/)
  * よかったらどうぞ
