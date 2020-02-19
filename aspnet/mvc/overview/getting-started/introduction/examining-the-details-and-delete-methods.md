---
uid: mvc/overview/getting-started/introduction/examining-the-details-and-delete-methods
title: 檢查 Details 和 Delete 方法 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 03/26/2015
ms.assetid: f1d2a916-626c-4a54-8df4-77e6b9fff355
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: da06815b5c1d76a939fdfb77ce11774081dfb881
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456396"
---
# <a name="examining-the-details-and-delete-methods"></a>檢查 Details 和 Delete 方法

依[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [Tutorial Note](index.md)]

在本教學課程的這個部分中，您將會檢查自動產生的 `Details` 和 `Delete` 方法。

## <a name="examining-the-details-and-delete-methods"></a>檢查 Details 和 Delete 方法

開啟 `Movie` 控制器，並檢查 `Details` 方法。

![](examining-the-details-and-delete-methods/_static/image1.png)

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample1.cs)]

建立此動作方法的 MVC 樣板引擎會加入批註，其中會顯示叫用方法的 HTTP 要求。 在此情況下，它是具有三個 URL 區段、`Movies` 控制器、`Details` 方法和 `ID` 值的 `GET` 要求。

Code First 可讓您輕鬆地使用 `Find` 方法來搜尋資料。 方法內建一項重要的安全性功能，就是程式碼確認 `Find` 方法在程式碼嘗試執行任何動作之前，已找到電影。 例如，駭客可能會將連結所建立的 URL 從 `http://localhost:xxxx/Movies/Details/1` 變更為類似 `http://localhost:xxxx/Movies/Details/12345` （或其他不代表實際電影的其他值），藉此將錯誤導入網站中。 如果您未檢查是否有 null 電影，null 電影會導致資料庫錯誤。

檢查 `Delete` 和 `DeleteConfirmed` 方法。

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample2.cs?highlight=17)]

請注意，HTTP GET `Delete` 方法不會刪除指定的電影，它會傳回電影的觀看畫面，您可以在其中提交（`HttpPost`）刪除。 如果您執行刪除作業以回應 GET 要求 (或是執行相關編輯作業、建立作業或任何會變更資料的其他作業)，則會造成安全性漏洞。 如需有關此情況的詳細資訊，請參閱 Stephen Walther 的 blog 專案[ASP.NET MVC Tip #46-請勿使用刪除連結，因為它們會建立安全性漏洞](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)。

我們將可刪除資料的 `HttpPost` 方法命名為 `DeleteConfirmed`，以提供 HTTP POST 方法的唯一簽章或名稱。 這兩個方法簽章如下所示：

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample3.cs)]

通用語言執行平台 (CLR) 需要多載方法，以提供唯一的參數簽章 (方法名稱相同但參數清單不同)。 不過，在這裡您需要兩個 Delete 方法，一個用於 GET，另一個用於 POST--兩者都有相同的參數簽章。 (它們都需要接受單一整數作為參數)。

若要將其排序，您可以執行幾項工作。 其中一個是提供不同名稱的方法。 這是 scaffolding 機制在上述範例採取的方法。 不過，這麼做會導致一個小問題：ASP.NET 會依名稱將 URL 區段與動作方法對應，一旦您重新命名方法，路由通常就會找不到這個方法。 解決辦法正如您看到的這個範例：將 `ActionName("Delete")` 屬性新增至 `DeleteConfirmed` 方法。 這會有效地執行路由系統的對應，使包含 POST 要求 */Delete/* 的 URL 會找到 `DeleteConfirmed` 方法。

另一個避免具有相同名稱和簽章之方法發生問題的常見方法，就是將 POST 方法的簽章變更為包含未使用的參數。 例如，有些開發人員會加入一個參數型別，`FormCollection` 傳遞至 POST 方法，然後直接不使用參數：

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="summary"></a>摘要

您現在有一個完整的 ASP.NET MVC 應用程式，可將資料儲存在本機 DB 資料庫中。 您可以建立、讀取、更新、刪除及搜尋電影。

![](examining-the-details-and-delete-methods/_static/image2.png)

## <a name="next-steps"></a>後續步驟

在您建立並測試 web 應用程式之後，下一個步驟是讓其他人可以透過網際網路使用它。 若要這麼做，您必須將它部署到 web 主控提供者。 Microsoft 在[免費的 Azure 試用帳戶](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)中，最多可為10個網站提供免費的 web 主機。 我建議您接著遵循我的教學課程，將[具有成員資格、OAuth 和 SQL Database 的安全 ASP.NET MVC 應用程式部署至 Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 一個絕佳的教學課程是 Tom 作者: dykstra 的中繼層級，[為 ASP.NET MVC 應用程式建立 Entity Framework 資料模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 [Stackoverflow](http://stackoverflow.com/help)和[ASP.NET MVC 論壇](https://forums.asp.net/1146.aspx)是提出問題的絕佳地方。 請在 twitter 上追蹤[我](https://twitter.com/RickAndMSFT)的最新教學課程，以取得更新。

歡迎您提供意見反應。

— [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter： [@RickAndMSFT](https://twitter.com/RickAndMSFT)  
— [Scott Hanselman](http://www.hanselman.com/blog/) twitter： [@shanselman](https://twitter.com/shanselman)

> [!div class="step-by-step"]
> [[上一步]](adding-validation.md)
