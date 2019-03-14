---
ms.openlocfilehash: 3965884c8e0d7116f5d8a42e6aefb0dc5be94f1e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57054215"
---
<a name="open-iconic-v111httpuseiconiccomopen"></a>[Open Iconic 1.1.1 版](http://useiconic.com/open)
===========

### <a name="open-iconic-is-the-open-source-sibling-of-iconichttpuseiconiccom-it-is-a-hyper-legible-collection-of-223-icons-with-a-tiny-footprintmdashready-to-use-with-bootstrap-and-foundation-view-the-collectionhttpuseiconiccomopenicons"></a>Open Iconic 是 [Iconic](http://useiconic.com) 的開放原始碼同層級。 它是超高清晰且面積很小的圖示集合，內有 223 個圖示&mdash;可與啟動程序和 Foundation 搭配使用。 [檢視集合](http://useiconic.com/open#icons)



## <a name="whats-in-open-iconic"></a>Open Iconic 中有什麼？

* 223 個清晰可見的 8 像素圖示
* 超輕量型 SVG 檔案 - 整個集合 61.8 
* SVG Sprite&mdash;圖示字型的現代取代項
* Webfont (EOT、OTF、SVG、TTF、WOFF)、PNG 和 WebP 格式
* CSS、LESS、SCSS 和 Stylus 格式中的 Webfont 樣式表 (包括啟動程序和 Foundation 的版本)
* 8 像素、16 像素、24 像素、32 像素、48 像素和 64 像素的 PNG 和 WebP 點陣影像。


## <a name="getting-started"></a>快速入門

#### <a name="for-code-samples-and-everything-else-you-need-to-get-started-with-open-iconic-check-out-our-iconshttpuseiconiccomopenicons-and-referencehttpuseiconiccomopenreference-sections"></a>如需程式碼範例和其他開始使用 Open Iconic 所需的一切，請參閱我們的[圖示](http://useiconic.com/open#icons)和[參考](http://useiconic.com/open#reference)章節。

### <a name="general-usage"></a>一般使用方式

#### <a name="using-open-iconics-svgs"></a>使用 Open Iconic 的 SVG

我們喜歡 SVG，而且認為它們是在 Web 上顯示圖示的方式。 因為 Open Iconic 只是基本 SVG，所以建議您就像顯示任何其他映像一樣顯示它們 (別忘了 `alt` 屬性)。

```
<img src="/open-iconic/svg/icon-name.svg" alt="icon name">
```

#### <a name="using-open-iconics-svg-sprite"></a>使用 Open Iconic 的 SVG Sprite

Open Iconic 也附有一個 SVG Sprite，可讓您只需一個請求即可顯示集合中的所有圖示。 它就像圖示字型一樣，不需破解。

從 SVG Sprite 新增圖示與您先前使用的方式略有不同，但仍是輕而易舉。 *秘訣：若要讓圖示能夠輕鬆建立樣式，建議您將一般類別新增至*  `<svg>` *標籤，並對* `<use>`  *標籤中的每個不同圖示新增唯一類別名稱。*  

```
<svg class="icon">
  <use xlink:href="open-iconic.svg#account-login" class="icon-account-login"></use>
</svg>
```

調整圖示大小只需要基本 CSS。 所有圖示都採用方形格式，因此只需設定等寬和等高的 `<svg>` 標籤即可。

```
.icon {
  width: 16px;
  height: 16px;
}
```

著色圖示甚至更簡單。 您只需在 `<use>` 標籤上設定 `fill` 規則。

```
.icon-account-login {
  fill: #f00;
}
```

若要深入了解 SVG Sprite，請閱讀 [Chris Coyier 指南](http://css-tricks.com/svg-sprites-use-better-icon-fonts/)。

#### <a name="using-open-iconics-icon-font"></a>使用 Open Iconic 的圖示字型...


##### <a name="with-bootstrap"></a>…搭配啟動程序

您可以在 `font/css/open-iconic-bootstrap.{css, less, scss, styl}` 找到我們的啟動程序樣式表


```
<link href="/open-iconic/font/css/open-iconic-bootstrap.css" rel="stylesheet">
```


```
<span class="oi oi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="with-foundation"></a>…搭配 Foundation

您可以在 `font/css/open-iconic-foundation.{css, less, scss, styl}` 找到我們的 Foundation 樣式表

```
<link href="/open-iconic/font/css/open-iconic-foundation.css" rel="stylesheet">
```


```
<span class="fi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="on-its-own"></a>…本身

您可以在 `font/css/open-iconic.{css, less, scss, styl}` 找到我們的預設樣式表

```
<link href="/open-iconic/font/css/open-iconic.css" rel="stylesheet">
```

```
<span class="oi" data-glyph="icon-name" title="icon name" aria-hidden="true"></span>
```


## <a name="license"></a>使用權

### <a name="icons"></a>圖示

所有程式碼 (包括 SVG 標記) 是在 [MIT 授權](http://opensource.org/licenses/MIT) 之下。

### <a name="fonts"></a>字型

所有字型是在 [SIL 授權](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web) 之下。
