# Python x Visual Studio Code x Jupyterlab x Qaurto でデータ分析レポートを速攻作成

## はじめに

- Quartoを使ってみたらPythonでのデータ分析レポート作成がとても便利だったので紹介します。
- 想定読者: Pythonでデータ分析をしている方、これからしようと勉強している方。
## Quartoとは

### [公式サイト](https://quarto.org/)解説(抜粋・翻訳)

- QuartoはPandocを使って科学技術ドキュメントを生成するオープンソースのシステムです
- MarkdownまたはJupyter notebookからドキュメントを生成できます
- Python, R, Juliaに対応
- HTML, PDF, MS Word, ePubで出力可能

### Jupyterlabによるレポート作成よりも優れている点

- コードが短くて済む
- コードを隠せる

詳細は後述します
## 準備

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
  - 拡張機能をクリック
  - "Marketplaseで拡張機能を検索する"のボックスにQuartoを入れ検索
  - 表示されたQuarto をインストールしてください

## 使用例

### マークダウン同様に書くことができます。下記はリスト記入例です。
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

- ファイルをqmd拡張子で保存するとVisual studio codeのQuarto拡張機能が働きます
- 右上のRenderをクリック
- Render HTMlをクリック

出力例。３Dグラフをドラックすると、見る角度を動かすことができます。

出力元のqmdファイル含めソースコードはこちら

### 参考サイト

- [Pandocユーザーガイド](https://pandoc-doc-ja.readthedocs.io/ja/latest/users-guide.html)
  - Markdown書式の解説などがあります
- [R Markdownによるレポート生成](https://qiita.com/tomotagwork/items/c92fb40a76f56ea16aa4)
  - R Markdown(R言語+Markdown)はQuartoとは別物ですが、とても似ているので書き方・活用の仕方の参考になると思います。特に現時点では、日本語のQuartoの解説記事が少ないので。