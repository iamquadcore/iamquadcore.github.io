---
title: IES Lightのすゝめ | CG雑談
date: 2024-04-28
tags: CG_Chat
categories: 3DCG
cover: img/covers/cg-chat-IES.jpg
banner: 
    type: img
    bgurl: img/banners/cg-chat-IES.jpg
    bannerText: 
og_image: img/covers/cg-chat-IES.jpg
---
# IES Lightのすゝめ
**「CGソフトに備わってるライトを一々それっぽく調整するのが手間！」**

みたいなことありますよね。多分。
そんな時に使える便利な物を紹介したいと思います。
　
それが**IES Light**です。
　
ざっくりいうと、IESとは、配光データというもので、それをベースに作られたライトをIES Lightといいます。
これを使うと現実の照明のような光り方を簡単に再現することができます。
　
UEは初心者なので解説が荒いかもですが、Blenderとともに使い方も書いておきます。

- 目次
  - [もう少し掘り下げると](#もう少し掘り下げると)
  - [Blender, UE5での使い方](#Blender-UE5での使い方)
  - [参考資料](#参考資料)
  - [最後に](#最後に)


## もう少し掘り下げると
先程も述べた通り、IES Lightは、現実の照明の設計や数値等をベースに、「光の形状(光度の分布)」、「光の強度」などをデータ化して3DCG上で再現できるようにしたものです。
　
といっても**Real IES**等のツールでIES Lightを作ることもできるので、「仮想光源」とか「リアル指向ライト」みたいな感じで捉えて大丈夫だと思います。
　
建築、設計系のCGでは厳密な定義があると思いますが、私は映像や画像を創作することのみを目的としているのでご容赦くださいませ。
　
使い方としては、「光源オブジェクトに.iesという拡張子のファイルを読み込ませる」といったシンプルなものです。
　
Blender 4.1 Cycles Renderのデフォルトの照明とIES Lightの比較はこんな感じ。
*光の強さは同じ値でも差があるので均一になるように調整しています。
<img width="700" src="{% asset_path Image1.jpg %}" title="Image1" class="img-left" />

~~ちょっとセッティングに手抜き感ありますが~~
読み込んだだけでこのクオリティは素晴らしいですね。
　
また、iesファイルを配布しているサイトもあります。
今回は一つ、恐らく最大手のサイトを紹介させていただきます。
- [IES-Library(外部リンク)](https://ieslibrary.com/)
　
話が本筋から逸れますが、大元のIES(Illuminating Engineering Society)とは、照明に関する技術や教育等を扱う実際に存在する協会、学会です。
想像以上に規模がでかいものが出てきてびっくりしましたが、調べたら結構面白かったです。
詳しくは[IESの公式サイト(外部リンク)](https://www.ies.org/about/)を御覧ください。
　
## Blender, UE5での使い方
iesファイルを適応する基本的な手順を置いときますね。
どちらのソフトもノードや設定からより細かく調整できます。
　
<strong>1.&nbsp;Blender 4.1</strong>

BlenderはCyclesレンダーのみ利用可能です。
(ライトにノードを適応できるのがCycles限定みたい)
　
ポイントライトを置いて、ノードを使用(Use Nodes)を押すとシェーダーエディターから調整できるようになります。
<img width="400" src="{% asset_path Image2.jpg %}" title="Image2" class="img-left" />

IES Textureノードを出して、iesファイルを指定すると使えます。
<img width="700" src="{% asset_path Image3.png %}" title="Image3" class="img-left" />
光の強さはIES Textureノードからもライト本体の設定からもできます。
　
<strong>2.&nbsp;Unreal Engine 5.3.2</strong>

UEもBlenderと同じ感覚でiesファイルを利用できます。
むしろ基本の設定項目にIESの設定箇所があるのでBlenderより少しだけ楽かも。
　
ポイントライトを置いて、設定のRenderingタブにある**Light Profile**に移り、
適応したいiesを画像の様にドラッグアンドドロップ、IESが持つ強度(Intensity)の値を使うようにチェックを入れます。
<img width="700" src="{% asset_path Image4.gif %}" title="Image4" class="img-left" />

ies適応後ライトが下を向いていないことがあるので修正して、さっきチェックを入れた箇所の下のIntensity Scaleの値を調整して終わりです。
　
## 参考資料
- ODED MAOZ ERELL'S CG LOG
[IES Lighting in CG(外部リンク)](https://odederell3d.blog/2018/09/09/ies-lighting-in-cg/)

- YouTube
[Stop Using The Default Lamp in Blender - IES Lights(外部リンク)](https://www.youtube.com/watch?v=8VSDWyDIBl8)

- YouTube
[How to use IES Light description in Unreal Engine.(外部リンク)](https://www.youtube.com/watch?v=KkKfkwo_ul8)
 ※UE4

## 最後に
Unityについてですが、情報が少なく軽く見た感じ複雑そうなので、分かり次第また記事にしようと思います。
　
企業さんによっては実際に売られている照明にIESが記載されていることもあるみたいなので、部屋モデリングなんかで実際の見え方に寄せて作ることができると思うと面白いですね～。
fbxを作った(所有してる)Autodeskみたいな建築設計CG系の会社が定めたような規格かと思ったら、想像と違う角度の情報が出てきてびっくりしましたｗ
世界って広いな...。
　
閲覧頂きありがとうございました。