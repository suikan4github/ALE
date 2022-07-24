# ALEが対応するLaTeX文書プロジェクトのディレクトリ構造

ALEのサンプルLaTeX文書プロジェクトのディレクトリ構造は以下の通りです。
```
../ALE
├── FILES.md
├── install
├── INSTALL.md
├── LICENSE
├── README.md
└── sample                          : LaTeX文書プロジェクトの文書ルート・ディレクトリ
    ├── 000_preface.tex             : TeXソース「初めに」。
    ├── 010_body.tex                : TeXソース。本文。
    ├── a10_appendix.tex            : TeXソース「付録」。
    ├── b10_authers_note.tex        : TeXソース「あとがき」。
    ├── image                       : ALEの作業用ディレクトリ。筆者は使わない。
    ├── image_src                   : 文書で使用する画像ファイルのソース・ファイルを納める。
    │   ├── diagram.drawio          : DRAWIOファイルの例。
    │   ├── IMGP3933.pdf            : PDFファイルの例。
    │   ├── IMGP3954.jpg            : JPEGファイルの例。
    │   ├── paint1.png              : PNGファイルの例。
    │   └── paint2.gif              : GIFファイルの例。
    ├── out                         : LaTeXの出力ディレクトリ。PDFはここに出力される。
    ├── .latexmkrc                  : latexmkの動作を決める設定ファイル。
    ├── preamble.tex                : TeXソース。プリアンブル。
    ├── sample.bib                  : BiBTeXのソース。
    ├── sample.tex                  : TeXソース。文書のトップ構造を記述したファイル。
    └── script                      : 画像処理用スクリプト集
        ├── convert2pdf             : sampleディレクトリの中のファイルをPDFに変換する。
        └── process_of_conversion   : 下請けスクリプト。ユーザーは直接使わない。
```

いくつか重要なファイルとディレクトリがあり、それらはALEを
使う場合上記と同じ位置に同じ名前で配置してある必要があります。

なお、以下で「文書ルート」と呼ぶとき、それはLaTeX文書プロジェクトの最上位ディレクトリを指します。
上のディレクトリ構造では"sample"が文書ルートです。

## 必須ファイルとディレクトリ

### image_src
image_srcは文書内に埋め込む画像のソース・ファイルを置く場所です。
ここに置いたファイルはLaTeX文書のビルド時に自動的にPDFファイルに変換
されてimageディレクトリにコピーされます。

### image
imageは上述の通り自動的に作られ、画像ファイルから変換されたPDFファイルが置かれる場所です。
執筆者はimage_srcの中の画像ではなくimageの中のPDFを参照してLaTeXソース・ファイルを書いて
ください。

### script
scriptは画像変換用のスクリプトを納めているディレクトリです。このディレクトリの中の
スクリプトはALEがLaTeXをビルドする際に自動的に呼ばれます。スクリプトはsampleからコピー
してください。変更の必要はありません。

なお、画像の変換を人手で行いたいときは、文書ルートから以下のプログラムを
実行してください

```
script/convert2pdf
```

### .latexmkrc
.latexmkrcはlatexmkコマンドに対して、実行のルールとステップを説明するためのファイルです。
このファイルはsampleからコピーして使ってください。変更の必要はありません。
