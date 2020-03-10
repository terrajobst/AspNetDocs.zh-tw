---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
title: 瞭解動作篩選（VB） |Microsoft Docs
author: microsoft
description: 本教學課程的目的是要說明動作篩選準則。 動作篩選準則是可套用至控制器動作或整個控制器的屬性 。
ms.author: riande
ms.date: 10/16/2008
ms.assetid: e83812f2-c53e-4a43-a7c1-d64c59ecf694
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
msc.type: authoredcontent
ms.openlocfilehash: 263658231ccaa7863508c691a3570bc00b9e8039
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601168"
---
# <a name="understanding-action-filters-vb"></a>了解動作篩選 (VB)

由[Microsoft](https://github.com/microsoft)

[下載 PDF](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_VB.pdf)

> 本教學課程的目的是要說明動作篩選準則。 動作篩選準則是一種屬性，可套用至控制器動作或整個控制器--修改動作的執行方式。

## <a name="understanding-action-filters"></a>瞭解動作篩選準則

本教學課程的目的是要說明動作篩選準則。 動作篩選準則是一種屬性，可套用至控制器動作或整個控制器--修改動作的執行方式。 ASP.NET MVC 架構包含數個動作篩選準則：

- OutputCache –此動作篩選準則會在一段指定的時間內快取控制器動作的輸出。
- HandleError –此動作篩選準則會處理控制器動作執行時引發的錯誤。
- 授權–此動作篩選準則可讓您限制對特定使用者或角色的存取。

您也可以建立自己的自訂動作篩選準則。 例如，您可能會想要建立自訂動作篩選準則，以便執行自訂驗證系統。 或者，您可能會想要建立動作篩選準則，以修改控制器動作所傳回的視圖資料。

在本教學課程中，您將瞭解如何從頭開始建立動作篩選準則。 我們會建立記錄動作篩選，將動作處理的不同階段記錄到 Visual Studio 的 [輸出] 視窗。

### <a name="using-an-action-filter"></a>使用動作篩選準則

動作篩選準則是一個屬性。 您可以將大部分的動作篩選準則套用至個別的控制器動作或整個控制器。

例如，[清單 1] 中的資料控制站會公開名為 `Index()` 的動作，以傳回目前的時間。 此動作會使用 [`OutputCache` 動作] 篩選準則裝飾。 此篩選會使動作所傳回的值快取10秒。

**清單1– `Controllers\DataController.vb`**

[!code-vb[Main](understanding-action-filters-vb/samples/sample1.vb)]

如果您藉由在瀏覽器的網址列中輸入 URL/Data/Index，重複叫用 `Index()` 動作，並多次按下 [重新整理] 按鈕，則會看到10秒的相同時間。 `Index()` 動作的輸出會快取10秒（請參閱 [圖 1]）。

[![快取時間](understanding-action-filters-vb/_static/image2.png)](understanding-action-filters-vb/_static/image1.png)

**圖 01**：快取的時間（[按一下以觀看完整大小的影像](understanding-action-filters-vb/_static/image3.png)）

在 [清單 1] 中，單一動作篩選準則– `OutputCache` 動作篩選準則–套用至 `Index()` 方法。 如有需要，您可以將多個動作篩選準則套用至相同的動作。 例如，您可能會想要將 `OutputCache` 和 `HandleError` 動作篩選準則套用至相同的動作。

在 [清單 1] 中，[`OutputCache` 動作] 篩選準則會套用至 [`Index()`] 動作。 您也可以將此屬性套用至 `DataController` 類別本身。 在此情況下，控制器所公開的任何動作所傳回的結果會快取10秒。

### <a name="the-different-types-of-filters"></a>不同類型的篩選準則

ASP.NET MVC 架構支援四種不同類型的篩選準則：

1. 授權篩選–會執行 `IAuthorizationFilter` 屬性。
2. 動作篩選–執行 `IActionFilter` 屬性。
3. 結果篩選–執行 `IResultFilter` 屬性。
4. 例外狀況篩選準則–執行 `IExceptionFilter` 屬性。

篩選器會依照上列循序執行。 例如，授權篩選準則一律會在動作篩選準則之前執行，而例外狀況篩選準則一律會在每個其他類型的篩選器之後執行。

授權篩選器用來執行控制器動作的驗證和授權。 例如，授權篩選準則就是授權篩選準則的範例。

動作篩選包含在控制器動作執行前後執行的邏輯。 例如，您可以使用動作篩選準則來修改控制器動作所傳回的視圖資料。

結果篩選包含在執行視圖結果之前和之後執行的邏輯。 例如，您可能會想要在將視圖轉譯至瀏覽器之前修改視圖結果。

例外狀況篩選是要執行的最後一個篩選準則類型。 您可以使用例外狀況篩選器來處理控制器動作或控制器動作結果所引發的錯誤。 您也可以使用例外狀況篩選來記錄錯誤。

每個不同類型的篩選準則都會以特定循序執行。 如果您想要控制執行相同類型篩選準則的順序，您可以設定篩選的 Order 屬性。

所有動作篩選準則的基類都是 `System.Web.Mvc.FilterAttribute` 類別。 如果您想要實作為特定類型的篩選準則，則需要建立繼承自基底篩選準則類別的類別，並執行一或多個 IAuthorizationFilter、IActionFilter、IResultFilter 或 Setunhandledexceptionfilter 介面。

### <a name="the-base-actionfilterattribute-class"></a>基底 Actionfilterattribut 類別

為了讓您更輕鬆地執行自訂動作篩選準則，ASP.NET MVC 架構包含基底 `ActionFilterAttribute` 類別。 這個類別會同時執行 `IActionFilter` 和 `IResultFilter` 介面，並繼承自 `Filter` 類別。

此處的術語並不完全一致。 就技術上而言，繼承自 Actionfilterattribut 類別的類別同時是動作篩選準則和結果篩選準則。 不過，在鬆散的意義下，word 動作篩選準則是用來參考 ASP.NET MVC 架構中的任何類型篩選。

基底 Actionfilterattribut 類別具有下列可覆寫的方法：

- OnActionExecuting –在執行控制器動作之前，會呼叫這個方法。
- OnActionExecuted –在執行控制器動作之後，會呼叫這個方法。
- OnResultExecuting –在執行控制器動作結果之前，會呼叫這個方法。
- OnResultExecuted –在執行控制器動作結果之後，會呼叫這個方法。

在下一節中，我們將瞭解如何執行這兩種不同的方法。

### <a name="creating-a-log-action-filter"></a>建立記錄動作篩選準則

為了說明您可以如何建立自訂動作篩選準則，我們將建立自訂動作篩選準則，將處理控制器動作的階段記錄到 Visual Studio 的輸出視窗。 我們的 `LogActionFilter` 包含在 [清單 2] 中。

**清單2– `ActionFilters\LogActionFilter.vb`**

[!code-vb[Main](understanding-action-filters-vb/samples/sample2.vb)]

在 [清單 2] 中，`OnActionExecuting()`、`OnActionExecuted()`、`OnResultExecuting()`和 `OnResultExecuted()` 方法全都會呼叫 `Log()` 方法。 方法的名稱和目前的路由資料會傳遞至 `Log()` 方法。 `Log()` 方法會將訊息寫入 Visual Studio 的 [輸出] 視窗（請參閱 [圖 2]）。

[![寫入 Visual Studio 輸出視窗](understanding-action-filters-vb/_static/image5.png)](understanding-action-filters-vb/_static/image4.png)

**圖 02**：寫入 Visual Studio 的輸出視窗（[按一下以查看完整大小的影像](understanding-action-filters-vb/_static/image6.png)）

[清單 3] 中的 Home 控制器說明如何將記錄動作篩選套用至整個控制器類別。 每當叫用 Home 控制器所公開的任何動作時（`Index()` 方法或 `About()` 方法），處理動作的階段就會記錄到 [Visual Studio 輸出] 視窗中。

**清單3– `Controllers\HomeController.vb`**

[!code-vb[Main](understanding-action-filters-vb/samples/sample3.vb)]

### <a name="summary"></a>總結

在本教學課程中，您已引進 ASP.NET MVC 動作篩選器。 您已瞭解四種不同類型的篩選準則：授權篩選準則、動作篩選準則、結果篩選準則和例外狀況篩選器。 您也已瞭解基底 `ActionFilterAttribute` 類別的相關資訊。

最後，您已瞭解如何執行簡單的動作篩選準則。 我們已建立記錄動作篩選器，將處理控制器動作的階段記錄到 Visual Studio 的輸出視窗。

> [!div class="step-by-step"]
> [上一頁](asp-net-mvc-routing-overview-vb.md)
> [下一頁](improving-performance-with-output-caching-vb.md)
