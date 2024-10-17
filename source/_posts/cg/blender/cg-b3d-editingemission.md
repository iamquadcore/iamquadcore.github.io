---
title: Emissionノードを少しグレードアップさせるあれこれ | Blender
date: 2024-07-06 
tags: Blender
categories: 3DCG
cover: img/covers/cg-b3d-editingemission.png
banner: 
    type: img
    bgurl: img/mainimages/emo.png
    bannerText: 
---
# Emission(放射)ノードを少しグレードアップさせるあれこれ
今回は、電球などを目的とした放射ノードにリアルタイムなグラデーションを施し、少しばかりきれいに見せる方法を見つけました。
　
Cyclesの放射ノードは単調になりがちですが、比較的簡単、尚且つ他にも応用できそうなものなのでメモとして残しておきます。

こんな感じのものが
<img width="300" src="{% asset_path Image1.png %}" title="Image1" class="img-left" />

こうなります。
<img width="330" src="{% asset_path Image2.png %}" title="Image2" class="img-left" />

※完全なオリジナルではなく、ある方の動画で使われていたノードを自分なりに改良したものです。
 [参考資料](#参考資料) に乗せてます。

- 目次
  - [前提](#前提)
  - [手順1. 必要なノードの用意](#手順1-必要なノードの用意)
  - [手順2. 各ノードの設定](#手順2-各ノードの設定)
  - [補足](#補足)
  - [参考資料](#参考資料)
  - [最後に](#最後に)

## 前提
・使用ソフト:Blender
・バージョン:3.4
・レンダラー:Cycles
・言語:英語
・その他:EeveeではCyclesのような挙動が見られませんでした。

## 手順1. 必要なノードの用意
必要なノードは画像の通りです。

<img width="800" src="{% asset_path Image3.png %}" title="Image3" class="img-left" />

・Principled BSDF(ベースになります)
・Emission(放射ノード)
・Mixノード（混ぜ混ぜ）
・ColorRamp(しきい値調整要員)
・LayerWeight(本日のメイン)

## 手順2. 各ノードの設定
<strong>1.&nbsp;&nbsp;Principled BSDF</strong>

こいつにはガラス感を担ってもらいます。
　
まずRoughness(粗さ)を0にします。

続いてマテリアルタブから、Blend ModeをAlpha Blendに、Shadow ModeをAlpha Hashedに変更します。
<img width="550" src="{% asset_path Image4.jpg %}" title="Image4" class="img-left" />
(この画像は後付で4.1で撮影したものになります。)

<strong>2.&nbsp;&nbsp;LayerWeight</strong>

Mixシェーダーを"混ぜる"ノードだとすると、LayerWeightノードは"混ぜ方"を決めるものになります。
Blendという項目を調整して、２つのシェーダーを混ぜる加減を調整します。
今回は0.2にしました。

## 補足
LayerWeightは、カメラ(自分の視点)の角度を元に値を振り分けてくれるノードです。
Blender Manualでは"シェーダーをレイヤー化してくれるもの"と説明されていますね。
今回は放射させるノードに半透明なノードを混ぜることで多少のグラデーションを付けています。
　
「LayerWeightで混ぜ方を決めて、混ざる範囲(しきい値)をColorRampで調整、Mixノードで２つのシェーダーを混ぜる」
といった流れで処理していますね。
　
これにVolumeノードなどを組み合わせてBloom感を加えると非常に綺麗なオブジェクトになります。
記事の最後にそれらを組み合わせて使っている様子を載せておきますね。

## 参考資料
- Blender 4.1 Manual
[Layer Weight Node(外部リンク)](https://docs.blender.org/manual/en/latest/render/shader_nodes/input/layer_weight.html)
- Youtube
[Making a Light Bulb in Blender(外部リンク)](https://youtu.be/_kXXOsUGAQ4?si=kYkfRV-ztVuxznGC)

## 最後に
今回のノードに加えて、自作のガラス風マテリアルと組み合わせた照明を置いておきます。
~~モデル自体はTutorialを見て作ったものですが~~
<img width="300" src="{% asset_path Image5.png %}" title="Image5" class="img-left" />
　
結構味があって気に入ってます( ﾟ∀ﾟ)
　
閲覧頂きありがとうございました。