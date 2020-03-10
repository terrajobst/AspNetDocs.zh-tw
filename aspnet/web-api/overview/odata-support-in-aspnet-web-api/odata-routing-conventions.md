---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
title: ASP.NET Web API 2 Odata 中的路由慣例-ASP.NET 4。x
author: MikeWasson
description: 描述 ASP.NET 4.x 中的 Web API 2 用於 OData 端點的路由慣例。
ms.author: riande
ms.date: 07/31/2013
ms.custom: seoapril2019
ms.assetid: adbc175a-14eb-4ab2-a441-d056ffa8266f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
msc.type: authoredcontent
ms.openlocfilehash: 63df4a82cd8df92631485b2544117844cfd0ca56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614713"
---
# <a name="routing-conventions-in-aspnet-web-api-2-odata"></a>ASP.NET Web API 2 Odata 中的路由慣例

由[Mike Wasson](https://github.com/MikeWasson)

> 本文說明 ASP.NET 4.x 中的 Web API 2 用於 OData 端點的路由慣例。

當 Web API 取得 OData 要求時，它會將要求對應至控制器名稱和動作名稱。 對應是以 HTTP 方法和 URI 為基礎。 例如，`GET /odata/Products(1)` 對應至 `ProductsController.GetProduct`。

在本文的第1部分中，我將說明內建的 OData 路由慣例。 這些慣例是特別針對 OData 端點所設計，而且它們會取代預設的 Web API 路由系統。 （當您呼叫**MapODataRoute**時，就會發生取代）。

在第2部分中，我會示範如何新增自訂路由慣例。 目前內建慣例並不涵蓋整個範圍的 OData Uri，但您可以擴充它們來處理其他案例。

- [內建路由慣例](#conventions)
- [自訂路由慣例](#custom)

<a id="conventions"></a>
## <a name="built-in-routing-conventions"></a>內建路由慣例

在我描述 Web API 中的 OData 路由慣例之前，瞭解 OData Uri 會很有説明。 [ODATA URI](http://www.odata.org/documentation/odata-v3-documentation/url-conventions/)是由下列各項所組成：

- 服務根目錄
- 資源路徑
- 查詢選項

![](odata-routing-conventions/_static/image1.png)

針對路由，重要的部分是資源路徑。 資源路徑會分割成區段。 例如，`/Products(1)/Supplier` 有三個區段：

- `Products` 指的是名為 "Products" 的實體集。
- `1` 是實體索引鍵，可從集合中選取單一實體。
- `Supplier` 是選取相關實體的導覽屬性。

因此，此路徑會挑選產品1的供應商。

> [!NOTE]
> OData 路徑區段不一定會對應到 URI 區段。 例如，"1" 視為路徑區段。

**控制器名稱。** 控制器名稱一律衍生自資源路徑根目錄的實體集。 例如，如果資源路徑是 `/Products(1)/Supplier`，Web API 會尋找名為 `ProductsController`的控制器。

**動作名稱。** 動作名稱衍生自路徑區段，再加上 entity data model （EDM），如下表所列。 在某些情況下，您有兩個動作名稱的選擇。 例如，"Get" 或 &quot;GetProducts&quot;。

**查詢實體**

| 要求 | 範例 URI | 動作名稱 | 範例動作 |
| --- | --- | --- | --- |
| 取得/entityset | /Products | GetEntitySet 或 Get | GetProducts |
| 取得/entityset （索引鍵） | /Products （1） | GetEntityType 或 Get | GetProduct |
| 取得/entityset （金鑰）/cast | /Products （1）/Models.Book | GetEntityType 或 Get | GetBook |

如需詳細資訊，請參閱[建立唯讀 OData 端點](odata-v3/creating-an-odata-endpoint.md)。

**建立、更新和刪除實體**

| 要求 | 範例 URI | 動作名稱 | 範例動作 |
| --- | --- | --- | --- |
| 張貼/entityset | /Products | PostEntityType 或 Post | PostProduct |
| PUT/entityset （索引鍵） | /Products （1） | PutEntityType 或 Put | PutProduct |
| PUT/entityset （key）/cast | /Products （1）/Models.Book | PutEntityType 或 Put | PutBook |
| 修補程式/entityset （金鑰） | /Products （1） | PatchEntityType 或修補程式 | PatchProduct |
| PATCH/entityset （金鑰）/cast | /Products （1）/Models.Book | PatchEntityType 或修補程式 | PatchBook |
| 刪除/entityset （索引鍵） | /Products （1） | DeleteEntityType 或刪除 | DeleteProduct |
| 刪除/entityset （金鑰）/cast | /Products （1）/Models.Book | DeleteEntityType 或刪除 | DeleteBook |

**查詢導覽屬性**

| 要求 | 範例 URI | 動作名稱 | 範例動作 |
| --- | --- | --- | --- |
| 取得/entityset （金鑰）/navigation | /Products （1）/Supplier | GetNavigationFromEntityType 或 GetNavigation | GetSupplierFromProduct |
| 取得/entityset （金鑰）/cast/navigation | /Products （1）/Models.Book/Author | GetNavigationFromEntityType 或 GetNavigation | GetAuthorFromBook |

如需詳細資訊，請參閱[使用實體](odata-v3/working-with-entity-relations.md)關聯。

**建立和刪除連結**

| 要求 | 範例 URI | 動作名稱 |
| --- | --- | --- |
| POST/entityset （金鑰）/$links/navigation | /Products （1）/$links/Supplier | CreateLink |
| PUT/entityset （key）/$links/navigation | /Products （1）/$links/Supplier | CreateLink |
| 刪除/entityset （key）/$links/navigation | /Products （1）/$links/Supplier | DeleteLink |
| DELETE/entityset （key）/$links/navigation （relatedKey） | /Products/（1）/$links/Suppliers （1） | DeleteLink |

如需詳細資訊，請參閱[使用實體](odata-v3/working-with-entity-relations.md)關聯。

**內容**

*需要 Web API 2*

| 要求 | 範例 URI | 動作名稱 | 範例動作 |
| --- | --- | --- | --- |
| 取得/entityset （金鑰）/property | /Products （1）/Name | GetPropertyFromEntityType 或 GetProperty | GetNameFromProduct |
| 取得/entityset （金鑰）/cast/property | /Products （1）/Models.Book/Author | GetPropertyFromEntityType 或 GetProperty | GetTitleFromBook |

**動作**

| 要求 | 範例 URI | 動作名稱 | 範例動作 |
| --- | --- | --- | --- |
| POST/entityset （金鑰）/action | /Products （1）/Rate | ActionNameOnEntityType 或 ActionName | RateOnProduct |
| POST/entityset （金鑰）/cast/action | /Products （1）/Models.Book/CheckOut | ActionNameOnEntityType 或 ActionName | CheckOutOnBook |

如需詳細資訊，請參閱[OData 動作](odata-v3/odata-actions.md)。

**方法簽章**

以下是方法簽章的一些規則：

- 如果路徑包含索引鍵，則動作應該具有名為*key*的參數。
- 如果路徑在導覽屬性中包含索引鍵，動作應該會有一個名為*relatedKey*的參數。
- 使用 **[FromODataUri]** 參數裝飾索引*鍵*和*relatedKey*參數。
- POST 和 PUT 要求會採用實體類型的參數。
- PATCH 要求接受類型**Delta&lt;t&gt;** 的參數，其中*t*是實體類型。

如需參考，以下範例顯示每個內建 OData 路由慣例的方法簽章。

[!code-csharp[Main](odata-routing-conventions/samples/sample1.cs)]

<a id="custom"></a>
## <a name="custom-routing-conventions"></a>自訂路由慣例

目前內建慣例並不涵蓋所有可能的 OData Uri。 您可以藉由執行**IODataRoutingConvention**介面來加入新的慣例。 這個介面有兩種方法：

[!code-csharp[Main](odata-routing-conventions/samples/sample2.cs)]

- **SelectController**會傳回控制器的名稱。
- **SelectAction**會傳回動作的名稱。

對於這兩種方法，如果慣例不適用於該要求，此方法應該會傳回 null。

**ODataPath**參數代表已剖析的 OData 資源路徑。 其中包含 **[ODataPathSegment](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatapathsegment.aspx)** 實例的清單，每個資源路徑的區段各一個。 **ODataPathSegment**是抽象類別;每個區段類型都是由衍生自**ODataPathSegment**的類別表示。

**ODataPath. TemplatePath**屬性是一個字串，表示串連所有路徑區段。 例如，如果 URI 為 `/Products(1)/Supplier`，則路徑範本會 &quot;~/entityset/key/navigation&quot;。 請注意，區段不會直接對應到 URI 區段。 例如，實體索引鍵（1）會表示為其本身的**ODataPathSegment**。

一般來說， **IODataRoutingConvention**的執行會執行下列動作：

1. 比較路徑範本，以查看此慣例是否適用于目前的要求。 如果不適用，則傳回 null。
2. 如果套用慣例，請使用**ODataPathSegment**實例的屬性來衍生控制器和動作名稱。
3. 針對 [動作]，將任何值新增至應系結至動作參數（通常是實體索引鍵）的路由字典。

讓我們來看一個特定的範例。 內建路由慣例不支援在導覽集合中編制索引。 換句話說，Uri 沒有任何慣例，如下所示：

[!code-javascript[Main](odata-routing-conventions/samples/sample3.js)]

以下是用來處理這種查詢類型的自訂路由慣例。

[!code-csharp[Main](odata-routing-conventions/samples/sample4.cs)]

附註：

1. 我衍生自**EntitySetRoutingConvention**，因為該類別中的**SelectController**方法適用于這個新的路由慣例。 這表示我不需要重新執行**SelectController**。
2. 此慣例僅適用于 GET 要求，而且只有在路徑範本是 &quot;~/entityset/key/navigation/key&quot;時。
3. 動作名稱是 &quot;Get {EntityType}&quot;，其中 *{entitytype}* 是導覽集合的類型。 例如，&quot;GetSupplier&quot;。 您可以使用任何您喜歡&#8212;的命名慣例，以確保您的控制器動作符合。
4. 此動作會接受名為*key*和*relatedKey*的兩個參數。 （如需一些預先定義之參數名稱的清單，請參閱[ODataRouteConstants](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatarouteconstants.aspx)）。

下一個步驟是將新的慣例加入至路由慣例清單。 這會在設定期間發生，如下列程式碼所示：

[!code-csharp[Main](odata-routing-conventions/samples/sample5.cs)]

以下是一些有助於研究的其他範例路由慣例：

- [CompositeKeyRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataCompositeKeySample/ODataCompositeKeySample/Extensions/CompositeKeyRoutingConvention.cs)
- [CustomNavigationRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataServiceSample/ODataService/Extensions/CustomNavigationRoutingConvention.cs)
- [NonBindableActionRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataActionsSample/ODataActionsSample/NonBindableActionRoutingConvention.cs)
- [ODataVersionRouteConstraint](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataVersioningSample/ODataVersioningSample/Extensions/ODataVersionRouteConstraint.cs)

而 Web API 本身是開放原始碼，因此您可以看到內建路由慣例的[原始程式碼](http://aspnetwebstack.codeplex.com/)。 這些是在 System.web. **HTTP.sys**命名空間中定義。
