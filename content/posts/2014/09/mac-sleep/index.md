---
author:
- '@ottanxyz'
categories:
- Mac
date: 2014-09-19 00:00:00+00:00
draft: false
tags:
- スリープ
- sleep
- jst
- 状態
- モード
title: Macがスリープから復帰するのが遅い場合の対処法
type: post
---

![](140919-541bc2a262e05.jpg)

Macを開いてスリープから復帰させた際に、マウスカーソルだけがぽつんと表れて、画面がなかなか表示されないという現象に遭遇したことはありませんか？その場合、スリープ時に問題が発生している可能性があります。

そもそもMacのスリープとは何なのか、そこからまずは入り込んでいき、最終的に問題の根本を探ることにしました。

## Macのスリープは3種類存在する

まず、Macのスリープには3種類存在することをご存知でしたか？ターミナルを開いて以下のコマンドを実行してみてください。

```bash
pmset -g
```

以下のような結果が得られたでしょうか。

    Active Profiles:
    Battery Power  -1*
    AC Power  -1
    Currently in use:
     standbydelay         10800
     standby              1
     halfdim              1
     hibernatefile        /var/vm/sleepimage
     darkwakes            0
     gpuswitch            2
     disksleep            10
     sleep                1
     autopoweroffdelay    14400
     hibernatemode        3
     autopoweroff         1
     ttyskeepawake        1
     displaysleep         2
     acwake               0
     lidwake              1

`Battery Power`の横の`*`は、Macがバッテリー電源で駆動中であることを表しています。`pmset`コマンドの結果に表示されている数値はすべてバッテリー駆動時のものです。

さて、この`hibernatemode`がスリープの種類を表していて、MacBookの場合は「3」が初期設定となっています。この`hibernatemode`には以下のような意味があります。

| hibernatemode | モード     | メモリの状態 | ディスクへの保存 | 消費電力 |
| ------------- | ---------- | ------------ | ---------------- | -------- |
| 0             | Sleep      | 維持         | しない           | 高       |
| 3             | Safe Sleep | 維持         | する             | 高       |
| 25            | Deep Sleep | 破棄         | する             | 低       |

Sleepモード、Safe Sleepモードの場合、メモリの状態を維持しますが、**休止状態になると、その内容は破棄されてしまいます**。また、Safe Sleepモード、Deep Sleepモードの場合、メモリの状態をファイルへ書き込みを行います。そのため、**休止状態になった場合でも、ファイルの内容から状態を復元**できます。Deep Sleepモードの場合、スリープおよびスリープからの復帰に時間を要します。ただし、Safe Sleepモードの場合は、メモリの状態も維持しているため、休止状態になっていなければ高速な復帰が可能です。

### メモリの状態はどこに保存される？

デフォルトの保存先は`/var/vm/sleepimage`です。`pmset`コマンドの実行結果にある`hibernatefile`がイメージファイルの保存場所を表しています。

```bash
ls -l /var/vm/sleepimage
```

    -rw------T  1 root  wheel  1073741824  9 18 08:29 /var/vm/sleepimage

### その他の内容について

`pmset`コマンドで表示されるその他の内容について確認しておきましょう。

| 項目                                                                 | 説明                                                                                                                                                            |
| -------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| standbydelay                                                         | ディスクにメモリの状態を書き込み必要のあるSafe Sleep、Deep Sleepモードの場合の、ディスクをスリープさせるまでの遅延時間（秒）                                    |
| standby                                                              | スタンバイを行うかどうか（0：スタンバイオフ、1：スタンバイオン）                                                                                                |
| halfdim                                                              | ディスプレイがスリープ状態になる前に輝度を下げるかどうか（輝度を下げない：0、輝度を下げる：1）                                                                  |
| darkwakes                                                            | バッテリー電源使用時に`Power Nap`（スリープ中にバックグラウンドで新着メール等のタスクを実行する）をオンにするかどうか（Power Napをオフ：0、Power Napをオン：1） |
| gpuswicth                                                            | 不明（調査不足。GPUに関連するフラグと思われる）                                                                                                                 |
| disksleep                                                            | ディスクをスリープさせるまでの時間（分）                                                                                                                        |
| autopoweroffdelay                                                    | スリープから休止状態になるまでの時間（秒）                                                                                                                      |
| autopoweroff休止状態を使用するかどうか（0：使用しない、1：使用する） |                                                                                                                                                                 |
| ttyskeepawake                                                        | リモートセッションがアクティブの場合にスリープするかどうか（0：スリープする、1：スリープしない）                                                                |
| displaysleep                                                         | ディスプレイをスリープさせるまでの時間（分）                                                                                                                    |
| acwake                                                               | 電源が変更されたら（バッテリー駆動からACコンセントなど）スリープを解除するかどうか（0：解除しない、1：解除する）                                                |
| lidwake                                                              | ディスプレイを開いたときにスリープを解除するかどうか（解除しない：0、解除する：0）                                                                              |

### 設定値を変更するためには？

これらの設定値を変更するためには、同様に`pmset`コマンドを使用します。

```bash
sudo pmset -a [項目名] [値]
```

たとえば、スリープモードについて、休止状態になり内容が失われても良い場合は、「Safe Sleep」から「Sleep」に変更することでより高速なスリープを実現できます。

```bash
sudo pmset -a hibernatemode 0
```

## スリープ状態から復帰時の問題

さて、前置きが長くなりましたが、冒頭のようにスリープ状態からの復帰時、黒い画面にマウスカーソルだけぽつんと表示されてしまい、なかなか復帰しないことがありました。このような時にはスリープに問題が発生している可能性があります。ターミナルで以下のコマンドを実行してみましょう。（一時的にテキストファイルにリダイレクトすることをオススメします）

```bash
pmset -g log
```

これで電源管理（スリープ、休止）に関するログが出力されます。その中から「Timedout」を探します。

    2014/09/18 21:38:10 JST  Sleep                Idle Sleep: Using BATT (Charge:57%)                                         673 secs
    2014/09/18 21:38:11 JST  SlowResponse         PMConnection: Response from mDNSResponder is slow (powercaps:0x0)                     614 ms
    2014/09/18 21:38:11 JST  WakeRequests         Clients requested wake events: None
    2014/09/18 21:49:23 JST  DarkWake             DarkWake [CDN] due to EC.LidClose/Maintenance: Using BATT (Charge:57%)
    2014/09/18 21:49:23 JST  HibernateStats       hibmode=3 standbydelay=10800                                                          rd=224 ms
    2014/09/18 21:49:23 JST  Timedout             Kernel: Response from Creative Cloud timed out (powercaps:0x9)                        30000 ms
    2014/09/18 21:49:23 JST  Timedout             Kernel: Response from Adobe CEF Helper timed out (powercaps:0x9)                      30000 ms
    2014/09/18 21:49:23 JST  Sleep                Maintenance Sleep: Using BATT (Charge:57%)                                  2014 secs
    2014/09/18 21:49:23 JST  WakeRequests         Clients requested wake events: None
    2014/09/18 22:22:57 JST  Wake                 Wake [CDNVA] due to EC.LidOpen/Lid Open: Using BATT (Charge:56%)
    2014/09/18 22:22:57 JST  HibernateStats       hibmode=3 standbydelay=10800

Adobe Creative Cloudが原因で30,000ミリ秒（30秒）間待機していることがわかります。最近、Adobe製品を触る機会はめっきりなくなったので、Adobe Creative Cloudは真っ先に削除しました。

それ以来、スリープ状態からの復帰は今まで通りの早さを取り戻しました。スリープで問題を抱えている場合は是非お試しください。

## 参考リンク

以下のサイトが大変参考になりました！

<https://zariganitosh.hatenablog.jp/entry/20110706/about_sleep>
