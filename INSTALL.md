# PaleALEのインストール

PaleALEのインストールは3つの手順を踏みます。
1. ツール類のインストール
2. LaTeX Workshopのインストールと設定
3. LaTeXプロジェクト構造の設定

このうち、1と2はコンピュータ（あるいはユーザー・アカウント）に対して1度だけ行えば済みます。3はLaTeX文書プロジェクト（つまり論文や書籍）ごとに設定する必要があります。

PaleALEはVisual Studio Codeをインストールしません。Visual Studio Codeは手作業でインストールしてください。

以下にこれらの作業について説明します。なお、Ubuntu / WSL / Visual Studio Codeのインストール方法及び一般的な使い方については説明しません。これらについては各種資料を参考にしてください。

## ツール類のインストール
ツール類のインストールを行うには、PaleALEプロジェクトのルート・ディレクトリにあるinstallスクリプトを実行してください。引数は不要です。

```
install
```
インストール・スクリプトは以下のツールと、その他必要なモジュールをインストールします。
- TeX Live
- DrawIO
- ImageMagick

また、ImageMagickについてはポリシー・ファイルを編集し、PDFデータを出力できるようにします。

インストール中に必要に応じてUbuntuのユーザー・パスワードを聞いてきますので入力してください。パスワードを聞くのはインストール開始時と終了時の2回です。

また、これらとは別にインストール途中に2回ユーザーに問い合わせがあります。

1. cpanからのモジュールのインストールについて、自動設定を行ってよいか。
2. LaTeXのインストールについて、どのようなアクションを取るか。

1.についは"Yes"（自動設定を認める）, 2.については"I"（インストールを行う）と指定することでインストールを行うことが出来ます。

## LaTeX Workshopのインストールと設定
[LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop)はVisual Studio Codeの拡張機能であり、LaTeX文書作成時にユーザーを支援してくれるモジュールです。

LaTeX Workshop拡張機能のインストールに当たっては当然ながら事前にVisual Studio Codeをインストールしている必要があります。拡張機能のインストールについてはLaTeX Workshopの[公式ページ](https://github.com/James-Yu/LaTeX-Workshop/wiki/Install#installation)を参考にしてください。

LaTeX Workshopのインストール後、Visual Studio Codeのsetting.jsonを編集します。settings.jsonの開き方についてはネット上に多くの資料がありますのでそちらを参考にしてください。例えば[VS Codeのsettings.jsonの開き方](https://qiita.com/y-w/items/614843b259c04bb91495)が参考になるでしょう。

Settings.jsonを開いたら、以下のコードを追加してください。なお、追加にあたってはJSON形式をある程度理解している必要があります。事前にならんかの試料を読んでおく事をお勧めします。

大雑把に言えば、一番外側の"{"と"}"の中に以下のコードを埋め込みます。

このコードは[VSCode で最高の LaTeX 環境を作る](https://qiita.com/rainbartown/items/d7718f12d71e688f3573)で公開されている設定ファイルを変更して、LaTeXのビルド前に画像ファイルの変換を行うようにしたものです。

```JSON
    // ---------- Language ----------
    "[tex]": {
        // スニペット補完中にも補完を使えるようにする
        "editor.suggest.snippetsPreventQuickSuggestions": false,
        // インデント幅を2にする
        "editor.tabSize": 2
    },
    "[latex]": {
        // スニペット補完中にも補完を使えるようにする
        "editor.suggest.snippetsPreventQuickSuggestions": false,
        // インデント幅を2にする
        "editor.tabSize": 2
    },
    "[bibtex]": {
        // インデント幅を2にする
        "editor.tabSize": 2
    },
    // ---------- LaTeX Workshop ----------
    // 使用パッケージのコマンドや環境の補完を有効にする
    "latex-workshop.intellisense.package.enabled": true,
    // 生成ファイルを削除するときに対象とするファイル
    // デフォルト値に "*.synctex.gz" を追加
    "latex-workshop.latex.clean.fileTypes": [
        "*.aux",
        "*.bbl",
        "*.blg",
        "*.idx",
        "*.ind",
        "*.lof",
        "*.lot",
        "*.out",
        "*.toc",
        "*.acn",
        "*.acr",
        "*.alg",
        "*.glg",
        "*.glo",
        "*.gls",
        "*.ist",
        "*.fls",
        "*.log",
        "*.fdb_latexmk",
        "*.snm",
        "*.nav",
        "*.dvi",
        "*.synctex.gz"
    ],
    // 生成ファイルを "out" ディレクトリに吐き出す
    "latex-workshop.latex.outDir": "out",
    // ビルドのレシピ
    "latex-workshop.latex.recipes": [
        {
            "name": "latexmk",
            "tools": [
                "convert2pdf",
                "latexmk"
            ]
        },
    ],
    // ビルドのレシピに使われるパーツ
    "latex-workshop.latex.tools": [
        {
            "name": "latexmk",
            "command": "latexmk",
            "args": [
                "-silent",
                "-outdir=%OUTDIR%",
                "%DOC%"
            ],
        },
        {
            "name": "convert2pdf",
            "command": "script/convert2pdf",
        },
    ],
 
```
## LaTeXプロジェクト構造の設定
これまでのインストールと設定はコンピュータ1台（あるいはユーザーアカウント1つ）につき一度だけ必要なものでした。LaTeXプロジェクト構造は、論文や書籍ごとに設定しなければなりません。

必要な作業は以下の通りです。なお、この説明において「文書ルート」とはプロジェクトの最上位ディレクトリの事です。文書ルートにはLaTeXのソース・ファイルをおさめます。すなわち、*.texファイル起き場です。
1. 文書ルートに.latexmkrcをコピーする
2. 文書ルートにscriptディレクトリをコピーする
3. 文書ルートにimage_srcディレクトリを作る

.latexmkrcは、PaleALEが使用するlatexmkコマンドの設定ファイルです。このファイルは、TeXビルドの各パスで何をするかを指定しています。なお、.latexmkrcファイルは[VSCode で最高の LaTeX 環境を作る](https://qiita.com/rainbartown/items/d7718f12d71e688f3573)で公開されているものをそのまま使用しています。

.latexmkrcは文書ルートディレクトリのほか、ホームディレクトリにおいても構いません。

scriptディレクトリにはファイル変換を行うスクリプトが納められています。手作業で変換する場合は、文書ルートからコマンドラインで以下のスクリプトを実行してください。

```
scirpt/convert2pdf
```

image_srcディレクトリは名前の通り、LaTeX文書に挿入する画像のソースを置きます。ここには、GIF, PND, JPEG, PDF, draw.ioファイルを置くことが出来ます。PaleALEはビルド中に文書ルート直下にimageディレクトリを作り、image_srcの画像ファイルから生成したPDFファイルを置きます。

文書ディレクトリの構造については[FILES.md](FILES.md)も参考にしてください。
