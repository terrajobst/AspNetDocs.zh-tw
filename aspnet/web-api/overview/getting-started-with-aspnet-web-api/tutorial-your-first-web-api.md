---
uid: web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
title: 開始使用 ASP.NET Web API 2 （C#）-ASP.NET 4。x
author: MikeWasson
description: 教學課程與程式碼。 使用 ASP.NET Web API 建立可傳回產品清單的 Web API。
ms.author: riande
ms.date: 11/28/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
msc.type: authoredcontent
ms.openlocfilehash: 3e35c2bc0e46dfdb4544b772775eddd533f27be3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556795"
---
# <a name="get-started-with-aspnet-web-api-2-c"></a>開始使用 ASP.NET Web API 2 （C#）

由[Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://code.msdn.microsoft.com/Sample-code-of-Getting-c56ccb28)

在本教學課程中，您將使用 ASP.NET Web API 來建立可傳回產品清單的 Web API。

HTTP 並不只是用來提供網頁。 HTTP 也是一個功能強大的平臺，可用於建立公開服務和資料的 Api。 HTTP 既簡單、有彈性，而且十分普遍。 幾乎任何您可以想到的平臺都有 HTTP 程式庫，因此 HTTP 服務可以連線到各種用戶端，包括瀏覽器、行動裝置和傳統桌面應用程式。

ASP.NET Web API 是在 .NET Framework 之上建立 Web Api 的架構。 

## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本

- [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
- Web API 2

如需本教學課程的較新版本，請參閱[使用適用于 Windows 的 ASP.NET Core 和 Visual Studio 建立 Web API](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) 。

## <a name="create-a-web-api-project"></a>建立 Web API 專案

在本教學課程中，您將使用 ASP.NET Web API 來建立可傳回產品清單的 Web API。 前端網頁會使用 jQuery 來顯示結果。

![](tutorial-your-first-web-api/_static/image1.png)

啟動 Visual Studio，然後從 [**開始**] 頁面選取 [**新增專案**]。 或者，**從 [檔案**] 功能表選取 [**新增**]，然後選取 [**專案**]。

在 [**範本**] 窗格中，選取 [**已安裝的範本**]，然後展開 **C#視覺效果**節點。 在 **[ C#視覺效果**] 底下，選取 [ **Web**]。 在專案範本清單中，選取 [ **ASP.NET Web 應用程式**]。 將專案命名為 "ProductsApp"，然後按一下 **[確定]** 。

![](tutorial-your-first-web-api/_static/image2.png)

在 [**新增 ASP.NET 專案**] 對話方塊中，選取 [**空白**] 範本。 在 [&quot;新增&quot;的資料夾和核心參考] 底下，檢查 [ **WEB API**]。 按一下 [確定]。

![](tutorial-your-first-web-api/_static/image3.png)

> [!NOTE]
> 您也可以使用 &quot;Web API&quot; 範本來建立 Web API 專案。 Web API 範本會使用 ASP.NET MVC 來提供 API 說明頁面。 我在本教學課程中使用空白範本，因為我想要顯示不含 MVC 的 Web API。 一般來說，您不需要知道 ASP.NET MVC 就能使用 Web API。

## <a name="adding-a-model"></a>新增模型

「模型」是代表應用程式中資料的物件。 ASP.NET Web API 可以自動將您的模型序列化為 JSON、XML 或其他格式，然後將序列化資料寫入 HTTP 回應訊息的本文中。 只要用戶端可以讀取序列化格式，它就可以還原序列化物件。 大部分的用戶端都可以剖析 XML 或 JSON。 此外，用戶端可以藉由設定 HTTP 要求訊息中的 Accept 標頭，來指出所要的格式。

讓我們從建立代表產品的簡單模型開始。

如果沒有顯示 [方案總管]，請按一下 [檢視] 功能表，然後選取 [方案總管]。 在 [方案總管] 中，於 Models 資料夾上按一下滑鼠右鍵。 從操作功能表中，選取 [新增]，然後選取 [類別]。

![](tutorial-your-first-web-api/_static/image4.png)

將類別命名為 &quot;產品&quot;。 將下列屬性新增至 `Product` 類別。

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample1.cs)]

## <a name="adding-a-controller"></a>新增控制器

在 Web API 中，*控制器*是處理 HTTP 要求的物件。 我們會新增可傳回產品清單的控制器，或由識別碼所指定的單一產品。

> [!NOTE]
> 如果您已使用 ASP.NET MVC，則您已經熟悉控制器。 Web API 控制器類似于 MVC 控制器，但會繼承**ApiController**類別，而不是**控制器**類別。

在 [方案總管] 中，於 Controllers 資料夾上按一下滑鼠右鍵。 選取 [新增]，然後選取 [控制器]。

![](tutorial-your-first-web-api/_static/image5.png)

在 [新增 Scaffold] 對話方塊中，選取 [Web API 控制器 - 空白]。 按一下 [新增]。

![](tutorial-your-first-web-api/_static/image6.png)

在 [**新增控制器**] 對話方塊中，將控制器命名為 &quot;productscontroller.cs&quot;。 按一下 [新增]。

![](tutorial-your-first-web-api/_static/image7.png)

此樣板會在 [控制器] 資料夾中建立名為 ProductsController.cs 的檔案。

![](tutorial-your-first-web-api/_static/image8.png)

> [!NOTE]
> 您不需要將控制器放入名為 [控制器] 的資料夾。 資料夾名稱只是組織原始程式檔的便利方式。

如果此檔案尚未開啟，請按兩下檔案將它開啟。 將此檔案中的程式碼取代為下列內容：

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample2.cs)]

為了讓範例保持簡單，產品會儲存在控制器類別內的固定陣列中。 當然，在實際的應用程式中，您會查詢資料庫或使用其他外部資料源。

控制器會定義兩個傳回產品的方法：

- `GetAllProducts` 方法會傳回完整的產品清單，做為**IEnumerable&lt;產品&gt;** 類型。
- `GetProduct` 方法會依識別碼查閱單一產品。

就這麼容易！ 您有一個可運作的 Web API。 控制器上的每個方法都會對應至一或多個 Uri：

| 控制器方法 | URI |
| --- | --- |
| Getallproductswithcategories | /api/products |
| GetProduct | /api/products/*識別碼* |

針對 `GetProduct` 方法，URI 中的*識別碼*是預留位置。 例如，若要取得識別碼為5的產品，則 URI 為 `api/products/5`。

如需 Web API 如何將 HTTP 要求路由傳送至控制器方法的詳細資訊，請參閱[ASP.NET Web API 中的路由](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)。

## <a name="calling-the-web-api-with-javascript-and-jquery"></a>使用 JAVAscript 和 jQuery 呼叫 Web API

在本節中，我們將新增使用 AJAX 呼叫 Web API 的 HTML 網頁。 我們將使用 jQuery 來進行 AJAX 呼叫，並以結果更新頁面。

在方案總管中，以滑鼠右鍵按一下專案並選取 [**加入**]，然後選取 [**新增專案**]。

![](tutorial-your-first-web-api/_static/image9.png)

在 [**加入新專案**] 對話方塊中，選取 [**視覺效果C#** ] 底下的 [ **Web** ] 節點，然後選取 [ **HTML] 頁面**專案。 將頁面命名為 &quot;index .html&quot;。

![](tutorial-your-first-web-api/_static/image10.png)

以下列內容取代此檔案中的所有專案：

[!code-html[Main](tutorial-your-first-web-api/samples/sample3.html)]

您可以使用幾種方式來取得 jQuery。 在此範例中，我使用了[Microsoft AJAX CDN](../../../ajax/cdn/overview.md)。 您也可以從[http://jquery.com/](http://jquery.com/)下載，而 ASP.NET 的「Web API」專案範本也包含 jQuery。

### <a name="getting-a-list-of-products"></a>取得產品清單

若要取得產品清單，請將 HTTP GET 要求傳送至 &quot;/api/products&quot;。

JQuery [getJSON](http://api.jquery.com/jQuery.getJSON/)函數會傳送 AJAX 要求。 For response 包含 JSON 物件的陣列。 `done` 函式會指定要求成功時所呼叫的回呼。 在回呼中，我們會使用產品資訊來更新 DOM。

[!code-html[Main](tutorial-your-first-web-api/samples/sample4.html)]

### <a name="getting-a-product-by-id"></a>依識別碼取得產品

若要依識別碼取得產品，請將 HTTP GET 要求傳送至 &quot;/api/products/*id*&quot;，其中*ID*是產品識別碼。

[!code-javascript[Main](tutorial-your-first-web-api/samples/sample5.js)]

我們仍然會呼叫 `getJSON` 來傳送 AJAX 要求，但這次我們將識別碼放在要求 URI 中。 此要求的回應是單一產品的 JSON 標記法。

## <a name="running-the-application"></a>執行應用程式

按 F5 開始對應用程式進行偵錯。 網頁看起來應該如下所示：

![](tutorial-your-first-web-api/_static/image11.png)

若要依識別碼取得產品，請輸入識別碼，然後按一下 [搜尋]：

![](tutorial-your-first-web-api/_static/image12.png)

如果您輸入不正確識別碼，伺服器會傳回 HTTP 錯誤：

![](tutorial-your-first-web-api/_static/image13.png)

## <a name="using-f12-to-view-the-http-request-and-response"></a>使用 F12 來查看 HTTP 要求和回應

當您使用 HTTP 服務時，查看 HTTP 要求和要求訊息會非常有用。 您可以使用 Internet Explorer 9 中的 F12 開發人員工具來執行這項操作。 從 Internet Explorer 9，按**F12**開啟工具。 按一下 [**網路**] 索引標籤，然後按 [**開始捕獲**]。 現在請回到網頁，然後按**F5**重載網頁。 Internet Explorer 將會在瀏覽器與 web 伺服器之間捕捉 HTTP 流量。 [摘要] 視圖會顯示頁面的所有網路流量：

![](tutorial-your-first-web-api/_static/image14.png)

找出相對 URI "api/products/" 的專案。 選取此專案，然後按一下 [**移至詳細視圖**]。 在 [詳細資料] 視圖中，有一些索引標籤可供您查看要求和回應標頭和主體。 例如，如果您按一下 [**要求標頭**] 索引標籤，您可以看到用戶端要求的 &quot;application/json&quot; 在 Accept 標頭中。

![](tutorial-your-first-web-api/_static/image15.png)

如果您按一下 [回應主體] 索引標籤，您可以看到產品清單如何序列化為 JSON。 其他瀏覽器具有類似的功能。 另一個有用的工具是[Fiddler](http://www.fiddler2.com/fiddler2/)，也就是 web 調試的 proxy。 您可以使用 Fiddler 來查看您的 HTTP 流量，並撰寫 HTTP 要求，讓您完全掌控要求中的 HTTP 標頭。

## <a name="see-this-app-running-on-azure"></a>請參閱此應用程式在 Azure 上執行

您是否想要查看已完成的網站以即時 web 應用程式的形式執行？ 只要按一下下列按鈕，您就可以將應用程式的完整版本部署至您的 Azure 帳戶。

[![](https://azuredeploy.net/deploybutton.png)](https://deploy.azure.com/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebAPI-ProductsApp#/form/setup)

您需要 Azure 帳戶，才能將此解決方案部署至 Azure。 如果您還沒有帳戶，您可以使用下列選項：

- [免費申請 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-您將取得可試用付費 azure 服務的額度，且即使在用完後，您仍可保留帳戶，並使用免費的 azure 服務。
- [啟用 msdn 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)-您的 msdn 訂用帳戶每月會提供您額度，供您用於付費 Azure 服務。

## <a name="next-steps"></a>後續步驟

- 如需可支援 POST、PUT 和 DELETE 動作及寫入至資料庫之 HTTP 服務的更完整範例，請參閱搭配[使用 WEB API 2 與 Entity Framework 6](../data/using-web-api-with-entity-framework/part-1.md)。
- 如需有關在 HTTP 服務上建立流暢且回應式 web 應用程式的詳細資訊，請參閱[ASP.NET 單一頁面應用程式](../../../single-page-application/index.md)。
- 如需如何將 Visual Studio Web 專案部署至 Azure App Service 的詳細資訊，請參閱[在 Azure App Service 中建立 ASP.NET web 應用程式](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)。
