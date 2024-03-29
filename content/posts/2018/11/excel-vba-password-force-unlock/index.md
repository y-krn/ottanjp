---
author:
- '@ottanxyz'
categories:
- Windows
date: 2018-11-13 00:00:00+00:00
draft: false
tags:
- excel
- マクロ
- バイナリエディター
- ブック
- フォルダー
title: 解除パスワードのわからないExcelマクロ（Excel VBA）のパスワードを強制的に解除する方法
type: post
---

![](181113-5beaece811ac7.png)
￼

悪用厳禁ですよ。

企業の社内システムで Excel マクロがいまだに幅を利かせている事は事実であり、その Excel マクロをメンテナンスしている「Excel おじさん」がいるのも紛れもない事実です。

ところが、年月の経過と共に Excel マクロの中身はしだいにブラックボックス化します。また、Excel おじさんの定年退職や部署異動に伴い、属人化していた Excel マクロをメンテナンスできる人材が減少、もしくは不在になる事も、長年企業に勤めているとありがちな事です。

ある日、上司に「君、業務で使っているこの Excel マクロ、ちょっと改修して欲しいんだが」と頼まれました。

Excel マクロは、なぜか新入社員時代に OJT（On the Job Training）の一環という名目のもと散々勉強した経験のある「君」ですから、多少スパゲティ化していたとしても、「たかだか Excel マクロ」と思い込んでいます。

上司からの依頼に二つ返事で引き受けます。「時間はかかるかもしれませんが、解読しながら隙間時間を見つけてやってみます」

しかし、そこで待ち受けていたのは思わぬ事態でした。Excel マクロ自体がスパゲティ化している、という事実の前に、Excel マクロ（Excel プロジェクト）に Excel おじさんが仕掛けたと思われる解除用パスワードが設定されていたのです。

![](181113-5beaece83d001.png)
￼

## Excel マクロの解除用パスワードを強制的に解除する方法

前置きが長くなりましたが、ここからが本題です。冒頭のような、考えられないような事態ですが、往々にして起こってしまう事が否めません。緊急手段として、今回の方法をご紹介しますが、お願いがあります。

- 緊急手段以外で本手順を使用してパスワードの解除を行わないようにしてください。悪用厳禁です
- バイナリエディターを用いて、Excel マクロのバイナリを強制的に書き換える、非公式な方法です。Microsoft が推奨しているわけではありません
- バイナリを強制的に書き換えるため、Excel ブックが破損する可能性があります。あらかじめバックアップを取得してください

### バイナリエディターをダウンロードしよう

今回の検証用の環境は以下の通りです。

- Windows 7 Professional（64bit）
- Excel 2010（32bit）or Office 365（1810）（32bit）
- stirling

Excel 2013、2016 での実績はありませんが、2010、および Office 365（リビジョン 1810）で同様の方法が利用できたため、恐らく問題はないと思います。ただし、64bit 版では検証できていないため、手順が異なる可能性があります。

バイナリエディターには、「stirling」を使用しましたが、Excel ブックをバイナリエディターで編集できるものであれば何でも構いません。

[stirling](https://www.vector.co.jp/soft/dl/win95/util/se079072.html)

### Excel マクロのパスワードを解除する（xlsm 編）

では、具体的に Excel マクロのパスワードを解除する方法を以下に示します。実は、Excel 2007 以前と、Excel 2010 以降、具体的には Excel マクロの拡張子が「xls」か「xlsm」かで解除の方法が異なります。「xls」の方が単純ですので、「xlsm」で今回はお見せします。

1. 「xlsm」ファイルの拡張子を「zip」に変更し任意のフォルダーに解凍する
2. 解凍したフォルダー内の「xl」フォルダーにある「vbaProject.bin」ファイルをバイナリエディターで開く
3. バイナリエディター上で「DBP=」という文字列を検索する
4. バイナリエディター上で検索した文字列の先頭を任意の 1 バイト文字（英字）に置換し保存する
5. 解凍したフォルダー内のファイルとフォルダーをすべて選択した状態で、再度 zip 形式で圧縮する
6. 圧縮されたファイルの拡張子を「zip」から「xlsm」に変更する
7. Excel ブックを Excel で開きマクロの編集画面を開く
8. VBAProject のプロパティを表示して、ロックを解除して、Excel ファイルを保存する

流れとしては上記の手順になります。煩雑そうに見えますが、内容は至って単純です。一部、図を交えながら解説します。

まず、拡張子「xlsx」や「xlsm」ファイルに関してですが、Excel 2010 以降で形式が従来の「xls」から変更されました。これは、拡張子のみならず、Excel ファイル自体の保存形式が変更されており、標準で ZIP 形式で圧縮された状態で保存されるようになりました。そのため、拡張子を「zip」に変更することで Excel ファイルを解凍できます。解凍した中身には、Excel のコンテンツの情報や、Excel 上に貼り付けた画像ファイル等のアセットファイルがフォルダーに保存されていることがわかります。

![](181113-5beaece81c96c.png)
￼

次に、バイナリエディターによる編集についてです。stirling で該当ファイルを開き、文字列を検索してください。パスワードで保護された Excel プロジェクトの場合、「DBP=」という文字列が見つかります。

![](181113-5beaecea39b4d.png)
￼

この「DBP=」の先頭の文字を任意の 1 バイト文字に置き換えます（図中では「a」）。これでバイナリエディターを使用した手順は終了です。

![](181113-5beaece81c45e.png)
￼

次に、解凍した Excel ファイルを元の状態に戻します。その際に、解凍したフォルダーの親フォルダーから圧縮するのではなく、フォルダーの中身をすべて選択した状態で、zip 形式に圧縮してください。たとえば、「Book1」というフォルダーに展開された場合、「Book1」フォルダー自体を圧縮するのではなく、その中のファイルやフォルダー全体を選択して圧縮します。なお、stirling のデフォルトの設定では、ファイル保存時に、同一フォルダー上にバックアップファイルが保存されますが、圧縮の際には別フォルダーに移動しておいてください。

続いて、Excel から編集した Excel ブックを開くと下図のようなエラーダイアログが表示されますが、そのまま「OK」をクリックします。

![](181113-5beaecea1345b.png)
￼

![](181113-5beaecef26daa.png)
￼

そして、Excel マクロの編集画面を開くと、パスワードが解除されて内容がわかるようになっています。そのままの状態では、次回以降同様のエラーダイアログが表示されてしまいますので、「VBAProject」のプロパティを表示して、保護を解除しておきます（具体的にはチェックボックスを外します）。

![](181113-5beaecf067f0d.png)
￼

![](181113-5beaecf12ac5b.png)
￼

以上で、次回以降ファイルを開いた際にはパスワードが解除された状態で表示されるようになります。

### Excel マクロのパスワードを解除する（xls 編）

拡張子が「xls」形式、すなわち Excel 2007 以前の形式の場合、手順はより単純になります。

1. バイナリエディターで Excel ブックを開く
2. バイナリエディター上で「DBP=」という文字列を検索する
3. バイナリエディター上で検索した文字列の先頭を任意の 1 バイト文字（英字）に置換し保存する
4. バイナリエディターで編集した Excel ブックを Excel で開きマクロの編集画面を開く
5. VBAProject のプロパティを表示して、ロックを解除して、Excel ファイルを保存する

Excel 2007 以前の形式の Excel ファイルは単独のバイナリファイルです。そのため、zip ファイルの解凍等の作業が必要なくなり、直接バイナリエディターで編集するだけです。

## まとめ

Excel ファイルのパスワードは、暗号化された状態でファイルに埋め込まれた状態で保存されているため、それを応用して解除できます。ただし、冒頭述べたように、直接バイナリエディターで内容を編集するため、Excel ブックが破損する可能性があることと、自作のマクロや自社内のマクロでどうしてもパスワードを解除する必要がある場合のみ使用してください。

Excel マクロの現場からは以上です。
