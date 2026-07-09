---
title: CSS 選擇器 — 從 class 到 :has()
date: 2026-07-09
updated: 2026-07-09
tags:
  - CSS
  - Selector
categories:
  - 前端
description: CSS 選擇器遠比你想的強大。從基礎的 class、ID，到現代的 :has() 父元素選擇器，這篇帶你一次掌握。
---
![css-selector-map.png](https://cdn.jsdelivr.net/gh/cenjing8393-netizen/tech-blog-images/images/css-selector-map.png)

## 前言

我剛開始寫 CSS 的時候，從頭到尾只靠 class 選擇器。什麼東西都用 class 命名，class 長到像在寫小說。

後來才發現，CSS 選擇器遠比我想的強大。很多時候根本不需要 class，就能精準選到你要的元素。

## 基本選擇器

這四種你應該早就用過了，快速複習：

```css
/* 元素選擇器 */
p { color: red; }

/* class 選擇器 */
.card { background: white; }

/* ID 選擇器 */
#header { height: 60px; }

/* 屬性選擇器 */
input[type="email"] { border-color: blue; }
```

屬性選擇器還有很多變化，像是 `[class~="btn"]`（包含某個單詞）、`[href^="https"]`（開頭匹配）、`[src$=".png"]`（結尾匹配），在實戰中非常實用。

## 組合選擇器

```css
/* 後代：div 裡面的所有 p */
div p { }

/* 子元素：div 的直接下一層 p */
div > p { }

/* 相鄰兄弟：h2 後面緊接的第一個 p */
h2 + p { }

/* 通用兄弟：h2 後面的所有 p */
h2 ~ p { }
```

這四個組合符號用對的話，可以少寫很多 class。

## 偽類選擇器

偽類用一個冒號 `:` 開頭，選取元素的特定狀態或位置。

### 位置相關

```css
/* 第一個和最後一個 */
li:first-child { }
li:last-child { }

/* 奇數偶數 */
li:nth-child(odd) { background: #f5f5f5; }
li:nth-child(even) { background: #fff; }

/* 自訂數列：選第 2、5、8、11……個 */
li:nth-child(3n+2) { }
```

`nth-child` 的 `An+B` 語法很多人覺得難懂，我的記憶法是：**n 從 0 開始數，A 是間隔，B 是起點**。`3n+2` 就是從第 2 個開始，每 3 個取一個。

### 邏輯相關

```css
/* 反選：選出所有不是 .disabled 的 input */
input:not(.disabled) { }

/* 多條件 OR */
:is(header, main, footer) p { }

/* 低優先級：跟 is 很像，但優先度是 0 */
:where(.alert, .warning) { color: red; }
```

`:where()` 一個很實用的場景是用在第三方元件覆寫樣式，因為它的優先度永遠是 0，不怕蓋不掉。

### 現代王者：`:has()`

`:has()` 被稱為「父元素選擇器」，雖然 CSS 沒有真正的父選擇器，但 `:has()` 做到了。

```css
/* 選取包含 .active 子元素的 li */
li:has(.active) { font-weight: bold; }

/* 選取包含 img 的 figure */
figure:has(img) { border: 1px solid #ddd; }

/* 表單驗證：選取包含無效輸入的表單 */
form:has(input:invalid) { border-color: red; }

/* 前面有圖示的 h2 */
h2:has(+ p) { margin-bottom: 0; }
```

## 偽元素

偽元素用 `::` 開頭，創造出原本 HTML 不存在的元素。

```css
/* 前後插入內容 */
.quote::before { content: "「"; }
.quote::after  { content: "」"; }

/* 選取第一行或第一個字母 */
p::first-line { font-weight: bold; }
p::first-letter { font-size: 2em; }

/* 選取使用者反白的文字 */
::selection { background: #ffd700; }
```

## 實戰範例：卡片列表

把上面學到的組合起來：

```css
/* 第一張卡片特殊樣式 */
.cards > article:first-child {
  border-top: none;
}

/* 每張卡片裡的標題，除了最後一個區塊 */
.card section:not(:last-child) {
  border-bottom: 1px solid #eee;
}

/* 含有圖片連結的卡片自動加上標記 */
.card:has(a img)::after {
  content: "含圖片";
  font-size: 0.8em;
}
```

## 結語

CSS 選擇器最棒的地方是：**你永遠不需要學完所有東西才開始用**。先從 class 和組合器開始，遇到需要篩選特定元素的時候，再打開這篇文章找對應的偽類。

等到你習慣用 `:nth-child` 取代 `.item-1`、`.item-2`……的時候，你已經回不去了。

## 參考資料

- [MDN Web Docs — :nth-child()](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/:nth-child)
- [CSS 選擇器完整列表 — 菜鸟教程](https://www.runoob.com/cssref/css-selectors.html)
- [STEAM 教育學習網 — CSS 選擇器](https://steam.oxxostudio.tw/category/css/selector/about-selector.html)
- [Chrome Developers — :nth-child() of S 語法](https://developer.chrome.com/docs/css-ui/css-nth-child-of-s?hl=zh-tw)
- [新人日誌 — CSS first-child、last-child、nth-child 指南](https://realnewbie.com/posts/css-first-childlast-childnth-child-nth-of-type)
