---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
title: 將動態內容新增至快取的C#頁面（） |Microsoft Docs
author: microsoft
description: 瞭解如何在相同頁面中混合動態和快取的內容。 快取後的替代功能可讓您顯示動態內容，例如橫幅廣告 o 。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 2ddd4407-d143-4a94-877c-21771bfb97a6
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
msc.type: authoredcontent
ms.openlocfilehash: be43712d3dd5235117558e991d9dd71aa30ec470
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601581"
---
# <a name="adding-dynamic-content-to-a-cached-page-c"></a>將動態內容新增至快取的頁面 (C#)

由[Microsoft](https://github.com/microsoft)

> 瞭解如何在相同頁面中混合動態和快取的內容。 快取後的替代功能可讓您在已快取輸出的頁面中顯示動態內容，例如橫幅廣告或新聞專案。

藉由利用輸出快取，您可以大幅提升 ASP.NET MVC 應用程式的效能。 每次要求頁面時，不需要重新產生頁面，而是會產生一次頁面，並快取到記憶體中供多位使用者使用。

但還是有問題。 如果您需要在頁面中顯示動態內容，該怎麼做？ 例如，假設您想要在頁面中顯示橫幅廣告。 您不想要快取橫幅廣告，讓每位使用者都看到相同的廣告。 您不需要任何錢就能完成！

幸運的是，有一個簡單的解決方案。 您可以利用 ASP.NET 架構的一項功能，稱為*後置*快取替代。 快取後的替代功能可讓您替代已在記憶體中快取的頁面中的動態內容。

一般來說，當您使用 [OutputCache] 屬性來輸出快取頁面時，會在伺服器和用戶端（網頁瀏覽器）上快取頁面。 當您使用快取後的替換時，只會在伺服器上快取頁面。

#### <a name="using-post-cache-substitution"></a>使用快取後的替代

使用快取後的替代需要兩個步驟。 首先，您必須定義方法來傳回字串，表示您想要在快取頁面中顯示的動態內容。 接下來，您會呼叫 HttpResponse. WriteSubstitution （）方法，將動態內容插入頁面中。

例如，假設您想要在快取的頁面中隨機顯示不同的新聞專案。 [清單 1] 中的類別會公開名為 RenderNews （）的單一方法，它會從三個新聞專案的清單隨機傳回一個新聞專案。

**清單1– Models\News.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample1.cs)]

若要利用快取後的替代，請呼叫 HttpResponse. WriteSubstitution （）方法。 WriteSubstitution （）方法會設定程式碼，以動態內容取代快取頁面的區域。 WriteSubstitution （）方法是用來在 [清單 2] 的視圖中顯示隨機新聞專案。

**清單2– Views\Home\Index.aspx**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample2.aspx)]

RenderNews 方法會傳遞至 WriteSubstitution （）方法。 請注意，不會呼叫 RenderNews 方法（沒有括弧）。 相反地，會將方法的參考傳遞給 WriteSubstitution （）。

索引視圖會被快取。 [清單 3] 中的控制器會傳回此視圖。 請注意，Index （）動作是以 [OutputCache] 屬性裝飾，這會導致索引視圖快取60秒。

**清單3– Controllers\HomeController.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample3.cs)]

即使快取索引視圖，當您要求 [索引] 頁面時，也會顯示不同的隨機新聞專案。 當您要求 [索引] 頁面時，頁面所顯示的時間不會變更60秒（請參閱 [圖 1]）。 但時間不會改變，而是會證明頁面已快取。 不過，WriteSubstitution （）方法插入的內容（隨機新聞專案），會隨著每個要求而變更。

**圖1–在快取的頁面中插入動態新聞專案**

![clip_image002](adding-dynamic-content-to-a-cached-page-cs/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a>在 Helper 方法中使用後置快取替代

更簡單的方法是利用快取後的替代方式，在自訂 helper 方法內封裝對 WriteSubstitution （）方法的呼叫。 這種方法是由 [清單 4] 中的 helper 方法來說明。

**清單4– AdHelper.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample4.cs)]

[清單 4] 包含一個會公開兩個方法的靜態類別： RenderBanner （）和 RenderBannerInternal （）。 RenderBanner （）方法代表實際的 helper 方法。 這個方法會擴充標準的 ASP.NET MVC HtmlHelper 類別，讓您可以在視圖中呼叫 RenderBanner （），就像任何其他 helper 方法一樣。

RenderBanner （）方法會呼叫 HttpResponse. WriteSubstitution （）方法，並將 RenderBannerInternal （）方法傳遞至 WriteSubstitution （）方法。

RenderBannerInternal （）方法是私用方法。 這個方法不會公開為 helper 方法。 RenderBannerInternal （）方法會從三個橫幅廣告影像的清單中隨機傳回一個橫幅廣告影像。

[清單 5] 中修改過的索引視圖會說明如何使用 RenderBanner （） helper 方法。 請注意，在此視圖頂端會包含額外的 &lt;% @ Import%&gt; 指示詞，以匯入 MvcApplication1. helper 命名空間。 如果您不想匯入此命名空間，則 RenderBanner （）方法不會顯示為 Html 屬性上的方法。

**清單5– Views\Home\Index.aspx （使用 RenderBanner （）方法）**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample5.aspx)]

當您要求清單5中的視圖所呈現的頁面時，每個要求都會顯示不同的橫幅廣告（請參閱 [圖 2]）。 會快取頁面，但 RenderBanner （） helper 方法會動態插入橫幅廣告。

**圖2–顯示隨機橫幅廣告的索引視圖**

![clip_image004](adding-dynamic-content-to-a-cached-page-cs/_static/image2.jpg)

#### <a name="summary"></a>總結

本教學課程說明如何動態更新快取頁面中的內容。 您已瞭解如何使用 HttpResponse. WriteSubstitution （）方法，讓動態內容插入快取的頁面中。 您也已瞭解如何在 HTML helper 方法內封裝對 WriteSubstitution （）方法的呼叫。

盡可能利用快取，這可能會對 web 應用程式的效能產生顯著的影響。 如本教學課程中所述，即使您需要在頁面中顯示動態內容，您也可以利用快取。

> [!div class="step-by-step"]
> [上一頁](improving-performance-with-output-caching-cs.md)
> [下一頁](creating-a-controller-cs.md)
