---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
title: 使用 Web API 2 支援 OData v3 中的實體關聯 |Microsoft Docs
author: MikeWasson
description: 大部分的資料集會定義實體之間的關聯性：客戶具有訂單;書籍有作者;產品有供應商。 使用 OData 時，用戶端可以流覽 。
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 1e4c2eb4-b6cf-42ff-8a65-4d71ddca0394
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
msc.type: authoredcontent
ms.openlocfilehash: 726a7d51123805e05f6831ef9cd7eaa84b6c44bd
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600305"
---
# <a name="supporting-entity-relations-in-odata-v3-with-web-api-2"></a>使用 Web API 2 支援 OData v3 中的實體關聯

由[Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> 大部分的資料集會定義實體之間的關聯性：客戶具有訂單;書籍有作者;產品有供應商。 使用 OData 時，用戶端可以流覽實體關聯。 提供產品之後，您就可以找到供應商。 您也可以建立或移除關聯性。 例如，您可以設定產品的供應商。
> 
> 本教學課程說明如何在 ASP.NET Web API 中支援這些作業。 本教學課程是[以使用 WEB API 2 建立 OData V3 端點](creating-an-odata-endpoint.md)教學課程為基礎。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - Web API 2
> - OData 第3版
> - Entity Framework 6

## <a name="add-a-supplier-entity"></a>新增供應商實體

首先，我們需要將新的實體類型新增至我們的 OData 摘要。 我們會新增 `Supplier` 類別。

[!code-csharp[Main](working-with-entity-relations/samples/sample1.cs)]

此類別使用實體索引鍵的字串。 實際上，這可能比使用整數索引鍵少。 但是，值得一提的是，OData 如何處理其他金鑰類型，但整數除外。

接下來，我們將藉由將 `Supplier` 屬性新增至 `Product` 類別來建立關聯性：

[!code-csharp[Main](working-with-entity-relations/samples/sample2.cs)]

將新的**DbSet**加入 `ProductServiceContext` 類別，使 Entity Framework 將在資料庫中包含 `Supplier` 資料表。

[!code-csharp[Main](working-with-entity-relations/samples/sample3.cs?highlight=9)]

在 WebApiConfig.cs 中，將「供應商」實體新增至 EDM 模型：

[!code-csharp[Main](working-with-entity-relations/samples/sample4.cs?highlight=4)]

## <a name="navigation-properties"></a>導覽屬性

若要取得產品的供應商，用戶端會傳送 GET 要求：

[!code-console[Main](working-with-entity-relations/samples/sample5.cmd)]

這裡的「供應商」是 `Product` 類型的導覽屬性。 在此情況下，`Supplier` 指的是單一專案，但導覽屬性也可以傳回集合（一對多或多對多關聯性）。

若要支援此要求，請將下列方法新增至 `ProductsController` 類別：

[!code-csharp[Main](working-with-entity-relations/samples/sample6.cs)]

*金鑰*參數是產品的索引鍵。 此方法會傳回相關實體&#8212;，在此案例中為 `Supplier` 實例。 方法名稱和參數名稱都很重要。 一般而言，如果導覽屬性的名稱為 "X"，您就必須加入名為 "GetX" 的方法。 此方法必須採用名為 "*key*" 的參數，以符合父系索引鍵的資料類型。

此外，在*key*參數中包含 **[FromOdataUri]** 屬性也很重要。 這個屬性會告知 Web API 在從要求 URI 剖析金鑰時，使用 OData 語法規則。

## <a name="creating-and-deleting-links"></a>建立和刪除連結

OData 支援建立或移除兩個實體之間的關聯性。 在 OData 術語中，關聯性是「連結」。 每個連結都有一個具有*entity*/$links/*實體*格式的 URI。 例如，從產品到供應商的連結看起來像這樣：

[!code-console[Main](working-with-entity-relations/samples/sample7.cmd)]

若要建立新的連結，用戶端會將 POST 要求傳送至連結 URI。 要求的主體是目標實體的 URI。 例如，假設有一個具有索引鍵 "CTSO" 的供應商。 若要建立從「產品（1）」到「供應商（' CTSO '）」的連結，用戶端會傳送如下所示的要求：

[!code-console[Main](working-with-entity-relations/samples/sample8.cmd)]

若要刪除連結，用戶端會將刪除要求傳送至連結 URI。

**建立連結**

若要讓用戶端建立產品供應商連結，請將下列程式碼新增至 `ProductsController` 類別：

[!code-csharp[Main](working-with-entity-relations/samples/sample9.cs)]

此方法採用三個參數：

- *金鑰*：父實體的金鑰（產品）
- *navigationProperty*：導覽屬性的名稱。 在此範例中，唯一有效的導覽屬性是「供應商」。
- *連結*：相關實體的 OData URI。 此值取自要求主體。 例如，連結 URI 可能是 "`http://localhost/odata/Suppliers('CTSO')`，表示識別碼 = ' CTSO ' 的供應商。

方法會使用連結來查閱供應商。 如果找到相符的供應商，方法會設定 `Product.Supplier` 屬性，並將結果儲存至資料庫。

最困難的部分是剖析連結 URI。 基本上，您需要模擬將 GET 要求傳送至該 URI 的結果。 下列 helper 方法說明如何執行這項操作。 方法會叫用 Web API 路由進程，並取得代表已剖析 OData 路徑的**ODataPath**實例。 若為連結 URI，其中一個區段應該是實體索引鍵。 （如果不是，用戶端傳送了錯誤的 URI）。

[!code-csharp[Main](working-with-entity-relations/samples/sample10.cs)]

**刪除連結**

若要刪除連結，請將下列程式碼新增至 `ProductsController` 類別：

[!code-csharp[Main](working-with-entity-relations/samples/sample11.cs)]

在此範例中，導覽屬性是單一 `Supplier` 實體。 如果導覽屬性是集合，則要刪除連結的 URI 必須包含相關實體的索引鍵。 例如：

[!code-console[Main](working-with-entity-relations/samples/sample12.cmd)]

此要求會移除客戶1的訂單1。 在此情況下，DeleteLink 方法會具有下列簽章：

[!code-csharp[Main](working-with-entity-relations/samples/sample13.cs)]

*RelatedKey*參數會提供相關實體的索引鍵。 因此，在您的 `DeleteLink` 方法中，請依索引*鍵*參數查閱主要實體、依*relatedKey*參數尋找相關實體，然後移除關聯。 根據您的資料模型，您可能需要同時執行這兩個版本的 `DeleteLink`。 Web API 會根據要求 URI 來呼叫正確的版本。
