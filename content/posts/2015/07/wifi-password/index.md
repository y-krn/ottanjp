---
author:
- '@ottanxyz'
categories:
- Mac
date: 2015-07-15 00:00:00+00:00
draft: false
tags:
- password
- fi
- wi
- ssid
- ネットワーク
title: 現在接続しているWi-Fiネットワークのパスワードを確認する方法
type: post
---

![](150715-55a671d220f31.jpg)

現在接続されているWi-Fiネットワークのパスワードを忘れてしまった場合、以下のコマンドを実行することで、パスワードを表示できます。ただし、実行には管理者権限が必要ですので注意してください。

    security find-generic-password -ga <SSID>

<SSID>には、接続しているWi-FiネットワークのSSIDを入力します。また、過去に接続したことのあるWi-Fiネットワークであれば、そのSSIDでも構いません。

**実行例**

    security find-generic-password -ga "Time Capsule 5GHz"

![](150715-55a671ce37e28.png)

コマンドを実行すると、管理者権限を持つユーザのユーザ名とパスワードの入力を求められますので、入力します。

![](150715-55a671d01ad66.png)

すると、「password:」欄に平文でパスワードが表示されます。

## 参考リンク

<http://www.labnol.org/software/find-wi-fi-network-password/28949/>
