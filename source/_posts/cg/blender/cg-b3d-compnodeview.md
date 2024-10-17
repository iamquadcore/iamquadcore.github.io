---
title: コンポジターでレンダー結果を表示するあれこれ | Blender
date: 2024-04-21
tags: Blender
categories: 3DCG
cover: img/covers/cg-b3d-compnodeview.png
banner: 
    type: img
    bgurl: img/banners/cg-b3d-compnodeview.png
    bannerText: 
---
# コンポジター（コンポジットノード）でレンダー結果を表示する設定と操作

個人的に地味に忘れがちなやつだったのでメモとして置いときます(´・ω・｀)
　
Blenderでレンダー結果に手を加える時に必須の操作です。

## 前提
・使用ソフト:Blender
・バージョン:4.1
・レンダラー:Cycles
・言語:英語
・その他:なし

## 設定
コンポジター(Compositor)のプレビューはレンダー結果を元にするので、まずはレンダリングをします。
　　
次に適当な窓から切り替えるか、上のタブからコンポジターを表示します。
<img width="300" src="{% asset_path Image1.png %}" title="Image1" class="img-left" />

<img width="700" src="{% asset_path Image2.png %}" title="Image2" class="img-left" />
<br>
続いて背景(Backdrop)を有効化、ビューアー(Viewer)ノードを出して、レンダー結果をプレビュー画面に繋ぎます。
<img width="700" src="{% asset_path Image3.gif %}" title="Image3" class="img-left" />

## 操作
V : 縮小
Alt+V : 拡大
Alt+ホイールクリック+ドラッグ : 移動

<img width="700" src="{% asset_path Image4.gif %}" title="Image4" class="img-left" />

また、横のViewタブからも調整できます。

## 最後に
コンポジットではレンダリング時に深度を抽出してそれを元に後ろをぼかしたり、
ノードで後からデノイズしたりと単純な加工以外にも色々できるので、この機能は必須知識です。
　
が、自分は過去３回程Viewerノードを繋げないと映らないことを忘れたので書きました。
　　
閲覧頂きありがとうございました。