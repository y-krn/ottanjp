---
author:
- '@ottanxyz'
categories:
- Mac
date: 2015-08-23 00:00:00+00:00
draft: false
tags:
- youtube
- dl
- 動画
- ho
- c3
title: YouTubeから簡単に動画をダウンロードできる「youtube-dl」
type: post
---

![](150823-55d96dac3037b.jpg)

コマンドラインから簡単に YouTube の動画をダウンロードできる「youtube-dl」をご紹介します。ニコニコ動画や dailymotion にも対応しているため、非常に便利なツールです。YouTube からダウンロードする方法をお探しの方はぜひ使ってみてください。

## YouTube から簡単に動画をダウンロードできる「youtube-dl」

### 「youtube-dl」のインストール

「youtube-dl」のダウンロードは、Homebrew が便利です。Homebrew については、[Mac でプレゼン資料に数式を貼り付けるのに便利な「LaTeXiT」](posts/2014/09/mac-latex-presentation-92/)でも詳しくご紹介していますのでご参照ください。

「youtube-dl」をインストールするためには、以下のコマンドを実行します。

    brew install youtube-dl

### 「youtube-dl」の使い方

「youtube-dl」の使い方はとても簡単です。「youtube-dl」の後にダウンロードしたい YouTube の動画の URL を指定するだけです。

<https://www.youtube.com/watch?v=2MNL2mU8pBE>

    $ youtube-dl https://www.youtube.com/watch?v=2MNL2mU8pBE
    youtube-dl https://www.youtube.com/watch\?v\=2MNL2mU8pBE
    [youtube] ShhoC3nHX8E: Downloading webpage
    [youtube] ShhoC3nHX8E: Downloading video info webpage
    [youtube] ShhoC3nHX8E: Extracting video information
    [youtube] ShhoC3nHX8E: Downloading DASH manifest
    [youtube] ShhoC3nHX8E: Downloading DASH manifest
    [download] Destination: ....
    [download] 100% of 56.27MiB in 00:02

たった 1 行で YouTube の動画をダウンロードすることができるので非常に便利です。また、単独の動画だけではなく、あらかじめ作成したプレイリストからもダウンロードできます。使い方は、単独の動画をダウンロードする場合と同様です。

    youtube-dl https://www.youtube.com/playlist?list=PLgegCeSlC24bFHsvEUYBAYj4wkOd8-BbK

当たり前ですが、違法にアップロードされていると知りながら、その動画をダウンロードする行為は禁止されています。著作権にはお気をつけくださいね。
