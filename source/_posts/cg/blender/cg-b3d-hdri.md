---
title: Worldを環境テクスチャ化しよう～ | Blender(+PS)
date: 2024-04-11
tags: Blender
categories: 3DCG
cover: img/covers/cg-b3d-hdri2.png
banner: 
    type: img
    bgurl: img/banners/cg-b3d-hdri.png
    bannerText: 
---
# Worldを環境テクスチャ(EXRファイル&HDRファイル)にする方法

ノードを適応した状態のWorldを画像化して他の場所で使いたい、今作っている背景をそのまま焼き付けて使いたい、といったシチュエーションで有効な手段です。

<img width="400" src="{% asset_path Image1.png %}" title="Image1" class="img-left" />

手順としては、カメラの設定からパノラマ状態にして、EXRファイル、またはHDRファイルとしてレンダリングする、といった感じです。
Eeveeはパノラマに設定することができないので、Cyclesレンダーのみの方法となっております。

- 目次
  - [前提](#前提)
  - [手順0. 確認](#手順0-確認)
  - [手順1. カメラの設定](#手順1-カメラの設定)
  - [手順2. レンダーの設定](#手順2-レンダーの設定)
  - [完成](#完成)
  - [PhotoshopでEXRファイルを扱う時のポイント](#PhotoshopでEXRファイルを扱う時のポイント)
  - [参考資料](#参考資料)
  - [最後に](#最後に)

## 前提
・使用ソフト:Blender, Photoshop
・バージョン:4.0
・レンダラー:Cycles
・言語:英語(PSは日本語)
・その他:加えてPhotoshopでの扱い方についても置いときます。

## 手順0. 確認
一応の確認ですが、やることは普通のレンダリングなので、映ってほしくないものはきちんと非表示にしておきましょう。
上記の通りカメラの設定の関係でEeveeレンダーは使えません。
　　
## 手順1. カメラの設定
簡単です。
<img width="800" src="{% asset_path Image2.gif %}" title="Image2" class="img-left" />

Type → **Panoramic(パノラマ状)**
　　
Panorama Type→ **Equirectangular(正距円筒図)**
　　
これだけです。Panorama Typeの中の値はデフォルトで大丈夫です。
　　
## 手順2. レンダーの設定

<strong>1.&nbsp;&nbsp;解像度の設定</strong>
解像度について、自分は少し大きめの8Kで作ってあとから小さくしても問題ないようにしました。

<img width="800" src="{% asset_path Image3.png %}" title="Image3" class="img-left" />

X:8192 px
Y:4096 px
　　
適当にダウンロードしてたHDRIを参考に合わせただけです。
他の解像度はチートシートなんかを活用してみましょう。
[Aspect Ratio Cheat Sheet v2(外部リンク)](https://www.wearethefirehouse.com/aspect-ratio-cheat-sheet)
　　
<strong>2.&nbsp;&nbsp;ファイル形式の設定</strong>
続いてファイル形式の設定。画像の通りです。
　　
<img width="800" src="{% asset_path Image4.png %}" title="Image4" class="img-left" /> 

<details><summary>.hdrの場合</summary>

EXRではなくHDRで書き出したい方向けです。こちらはそのままの設定で機能しました。

<img width="600" src="{% asset_path Image5.png %}" title="Image5" class="img-left" />
<img width="600" src="{% asset_path Image6.png %}" title="Image6" class="img-left" />

</details>

あとは通常通りレンダリングします。

## 完成
いつも通りEnvironment Texture(環境テクスチャ)ノードから読み込むだけですね。
　　
Blender
<img width="600" src="{% asset_path Image7.png %}" title="Image7" class="img-left" />

<details><summary>Unity</summary>
マテリアルを作って、ShaderをSkybox/Panoramicに。<br>
HDRのところにimportしたexrファイルを挿し込む。<br>
LightingタブのEnvironmentからSkybox Materialで作ったマテリアルを指定。<br>
<img width="600" src="{% asset_path Image8.png %}" title="Image8" class="img-left" />

</details>

<details><summary>Unreal Engine 5</summary>
(多分既存のシェーダーが絡んで色濃く見えてると予想)<br>
UE5に関してはプラグインが絡んだり、色々設定が必要だったのでまた記事にしたいと思います。<br>

<img width="600" src="{% asset_path Image9.png %}" title="Image9" class="img-left" />

</details>

<details><summary>背景オブジェクト込みバージョン</summary>

過去に映像で使った背景用の街オブジェクトを適当に並べて書き出してみました。
手前のオブジェクトは新しく設置したものです。

<img width="600" src="{% asset_path Image10.png %}" title="Image10" class="img-left" />

</details>

## PhotoshopでEXRファイルを扱う時のポイント
**4月15日に全体的に編集を加えました。**

> **_追記_**
私のPhotoshopの知識が浅く、保存に関する認識が間違っていました。
**別名で保存**は再編集可能な状態で保存するもので、
その下の**コピーの保存**を使うとプラグインなしでもexrファイルで書き出しできるみたいです。
今回の以下のプラグインに関する内容は、再び編集ができる状態として保存したい時に活用できるものです。

素のフォトショはEXRファイルに関してかなり微妙で、
画像の解像度変更や切り取り等以外の**レイヤーを重ねるような編集**をした場合、
"別名で保存"は多分できないと思われます。
　　
また、レイヤー情報などを正確にEXRファイル内の情報を読み取っているわけではなく、書き出しも不便なため、
[Exr-IO(外部リンク)](https://www.exr-io.com/)というプラグインを入れて改善します。
  　
このプラグインを導入すると、EXRファイルを読み込んだ時にこんな画面が表示されます。
<img width="800" src="{% asset_path Image13.png %}" title="Image13" class="img-left" />

今回の目的ではいじらなくても問題なかったので、そのままOpenをクリック。
　　
**別名で保存**を押すと、EXRで(編集可能のまま)保存できるようになっています。
<img width="400" src="{% asset_path Image14.png %}" title="Image14" class="img-left" />

(追記)
**コピーを保存**を押すと、再び開いた時に編集状態にはなりませんが、EXRだけでなくHDRで書き出すことも可能です。
こちらはプラグインなしで可能です。
<img width="400" src="{% asset_path Image15.png %}" title="Image15" class="img-left" />

## 参考資料
- YouTube
[Make Your Own HDRI in Blender 3.0(外部リンク)](https://youtu.be/o7q7O5RuE6s?si=1i-VJo4atig6wWlA)

## 最後に
今回だいぶ長くなってしまったのですが、その分自分も勉強になりました。
exrは作ることよりもその後の扱いのほうが難しいみたいですね。
　　
本編とは関係ない雑談ですが、最近寒暖差に体が追いつきません。
あと、花見行こうかなと思った前日に土砂降りかまされました。
閲覧頂きありがとうございました。
　　
(追記)
桜無事見れました。最高