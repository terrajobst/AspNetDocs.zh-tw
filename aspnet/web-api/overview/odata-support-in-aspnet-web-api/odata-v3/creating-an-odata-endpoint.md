---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
title: 使用 Web API 2 建立 OData v3 端點 |Microsoft Docs
author: MikeWasson
description: 開放式資料通訊協定（OData）是 web 的資料存取通訊協定。 OData 提供統一的方式來結構資料、查詢資料，以及運算元據 。
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 262843d6-43a2-4f1c-82d9-0b90ae6df0cf
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
msc.type: authoredcontent
ms.openlocfilehash: e68a454398f109dfd089be9c9a44d3fe662acc2f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556410"
---
# <a name="creating-an-odata-v3-endpoint-with-web-api-2"></a>使用 Web API 2 建立 OData v3 端點

由[Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> [開放式資料通訊協定](http://www.odata.org/)（OData）是 web 的資料存取通訊協定。 OData 提供統一的方式來結構資料、查詢資料，以及透過 CRUD 作業（建立、讀取、更新和刪除）來運算元據集。 OData 同時支援 AtomPub （XML）和 JSON 格式。 OData 也會定義公開資料相關中繼資料的方式。 用戶端可以使用中繼資料來探索資料集的類型資訊和關聯性。
>
> ASP.NET Web API 可讓您輕鬆地建立資料集的 OData 端點。 您可以完全控制端點所支援的 OData 作業。 您可以將多個 OData 端點與非 OData 端點一起裝載。 您可以完全掌控您的資料模型、後端商務邏輯和資料層。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - Web API 2
> - OData 第3版
> - Entity Framework 6
> - [Fiddler Web 調試的 Proxy （選擇性）](http://www.fiddler2.com)
>
> 已在[ASP.NET 和 Web 工具2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=282650)中新增 Web API OData 支援。 不過，本教學課程使用 Visual Studio 2013 中新增的樣板。

在本教學課程中，您將建立用戶端可以查詢的簡單 OData 端點。 您也會建立端點C#的用戶端。 完成本教學課程之後，下一組教學課程會示範如何新增更多功能，包括實體關聯、動作和 $expand/$select。

- [建立 Visual Studio 專案](#create-project)
- [新增實體模型](#add-model)
- [新增 OData 控制器](#add-controller)
- [加入 EDM 和 Route](#edm)
- [植入資料庫（選擇性）](#seed-db)
- [探索 OData 端點](#explore)
- [OData 序列化格式](#formats)

<a id="create-project"></a>
## <a name="create-the-visual-studio-project"></a>建立 Visual Studio 專案

在本教學課程中，您將建立支援基本 CRUD 作業的 OData 端點。 端點會公開單一資源，也就是一份產品清單。 稍後的教學課程會新增更多功能。

啟動 Visual Studio，然後從 [開始] 頁面選取 [**新增專案**]。 或者，**從 [檔案**] 功能表選取 [**新增**]，然後選取 [**專案**]。

在 [**範本**] 窗格中，選取 [**已安裝**的C#範本]，然後展開視覺效果節點。 在 **[ C#視覺效果**] 底下，選取 [ **Web**]。 選取 **[ASP.NET Web 應用程式**] 範本。

![](creating-an-odata-endpoint/_static/image1.png)

在 [**新增 ASP.NET 專案**] 對話方塊中，選取 [**空白**] 範本。 在 [&quot;新增&quot;的資料夾和核心參考] 底下，檢查 [ **WEB API**]。 按一下 [確定]。

![](creating-an-odata-endpoint/_static/image2.png)

<a id="add-model"></a>
## <a name="add-an-entity-model"></a>新增實體模型

「模型」是代表應用程式中資料的物件。 在本教學課程中，我們需要代表產品的模型。 模型會對應至我們的 OData 實體類型。

在 [方案總管] 中，於 Models 資料夾上按一下滑鼠右鍵。 從操作功能表中，選取 [新增]，然後選取 [類別]。

![](creating-an-odata-endpoint/_static/image3.png)

在 [**加入新**專案] 對話方塊中，將類別命名為 &quot;產品&quot;。

![](creating-an-odata-endpoint/_static/image4.png)

> [!NOTE]
> 依照慣例，模型類別會放在 [模型] 資料夾中。 您不需要在自己的專案中遵循此慣例，但我們將在本教學課程中使用它。

在 Product.cs 檔案中，新增下列類別定義：

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample1.cs)]

ID 屬性將會是實體索引鍵。 用戶端可以依識別碼查詢產品。 此欄位也會是後端資料庫中的主要金鑰。

立即建立專案。 在下一個步驟中，我們將使用一些使用反映的 Visual Studio 樣板來尋找產品類型。

<a id="add-controller"></a>
## <a name="add-an-odata-controller"></a>新增 OData 控制器

*控制器*是處理 HTTP 要求的類別。 您可以針對 OData 服務中的每個實體集定義個別的控制器。 在本教學課程中，我們將建立單一控制器。

在方案總管中，以滑鼠右鍵按一下 [控制器] 資料夾。 選取 [新增]，然後選取 [控制器]。

![](creating-an-odata-endpoint/_static/image5.png)

在 **新增 Scaffold**  對話方塊中，選取 使用 Entity Framework&quot;&quot;具有動作的 Web API 2 OData 控制器。

![](creating-an-odata-endpoint/_static/image6.png)

在 [**新增控制器**] 對話方塊中，將控制器命名為 "productscontroller.cs"。 選取 [&quot;使用非同步控制器動作&quot;] 核取方塊。 在 [**模型**] 下拉式清單中，選取 [Product] 類別。

![](creating-an-odata-endpoint/_static/image7.png)

按一下 [**新增資料內容 ...** ] 按鈕。 保留 [資料內容類型] 的預設名稱，然後按一下 [**新增**]。

![](creating-an-odata-endpoint/_static/image8.png)

按一下 [新增控制器] 對話方塊中的 [新增]，以新增控制器。

![](creating-an-odata-endpoint/_static/image9.png)

注意：如果您收到錯誤訊息，指出 &quot;取得類型 ...&quot;時發生錯誤，請確定您在新增 Product 類別之後，已建立 Visual Studio 專案。 此樣板會使用反映來尋找類別。

![](creating-an-odata-endpoint/_static/image10.png)

此架構會將兩個程式碼檔案加入至專案：

- Products.cs 會定義用來執行 OData 端點的 Web API 控制器。
- ProductServiceCoNtext.cs 提供使用 Entity Framework 查詢基礎資料庫的方法。

![](creating-an-odata-endpoint/_static/image11.png)

<a id="edm"></a>
## <a name="add-the-edm-and-route"></a>加入 EDM 和 Route

在方案總管中，展開應用程式\_開始 資料夾，然後開啟名為 WebApiConfig.cs 的檔案。 此類別會保存 Web API 的設定程式碼。 將此程式碼取代為下列內容：

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample2.cs)]

這段程式碼會執行兩項工作：

- 建立 OData 端點的實體資料模型（EDM）。
- 加入端點的路由。

EDM 是資料的抽象模型。 EDM 是用來建立元資料檔案，並定義服務的 Uri。 **ODataConventionModelBuilder**會使用一組預設的命名慣例 edm 來建立 EDM。 這種方法需要最少的程式碼。 如果您想要更充分掌控 EDM，您可以使用**用**類別來明確地新增屬性、索引鍵和導覽屬性來建立 edm。

**EntitySet**方法會將實體集加入至 EDM：

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample3.cs)]

"Products" 字串會定義實體集的名稱。 控制器的名稱必須符合實體集的名稱。 在本教學課程中，實體集命名為 "Products"，而控制器的名稱為 `ProductsController`。 如果您將實體集命名為 "ProductSet"，則會將控制器命名為 `ProductSetController`。 請注意，端點可以有多個實體集。 針對每個實體集呼叫**EntitySet&lt;t&gt;** ，然後定義對應的控制器。

**MapODataRoute**方法會加入 OData 端點的路由。

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample4.cs)]

第一個參數是路由的易記名稱。 您服務的用戶端看不到此名稱。 第二個參數是端點的 URI 前置詞。 假設有此程式碼，Products 實體集的 URI 為 HTTP://<em>hostname</em>/odata/Products。 您的應用程式可以有一個以上的 OData 端點。 針對每個端點，呼叫<strong>MapODataRoute</strong>並提供唯一的路由名稱和唯一的 URI 前置詞。

<a id="seed-db"></a>
## <a name="seed-the-database-optional"></a>植入資料庫（選擇性）

在此步驟中，您將使用 Entity Framework 來植入具有一些測試資料的資料庫。 此步驟是選擇性的，但可讓您立即測試您的 OData 端點。

從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。 在 [Package Manager Console] 視窗中，輸入下列命令：

[!code-console[Main](creating-an-odata-endpoint/samples/sample5.cmd)]

這會新增名為「遷移」的資料夾和名為 Configuration.cs 的程式碼檔案。

![](creating-an-odata-endpoint/_static/image12.png)

開啟此檔案，並將下列程式碼新增至 `Configuration.Seed` 方法。

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample6.cs)]

在 [套件管理員主控台] 視窗中，輸入下列命令：

[!code-console[Main](creating-an-odata-endpoint/samples/sample7.cmd)]

這些命令會產生建立資料庫的程式碼，然後執行該程式碼。

<a id="explore"></a>
## <a name="exploring-the-odata-endpoint"></a>探索 OData 端點

在本節中，我們將使用[Fiddler Web 調試的 Proxy](http://www.fiddler2.com) ，將要求傳送至端點，並檢查回應訊息。 這可協助您瞭解 OData 端點的功能。

在 Visual Studio 中，按 F5 開始進行調試。 根據預設，Visual Studio 會開啟您的瀏覽器以 `http://localhost:*port*`，其中*port*是在專案設定中設定的埠號碼。

您可以在專案設定中變更埠號碼。 在方案總管中，以滑鼠右鍵按一下專案，然後選取 [**屬性**]。 在 [屬性] 視窗中，選取 [ **Web**]。 在 [**專案 Url**] 底下輸入埠號碼。

### <a name="service-document"></a>服務檔

*服務檔*包含 OData 端點的實體集清單。 若要取得服務檔，請將 GET 要求傳送至服務的根 URI。

使用 Fiddler，在 [**編輯器**] 索引標籤中輸入下列 URI： [`http://localhost:port/odata/`]，其中*port*是埠號碼。

![](creating-an-odata-endpoint/_static/image13.png)

按一下 [執行] 按鈕。 Fiddler 會將 HTTP GET 要求傳送至您的應用程式。 您應該會在 [Web 會話] 清單中看到回應。 如果所有專案都正常運作，狀態碼將會是200。

![](creating-an-odata-endpoint/_static/image14.png)

在 [Web 會話] 清單中按兩下回應，以在 [偵測器] 索引標籤中查看回應訊息的詳細資料。

![](creating-an-odata-endpoint/_static/image15.png)

原始 HTTP 回應訊息看起來應該如下所示：

[!code-console[Main](creating-an-odata-endpoint/samples/sample8.cmd)]

根據預設，Web API 會以 AtomPub 格式傳回服務檔。 若要要求 JSON，請將下列標頭新增至 HTTP 要求：

`Accept: application/json`

![](creating-an-odata-endpoint/_static/image16.png)

現在 HTTP 回應包含 JSON 承載：

[!code-console[Main](creating-an-odata-endpoint/samples/sample9.cmd)]

### <a name="service-metadata-document"></a>服務元資料檔案

*服務元資料檔案*會使用稱為概念結構定義語言（CSDL）的 XML 語言來描述服務的資料模型。 元資料檔案會顯示服務中的資料結構，而且可用來產生用戶端程式代碼。

若要取得元資料檔案，請將 GET 要求傳送至 `http://localhost:port/odata/$metadata`。 以下是本教學課程中所顯示之端點的中繼資料。

[!code-console[Main](creating-an-odata-endpoint/samples/sample10.cmd)]

### <a name="entity-set"></a>實體集

若要取得 Products 實體集，請將 GET 要求傳送至 `http://localhost:port/odata/Products`。

[!code-console[Main](creating-an-odata-endpoint/samples/sample11.cmd)]

### <a name="entity"></a>實體

若要取得個別產品，請將 GET 要求傳送至 `http://localhost:port/odata/Products(1)`，其中 "1" 是產品識別碼。

[!code-console[Main](creating-an-odata-endpoint/samples/sample12.cmd)]

<a id="formats"></a>
## <a name="odata-serialization-formats"></a>OData 序列化格式

OData 支援數種序列化格式：

- Atom Pub （XML）
- JSON 「light」（在 OData v3 中引進）
- JSON 「詳細資訊」（OData v2）

根據預設，Web API 會使用 AtomPubJSON "light" 格式。

若要取得 AtomPub 格式，請將 Accept 標頭設為 "application/atom + xml"。 下列為回應本文的範例：

[!code-console[Main](creating-an-odata-endpoint/samples/sample13.cmd)]

您可以看到 Atom 格式的一個明顯缺點：比 JSON 光線更多的詳細資訊。 不過，如果您有了解 AtomPub 的用戶端，用戶端可能會偏好該格式超過 JSON。

以下是相同實體的 JSON light 版本：

[!code-console[Main](creating-an-odata-endpoint/samples/sample14.cmd)]

JSON light 格式是在 OData 通訊協定的第3版中引進。 為了回溯相容性，用戶端可以要求較舊的「詳細資訊」 JSON 格式。 若要要求詳細資訊 JSON，請將 Accept 標頭設為 `application/json;odata=verbose`。 詳細資訊版本如下：

[!code-console[Main](creating-an-odata-endpoint/samples/sample15.cmd)]

此格式會在回應本文中傳達更多的中繼資料，這可能會在整個會話上增加相當大的負擔。 此外，它也會將物件包裝在名為 "d" 的屬性中，藉此加入間接取值層級。

## <a name="next-steps"></a>後續步驟

- [新增實體關聯](working-with-entity-relations.md)
- [新增 OData 動作](odata-actions.md)
- [從 .NET 用戶端呼叫 OData 服務](calling-an-odata-service-from-a-net-client.md)
