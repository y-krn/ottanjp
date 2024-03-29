---
categories:
- Blog
date: 2021-07-09 11:16:52+00:00
draft: false
tags:
- github
- ev
- post
- en
- 起票
title: Issueを起票したらGitHub ActionsによりIssueの内容がそのまま記事として公開されるようにしてみた
type: post
---

当ブログは、Netlify + Hugoで構築してます。GitHubへMarkdownで記述したコンテンツをコミットすると、Netlifyにより自動ビルドが走り、記事が公開されます。しばらくは、このフローで問題ありませんでしたが、基本的に横着な自分なので、ある理由によりブログ更新が滞るようになりました。

## Netlify + Hugo構成はiPhoneから管理できない

「GitHubへコミットする」、この行為が意外とめんどうだったのです。WordPressを使用していた時は、公式アプリやサードパーティのアプリを用いることで、どこからでもiPhoneから記事の公開ができていました。Netlifyにも簡易的なCMS機能はあるのですが、管理画面がレスポンシブ対応しておらず、使い勝手は良いとは言えません。また、GitHubへのコミットという行為が追加された事も大きなネックでした。記事を公開するには、iPhoneではなくMacやPCをわざわざ用意する必要があったのです。

iPhoneにもGitHubの公式アプリがありますが、MacやPCのGitクライアントのように多機能ではありません。Markdownで記述したファイルをコミットする手順も、iPhoneだけで完結しようとすると手間がかかります。ただ、IssueやPull Requestを参照したり、コメントを付けたりするには十分な機能が備わってます。

### Issueに特定のラベルを付与したらGitHub Actionsを起動して、自動的にプルリクエストを作成する

GitHubのIssueは、Markdown記法が利用できます。これはもしかして、Hugo + Netlifyと相性が良いのではないかと思いました。また、Issueの起票、編集のみであれば、iPhoneのGitHubアプリでも十分可能です。このアイデアの実現にあたっては、[こちら](https://shazow.net/posts/github-issues-as-a-hugo-frontend/)の記事、特にGitHub Actionsの設定ファイルをかなり参考にさせていただきました。

ただし、問題点もあります。

まず、ブログのタイトルですが、これはIssueのタイトルをそのまま転用できそうです。

次に、記事のカテゴリです。単一の記事には複数のカテゴリーを付与できます。Issueに付与したラベルを、そのままカテゴリーとすることも考えましたが、Issueの起票を何らかの手段でGitHub Actionsに渡さなければなりません。今回は、「publish」というラベルの付与をトリガーにGitHub Actionsを起動するため、安易にラベルが散らかると処理が複雑になる恐れがありました。そこで、付与された最初のラベルをそのままカテゴリーとすることとしました。何も付与されてない場合、「publish」というカテゴリーが付与されてしまう問題もありましたが、個人で使うものですし妥協しました。

次に、スラッグ（slug）です。これは、URLの一部を構成する要素で、これまではタイトルをDeepL等で英訳し、助詞等のノイズを除去したものを手動で割り当ててました。Issueの1行目はスラッグ、とういうルールを作ることも考えました。しかし、忘れることもありますし、何よりIssueは記事を書くことに集中したかったのです。今回はGitHub Actionsで取得できるリポジトリ単位で一意となるIssueのID（数字）を用いることとしました。URLがただの数字の羅列になる、これまで公開した記事と整合性が取れなくなるなど、課題はありましたが妥協できる範囲と判断しました。

### 作成したIssueからPull Requestを作成する

GitHub Actionsのマーケットプレイスで公開されている、[こちら](https://github.com/marketplace/actions/create-pull-request)を使用しました。GitHub Actionsで、自動的にブランチの作成からプルリクエストの作成まで行ってくれます。詳細は、上記のリンクのREADMEを参照してください。

### GitHub Actionsの全容

参考までにGitHub Actionsの設定ファイルを記載しておきます。Issueの制御は、リポジトリのアクセス権限次第ですが、基本オープンであるため、誰でも起票からプルリクエストを作成できてしまいます。Front MatterにAuthorを用意して、複数人で管理することもできそうです。

```yml
name: Publish post from issue

on:
  issues:
    types: ['labeled']

jobs:
  build:
    if: ${{ github.event.label.name == 'publish' }}
    runs-on: ubuntu-18.04
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true
          fetch-depth: 0

      - name: Generate Post
        env:
          POST_TITLE: ${{ github.event.issue.title }}
          POST_BODY: ${{ github.event.issue.body }}
          POST_ID: ${{ github.event.issue.id }}
          POST_CATEGORY: ${{ github.event.issue.labels[0].name }}
        run: |
           YEAR=`date "+%Y"`
           MONTH=`date "+%m"`
           mkdir -p content/posts/$YEAR/$MONTH
           cd content/posts/$YEAR/$MONTH
           cat > $POST_ID.md << EOF
           ---
           draft: false
           title: $POST_TITLE
           date: ${{ github.event.issue.updated_at }}
           type: post
           slug: $POST_ID
           category: ["${POST_CATEGORY}"]
           ---

           $POST_BODY
           EOF

      - name: Create Pull Request
        uses: peter-evans/create-pull-request@v3
        with:
          delete-branch: true
          title: "publish: ${{ github.event.issue.title}}"
          body: |
            Automatically sprouted for publishing.
            Merging will publish to: https://ottan.jp/
              Closes #${{ github.event.issue.number }}
            reviewers: "${{ github.repository_owner }}"
            commit-message: "post: ${{ github.event.issue.title }}"
```

## 良かったこと

- iPhoneのGitHub公式アプリの、Markdown記法をサポートする機能が意外と充実（コピーしたリンクをペーストすると、自動的にMarkdown記法に変換してくれる）
- iPhoneから手軽にブログを更新できるようになった（移動時間など、Macを使用できない時間帯でもブログが書ける）
- Issueに起票しておけばどこからでも参照できる

## あきらめたこと・改善が必要な点

- タグ（単一の記事に、複数付与できる）には未対応
- 画像を貼れない（Issueに画像は添付できますが、そのままでは一緒にビルドされない）

ちょっと2点目が痛いところではあるのですが、そういった記事を書きたい場合は、従来通りVS Codeなど使用すれば良いのではないかと思います。
