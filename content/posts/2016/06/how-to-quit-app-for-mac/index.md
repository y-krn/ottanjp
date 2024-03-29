---
author:
- '@ottanxyz'
categories:
- Mac
date: 2016-06-02 00:00:00+00:00
draft: false
tags:
- アプリケーション
- メニュー
- 6つ
- ショートカット
- キーボード
title: Macの基礎：Macでアプリケーションを終了させる6つの方法
type: post
---

![](160602-57502d48e7a58.jpg)

WindowsからMacに乗り換えた時に戸惑うのがアプリケーションの扱い方。Windowsと概念はよく似ていますが、Macでのアプリケーションの扱い方の基礎として、アプリケーションを終了させる方法をご紹介します。

## アプリケーションを終了させる6つの方法

一般的な方法から、一風変わった方法まで、6つの方法をご紹介します。

### アプリケーションのメニューから終了する

![](160602-57502d5291bd8.png)

アプリケーションを起動すると、画面上部のメニューバーにメニューが表示されます。アプリケーション名のメニュー（の隣にあります）をクリックすると、「[アプリケーション名] を終了」という項目があります。こちらのメニューをクリックすると、アプリケーションを終了できます。

### Dockからアプリケーションを終了する

![](160602-57502d59b335a.png)

アプリケーションを起動すると、画面下部のDockと呼ばれるバーにアプリケーションのアイコンが現れます。また、デフォルトの設定では、アクティブなアプリケーションにはインジケーターー（アプリケーションのアイコンの下の点）が表示されます。このアプリケーションのアイコンを⌃（control）を押しながらクリックする（副クリック／右クリック）と、「終了」というメニューが表示されます。こちらをクリックしてアプリケーションを終了させることができます。

また、⌥（option）を押しながら右クリックすると、応答のないアプリケーションを強制終了させることもできます。

### キーボードショートカットからアプリケーションを終了する

キーボードショートカットを使用してアプリケーションを終了させることもできます。キーボードでアプリケーションを終了させるためには、⌘（command）+Qを押します。このショートカットは、「システム環境設定」→「キーボード」→「ショートカット」から変更することもできます。

### メニューバーのアイコンからアプリケーションを終了する

![](160602-57502d605effe.png)

アプリケーションによっては、Dockにアイコンを表示せず、メニューバーに常駐するものもあります。このようなアプリケーションを終了させる場合は、メニューバーに表示されたアプリケーションのアイコンをクリックします。すると、たいていの場合、メニューの最下部に「[アプリケーション名] を終了」という項目があります。そのメニューをクリックすると、アプリケーションを終了させることができます。

### アクティビティモニターからアプリケーションを終了する

![](160602-57502d662333f.png)

「アプリケーション」→「ユーティリティ」フォルダーの下に、「アクティビティモニター.app」という見慣れないアプリケーションがあります。これは、Windowsのタスクマネージャーのようなものです。CPU消費率、メモリ消費率、エネルギー消費率（バッテリーに影響を与えるアプリケーション）の降順に並べ替えて、消費率の多いアプリケーションを見つけて、強制的に終了させることもできます。アプリケーションを終了させるためには、該当のアプリケーション名を選択して、左上の __ アイコンをクリックします。

### ターミナルからアプリケーションを終了する

![](160602-57502da140af2.png)

最後は、少し変わった方法のご紹介です。「アプリケーション」→「ユーティリティ」フォルダーの下に「ターミナル.app」というアプリケーションがあるので、こちらを起動します。起動したら、以下のコマンドを実行してください。

    osascript -e 'quit app "[アプリケーション名]"'

たとえば、「MarsEdit.app」というアプリケーションを終了させるためには、以下のコマンドを実行します。

    osascript -e 'quit app "MarsEdit"'

## まとめ

とくに、⌘+Qコンボは覚えておいて損のないキーボードショートカットです。頻繁に使用しますので、これを機に使用してみてください。

### 参考リンク

<http://www.idownloadblog.com/2016/06/01/quit-apps-mac/>
