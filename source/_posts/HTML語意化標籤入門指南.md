---
title: HTML 語意化標籤入門指南
date: 2026-07-08
updated: 2026-07-08
tags:
  - HTML
  - SEO
  - Accessibility
  - Semantics
categories:
  - 前端
description: 什麼是 HTML 語意化標籤？為什麼不要什麼都用 <div> 包？這篇帶你認識 header、main、article 等常用語意標籤，附完整範例。
---

![HTML 語意化標籤](https://cdn.jsdelivr.net/gh/cenjing8393-netizen/tech-blog-images/images/blog-cover-accessibility.png)
## 前言

我剛學 HTML 的時候，很習慣什麼都用 `<div>` 包。左邊一個 div，右邊一個 div，全部塞進 div。反正看起來都差不多，能跑就好嘛。

後來回頭看自己寫的 code，滿滿的 `<div class="header-wrapper">`、`<div class="content-container">`、`<div class="footer-box">`……我才發現一件尷尬的事：我的 HTML 什麼都沒說，只是靠 class 名稱在解釋自己。

這就是為什麼我們需要**語意化標籤**。

## 語意化標籤到底是什麼？

簡單講，就是「用標籤的名字來表達內容的用途」。

與其寫 `<div class="nav">`，不如直接寫 `<nav>`。與其寫 `<div class="main-content">`，不如直接寫 `<main>`。瀏覽器、搜尋引擎、螢幕閱讀器一看就知道這是什麼意思。

好處有三個：

1. **SEO 更好** — Google 知道哪裡是主要內容、哪裡是導覽列，權重給得更準確
2. **無障礙友善** — 螢幕閱讀器可以直接跳到 `<main>` 或 `<nav>`，不用在 div 海裡迷路
3. **你自己看得懂** — 三個月後回來改 code，不用靠 class 名稱推理

## 七個你一定要知道的語意標籤

### `<header>` — 頁首

放網站 Logo、主標題、導覽列的地方。注意：一頁可以有多個 `<header>`，例如文章裡面也可以有 header。

```html
<header>
  <h1>我的技術部落格</h1>
  <nav>
    <ul>
      <li><a href="/">首頁</a></li>
      <li><a href="/about">關於我</a></li>
    </ul>
  </nav>
</header>
```

### `<nav>` — 導覽區

包主要導覽連結用的。通常放在 `<header>` 裡，也可以放在 `<footer>` 做次要選單。

```html
<nav aria-label="主要選單">
  <ul>
    <li><a href="/posts">文章列表</a></li>
    <li><a href="/tags">標籤</a></li>
    <li><a href="/contact">聯絡我</a></li>
  </ul>
</nav>
```

### `<main>` — 主要內容

一頁只能有一個。把所有獨特的內容放這裡，不要把導覽列、側邊欄、頁尾塞進來。

```html
<main>
  <!-- 這裡放真正的文章內容 -->
</main>
```

### `<article>` — 獨立內容單元

適合放部落格文章、新聞、產品卡片。關鍵判斷：如果把這段內容抽出來貼到別的地方，它自己還說得通嗎？說得通就是 `<article>`。

```html
<article>
  <h2>用 Flexbox 還是 Grid？</h2>
  <p>很多新手會問這個問題。其實重點很簡單……</p>
  <footer>
    <p>發表於 2026-07-08 | 標籤：CSS, Layout</p>
  </footer>
</article>
```

### `<section>` — 主題區塊

把相關內容分組。跟 `<article>` 的差別是：`<section>` 的內容脫離上下文可能會沒頭沒尾。

```html
<section>
  <h2>為什麼要學 CSS Grid？</h2>
  <p>Grid 是專門處理二維佈局的工具……</p>
</section>
```

### `<aside>` — 補充資訊

側邊欄、相關文章、廣告，這些跟主要內容有關但不影響主體架構的東西。

```html
<aside>
  <h3>熱門文章</h3>
  <ul>
    <li><a href="/flexbox-guide">Flexbox 完全指南</a></li>
    <li><a href="/css-grid">CSS Grid 實戰</a></li>
  </ul>
</aside>
```

### `<footer>` — 頁尾

版權宣告、聯絡方式、社群連結。像 `<header>` 一樣，一頁可以有多個（文章裡也可以有 footer）。

```html
<footer>
  <p>&copy; 2026 我的技術部落格. All rights reserved.</p>
  <nav>
    <a href="/privacy">隱私權政策</a>
  </nav>
</footer>
```

## 完整範例：部落格頁面骨架

把上面全部兜起來，就是一個標準的部落格頁面：

```html
<body>
  <header>
    <h1>我的技術部落格</h1>
    <nav>
      <ul>
        <li><a href="/">首頁</a></li>
        <li><a href="/posts">文章</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <article>
      <header>
        <h2>HTML 語意化標籤入門</h2>
        <p>2026-07-08</p>
      </header>

      <section>
        <h3>為什麼要語意化？</h3>
        <p>內容……</p>
      </section>

      <section>
        <h3>常見標籤</h3>
        <p>內容……</p>
      </section>
    </article>

    <aside>
      <h3>相關文章</h3>
      <ul>
        <li><a href="/css-guide">CSS 入門</a></li>
      </ul>
    </aside>
  </main>

  <footer>
    <p>&copy; 2026 我的技術部落格</p>
  </footer>
</body>
```

## 結語

學語意化標籤不用一次記全部，先從 `<header>`、`<nav>`、`<main>`、`<article>`、`<section>`、`<aside>`、`<footer>` 這七個開始就好。

下次寫 HTML 的時候，問自己一句話：「這個 div 真的需要嗎？還是換成語意標籤更適合？」

用對標籤之後，你會發現 code 自己就會說話。

![對比漫畫：div vs 語意化標籤](https://cdn.jsdelivr.net/gh/cenjing8393-netizen/tech-blog-images/images/blog-cover-semantic-comparison.png)

## 圖片提示詞

## 參考資料

- [MDN Web Docs — HTML 語意元素](https://developer.mozilla.org/zh-CN/docs/Glossary/Semantics)
- [iThome 鐵人賽 — HTML5 的語意標籤介紹](https://ithelp.ithome.com.tw/articles/10240446)
- [vocus — 我花了兩週學會 HTML：5 個語意標籤初學者真正需要](https://vocus.cc/article/690078ddfd897800017e9d4c)
- [愛立歐網路 — 2026 HTML 架構教學：從草稿到語意化版型](https://www.ileo.com.tw/school-detail/html5-website-structure-guide/)
- [W3C — HTML5 規範：The aside element](https://html.spec.whatwg.org/multipage/sections.html#the-aside-element)
- [新視野網頁設計 — HTML \<strong\>、\<b\>、\<em\> 標籤語意與正確用法](https://www.nsc.tw/article_detail/html-strong-b-em-tags-usage-guide)
- [文網股份 — HTML 語意標籤：提升網頁設計的語意結構與可訪問性](https://www.cx.com.tw/modules/news/article.php?storyid=135)
- [Sean 工作版 — HTML 5 基本語法、語意標籤、元素總整理](https://seanacnet.com/html/html5-tag/)

---
