---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/improving-the-details-and-delete-methods
title: 改善 Details 和 Delete 方法（C#） |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，也就是 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 3f42edd9-c5b8-4712-9055-970f7d38e350
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/improving-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 54d7be8fe1bff604ae9c9e9914d7c6426ab85c1c
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457501"
---
# <a name="improving-the-details-and-delete-methods-c"></a>改善 Details 和 Delete 方法 (C#)

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > 本教學課程的更新版本可在[這裡](../../../getting-started/introduction/getting-started.md)取得，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。 它更安全、更容易遵循，並示範更多功能。
> 
> 
> 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，這是 Microsoft Visual Studio 的免費版本。 開始之前，請先確定您已安裝下列必要條件。 您可以按一下下列連結來安裝所有這些專案： [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，您可以使用下列連結個別安裝必要條件：
> 
> - [Visual Studio Web Developer Express SP1 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（執行時間 + 工具支援）
> 
> 如果您使用 Visual Studio 2010，而不是 Visual Web Developer 2010，請按一下下列連結來安裝必要條件： [Visual Studio 2010 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 本主題提供具有C#原始程式碼的 Visual Web Developer 專案。 [下載C#版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果您偏好 Visual Basic，請切換到本教學課程的[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)。

在本教學課程的這個部分中，您將會對自動產生的 `Details` 和 `Delete` 方法進行一些改進。 這些變更並不是必要的，但只要幾個小部分的程式碼，您就可以輕鬆地增強應用程式。

## <a name="improving-the-details-and-delete-methods"></a>改善 Details 和 Delete 方法

當您 scaffold `Movie` 控制器時，請 ASP.NET MVC 產生的程式碼，而這只是幾個小部分的變更，才能夠更穩固。

開啟 `Movie` 控制器，並在找不到電影時傳回 `HttpNotFound` 來修改 `Details` 方法。 您也應該修改 `Details` 方法，為傳遞給它的識別碼設定預設值。 （您在本教學課程的[第6部分](examining-the-edit-methods-and-edit-view.md)中，對 `Edit` 方法進行了類似的變更）。不過，您必須將 `Details` 方法的傳回型別從 `ViewResult` 變更為 `ActionResult`，因為 `HttpNotFound` 方法不會傳回 `ViewResult` 物件。 下列範例顯示已修改的 `Details` 方法。

[!code-csharp[Main](improving-the-details-and-delete-methods/samples/sample1.cs)]

Code First 可讓您輕鬆地使用 `Find` 方法來搜尋資料。 我們在方法中建立了一項重要的安全性功能，那就是程式碼會驗證 `Find` 方法在程式碼嘗試執行任何動作之前，已找到電影。 例如，駭客可能會將連結所建立的 URL 從 `http://localhost:xxxx/Movies/Details/1` 變更為類似 `http://localhost:xxxx/Movies/Details/12345` （或其他不代表實際電影的其他值），藉此將錯誤導入網站中。 如果您不檢查是否有 null 電影，這可能會導致資料庫錯誤。

同樣地，變更 `Delete` 和 `DeleteConfirmed` 方法，以指定 ID 參數的預設值，並在找不到電影時傳回 `HttpNotFound`。 `Movie` 控制器中已更新的 `Delete` 方法如下所示。

[!code-csharp[Main](improving-the-details-and-delete-methods/samples/sample2.cs)]

請注意，`Delete` 方法不會刪除資料。 如果您執行刪除作業以回應 GET 要求 (或是執行相關編輯作業、建立作業或任何會變更資料的其他作業)，則會造成安全性漏洞。 如需有關此情況的詳細資訊，請參閱 Stephen Walther 的 blog 專案[ASP.NET MVC Tip #46-請勿使用刪除連結，因為它們會建立安全性漏洞](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)。

我們將可刪除資料的 `HttpPost` 方法命名為 `DeleteConfirmed`，以提供 HTTP POST 方法的唯一簽章或名稱。 這兩個方法簽章如下所示：

[!code-csharp[Main](improving-the-details-and-delete-methods/samples/sample3.cs)]

Common language runtime （CLR）需要多載的方法，才能擁有唯一的簽章（相同名稱、不同的參數清單）。 不過，在這裡您需要兩個刪除方法：一個用於 GET，另一個用於 POST--這兩者都需要相同的簽章。 (它們都需要接受單一整數作為參數)。

若要將其排序，您可以執行幾項工作。 其中一個是提供不同名稱的方法。 這就是我們在先前範例中所做的工作。 不過，這麼做會導致一個小問題：ASP.NET 會依名稱將 URL 區段與動作方法對應，一旦您重新命名方法，路由通常就會找不到這個方法。 解決辦法正如您看到的這個範例：將 `ActionName("Delete")` 屬性新增至 `DeleteConfirmed` 方法。 這會有效地執行路由系統的對應，使包含 POST 要求<em>/Delete/</em>的 URL 會找到 `DeleteConfirmed` 方法。

另一種避免具有相同名稱和簽章之方法發生問題的方法，就是將 POST 方法的簽章變更為包含未使用的參數。 例如，有些開發人員會加入一個參數型別，`FormCollection` 傳遞至 POST 方法，然後直接不使用參數：

[!code-csharp[Main](improving-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="wrapping-up"></a>總結

您現在有一個完整的 ASP.NET MVC 應用程式，可將資料儲存在 SQL Server Compact 資料庫中。 您可以建立、讀取、更新、刪除及搜尋電影。

![](improving-the-details-and-delete-methods/_static/image1.png)

這個基本教學課程讓您開始建立控制器、將它們與 views 產生關聯，以及傳遞硬式編碼的資料。 然後，您建立並設計了資料模型。 Entity Framework Code First 會即時從資料模型建立資料庫，而 ASP.NET MVC 架構系統會自動產生基本 CRUD 作業的動作方法和 views。 您接著加入了搜尋表單，讓使用者可以搜尋資料庫。 您已變更資料庫以包含新的資料行，然後更新兩個頁面來建立和顯示此新資料。 您可以使用 `DataAnnotations` 命名空間中的屬性來標記資料模型，藉以加入驗證。 產生的驗證會在用戶端和伺服器上執行。

如果您想要部署應用程式，請先在本機 IIS 7 伺服器上測試應用程式，這樣做會很有説明。 您可以使用此[Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=ASPNET;)連結來啟用 ASP.NET 應用程式的 IIS 設定。 請參閱下列部署連結：

- [ASP.NET 部署內容對應](https://msdn.microsoft.com/library/dd394698.aspx)
- [啟用 IIS 7。x](https://blogs.msdn.com/b/rickandy/archive/2011/03/14/enabling-iis-7-x-on-windows-7-vista-sp1-windows-2008-windows-2008-r2.aspx)
- [Web 應用程式專案部署](https://msdn.microsoft.com/library/dd394698.aspx)

現在，我建議您移至中繼層級[建立 Entity Framework 資料模型以取得 ASP.NET Mvc 應用程式](../../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)和[MVC 音樂存放](../../mvc-music-store/mvc-music-store-part-1.md)教學課程、流覽[MSDN 上的 ASP.NET 文章](https://msdn.microsoft.com/library/gg416514(VS.98).aspx)，並查看[https://asp.net/mvc](https://asp.net/mvc)的許多影片和資源，以深入瞭解 ASP.NET MVC！ [ASP.NET MVC 論壇](https://forums.asp.net/1146.aspx)是提出問題的絕佳地方。

盡情享受！

— Scott Hanselman （在 Twitter 上[http://hanselman.com](http://hanselman.com)和[@shanselman](http://twitter.com/shanselman) ，以及 Rick Anderson [blogs.msdn.com/rickAndy](https://blogs.msdn.com/rickAndy)

> [!div class="step-by-step"]
> [[上一步]](adding-validation-to-the-model.md)
