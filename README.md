# ALE
ALE : A LaTeX Environmentは、Visual Studio Codeエディタを使う
LaTeX執筆環境の構築用スクリプト、ツール、およびサンプルLaTeX文書の
コレクションです
## 概要
ALEプロジェクトの目的は二つあります。
- Visual Sudio CodeによるLaTeX執筆環境のインストール・スクリプトを提供する
- 同環境での執筆環境のためのツールを提供する

ALEが構築する執筆環境はVisual Studio Codeと、そのうえで動作するLaTeX Workshopプラグインを用いたものです。LaTeX Workshopを使うことで、LaTeXファイルを保存するたびにビルドが自動的に行われ、Visual Studio Code上で即座に生成したPDFファイルが自動的に表示されます。執筆者はビルドのたびにコマンドを叩く必要はありません。

LaTeXは美しい文書を作ることが出来るツールですが、文献の整理や画像の挿入といった事を始めると、非常に多くのツールとの連携が必要になってきます。これらのツールを使う環境の準備や、手作業によるツールの起動を行っていては執筆に集中できません。

ALEは環境の手軽な設定と、画像をLaTeX文書を使うためのスクリプトを提供します。具体的にはスクリプトを使うことで以下の画像形式をLaTeX上で利用できるようになります。
- PDF
- PNG
- GIF
- JPEG
- DRAWIO

PDF以外の画像はスクリプトによってPDFに変換されます。変換はマルチプロセスで行いますので、大量の画像データがある場合もマルチコア・プロセッサを利用して手早く変換をすることが出来ます。

画像の変換はLaTeXのビルド・シーケンスに組み込まれているため、手作業で変換スクリプトを呼ぶ必要はありません。

## 試験環境

ALEのスクリプトは以下の環境で試験しています。
- Ubuntu 22.04 LTS + Visual Studio Code
- Ubuntu 22.04 LTS on WSL + Visual Studio Code on Windows 11. 

## 使い方
インストールが完了すると、LaTeX文書のソース(.tex)を開いた状態で以下のショートカットを利用できます。
- Alt-Ctrl-B : LaTeX文書のビルド
- Alt-Ctrl-V : 生成したPDFのプレビュー

一度ビルドを行うと、LaTeX文書のソースを保存するたびにビルドが行われプレビューがアップデートされます。

## インストール方法
インストール方法については[INSTALL.md](INSTALL.md)を参照してください。
## LaTeXプロジェクトの構造
LaTeXプロジェクトの構造に関しては[FILES.md](FILES.md)を参照してください。
## 既知の問題
### WSLでDRAWIOファイルの変換に失敗する
この問題はWSL上のUbuntuで発生します。
非WSLのUbuntu Desktop環境では発生しません。

WSL上のUbuntuにはD-BUSサービスが起動しない問題があります。この問題が発生すると、DRAWIOファイルをPDFに変換することが出来ません。
解決するには事前に以下のコマンドを実行してD-BUSサービスを
起動しておいてください。
```
sudo /etc/init.d/dbus start
```

### LaTeXワークショップによるビルドでDRAWIOファイルの変換に失敗する
この問題はLaTeXワークショップによる自動ビルド時に発生します。
コマンドラインからの実行では発生しません。

おそらくは[Visual Stuido CodeによるElectronアプリケーションの起動方法](https://github.com/microsoft/vscode-cmake-tools/issues/1545)が理由で発生しています。

DRAWIOファイルを使わない文書には影響はありません。

DRAWIOファイルを使う文書では、事前にscript/convert2pdfスクリプトをコマンドラインで実行してファイルを変換してください。

### 索引が空の場合にビルドが異常終了する
索引ページが空の場合はLaTeXのビルドに失敗します。

索引ページは\printindexおよびpreamble.texで宣言している\termマクロを
使用して作っています。文書中に\termによる用語登録が一つもない場合、
LaTeXはビルド中に異常終了します。

この問題を解決するには、最低一つの用語を索引に登録してください。あるいは
\printindexによる索引ページを削除してもよいです。

## ライセンス
本プロジェクトは[MITライセンス](LICENSE)に基づいて配布しています。
