[AOS - Animate on scroll library](http://michalsnik.github.io/aos/)

版本：2.3.4

[![NPM version](https://img.shields.io/npm/v/aos.svg?style=flat)](https://npmjs.org/package/aos)
[![NPM downloads](https://img.shields.io/npm/dm/aos.svg?style=flat)](https://npmjs.org/package/aos)
[![Build Status](https://travis-ci.org/michalsnik/aos.svg?branch=master)](https://travis-ci.org/michalsnik/aos)
[![Gitter](https://badges.gitter.im/michalsnik/aos.svg)](https://gitter.im/michalsnik/aos?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

[![Twitter Follow](https://img.shields.io/twitter/follow/michalsnik.svg?style=social)](https://twitter.com/michalsnik) [![Twitter URL](https://img.shields.io/twitter/url/http/shields.io.svg?style=social)](https://twitter.com/home?status=AOS%20-%20Animate%20on%20Scroll%20library%0Ahttps%3A//github.com/michalsnik/aos)

一個小型的函式庫(library)，用於在您捲動頁面時為元素添加動畫。

您可能會說它類似於 WOWJS，是的，您說得對，效果與 WOWJS 相似，但我對如何製作這樣的外掛有不同的想法，所以就有了這個。一個由 CSS3 驅動的捲軸動畫函式庫(library)。

AOS 允許您在向下捲動和向上捲動時為元素添加動畫。
如果您捲動回頁面頂端，元素將會動畫到其先前的狀態，並且如果您向下捲動，則可以再次添加動畫。

👉 為了更好地理解這實際上是如何運作的，我建議您查看 [我在 CSS-tricks 上的文章](https://css-tricks.com/aos-css-driven-scroll-animation-library/).

---

### 🚀 [Demo](http://michalsnik.github.io/aos/)

### 🌟 Codepen Examples
- [不同的內建動畫](http://codepen.io/michalsnik/pen/WxNdvq)
- [使用錨點(anchor)](http://codepen.io/michalsnik/pen/jrOYVO)
- [使用錨點(anchor)放置和不同的緩動(easing)](http://codepen.io/michalsnik/pen/EyxoNm)
- [使用簡單的自訂動畫](http://codepen.io/michalsnik/pen/WxvNvE)

---

## ❗ 注意
從版本 `2.0.0` 開始，不再支援 `aos` 屬性，請始終使用 `data-aos`。

## ⚙ 設定

### 安裝 AOS

- 使用 `bower`

    ```bash
      bower install aos --save
    ```

- 使用 `npm`

    ```bash
      npm install aos --save
    ```

- 直接下載 -> [點擊這裡](https://github.com/michalsnik/aos/archive/master.zip)


### 連結樣式

```html
  <link rel="stylesheet" href="bower_components/aos/dist/aos.css" />
```

### 添加 scripts

```html
  <script src="bower_components/aos/dist/aos.js"></script>
```

AOS from version `1.2.0` is available as UMD module, so you can use it as AMD, Global, Node or ES6 module.
從版本 `1.2.0` 開始，AOS 可作為 UMD 模組，因此您可以將其用作 AMD、全域、節點或 ES6 模組。

### 初始化 AOS

```javascript
  <script>
    AOS.init();
  </script>
```

## 🤔 如何使用它?

### 基本用法

  您只需要將 `data-aos` 屬性添加到 HTML 元素，如下所示：

```html
  <div data-aos="animation_name">
```

  如果您捲動到此元素，Script 將會觸發此元素上的 "animation_name" 動畫。

  [在下方](https://github.com/michalsnik/aos#-animations) 是目前所有可用動畫的清單 :)

### 🔥 進階設定

這些設定可以在特定元素上設定，也可以在初始化腳本(script)時作為預設設定（在沒有 `data-` 部分的選項物件中）。

| 屬性(Attribute) | 描述 | Example value | 預設值 |
|---------------------------|-------------|---------------|---------|
| *`data-aos-offset`* | 變更偏移量以更早或更晚觸發動畫 (px) | 200 | 120 |
| *`data-aos-duration`* | *動畫持續時間 (ms) | 600 | 400 |
| *`data-aos-easing`* | 選擇時間函數以不同的方式緩動元素 | ease-in-sine | ease |
| *`data-aos-delay`* | 延遲動畫 (ms) | 300 | 0 |
| *`data-aos-anchor`* | 錨點(Anchor)元素，其偏移量將被計算以觸發動畫，而不是實際元素的偏移量 | #selector | null |
| *`data-aos-anchor-placement`* | 錨點(Anchor)放置 - 螢幕上元素的哪個位置應該觸發動畫 | top-center | top-bottom |
| *`data-aos-once`* | 選擇動畫是否應該觸發一次，或者每次您向上/向下捲動到元素時都觸發 | true | false |

*持續時間接受從 50 到 3000 的值，step 為 50ms，這是因為動畫的持續時間由 css 處理，為了不讓 css 比它已經有的更長，我僅在這個範圍內創建了實現。我認為這對幾乎所有情況都應該足夠了。

如果不是，您可以在頁面上寫入簡單的 CSS，它將添加另一個可用的持續時間選項值，例如：

```css
  body[data-aos-duration='4000'] [data-aos], [data-aos][data-aos][data-aos-duration='4000']{
    transition-duration: 4000ms;
  }
```

這段程式碼將為您添加 4000ms 的持續時間，您可以將其設定在 AOS 元素上，或者在初始化 AOS script 時將其設定為全域持續時間。

請注意雙重 `[data-aos][data-aos]` - 這不是錯誤，它是一個技巧，讓個別設定比全域設定更重要，而無需在那裡寫入難看的 "!important" :)

`data-aos-anchor-placement` - 您可以在每個元素上設定不同的放置選項，原理非常簡單，每個錨點(anchor)放置選項都包含兩個詞，例如 `top-center`。這意味著當元素的 `top` 抵達視窗的 `center` 時，動畫將會觸發。

`bottom-top` 意味著當元素的 `bottom` 抵達視窗的 `top` 時，動畫將會觸發，依此類推。

在下方您可以找到所有錨點放置選項的清單。

#### 範例:

```html
  <div data-aos="fade-zoom-in" data-aos-offset="200" data-aos-easing="ease-in-sine" data-aos-duration="600">
```
```html
  <div data-aos="flip-left" data-aos-delay="100" data-aos-anchor=".example-selector">
```
```html
  <div data-aos="fade-up" data-aos-anchor-placement="top-center">
```


#### API

AOS 物件作為全域變數公開，目前有三個方法可用：

  * `init` - 初始化 AOS
  * `refresh` - 重新計算所有元素的偏移量和位置（在視窗調整大小時呼叫）
  * `refreshHard` - 使用 AOS 元素重新初始化陣列並觸發 `refresh`（在與 `aos` 元素相關的 DOM 變更時呼叫）

執行範例：
```javascript
  AOS.refresh();
```

預設情況下，AOS 會監控 DOM 變更，如果存在任何新的元素被非同步載入，或者當某些東西從 DOM 中移除時，它會自動呼叫 `refreshHard`。在不支持 `MutationObserver` 的瀏覽器（如 IE）中，您可能需要自己呼叫 `AOS.refreshHard()`。

`refresh` 方法在視窗調整大小時被呼叫，等等，因為它不需要建立新的 AOS 元素儲存，並且應該盡可能輕量。

### 全域設定

如果您不想為每個元素單獨更改設定，您可以全局更改它。

要做到這一點，請將選項物件傳遞給 `init()` 函數，如下所示：

```javascript
  <script>
    AOS.init({
      offset: 200,
      duration: 600,
      easing: 'ease-in-sine',
      delay: 100,
    });
  </script>
```

#### 其他配置

這些設定只能在初始化 AOS 時在選項物件中設定。

| Setting | 描述(Description) | Example value | 預設值 |
|---------------------------|-------------|---------------|---------|
| *`disable`* | Condition when AOS should be disabled | mobile | false |
| *`startEvent`* | Name of event, on which AOS should be initialized | exampleEvent | DOMContentLoaded |

##### 停用(Disabling) AOS

如果您想在特定裝置上或在任何語句下停用(Disabling) AOS，您可以設定 `disable` 選項。如下所示：

```javascript
  <script>
    AOS.init({
      disable: 'mobile'
    });
  </script>
```

您可以使用多種選項來讓 AOS 完美地融入您的專案，您可以傳遞三種裝置類型之一：
`mobile`（手機和平板電腦）、`phone` 或 `tablet`。這將在這些特定裝置上停用(disable) AOS。但是，如果您想建立自己的條件，只需輸入您的語句，而不是裝置類型名稱：

```javascript
  disable: window.innerWidth < 1024
```

您也可以傳遞一個 `function`，它應該在最後回傳 `true` 或 `false`：

```javascript
  disable: function () {
    var maxWidth = 1024;
    return window.innerWidth < maxWidth;
  }
```

##### 開始事件(event)

如果您不想在 `DOMContentLoaded` 事件上初始化 AOS，您可以傳遞您自己的事件名稱並在您想要的時候觸發它。AOS 在 `document` 元素上監聽此事件。

```javascript
  <script>
    AOS.init({
      startEvent: 'someCoolEvent'
    });
  </script>
```

**重要提示：**如果您設定 `startEvent: 'load'`，它將在 `window` 上添加事件監聽器，而不是 `document`。


### 👻 動畫(Animations)

您可以使用多種預定義的動畫：

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

  * 放大縮小動畫：
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

### 錨點(Anchor)放置：
  * top-bottom
  * top-center
  * top-top
  * center-bottom
  * center-center
  * center-top
  * bottom-bottom
  * bottom-center
  * bottom-top


### 緩動(Easing)函數：

您可以選擇其中一個時間函數來為元素添加漂亮的動畫：

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

## ✌️ [貢獻](CONTRIBUTING.md)

## 📝 [變更日誌](CHANGELOG.md)

## ❔問題

如果您有任何問題、想法或其他任何事，請查看 [AOS 貢獻指南](https://github.com/michalsnik/aos/blob/v2/CONTRIBUTING.md) 並隨時建立新的問題。[lang=zh-Hant] 
