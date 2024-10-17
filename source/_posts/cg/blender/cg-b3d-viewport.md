---
title: 個人的見やすい3D Viewの設定とか | Blender
date: 2024-04-06
tags: Blender
categories: 3DCG
cover: img/covers/cg-b3d-viewport2.png
banner: 
    type: img
    bgurl: img/banners/cg-b3d-viewport.png
    bannerText: 
---
# ビューポートの設定周りの軽い解説(メモ)
どこまで掘り下げるか難しいのですが、とりあえず軽く触るにしてもこれは気をつけたほうが良いな～程度のものを置いときます。

- 目次
  - [前提](#前提)
  - [Solidモードの設定](#Solidモードの設定)
  - [Renderモードの設定](#Renderモードの設定)
  - [その他](#その他)
  - [最後に](#最後に)

## 前提
・使用ソフト:Blender
・バージョン:4.0
・レンダラー:Cycles/Eevee
・言語:英語
・その他:どのバージョンでもおそらく共通。

## Solidモードの設定
　　
3D View右上の三角を押すとビューポートに関するプロパティが開けます。

<img width="300" src="{% asset_path Image1.png %}" title="Image1" class="img-left" />
　　

1.&nbsp;&nbsp;Solidモード(3D Viewのデフォルトモード)で自動でオブジェクトの色分けをしてくれます。
自分は基本オン。　　
　　
2.&nbsp;&nbsp;Cavityは輪郭やその周辺を強調表示してくれます。
オフだと結構のっぺりしていて奥行きが掴みづらいのでオン。
　　
3.&nbsp;&nbsp;Cavityのオプション。
デフォルトはScreenで、BothかWorldにするとテンキー視点にしたときに同じNormal(法線)の面でもカメラからの距離によってしっかり境界線が表示されます。　

<img width="800" src="{% asset_path Image2.gif %}" title="Image2" class="img-left" />

4.&nbsp;&nbsp;カメラのDepth of Field(被写界深度)の設定をSolidモード状態で適応できます。
カメラ側で設定していないと機能しません。基本オフで良いかと。
　　
5.&nbsp;&nbsp;オブジェクトにアウトラインを付けられます。
オブジェクトが密集している状態でCavityも有効だとくどいかも？自分は基本オン。
　　
6.&nbsp;&nbsp;オブジェクトに対する光の反射が反映されます。
自分はなんとなくオン。

<img width="800" src="{% asset_path Image3.gif %}" title="Image3" class="img-left" />

## Renderモードの設定

同じ感覚でRenderモードの設定いきましょう。

<img width="800" src="{% asset_path Image4.png %}" title="Image4" class="img-left" />

1.&nbsp;&nbsp;この二箇所をオフにすると、シーンに設置した照明や設定した背景の光源効果を無視して描写できます。
レンダリング結果にのみ適応されるノードや機能の関係で結構使うと思います。
　　
2.&nbsp;&nbsp;1で二箇所をオフにした際に代わりに設定される背景をここから設定できます。
夜や屋内、屋外様々なシチュエーションを想定したものが用意されています。
反射や光量等の関係で追加されるものなので、自分で設定する背景とは別物みたいです。
また、Material Previewモードでも同様に設定が可能です。

<details><summary>余談</summary>

ここに用意されているHDRIは

<strong>"インストール先\Blender [version]\ [version] \datafiles\studiolights\world"</strong>

に収納されているみたいです。
(自分の環境の場合 "インストール先\Blender 4.0\4.0\ ~" となります。)

</details>

## その他

基本モード関係なく使えるものです。

<img width="600" src="{% asset_path Image5.png %}" title="Image5" class="img-left" />

1.&nbsp;&nbsp;移動や回転ツール(アクティブツール)の表示を切り替えられます。
中を見てみると移動や変形の基準を変更できたり色々できます。
~~書いてて思ったけどあまり使わないかも。~~ 
<img width="400" src="{% asset_path Image6.png %}" title="Image6" class="img-left" />

2.&nbsp;&nbsp;グリッドや3Dカーソル、アクティブツールの表示を一括で切り替えられます。
中を見てみると3D View内のUIに関する細かい設定ができます。
ノーマル(法線)を確認する時などいろいろ使い道はあるのですが、今回は軽い紹介ということで。
　　
3.&nbsp;&nbsp;オブジェクトを半透明状態にして描写できます。
Editモードでは選択範囲を貫通して裏面も選択できるのでモデリングでは必須の機能。
<img width="800" src="{% asset_path Image7.gif %}" title="Image7" class="img-left" />
　　
4.&nbsp;&nbsp;値を入力して描写範囲を指定できます。
**こちらは画面上ではなく、すぐ横の縦に並んでいるタブのViewタブにあります。**
カメラにも同様の設定がありますが、これはViewport内でのみ機能するものです。
遠くにオブジェクトを置くプロジェクトではEndの数値を上げたり、入り組んだ場所を編集する時にStartを一時的に上げたり、みたいな使い方をよくしています。
<img width="800" src="{% asset_path Image8.gif %}" title="Image8" class="img-left" />

## 最後に

経験が浅く、拙い知識、拙い文章力だったとは思いますが、閲覧頂きありがとうございました。
今後CGカテゴリーの備忘録記事(+プチ日記)はこんな感じで書いていこうと思います。
　　
本編とは関係ない愚痴ですが、花粉症で鼻水を垂らしながら深夜テンションで書いてました。
毎年、鼻の中で流体シミュレーションをさせられる僕は一体、何と戦わされてるんでしょうか。
<img width="500" src="{% asset_path Image9.png %}" title="Image9" class="img-left" />