---
author:
- '@ottanxyz'
categories:
- Mac
date: 2019-06-29 00:00:00+00:00
draft: false
tags:
- catalina
- ボリューム
- mojave
- macos
- インストール
title: macOS Mojaveの環境を壊さずにmacOS Catalinaを試す方法
toc: true
type: post
---

![](190629-ea91ab94c61a1e81.jpg)

macOS Catalinaを今すぐ試す方法をご紹介します。新機能は今すぐ試したいですけど、仕事やプライベートで普段使用している環境にβ版のソフトウェアをインストールすることは避けたいですよね。

ただ、Time Machineで事前にフルバックアップを取得しておいて、事前準備を入念にした上で既存環境をアップデートする。そして、ソフトウェアが動かないなどの問題があれば元に戻す。考えただけでも時間がかかりそうです。

そこで、今回は既存の環境を壊さずに、macOS Catalina Public Betaを今すぐお試しする方法をご紹介します。毎回、恒例の記事なので、ご存知の方は読み飛ばしていただいて構いません。

## macOS Catalinaを別のボリュームにインストールする

macOS MojaveとCatalinaの環境を分離するために、ディスクユーティリティで既存のAPFSコンテナに新規ボリュームを作成しましょう。ファイルシステムの標準が、HFS+からAPFSに変わり、ボリュームの作成方法が今までと若干異なりますので注意してください。

### ディスクユーティリティで新規ボリュームを作成する

「/Applications/Utilities/Disk Utility.app」を開きます。macOS Mojaveがインストールされているボリュームを選択し、「パーティション作成」をクリックします。

![](190629-06d0ebdc490cd140.png)

「ボリュームを追加」をクリックします。

![](190629-95ac16650fff53fd.png)

分かりやすいボリューム名にしておきましょう。今回は、`Catalina`としました。また、フォーマットは「APFS」を選択します。「追加」をクリックします。「容量」は自動的に割り当てられるため、気にしなくて大丈夫です。

![](190629-c42933f42edae34a.png)

### Public Beta Software Programに登録

Catalinaはまだβ版のため、[Apple Beta Software Program](https://beta.apple.com/sp/ja/betaprogram/)へ登録する必要があります。登録が完了したら、上部メニューの「デバイスを登録」をクリックします。

![](190629-8beb6179c36b5286.png)

少し下にスクロールし、「macOS Public Betaアクセスユーティリティをダウンロード」をクリックします。

![](190629-dda9de0afd3db654.png)

ダウンロードされたインストーラをダブルクリックし、ウィザードの内容に従いインストールします。すると、自動的にシステム環境設定の「ソフトウェア・アップデート」が起動します。「今すぐアップグレード」をクリックしましょう。既存のボリュームがそのまま上書きされることはありませんので、そのまま進めてください。

![](190629-a164aac7d1795259.png)

しばらくすると、Catalinaのインストーラが起動します。

![](190629-dd925d36177a728d.png)

インストールするボリュームを選択する画面が表示されます。**Machintosh HDは既存のボリュームのため、誤って上書きしないよう注意してください**。「すべてのディスクを表示」をクリックしましょう。

![](190629-7bb1993df73c8950.png)

先ほど作成したボリューム（今回は`Catalina`）を選択します。

![](190629-b54da3f3dc878dcf.png)

インストールが完了すると、自動的に再起動を促すメッセージが表示されます。

### 「macOS Installer」ボリュームを選択して起動する

<kbd>&#8997;</kbd>を押しながら再起動することで、起動するボリュームを選択できます。「Machintosh HD」に加えて、「macOS Installer」というボリュームが増えています。起動時にこちらを選択すると、そのまま新規作成したボリュームに対して「Catalina」のインストールが始まります。

## 注意点

macOS Catalina Public Betaをインストールする上で、いくつか注意事項があります。

### Catalinaが専有するボリュームのサイズ

「Catalina」をインストールすると、「Catalina」「Catalina - Data」という2つのボリュームが自動的に作成されます。事前に作成したボリューム名によって、この名称は変更されます。macOS Catalinaから、システムボリュームと、ユーザが自由に読み書き可能なボリューム（データボリューム）が完全に分離されました。

![](190629-e3707038ade6dc07.png)

初期設定だけを済ませた状態で、Catalinaのボリュームは、システムボリュームが約10GB、データボリュームが約5GBでした。Catalinaをインストールすることで、約15GBのサイズを専有すると考えておいたほうが良いでしょう。

### インストール時にApple IDの設定はスキップするか、新規Apple IDを取得する

macOS Catalinaのインストール時に、Apple IDを設定する画面が表示されます。このApple IDの設定は後からでもできるので、インストール時にはスキップしましょう。というのも、macOS MojaveとCatalinaで同一のApple IDを使用した場合、iCloud Driveの領域が二重に使用されたりするなど、何らかの問題が発生する可能性もあります。何がある、というわけではないのですが、これまでの経験上、予期せぬ問題が発生することも多いです。そもそもβ版ですし。

ただ、Apple IDを設定しないと、Mac App StoreやiCloudなどの機能はもちろん利用できません。もし、Apple IDを設定した場合は、新規にApple IDを取得しておくと良いでしょう。私も、β版を試用するために開発者用のApple IDを、普段利用するApple IDとは別に取得しています。

### ソフトウェア・アップデートに「Catalina」のアップデートが表示されるのをやめたい

macOS MojaveとCatalinaの環境を並存している場合、MojaveはPublic Beta Programにデバイスが登録されたままの状態になっています。そのため、ソフトウェア・アップデートを開くと、常にCatalinaに関するアップデートが表示されます。もし、Public Beta Programからオプトアウトしたい場合は、ソフトウェア・アップデートを開き、左下の「詳細」をクリックします。

![](190629-3e2876bb2817075d.png)

「デフォルトに戻す」でβ版のアップデートが受信されなくなります。

![](190629-40822bcf7f573e86.png)

### 起動ディスクをMachintosh HDに戻しておこう

macOS Catalinaをインストールすると、自動的に起動ディスクがCatalinaのボリュームに設定されます。OSを再起動すると、<kbd>&#8997;</kbd>を押さない限り自動的にCatalinaが起動してしまいます。Mojaveにしたい場合は、システム環境設定の「起動ディスク」からMojaveがインストールされているボリューム（Machintosh HD）を選択しておきましょう。

![](190629-d7a7e1d48d8a7eae.png)

### Catalinaのボリュームを削除したい

ディスクユーティリティから「Catalina」「Catalina - Data」のボリュームを削除してください。「消去」ではなく、「ボリューム」の「-」ボタンをクリックします。

![](190629-8d9b5e00cf7a6553.png)

## 参考リンク

- [Apple Beta Software Program](https://beta.apple.com/sp/ja/betaprogram/)
