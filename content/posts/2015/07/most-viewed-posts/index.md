---
author:
- '@ottanxyz'
categories:
- Blog
date: 2015-07-12 00:00:00+00:00
draft: false
tags:
- post
- gt
- ソート
- 記事
- カラム
title: WordPressでプラグインを使わずに閲覧数の多い人気記事を取得し、管理画面に閲覧数を表示する
type: post
---

![](150712-55a243bd758e7.jpg)

WordPressで閲覧数の多い人気記事を表示するプラグインは数多くありますが、今回はプラグインの力を借りずに自力で実装してみたいと思います。

そもそも、データベースを有するWordPressにおいて、なぜ簡単に閲覧数の多い記事を表示できないか。それは、WordPressのデータベースには、**閲覧数を保持するカラムがない**からです。何やら雲行きが怪しくなってきましたが、メゲズに最後までお付き合いいただければと思います。

## 閲覧数を保持するカスタムフィールド

WordPress初期構築時に作成するデータベースの各テーブルの接頭辞は`wp_`とします。また、記事執筆時のWordPressのバージョンは、`4.2.2`です。バージョンが異なる場合、以下のコードが正常に動作しない場合があります。

さて、記事を保持するWordPressのテーブルはというと`wp_posts`です。このテーブルには、コメント数をカウントするカラム（`comment_count`）はあっても、閲覧数をカウントするものはありません。

![](150712-55a243bee8cbf.png)

このテーブルに`post_views`のようなカラムがあれば苦労しなくてすむのですが…。では、自分でカラムを追加すればよいのか？いいえ、それもできません（技術的には可能ですが…）。WordPressのコアとなるテーブルの構造を変更することになり、仕様通りに動作しなくなる可能性があるからです。将来的なバージョンアップのことを考えれば、影響範囲は極力最小限に抑えたいものです。

![](150712-55a243c22ec55.png)

そこで、今回はいったんこのテーブルのことを忘れて、`wp_postmeta`テーブルに注目します。`wp_posts`と比較すると、単純な構造をしています。このテーブルには、**記事のメタ情報**が格納されています。

![](150712-55a243c4e71b5.png)

分かりやすい例が、WordPress標準機能のアイキャッチ画像です。上図をご覧ください。記事を一意に識別する`post_id`と共に、アイキャッチ画像のファイル名や、画像ファイルのメタ情報が保存されていることがわかります。

`wp_postmeta`には、**カスタムフィールドの情報が格納されます**。アイキャッチ画像もカスタムフィールドの一種です。弊サイトでは、検索エンジン向けの記事ごとのキーワード情報を格納しています。これを応用すれば、何となく実装できそうな気がしませんか。

- 記事ごとに閲覧数を保持するメタ情報を`wp_postmeta`テーブルに格納する
- 記事が閲覧される都度、同テーブルに格納した値をインクリメントする
- 人気記事を表示したい場合は、同テーブルに格納した閲覧数をもとに記事をソートする

### 記事表示時にカスタムフィールドを更新する

`wp_postmeta`テーブルの値を更新するためには、`update_post_meta`関数を使います。同関数のパラメーターには記事のIDを指定しますが、該当のIDが同テーブルに存在しない場合は、新規にキーと値を追加します。

<https://codex.wordpress.org/Function_Reference/update_post_meta>

また、カスタムフィールドの値を取得するためには、`get_post_meta`関数を使います。メタ情報は記事ごとに保持していますから、パラメーターには記事のIDを指定する必要があります。詳細な使用方法については、後半に記述します。

<https://codex.wordpress.org/Function_Reference/get_post_meta>

以降、閲覧数を表すカスタムフィールドのキーの名称は`_custom_meta_views`とします。記事が表示された場合に、このカスタムフィールドをインクリメントできるように、以下のコードを**functions.php**に追加します。

```php
function update_custom_meta_views() {
 global $post;
 if ( 'publish' === get_post_status( $post ) && is_single() ) {
  $views = intval( get_post_meta( $post->ID, '_custom_meta_views', true ) );
  update_post_meta( $post->ID, '_custom_meta_views', ( $views + 1 ) );
 }
}
add_action( 'wp_head', 'update_custom_meta_views' );
```

`wp_head`にアクションを追加しています。`wp_head`関数が呼ばれた際に、今回追加した関数が呼ばれるようになります。逆に言えば、自作テーマ等で同関数が呼ばれない場合、カスタムフィールドはインクリメントされないことになりますので注意してください。

また、`is_single`関数で記事（固定ページ除く）の場合、`get_post_status`関数で記事の状態が「publish」（公開済み）である場合のみ、メタ情報を更新するようにしています。ドラフト（下書き）状態の場合、メタ情報は更新されません。

### 閲覧数でソートして人気記事を表示する

記事が閲覧されるたびにインクリメントされるカスタムフィールドの作成はここまでです。続いて、このカスタムフィールドを使用して、閲覧数の多い人気記事を取得する関数を作成しましょう。以下のコードを**functions.php**に追加します。

```php
function get_most_viewed() {
 $args = array(
  'post_type' => 'post',
  'post_status' => 'publish',
  'posts_per_page' => 5,
  'orderby' => 'meta_value_num',
  'meta_key' => '_custom_meta_views',
  'order' => 'DESC'
 );
 $posts = get_posts( $args );
 $output = "<ul>¥n";
 foreach( $posts as $post ) {
  $output .= "<li>" . $post->post_title . " - " . $post->_custom_meta_views . "Views</li>n";
 }

 $output .= "</ul>n";
 echo $output;
}
```

`get_posts`は指定された条件にもとづき合致する記事を配列で取得します。`$args`に指定しているパラメーターの意味は以下の通りです。

| パラメーター   | 説明                                                                                                                                                                                         |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| post_type      | 投稿タイプを表します。投稿タイプが「post」（記事）に限定します。                                                                                                                             |
| post_status    | 投稿の状態を表します。状態が「publish」（公開済み）に限定します。                                                                                                                            |
| posts_per_page | 取得する記事の件数です。                                                                                                                                                                     |
| orderby        | ソートする基準を指定します。閲覧数でソートしたいため`wp_postmeta`テーブルの`meta_value`を指定します。 また、`meta_value_num`を指定することで`meta_value`の値を数値に変換してソートできます。 |
| meta_key       | `meta_value`、`meta_value_num`を指定する場合は、必ず`meta_key`も合わせて指定します。閲覧数でソートしたいため、`_custom_meta_views`を指定します。                                             |
| order          | `DESC`（降順）、`ASC`（昇順）のいずれかを指定します。デフォルトは昇順です。`                                                                                                                 |

<https://codex.wordpress.org/Template_Tags/get_posts>

あとは`get_posts`で取得した配列を`foreach`でループします。`$post`変数には、`wp_posts`テーブルの情報が含まれています。例外的に、**カスタムフィールドの値を取得する場合は、`$post->_custom_meta_views`とカスタムフィールドのキー名を指定します**。その他、`$post`変数に含まれる情報としてよく使うものを挙げておきます。

| パラメーター  | 内容                                                                                  |
| ------------- | ------------------------------------------------------------------------------------- |
| ID            | 記事のIDです。                                                                        |
| post_author   | 記事の投稿者の**ID**です（投稿者名ではありません）                                    |
| post_date     | 投稿日時（現地時間：日本語版なら日本時間）です。YYYY-MM-DD HH:MM:SSの形式。           |
| post_modified | 投稿の最終更新日時（現地時間：日本語版なら日本時間）です。YYYY-MM-DD HH:MM:SSの形式。 |
| post_content  | 記事の内容。                                                                          |
| post_title    | 記事のタイトルです。                                                                  |
| post_excerpt  | 記事の抜粋です。                                                                      |
| comment_count | 記事に対するコメント数です。                                                          |

今回自作した`get_most_viewed`関数を使用すれば、好きな位置に人気記事一覧を表示できます。そのまま使用すると、以下のようなHTMLが出力されます。適宜カスタマイズして使用してください。

```html
<ul>
<li>WordPressのfunctions.phpの肥大化を防ぐ2つの方法 - 2Views</li>
<li>Alfredのカスタムサーチを利用して検索エンジンをハックする - 2Views</li>
<li>三日坊主でもできる、魅力にあふれた日記をiPhoneでつける方法 - 2Views</li>
<li>体が疲れてなかなか眠れない時はiPhoneを枕の下に置いてみよう - 1Views</li>
<li>Alfredで簡単にApp Storeのリンクを作成できる「iTunes Link Maker with Alfred」 - 1Views</li>
</ul>
```

#### get_most_viewed()関数の問題

`get_most_viewed()`関数は、閲覧数の多い記事を順に表示しますが、閲覧数は常に上書きされるため、ある程度人気記事が固定されて表示される可能性があります。そのため、たとえば、先月から今月にかけて投稿した記事に絞って人気記事を表示したい場合には、`date_query`等を使って下記のように編集します。

```php
function get_most_viewed() {
 $args = array(
 'post_type' => 'post',
 'post_status' => 'publish',
 'posts_per_page' => 5,
 'orderby' => 'meta_value_num',
 'meta_key' => '_custom_meta_views',
 'order' => 'DESC',
 'date_query' => array(
  array(
  'after' => date( 'Y/n/j', strtotime( date( 'Y-m-1' ) . '-1 month' ) ),
  'inclusive' => true,
  ),
 ),
 );
 $posts = get_posts( $args );
 $output = "<ul>¥n";
 foreach( $posts as $post ) {
 $output .= "<li>" . $post->post_title . " - " . $post->_custom_meta_views . "Views</li>n";
 }

 $output .= "</ul>n";
 echo $output;
}
```

### 管理画面の投稿一覧で閲覧数を確認する

ここまでで閲覧数で人気記事一覧を表示できることはわかりました。さらに、各々の記事がどれぐらい閲覧されているのか、管理画面の投稿一覧で見られると何かと便利ですよね。そこで、投稿一覧に追加したカスタムフィールドを表示できるようカスタマイズします。カスタマイズ後のイメージは以下の通りです。

![](150712-55a243c8ee334.png)

まず、投稿一覧にカラムを追加します。以下のコードを**functions.php**に追加します。

```php
function add_column_custom_meta_views( $columns ) {
 $columns['views'] = 'Views';
 return $columns;
}
add_filter( 'manage_posts_columns', 'add_column_custom_meta_views' );
```

`$columns`は、 投稿一覧のカラムを表しています。今回は、`views`というIDのカラムを追加します。また、`Views`は実際に投稿一覧の列名として表示される名前です。注意点として、**デフォルトのカラムと重複してはいけません**。`$columns`を出力した結果は以下の通りです。

    Array (
        [cb] => <input type="checkbox" />
        [title] => タイトル
        [author] => 作成者
        [categories] => カテゴリー
        [tags] => タグ
        [comments] => <span class="vers"><span title="コメント" class="comment-grey-bubble"></span></span>
        [date] => 日時 )

追加するカラムには、HTMLタグを使用できることもわかります。たとえば、コメントカラムにはWebフォントが指定されていますね。

これで投稿一覧に「Views」という名前のカラムを追加することはできましたが、まだ肝心要な値の表示ができません。値を表示するためには、以下のコードを**functions.php**追加します。

```php
function add_column_custom_meta_views_content( $column_name, $post_id ) {
 $views = intval( get_post_meta( $post_id, '_custom_meta_views', true ) );
 echo $views;
}
add_action( 'manage_posts_custom_column', 'add_column_custom_meta_views_content', 10, 2 );
```

`get_post_meta`は、前述のようにパラメーターに指定した記事のID、カスタムフィールドのキーをもとに値を取得する関数です。`get_post_meta`の最後のパラメーターは、値を配列、または文字列のどちらで取得するかを指定します。デフォルト値は配列を取得する`false`ですが、単独の値を取得する場合には`true`を指定したほうが便利です。

### 管理画面の投稿一覧で閲覧数でソートする

管理画面で閲覧数をもとにソートできれば素敵だと思いませんか。人気記事一覧を表示しなくても投稿一覧を見れば一目瞭然です。閲覧数でソートするためには、以下のコードを**functions.php**に追加してください。

```
function sortable_column_custom_meta_views( $columns ) {
 $columns['views'] = 'Views';
 return $columns;
}
add_filter( 'manage_edit-post_sortable_columns', 'sortable_column_custom_meta_views' );
```

`$columns`は、投稿一覧のカラムを表しています。追加するカラムのIDは、**投稿一覧に追加したカラムのIDと同一**にしてください。`Views`は、ソートするときURLの`orderby=`の後ろに表示される値です。何でも構いませんが、分かりやすく投稿一覧のカラム名と同一にしておくのが無難でしょう。

今回のポイントはフィルターです。管理画面には、さまざまなソート可能なカラムが存在します。カテゴリー、タグ、固定ページ一覧など、すべてソートできるカラムが存在します。投稿一覧の管理画面のカラムをソートするためには、`manage_**edit-post**_sortable_columns`をフィルターする必要があります。この、`edit-post`は、投稿一覧を表しています。

#### Viewsを数値としてソートする

以上で、管理画面で`views`をソートできるようになりましたが、`views`は数値として認識されないため、正しくソートされません。そこで、数値としてソートされるように、**functions.php**に以下のコードを追加します。

```php
function custom_orderby_custom_meta_views( $vars ) {
 if ( isset( $vars['orderby'] ) && 'Views' == $vars['orderby'] ) {
 $vars = array_merge( $vars, array(
  'meta_key' => '_custom_meta_views',
  'orderby' => 'meta_value_num'
  ));
 }
 return $vars;
}
add_filter( 'request', 'custom_orderby_custom_meta_views' );
```

URLに`orderby`が含まれ、かつ`orderby`の値が`Views`に等しいときのみ、`meta_key`、および`orderby`に指定した値でソートするよう、`request`をフィルターします。`meta_value_num`は、閲覧数でソートして人気記事を取得するために指定した値と同様の意味を持ちます。

## まとめ

今回作成したコードはあくまで実装を目的として記載しています。たとえば、同じページを何回もリロードした場合、その記事の閲覧数がその都度更新されます。そのため、あっという間に人気記事のねつ造が可能になってしまいます。

そのあたりの深掘りした考察については、長くなりそうなのでまた別の機会に譲りたいと思います。最後まで長文にお付き合いいただきまして、ありがとうございました。

### 参考リンク

今回、この記事を執筆するにあたって参考にさせていただいたサイトは以下の通りです。

- <http://notnil-creative.com/blog/archives/1476>
- <http://www.webopixel.net/wordpress/167.html>
