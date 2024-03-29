---
author:
- '@ottanxyz'
categories:
- Mac
date: 2015-05-30 00:00:00+00:00
draft: false
tags:
- xxx
- gt
- token
- echo
- トークン
title: Homebrewで検索時にGitHubのエラーが出る場合の対処法
type: post
---

![](150530-5569bc9476a8f.png)

Homebrew については、[Mac でプレゼン資料に数式を貼り付けるのに便利な「LaTeXiT」](/posts/2014/09/mac-latex-presentation-92/)で詳細を解説していますのでご覧いただくとして、Homebrew で便利なアプリケーションを検索している時に、GitHub のエラーが表示されてしまう事象の対処法をメモしておきたいと思います。

## Homebrew でエラーが発生した場合の対処法

    brew search <keyword>

一定期間中に、繰り返し連続して以下のコマンドを実行すると、下記のエラーが表示されることがあります。「XXX.XXX.XXX.XXX」は、自身の IP アドレスを示しています。期間を置いて実行するか、トークンを取得しなさいという意味のエラーです。期間を置いて実行するのも面倒臭いので、トークンで解決したいと思います。

    Error: GitHub API rate limit exceeded for XXX.XXX.XXX.XXX. (But here's the good news: Authenticated requests get a higher rate limit. Check out the documentation for more details.)
    Try again in 48 minutes 37 seconds, or create an personal access token:
      https://github.com/settings/tokens
    and then set it as HOMEBREW_GITHUB_API_TOKEN.

### GitHub で Homebrew のトークンを入手する

以下のリンクにアクセスし、GitHub にログインしてください。

<https://github.com/settings/tokens>

「Generate new token」ボタンをクリックします。

![](150530-5569b77a46e8a.png)

「Token description」に任意の名称を入力して、「Generate token」をクリックします。

![](150530-5569b77c7f4fa.png)

薄い緑色の枠に囲まれた箇所に表示されている文字列がアクセストークンになります。このトークンを、ターミナルの環境変数に設定します。

![](150530-5569b77fb0a33.png)

### ログインシェルに zsh を使用している場合

ログインシェルに`/bin/zsh`を使用している場合は、以下のコマンドを実行してください。`XXXXXXXX`にはさきほど入手したアクセストークンを入力します。

    $ echo HOMEBREW_GITHUB_API_TOKEN=XXXXXXXX >> ~/.zshrc
    echo export HOMEBREW_GITHUB_API_TOKEN >> ~/.zshrc

現在、自分が何のログインシェルを使用しているかわからない場合は、以下のコマンドを実行してください。大抵の場合、`/bin/zsh`、または`/bin/bash`と思われます。

    echo $SHELL

### ログインシェルに bash を使用している場合

ログインシェルに`/bin/bash`を使用している場合は、以下のコマンドを実行してください。`XXXXXXXX`にはさきほど入手したアクセストークンを入力します。`/bin/zsh`の場合と比較して、やや複雑ですが、これはログイン時に`~/.bashrc`が読み込まれないことを未然に防止するものです。

    echo HOMEBREW_GITHUB_API_TOKEN=XXXXXXXX >> ~/.bashrc
    echo export HOMEBREW_GITHUB_API_TOKEN >> ~/.bashrc

    echo "if [ -f ~/.bashrc ] ; then" >> ~/.bash_profile
    echo ". ~/.bashrc" >> ~/.bash_profile
    echo "fi" >> ~/.bash_profile

## まとめ

ターミナルに不慣れな場合は、やや複雑に感じますが、このままコマンドを実行すれば環境が整うように記述しましたので、ぜひチャレンジしてみてください。
