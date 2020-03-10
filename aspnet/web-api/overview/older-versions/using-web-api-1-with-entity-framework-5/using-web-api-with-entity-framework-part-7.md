---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
title: 第7部分：建立主頁面 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: eb32a17b-626c-4373-9a7d-3387992f3c04
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
msc.type: authoredcontent
ms.openlocfilehash: fe4074c701159a137be3644d65ca844f160c2399
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598676"
---
# <a name="part-7-creating-the-main-page"></a>第7部分：建立主頁面

由[Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-the-main-page"></a>建立主要頁面

在本節中，您將建立主應用程式頁面。 此頁面比管理頁面更為複雜，因此我們將在幾個步驟中進行處理。 在此過程中，您將會看到一些更先進的「挖加」的方法。 以下是頁面的基本版面配置：

![](using-web-api-with-entity-framework-part-7/_static/image1.png)

- 「產品」包含產品的陣列。
- 「購物車」包含具有數量的產品陣列。 按一下 [新增至購物車] 會更新購物車。
- 「訂單」包含訂單識別碼的陣列。
- 「詳細資料」包含訂單詳細資料，也就是專案的陣列（具有數量的產品）

我們一開始會在 HTML 中定義一些基本版面配置，而不會有任何資料系結或腳本。 開啟檔案 Views/Home/Index. cshtml，並將所有內容取代為下列內容：

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample1.html)]

接下來，新增腳本區段並建立空白的視圖模型：

[!code-cshtml[Main](using-web-api-with-entity-framework-part-7/samples/sample2.cshtml)]

根據稍早所繪的設計，我們的視圖模型需要產品、購物車、訂單和詳細資料的可預見值。 將下列變數新增至 `AppViewModel` 物件：

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample3.js)]

使用者可以將產品清單中的專案新增至購物車，並移除購物車中的專案。 為了封裝這些函式，我們將建立另一個代表產品的視圖模型類別。 將下列程式碼新增至 `AppViewModel`：

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample4.js?highlight=4)]

`ProductViewModel` 類別包含兩個函式，可用來將產品移至購物車或從中移動： `addItemToCart` 會將產品的一個單位新增至購物車，而 `removeAllFromCart` 則會移除產品的所有數量。

使用者可以選取現有的訂單，並取得訂單詳細資料。 我們會將此功能封裝到另一個視圖模型中：

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample5.js?highlight=4)]

`OrderDetailsViewModel` 會以訂單進行初始化，並藉由將 AJAX 要求傳送至伺服器來提取訂單詳細資料。

此外，請注意 `OrderDetailsViewModel`上的 `total` 屬性。 此屬性是一種特殊類型的可觀察，稱為計算的可[觀察](http://knockoutjs.com/documentation/computedObservables.html)。 顧名思義，「計算的可觀察」可讓您將資料系結至&#8212;計算的值，在此案例中為訂單的總成本。

接下來，將下列函式新增至 `AppViewModel`：

- `resetCart` 會移除購物車中的所有專案。
- `getDetails` 取得訂單的詳細資料（藉由將新的 `OrderDetailsViewModel` 推送至 `details` 清單）。
- `createOrder` 會建立新的訂單，並清空購物車。

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample6.js?highlight=4)]

最後，藉由對產品和訂單提出 AJAX 要求來初始化視圖模型：

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample7.js)]

好的，這是很多程式碼，但是我們會逐步建立它，因此希望設計清楚明瞭。 現在我們可以將一些挖的 .js 系結新增至 HTML。

**產品**

以下是產品清單的系結：

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample8.html)]

這會逐一查看 products 陣列，並顯示名稱和價格。 只有在使用者登入時，才可以看到 [加入順序] 按鈕。

[加入至訂單] 按鈕會在產品的 `ProductViewModel` 實例上呼叫 `addItemToCart`。 這會示範挖式 .js 的絕佳功能：當視圖模型包含其他視圖模型時，您可以將系結套用至內部模型。 在此範例中，`foreach` 內的系結會套用至每個 `ProductViewModel` 實例。 這種方法比將所有功能放入單一視圖模型中更為簡潔。

**放**

以下是購物車的系結：

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample9.html)]

這會逐一查看購物車陣列，並顯示名稱、價格和數量。 請注意，[移除] 連結和 [建立順序] 按鈕會系結至視圖模型函數。

**訂單**

以下是 orders 清單的系結：

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample10.html)]

這會逐一查看訂單，並顯示訂單識別碼。 連結上的 click 事件會系結到 `getDetails` 函數。

**訂單詳細資料**

以下是訂單詳細資料的系結：

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample11.html)]

這會逐一查看訂單中的專案，並顯示產品、價格和數量。 只有當詳細資料陣列包含一個或多個專案時，才會顯示周圍的 div。

## <a name="conclusion"></a>結論

在本教學課程中，您已建立使用 Entity Framework 與資料庫通訊的應用程式，並 ASP.NET Web API 在資料層上提供公開介面。 我們會使用 ASP.NET MVC 4 來轉譯 HTML 網頁，並使用挖加 jQuery 來提供動態互動，而不需要頁面重載。

其他資源：

- [ASP.NET 資料存取內容地圖](https://msdn.microsoft.com/library/6759sth4.aspx)
- [Entity Framework 開發人員中心](https://msdn.microsoft.com/data/ef)

> [!div class="step-by-step"]
> [上一篇](using-web-api-with-entity-framework-part-6.md)
