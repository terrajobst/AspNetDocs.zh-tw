---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
title: ASP.NET MVC 控制器總覽（VB） |Microsoft Docs
author: StephenWalther
description: 在本教學課程中，Stephen Walther 會介紹如何 ASP.NET MVC 控制器。 您將瞭解如何建立新的控制器，並傳回不同類型的動作 res 。
ms.author: riande
ms.date: 02/16/2008
ms.assetid: 94c3e5d9-a904-445e-a34e-d92fd1ca108a
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: f19e7dd7fc025de2e0c387db898d36623e790e6a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601560"
---
# <a name="aspnet-mvc-controller-overview-vb"></a>ASP.NET MVC 控制器概觀 (VB)

依[Stephen Walther](https://github.com/StephenWalther)

> 在本教學課程中，Stephen Walther 會介紹如何 ASP.NET MVC 控制器。 您將瞭解如何建立新的控制器，並傳回不同類型的動作結果。

本教學課程會探索 ASP.NET MVC 控制器、控制器動作和動作結果的主題。 完成本教學課程之後，您將瞭解如何使用控制器來控制造訪者與 ASP.NET MVC 網站互動的方式。

## <a name="understanding-controllers"></a>瞭解控制器

MVC 控制器負責回應對 ASP.NET MVC 網站提出的要求。 每個瀏覽器要求都會對應到特定的控制器。 例如，假設您在瀏覽器的網址列中輸入下列 URL：

`http://localhost/Product/Index/3`

在此情況下，會叫用名為 ProductController 的控制器。 ProductController 會負責產生瀏覽器要求的回應。 例如，控制器可能會將特定的視圖傳回給瀏覽器，或控制器可能會將使用者重新導向至另一個控制器。

[清單 1] 包含名為 ProductController 的簡單控制器。

**Listing1 - Controllers\ProductController.vb**

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample1.vb)]

如 [清單 1] 所示，控制器只是一個類別（一個 Visual Basic 的 .NET 或C#類別）。 「控制器」（controller）是衍生自基底 System.web. Controller 類別的類別。 由於控制器繼承自這個基類，因此控制器會繼承數個有用的方法（我們稍後會討論這些方法）。

## <a name="understanding-controller-actions"></a>瞭解控制器動作

控制器會公開控制器動作。 動作是控制器上的方法，當您在瀏覽器的網址列中輸入特定 URL 時，會呼叫此方法。 例如，假設您提出下列 URL 的要求：

`http://localhost/Product/Index/3`

在此情況下，會在 ProductController 類別上呼叫 Index （）方法。 Index （）方法是控制器動作的範例。

控制器動作必須是控制器類別的公用方法。 根據預設，Visual Basic.NET 方法是公用方法。 請注意，您新增至控制器類別的任何公用方法都會自動公開為控制器動作（您必須特別小心，因為只要在瀏覽器網址列中輸入正確的 URL，就可以讓 universe 中的任何人叫用控制器動作）。

控制器動作必須滿足一些額外的需求。 做為控制器動作使用的方法無法多載。 此外，控制器動作不可以是靜態方法。 另一方面，您可以使用任何方法做為控制器動作。

## <a name="understanding-action-results"></a>瞭解動作結果

控制器動作會傳回稱為*動作結果*的內容。 動作結果是控制器動作為了回應瀏覽器要求所傳回的內容。

ASP.NET MVC 架構支援數種類型的動作結果，包括：

1. ViewResult-表示 HTML 和標記。
2. EmptyResult-不代表任何結果。
3. RedirectResult-代表重新導向至新的 URL。
4. JsonResult-代表可在 AJAX 應用程式中使用的 JavaScript 物件標記法結果。
5. JavaScriptResult-代表 JavaScript 腳本。
6. ContentResult-代表文字結果。
7. FileContentResult-代表可下載的檔案（包含二進位內容）。
8. FilePathResult-代表可下載的檔案（具有路徑）。
9. FileStreamResult-代表可下載的檔案（含檔案資料流程）。

所有這些動作結果都是繼承自基底 ActionResult 類別。

在大部分情況下，控制器動作會傳回 ViewResult。 例如，[清單 2] 中的索引控制器動作會傳回 ViewResult。

**清單 2-Controllers\BookController.vb**

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample2.vb)]

當動作傳回 ViewResult 時，會將 HTML 傳回到瀏覽器。 [清單 2] 中的 Index （）方法會將名為 Index 的視圖傳回給瀏覽器。

請注意，[清單 2] 中的 Index （）動作並不會傳回 ViewResult （）。 相反地，會呼叫控制器基類的 View （）方法。 一般來說，您不會直接傳回動作結果。 相反地，您會呼叫控制器基類的下列其中一個方法：

1. View-傳回 ViewResult 動作結果。
2. 重新導向-傳回 RedirectResult 動作結果。
3. RedirectToAction-傳回 RedirectToRouteResult 動作結果。
4. RedirectToRoute-傳回 RedirectToRouteResult 動作結果。
5. Json-傳回 JsonResult 動作結果。
6. JavaScriptResult-傳回 JavaScriptResult。
7. Content-傳回 ContentResult 動作結果。
8. File-根據傳遞至方法的參數，傳回 FileContentResult、FilePathResult 或 FileStreamResult。

因此，如果您想要將視圖傳回給瀏覽器，請呼叫 View （）方法。 如果您想要將使用者從一個控制器動作重新導向到另一個，您可以呼叫 RedirectToAction （）方法。 例如，[清單 3] 中的 [詳細資料] （）動作會顯示一個視圖，或將使用者重新導向至 [索引] （）動作，這取決於識別碼參數是否具有值。

**清單 3-CustomerController .vb**

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample3.vb)]

ContentResult 動作結果是特殊的。 您可以使用 ContentResult 動作結果，以純文字傳回動作結果。 例如，[清單 4] 中的 Index （）方法會傳回純文字格式的訊息，而不是 HTML。

**清單 4-Controllers\StatusController.vb**

> StatusController
> 
> 
> System.web. Mvc. 控制器

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample4.vb)]

叫用 StatusController （）動作時，不會傳回 view。 相反地，原始文字 "Hello World！" 會傳回至瀏覽器。

如果控制器動作傳回的結果不是動作結果，例如日期或整數，則會自動將結果包裝在 ContentResult 中。 例如，當叫用清單5中 WorkController 的 Index （）動作時，會自動以 ContentResult 的形式傳回日期。

**清單 5-WorkController .vb**

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample5.vb)]

[清單 5] 中的 Index （）動作會傳回 DateTime 物件。 ASP.NET MVC 架構會將 DateTime 物件轉換成字串，並自動將 DateTime 值包裝在 ContentResult 中。 瀏覽器會以純文字的形式接收日期和時間。

## <a name="summary"></a>總結

本教學課程的目的是要為您介紹 ASP.NET MVC 控制器、控制器動作和控制器動作結果的概念。 在第一節中，您已瞭解如何將新的控制器新增至 ASP.NET MVC 專案。 接下來，您已瞭解如何將控制器的公用方法公開至 universe 做為控制器動作。 最後，我們討論了可從控制器動作傳回的不同類型動作結果。 特別是，我們討論了如何從控制器動作傳回 ViewResult、RedirectToActionResult 和 ContentResult。

> [!div class="step-by-step"]
> [上一頁](creating-a-custom-route-constraint-cs.md)
> [下一頁](creating-custom-routes-vb.md)
