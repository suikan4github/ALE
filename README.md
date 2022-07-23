# ALE
A Latex Environment : Script and document to create the Latex environment for WSL+VS CODE


## 既知の問題
### WSLでDRAWIOファイルの変換に失敗する
この問題はWSL上のUbuntuで発生します。
非WSLのUbuntu Desktop環境では発生しません。

WSL上のUbuntuにはD-BUSサービスが起動しない問題があります。この問題が発生すると、DRAWIOファイルをPDFに変換することが出来ません。
解決するには事前に以下のコマンドを実行してD-BUSサービスを
起動しておいてください。
sudo /etc/init.d/dbus startv