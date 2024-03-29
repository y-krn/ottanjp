---
author:
- '@ottanxyz'
categories:
- iPhone
date: 2016-11-08 00:00:00+00:00
draft: false
tags:
- rssリーダー
- 全文
- 記事
- インポート
- 既読
title: RSSリーダーはFeedlyからのインポートが可能な「Inoreader」がオススメ！
type: post
---

![](161108-5821c6ace8beb.jpg)

iPhone の RSS リーダーは、「Reeder」が常々素晴らしいと思っていました。有償アプリであるため初期投資はかかります。また、Mac 版も同様に有償アプリとして販売されていますが、iPhone と同様のインタフェースを提供してくれます。「Reeder」の素晴らしさは、何と言っても、**その見た目の美しさと使い勝手**、これに尽きます。今でも「Reeder」に対して、右に出るものはないというほど、その美しさと使い勝手は素晴らしいと思います。しかし、先日の[Readability](https://www.readability.com/)のサービス終了に伴い、使い勝手が大きく変化してしまいました。

{{< itunes 697846300 >}}

「Reeder」では、Feedly などの RSS リーダーと、「Readability」の「あとで読む」記事を同時に閲覧することができました。次々と配信される記事のタイトルと内容を斜め読みし、気になる記事は「Readability」に保存して、時間ができた時にまとめて読む、これが王道でした。が、「Readability」終了の今、これはもはや実現できません。ただ、「あとで読む」サービスについては、[「Instapaper」](/posts/2016/11/pocket-to-instapaper-5181/)という素晴らしいサービスの無料化により解消されました。

しかし、それでも超えられない壁があります。それは、サービス終了との因果関係はないはずですが、**「Readability」の API が不安定過ぎる**という点です。この API の優れている点は、**全文配信されていない RSS を、内蔵ブラウザを開かなくても全文「最適化」された形で読むことができる**というもの。Safari の「リーダー表示」をイメージしていただければわかりやすいかと思います。「Reeder」も多分にもれず、この「Readability」の API を使用しています。そのため、「Readability」が使用できない場合、API も機能しません。全文読むためには、内蔵ブラウザや Safari でその記事を開いて読むしかありません。

というわけで、「Reeder」が「Readability」に依存しない「リーダー表示」に対応してもらえればすべて解決するのですが、ここ最近「Reeder」がアップデートされる気配はありません。そもそも「Reeder」自体が安定していますしね。ただ、前述のように、全文配信されていない RSS を、わざわざブラウザを開いて読むのは気がひけるのです。というわけで、代替となる RSS リーダーを模索していたところ、辿り着いたのが「Inoreader」と呼ばれる RSS リーダーです。Feedly のように、Safari などの Web ブラウザから読むこともできますが、アプリを導入するともっと便利です。今回は、その「Inoreader」についてのご紹介です。

## Inoreader の使い方

まず、Inoreader を使用するためには、事前に無料登録が必要です。実は、Inoreader には無料プラン以外に、有料プランも用意されていますが、しばらく使用してみた限りでは、私の用途においては無料プランでも恩恵を受けることができますし、むしろ必要最低限な機能は備わっています。有料プランの詳細については、[Inoreader - Upgrade](http://www.inoreader.com/upgrade/feature/upgrade_badge)をご覧ください。

<http://www.inoreader.com>

兎にも角にも、上記リンクから無料登録しましょう。登録自体は無料です。Google アカウントでもログイン可能ですが、私の場合、Google アカウントが乗っ取られた場合の脅威を考えると、利便性を無視してでもサービスごとに異なるアカウントを作成しています。もちろん、パスワードはサービスごとに無作為に抽出したランダムな文字列を使用しています。

### Feedly からのインポート

Inoreader には、RSS フィードを登録してカスタマイズできますが、RSS リーダーとして「Feedly」をすでに利用している方も多いことでしょう。そのような場合には、「Feedly」からフィード情報をインポートできます。

![](161108-5821c6b3ca7df.png)

初回のみ、すべて Mac や PC の Safari 等のブラウザから作業します。初期設定完了後は、すべて iPhone のアプリだけで完結できますのでご安心を。Inoreader にログイン後に、「IMPORT YOUR SUBSCRIPTIONS」をクリックします。

![](161108-5821c6ccb9f86.png)

「Import/Export」の項目の「Feedly import」に注目します。「access token from here」と書かれたリンクをクリックします。

![](161108-5821c6ba5af0c.png)

「Feedly」のアクセストークンと呼ばれる、「Feedly」からの RSS フィード情報インポートに必要なキーを入手するための画面に遷移します。「Feedly」にログインします。

すると、「Feedly」に登録しているメールアドレス宛にアクセストークンを表示可能なリンクが書かれたメールが配信されますので、クリックします。

![](161108-5821c6c664803.png)

「Your access token:」のラベルに表示されているテキストボックス内のアクセストークンをコピーします。テキストボックスには、アクセストークンがすべて表示されていませんので、コピーには注意が必要です。1 回、テキストボックスをクリックして、⌘（command）+A 等で全選択してコピーして使用してください。アクセストークンはとても長い文字列です。

![](161108-5821c6ccb9f86.png)

先ほどの画面に戻り、アクセストークンを入力し、「Import」をクリックします。初回インポートにはやや時間を要します。お茶を飲みながら待ちます。

![](161108-5821c6d3206c8.png)

このように、RSS の情報が表示されれば作業完了です。

### iPhone アプリ「Inoreader」の使い方

まずは、「Inoreader」をダウンロードします。記事執筆時点では無料アプリです。

{{< itunes 892355414 >}}

ダウンロードが完了したらアプリを起動します。

![](161108-5821c6d8cd4ad.png)

起動したら、「ここからサインインできます」をタップします。

![](161108-5821c6ddb1b81.png)

「Inoreader」に登録したアカウントでサインインします。

![](161108-5821c6e55c0cb.png)

「すべての記事」をタップします。

![](161108-5821c6ec08d19.png)

右上の「目」のようなアイコンをタップします。

![](161108-5821ce0a86961.png)

「フィルター」で「未読のみ」としておきます。これで、毎回すべての記事を表示しなくてすみます。なお、**Inoreader と Feedly の未読、既読情報は同期されません**。そのため、Inoreader では既読扱いでも、Feedly 状態では未読状態です。他の RSS リーダーから「Feedly」を閲覧すると、大量に未読の記事が表示されます。同様に、「Inoreader」で追加した RSS フィードは、「Feedly」には反映されません。あくまでインポートです。

![](161108-5821c702e97fe.png)

続いて、記事の本文を表示します。このように RSS 配信サイトのほとんどが全文配信ではありません。では、記事を上から下にスワイプしてみましょう。

![](161108-5821c7084e7ca.png)

**全文表示されました！**なお、「Readability」を使用していても同様ですが、「次のページ」など記事本文がページ分割されている場合は、残念ながら全文表示することはできません。このような場合には、内蔵ブラウザ（Safari View）で表示します。私はこのようにページ分割されたサイトが嫌いです。

記事は、左右のスワイプで次の記事、前の記事を切り替えることができます。その他、使い方で特筆するところはありません。

### 「Inoreader」のオススメの設定

最後に、「Inoreader」の初期設定は、私にとって使いづらかったため、カスタマイズ方法をご紹介します。左上のハンバーガーアイコンをタップするとメニューが表示されます。

![](161108-5821c70e16d74.png)

「更新があったものの…」（更新があったもののみを表示…？）を「オン」、「フィードアイコンを…」（フィードアイコンを表示…？）を「オン」、他はオフにしておきます。記事リスト表示時にファビコンが表示されます。続いて、歯車アイコンをタップします。

![](161108-5821c71475d52.png)

「デフォルトレイアウト」は「リストビュー」、「リストビューで完全なタイトルを表示」をオンにしておきます。他は好みに応じて。Inoreader のデフォルトは、最近流行り（？）のカードビューなのですが、「Reeder」に慣れた私にとっては余計な情報が表示されない「リストビュー」が一番しっくりきました。

![](161108-5821c71a2d185.png)

また、「すべて既読にするの確認」をオン、「画像を画面の幅に拡大する」をオン、「iOS のデフォルト共有」をオンにしておきます。記事リスト表示時に、画面上の「チェックマーク」をタップすると、すべて既読にできますが、誤って既読にしてしまうことを防ぐために「確認」をオンにしておきます。また、「iOS のデフォルト共有」とは、iOS 標準の共有機能（AirDrop や Twitter やメールで送信や、その他サードパーティの拡張機能）を使用できます。これがないと話になりません。「Instapaper」に保存できません。

「ソーシャル機能」は、Inoreader にソーシャル機能を持たせる機能ですが私は使用しない、興味がないためオフ、「Google Analytics」は何やら個人情報を収集してより便利にという今時の機能ですが、とくに興味がないのでオフにしました。

{{< itunes 892355414 >}}

## まとめ

以上、簡単ですが RSS リーダー「Inoreader」をご紹介しました。「Readability」および「Reeder」からの乗り換えの際のご参考になればと思います。「Feedly」からインポートできるものの、同期できないのがやや不便ですが、今のところは快適に使用しています。ただし、見た目の美しさ、シンプルさだけは、どうしても「Reeder」に見劣りしてしまうのですが…。
