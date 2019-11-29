---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
title: 第2部分：建立領域模型 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: fe3ef85f-bdc6-4e10-9768-25aa565c01d0
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
msc.type: authoredcontent
ms.openlocfilehash: 7c5ed1bdb4b390c94907b14e208231f16ad42d96
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600364"
---
# <a name="part-2-creating-the-domain-models"></a>第2部分：建立領域模型

由[Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-models"></a>加入模型

有三種方法可以 Entity Framework：

- Database-首先：您會開始使用資料庫，而 Entity Framework 會產生程式碼。
- 模型優先：從視覺模型開始，Entity Framework 會產生資料庫和程式碼。
- 程式碼優先：開始使用程式碼，Entity Framework 產生資料庫。

我們使用的是程式碼優先方法，因此我們一開始會將網域物件定義為 Poco （純舊的 CLR 物件）。 透過程式碼優先方法，網域物件不需要任何額外的程式碼來支援資料庫層，例如交易或持續性。 （具體而言，它們不需要繼承自[EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx)類別）。您仍然可以使用資料批註來控制 Entity Framework 如何建立資料庫架構。

由於 Poco 不會包含任何描述[資料庫狀態](https://msdn.microsoft.com/library/system.data.entitystate.aspx)的額外屬性，因此可以輕鬆地序列化為 JSON 或 XML。 不過，這並不表示您應該一律將 Entity Framework 模型直接公開給用戶端，如我們稍後在本教學課程中所見。

我們將建立下列 Poco：

- 產品
- 使用
- OrderDetail

若要建立每個類別，請以滑鼠右鍵按一下方案總管中的 [模型] 資料夾。 從內容功能表中，選取 [**新增**]，然後選取 [**類別]。**

![](using-web-api-with-entity-framework-part-2/_static/image1.png)

新增具有下列執行的 `Product` 類別：

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample1.cs)]

依照慣例，Entity Framework 會使用 `Id` 屬性作為主要索引鍵，並將它對應至資料庫資料表中的識別欄位。 當您建立新的 `Product` 實例時，您不會設定 `Id`的值，因為資料庫會產生值。

**ScaffoldColumn**屬性會在產生編輯器表單時，告訴 ASP.NET MVC 略過 `Id` 屬性。 **必要**的屬性是用來驗證模型。 它會指定 `Name` 屬性必須是非空白字串。

新增 `Order` 類別：

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample2.cs)]

新增 `OrderDetail` 類別：

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample3.cs)]

## <a name="foreign-key-relations"></a>外鍵關聯性

訂單包含許多訂單明細，而每個訂單詳細資料則是指單一產品。 為了表示這些關聯性，`OrderDetail` 類別會定義名為 `OrderId` 和 `ProductId`的屬性。 Entity Framework 會推斷這些屬性代表外鍵，而且會將外鍵條件約束加入至資料庫。

![](using-web-api-with-entity-framework-part-2/_static/image2.png)

`Order` 和 `OrderDetail` 類別也包含 "導覽" 屬性，其中包含相關物件的參考。 根據您的順序，您可以遵循導覽屬性，流覽至訂單中的產品。

立即編譯專案。 Entity Framework 會使用反映來探索模型的屬性，因此需要已編譯的元件來建立資料庫架構。

## <a name="configure-the-media-type-formatters"></a>設定媒體類型格式器

[媒體類型格式](../../formats-and-model-binding/media-formatters.md)器是一種物件，可在 Web API 寫入 HTTP 回應本文時，將您的資料序列化。 內建的格式器支援 JSON 和 XML 輸出。 根據預設，這兩個格式子都會以傳值方式序列化所有物件。

如果物件圖形包含迴圈參考，依值序列化會產生問題。 這就是 `Order` 和 `OrderDetail` 類別的情況，因為每個類別都有另一個參考。 格式器會遵循參考、以傳值方式寫入每個物件，然後進入圓圈。 因此，我們需要變更預設行為。

在方案總管中，展開應用程式\_開始 資料夾，然後開啟名為 WebApiConfig.cs 的檔案。 將下列程式碼加入 `WebApiConfig` 類別：

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample4.cs?highlight=11)]

這段程式碼會設定 JSON 格式器來保留物件參考，並從管線中移除 XML 格式器。 （您可以設定 XML 格式器來保留物件參考，但這是比較好的工作，而且我們只需要此應用程式的 JSON。 如需詳細資訊，請參閱[處理迴圈物件參考](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)。）

> [!div class="step-by-step"]
> [上一頁](using-web-api-with-entity-framework-part-1.md)
> [下一頁](using-web-api-with-entity-framework-part-3.md)
