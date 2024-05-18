---
title: 物理演算が250フレームで止まる時の対処法+α | Blender
date: 2024-05-19
tags: Blender
categories: 3DCG
cover: img/covers/cg-b3d-250ffix.png
banner: 
    type: img
    bgurl: img/banners/cg-b3d-250ffix.png
    bannerText: 
Thumbnail: img/covers/cg-b3d-250ffix.png
---
# 物理演算が250フレームで止まる時の対処法+演算開始地点の変更方法
250フレーム以降で演算処理が止まる時の対処法と、演算の開始地点を変更するときの方法です。
　
プロジェクトの途中に紙吹雪などの長めの演算を組み込む時に最初困惑しました。
　
すぐ終わるCloth演算ばっかり使ってた自分が少し悩んだことだったので載せておきます。

## 前提
・使用ソフト:Blender
・バージョン:4.0
・レンダラー:Cycles/Eevee
・言語:英語
・その他:一部画像は4.1環境で後撮りしたものですが、問題はないと思われます。
　
## 原因と対処法
この演算が止まる現象について、原因として挙げられるのはシミュレーションの設定、もしくはシーンの設定です。
　
演算の範囲というのは上記のどちらかで決められていて、その範囲外では処理が停止します。
そのデフォルト値が1~250フレーム目までなので、そのままの設定だと範囲を超えて固まってしまうわけですね。
　
対処法は簡単。
タイムラインの範囲を変えた時と同じ要領で演算の設定の中でシミュレーション範囲を書き換えると解決します。
<img width="300" src="{% asset_path Image1.png %}" title="Image1" class="img-left" />
<img width="300" src="{% asset_path Image2.png %}" title="Image2" class="img-left" />

ベイクする時に見る項目ですね。
　
しかし、この方法には例外もあって、その代表がRigid Bodyです。
Rigid Body(剛体)は後者のシーンの設定から変更することができます。
<img width="300" src="{% asset_path Image3.jpg %}" title="Image3" class="img-left" />

これらを調整することで、開始位置を調整することもできます。
　
ちなみに、途中まで演算開始前のオブジェクトを非表示にしておきたい場合は、モーションをベイクしてからオブジェクト自体のサイズにキーフレームを打つと上手くいきます。
逆の手順を踏むと演算がうまく行かなかったか、打ったキーフレームが機能しなかったみたいなことが起こった気がします。

<dev>
<details><summary>余談その1:Rigid Bodyだけ設定場所が違う理由</summary>
"剛体"を意味するRigid Bodyですが、そもそも鋼体とは、<strong>"圧力や重力など外部の力を加えても形状を変えない理想化された物体"</strong>と定義されています。

Blenderでは、ClothやSoft Body等の形状変化を伴うシミュレーションとはカテゴライズが違うため、シミュレーションの設定＆シーンの設定で管理されています。
オブジェクト単体以上に環境に影響を与えるものですしね。

詳しくは英語ですがBlenderの[ドキュメント(外部リンク)](https://docs.blender.org/manual/en/latest/physics/rigid_body/world.html)をどうぞ。
</details>
</dev>

<dev>
<details><summary>余談その2:"シミュレーション範囲"について</summary>
シーン設定にある"Simulation Range(シミュレーション範囲)"についてですが、これはジオメトリーノードのシミュレーションノード等特殊な演算の範囲を指定するためのものみたいです。
<img width="600" src="{% asset_path Image4.png %}" title="Image4" class="img-left" />
</details>
</dev>

## 参考資料
- Blender 4.1 Reference Manual
[Scene Properties(外部リンク)](https://docs.blender.org/manual/en/latest/scene_layout/scene/properties.html)

## 最後に
自分がモデリングでClothシミュレーションを使うときはそのままモディファイアとして適応するし、開始位置を変える必要もないので、映像でSoftbodyを使って紙くずを飛ばす演出を作る時にちょっと戸惑いました。
　
本編と関係ない雑談シリーズですが、栄養失調みたいなもので体調が最悪な状態になってました。
ブログに書き残すことがCGのモチベになりつつあるので、今日からまた頑張ろうと思いますー。
　
閲覧頂きありがとうございました。