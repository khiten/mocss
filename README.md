# MOCSS 基本方針

**MOCSS = Modularized CSS**
ver. 3
05.Jul.2019 改定

## 基本形式＝モジュール＆エレメント

- モジュールは再利用可能な一つのまとまりのあるHTML群
- エレメントはモジュール配下の各要素
- クラス名の基本はモジュールとエレメントで構成する
- モジュールとエレメントは「-」でつなぐ
- エレメントが入れ子になる場合も「-」でつなぐ


```
class="module"
```
```
class="module-element"
```
```
class="module-element-element"
```

### 命名規則

#### なるべく英語を使う

世界で認識されているような日本語はOK

○ item  
✕ shohin  
○ cars  
✕ kuruma  
○ kimono  

#### 変に省略しない

長いより短いほうがベターだけど見て意味がわからないくらいなら長いほうがいい  
誤解するような省略語も避ける。一般的に定着している省略形はOK

○ kimonoHakamaSet  
✕ kmset  
○ dateTime  
✕ dtm  
○ admin (administrator)  
○ auth (authentication)  
○ btn (button)  
○ bg (background)  


## モジュール・エレメントはキャメルケースで記述

モジュール・エレメント名にアンダースコアやハイフンは使用しない。  
→ 複数ワードで一つのモジュール・エレメント名となる場合は注意

○ news  
○ headlineNews  
○ news-publishDate  
✕ headline-news  
✕ headline_news  
✕ news-publish-date  
✕ news-publish_date  


## モディファイアー（派生クラス）

すでにあるクラスのスタイルの一部のみ変更となる要素が対象。

### 基本形

**接頭辞 as_**

**as_xxxx**

css では必ず複合クラスとして記述する（同名のモディファイアーを別の場所でも使えるよう）

```
.news {
  ..
}
.news.as-headline {
  ..
}
```

ex).
```
<section class="news as_headline">
...
```
```
<a class="socialButton as_facebook">
...
```


## ステート（状態クラス）

ページ遷移、クリック、マウスオーバーなど、ユーザーのアクションによって変化する要素が対象。

### 基本形

**接頭辞 is_**

**is_xxxx**

ex).
```
<ul class="categories">
  <li class="category is_selected">
  ...
```
```
<section class="item">
  <figure class="item-image is_focused">
  ...
```

## ファンクション（JS発動クラス）

JS側の処理を発動するためのクラス。  
このクラスがあたっているとHTMLを見るだけでJSの処理が存在することがひと目で分かる。  
→ ファンクションにはスタイルをあてない。スタイルを当てたいなら別途クラスを適用する。

### 基本形

**接頭辞 fn_**

**fn_xxxx**

ex).
```
<img class="fn_srcset">
...
```

## 汎用クラス

モジュールではない、単独で機能する汎用クラス

### 基本形

**接頭辞 ge_**

**ge_xxxx**

※ 基本的には ge_ + cssプロパティ名 + 値

ex).
```
<p class="ge_colorRed">
...
```
```
<div class="ge_bgGray">
...
```




---

## レイアウトクラス

レイアウト（段組み）のためだけのクラス

接頭辞はとくになし、単純にエレメントとして表現する

優先的に
- wrapper
- outer
- inner

などを使う

```
<div class="news-wrapper">
  <section class="news">
  ...
```
```
<div class="news-textWrapper">
  <h3 class="news-heading">
  ..
</div>
<figure class="news-imageWrapper">
  <img class="news-thumbnail">
  ...
</div>
```

# 注意

## エレメントを無理に階層化しない

HTMLがどれだけ階層化しても、エレメントは**その要素を簡潔に表現**できていればそれでよい。

### ○ 要素の役割を簡潔に表現
```
<section class="news">
  <div class="news-textWrapper">
    <h3 class="news-title">TITLE</h3>
    <time class="news-publishDate" datetime="2019-07-03T11:22:00+09:00">2019.07.03</time>
    <p class="news-category">EVENT</p>
    <div class="news-content">CONTENT</div>
  </div>
  <figure class="news-imageWrapper">
    <img class="news-thumbnail" src="/img/news03.jpg">
  </figure>
</section>
```

### ✕（無駄な階層化）
```
<section class="news">
  <div class="news-textWrapper">
    <h3 class="news-textWrapper-title">TITLE</h3>
    <time class="news-textWrapper-publishDate" datetime="2019-07-03T11:22:00+09:00">2019.07.03</time>
    <p class="news-textWrapper-category">EVENT</p>
    <div class="news-textWrapper-content">CONTENT</div>
  </div>
  <figure class="news-imageWrapper">
    <img class="news-imageWrapper-thumbnail" src="/img/news03.jpg">
  </figure>
</section>
```


---


# サンプルコード

```

<div class="headlineNews-wrapper indexContent-wrapper as_bgGray">
  <section class="headlineNews indexContent">
    <h2 class="headlineNews-heading indexContent-heading">NEWS</h2>
    <div class="headlineNews-list indexContent-content">
      
      <section class="news as_headline">
        <div class="news-textWrapper">
          <h3 class="news-title">これはニュース３です。</h3>
          <time class="news-publishDate">2019.07.03</time>
          <p class="news-category">イベント</p>
          <div class="news-content">これはニュース３の最初の30文字とかそんな感じの文字列が並んでいるイメージなんですよ。</div>
        </div>
        <figure class="news-imageWrapper">
          <img class="news-thumbnail fn_srcset" src="/img/news03.jpg">
        </figure>
      </section>
      
      <section class="news as_headline">
        <div class="news-textWrapper">
          <h3 class="news-title">これはニュース２です。</h3>
          <time class="news-publishDate">2019.06.30</time>
          <p class="news-category">お知らせ</p>
          <div class="news-content">これはニュース２の最初の30文字とかそんな感じの文字列が並んでいるイメージなんですよ。</div>
        </div>
        <figure class="news-imageWrapper">
          <img class="news-thumbnail fn_srcset" src="/img/news02.jpg">
        </figure>
      </section>
      
      <section class="news as_headline">
        <div class="news-textWrapper">
          <h3 class="news-title">これはニュース１です。</h3>
          <time class="news-publishDate">2019.06.10</time>
          <p class="news-category">募集</p>
          <div class="news-content">これはニュース１の最初の30文字とかそんな感じの文字列が並んでいるイメージなんですよ。</div>
        </div>
        <figure class="news-imageWrapper">
          <img class="news-thumbnail fn_srcset" src="/img/news01.jpg">
        </figure>
      </section>

    </div>
  </section>
</div>
```