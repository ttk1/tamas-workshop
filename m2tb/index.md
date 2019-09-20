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

* 初出イベント
  * [技術書典7 2019-09-22](https://techbookfest.org/event/tbf07/circle/5088651352473600)
* 価格
  * ￥1,000
* ページ数
  * 102p
* 電子版/通販
  * 未定...
* 2ヶ月前まで、WebGLなんもわからん状態だった著者が、プライベートの時間を全て注ぎ込んで書き上げました
* WebGLはいいぞ

## 目次

* 前書き
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
* 第3章
  * [Transform Feedbackを用いた計算サンプル](https://github.com/ttk1/TransformFeedbackSample)
    * [デモ](./demo/sample02.html)
* 第4章
  * [多体問題の実装例](https://github.com/ttk1/n-body)
    * [デモ（高負荷に注意）](./demo/sample03.html)

### 注意

* デモを動作させるには、少なくともWebGL 2.0に対応した環境が必要です
* サンプルコードのイケてなかった部分は、ちょくちょく修正入れてます

## 補足等

* 何かあれば追記します
