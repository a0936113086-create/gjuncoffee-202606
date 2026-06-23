# 好鄰居托嬰網站維護規格

## 專案概述

本專案為「好鄰居托嬰」單頁式形象網站，使用 Bootstrap 5 作為版面框架，並搭配自訂 CSS 完成品牌視覺、輪播、月齡卡片、關於我們與頁尾聯絡資訊。

目前網站為純靜態頁面，可直接以瀏覽器開啟 `index.html` 預覽。

## 檔案結構

```text
website/
├── index.html
├── SPEC.md
├── css/
│   ├── bootstrap.min.css
│   └── custom.css
└── js/
    └── bootstrap.bundle.min.js
```

## 技術規格

- HTML：`index.html`
- CSS 框架：Bootstrap 5，本地端引用
- 自訂樣式：`css/custom.css`
- JavaScript：Bootstrap Bundle，本地端引用
- 圖片來源：目前使用線上 Unsplash 圖片網址
- Icons：未使用外部 icon CDN，社群與聯絡圖示目前以文字搭配 CSS 呈現

## CSS 載入順序

`index.html` 的 `<head>` 必須先載入 Bootstrap，再載入自訂樣式：

```html
<link href="css/bootstrap.min.css" rel="stylesheet">
<link href="css/custom.css" rel="stylesheet">
```

此順序不可反過來，因為 `custom.css` 需要覆蓋部分 Bootstrap 預設樣式。

## JavaScript 載入

頁面底部載入 Bootstrap Bundle：

```html
<script src="js/bootstrap.bundle.min.js"></script>
```

`bootstrap.bundle.min.js` 已包含 Carousel、Collapse 等互動元件所需功能，不需額外載入 Popper。

## 頁面區塊

### 1. Header / Navbar

位置：`index.html` 的 `<nav class="navbar ...">`

內容包含：

- SVG 品牌 Logo
- 品牌名稱：好鄰居托嬰
- 英文副標：Infant Care Center
- 導覽連結：首頁、關於我、寶寶月齡介紹、聯絡我們、登入
- 預約諮詢按鈕

主要樣式：

- `.navbar`
- `.navbar-brand`
- `.brand-logo`
- `.brand-title`
- `.brand-subtitle`
- `.nav-link`
- `.btn-brand`

### 2. 首頁輪播

位置：`<section class="hero-wrap">`

使用 Bootstrap Carousel：

- ID：`babyCarousel`
- 目前共 5 張輪播
- 每張圖片使用 inline `background-image`
- 文字覆蓋在圖片左側

主要樣式：

- `.hero-wrap`
- `.hero-carousel`
- `.hero-copy`

維護注意：

- 若新增或刪除輪播張數，需同步調整 `.carousel-indicators` 的按鈕數量與 `data-bs-slide-to` 編號。
- 輪播圖片目前為線上圖片，若要改成本地圖片，建議新增 `images/` 資料夾並使用相對路徑，例如 `images/hero-01.jpg`。

### 3. 寶寶月齡介紹

位置：`<section id="baby-age">`

目前卡片：

- 3M 嬰幼兒照護
- 6M 嬰幼兒照護
- 9M 嬰幼兒照護
- 12M 嬰幼兒照護

主要樣式：

- `.age-section`
- `.age-card`
- `.more-btn`

維護注意：

- 每張卡片使用 Bootstrap Grid：`col-sm-6 col-xl-3`
- 若卡片超過 4 張，可維持同樣欄位結構，會自動換行。

### 4. 關於我

位置：`<section id="about">`

內容包含：

- 左側圖片區塊
- 右側文字說明

主要樣式：

- `.about-section`
- `.about-panel`
- `.about-photo`
- `.about-content`

維護注意：

- `.about-photo` 的圖片目前寫在 `custom.css` 中。
- 若要頻繁更換關於我圖片，建議改成 HTML `<img>`，方便非工程人員維護。

### 5. 回到頂端

位置：`<a class="back-top" href="#top">`

目前使用純文字箭頭 `↑`，透過 CSS 製作成固定右下角按鈕。

主要樣式：

- `.back-top`

### 6. Footer

位置：`<footer id="contact">`

內容包含：

- Footer 品牌 Logo
- 聯絡我們按鈕
- 社群連結
- 電話
- Email
- 地址
- 版權宣告

主要樣式：

- `.site-footer`
- `.footer-brand`
- `.contact-pill`
- `.socials`
- `.contact-row`
- `.contact-icon`
- `.copyright`

## 品牌視覺

主要色彩定義在 `css/custom.css` 的 `:root`：

```css
:root {
  --mint: #b7f4da;
  --mint-soft: #e6fff1;
  --green: #188553;
  --green-dark: #0d5f3b;
  --leaf: #65bb4a;
  --sun: #f5c05e;
  --red: #ef233c;
  --blue: #224f9f;
  --ink: #172322;
  --muted: #667472;
}
```

設計方向：

- 主色：薄荷綠、托嬰友善感
- 輔色：深綠，提升穩定與信任感
- 強調色：紅色，用於「瞭解更多」等行動按鈕
- 文字重點：藍色，用於關於我區塊，呼應原始設計稿

## RWD 響應式

自訂 CSS 目前包含兩組主要斷點：

- `max-width: 991.98px`：平板與手機導覽、輪播高度、關於我圖片高度
- `max-width: 575.98px`：手機 Logo、輪播、區塊間距、回頂端按鈕

維護時請優先沿用 Bootstrap Grid 與現有斷點，避免新增過多零散 media query。

## 後續維護建議

- 新增頁面時，沿用相同 head 引用：
  - `css/bootstrap.min.css`
  - `css/custom.css`
  - `js/bootstrap.bundle.min.js`
- 不要再使用 Bootstrap CDN，避免離線環境樣式失效。
- 若要加入本地圖片，建議建立：

```text
images/
├── hero-01.jpg
├── hero-02.jpg
├── baby-3m.jpg
└── about.jpg
```

- 若要加入真正圖示，可下載 Bootstrap Icons 到本地端，再新增：

```html
<link href="css/bootstrap-icons.css" rel="stylesheet">
```

- 自訂樣式請集中維護在 `css/custom.css`，不要再放回 `index.html` 的 `<style>`。

## 目前已知限制

- 輪播與卡片圖片仍使用線上圖片網址。
- Logo 目前為內嵌 SVG，若多頁共用且需要集中管理，可改成獨立 `images/logo.svg`。
- Footer 社群連結目前為 `#`，正式上線前需替換為實際網址。
- 「登入」目前只有導覽連結，尚未建立登入頁或登入功能。

