---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
title: 第6部分：建立產品和訂單控制器 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 91ee29ee-0689-40ee-914a-e7dd733b6622
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
msc.type: authoredcontent
ms.openlocfilehash: e0bf88e3477acbde910cde956042449bc86ce79a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600019"
---
# <a name="part-6-creating-product-and-order-controllers"></a>第6部分：建立產品和訂單控制器

由[Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-a-products-controller"></a>新增產品控制器

管理控制器是針對具有系統管理員許可權的使用者。 另一方面，客戶可以查看產品，但無法建立、更新或刪除它們。

我們可以輕鬆地限制對 Post、Put 和 Delete 方法的存取，同時讓 Get 方法保持開啟。 但請查看針對產品所傳回的資料：

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample1.json?highlight=1)]

客戶應該看不到 `ActualCost` 屬性！ 解決方法是定義*資料傳輸物件*（DTO），其中包含客戶應看到的屬性子集。 我們將使用 LINQ to project `Product` 實例來 `ProductDTO` 實例。

將名為 `ProductDTO` 的類別新增至 [模型] 資料夾。

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample2.cs)]

現在新增控制器。 在方案總管中，以滑鼠右鍵按一下 [控制器] 資料夾。 選取 [**新增**]，然後選取 [**控制器**]。 在 [**新增控制器**] 對話方塊中，將控制器命名為 &quot;productscontroller.cs&quot;。 在 [**範本**] 底下，選取 [**空的 API 控制器**]。

![](using-web-api-with-entity-framework-part-6/_static/image1.png)

使用下列程式碼取代原始程式檔中的所有專案：

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample3.cs)]

控制器仍然會使用 `OrdersContext` 來查詢資料庫。 但我們不會直接傳回 `Product` 實例，而是呼叫 `MapProducts` 將其投射至 `ProductDTO` 實例：

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample4.cs?highlight=1)]

`MapProducts` 方法會傳回**IQueryable**，因此我們可以使用其他查詢參數來撰寫結果。 您可以在 `GetProduct` 方法中看到這個，這會在查詢中加入**where**子句：

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample5.cs?highlight=2)]

## <a name="add-an-orders-controller"></a>新增訂單控制器

接下來，新增可讓使用者建立和查看訂單的控制器。

我們會從另一個 DTO 開始。 在方案總管中，以滑鼠右鍵按一下 [模型] 資料夾，然後新增名為 `OrderDTO` 的類別使用下列執行：

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample6.cs)]

現在新增控制器。 在方案總管中，以滑鼠右鍵按一下 [控制器] 資料夾。 選取 [**新增**]，然後選取 [**控制器**]。 在 [**新增控制器**] 對話方塊中，設定下列選項：

- 在 [**控制器名稱**] 下，輸入 "OrdersController"。
- 在 **範本** 底下，選取 具有讀取/寫入動作的 API 控制器，並使用 Entity Framework。
- 在 [**模型類別**] 下，選取 [&quot;順序] （ProductStore）&quot;。
- 在 [**資料內容類別**] 底下，選取 [&quot;OrdersCoNtext （ProductStore）]&quot;。

![](using-web-api-with-entity-framework-part-6/_static/image2.png)

按一下 [加入]。 這會新增名為 OrdersController.cs 的檔案。 接下來，我們需要修改控制器的預設執行。

首先，刪除 `PutOrder` 和 `DeleteOrder` 方法。 在此範例中，客戶無法修改或刪除現有的訂單。 在實際的應用程式中，您需要許多後端邏輯來處理這些情況。 （例如，訂單是否已出貨？）

變更 `GetOrders` 方法，只傳回屬於使用者的訂單：

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample7.cs)]

變更 `GetOrder` 方法，如下所示：

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample8.cs)]

以下是我們對方法所做的變更：

- 傳回值是 `OrderDTO` 實例，而不是 `Order`。
- 當我們查詢資料庫的順序時，我們會使用[DbQuery](https://msdn.microsoft.com/library/gg696395)方法來提取相關的 `OrderDetail` 和 `Product` 實體。
- 我們使用投射來壓平合併結果。

HTTP 回應會包含具有數量的產品陣列：

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample9.json)]

此格式比原始物件圖形更容易取用，其包含嵌套的實體（順序、詳細資料和產品）。

要將它視為 `PostOrder`的最後一個方法。 現在，這個方法會採用 `Order` 實例。 但是，請考慮用戶端傳送要求本文時所發生的狀況，如下所示：

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample10.json)]

這是結構良好的順序，Entity Framework 會很高興地將它插入資料庫中。 但它包含先前不存在的產品實體。 用戶端剛剛在資料庫中建立了新的產品！ 當訂單履行部門看到 koala 的人的訂單時，這會很驚訝。 值得注意的是，您在 POST 或 PUT 要求中所接受的資料非常謹慎。

若要避免這個問題，請將 `PostOrder` 方法變更為採用 `OrderDTO` 實例。 使用 `OrderDTO` 來建立 `Order`。

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample11.cs)]

請注意，我們會使用 `ProductID` 和 `Quantity` 屬性，而我們會忽略用戶端針對產品名稱或價格所傳送的任何值。 如果產品識別碼無效，它會違反資料庫中的外鍵條件約束，而插入將會失敗，如其所示。

以下是完整的 `PostOrder` 方法：

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample12.cs)]

最後，將**授權**屬性新增至控制器：

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample13.cs)]

現在只有已註冊的使用者可以建立或查看訂單。

> [!div class="step-by-step"]
> [上一頁](using-web-api-with-entity-framework-part-5.md)
> [下一頁](using-web-api-with-entity-framework-part-7.md)
