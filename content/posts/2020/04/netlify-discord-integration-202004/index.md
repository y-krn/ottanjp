---
author:
- '@ottanxyz'
categories:
- Blog
date: 2020-04-30 00:00:00+00:00
tags:
- slack
- デプロイ
- ウェブフック
- url
- started
title: NetlifyのDeploy結果をDiscordへ通知する
---

Netlify上でのデプロイ結果を、Discordへ通知する方法をご紹介します。Slack連携とほぼやり方は同一ですが、GitHub同様に1点のみ注意点があります。

## Discordのウェブフックを準備

チャンネルの編集画面から、ウェブフックを追加します。ウェブフック作成時に生成されるURLをコピーしておきます。Discord側の設定は以上です。

![](screenshot-2020-04-30-19.26.21.png)

## NetlifyのSlack integration

「Settings」→「Build & Deploy」→「Deploy notifications」をクリックします。

![](screenshot-2020-04-30-19.32.05.png)

「Deploy notifications」→「Outgoing Notifications」から「Add notification」をクリックします。

![](screenshot-2020-04-30-19.25.48.png)

「Slack integration」に続いて「Outgoing webhook」があり、後者を選択したくなりますが、前者の「Slack integration」を選択します。

![](screenshot-2020-04-30-19.25.54.png)

「Slack integration」で以下の項目を入力します。

* Event to listen for
  * Deploy started（デプロイ開始時）
  * Deploy succeeded（デプロイ成功時）
  * Deploy failed（デプロイ失敗時）
* Slack Incoming Webhook URL
  * DiscordでコピーしたURL + **「/slack」**
* Channel (optional)
  * デフォルト

URLの末尾に**「/slack」**を付与してください。これで、デプロイ開始時、成功時、失敗時にDiscordへ通知されるようになります。

![](screenshot-2020-04-30-19.28.14.png)
