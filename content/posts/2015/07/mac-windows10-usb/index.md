---
author:
- '@ottanxyz'
categories:
- Mac
- Windows
date: 2015-07-30 00:00:00+00:00
draft: false
tags:
- ディスク
- usbメモリ
- windows
- '10'
- iso
title: MacでWindows 10の起動ディスク（USBメモリ）を作成する方法
type: post
---

![](150730-55b9fb2281432.jpg)

Windows 7以来の大型アップデートとなるか、ついに本日Windows 10が公開されました。Windows 10の「ISO」ファイルは公開されているため、いつでもインストールできますが、今回は、MacでWindows 10の起動ディスクを作成する方法をご紹介します。4GB以上のUSBメモリが必要ですので注意してください。（※注意：必ず最後までお読みください）

## MacでWindows 10の起動ディスクを作成する

まずは下準備としてUSBメモリのフォーマットから行います。USBメモリのフォーマットはmacOS標準のアプリである「ディスクユーティリティ」から行います。

### ディスクユーティリティでUSBメモリを初期化する

MacにUSBメモリを差し込んだら、「アプリケーション」→「ユーティリティ」フォルダーにある「ディスクユーティリティ」を起動しましょう。USBメモリを選択した状態で「消去」タブをクリックし、「フォーマット」を「MS-DOS (FAT)」、「名前」を「UNTITLED」（デフォルト：任意で構いません）にし「消去」をクリックします。この時点でUSBメモリに格納されているデータはすべて削除されますので注意してください。

![](150730-55b9fb2384ecc.png)

### Windows 10のISOファイルを入手する

次にWindows 10のISOファイルをダウンロードします。ISOファイルは、Microsoftの公式サイトで配布されています。

- <https://www.microsoft.com/ja-jp/software-download/windows10ISO>

まず、エディションを選択します。「エディションの選択」から「Windows 10」を選択してください。選択したら、「確認」ボタンをクリックします。

![](150730-55b9fb255e5be.png)

次に、製品の言語を選択します。「日本語」を選択して「確認」ボタンをクリックします。

![](150730-55b9fb26ca460.png)

CPUのアーキテクチャによって、32bitまたは64bitを選択して、「32-bitのダウンロード」、または「64-bitのダウンロード」をクリックします。約4GBありますので、気長にダウンロードが完了するのを待ちましょう。

![](150730-55b9fb2800dc8.png)

### 起動ディスクを作成する

ここでは、`~/Downloads/Win10_Japanese_x64.iso`にファイルがダウンロードされていると仮定して話を進めていきます。ダウンロードしたISOファイルをUSBに書き込めるようにフォーマットを変換します。

```bash
hdiutil convert -format UDRW -o ~/Downloads/.img ~/Downloads/Win10_Japanese_x64.iso
```

以下のように表示されることを確認してください。_XXXXXX_は、現在Macにログインしているユーザ名です。これで起動ディスクを作成する準備は整いました。

    J_CCSA_X64FRE_JA-JP_DV5         （Apple_UDF：0） を読み込み中...
    ...............................................................................
    経過時間：18.324s
    速度：215.8M バイト／秒
    節約率：0.0%
    created: /Users/XXXXX/Downloads/.img.dmg

次に、USBメモリのディスクの番号を確認します。「アプリケーション」→「ユーティリティ」フォルダーの「ターミナル」を起動します。以下を入力してください。

```bash
diskutil list
```

Macにマウントされているディスクがすべて表示されます。この中から先ほどフォーマットしたUSBメモリのディスク番号をメモしておきます。デフォルトのままフォーマットした場合は、「UNTITLED」となっているディスク番号（図では、「/dev/disk2」）

![](150730-55b9fb29787e2.png)

次に、以下のコマンドを実行します。「disk_N_」の「N」については、先ほど確認したディスクの番号を入力してください。

```bash
diskutil unmountDisk /dev/diskN
```

実行後に、以下のように表示されることを確認してください。

    Unmount of all volumes on disk2 was successful

次に、以下のコマンドを実行します。_N_は、先ほど`diskutil list`で確認したディスクの番号です。_XXXXX_は、Macにログインしているユーザ名です。

```bash
sudo dd if=/Users/XXXXX/Downloads/.img.dmg of=/dev/diskN bs=1m
```

ログインしているユーザのパスワードを要求されますので入力します。また、「~/Downloads」ではなく、「Users/_XXXXX_/Downloads」のように、フルパスで入力する必要がある点に注意してください。また、変換には時間がかかりますので、気長にお茶を飲みながら待ちましょう。

    3953+1 records in
    3953+1 records out
    4145700864 bytes transferred in 432.549094 secs (9584348 bytes/sec)

このように表示されていれば問題なく起動ディスクの作成は完了しています。最後に以下のコマンドを実行し、USBメモリを抜き出すことができる状態にします。_N_は、先ほど`diskutil list`で確認した番号です。

```bash
diskutil eject /dev/diskN
```

これでいつでもUSBメモリを取り出せる状態になりました。

### Windows 10をクリーンインストールする

⌥（オプション）キーを押しながら、Macを再起動します。するとブートローダーにWindows 10の起動ディスクが認識されるはず。しかし、認識されませんでした。

## Boot Campアシスタントを使って起動ディスクを作成する

Macには、Boot Campと呼ばれるMacへのWindowsを導入するためのアシスタント機能が用意されています。これで、起動ディスクを作成することとしましょう。

### ディスクユーティリティでUSBメモリを初期化する

これは前項とまったく同様であるため内容については割愛します。

### Boot Campアシスタントで起動ディスクを作成します

Boot Camp アシスタントを起動して、「続ける」ボタンをクリックします。

![](150730-55b9fe5b1017e.png)

「Windows 7 またはそれ以降のバージョンのインストールディスクを作成」のみをチェックします。「Windows 7 またはそれ以降のバージョンを削除」はチェックを外します。

![](150730-55b9fe5e38e05.png)

ISOイメージに、自動的に事前にダウンロードしたWindows 10のISOファイルが選択されていることを確認します。また、保存先ディスクがUSBメモリになっていることを確認し、「続ける」ボタンをクリックします。

![](150730-55b9fe615a93f.png)

USBメモリが初期化される旨の警告ダイアログが表示されますが、そのまま「続ける」ボタンをクリックします。

![](150730-55b9fe64157de.png)

起動ディスクの作成が始まりますが、かなりの時間を要しますので気長にお茶でも飲みながら待ちましょう。

![](150730-55b9fe668f538.png)

途中、このようなダイアログが表示された場合は、管理者のユーザのユーザ名とパスワードを入力します。

![](150730-55b9fe685345f.png)

「Windows サポートソフトウェアが保存されました」という画面が表示された場合は正常終了しています。

![](150730-55b9fe69b27e1.png)

### Windows 10をクリーンインストールする

⌥（オプション）キーを押しながら、Macを再起動します。するとブートローダーにWindows 10の起動ディスクが認識され…ました！

![](150730-55b9fe747ffd9.png)

Windowsを選択すると、Windows 10をクリーンインストールできます。

## まとめ

従来の方法で起動ディスクが作成できないのは予想外でした。しかし、Boot Campアシスタントで無事起動ディスクを作成できました。手元にWindows環境がないためWindwsで起動ディスクを作成できない、という方はぜひお試しください。
