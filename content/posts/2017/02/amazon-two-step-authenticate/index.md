---
author:
- '@ottanxyz'
categories:
- iPhone
- Mac
date: 2017-02-21 00:00:00+00:00
draft: false
tags:
- amazon
- パスワード
- ワンタイムパスワード
- 2段階認証
- jp
title: Amazon.co.jpの2段階認証を今すぐ設定してセキュリティを強化しよう！
type: post
---

![](170221-58ac127f42e4b.jpg)

Amazon Primeは年額3,980円の魅力的なサービスです。Amazon Primeに加入することにより、プライム対応商品であればお急ぎ便が無料になったり、最近ではAmazon MusicやAmazon Prime Videoなどでプライム指定のものに限られますが、音楽や動画が見放題となっています。もはや、ネットショッピングに限らず多方面で活躍するAmazon.co.jpのお世話になっている方も多いのではないでしょうか。

また、1-Click設定を有効にすることにより、思い付いたらスマホからその場で1タップで購入できるので、その手軽さから利用している方は多いはずです。しかし、以下のように考えたことはありませんか。

「Amazon.co.jpのアカウントが乗っ取られたらどうなるのだろう？」

考えただけでも恐ろしいですね。Amazon MusicやAmazon Prime Videoは、まだ付属のサービスなのでそこまで影響は大きくありませんが、もっとも影響を受けるのが、Amazon.co.jpでの買い物です。前述の1-Click設定の有効化はともかく、アカウントにはクレジットカードなどさまざまな個人情報が登録されています。

パスワードが分からなければ乗っ取られることはない、これはその通りの考え方なのですが、たとえば他のサービスと同様のパスワードを使い回していた結果、そのサービスがサイバー攻撃の被害にあい、万が一パスワードが流出してしまったら…。簡単にあなたのアカウントが乗っ取られてしまうかもしれません。

それだけではありません。ついつい、覚えやすいように、メールアドレスや携帯電話の電話番号、誕生日、銀行の暗証番号などを組み合わせた簡単なパスワードにしている場合、ブルートフォースアタックなどの無差別攻撃により簡単にアカウントが乗っ取られてしまう可能性があります。メールアドレス、パスワードの無差別攻撃です。考えただけでも恐ろしいことですね。

そもそも、このようなパスワードの使い回しや覚えやすい簡単なパスワードを使用することこそに問題があるのですが、その対策を施したとしても、パスワードが流出してしまっては乗っ取りを防ぎようがありません。

そこで、今回ご紹介するのがAmazon.co.jpの2段階認証です。ついに、Amazon.co.jpでも2段階認証が使用できるようになりました。Amazon.co.jpの2段階認証は、パスワードと、パスワードと異なる認証（ワンタイムパスワード）による2段階認証です。SMSや音声通話を使用することもできますが、オススメは1PasswordやGoogle AuthenticatorなどのOTPに対応したスマホのアプリを使用することです。

2段階認証を設定しておくことにより、万が一アカウント情報が盗まれた場合においても、ワンタイムパスワード（極めて短時間だけ有効な一時的なパスワード）を知らなければログインすることができません。これで、パスワードが盗まれてしまった場合においても、新しいパスワードに変更するまでの時間を稼ぐことができます。

利便性が落ちるのでは？と思われる方もいらっしゃるかもしれませんが、本人しか利用しないデバイス（自宅のMacやiPhoneなど）を登録しておくことにより、パスワードのみでログインすることもできます。また、iPhoneのAmaonアプリの場合、Touch IDによるログインにも対応していますが、2段階認証を有効にした場合においても、そのまま継続して使用できます。設定しない手はありません、今すぐ設定しましょう。

## Amazon.co.jpの2段階認証を有効にし、ログインする方法

では、早速Amazon.co.jpの2段階認証を有効にしましょう。まずは、Amazon.co.jpにアクセスして、従来通りメールアドレス（または電話番号）とパスワードでログインします。

<https://www.amazon.co.jp/a/settings/approval>

次に、上記のURLにアクセスしてください。

![](170221-58ac1409591c7.png)

ここから2段階認証の設定が始まります。「設定を開始」をクリックします。

![](170221-58ac1410b1c1f.png)

次に、ワンタイムパスワードを受け取る方法を選択します。テキストメッセージ（SMS）、または認証アプリを使用できます。テキストメッセージは、文字通りパスワードによるログイン後に、登録した電話番号宛にSMSが送信され、そこに記載されたパスワードを入力してログインする方法です。認証アプリは後述の1PasswordやGoogle Authenticatorなどの、時間ベースのワンタイムパスワード（Time-based One Time Password）に対応しているアプリを使用する方法です。今回は弊サイトでも度々ご紹介している1Passwordを使用します。なお、1Password自体は無料で使用できますが、ワンタイムパスワードを管理する場合には、App内課金が必要です。

![](170221-58ac141725a41.png)

認証アプリを選択すると、QRコードが表示されるため、Macの1Password、またはiPhoneの1PasswordからQRコードを読み込みます。

{{< itunes 568903335 >}}

{{< itunes 388497605 >}}

今回は、iPhoneの1Passwordを例にご紹介します。Macの1Passwordでも同様の方法でQRコードをスキャンできます。ワンタイムパスワードのフィールド追加時にQRコードのマークをタップする手順は、iPhone、Mac共通です。

![](170221-58ac1433d38e6.png)

Amazon.co.jpのメールアドレスとパスワードを登録している項目を開いたら編集します。「新規フィールドを追加」と書かれたラベルをタップします。

![](170221-58ac143ab87a9.png)

「One-Time Password」を選択します。

![](170221-58ac144004cf1.png)

「One-Time Password」の隣にQRコードのマークが表示されます。タップすると、1Passwordからカメラへのアクセスを求められるため（初回のみ）許可します。iPhoneのカメラが起動するため、カメラで画面に表示されたQRコードを読み込みます。「完了」をタップすると、1Passwordにワンタイムパスワードが表示されるようになります。

![](170221-58ac14454f87f.png)

![](170221-58ac141725a41.png)

続いて、1Passwordに表示されているワンタイムパスワードを、上図のテキストボックスに入力したら「コードを確認して続行」をクリックします。

![](170221-58ac141d52d33.png)

次に、万が一iPhoneを紛失した場合などに備えて、バックアップ用の電話番号を登録します。ワンタイムパスワードを管理するiPhoneとは異なる電話番号を入力しましょう。SMSに対応している携帯電話の場合はテキストメッセージ、固定電話を使用したい場合には音声電話を選択するのが良いでしょう。「コードを送信」と押すと、SMS、もしくは電話でコードが送信されます。そのコードを入力したら「コードを確認して続行」をクリックします。

![](170221-58ac1426bffc9.png)

2段階認証を有効にした場合のログイン方法が表示されますが、画面の内容がやや古いため読み飛ばして構いません。

![](170221-58ac142d8a4bb.png)

最後に、本人しか利用しない、普段利用する端末（iPhoneやMac）の場合は「この端末ではコードの入力は不要です」をチェックしておきます。こうすることで、次回のログイン以降パスワードのみでログインできるようになります。ただし、別のMacやブラウザ等で再びAmazon.co.jpにアクセスしようとすると、再びワンタイムパスワードの入力が求められるため、万が一パスワードが流出した場合も乗っ取りの被害を防ぐことができます。そのような兆候があった場合には、すぐにパスワードを変更することをオススメします。

### Amazonのサービスにログインする

今回は、iPhone版のAmazon Musicのログイン方法についてご紹介しますが、すべてのアプリでインタフェースは共通していますのでご安心ください。

![](170221-58ac144a0b6e4.png)

アプリを起動し、まずは従来通りメールアドレス（または電話番号）とパスワードを入力して「サインイン」します。なお、すでにサインインしている場合は再びサインインする必要はありません。今回は実験のためにあえて一度サインアウトしました。

![](170221-58ac1450b59e2.png)

次に、1Passwordに表示されたワンタイムパスワードを入力します。「このデバイスで再度コードを要求しないでください」をチェックしておくと、次回以降、このiPhoneでAmazon Musicにログインしようとした場合に、ワンタイムパスワードの入力の手間を省くことができます。なお、他のデバイス（iPadや、他人のiPhone）でログインしようとした場合は、再度ワンタイムパスワードの入力が必要です。

## まとめ

ますます便利になるAmazon.co.jpですが、その分、アカウントが乗っ取られてしまった場合の被害は甚大です。2段階認証を設定しないメリットも、設定するデメリットもないため、ぜひ登録しておくことをオススメします。
