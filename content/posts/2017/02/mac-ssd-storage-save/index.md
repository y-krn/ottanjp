---
author:
- '@ottanxyz'
categories:
- Mac
date: 2017-02-11 00:00:00+00:00
draft: false
tags:
- sierra
- ストレージ
- 書類
- ファイル
- 容量
title: Macの内蔵ストレージを効率的に節約する方法（macOS Sierra編）
type: post
---

![](170211-589e83b9c1db7.jpg)

macOS Sierra で追加された新機能といえば、しばらく前の iOS から搭載されている Siri が有名ですが、Siri 以上に素晴らしいと個人的に感じている機能がストレージの管理機能です。過去にも[Mac のストレージの空き容量が少なくなったら、GrandPerspective で肥大化させている項目を特定しよう！](/posts/2016/02/mac-storage-grandperspective-6840/)など、サードパーティ製アプリを使用して、巨大なファイルを検索して掃除する方法をご紹介しましたが、もうサードパーティの力は必要ありません。

とくに、MacBook などの内蔵ストレージ（SSD）の容量の小さな筐体の場合、増設もできないため、いざとなったら外付けの HDD にデータを退避してということもできますが、極力ムダなファイルを減らしていくということがもっとも効果的な方法です。今回は、そのための補助となる macOS Sierra の新機能を紹介します。

## macOS Sierra で内蔵ストレージの使用状況を効率的に管理しよう

いつの間にやら Mac の内蔵ストレージの空き容量が少なくなっている、といった経験をしたことがある方は少なくないはずです。macOS Sierra 以前の場合は、冒頭のサードパーティ製のアプリを使用して、ストレージを占有するファイルを見つける方法が一般的でしたが、macOS Sierra からは OS 標準機能で簡単に見つけることができます。

![](170211-589e86ca3ebeb.png)

方法はいたって簡単です。メニューバーの「」→「この Mac について」を開きます。「この Mac について」自体は、macOS Sierra 以前の OS にも搭載されています。Mac のハードウェア情報を一瞥することができるため、Mac のモデル名（Late 2013 など）やサポート対応に必要なシリアル番号等を簡単に確認できます。この画面が開いたら「ストレージ」タブを選択します。

![](170211-589e83c5cf529.png)

この画面も macOS Sierra 以前の OS にも搭載されていました。これまでは、「書類」「ミュージック」「その他」など大雑把に分類され、それぞれの種類のファイルがどれくらいの割合で内蔵ストレージを占有しているかどうかがわかるだけでした。ここで大体の情報は把握できるのですが、これだけではまったく情報が足りません。とくに、「その他」の項目は、何が「その他」かわからず途方に暮れてしまいますよね。そこで、macOS Sierra から実装された「管理」ボタンをクリックしましょう。

![](170211-589e83cc2c802.png)

ここからは、macOS Sierra 以降の OS で使用できる機能です。「管理」ボタンを押すと、まずこの画面が開きます。「iCloud に保存」は、デスクトップとドキュメントフォルダー、写真やミュージック等のファイルをすべて iCloud に保存して内蔵ストレージを節約しよう、という方法ですが、iCloud の無料プランで保存可能な容量は 5GB までなので、写真を保存するにしても乏しい容量です。写真の管理はサードパーティ（とくに、Google フォトが現時点ではオススメ。Amazon Prime に登録されている方であれば、Amazon のオンラインストレージを活用するのも良いでしょう）に任せてしまうのが良いでしょう。

![](170211-589e83d35606e.png)

「iCloud Drive」を選択すると、「iCloud の"デスクトップ"と"書類"を有効にする」ボタンが現れます。macOS Sierra インストール、初期セットアップ時にそのままオンにしている方もいらっしゃるかもしれません。これは、文字どおり「デスクトップ」と「書類」を複数の iCloud 搭載デバイスで共有することができる機能ですが、そのような用途で使用しない場合には、iCloud の容量をムダに消費してしまうだけなのでオフにしておくと良いでしょう。

![](170211-589e83da10027.png)

左側のメニューには、先ほどの「この Mac について」のストレージ情報だけではわからなかった、より細かな種別ごとに内蔵ストレージのファイルサイズをどれくらい占有しているかどうかがわかるようになっています。たとえば、「書類」を選択してみましょう。上図の例では「書類」だけで 66.92GB を占有していることがわかります。「書類」を開くと、「大きいファイル」「ダウンロード」「ファイルブラウザ」というタブが選択できます。「大きいファイル」を選択すると、「書類」の中でもどのファイルが容量を占有しているのかどうかを一目瞭然で確認できます。私の場合は、Windows や Linux 等の仮想マシンの仮想イメージが占めていることがわかります。

![](170211-589e83e0b8f1c.png)

「ダウンロード」を選択すると、「ダウンロード」フォルダーに保存されているファイルを一覧で知ることができます。とくに、「ダウンロード」フォルダーは、大きなサイズのファイルをダウンロードしたままそのまま放置していることがよくあるフォルダーですので、定期的に整理しておきましょう。

![](170211-589e83e70d555.png)

もっと情報を詳細に知りたい！という場合には「ファイルブラウザ」が便利です。Finder でもファイルの容量を確認できますが、Finder より表示される情報が簡略化され、ここではファイルサイズに特化した情報を知ることができます。とくにフォルダーごとの容量を簡単に把握できるのは便利ですね。

![](170211-589e83ed47f27.png)

私は VMware Fusion と Parallels Desktop を併用しているため、内蔵ストレージを占めているのは大多数が仮想マシンのイメージファイルです。逆に、それ以外の大きなサイズのファイルが見つかった場合には、ここで定期的にクリーンしています。そのままサイズの大きなファイルを削除することもできるため重宝しています。

![](170211-589e83f47d315.png)

また、意外と容量を占有しているのが「アプリケーション」です。話題になったアプリケーションをダウンロード、インストールしたのはいいものの、気付けば使用していないというアプリケーションがありませんか？そして、そのアプリケーションが意外と容量を占有していたりするため、定期的にチェックしてみましょう。

## まとめ

macOS Sierra 標準の機能では、巨大なファイルを簡単に検索できるようになりました。サードパーティ製のアプリのように、巨大なファイルを見つけて削除する、といったところまでは自動化できないものの、OS 標準機能でここまでできるよになったのは本当に便利です。これからも macOS Sierra の進化に期待しましょう！
