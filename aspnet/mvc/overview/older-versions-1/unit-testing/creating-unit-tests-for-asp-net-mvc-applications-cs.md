---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
title: 建立 ASP.NET MVC 應用程式的單元測試C#（） |Microsoft Docs
author: StephenWalther
description: 瞭解如何建立控制器動作的單元測試。 在本教學課程中，Stephen Walther 示範如何測試控制器動作是否會傳回 parti 。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: d3a270b9-d7b1-47f2-8775-fc3beb518b5c
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
msc.type: authoredcontent
ms.openlocfilehash: 35fd0d85c63e5bd196394ce11b851c822a6405d9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623939"
---
# <a name="creating-unit-tests-for-aspnet-mvc-applications-c"></a>建立 ASP.NET MVC 應用程式的單元測試 (C#)

依[Stephen Walther](https://github.com/StephenWalther)

[下載 PDF](https://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_CS.pdf)

> 瞭解如何建立控制器動作的單元測試。 在本教學課程中，Stephen Walther 示範如何測試控制器動作是否會傳回特定的視圖、傳回一組特定的資料，或傳回不同類型的動作結果。

本教學課程的目的是要示範如何為 ASP.NET MVC 應用程式中的控制器撰寫單元測試。 我們會討論如何建立三種不同類型的單元測試。 您將瞭解如何測試控制器動作所傳回的視圖、如何測試控制器動作所傳回的 View 資料，以及如何測試某個控制器動作是否會將您重新導向至第二個控制器動作。

## <a name="creating-the-controller-under-test"></a>建立受測試的控制器

讓我們從建立要測試的控制器開始。 名為 `ProductController`的控制器包含在 [清單 1] 中。

**清單1– `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample1.cs)]

`ProductController` 包含兩個名為 `Index()` 和 `Details()`的動作方法。 這兩個動作方法都會傳回一個視圖。 請注意，[`Details()`] 動作會接受名為 [識別碼] 的參數。

## <a name="testing-the-view-returned-by-a-controller"></a>測試控制器所傳回的視圖

假設我們想要測試 `ProductController` 是否會傳回正確的視圖。 我們想要確保叫用 `ProductController.Details()` 動作時，會傳回詳細資料檢視。 [清單 2] 中的測試類別包含測試 `ProductController.Details()` 動作所傳回之視圖的單元測試。

**清單2– `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample2.cs)]

[清單 2] 中的類別包含名為 `TestDetailsView()`的測試方法。 這個方法包含三行程式碼。 第一行程式碼會建立 `ProductController` 類別的新實例。 第二行程式碼會叫用控制器的 `Details()` 動作方法。 最後，程式碼的最後一行會檢查 `Details()` 動作所傳回的視圖是否為詳細資料檢視。

`ViewResult.ViewName` 屬性代表控制器傳回的視圖名稱。 關於測試這個屬性的一個重大警告。 有兩種方式可讓控制器傳回一個視圖。 控制器可以明確地傳回如下所示的視圖：

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample3.cs)]

或者，您也可以從控制器動作的名稱推斷視圖名稱，如下所示：

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample4.cs)]

此控制器動作也會傳回名為 `Details`的視圖。 不過，此視圖的名稱是從動作名稱推斷而來。 如果您想要測試檢視名稱，則必須明確地從控制器動作傳回視圖名稱。

您可以透過輸入鍵盤組合**Ctrl-R、** 或按一下 [**在方案中執行所有測試**] 按鈕（請參閱 [圖 1]）來執行 [清單 2] 中的單元測試。 如果測試成功，您會看到 [圖 2] 中的 [測試結果] 視窗。

[![在方案中執行所有測試](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)

**圖 01**：在方案中執行所有測試（[按一下以查看完整大小的影像](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png)）

[![成功！](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)

**圖 02**：成功！ （[按一下以查看完整大小的影像](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png)）

## <a name="testing-the-view-data-returned-by-a-controller"></a>測試控制器所傳回的 View 資料

MVC 控制器會使用稱為 *`View Data`* 的內容，將資料傳遞給視圖。 例如，假設您想要在叫用 `ProductController Details()` 動作時，顯示特定產品的詳細資料。 在此情況下，您可以建立 `Product` 類別的實例（定義于模型中），並利用 `View Data`來將實例傳遞至 `Details` 視圖。

[清單 3] 中修改過的 `ProductController` 包含會傳回產品的已更新 `Details()` 動作。

**清單3– `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample5.cs)]

首先，`Details()` 動作會建立代表膝上型電腦的 `Product` 類別的新實例。 接下來，`Product` 類別的實例會當做第二個參數傳遞至 `View()` 方法。

您可以撰寫單元測試來測試預期的資料是否包含在視圖資料中。 [清單 4] 中的單元測試會在您呼叫 `ProductController Details()` 動作方法時，測試是否會傳回代表膝上型電腦的產品。

**清單4– `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample6.cs)]

在 [清單 4] 中，`TestDetailsView()` 方法會測試藉由叫用 `Details()` 方法所傳回的 View 資料。 `ViewData` 會在叫用 `Details()` 方法所傳回的 `ViewResult` 上公開為屬性。 `ViewData.Model` 屬性包含傳遞至視圖的產品。 測試只會驗證封裝含在 View 資料中的產品具有名稱 [膝上型電腦]。

## <a name="testing-the-action-result-returned-by-a-controller"></a>測試控制器所傳回的動作結果

較複雜的控制器動作可能會根據傳遞至控制器動作的參數值，傳回不同類型的動作結果。 控制器動作可以傳回各種類型的動作結果，包括 `ViewResult`、`RedirectToRouteResult`或 `JsonResult`。

例如，當您將有效的產品識別碼傳遞給動作時，[清單 5] 中的 [修改的 `Details()`] 動作會傳回 [`Details`] 視圖。 如果您傳遞不正確產品識別碼--值小於1的識別碼，則會將您重新導向至 `Index()` 動作。

**清單5– `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample7.cs)]

您可以使用 [清單 6] 中的單元測試來測試 `Details()` 動作的行為。 [清單 6] 中的單元測試會在將值為-1 的識別碼傳遞給 `Details()` 方法時，確認您已重新導向至 `Index` 視圖。

**清單6– `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample8.cs)]

當您在控制器動作中呼叫 `RedirectToAction()` 方法時，控制器動作會傳回 `RedirectToRouteResult`。 測試會檢查 `RedirectToRouteResult` 是否會將使用者重新導向至名為 `Index`的控制器動作。

## <a name="summary"></a>總結

在本教學課程中，您已瞭解如何建立 MVC 控制器動作的單元測試。 首先，您已瞭解如何確認控制器動作是否傳回正確的視圖。 您已瞭解如何使用 `ViewResult.ViewName` 屬性來驗證視圖的名稱。

接下來，我們會探討如何測試 `View Data`的內容。 您已瞭解如何在呼叫控制器動作之後，檢查 `View Data` 中是否傳回正確的產品。

最後，我們會討論如何測試控制器動作是否傳回不同類型的動作結果。 您已瞭解如何測試控制器是否會傳回 `ViewResult` 或 `RedirectToRouteResult`。

> [!div class="step-by-step"]
> [下一個](creating-unit-tests-for-asp-net-mvc-applications-vb.md)
