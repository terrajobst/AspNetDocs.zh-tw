---
ms.openlocfilehash: 3965884c8e0d7116f5d8a42e6aefb0dc5be94f1e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029655"
---
<a name="open-iconic-v111httpuseiconiccomopen"></a>[<span data-ttu-id="443ae-101">Open Iconic 1.1.1 版</span><span class="sxs-lookup"><span data-stu-id="443ae-101">Open Iconic v1.1.1</span></span>](http://useiconic.com/open)
===========

### <a name="open-iconic-is-the-open-source-sibling-of-iconichttpuseiconiccom-it-is-a-hyper-legible-collection-of-223-icons-with-a-tiny-footprintmdashready-to-use-with-bootstrap-and-foundation-view-the-collectionhttpuseiconiccomopenicons"></a><span data-ttu-id="443ae-102">Open Iconic 是 [Iconic](http://useiconic.com) 的開放原始碼同層級。</span><span class="sxs-lookup"><span data-stu-id="443ae-102">Open Iconic is the open source sibling of [Iconic](http://useiconic.com).</span></span> <span data-ttu-id="443ae-103">它是超高清晰且面積很小的圖示集合，內有 223 個圖示&mdash;可與啟動程序和 Foundation 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="443ae-103">It is a hyper-legible collection of 223 icons with a tiny footprint&mdash;ready to use with Bootstrap and Foundation.</span></span> [<span data-ttu-id="443ae-104">檢視集合</span><span class="sxs-lookup"><span data-stu-id="443ae-104">View the collection</span></span>](http://useiconic.com/open#icons)



## <a name="whats-in-open-iconic"></a><span data-ttu-id="443ae-105">Open Iconic 中有什麼？</span><span class="sxs-lookup"><span data-stu-id="443ae-105">What's in Open Iconic?</span></span>

* <span data-ttu-id="443ae-106">223 個清晰可見的 8 像素圖示</span><span class="sxs-lookup"><span data-stu-id="443ae-106">223 icons designed to be legible down to 8 pixels</span></span>
* <span data-ttu-id="443ae-107">超輕量型 SVG 檔案 - 整個集合 61.8</span><span class="sxs-lookup"><span data-stu-id="443ae-107">Super-light SVG files - 61.8 for the entire set</span></span> 
* <span data-ttu-id="443ae-108">SVG Sprite&mdash;圖示字型的現代取代項</span><span class="sxs-lookup"><span data-stu-id="443ae-108">SVG sprite&mdash;the modern replacement for icon fonts</span></span>
* <span data-ttu-id="443ae-109">Webfont (EOT、OTF、SVG、TTF、WOFF)、PNG 和 WebP 格式</span><span class="sxs-lookup"><span data-stu-id="443ae-109">Webfont (EOT, OTF, SVG, TTF, WOFF), PNG and WebP formats</span></span>
* <span data-ttu-id="443ae-110">CSS、LESS、SCSS 和 Stylus 格式中的 Webfont 樣式表 (包括啟動程序和 Foundation 的版本)</span><span class="sxs-lookup"><span data-stu-id="443ae-110">Webfont stylesheets (including versions for Bootstrap and Foundation) in CSS, LESS, SCSS and Stylus formats</span></span>
* <span data-ttu-id="443ae-111">8 像素、16 像素、24 像素、32 像素、48 像素和 64 像素的 PNG 和 WebP 點陣影像。</span><span class="sxs-lookup"><span data-stu-id="443ae-111">PNG and WebP raster images in 8px, 16px, 24px, 32px, 48px and 64px.</span></span>


## <a name="getting-started"></a><span data-ttu-id="443ae-112">快速入門</span><span class="sxs-lookup"><span data-stu-id="443ae-112">Getting Started</span></span>

#### <a name="for-code-samples-and-everything-else-you-need-to-get-started-with-open-iconic-check-out-our-iconshttpuseiconiccomopenicons-and-referencehttpuseiconiccomopenreference-sections"></a><span data-ttu-id="443ae-113">如需程式碼範例和其他開始使用 Open Iconic 所需的一切，請參閱我們的[圖示](http://useiconic.com/open#icons)和[參考](http://useiconic.com/open#reference)章節。</span><span class="sxs-lookup"><span data-stu-id="443ae-113">For code samples and everything else you need to get started with Open Iconic, check out our [Icons](http://useiconic.com/open#icons) and [Reference](http://useiconic.com/open#reference) sections.</span></span>

### <a name="general-usage"></a><span data-ttu-id="443ae-114">一般使用方式</span><span class="sxs-lookup"><span data-stu-id="443ae-114">General Usage</span></span>

#### <a name="using-open-iconics-svgs"></a><span data-ttu-id="443ae-115">使用 Open Iconic 的 SVG</span><span class="sxs-lookup"><span data-stu-id="443ae-115">Using Open Iconic's SVGs</span></span>

<span data-ttu-id="443ae-116">我們喜歡 SVG，而且認為它們是在 Web 上顯示圖示的方式。</span><span class="sxs-lookup"><span data-stu-id="443ae-116">We like SVGs and we think they're the way to display icons on the web.</span></span> <span data-ttu-id="443ae-117">因為 Open Iconic 只是基本 SVG，所以建議您就像顯示任何其他映像一樣顯示它們 (別忘了 `alt` 屬性)。</span><span class="sxs-lookup"><span data-stu-id="443ae-117">Since Open Iconic are just basic SVGs, we suggest you display them like you would any other image (don't forget the `alt` attribute).</span></span>

```
<img src="/open-iconic/svg/icon-name.svg" alt="icon name">
```

#### <a name="using-open-iconics-svg-sprite"></a><span data-ttu-id="443ae-118">使用 Open Iconic 的 SVG Sprite</span><span class="sxs-lookup"><span data-stu-id="443ae-118">Using Open Iconic's SVG Sprite</span></span>

<span data-ttu-id="443ae-119">Open Iconic 也附有一個 SVG Sprite，可讓您只需一個請求即可顯示集合中的所有圖示。</span><span class="sxs-lookup"><span data-stu-id="443ae-119">Open Iconic also comes in a SVG sprite which allows you to display all the icons in the set with a single request.</span></span> <span data-ttu-id="443ae-120">它就像圖示字型一樣，不需破解。</span><span class="sxs-lookup"><span data-stu-id="443ae-120">It's like an icon font, without being a hack.</span></span>

<span data-ttu-id="443ae-121">從 SVG Sprite 新增圖示與您先前使用的方式略有不同，但仍是輕而易舉。</span><span class="sxs-lookup"><span data-stu-id="443ae-121">Adding an icon from an SVG sprite is a little different than what you're used to, but it's still a piece of cake.</span></span> <span data-ttu-id="443ae-122">*秘訣：若要讓圖示能夠輕鬆建立樣式，建議您將一般類別新增至*  `<svg>` *標籤，並對* `<use>`  *標籤中的每個不同圖示新增唯一類別名稱。*</span><span class="sxs-lookup"><span data-stu-id="443ae-122">*Tip: To make your icons easily style able, we suggest adding a general class to the* `<svg>` *tag and a unique class name for each different icon in the* `<use>` *tag.*</span></span>  

```
<svg class="icon">
  <use xlink:href="open-iconic.svg#account-login" class="icon-account-login"></use>
</svg>
```

<span data-ttu-id="443ae-123">調整圖示大小只需要基本 CSS。</span><span class="sxs-lookup"><span data-stu-id="443ae-123">Sizing icons only needs basic CSS.</span></span> <span data-ttu-id="443ae-124">所有圖示都採用方形格式，因此只需設定等寬和等高的 `<svg>` 標籤即可。</span><span class="sxs-lookup"><span data-stu-id="443ae-124">All the icons are in a square format, so just set the `<svg>` tag with equal width and height dimensions.</span></span>

```
.icon {
  width: 16px;
  height: 16px;
}
```

<span data-ttu-id="443ae-125">著色圖示甚至更簡單。</span><span class="sxs-lookup"><span data-stu-id="443ae-125">Coloring icons is even easier.</span></span> <span data-ttu-id="443ae-126">您只需在 `<use>` 標籤上設定 `fill` 規則。</span><span class="sxs-lookup"><span data-stu-id="443ae-126">All you need to do is set the `fill` rule on the `<use>` tag.</span></span>

```
.icon-account-login {
  fill: #f00;
}
```

<span data-ttu-id="443ae-127">若要深入了解 SVG Sprite，請閱讀 [Chris Coyier 指南](http://css-tricks.com/svg-sprites-use-better-icon-fonts/)。</span><span class="sxs-lookup"><span data-stu-id="443ae-127">To learn more about SVG Sprites, read [Chris Coyier's guide](http://css-tricks.com/svg-sprites-use-better-icon-fonts/).</span></span>

#### <a name="using-open-iconics-icon-font"></a><span data-ttu-id="443ae-128">使用 Open Iconic 的圖示字型...</span><span class="sxs-lookup"><span data-stu-id="443ae-128">Using Open Iconic's Icon Font...</span></span>


##### <a name="with-bootstrap"></a><span data-ttu-id="443ae-129">…搭配啟動程序</span><span class="sxs-lookup"><span data-stu-id="443ae-129">…with Bootstrap</span></span>

<span data-ttu-id="443ae-130">您可以在 `font/css/open-iconic-bootstrap.{css, less, scss, styl}` 找到我們的啟動程序樣式表</span><span class="sxs-lookup"><span data-stu-id="443ae-130">You can find our Bootstrap stylesheets in `font/css/open-iconic-bootstrap.{css, less, scss, styl}`</span></span>


```
<link href="/open-iconic/font/css/open-iconic-bootstrap.css" rel="stylesheet">
```


```
<span class="oi oi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="with-foundation"></a><span data-ttu-id="443ae-131">…搭配 Foundation</span><span class="sxs-lookup"><span data-stu-id="443ae-131">…with Foundation</span></span>

<span data-ttu-id="443ae-132">您可以在 `font/css/open-iconic-foundation.{css, less, scss, styl}` 找到我們的 Foundation 樣式表</span><span class="sxs-lookup"><span data-stu-id="443ae-132">You can find our Foundation stylesheets in `font/css/open-iconic-foundation.{css, less, scss, styl}`</span></span>

```
<link href="/open-iconic/font/css/open-iconic-foundation.css" rel="stylesheet">
```


```
<span class="fi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="on-its-own"></a><span data-ttu-id="443ae-133">…本身</span><span class="sxs-lookup"><span data-stu-id="443ae-133">…on its own</span></span>

<span data-ttu-id="443ae-134">您可以在 `font/css/open-iconic.{css, less, scss, styl}` 找到我們的預設樣式表</span><span class="sxs-lookup"><span data-stu-id="443ae-134">You can find our default stylesheets in `font/css/open-iconic.{css, less, scss, styl}`</span></span>

```
<link href="/open-iconic/font/css/open-iconic.css" rel="stylesheet">
```

```
<span class="oi" data-glyph="icon-name" title="icon name" aria-hidden="true"></span>
```


## <a name="license"></a><span data-ttu-id="443ae-135">使用權</span><span class="sxs-lookup"><span data-stu-id="443ae-135">License</span></span>

### <a name="icons"></a><span data-ttu-id="443ae-136">圖示</span><span class="sxs-lookup"><span data-stu-id="443ae-136">Icons</span></span>

<span data-ttu-id="443ae-137">所有程式碼 (包括 SVG 標記) 是在 [MIT 授權](http://opensource.org/licenses/MIT) 之下。</span><span class="sxs-lookup"><span data-stu-id="443ae-137">All code (including SVG markup) is under the [MIT License](http://opensource.org/licenses/MIT).</span></span>

### <a name="fonts"></a><span data-ttu-id="443ae-138">字型</span><span class="sxs-lookup"><span data-stu-id="443ae-138">Fonts</span></span>

<span data-ttu-id="443ae-139">所有字型是在 [SIL 授權](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web) 之下。</span><span class="sxs-lookup"><span data-stu-id="443ae-139">All fonts are under the [SIL Licensed](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web).</span></span>
