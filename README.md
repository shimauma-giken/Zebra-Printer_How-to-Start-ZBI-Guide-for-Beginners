## ZBI2.0を用いてBluetooth経由でスキャナから直接ラベル印刷をする方法

本ガイドはDS8178をベースに説明をする。
他スキャナを利用の際は設定が一部異なる可能性があることをご了承頂きたい。

</br>

### プリンタの初期設定

1. プリンタを工場出荷状態に戻す。


    [Link-OS プリンタを工場出荷状態に戻す方法](https://github.com/shimauma-giken/Zebra-Printer_Factory-Reset-Link-OS-Printer#link-os-%E3%83%97%E3%83%AA%E3%83%B3%E3%82%BF%E3%82%92%E5%B7%A5%E5%A0%B4%E5%87%BA%E8%8D%B7%E7%8A%B6%E6%85%8B%E3%81%AB%E6%88%BB%E3%81%99%E6%96%B9%E6%B3%95)

1. 利用サプライが利用できるように、プリンタの初期設定をする。
    - 用紙の設定
    - 通信設定

### ZBIの設定

1. ZBIをActivateする。

    [Activating ZBI (Zebra Basic Interpreter) Article ID:000015434  •  February 15, 2022](https://supportcommunity.zebra.com/s/article/Activating-and-deactivating-ZBI-Zebra-Basic-Interpreter?language=en_US)

### ZBIコーディング

1. ZBI Developersをインストールする。

    [ZBI Developer Download](https://www.zebra.com/us/en/support-downloads/software/printer-software/zebra-basic-interpreter-zbi.html)

1. ZBI DeveloperでZBIコードを開発する。

    ZBIの開発に関する情報は[ZPLプログラミングガイド](https://www.zebra.com/content/dam/support-dam/en/documentation/unrestricted/guide/software/zpl-zbi2-pg-en.pdf)を熟読すること。

### ZBIインストーラ作成

1. ZBI インストーラ（ZPLファイル）を作成する。

    ```
    "ZBIファイル"を右クリック > "Export ZBI Program"
    ```

    ![alt text](image.png)


1. インストール先情報を入力する。

    ![alt text](image-1.png)

    |項目|説明|
    |------|---------|
    |Name| インストーラの保存先（ローカルPC）|
    |Script Name | プリンタに保存するファイル名（*.BAS) |
    |Momory Location    | "E"を選択すること

### ZBIをプリンタにインストール


1. 下記ファイルをZebra Setup Utilitiesを用いてプリンタに送信する。
    ```
    "Open Printer Tools" > Settings > Send File (作成したファイルを選択) > Send
    ```
    ![alt text](image-2.png)

### ZBIの実行


1. プリンタにインストールされたZBIを実行する。

    ```
    構文、
     ^XA^JIE:[filename],N,N,50K^FS^XZ
    
    例、
     ^XA^JIE:HELLO01.BAS,N,N,50K^FS^XZ

     ```

    - 液晶メニューからの実行でもOK。

     ```
    "メニュー" > "システム" > "プログラム言語" > "言語" > (インストールしたBASファイルを選択し、実行)
     ```


1. 実行したZBIの検証をする。


### [Tips] 常時ZBIを実行する場合の設定

1. Autoexecのインストーラを作成する。

    ```
    "ZBIファイル"を右クリック > "Generate Autoexec.zpl"
    ```
    ![alt text](image-3.png)

    |項目|説明|
    |------|---------|
    |Name| インストーラの保存先（ローカルPC）|
    |Script Name | 実行するZBIファイル名（*.BAS) |
    |Console    | メモリ使用容量。わからないときはデフォルト値のままにしておく |

1. 
