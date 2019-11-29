---
uid: web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
title: 在 ASP.NET Web API 1-ASP.NET 4.x 中啟用 CRUD 作業
author: MikeWasson
description: 教學課程說明如何使用 ASP.NET 4.x 的 ASP.NET Web API，在 HTTP 服務中支援 CRUD 作業。
ms.author: riande
ms.date: 01/28/2012
ms.custom: seoapril2019
ms.assetid: c125ca47-606a-4d6f-a1fc-1fc62928af93
msc.legacyurl: /web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
msc.type: authoredcontent
ms.openlocfilehash: a096fd1c54df33b40115907a5c2517b2e3fec5b8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600343"
---
# <a name="enabling-crud-operations-in-aspnet-web-api-1"></a>啟用 ASP.NET Web API 1 中的 CRUD 作業

由[Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-c4761894)

> 本教學課程說明如何使用 ASP.NET 4.x 的 ASP.NET Web API，支援 HTTP 服務中的 CRUD 作業。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - Visual Studio 2012
> - Web API 1 （也適用于 Web API 2）

CRUD 代表 &quot;建立、讀取、更新和刪除，&quot; 這四種基本資料庫作業。 許多 HTTP 服務也會透過 REST 或 REST 之類的 Api 來建立 CRUD 作業的模型。

在本教學課程中，您將建立一個非常簡單的 Web API 來管理產品清單。 每項產品都會包含名稱、價格及類別（例如 &quot;玩具&quot; 或 &quot;硬體&quot;），加上產品識別碼。

產品 API 將會公開下列方法。

| 動作 | HTTP 方法 | 相對 URI |
| --- | --- | --- |
| 取得所有產品的清單 | GET | /api/products |
| 依識別碼取得產品 | GET | /api/products/*識別碼* |
| 依類別取得產品 | GET | /api/products？ category =*category* |
| 建立新的產品 | POST | /api/products |
| 更新產品 | PUT | /api/products/*識別碼* |
| 刪除產品 | Delete | /api/products/*識別碼* |

請注意，部分 Uri 會在 path 中包含產品識別碼。 例如，若要取得識別碼為28的產品，用戶端會傳送 `http://hostname/api/products/28`的 GET 要求。

### <a name="resources"></a>資源

產品 API 會定義兩個資源類型的 Uri：

| 資源 | URI |
| --- | --- |
| 所有產品的清單。 | /api/products |
| 個別產品。 | /api/products/*識別碼* |

### <a name="methods"></a>方法

四個主要的 HTTP 方法（GET、PUT、POST 和 DELETE）可以對應至 CRUD 作業，如下所示：

- GET 會在指定的 URI 上抓取資源的表示。 GET 在伺服器上應該沒有任何副作用。
- PUT 會將資源更新為指定的 URI。 如果伺服器允許用戶端指定新的 Uri，PUT 也可以用來在指定的 URI 建立新的資源。 在本教學課程中，API 將不支援透過 PUT 建立。
- POST 會建立新的資源。 伺服器會指派新物件的 URI，並在回應訊息中傳回此 URI。
- DELETE 刪除指定 URI 的資源。

注意： PUT 方法會取代整個 product 實體。 也就是說，用戶端預期會傳送已更新產品的完整標記法。 如果您想要支援部分更新，建議您選擇 PATCH 方法。 本教學課程不會執行修補程式。

## <a name="create-a-new-web-api-project"></a>建立新的 Web API 專案

從執行 Visual Studio 開始，然後從 [**開始**] 頁面選取 [**新增專案**]。 或者，**從 [檔案**] 功能表選取 [**新增**]，然後選取 [**專案**]。

在 [**範本**] 窗格中，選取 [**已安裝的範本**]，然後展開 **C#視覺效果**節點。 在 **[ C#視覺效果**] 底下，選取 [ **Web**]。 在專案範本清單中，選取 [ **ASP.NET MVC 4 Web 應用程式**]。 將專案命名為 &quot;ProductStore&quot; 然後按一下 **[確定]** 。

![](creating-a-web-api-that-supports-crud-operations/_static/image1.png)

在 [**新增 ASP.NET MVC 4 專案**] 對話方塊中，選取 [ **Web API** ]，然後按一下 **[確定]** 。

![](creating-a-web-api-that-supports-crud-operations/_static/image2.png)

## <a name="adding-a-model"></a>新增模型

「模型」是代表應用程式中資料的物件。 在 ASP.NET Web API 中，您可以使用強型別 CLR 物件做為模型，而且它們會自動序列化為用戶端的 XML 或 JSON。

針對 ProductStore API，我們的資料是由產品所組成，因此我們將建立名為 `Product`的新類別。

如果方案總管尚未顯示，請按一下 [ **View** ] 功能表，然後選取 [**方案總管**]。 在方案總管中，以滑鼠右鍵按一下 [**模型**] 資料夾。 從內容功能表中，選取 [**新增**]，然後選取 [**類別**]。 將類別命名為 &quot;產品&quot;。

![](creating-a-web-api-that-supports-crud-operations/_static/image3.png)

將下列屬性新增至 `Product` 類別。

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample1.cs)]

## <a name="adding-a-repository"></a>加入儲存機制

我們需要儲存一系列產品。 將集合與我們的服務實作為區隔是個不錯的主意。 如此一來，我們就可以變更備份存放區，而不需要重寫服務類別。 這種設計稱為「*儲存*機制」模式。 一開始請先定義存放庫的泛型介面。

在方案總管中，以滑鼠右鍵按一下 [**模型**] 資料夾。 選取 [**加入**]，然後選取 [**新增專案**]。

![](creating-a-web-api-that-supports-crud-operations/_static/image4.png)

在 [**範本**] 窗格中，選取 [**已安裝的範本**]，然後展開C#節點。 在C#底下選取 [程式**代碼**]。 在程式碼範本清單中，選取 [**介面**]。 將介面命名 &quot;IProductRepository&quot;。

![](creating-a-web-api-that-supports-crud-operations/_static/image5.png)

新增下列執行：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample2.cs)]

現在將另一個類別新增至 [模型] 資料夾，名為 &quot;ProductRepository。&quot; 這個類別將會執行 `IProductRepository` 介面。 新增下列執行：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample3.cs)]

存放庫會將清單保留在本機記憶體中。 這在教學課程中是正常的，但在實際的應用程式中，您會將資料儲存在外部，也就是資料庫或雲端儲存體。 儲存機制模式可讓您稍後更輕鬆地變更執行。

## <a name="adding-a-web-api-controller"></a>新增 Web API 控制器

如果您曾經使用過 ASP.NET MVC，則您已經熟悉控制器。 在 ASP.NET Web API 中，*控制器*是處理來自用戶端之 HTTP 要求的類別。 [新增專案] wizard 會在建立專案時，為您建立兩個控制器。 若要查看它們，請展開方案總管中的 [控制器] 資料夾。

- HomeController 是傳統的 ASP.NET MVC 控制器。 它負責為網站提供 HTML 網頁，而不是與我們的 Web API 直接相關。
- ValuesController 是 WebAPI 控制器的範例。

繼續並刪除 ValuesController，方法是以滑鼠右鍵按一下方案總管中的檔案，然後選取 [**刪除]。** 現在加入新的控制器，如下所示：

在**方案總管**中，以滑鼠右鍵按一下 [控制器] 資料夾。 選取 [**新增**]，然後選取 [**控制器**]。

![](creating-a-web-api-that-supports-crud-operations/_static/image6.png)

在 [**新增控制器**嚮導] 中，將控制器命名為 &quot;productscontroller.cs&quot;。 在 [**範本**] 下拉式清單中，選取 [**空的 API 控制器**]。 然後按一下 [加入]。

![](creating-a-web-api-that-supports-crud-operations/_static/image7.png)

> [!NOTE]
> 您不需要將控制器放入名為 [控制器] 的資料夾。 資料夾名稱並不重要;這只是一個方便的方式來組織您的來源檔案。

「**新增控制器**」 wizard 會在 [控制器] 資料夾中建立名為 ProductsController.cs 的檔案。 如果此檔案尚未開啟，請按兩下檔案將其開啟。 新增下列**using**語句：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample4.cs)]

新增保存**IProductRepository**實例的欄位。

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample5.cs)]

> [!NOTE]
> 在控制器中呼叫 `new ProductRepository()` 並不是最佳設計，因為它會將控制器系結至特定的 `IProductRepository`執行。 如需更好的方法，請參閱[使用 WEB API 相依性解析程式](../advanced/dependency-injection.md)。

## <a name="getting-a-resource"></a>取得資源

ProductStore API 會公開數個 &quot;讀取&quot; 動作作為 HTTP GET 方法。 每個動作都會對應至 `ProductsController` 類別中的方法。

| 動作 | HTTP 方法 | 相對 URI |
| --- | --- | --- |
| 取得所有產品的清單 | GET | /api/products |
| 依識別碼取得產品 | GET | /api/products/*識別碼* |
| 依類別取得產品 | GET | /api/products？ category =*category* |

若要取得所有產品的清單，請將下列方法新增至 `ProductsController` 類別：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample6.cs)]

方法名稱的開頭為 &quot;取得&quot;，因此依照慣例，它會對應至 GET 要求。 此外，因為方法沒有參數，所以它會對應到路徑中不包含 *&quot;識別碼&quot;* 區段的 URI。

若要依識別碼取得產品，請將下列方法新增至 `ProductsController` 類別：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample7.cs)]

這個方法名稱也是以 &quot;Get&quot;開頭，但方法具有名為*id*的參數。這個參數會對應至 URI 路徑的 &quot;識別碼&quot; 區段。 ASP.NET Web API 架構會自動將識別碼轉換為參數的正確資料類型（**int**）。

如果*識別碼*無效，GetProduct 方法會擲回**HttpResponseException**類型的例外狀況。 架構會將此例外狀況轉譯為404（找不到）錯誤。

最後，新增方法以依類別尋找產品：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample8.cs)]

如果要求 URI 有查詢字串，Web API 會嘗試將查詢參數與控制器方法上的參數比對。 因此，"api/products？ category =*category*" 格式的 URI 會對應至此方法。

## <a name="creating-a-resource"></a>建立資源

接下來，我們會將方法新增至 `ProductsController` 類別，以建立新的產品。 以下是方法的簡單執行：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample9.cs)]

請注意這種方法的兩個相關事項：

- 方法名稱是以 &quot;Post ...&quot;開頭。 若要建立新的產品，用戶端會傳送 HTTP POST 要求。
- 方法會使用產品類型的參數。 在 Web API 中，具有複雜類型的參數會從要求主體還原序列化。 因此，我們預期用戶端會以 XML 或 JSON 格式傳送產品物件的序列化標記法。

此實作為可行的，但不是完全一樣。 在理想的情況下，我們希望 HTTP 回應包含下列內容：

- **回應碼：** 根據預設，Web API 架構會將回應狀態碼設定為200（確定）。 但是根據 HTTP/1.1 通訊協定，當 POST 要求導致資源的建立時，伺服器應該會回復狀態201（已建立）。
- **位置：** 當伺服器建立資源時，它應該在回應的位置標頭中包含新資源的 URI。

ASP.NET Web API 可讓您輕鬆地操作 HTTP 回應訊息。 以下是改良的執行：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample10.cs)]

請注意，方法傳回類型現在是**HttpResponseMessage**。 藉由傳回**HttpResponseMessage**而不是產品，我們可以控制 HTTP 回應訊息的詳細資料，包括狀態碼和位置標頭。

**CreateResponse**方法會建立**HttpResponseMessage** ，並自動將產品物件的序列化表示寫入回應訊息的本文中。

> [!NOTE]
> 這個範例不會驗證 `Product`。 如需模型驗證的相關資訊，請參閱[ASP.NET Web API 中的模型驗證](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)。

## <a name="updating-a-resource"></a>更新資源

使用 PUT 來更新產品非常簡單：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample11.cs)]

方法名稱是以 &quot;Put ...&quot;開頭，因此 Web API 會與它相符以提出要求。 方法會採用兩個參數：產品識別碼和更新的產品。 *識別碼*參數取自 URI 路徑，而*product*參數則會從要求主體還原序列化。 根據預設，ASP.NET Web API 架構會從要求主體中的路由和複雜類型取得簡單的參數類型。

## <a name="deleting-a-resource"></a>刪除資源

若要刪除資源，請定義「刪除 ...」方法.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample12.cs)]

如果 DELETE 要求成功，它會傳回狀態200（確定）與描述狀態的實體主體。狀態202（已接受），如果刪除仍待決;或沒有實體主體的狀態204（沒有內容）。 在此情況下，`DeleteProduct` 方法會有 `void` 傳回型別，因此 ASP.NET Web API 會自動將此轉譯為狀態碼204（沒有內容）。
