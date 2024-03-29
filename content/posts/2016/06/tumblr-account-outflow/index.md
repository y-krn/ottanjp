---
author:
- '@ottanxyz'
categories:
- Web
date: 2016-06-18 00:00:00+00:00
draft: false
tags:
- 被害
- パスワード
- jtb
- 個人情報流出
- adobe
title: いつの間にかTumblrからアカウント情報が流出していたことが判明
type: post
---

![](160618-5764cb28ce652.jpg)

JTB の個人情報流出が明るみになったのは記憶に新しい事ですが、とくにここ最近、悪質なマルウェアによる企業の被害が広まっています。JTB で猛威を奮ったマルウェアは、従来のパターンファイルと呼ばれるウイルス定義ファイルでは防ぐことができず、手口も年々巧妙になっており、社会問題化しています。

<https://news.mynavi.jp/article/20160617-plugx/>

私自身は、JTB を利用した覚えがありませんでした。そのため、対岸の火事のように事の成り行きを、ただただ傍観しているだけだったのですが、この事件を機に、ふとしたことを思い出しました。

## Adobe と Tumblr からアカウント情報が流出

<https://haveibeenpwned.com/>

メールアドレスを入力することで、そのメールアドレスが過去に流出した可能性があるかどうかを調べることができます。流出した結果、それが直接被害に及んでしまったかどうかは、また別の話になりますが、参考程度に見ておくと良いのではないでしょうか。

以前、Adobe の個人情報流出が発覚した際、上記サイトで登録しているメールアドレスを入力してみたところ、見事に Adobe から流出していることがわかり、慌ててパスワードを変更した覚えがあります。パスワードの使い回しは非常に危険です。複雑なパスワードを使用することよりも、同じパスワードの使い回しを避けることの方が重要です。

* [iOS版の1Passwordでウェブページの登録からワンタイムパスワードの使い方まで徹底解説！](/posts/2015/04/ios-1password-description-part2-875/)

パスワード管理に最適な、iOS／Android で利用可能なアプリケーション「1Password」について、過去に度々紹介しています。覚えきれない複雑なパスワードを、簡単に管理することができるため、初期投資費用はかかりますが、非常にオススメです。

さて、話を本題に戻しますが、私は WordPress を利用する前に、Tumblr でもアカウントを作成していたことがあります。簡単におしゃれなデザインのブログを構築できることから、登録はしてみたものの、結局 WordPress のように思うようなカスタマイズができず、使用しないまま放置していたのです。

ふと思い立ち、上記の Web サイトから過去に登録したメールアドレスを入力してみたところ、

![](160618-5764cdc25cbbc.png)

いつの間にやら、Tumblr からも個人情報が流出したかもしれないこと。Tumblr と他のサービスにおいて、1Password を使用してパスワードの使い回しは避けていたため、直接的な被害にはまだあっていませんが、これもまた念のためパスワードを変更するか、そもそも必要でないならアカウントを退会してしまっても良いかもしれません。

<http://www.accountkiller.com/en/>

ご丁寧にアカウントの退会方法を説明してくれる便利なサービスまで世の中には存在します。Tumblr も、このサイトで紹介されている方法で退会することが可能です。

私自身、以前クレジットカードの不正利用の被害にあったことがあります。不必要なクレジットカードは保持しない、肌身離さず持っておくことが重要だと身にしみた瞬間でした。（無事に、被害にあった金額は取り戻すことができましたが）

個人情報流出は、企業の信頼喪失も去ることながら、我々サービス利用者にとっては非常に大きな問題です。これを機に、今使用しているサービスの断捨離をしてみてはいかがでしょうか？あなたはパスワードを使い回していませんか？
