# Python, Visual Studio Code, Jupyterlab, Qaurto でデータ分析レポートを速攻作成

## はじめに

- Quartoを使ってみたらPythonでのデータ分析レポート作成がとても便利だったので紹介します。
- 想定読者: Pythonでデータ分析をしている方、これから始めようとしている方。(Pythonおよびマークダウンを書いたことがあると想定します)
- なおR Markdown+RStudioと非常に似ていますが、R/RStudioをインストールしなくても使える点が便利です。
## Quartoとは

### [公式サイト](https://quarto.org/)解説(抜粋・翻訳)

- QuartoはPandocを使って科学技術ドキュメントを生成するオープンソースのシステムです
- MarkdownまたはJupyter notebookからドキュメントを生成できます
- Python, R, Juliaに対応
- HTML, PDF, MS Word, ePubで出力可能

### Jupyterlabによるレポート作成(HTML出力)よりも優れている点

- ソースコードが短くて済む
  - 今回サンプルをJupyterlabのipynbファイルで作ると1354行、Quartのqmdファイルでは50行と短くてすみますので見直しや転用、Git管理が楽です。
- 出力HTML上で、コードを隠すこともできる
  - 一般の人にレポートを共有するのに向いています。方法は後述します。

## Quarto環境の準備

### Pythonのインストール

省略します

### Visual Studio Codeのインストール

- [公式サイト](https://code.visualstudio.com/download)から、"Windows8,10,11"又は"Mac"等をクリックして利用OSに対応したインストーラ/アプリケーションをダウンロードしてください。
### Jupyterlabをインストール

Macの場合 terminal.appで

```
$ pip3 install jupyterlab
```

Windowsの場合 PowerShellで

```
pip install jupyterlab
```

### Quarto CLIをインストール
 - [公式サイト](https://quarto.org/docs/get-started/)の"Download Quarto CLI"をクリック
 - ダウンロードされたファイルを使ってインストールしてください

### Visual studio codeの拡張機能をインストール
  - Visual studio codeを開き、左側の拡張機能アイコンをクリック
  - "Marketplaseで拡張機能を検索する"のボックスにQuartoを入れ検索
  - 表示されたQuarto をインストール

## 作成例

### 初期設定

.qmd拡張子でファイルを新規作成しVisual Studio Codeで編集します。冒頭に下記を入れます。title:のところに書いてある内容が、レポートの冒頭に大きく表示されます。

```python: index.qmd
---
title: "Quarto sample"
format:
  html:
    code-fold: false
jupyter: python3
---
```

出力したレポートでcodeを隠したいときは下記のようにcode-fold: trueとしてください

```python: sample2.qmd
---
title: "Quarto sample2"
format:
  html:
    code-fold: true
jupyter: python3
---
```

### リスト記入例
通常のマークダウンと同様に書くことができます。
```
- This is Quarto sample.
- これはQuartoのサンプルです。
```

### Print
コードチャンク(コードを書く場所のこと)を作り、実行すると出力されます。
```python: index.qmd
print('Hello, world!')
```
Hello, world!

### 計算
計算も可能です
```python: index.qmd
a=3
b=5
a+b
```
8

### 表

表を埋め込むこともできます

```python: index.qmd
import pandas as pd
price_list=pd.DataFrame({"お品物":["牛丼","ラーメン"],"値段(円)":["300","400"]})
price_list
```

### グラフの描画

グラフを埋め込むこともできます

```python: index.qmd
import numpy as np
import plotly.graph_objects as go
N = 30
t=np.linspace(0,1,N)
x0=np.cos(t*4*np.pi)
y0=np.sin(t*4*np.pi)
z0=t*10
fig = go.Figure(data=[go.Scatter3d(x=x0, y=y0, z=z0,
                                   mode='markers',
                                   marker=dict(
                                    size=3,
                                    color=z0,
                                    colorscale='mygbm',
                                    opacity=0.7
    ))])
fig
```

### HTMLに出力

上記で作った.qmdファイルをもとに、HTMLに出力します。
#### 手順

- Visual studio codeのQuarto拡張機能を使います。
- .qmdファイルを開いた状態で、右上のRenderをクリックすると、pythonコードが実行されたうえでHTMLに変換されます。
- 完了するとVisual studio code内でプレビューが出てきます。
- ワーキングディレクトリ内に変換されたHTMLが保存されますので、そちらからも出力結果を見ることができます。

#### 事例

#### HTML出力例

- 本記事で解説したindex.qmdのHTML出力例を公開しています。
  
https://nobukuni-hyakutake.github.io/Quarto_sample/index.html

- index.qmdと内容が同じだが、コードを隠す指示をしてHTML出力したもの。ソース：sample2.qmd,出力: sample2.htmlです。HTML上で"Code"をクリックするとコードを見ることができます。
  
https://nobukuni-hyakutake.github.io/Quarto_sample/sample2.html

- index.qmdと内容が同じで、Jupyterlabで作りHTML出力したもの。ソース: jupyterlab_sample.ipynb、出力：jupyterlab_sample.html。Quartoで作成したものと比べてセル番号が入っているのと、ページ全体のレイアウトが全幅になるなど、一部が違います。
  
https://nobukuni-hyakutake.github.io/Quarto_sample/jupyterlab_sample.html

#### 全ソースコードおよび出力結果

https://github.com/Nobukuni-Hyakutake/Quarto_sample
