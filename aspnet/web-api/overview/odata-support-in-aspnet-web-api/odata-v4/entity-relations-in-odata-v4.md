---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
title: 使用 ASP.NET Web API 2.2 的 OData v4 中的實體關聯 |Microsoft Docs
author: MikeWasson
description: 大部分的資料集會定義實體之間的關聯性：客戶具有訂單;書籍有作者;產品有供應商。 使用 OData 時，用戶端可以流覽 。
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 72657550-ec09-4779-9bfc-2fb15ecd51c7
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: fbafb2b2346689271905db5790cdddeeb809b070
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598690"
---
# <a name="entity-relations-in-odata-v4-using-aspnet-web-api-22"></a>使用 ASP.NET Web API 2.2 的 OData v4 中的實體關聯

由[Mike Wasson](https://github.com/MikeWasson)

> 大部分的資料集會定義實體之間的關聯性：客戶具有訂單;書籍有作者;產品有供應商。 使用 OData 時，用戶端可以流覽實體關聯。 提供產品之後，您就可以找到供應商。 您也可以建立或移除關聯性。 例如，您可以設定產品的供應商。
>
> 本教學課程說明如何使用 ASP.NET Web API 在 OData v4 中支援這些作業。 本教學課程是[以使用 ASP.NET Web API 2 建立 OData V4 端點](create-an-odata-v4-endpoint.md)教學課程為基礎。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
>
> - Web API 2。1
> - OData v4
> - Visual Studio 2013 （[在此](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)下載 Visual Studio 2017）
> - Entity Framework 6
> - .NET 4.5
>
> ## <a name="tutorial-versions"></a>教學課程版本
>
> 針對 OData 第3版，請參閱[支援 odata v3 中的實體](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations)關聯。

## <a name="add-a-supplier-entity"></a>新增供應商實體

> [!NOTE]
> 本教學課程是[以使用 ASP.NET Web API 2 建立 OData V4 端點](create-an-odata-v4-endpoint.md)教學課程為基礎。

首先，我們需要相關的實體。 在 [模型] 資料夾中，新增名為 `Supplier` 的類別。

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample1.cs)]

將導覽屬性新增至 `Product` 類別：

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample2.cs?highlight=13-15)]

將新的**DbSet**加入 `ProductsContext` 類別，使 Entity Framework 將在資料庫中包含供應商資料表。

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample3.cs?highlight=10)]

在 WebApiConfig.cs 中，將 &quot;供應商&quot; 實體集新增至實體資料模型：

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample4.cs?highlight=6)]

## <a name="add-a-suppliers-controller"></a>新增供應商控制器

將 `SuppliersController` 類別新增至 [控制器] 資料夾。

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample5.cs)]

我不會示範如何新增此控制器的 CRUD 作業。 這些步驟與產品控制器相同（請參閱[建立 OData V4 端點](create-an-odata-v4-endpoint.md)）。

## <a name="getting-related-entities"></a>取得相關實體

若要取得產品的供應商，用戶端會傳送 GET 要求：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample6.cmd)]

若要支援此要求，請將下列方法新增至 `ProductsController` 類別：

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample7.cs)]

這個方法會使用預設的命名慣例

- 方法名稱： GetX，其中 X 是導覽屬性。
- 參數名稱：*金鑰*

如果您遵循此命名慣例，Web API 會自動將 HTTP 要求對應至控制器方法。

範例 HTTP 要求：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample8.cmd)]

範例 HTTP 回應：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample9.cmd)]

### <a name="getting-a-related-collection"></a>取得相關集合

在上述範例中，產品有一個供應商。 導覽屬性也可以傳回集合。 下列程式碼會取得供應商的產品：

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample10.cs)]

在此情況下，方法會傳回**IQueryable** ，而不是**SingleResult&lt;t&gt;**

範例 HTTP 要求：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample11.cmd)]

範例 HTTP 回應：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample12.cmd)]

## <a name="creating-a-relationship-between-entities"></a>建立實體之間的關聯性

OData 支援建立或移除兩個現有實體之間的關聯性。 在 OData v4 術語中，關聯性是 &quot;的參考&quot;。 （在 OData v3 中，關聯性稱為「*連結*」。 此教學課程的通訊協定差異並不重要）。

參考有自己的 URI，格式為 `/Entity/NavigationProperty/$ref`。 例如，以下是用來處理產品和其供應商之間參考的 URI：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample13.cmd)]

若要加入關聯性，用戶端會將 POST 或 PUT 要求傳送至這個位址。

- 如果導覽屬性是單一實體（例如 `Product.Supplier`），則 PUT。
- 如果導覽屬性是集合（例如 `Supplier.Products`），則為 POST。

要求的主體包含關聯性中其他實體的 URI。 以下是範例要求：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample14.cmd)]

在此範例中，用戶端會將 PUT 要求傳送至 `/Products(6)/Supplier/$ref`，這是識別碼 = 6 之產品 `Supplier` 的 $ref URI。 如果要求成功，伺服器會傳送204（沒有內容）回應：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample15.cmd)]

以下是將關聯性新增至 `Product`的控制器方法：

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample16.cs)]

*NavigationProperty*參數會指定要設定的關聯性。 （如果實體上有一個以上的導覽屬性，您可以加入更多 `case` 語句）。

*連結*參數包含供應商的 URI。 Web API 會自動剖析要求主體，以取得此參數的值。

若要查閱供應商，我們需要識別碼（或金鑰），這是*連結*參數的一部分。 若要這麼做，請使用下列 helper 方法：

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample17.cs)]

基本上，這個方法會使用 OData 程式庫，將 URI 路徑分割成區段，找出包含索引鍵的區段，然後將索引鍵轉換成正確的型別。

## <a name="deleting-a-relationship-between-entities"></a>刪除實體之間的關聯性

若要刪除關聯性，用戶端會將 HTTP DELETE 要求傳送至 $ref URI：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample18.cmd)]

以下是用來刪除產品與供應商之間關聯性的控制器方法：

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample19.cs)]

在此情況下，`Product.Supplier` 是一對多關聯的 &quot;1&quot; 端，因此您只需將 `Product.Supplier` 設定為 [`null`]，即可移除關聯性。

在 &quot;關聯性的許多&quot; 端，用戶端必須指定要移除的相關實體。 若要這樣做，用戶端會在要求的查詢字串中傳送相關實體的 URI。 例如，若要從「供應商1」移除「產品1」：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample20.cmd?highlight=1)]

若要在 Web API 中支援這項功能，我們必須在 `DeleteRef` 方法中包含額外的參數。 以下是從 `Supplier.Products` 關聯移除產品的控制器方法。

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample21.cs)]

*金鑰*參數是供應商的金鑰，而*relatedKey*參數則是要從 `Products` 關聯性中移除之產品的索引鍵。 請注意，Web API 會自動從查詢字串取得金鑰。
