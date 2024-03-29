---
categories:
- Blog
date: 2021-07-20 07:37:36+00:00
draft: false
tags:
- lt
- gt
- div
- インデックス
- class
title: Hugo + Algolia + Instantsearch.jsで静的サイトに全文検索を導入
type: post
---

Hugo + Algolia + Instantsearch.jsで、静的サイトに全文検索を導入するまでの一部始終をまとめてみました。

## 完成版

メニューバー右側のテキストボックスに検索キーワードを入力して、Enterキーを押します。

![](126136903-23630997-b6c4-4a62-83b2-5ea431c3819a.png)

検索したキーワードにヒットした記事が表示されます。

![](126136149-044ba396-9da0-4167-a195-7c8fa9e3cc3c.png)

最低限の実装です。テーマに合わせた検索結果の表示のみこだわりました。しかし、検索したキーワードをハイライトする、そもそも検索したキーワードを表示するなど、改善の余地があります。

## Algoliaとは

<https://www.algolia.com/>

検索エンジンを自ホストで持つ必要がないため、Hugoなどで構築された静的サイトと相性がとても良いです。もちろん、動的サイトでも同様の実装は可能です。Hugoの公式ドキュメントもAlgoliaによる検索エンジンが採用されています。

無償プランの制限事項は以下の通りです。インデックスとして登録できるレコード件数が10,000件、月間のリクエスト数が10,000件と制限があります。ブログの場合、リクエスト数が無償プランを利用するかどうかの検討材料になりそうです。また、どれくらい全文検索が利用されているかどうかをテストしてみると良いでしょう。

- Forever free
- No credit card required
- 10,000 Records
- 10,000 Search requests/mo
- 10,000 Recommend requests/mo

また、無償プランの場合、検索結果の画面にAlgoliaのブランドロゴを表示するように求められていますので、忘れないように表示しましょう。

- The Free Plan requires you to display the Algolia logo next to the search results.

## Algoliaでインデックスを作成する

1. Algoliaのインデックスを更新するためのJSONファイルを作成する
2. 作成したJSONファイルを用いてインデックスを登録する
3. ブログ更新時にAlgoliaのインデックスを更新する

### Algoliaへ登録するためのJSONファイルを作成する

Algoliaのインデックスへ登録するために、JSONファイルを作成する必要があります。Hugoによるビルド時に、毎回自動的にJSONファイルが作成されるように`config.yaml`（今回はYAML形式）の記載を変更します。具体的には以下を追記します。`outputs`配下の項目は、テーマによっては既に記入されている場合があります。その場合、フォーマットの末尾に「Algolia」追加してください。

```yaml
outputFormats:
   Algolia:
     baseName: algolia
     isPlainText: true
     mediaType: application/json
     notAlternative: true
 outputs:
   home: [HTML, RSS, Algolia]
```

続いて、JSONファイルを自動生成するためのテンプレートを作成します。テーマのルートディレクトリ配下で、`layouts/list.algolia.json`を作成してください。

```go-html-template
{{/* Generates a valid Algolia search index */}}
{{- $.Scratch.Add "index" slice -}}
{{- range .Site.RegularPages -}}
     {{- $.Scratch.Add "index" (dict "objectID" .File.UniqueID "title" .Title "tags" .Params.tags "categories" .Params.categories "permalink" .Permalink "summary" .Summary "publish_date" .PublishDate) -}}
{{- end -}}
{{- $.Scratch.Get "index" | jsonify -}}
```

`objectID`は、Algoliaでレコードを一意に識別するためのキーです。Hugoの場合、ファイルのパスに応じてハッシュ値を生成する`.UniqueID`が便利です。一意に識別するキーがない場合、インデックス登録時にエラーになりますので注意してください。対象は、`.Site.RegularPages`のみで、カテゴリーやタグ毎に生成される固有のページは除外しています。

また、本文をすべてインデックスに含む場合、レコード毎のバイト数制限（10KB）を超過する可能性があるため除外し、代替手段として`.Summary`を追加しています。

<https://www.algolia.com/doc/faq/basics/is-there-a-size-limit-for-my-index-records/>

### Algoliaへインデックスを登録する

専用のCLIが用意されているため、そちらを利用するのが便利です。`npm`コマンドで`atomic-algolia`をインストールします。プロジェクトのルートディレクトリ配下で、以下のコマンドを実行してください。ここでは、`npm`コマンドの使い方は割愛します。

```bash
npm install -D atomic-algolia
```

また、`package.json`内の`scripts`に、`atomic-algolia`コマンドが実行されるよう登録しておきます。抜粋版の`package.json`は、以下の通りです。`npm run algolia`でコマンドが実行されるようになります。

```json
{
  "name": "ottanxyz",
  "scripts": {
    "algolia": "atomic-algolia"
  },
  "dependencies": {
    "algoliasearch": "^3.35.1",
    "atomic-algolia": "^0.3.19"
  }
}
```

続いて、Algoliaのダッシュボードの「API Keys」から、以下の項目を取得します。なお、`Admin API Key`は、文字通りAlgoliaに登録したインデックスに関する全ての権限（インデックスの登録から削除まで）を有する重要なアクセスキーです。外部へ流出しないよう十分に注意しましょう。

- Application ID
- Search-Only API Key
- Admin API Key

`atomic-algolia`コマンドで使用するために、`.env`ファイルをプロジェクトのルートディレクトリ直下に作成します。また、前述の「Admin API Key」を含みますので、誤ってGitHub等のGitリポジトリへ登録されないよう、`.gitignore`へ登録するのを忘れないようにしましょう。

```env
ALGOLIA_APP_ID=取得したApplication ID
ALGOLIA_ADMIN_KEY=取得したAdmin API Key
ALGOLIA_INDEX_NAME=作成するインデックス名
ALGOLIA_INDEX_FILE=public/algolia.json
```

インデックス名は、他のインデックスと区別できればなんでも良いですが、わかりやすい名前にしておきましょう。実際の検索時に、ここで作成したインデックス名を使用します。また、これまでの設定通りであれば、`public`ディレクトリ直下へ`algolia.json`という名前のファイルが生成されるようになります。

ここまで準備ができたら、いったん`hugo`コマンドでビルドし、以下のコマンドを実行し、Algoliaへインデックスを登録してみましょう。エラーが発生する場合、APIキーや、`aloglia.json`のビルドに失敗している可能性がありますので、設定を見直してみてください。

```bash
npm run algolia
```

### Algoliaの設定

Algoliaのダッシュボードを参照します。意図したインデックスが構築されているかどうかを確認しましょう。今回は、「Configuration」→「Searchable attributes」で、「title」「summary」を検索対象として設定しました。その他、Algoliaでは検索のアルゴリズムをカスタマイズすることが可能ですが、デフォルトのまま進みました。

![](126151189-40834640-8358-40c3-84fe-4c760eed044d.jpeg)

### Algoliaのインデックス自動更新

ブログ更新の都度、毎回手動でAlgoliaのインデックスを更新するのは面倒です。`hugo`コマンドによるビルドに加えて、`npm run algolia`が実行されるようにしておきましょう。（例：`hugo && npm run algolia`）

## Instantsearch.jsによる検索画面の作成

<https://www.algolia.com/doc/guides/building-search-ui/what-is-instantsearch/js/>

Instantsearch.jsによる、バニラなJavaScriptでのフロント部分を実装します。

ここまでで、検索のバックエンドは完成しました。続いて、フロント部分を作成していきます。まず、Hugoのテーマディレクトリに、`content/search.md`を作成します。`type`、`layout`で参照するテンプレートを指定するだけのファイルです。テンプレートとして、`layouts/static/search.html`が参照されます。また、サイトマップに含まれないように`priority`を極端に低い数値にしていますが、これがベストかどうかはわからないので調査予定です。

```markdown
—-
title: "検索結果"
sitemap:
  priority : 0.1
type: static
layout: search
—-
```

続いて、テンプレートとなる`layouts/static/search.html`を作成します。ここは、テーマのテンプレートにもよりますので、必須部分のみ抜粋して後ほど解説します。

```go-html-template
{{ define "main" }}
<section class="hero is-dark">
  <div class="hero-body">
    <div class="container has-text-centered">
      <h1 class="title has-text-weight-bold">
        検索結果<span id="search-term"></span>
      </h1>
    </div>
  </div>
</section>
<section class="section is-hidden">
  <div class="container">
    <div id="searchbox"></div>
  </div>
</section>
<section class="section">
  <div class="container">
    <div id="hits" class="columns is-multiline"></div>
  </div>
</section>
{{ end }}
{{ define "addscripts" }}
<script
  src="https://cdn.jsdelivr.net/npm/algoliasearch@4.5.1/dist/algoliasearch-lite.umd.js"
  integrity="sha256-EXPXz4W6pQgfYY3yTpnDa3OH8/EPn16ciVsPQ/ypsjk="
  crossorigin="anonymous"
></script>
<script
  src="https://cdn.jsdelivr.net/npm/instantsearch.js@4.8.3/dist/instantsearch.production.min.js"
  integrity="sha256-LAGhRRdtVoD6RLo2qDQsU2mp+XVSciKRC8XPOBWmofM="
  crossorigin="anonymous"
></script>
<script>
  let params = new URLSearchParams(document.location.search.substring(1));

  const searchClient = algoliasearch(
    "WHA9JKWNW0",
    "5b2c83156b29a7d67868e8440fc800b7"
  );

  const search = instantsearch({
    indexName: "index",
    searchClient,
  });

  search.addWidgets([
    instantsearch.widgets.searchBox({
      container: "#searchbox",
    }),

    instantsearch.widgets.hits({
      container: "#hits",
      templates: {
        empty: "No results",
        item: ``,
      },
    }),
  ]);

  const renderHits = (renderOptions, isFirstRender) => {
    const { hits, widgetParams } = renderOptions;

    widgetParams.container.innerHTML = `
    ${hits
      .map(
        (item) =>
          `<div class="column is-12-mobile is-6-tablet is-4-desktop">
            <div class="card">
                <div class="card-content">
                    <div class="title is-4"><a class="has-text-black-bis has-text-weight-bold" href="${item.permalink}">${item.title}</a></div>
                    <div class="mb-2">${item.summary}</div>
                    <footer class="card-footer">
                        <div class="card-footer-item">
                        <time datetime=${item.publish_date}>
                            <i class="far fa-calendar-alt"></i>&nbsp;${item.publish_date}
                        </time>
                        </div>
                    </footer>
                </div>
            </div>
        </div>`
      )
      .join("")}
  `;
  };

  const customHits = instantsearch.connectors.connectHits(renderHits);

  search.addWidgets([
    customHits({
      container: document.querySelector("#hits"),
    }),
  ]);

  search.start();
  search.setUiState({
    index: {
      query: params.get("q"),
    },
  });
</script>
{{ end }}
```

まず、表示用のHTMLを記述します。

```html
<div id="searchbox"></div>
<div id="hits" class="columns is-multiline"></div>
```

指定するIDが重要です。後ほど、Instantsearch.jsから参照します。IDを変更したい場合は、Instantsearch.js側も変更してください。`searchbox`が検索フォーム、`hits`が検索結果を表示するHTMLエレメントのルート要素となります。

ただし、今回はURLのクエリ文字列に渡された文字列をキーワードとして検索したいので、`searchbox`をCSSで表示しないよう制御しています。`searchbox`ウィジェットを使用せず、検索する方法が用意されているかもしれません。同ウィジェットへ渡した文字列が検索キーワードとなるため、ウィジェット自体は表示しないようにして残しています。後ほど、このウィジェットに直接クエリ文字列を指定します。

```html
<script
  src="https://cdn.jsdelivr.net/npm/algoliasearch@4.5.1/dist/algoliasearch-lite.umd.js"
  integrity="sha256-EXPXz4W6pQgfYY3yTpnDa3OH8/EPn16ciVsPQ/ypsjk="
  crossorigin="anonymous"
></script>
<script
  src="https://cdn.jsdelivr.net/npm/instantsearch.js@4.8.3/dist/instantsearch.production.min.js"
  integrity="sha256-LAGhRRdtVoD6RLo2qDQsU2mp+XVSciKRC8XPOBWmofM="
  crossorigin="anonymous"
></script>
```

続いて、`algoliasearch.js`と`instantsearch.js`を読み込みます。最新版は、本項の冒頭にあるAlgoliaのドキュメントページを参照してください。

```javascript
let params = new URLSearchParams(document.location.search.substring(1));
```

URLのクエリ文字列を受け取ります。Hugoで、URLのクエリ文字列を動的に処理することはできないため、JavaScript（ブラウザ）側で実装する必要があります。例えば、URLが`https://ottan.jp/search/?q=hoge`であれば、`params.get("q")`で`hoge`を取得できます。

```javascript
  const searchClient = algoliasearch(
    "WHA9JKWNW0", // 事前に取得したApplication ID
    "5b2c83156b29a7d67868e8440fc800b7" // 事前に取得したSearch-Only API Key。誤ってAdmin API Keyを公開しないよう注意
  );

  const search = instantsearch({
    indexName: "index", // 事前に作成したインデックス名
    searchClient,
  });

  search.addWidgets([
    instantsearch.widgets.searchBox({
      container: "#searchbox", // 検索フォームを表示するためのHTMLエレメントを指定
    }),

    instantsearch.widgets.hits({
      container: "#hits", // 検索結果を表示するためのHTMLエレメントを指定
      templates: {
        empty: "No results", // 検索結果に何もヒットしない場合の表示用文字列
        item: ``,
      },
    }),
  ]);
```

ここまでは、Algoliaのスタートガイドにあるテンプレートを、ほぼ流用しています。Admin API Keyを誤って公開するJavaScript内に記述しないように注意しましょう。無償プランでは、検索用のAPI Keyを隠蔽するための手段がないように見えます。もし、公開したくない場合は、Netlify FunctionsやVercelのServerless Functionsを利用するなど、サーバサイド側で処理するよう変更してみてください。

```javascript
  const renderHits = (renderOptions, isFirstRender) => {
    const { hits, widgetParams } = renderOptions;

    widgetParams.container.innerHTML = `
    ${hits
      .map(
        (item) =>
          `<div class="column is-12-mobile is-6-tablet is-4-desktop">
                …
                    <div class="title is-4"><a class="has-text-black-bis has-text-weight-bold" href="${item.permalink}">${item.title}</a></div>
                …
        </div>`
      )
      .join("")}
  `;
  };

  const customHits = instantsearch.connectors.connectHits(renderHits);

  search.addWidgets([
    customHits({
      container: document.querySelector("#hits"), // 検索結果を表示するためのHTMLエレメントを指定
    }),
  ]);
```

検索結果をカスタマイズするためのスクリプトです。`renderHits`関数を作成して、Instantsearch.jsへインスタンスを渡します。`widgetParams.container.innerHTML`で、検索結果に表示されるHTMLを書き換えています。ここでは、一部のみを抜粋しています。`map`関数により、`${item.title}`のようにして検索結果（JSON形式）を参照することができます。`${…}`の形式で参照する必要がありますので注意してください。また、`title`は、インデックスへ登録するJSONファイルを作成したときのキーを指定します。パーマリンクや更新日時等を別途取得すると良いでしょう。

ここではテンプレートをカスタマイズしましたが、デフォルトのテンプレートをそのまま使用することもできます。`renderHits`関数以降の定義が不要になるため、シンプルです。詳細はAlgoliaの公式ドキュメント（冒頭）を参照してください。

```javascript
  search.start();
  search.setUiState({
    // Algoliaに登録したインデックス名を指定
    index: {
      query: params.get("q"), // URLのクエリ文字列を指定
    },
  });
```

`setUiState`関数で、キーワードをAlgoliaへ渡します。

### 検索フォームの設置

以下の検索フォームをメニューバー等、検索しやすい場所に設置してください。`/search`へ移動する、`name=“q”`にクエリ文字列のキー（`q`）を指定しています。デザインは自由です。

```html
<form action="/search“>
    ….
    <input class="input" type="search" name="q" placeholder="Search..." />
    ….
</form>
```

## まとめ

まだまだ荒削りな部分はありますが、静的サイトでも全文検索を導入することができました。以前、サーバサイドで処理する必要はありましたが、Fuse.jsを利用した全文検索も紹介していますので、そちらもぜひご覧ください。
