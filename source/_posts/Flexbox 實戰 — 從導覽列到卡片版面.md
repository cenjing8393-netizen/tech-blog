---
title: Flexbox 實戰 — 從導覽列到卡片版面
date: 2026-07-10
updated: 2026-07-10
tags:
  - CSS
  - Flexbox
  - Layout
categories:
  - 前端
description: 不談理論，直接看實戰。導覽列、垂直居中、卡片列表、黏底 footer，四個最常用的 Flexbox 場景一次學會。
---
![flexbox-vertical-center.png](https://cdn.jsdelivr.net/gh/cenjing8393-netizen/tech-blog-images/images/flexbox-vertical-center.png)

## 前言

如果你問我 CSS 哪個屬性改變最多，我的答案一定是 `display: flex`。

在 Flexbox 出現之前，做垂直居中要寫 `position: absolute` + `transform`，做等高欄位要靠 JavaScript 或各種骯髒的 hack。Flexbox 把這些問題全簡化成幾行 CSS。

但很多人卡住的原因不是不懂屬性，而是**不知道什麼時候用哪個**。這篇我們不看完整的屬性列表，直接從實戰場景出發。

## 場景一：導覽列

最常見的 navbar 結構：Logo 在左、導覽連結在右。

```html
<nav class="navbar">
  <div class="logo">My Blog</div>
  <ul class="nav-links">
    <li><a href="#">首頁</a></li>
    <li><a href="#">文章</a></li>
    <li><a href="#">關於</a></li>
  </ul>
</nav>
```

```css
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
}

.nav-links {
  display: flex;
  gap: 1.5rem;
  list-style: none;
}
```

兩行 `display: flex` 就搞定。`justify-content: space-between` 把 Logo 推到左邊、連結推到右邊，`align-items: center` 讓兩者在交叉軸居中。

## 場景二：垂直居中

「把一個 div 放在畫面正中間」曾經是 CSS 面試經典題。現在只需要：

```css
.centered {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}
```

不管內容是一個按鈕還是一整段文字，三行就置中。

## 場景三：卡片列表

這是最常見的 Flexbox 實戰——一排卡片，自動換行，每個卡片等寬：

```css
.card-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 1.5rem;
}

.card {
  flex: 1 1 300px;
  /*  shorthand: grow shrink basis */
}
```

`flex: 1 1 300px` 的意思是：可以長大、可以縮小、基準寬度 300px。當容器夠寬時每張卡片等分空間，不夠寬時自動換行。

如果希望最後一排卡片靠左而不是拉伸：

```css
.card-grid::after {
  content: "";
  flex: 1 1 300px;
}
```

用一個偽元素吃掉多餘空間，讓最後一排的卡片保持原本寬度。

## 場景四：黏底 Footer

內容不夠高時 footer 黏在底部，內容超過時 footer 被往下推：

```css
body {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

main {
  flex: 1;  /* 撐滿剩餘空間 */
}

footer {
  /* 自然被推到最底部 */
}
```

## 場景五：表單欄位對齊

常常需要一個標籤 + 輸入框在同一行：

```css
.form-row {
  display: flex;
  align-items: baseline;  /* 文字基線對齊 */
  gap: 1rem;
}

.form-row label {
  flex: 0 0 120px;  /* 固定寬度 */
  text-align: right;
}

.form-row input {
  flex: 1;  /* 撐滿 */
}
```

## 常見迷思

**迷思一：flex: 1 就是等寬**

不對。`flex: 1` 是 `flex: 1 1 0%`，意思是基準寬度為 0，所以會等分空間。如果你想要「內容自適應寬度」，應該用 `flex: 1 1 auto` 或 `flex: auto`。

**迷思二：gap 不能用於舊瀏覽器**

`gap` 在 Flexbox 的支援度已經很好了。如果真的需要相容超舊瀏覽器，可以用 `margin` 搭配 `:not(:last-child)` 取代。

**迷思三：Flexbox 可以取代 Grid**

Flexbox 是一維（行或列），Grid 是二維（行列並存）。導覽列用 Flexbox，整體頁面大框架用 Grid。兩者是互補不是取代。

## 結語

Flexbox 最棒的地方是它的「彈性」。你不用算精確的寬度，只要告訴瀏覽器「這個撐滿、那個自動換行」，剩下的 Flexbox 會幫你處理。

熟練之後你會發現，八九成的版面問題其實不需要 Grid，一行 `display: flex` 就夠了。

## 參考資料

- [MDN Flexbox](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox)
- [CSS Tricks: A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [Flexbox Froggy — 互動式學習遊戲](https://flexboxfroggy.com/)
- [DevPalettes — Complete CSS Flexbox Guide (2026 Edition)](https://devpalettes.com/blog/css-flexbox-guide/)

