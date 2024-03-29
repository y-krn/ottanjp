---
author:
- '@ottanxyz'
categories:
- iPhone
- Mac
date: 2017-05-20 00:00:00+00:00
draft: false
tags:
- twitter
- プライバシーポリシー
- ユーザー
- プライバシー
- トラッキング
title: Twitterのプライバシーポリシーの変更に伴い無効化しておきたいプライバシー設定
type: post
---

![](170520-591fb2ebe431f.png)

Twitterのプライバシーポリシーが2017年6月18日に改訂されます。詳細については、Twitterの[Privacy Policy | Twitter](https://twitter.com/privacy?lang=ja)をご覧いただくとして、今回はプライバシーポリシー改訂に備えて実施しておきたい、Twitterのプライバシー設定をご紹介します。基本的に個人の同意なしに第三者への情報共有は行わない旨が記されていますが、デフォルトで有効になっている可能性もあるため無効化しておきましょう。また、Safari等のブラウザに実装されている、ブラウザによるトラッキング拒否も使用できなくなりますので、Twitter側で設定する必要があります。

## Twitterによるプライバシーポリシーの改訂

2017年6月18日にプライバシーポリシーが改訂され、いくつかの点が変更されますが、その中でも影響のありそうな項目をピックアップしてみました。

<blockquote>組み込まれたタイムラインまたはTwitterボタンなどのTwitterコンテンツを組み込んだ第三者のウェブサイトへのユーザーのアクセス履歴に基づき、Twitterはそのユーザー向けに本サービスを最適化できます。（中略）**30日以内**にこれらの情報を削除、難読化、あるいは集計情報化します。Twitterは、本サービスを向上させ、フォローをオススメするユーザー、広告、およびユーザーが興味を示しそうなその他のコンテンツなどの、ユーザー向けコンテンツをパーソナライズするために、このデータから抽出する興味・関心その他の情報を使用することがあります。</blockquote>

Twitterはユーザの嗜好に応じて広告配信を行っており、Twitterを介してクリックした広告の情報や、Webデータの情報を保管、集計化しています。従来、保存期間は10日間と定められていましたが、30日間に拡張されます。

<blockquote>Twitterは、人々がツイートをした回数、特定のリンクをクリックしたまたはツイートで調査に回答したユーザー数（1人だけの場合も含む）、端末またはその利用者の特性（端末が広告を受信できる場合）、特定の場所で人々がツイートしている話題、または広告を閲覧したりクリックしたユーザーに関する広告主への集計ベースや端末レベルのレポートなどの、非個人情報、集計情報、または端末レベルの情報を共有または公開することがあります。（中略）**Twitterは、パートナーシップを通じて、非個人情報、集計情報、または端末レベルの情報を他の会社と共有することがあり、これらの会社は、その保有するデータ（ユーザーが当該会社に提供したデータを含む）を用いて、Twitterが提供する情報にユーザー名、メールアドレス、またはその他の個人情報を関連付けることがあります**。</blockquote>

Twitterは、広告の最適化のために、広告主に対してユーザーの情報を匿名で提供していましたが、今回のプライバシーポリシーの改定により、第三者（広告主）に提供される情報が増える可能性があります。

<blockquote>TwitterはDo Not Track（トラッキング拒否）のブラウザ設定のサポートを終了しました。業界におけるDo Not Trackの活用促進を目指してTwitterはDo Not Trackをサポートしていましたが、Do Not Trackに対する業界の足並みはそろいませんでした。Twitterでは詳細なプライバシー設定を利用できます。</blockquote>

SafariやChrome等のブラウザに実装されている「トラッキング拒否」と呼ばれる項目があります。「トラッキング」とは、ユーザーの嗜好（Webサイトの訪問履歴等に基づきカスタマイズされる）に応じて表示される広告をカスタマイズするために利用されるものです。

![](170520-591fb4c85850b.png)

たとえば、MacのSafariの場合、環境設定を開き「プライバシー」タブから「Webサイトにトラッキングの停止を求める」をチェックしておくことにより、Twitterにおいてもブラウザのトラッキング拒否を使用してきましたが、これからはTwitter独自の実装になるようです。そのため、ユーザーの嗜好による広告のカスタマイズを希望しない場合は、Twitter側で設定を行う必要があります。

### Twitterでプライバシー設定を行う

では、プライバシーポリシーの改訂に向けて、ユーザー側で対処できる方法をご紹介します。さすがに、ユーザーの個人情報がすべてTwitterによって洗いざらい第三者に無条件に渡されたり、無許可で広告を表示するといったことはないと思いますが、あまり気持ちの良いものではありませんので、プライバシー設定を変更しておきましょう。

![](170520-591fb6913a7ab.png)

[Twitter / 設定](https://twitter.com/settings/account)にアクセスして、「プライバシーとセキュリティ」をクリックします。

![](170520-591fb697522e8.png)

「プライバシーとセキュリティ」から「カスタマイズとデータ」という項目を見つけてください。私の場合は、すでに無効化しているため「Off」と表示されていますが、標準では「On」になっているかもしれません。いずれにせよ「編集」をクリックします。

![](170520-591fb6a17907a.png)

すべてのチェックボックスを無効化します。以上で、プライバシー設定は完了です。なお、本ページには、<https://twitter.com/settings/personalization>から直接アクセスすることも可能です。

Twitterアプリからも同様の変更ができるようですが、すべてのユーザーに公開されているわけではなさそうです。今後、段階的に提供されていくのでしょうか。MacやPCのブラウザから実施するのが確実ですね。
