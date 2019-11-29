---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
title: URL 路由 |Microsoft Docs
author: Erikre
description: 本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 為我們建立 ASP.NET Web Forms 應用程式的基本概念 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 4f4bf092-c400-471f-a876-78fda0417890
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
msc.type: authoredcontent
ms.openlocfilehash: 66b727b69ca4f9a3d35b67f492f9a554146e09ef
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74590715"
---
# <a name="url-routing"></a>URL 路由

依[Erik Reitan](https://github.com/Erikre)

[下載 Wingtip 玩具範例專案（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下載電子書（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 建立 ASP.NET Web Forms 應用程式的基本概念。 本教學課程系列隨附有[ C#原始程式碼](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 專案。

在本教學課程中，您將修改 Wingtip 玩具範例應用程式以支援 URL 路由。 路由可讓您的 web 應用程式使用易記、容易記住的 Url，並提供更好的搜尋引擎支援。 本教學課程是以先前的教學課程「成員資格和系統管理」為基礎，而且是 Wingtip 玩具教學課程系列的一部分。

## <a name="what-youll-learn"></a>您將瞭解的內容：

- 如何註冊 ASP.NET Web Forms 應用程式的路由。
- 如何將路由加入至網頁。
- 如何從資料庫選取資料以支援路由。

## <a name="aspnet-routing-overview"></a>ASP.NET 路由總覽

URL 路由可讓您設定應用程式，以接受未對應至實體檔案的要求 Url。 要求 URL 只是使用者在瀏覽器中輸入的 URL，以便在您的網站上尋找頁面。 您可以使用路由來定義對使用者有意義的 Url，並可協助搜尋引擎優化（SEO）。

根據預設，Web Forms 範本包含[ASP.NET 易記 url](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)。 大部分的基本路由工作都是使用*易記 url*來執行。 不過，在本教學課程中，您將新增自訂的路由功能。

在自訂 URL 路由之前，Wingtip 玩具範例應用程式可以使用下列 URL 連結至產品：

`https://localhost:44300/ProductDetails.aspx?productID=2`

藉由自訂 URL 路由，Wingtip 玩具範例應用程式會使用更容易閱讀的 URL 來連結至相同的產品：

`https://localhost:44300/Product/Convertible%20Car`

### <a name="routes"></a>路由

路由是對應至處理常式的 URL 模式。 處理常式可以是實體檔案，例如 Web Forms 應用程式中的 .aspx 檔案。 處理常式也可以是處理要求的類別。 若要定義路由，您可以藉由指定 URL 模式、處理常式和選擇性的路由名稱，來建立路由類別的實例。

您可以藉由將 `Route` 物件加入至 `RouteTable` 類別的靜態 `Routes` 屬性，將路由新增至應用程式。 Route 屬性是一個 `RouteCollection` 物件，它會儲存應用程式的所有路由。

### <a name="url-patterns"></a>URL 模式

URL 模式可以包含常值和變數預留位置（稱為 URL 參數）。 常值和預留位置位於以斜線（`/`）字元分隔的 URL 區段中。

當您對 web 應用程式提出要求時，會將 URL 剖析為區段和預留位置，並將變數值提供給要求處理常式。 此程式類似于分析查詢字串中的資料，並將其傳遞給要求處理常式的方式。 在這兩種情況下，變數資訊都會包含在 URL 中，並以索引鍵/值組的形式傳遞至處理常式。 針對查詢字串，索引鍵和值都在 URL 中。 針對路由，索引鍵是在 URL 模式中定義的預留位置名稱，而且只有值在 URL 中。

在 URL 模式中，您可以將預留位置括在大括弧（`{` 和 `}`）來定義。 您可以在區段中定義一個以上的預留位置，但預留位置必須以常值分隔。 例如，`{language}-{country}/{action}` 是有效的路由模式。 不過，`{language}{country}/{action}` 不是有效的模式，因為預留位置之間沒有常值或分隔符號。 因此，路由無法判斷要將 language 預留位置的值與國家/地區預留位置的值分開。

### <a name="mapping-and-registering-routes"></a>對應和註冊路由

在您可以將路由包含在 Wingtip 玩具範例應用程式的頁面之前，您必須在應用程式啟動時註冊路由。 若要註冊路由，您將修改 `Application_Start` 事件處理常式。

1. 在 Visual Studio 的**方案總管**中，尋找並開啟*Global.asax.cs*檔案。
2. 將黃色反白顯示的程式碼新增至*Global.asax.cs*檔案，如下所示：   

    [!code-csharp[Main](url-routing/samples/sample1.cs?highlight=30-31,34-46)]

當 Wingtip 玩具範例應用程式啟動時，它會呼叫 `Application_Start` 事件處理常式。 在這個事件處理常式的結尾，會呼叫 `RegisterCustomRoutes` 方法。 `RegisterCustomRoutes` 方法會藉由呼叫 `RouteCollection` 物件的 `MapPageRoute` 方法來新增每個路由。 路由的定義是使用路由名稱、路由 URL 和實體 URL。

第一個參數（"`ProductsByCategoryRoute`"）是路由名稱。 它會在需要時用來呼叫路由。 第二個參數（"`Category/{categoryName}`"）定義了易記的取代 URL，可以根據程式碼動態地進行。 當您使用以資料為基礎所產生的連結填入資料控制項時，就會用到此路由。 路由如下所示：

[!code-csharp[Main](url-routing/samples/sample2.cs)]

路由的第二個參數包含以大括弧（`{ }`）指定的動態值。 在此情況下，`categoryName` 是用來判斷適當路由路徑的變數。

> [!NOTE] 
> 
> **Optional**
> 
> 藉由將 `RegisterCustomRoutes` 方法移至不同的類別，您可能會發現管理程式碼較容易。 在*邏輯*資料夾中，建立個別的 `RouteActions` 類別。 將上述 `RegisterCustomRoutes` 方法從*Global.asax.cs*檔案移至新的 `RoutesActions` 類別。 使用 `RoleActions` 類別和 `createAdmin` 方法，作為如何從*Global.asax.cs*檔案呼叫 `RegisterCustomRoutes` 方法的範例。

您也可能已注意到使用 `Application_Start` 事件處理常式開頭的 `RouteConfig` 物件 `RegisterRoutes` 方法呼叫。 此呼叫是用來執行預設路由。 當您使用 Visual Studio 的 Web form 範本建立應用程式時，它會包含為預設程式碼。

## <a name="retrieving-and-using-route-data"></a>正在抓取和使用路由資料

如先前所述，您可以定義路由。 您在*Global.asax.cs*檔案中新增至 `Application_Start` 事件處理常式的程式碼會載入可定義的路由。

### <a name="setting-routes"></a>設定路由

路由需要您新增額外的程式碼。 在本教學課程中，您將使用模型系結來抓取使用資料控制項的資料產生路由時所使用的 `RouteValueDictionary` 物件。 `RouteValueDictionary` 物件將包含屬於特定產品類別的產品名稱清單。 會根據資料和路線來建立每個產品的連結。

#### <a name="enable-routes-for-categories-and-products"></a>啟用類別和產品的路由

接下來，您將更新應用程式，以使用 `ProductsByCategoryRoute` 來決定要針對每個產品類別連結包含的正確路由。 您也會更新 [ *ProductList* ] 頁面，以包含每個產品的路由連結。 這些連結會顯示在變更之前，不過連結現在會使用 URL 路由。

1. 在**方案總管**中，開啟 [*網站*] 頁面（如果尚未開啟）。
2. 將名為 "`categoryList`" 的**ListView**控制項更新為黃色反白顯示的變更，讓標記看起來如下所示：   

    [!code-aspx[Main](url-routing/samples/sample3.aspx?highlight=7-9)]
3. 在**方案總管**中，開啟 [ *ProductList* ] 頁面。
4. 使用黃色反白顯示的更新來更新*ProductList*的 `ItemTemplate` 專案，讓標記看起來如下所示：   

    [!code-aspx[Main](url-routing/samples/sample4.aspx?highlight=6-9,14-16)]
5. 開啟*ProductList.aspx.cs*的程式碼後置，並新增下列命名空間（以黃色反白顯示）：  

    [!code-csharp[Main](url-routing/samples/sample5.cs?highlight=9)]
6. 使用下列程式碼取代程式碼後置（*ProductList.aspx.cs*）的 `GetProducts` 方法：   

    [!code-csharp[Main](url-routing/samples/sample6.cs)]

#### <a name="add-code-for-product-details"></a>新增產品詳細資料的程式碼

現在，更新*ProductDetails*頁面的程式碼後置（*ProductDetails.aspx.cs*），以使用路由資料。 請注意，新的 `GetProduct` 方法也會接受查詢字串值，在此案例中，使用者的連結會使用較舊的非易記、非路由 URL。

1. 使用下列程式碼取代程式碼後置（*ProductDetails.aspx.cs*）的 `GetProduct` 方法：   

    [!code-csharp[Main](url-routing/samples/sample7.cs)]

## <a name="running-the-application"></a>執行應用程式

您可以立即執行應用程式，以查看更新的路由。

1. 按**F5**執行 Wingtip 玩具範例應用程式。  
 瀏覽器會開啟並顯示*default.aspx*頁面。
2. 按一下頁面頂端的 [**產品**] 連結。  
 所有產品都會顯示在 ProductList 的 [ *.aspx* ] 頁面上。 系統會顯示瀏覽器的下列 URL （使用您的埠號碼）：  
    `https://localhost:44300/ProductList`
3. 接下來，按一下靠近頁面頂端的 [ **Cars** ] 類別連結。  
 只有 cars 才會顯示在*ProductList*的 [.aspx] 頁面上。 系統會顯示瀏覽器的下列 URL （使用您的埠號碼）：  
    `https://localhost:44300/Category/Cars`
4. 按一下包含頁面上所列第一個車輛名稱的連結（「可轉換的**車**」），以顯示產品詳細資料。  
 系統會顯示瀏覽器的下列 URL （使用您的埠號碼）：  
    `https://localhost:44300/Product/Convertible%20Car`
5. 接下來，在瀏覽器中輸入下列非路由 URL （使用您的埠號碼）：  
    `https://localhost:44300/ProductDetails.aspx?productID=2`  
 程式碼仍會辨識包含查詢字串的 URL，在此情況下，使用者會有已加入書簽的連結。

## <a name="summary"></a>總結

在本教學課程中，您已新增類別和產品的路由。 您已瞭解如何將路由與使用模型系結的資料控制整合。 在下一個教學課程中，您將會執行全域錯誤處理。

## <a name="additional-resources"></a>其他資源

[ASP.NET 易記 Url](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)  
[將具有成員資格、OAuth 和 SQL Database 的安全 ASP.NET Web Forms 應用程式部署至 Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> [上一頁](membership-and-administration.md)
> [下一頁](aspnet-error-handling.md)
