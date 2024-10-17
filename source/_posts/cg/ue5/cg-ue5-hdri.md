---
title: UE5でHDRIを適応するときの手順メモ | Unreal Engine 5
date: 2024-04-18
tags: UE5
categories: 3DCG
cover: img/covers/cg-ue5-hdri.png
banner: 
    type: img
    bgurl: img/banners/cg-b3d-hdri.png
    bannerText: 
---
# UE5でHDRIを適応するときの手順
前回は、Blenderで作成したWorldをEXR形式のイメージテクスチャにしました。
この際に色々なソフトで読み込ませてテストをしていたのですが、UE5は少し手順を踏まないと綺麗に表示されなかったため、メモに残しておこうと思いました。
　
(自分はUE初心者なので拙い内容だとは思いますがご容赦ください)

- 目次
  - [前提](#前提)
  - [準備](#準備)
  - [HDRの適応](#HDRの適応)
  - [HDRI Backdropの設定](#HDRI-Backdropの設定)
  - [参考資料(外部リンク)](#参考資料(外部リンク))
  - [最後に](#最後に)

## 前提
・使用ソフト:Unreal Engine 5
・バージョン:5.3.2
・言語:英語
・その他:一応前回の[HDRIを作ろうの続き的な記事](https://www.quadro1375.com/2024/04/11/cg/blender/cg-b3d-hdri/)の続きになります。

## 準備
<strong>0.&nbsp;HDR形式のものを用意</strong>

今回の場合、EXR形式は読み込めないみたいなので、EXRファイルの場合はHDRに変換します。
オンラインサービスでもソフトでも変換できればなんでも大丈夫です。

[前回の記事の後半](https://www.quadro1375.com/2024/04/11/cg/blender/cg-b3d-hdri/#Photoshop%E3%81%A7EXR%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%82%92%E6%89%B1%E3%81%86%E6%99%82%E3%81%AE%E3%83%9D%E3%82%A4%E3%83%B3%E3%83%88)にフォトショでHDRで書き出す方法を追記しました。
　　
Gimpの場合は"名前をつけてエクスポート"から拡張子をhdrに書き換えて保存すると大丈夫みたいです。（動作確認済み
　　
自作の場合、変換以前にBlender側でhdrで書き出しちゃってもいいと思います。
　　
<strong>1.&nbsp;新規プロジェクト作成&プラグインの確認</strong>

今回はFILMS / VIDEO & LIVE EVENTSからBlankを選んで、新規プロジェクトを作成します。
<img width="700" src="{% asset_path Image1.png %}" title="Image1" class="img-left" />

続いて、上のEditからPluginsを選択してプラグインの管理画面を開きます。
　
上の検索窓から、"HDRIBackdrop"と検索して有効なことを確認します。

<img width="700" src="{% asset_path Image2.png %}" title="Image2" class="img-left" />

準備完了！

## HDRの適応
<strong>1.&nbsp;HDRファイルをインポート</strong>

コンテンツブラウザに適当なフォルダを作って、HDRファイルを読み込みます。
<div class="image">
  <div>
    <ul>
        <dd><img width="200" src="{% asset_path Image3.png %}" title="Image3" class="img-left"/></dd>
        <dd><img width="435" src="{% asset_path Image4.png %}" title="Image4" class="img-left"/></dd>
    </ul>
    <style>
        .image > div {
          ul {
            display: flex;
            justify-content: center;
            }
        }
    </style>
  </div>
</div>

<strong>2.&nbsp;HDRI Backdropを追加</strong>

画面横の検索窓にHDRIと打つとHDRIBackdropが出てくるので、それをシーンに追加します。
加えて座標を0に調整。
<img width="700" src="{% asset_path Image5.png %}" title="Image5" class="img-left"/>

<strong>3.&nbsp;HDRファイルを適応</strong>

アウトライナー内のHDRIBackdropを選択すると、次のような詳細が表示されます。
HDRIBackdrop(self)を選択して、Cubemapという箇所に先程用意したHDRファイルを挿し込みます。

<img width="500" src="{% asset_path Image6.jpg %}" title="Image6" class="img-left"/>

最初はこれで「完成だーーー」と思っていたのですが、
よく見ると下は歪んでるし、少し離れると凄い見た目をしていることがわかります。

<img width="550" src="{% asset_path Image7.png %}" title="Image7" class="img-left"/>
<img width="550" src="{% asset_path Image8.png %}" title="Image8" class="img-left"/>

## HDRI Backdropの設定

<strong>1.&nbsp;HDRIの形状を変更</strong>

SceneComponentのGeometryを選択して、Static Meshという項目からSphereを選択して形状を球体に変更します。
<img width="800" src="{% asset_path Image9.gif %}" title="Image9" class="img-left"/>

手順通りだとここで一回HDRIが表示されなくなると思います。
　　
<strong>2.&nbsp;マテリアルの設定</strong>

私も知識が浅く完全に理解しているわけではないのですが、
（恐らく）この形状に対するマテリアルの設定をしていきます。

さっきのStatic Meshの下にある、MaterialsのElement 0に設定されているマテリアルをダブルクリックして設定を開きます。
<img width="800" src="{% asset_path Image10.jpg %}" title="Image10" class="img-left"/>

さらにそこのMaterial Instanceのプロパティを開いて、
右のMaterial Property Overridesから、Two Sidedの項目を有効化して、中のチェックをオンにして有効にします。
これで恐らく指定した形状の両面にテクスチャが描写されるようになります。
<img width="800" src="{% asset_path Image11.gif %}" title="Image11" class="img-left"/>

あとはHDRIBackdropの設定から、お好みにサイズを調整したりして完成です。
<img width="400" src="{% asset_path Image12.jpg %}" title="Image12" class="img-left"/>

お疲れ様でした！
<img width="800" src="{% asset_path Image13.png %}" title="Image13" class="img-left"/>

## 参考資料

- YouTube
[Unreal Engine Hdri Backdrop: How To Change The Shape(外部リンク)](https://youtu.be/cVy2QKIPZ5Q?si=Bt1myXUOVXw8S2x0)

## 最後に
UEもだんだん慣れてきてモチベーション湧いてきました。
この記事を書いている裏で少しVRMファイル系のプラグインを触っていたのですが、今度はそちらも挑戦してみようかなと。
　
閲覧頂きありがとうございました。