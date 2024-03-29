---
author:
- '@ottanxyz'
categories:
- iPhone
- Mac
date: 2015-02-01 00:00:00+00:00
draft: false
tags:
- dnsサーバ
- 5g
- fi
- wi
- ttl
title: iPhoneやMacのWi-Fi接続速度が遅い場合に見直したい項目
type: post
---

![](150201-54ce2c7ec4e10.jpg)

[@おったん](https://twitter.com/ottanxyz)です。iPhoneをWi-Fiネットワークに接続した場合の転送速度が遅い場合、ネットワーク構成を見直すことで、改善される可能性があります。

私の環境、iPhone 6 Plus + Time Capsuleでは、iPhoneの性能を発揮するには、必要十分な速度が出ています。私の環境を中心に改善ポイントを紹介します。

![](150201-54ce027799440.png)

## iPhoneやMacのWi-Fi接続速度が遅い場合に見直したい項目

### iOSを最新バージョンにアップデートする

iOSの最新バージョンでは、バグ修正を含むさまざまな点が改善されています。Wi-Fi接続にソフトウェア的な不具合がある場合は、解消されている可能性があります。iOSのバージョンが最新ではない場合は、今すぐにアップデートしましょう。

iOSのアップデートは、「設定」→「一般」→「ソフトウェアアップデート」から行います（OTA：Over The Air）。古いバージョンのiOSを使用している場合は、USBポート経由でPCに接続した上で、iTunesから行いましょう。

![](150201-54ce027dc76db.png)

### 無線LANの周波数帯に5GHzを使用する

iPhoneについてはiPhone 5以降、iPadについてはiPad 2以降であれば、無線LANの周波数帯が、2.4GHzと5GHzのデュアルバンドに対応しています。

一般的に2.4GHzの周波数帯は電子レンジなどの家電製品等で使用されている電磁波と同じ周波数のため干渉を引き起こしやすく、その影響により転送速度が遅い、または頻繁に切断されるといった症状を引き起こす場合があります。

そのため、お使いのルーターが5GHzの周波数帯に対応しているなら、5GHz帯のWi-Fiネットワークを用意しておきましょう。5GHz帯であれば、他の家電製品の影響を受けづらく、またチャンネルが混みあうことも少ないです。

![](150201-54ce027fe7e7b.png)

ただし、5GHz帯を使用する場合、5GHzは2.4GHzと比較し、壁など物理的な障害物に対して影響を受けやすく、また電波の届く範囲も2.4GHzと比較すると狭くなっている点に留意しておかなければなりません。5GHz帯に変更して電波の強度が弱まってしまう場合には、2.4GHz帯で運用した方が無難です。

最新のTime Capsuleであれば、2.4GHz帯と5GHz帯のデュアルバンドに対応しているため、状況によって2.4GHz、5GHzを使い分けることが可能です。5GHz帯で接続速度や安定性の恩恵を受けることができない場合は、5GHz帯は無効化しましょう。

#### 5GHz帯のWi-Fiネットワークを作成する方法（Time Caplsule）

Time Capsuleで5GHz帯のWi-Fiネットワークを作成するためには、AirMacユーティリティを使用します。AirMacユーティリティを開いたら、Time Capsuleを選択し、「編集」ボタンをクリックします。はじめてアクセスする場合には機器にアクセスするためのパスワードを求められるため、あらかじめ設定しているパスワードを入力しましょう。

![](150201-54ce2c6447cb0.png)

続いて、「ワイヤレス」タブを選択し、「ワイヤレスオプション」ボタンをクリックします。

![](150201-54ce028444193.png)

ワイヤレスオプションが開いたら、「5GHzネットワーク名」をチェックし、任意のアクセスポイントの名称（SSID）を入力します。チャンネルについては「自動」にしておくことにより、現在もっとも効率的なチャンネルをTime Capsuleが自動的に選択してくれます。これで、5GHz帯のWi-Fiネットワークの作成は完了です。

![](150201-54ce027fe7e7b.png)

### 2.4GHz帯の周波数を使用している場合は、無線チャンネルを最適化する

2.4GHz帯の周波数は、前述のとおり混雑しています。iPhoneやiPadなどのWi-Fi対応機器の急増に伴い、2.4GHz帯の周波数が頻繁に使用されるようになっているからです。

とはいえ、5GHz帯の周波数に対応している機器ばかりではないのが現状です。その場合は、2.4GHz帯の周波数で使用している無線チャンネルが、他の電波と互いに干渉していないかどうかを確認しましょう。

macOSにはWi-Fiネットワークのパフォーマンスやチャンネルの干渉を確認できるユーティリティが標準で具備されています。⌥を押しながらメニューバーのWi-Fiのアイコンをクリックします。アイコンをクリックすると、「"ワイヤレス診断"を開く」というメニューがあるので、これをクリックします。

![](150201-54ce2c66bef14.png)

「ワイヤレス診断」が開きます。ここでは、このウインドウはそのままにして、メニューの「ウインドウ」→「スキャン」をクリックします。

![](150201-54ce2c6b97e44.png)

すると、ネットワーク名、プロトコル、RSSI、ノイズ、チャンネル、バンドといった、デバイスの検索範囲内のワイヤレスネットワークの一覧が表示されます。太字のネットワーク名が現在接続されているWi-Fiネットワークです。もし、バンドが「2.4GHz」で、かつチャンネルが同一のWi-Fiネットワークが存在する場合は、チャンネルを変更することを検討しましょう。

![](150201-54ce2c68c412b.png)

同一チャンネルが使用されているWi-Fiネットワークが存在すると、干渉が発生するためパフォーマンスは低下します。Wi-Fiの接続速度が安定しない、遅いと感じた場合には、無線チャンネルを見直し、混雑していないチャンネルに切り替えてみましょう。

AirMacユーティリティを使用する場合は、前述のワイヤレスオプションからチャンネルを変更できます。

![](150201-54ce027fe7e7b.png)

### 無線LANの暗号化方式にWPA、またはWPA2を使用する

無線LANの暗号化方式には、「暗号化無し」「WEP（Wired Equivalent Privacy）」「WPA/WPA2（Wi-Fi Protected Access）」とさまざまな規格が存在します。

「暗号化」はWi-Fiの接続速度と直接的な関係性はありませんが、もはや「WEP」は過去の遺産となってきています。最新の暗号化規格である「WPA/WPA2」を使用することにより、より最適化された環境下で、安全に高速にWi-Fiを活用できます。

とくに、「暗号化無し」は情報漏洩と同等です。少しの知識があれば簡単に盗聴できます。公衆無線LANでは暗号化が行われていない場合も多いです。たとえば、仕事でやむなく公衆無線LANを使用する場合には、顧客情報など重要情報をWi-Fi経由でやり取りするのはやめておいた方が良いでしょう。

「WEP」も、もはや安全とは言えません。技術の進歩によりものの数十秒で暗号化キーを解読される心配があるからです。暗号化キーを解読されてしまえば、暗号化していないのと同然です。そのため、暗号化方式にはより高度なWPA、もしくはWPA2を使用しましょう。

### DNSサーバにGoogle Public DNSを設定する

Google Public DNSは、文字通り米Google社が提供するオープンリゾルバーです。膨大にキャッシュされたアドレス情報を武器に、高速な名前解決による高いパフォーマンスが期待できます。

Google Public DNSサーバを使用する場合は、DNSサーバに以下の値を設定します。プライマリDNSサーバには、より応答速度の早いサーバを選択するのが良いでしょう。

    8.8.8.8
    8.8.4.4

応答速度を確かめるための指標値としてpingコマンドによる計測方法があります。pingコマンドを実行し、「time」の値が小さければ小さいほど応答速度が早いといえます。「time」は、パケットを送信してから受信するまでの時間をミリ秒で表したものです。

実際に私のMacから上記の2つのIPアドレスに対してpingコマンドを実行した結果は以下の通りとなりました。

    PING 8.8.8.8 (8.8.8.8): 56 data bytes
    64 bytes from 8.8.8.8: icmp_seq=0 ttl=54 time=8.661 ms
    64 bytes from 8.8.8.8: icmp_seq=1 ttl=54 time=7.312 ms
    64 bytes from 8.8.8.8: icmp_seq=2 ttl=54 time=7.371 ms
    64 bytes from 8.8.8.8: icmp_seq=3 ttl=54 time=6.452 ms
    64 bytes from 8.8.8.8: icmp_seq=4 ttl=54 time=8.165 ms





    PING 8.8.4.4 (8.8.4.4): 56 data bytes
    64 bytes from 8.8.4.4: icmp_seq=0 ttl=52 time=7.771 ms
    64 bytes from 8.8.4.4: icmp_seq=1 ttl=52 time=8.031 ms
    64 bytes from 8.8.4.4: icmp_seq=2 ttl=52 time=7.685 ms
    64 bytes from 8.8.4.4: icmp_seq=3 ttl=52 time=6.560 ms
    64 bytes from 8.8.4.4: icmp_seq=4 ttl=52 time=5.962 ms

誤差の範囲内ではありますが、「8.8.4.4」のほうが平均的な応答速度は良いことがわかります。この場合には、プライマリDNSサーバには「8.8.4.4」を設定しましょう。

DNSサーバの応答速度の積み重ねが、全体のパフォーマンスの低下に繋がる可能性もあるため、ぜひ試してみましょう。

#### iPhoneでGoogle Public DNSサーバを設定する

iPhoneでDNSサーバの設定を変更するためには、「設定」→「Wi-Fi」と進み、設定するネットワークの右端の青いアイコンをタップします。

![](150201-54ce2c6dc31cb.png)

「DNS」をタップし、手動でDNSサーバのIPアドレスを設定します。

DNSは必ず1つ以上設定する必要がありますが、セカンダリDNSサーバとして2つ目のDNSサーバのIPアドレスを登録することもできます。その場合は、「プライマリDNSサーバアドレス,セカンダリDNSサーバアドレス」と、IPアドレスを”,”（カンマ）で区切ります。

![](150201-54ce2c6f59679.png)

「8.8.4.4」をプライマリDNSサーバ、「8.8.8.8」をセカンダリDNSサーバとして登録する場合は、「8.8.4.4,8.8.8.8」とカンマ区切りで続けて入力しましょう。

#### MacでGoogle Public DNSを設定する

MacでDNSサーバの設定を変更するためには、「システム環境設定」→「ネットワーク」を選択し、Wi-Fiの「詳細」ボタンをクリックします。その際、左下の鍵アイコンをクリックして施錠を解除しておきましょう。

![](150201-54ce2c71b285f.png)

「DNS」タブを選択し、「DNSサーバ」欄の「+」ボタンをクリックし、プライマリDNSサーバ、セカンダリDNSサーバの順に追加しましょう。

![](150201-54ce2c7a07a6e.png)

### ルーターのファームウェアを最新バージョンにアップデートする

お使いのルーターのファームウェアの最新版がリリースされていないか確認してみましょう。最新版には安定性やセキュリティの改善、不具合の修正等が含まれている場合があります。必ず最新版のファームウェアを使用するのが良いでしょう。

ルーターのファームウェアの最新情報については、各メーカーのホームページを確認してください。

AirMacワイヤレス装置（Express、Extreme、Time Capsuleなど）を使用している場合は、AirMacユーティリティーの環境設定で自動的にアップデートを確認する設定に変更しておきましょう。

![](150201-54ce2c7cea396.png)

### 最新のルーターに買い換える

ルーターの処理能力にも限界はあります。ルーターは「たかがインターネットに接続するためのもの」と思いがちですが、不正なパケットを遮断するなど簡易ファイアーウォールの役割を果たしたりと、本業以外の役割も多いのです。

最新のルーターであればあるほど、その処理能力は高くなっているため、一考してみる価値があります。安直な考えだと思われるかもしれませんが、数年前のパソコンと、今手元にあるパソコンの処理性能を比較した場合、その差は顕著であるのと同様です。

また最新の機種に買い換えることで、2.4GHz帯と5GHz帯のデュアルバンドに対応できる可能性もあります。前述のとおり、比較的混雑していない5GHz帯を利用することで、Wi-Fi転送速度が向上する可能性があります。

### インターネットプロバイダーを乗り換える

私の環境では、数年間インターネットプロバイダーとしてOCNを使用していましたが、夜間など混みあう時間帯のパフォーマンスが著しく低下する現象が、ここ数か月立て続けに発生していたため、思い切ってOCNからNURO光に乗り換えました。

<http://www.nuro.jp/>

NURO光は、世界最速下り2Gbpsを謳うSo-netが扱うインターネットプロバイダーで、料金は戸建ての場合、回線使用料とプロバイダー料金込みで4,743円と、他社のサービスと比較しても割安な価格設定となっています。

また、今なら新規申し込みで現金キャッシュバックや月々の割引サービスを受けることができるため、現在のプロバイダーやフレッツ光などの回線に満足していない場合は乗り換えを検討してみましょう。

お使いのプロバイダーによっては、加入条件に契約期間に縛りを設けている場合もあるため、乗り換えを検討する場合には、事前に十分に約款などを確認することをオススメします。

<https://kakaku.com/bb/>

## まとめ

私の環境で効果がテキメンだったのは、「最新のルーターに買い換える」ことでした。数Mbps〜十数Mbpsという低層地帯から、いっきに70〜80Mbpsの世界に飛び出したときは、インターネットの環境が目を見はるほど改善しました。

今回ご紹介した指針をもとに、Wi-Fi環境の改善にぜひチャレンジしてみてください。
