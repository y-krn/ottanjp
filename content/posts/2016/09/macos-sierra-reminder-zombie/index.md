---
author:
- '@ottanxyz'
categories:
- Mac
date: 2016-09-26 00:00:00+00:00
draft: false
tags:
- リマインダー
- カレンダー
- イベント
- 何回
- ゾンビ
title: macOS Sierraでリマインダーがゾンビのように復活し「実行済み」にできない場合の対処法
type: post
---

![](160926-57e92d41e52f6.jpg)

macOS Sierraは、起動ディスクを作成した上で、クリーンインストールをして使用しているのですが、不思議な事象に遭遇しました。通知されるリマインダーを何回「実行済み」にしても、ゾンビのように復活して同じ内容のリマインダーが通知されるのです。macOS Sierraのバグのような気がしなくもないので、将来的にアップデートで修正される可能性もありますが、とりあえず対処法を見つけましたのでご紹介します。

![](160926-57e92d48809ec.png)

何回も何回も資源ごみの日であることを通知してくれる可愛いリマインダー。

## リマインダーが「実行済み」にできない場合の対処法

我が家では、ゴミの日（とくに資源ごみ、燃えないゴミの日）を忘れないように、家族で共有したリマインダーに登録しています。iPhone（iOS 10）では問題なく動作するのですが、macOS Sierraだけ、そんなに忘れてほしくないのか、何回「実行済み」を選択しても選択しても、ゾンビのように通知が復活する事象に遭遇したのです。「実行済み」を選択しても、1分間経たないうちに再度通知される傍迷惑なリマインダーです。確かに忘れないでしょうけど…。

### iCloudのオフ、オン、Finderで関連ファイル削除で解決

Finderで関連ファイルを削除してしまうため、**Macローカルに保存されているカレンダーのイベントやリマインダーは削除される可能性があります**。以降の作業を実施する場合は、カレンダーのイベントやリマインダーはすべてiCloudに保存されているものとします。

![](160926-57e92d4d264d7.png)

「システム環境設定」→「iCloud」を選択します。

![](160926-57e92d53347b2.png)

「カレンダー」「リマインダー」を、いったんオフにします。この時点で、「カレンダー.app」「リマインダー.app」を開いている場合は、メニューから終了します。

![](160926-57e92d57d429a.png)

続いて、Finderを開いて、`~/Library/Calendars`を削除して、ゴミ箱を空にします。この時点で、Macローカルに保存されている、カレンダーのイベントやリマインダーは削除される可能性がありますので十分にご注意ください。

![](160926-57e92d5d37325.png)

再度「iCloud」から「カレンダー」「リマインダー」をオンにします。そして、「カレンダー.app」「リマインダー.app」を起動します。開いた直後は、イベントもリマインダーも空ですが、徐々にiCloudから復元されます。すべてのイベントやリマインダーが復活するまでは多少時間がかかります。

## まとめ

どういう状況で発生するのか原因がはっきりとしませんが、もし、リマインダーが「実行済み」にならない場合は、ぜひこの方法をお試しください。
