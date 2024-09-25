# [AOS - Animate on scroll library](http://michalsnik.github.io/aos/)

版本：3.0.0-beta.6

[![NPM version](https://img.shields.io/npm/v/aos/next.svg?style=flat)](https://npmjs.org/package/aos)
[![NPM downloads](https://img.shields.io/npm/dm/aos.svg?style=flat)](https://npmjs.org/package/aos)
[![Build Status](https://travis-ci.org/michalsnik/aos.svg?branch=master)](https://travis-ci.org/michalsnik/aos)
[![Gitter](https://badges.gitter.im/michalsnik/aos.svg)](https://gitter.im/michalsnik/aos?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

[![Twitter Follow](https://img.shields.io/twitter/follow/michalsnik.svg?style=social)](https://twitter.com/michalsnik) [![Twitter URL](https://img.shields.io/twitter/url/http/shields.io.svg?style=social)](https://twitter.com/home?status=AOS%20-%20Animate%20on%20Scroll%20library%0Ahttps%3A//github.com/michalsnik/aos)

## :exclamation::exclamation::exclamation: 這是 aos@next 的 README 檔案 :exclamation::exclamation::exclamation:

有關最新穩定版本 (v2) 的資訊，請前往 [這裡](https://github.com/michalsnik/aos/tree/v2)

---
### 🚀 [Demo](http://michalsnik.github.io/aos/)

### 🌟 Codepen 範例
- [不同的內建動畫](http://codepen.io/michalsnik/pen/WxNdvq)
- [使用錨點(Anchor)設定](http://codepen.io/michalsnik/pen/jrOYVO)
- [使用錨點(Anchor)位置和不同的緩和效果](http://codepen.io/michalsnik/pen/EyxoNm)
- [使用簡單的自訂動畫](http://codepen.io/michalsnik/pen/WxvNvE)

👉 為了更好地理解這實際上是如何運作的，我鼓勵您查看 [我在 CSS-tricks 上的文章](https://css-tricks.com/aos-css-driven-scroll-animation-library/).

---

## ⚙ 安裝

### 基本

在 `<head>` 中添加樣式：

```html
  <link rel="stylesheet" href="https://unpkg.com/aos@next/dist/aos.css" />
```

在 `</body>` 標籤關閉之前添加 script，並初始化 AOS：
```html
  <script src="https://unpkg.com/aos@next/dist/aos.js"></script>
  <script>
    AOS.init();
  </script>
```

### 使用套件管理器

安裝 `aos` 套件：
* `yarn add aos@next`
* 或 `npm install --save aos@next`

導入 script、樣式並初始化 AOS：
```js
import AOS from 'aos';
import 'aos/dist/aos.css'; // 您也可以使用 <link> 導入樣式
// ..
AOS.init();
```

為了使其正常運作，您需要確保您的建置流程已配置樣式載入器，並正確地將其捆綁在一起。
但是，如果您使用的是 [Parcel](https://parceljs.org/) ，則它將開箱即用。

---


## 🤔 如何使用它？

### 1. 初始化 AOS：

```js
AOS.init();

// 您也可以傳遞一個可選的設定物件
// 下面列出了預設設定
AOS.init({
  // 全域設定：
  disable: false, // 接受以下值：'phone'、'tablet'、'mobile'、布林值、運算式或函式
  startEvent: 'DOMContentLoaded', // 文件上發送的事件名稱，AOS 應該在該事件上初始化
  initClassName: 'aos-init', // 初始化後應用於元素的類別
  animatedClassName: 'aos-animate', // 在動畫期間應用於元素的類別
  useClassNames: false, // 如果為 true，將在滾動時將 `data-aos` 的內容添加為類別
  disableMutationObserver: false, // 禁用自動變異偵測（進階）
  debounceDelay: 50, // 調整視窗大小時使用的去抖動(debounce)延遲（進階）
  throttleDelay: 99, // 滾動頁面時使用的節流(throttle)延遲（進階）
  

  // 可以通過 `data-aos-*` 屬性在每個元素的基礎上覆蓋的設定：
  offset: 120, // 從原始觸發點偏移（以像素為單位）
  delay: 0, // 從 0 到 3000 的值，step 為 50 毫秒
  duration: 400, // 從 0 到 3000 的值，step 為 50 毫秒
  easing: 'ease', // AOS 動畫的預設緩和(easing)效果
  once: false, // 動畫是否只執行一次 - 在向下滾動時
  mirror: false, // 元素在滾動經過它們時是否應該向外動畫
  anchorPlacement: 'top-bottom', // 定義元素相對於視窗的哪個位置應該觸發動畫

});
```

### 2. 使用 `data-aos` 屬性設定動畫：

```html
  <div data-aos="fade-in"></div>
```

並使用 `data-aos-*` 屬性調整行為：
```html
  <div
    data-aos="fade-up"
    data-aos-offset="200"
    data-aos-delay="50"
    data-aos-duration="1000"
    data-aos-easing="ease-in-out"
    data-aos-mirror="true"
    data-aos-once="false"
    data-aos-anchor-placement="top-center"
  >
  </div>
```

[查看所有動畫、緩和效果和錨點(Anchor)位置的完整列表](https://github.com/michalsnik/aos#animations)

#### 錨點(Anchor)

還有一個設定只能在每個元素的基礎上使用：
* `data-aos-anchor` - 將使用其偏移量來觸發動畫，而不是實際元素。

範例：
```html
<div data-aos="fade-up" data-aos-anchor=".other-element"></div>
```

這樣，您就可以在滾動到另一個元素時，在一個元素上觸發動畫 - 這在為固定元素製作動畫時很有用。

---

## API

AOS 物件作為一個全域變數公開，目前有三個方法可用：

  * `init` - 初始化 AOS
  * `refresh` - 重新計算所有元素的偏移量和位置（在視窗調整大小時調用）
  * `refreshHard` - 重新初始化包含 AOS 元素的陣列並觸發 `refresh`（在與 `aos` 元素相關的 DOM 變更時調用）

範例執行：
```javascript
  AOS.refresh();
```

預設情況下，AOS 會監控 DOM 變更，如果存在任何新的元素異步載入或從 DOM 中刪除任何內容，它會自動調用 `refreshHard`。在不支持 `MutationObserver` 的瀏覽器（如 IE）中，您可能需要自己調用 `AOS.refreshHard()`。

`refresh` 方法在視窗調整大小等情況下被調用，因為它不需要建立包含 AOS 元素的新存儲，並且應該盡可能輕量級。

---

## JS 事件

AOS 在文檔上發送兩個事件：`aos:in` 和 `aos:out`，每當任何元素動畫進出時，以便您可以在 JS 中執行額外的操作：
```js
document.addEventListener('aos:in', ({ detail }) => {
  console.log('animated in', detail);
});

document.addEventListener('aos:out', ({ detail }) => {
  console.log('animated out', detail);
});
```

您也可以告訴 AOS 在特定元素上觸發自訂事件，方法是設定 `data-aos-id` 屬性：
```html
<div data-aos="fade-in" data-aos-id="super-duper"></div>
```

然後，您將能夠監聽兩個自訂事件：
- `aos:in:super-duper`
- `aos:out:super-duper`

---

## Recipes:

#### 添加自訂動畫:
有時內建動畫不夠用。假設您需要一個框根據解析度具有不同的動畫。
以下是如何做到這一點：

```css
[data-aos="new-animation"] {
  opacity: 0;
  transition-property: transform, opacity;

  &.aos-animate {
    opacity: 1;
  }

  @media screen and (min-width: 768px) {
    transform: translateX(100px);

    &.aos-animate {
      transform: translateX(0);
    }
  }
}
```
然後在 HTML 中使用它：
```html
<div data-aos="new-animation"></div>
```
該元素只會在行動裝置上對不透明度進行動畫處理，但從 768px 寬度開始，它也會從右向左滑動。

#### 添加自訂緩和效果：
與動畫類似，您可以添加自訂緩和效果：
```css
[data-aos] {
  body[data-aos-easing="new-easing"] &,
  &[data-aos][data-aos-easing="new-easing"] {
    transition-timing-function: cubic-bezier(.250, .250, .750, .750);
  }
}
```

#### 自訂預設動畫距離
內建動畫的預設距離為 100px。只要您使用 SCSS，就可以覆蓋它：
```css
$aos-distance: 200px; // 它必須在導入之前
@import 'node_modules/aos/src/sass/aos.scss';
```
但是，您必須先配置您的建置流程以允許它從 `node_modules` 導入樣式。

#### 整合外部 CSS 動畫庫（例如 Animate.css）：
使用 `animatedClassName` 來更改 AOS 的預設行為，以便在滾動時應用放置在 `data-aos` 中的類別名稱。

```html
<div data-aos="fadeInUp"></div>
```

```js
AOS.init({
  useClassNames: true,
  initClassName: false,
  animatedClassName: 'animated',
});
```

上面的元素將獲得兩個類別：`animated` 和 `fadeInUp`。通過使用上面三個設定的不同組合，您應該能夠整合任何外部 CSS 動畫庫。

但是，外部庫不太關心實際動畫之前的動畫狀態。因此，如果您希望這些元素在滾動之前不可見，您可能需要添加類似的樣式：
```css
[data-aos] {
  visibility: hidden;
}
[data-aos].animated {
  visibility: visible;
}
```

---

## 注意事項：

#### 設定：`duration`、`delay`

Duration 和 delay 接受從 50 到 3000 的值，step 為 50 毫秒，這是因為它們由 css 處理，為了不使 css 比它已經存在的更長，我僅實現了一個子集。我相信這些應該涵蓋大多數情況。

如果不是，您可以編寫簡單的 CSS 來添加另一個持續時間，例如：

```css
  body[data-aos-duration='4000'] [data-aos],
  [data-aos][data-aos][data-aos-duration='4000'] {
    transition-duration: 4000ms;
  }
```
此程式碼將添加 4000 毫秒的持續時間，您可以將其設定在 AOS 元素上，或在初始化 AOS script 時將其設定為全域持續時間。
請注意雙 `[data-aos][data-aos]` - 這不是錯誤，它是一個技巧，可以使個別設定比全域設定更重要，而無需在其中寫入難看的 "!important" :)

範例用法：
```html
  <div data-aos="fade-in" data-aos-duration="4000"></div>
```

---

## 預定義選項

### 動畫(Animations)

  * 淡入動畫：
    * fade
    * fade-up
    * fade-down
    * fade-left
    * fade-right
    * fade-up-right
    * fade-up-left
    * fade-down-right
    * fade-down-left

  * 翻轉動畫：
    * flip-up
    * flip-down
    * flip-left
    * flip-right

  * 滑動動畫：
    * slide-up
    * slide-down
    * slide-left
    * slide-right

  * 縮放動畫：
    * zoom-in
    * zoom-in-up
    * zoom-in-down
    * zoom-in-left
    * zoom-in-right
    * zoom-out
    * zoom-out-up
    * zoom-out-down
    * zoom-out-left
    * zoom-out-right

### 錨點(Anchor)位置：

  * top-bottom
  * top-center
  * top-top
  * center-bottom
  * center-center
  * center-top
  * bottom-bottom
  * bottom-center
  * bottom-top

### 緩和(Easing)函數:

  * linear
  * ease
  * ease-in
  * ease-out
  * ease-in-out
  * ease-in-back
  * ease-out-back
  * ease-in-out-back
  * ease-in-sine
  * ease-out-sine
  * ease-in-out-sine
  * ease-in-quad
  * ease-out-quad
  * ease-in-out-quad
  * ease-in-cubic
  * ease-out-cubic
  * ease-in-out-cubic
  * ease-in-quart
  * ease-out-quart
  * ease-in-out-quart

---

## ❔問題

如果您發現錯誤、有問題或有想法，請查看 [AOS 貢獻指南](https://github.com/michalsnik/aos/blob/next/CONTRIBUTING.md) 並隨時創建新的問題。