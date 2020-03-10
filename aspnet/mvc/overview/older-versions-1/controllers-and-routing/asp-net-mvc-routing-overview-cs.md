---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs
title: ASP.NET MVC 路由總覽（C#） |Microsoft Docs
author: StephenWalther
description: 在本教學課程中，Stephen Walther 會說明 ASP.NET MVC 架構如何將瀏覽器要求對應至控制器動作。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 5b39d2d5-4bf9-4d04-94c7-81b84dfeeb31
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs
msc.type: authoredcontent
ms.openlocfilehash: 5e1155ca676e7a25b5bfc63e251c6387a010eb34
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544139"
---
# <a name="aspnet-mvc-routing-overview-c"></a>ASP.NET MVC 路由概觀 (C#)

依[Stephen Walther](https://github.com/StephenWalther)

> 在本教學課程中，Stephen Walther 會說明 ASP.NET MVC 架構如何將瀏覽器要求對應至控制器動作。

在本教學課程中，您會在每個名為*ASP.NET 路由*的 ASP.NET MVC 應用程式中引進一項重要功能。 ASP.NET 路由模組負責將傳入瀏覽器要求對應至特定的 MVC 控制器動作。 本教學課程結束時，您將瞭解標準路由表如何將要求對應至控制器動作。

## <a name="using-the-default-route-table"></a>使用預設路由表

當您建立新的 ASP.NET MVC 應用程式時，應用程式已設定為使用 ASP.NET 路由。 ASP.NET 路由會在兩個地方設定。

首先，會在應用程式的 Web 設定檔案（Web.config 檔案）中啟用 ASP.NET 路由。 與路由相關的設定檔中有四個區段： system.web. HTTPHandlers 區段、system.webserver 和 system.web 區段，以及 system.webserver. web. web. web.config 區段和 system.servicemodel。 請小心不要刪除這些區段，因為如果沒有這些區段，路由將不再有效。

其次，更重要的是，在應用程式的 global.asax 檔案中建立路由表。 Global.asax 檔案是特殊的檔案，其中包含 ASP.NET 應用程式週期事件的事件處理常式。 在應用程式啟動事件期間，會建立路由表。

[清單 1] 中的檔案包含 ASP.NET MVC 應用程式的預設 global.asax 檔案。

**清單 1-Global.asax.cs**

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample1.cs)]

當 MVC 應用程式第一次啟動時，會呼叫應用程式\_Start （）方法。 這個方法接著會呼叫 RegisterRoutes （）方法。 RegisterRoutes （）方法會建立路由表。

預設路由表包含單一路由（名為 Default）。 預設路由會將 URL 的第一個區段對應至控制器名稱、控制器動作 URL 的第二個區段，以及第三個區段到名為**id**的參數。

假設您在網頁瀏覽器的網址列中輸入下列 URL：

/Home/Index/3

預設路由會將此 URL 對應至下列參數：

- 控制器 = 首頁

- action = 索引

- 識別碼 = 3

當您要求 URL/Home/Index/3 時，會執行下列程式碼：

HomeController。 Index （3）

預設路由會包含所有三個參數的預設值。 如果您未提供控制器，則控制器參數的預設值為**Home**。 如果您未提供動作，動作參數會預設為值**索引**。 最後，如果您未提供識別碼，則 id 參數會預設為空字串。

讓我們看看一些範例，說明預設路由如何將 Url 對應至控制器動作。 假設您在瀏覽器網址列中輸入下列 URL：

/Home

基於預設路由參數預設值，輸入此 URL 將會呼叫 [清單 2] 中 HomeController 類別的 Index （）方法。

**清單 2-HomeController.cs**

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample2.cs)]

在 [清單 2] 中，HomeController 類別包含名為 Index （）的方法，它會接受名為 Id 的單一參數。URL/Home 會導致使用空字串來呼叫 Index （）方法，做為 Id 參數的值。

由於 MVC 架構會叫用控制器動作的方式，因此 URL/Home 也會符合 [清單 3] 中 HomeController 類別的 Index （）方法。

**清單 3-HomeController.cs （不含參數的索引動作）**

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample3.cs)]

[清單 3] 中的 Index （）方法不接受任何參數。 URL/Home 會導致呼叫這個 Index （）方法。 URL/Home/Index/3 也會叫用這個方法（忽略識別碼）。

URL/Home 也符合清單4中 HomeController 類別的 Index （）方法。

**清單 4-HomeController.cs （具有可為 null 參數的索引動作）**

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample4.cs)]

在 [清單 4] 中，Index （）方法有一個整數參數。 因為參數是可為 null 的參數（可以有空值），所以可以呼叫索引（），而不會引發錯誤。

最後，使用 URL/Home 叫用清單5中的 Index （）方法會造成例外狀況，因為 Id 參數*不是*可為 null 的參數。 如果您嘗試叫用 Index （）方法，就會得到 [圖 1] 所示的錯誤。

**清單 5-HomeController.cs （具有識別碼參數的索引動作）**

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample5.cs)]

[![叫用需要參數值的控制器動作](asp-net-mvc-routing-overview-cs/_static/image1.jpg)](asp-net-mvc-routing-overview-cs/_static/image1.png)

**圖 01**：叫用需要參數值的控制器動作（[按一下以查看完整大小的影像](asp-net-mvc-routing-overview-cs/_static/image2.png)）

另一方面，URL/Home/Index/3 的運作方式與 [清單 5] 中的索引控制器動作沒什麼關係。 要求/Home/Index/3 會導致使用值3的 Id 參數來呼叫 Index （）方法。

## <a name="summary"></a>總結

本教學課程的目的是為您提供 ASP.NET 路由的簡介。 我們檢查了您使用新的 ASP.NET MVC 應用程式取得的預設路由表。 您已瞭解預設路由如何將 Url 對應至控制器動作。

> [!div class="step-by-step"]
> [下一個](understanding-action-filters-cs.md)
