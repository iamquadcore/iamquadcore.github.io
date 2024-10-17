---
title: UVマップを変形させずにオブジェクトを編集する方法 | Blender
date: 2024-04-23 
tags: Blender
categories: 3DCG
cover: img/covers/cg-b3d-stretchmesh.png
banner: 
    type: img
    bgurl: img/mainimages/good bye to a world small.png
    bannerText: 
---
# UVマップを変形させずにオブジェクトを編集する方法
通常、押し出し(Extrude)や面を引き伸ばす時に適応したUVも引き伸びます。
今回はその伸縮や変形を回避する方法になります。
主にループテクスチャを使っているときに有効です。

<div class="image">
  <div>
    <ul>
        <dd><img width="300" src="{% asset_path Image2.png %}" title="Image1" class="img-left" /></dd>
        <dd><img width="300" src="{% asset_path Image1.png %}" title="Image2" class="img-left" /></dd>
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

## 前提
・使用ソフト:Blender
・バージョン:3.4
・レンダラー:Cycles/Eevee
・言語:英語
・その他:4.1でも問題なくできます。

## 設定方法
編集したいオブジェクトを選択してEditモードに切り替えます。
　
そのまま3D Viewの右上にあるOptionから**面の属性を修正(Correct Face Attributes)** にチェックを入れます。
<img width="350" src="{% asset_path Image3.png %}" title="Image3" class="img-left" />

これで完了です。
　
押し出しだけでなく移動による面の引き伸ばしにも適応されます。

<img width="500" src="{% asset_path Image4.png %}" title="Image4" class="img-left" />

すでに展開済みのUVマップを元にしてくれるみたいなので、延長線上にないある辺をいきなり押し出しするとダメみたいです。
　
最初の画像の押し出した側面とかが例ですね。

## 最後に
Blenderでループテクスチャを使ってモデリングする自分にとっては結構便利な機能だと思いました。
　
雑に撮ったやつですが、綺麗に展開してくれてますね。
<img width="500" src="{% asset_path Image5.png %}" title="Image5" class="img-left" />

終盤ミスに気づいてちょっと手を加えたりする時に役立ちました。
　
閲覧頂きありがとうございました。