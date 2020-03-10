---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
title: 第5部分：使用挖的 .js 建立動態 UI |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 9d9cb3b0-f4a7-434e-a508-9fc0ad0eb813
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
msc.type: authoredcontent
ms.openlocfilehash: bbdeba756de7986cfeb92aa10a57f4f101382f99
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555990"
---
# <a name="part-5-creating-a-dynamic-ui-with-knockoutjs"></a>第5部分：使用挖的 .js 建立動態 UI

由[Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-a-dynamic-ui-with-knockoutjs"></a>使用 Knockout.js 建立動態 UI

在本節中，我們將使用 [挖加] 將功能新增至系統管理員視圖。

[挖式 .js](http://knockoutjs.com/)是 JAVAscript 程式庫，可讓您輕鬆地將 HTML 控制項系結至資料。 挖式 .js 會使用 ViewModel （MVVM）模式。

- *模型*是企業網域中資料的伺服器端標記法（在我們的案例中為產品和訂單）。
- 此*視圖*為展示層（HTML）。
- *視圖模型*是包含模型資料的 JAVAscript 物件。 視圖模型是 UI 的程式碼抽象概念。 它不知道 HTML 標記法。 相反地，它代表視圖的抽象功能，例如「專案清單」。

此視圖會資料系結至視圖模型。 視圖模型的更新會自動反映在視圖中。 視圖模型也會從視圖取得事件，例如按鈕按一下，然後在模型上執行作業，例如建立訂單。

![](using-web-api-with-entity-framework-part-5/_static/image1.png)

首先，我們要定義視圖模型。 之後，我們會將 HTML 標籤系結至視圖模型。

將下列 Razor 區段新增至 Admin. cshtml：

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample1.cshtml)]

您可以將此區段新增至檔案中的任何位置。 當此視圖呈現時，區段會顯示在 HTML 頁面的底部，在結尾 &lt;/body&gt; 標記之前。

此頁面的所有腳本都會放在批註所指示的腳本標記內：

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample2.html)]

首先，定義視圖模型類別：

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample3.js)]

**observableArray**是一種特殊類型的物件，稱為可*觀察*的。 從「[挖的 .js」檔](http://knockoutjs.com/documentation/observables.html)：可觀察的是可以通知訂閱者有關變更的「JavaScript 物件」。 當可觀察的變更內容時，會自動更新此視圖以符合。

若要填入 `products` 陣列，請向 Web API 發出 AJAX 要求。 回想一下，我們已將 API 的基底 URI 儲存在視圖包中（請參閱本教學課程的[第4部分](using-web-api-with-entity-framework-part-4.md)）。

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample4.js?highlight=5)]

接下來，將函數新增至視圖模型，以建立、更新和刪除產品。 這些函式會將 AJAX 呼叫提交至 Web API，並使用結果來更新視圖模型。

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample5.js?highlight=7)]

現在最重要的部分： fulled 載入 DOM 時，呼叫**applyBindings**函式並傳入 `ProductsViewModel`的新實例：

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample6.js)]

**ApplyBindings**方法會啟動挖式，並將視圖模式向上線到視圖。

既然我們已經有了視圖模型，我們就可以建立系結。 在挖的 .js 中，您可以藉由將 `data-bind` 屬性加入 HTML 專案來完成此動作。 例如，若要將 HTML 清單系結至陣列，請使用 `foreach` 系結：

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample7.html?highlight=1)]

`foreach` 系結會逐一查看陣列，並針對陣列中的每個物件建立子項目。 子項目上的系結可以參考陣列物件上的屬性。

將下列系結新增至 [更新產品] 清單：

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample8.html)]

`<li>` 元素會在**foreach**系結的範圍內發生。 也就是說，「挖隔」會針對 `products` 陣列中的每個產品轉譯一次元素。 `<li>` 元素內的所有系結都會參考該產品實例。 例如，`$data.Name` 指的是產品上的 `Name` 屬性。

若要設定文字輸入的值，請使用 `value` 系結。 這些按鈕會使用 `click` 系結，系結至模型視圖上的函式。 產品實例會當做參數傳遞至每個函式。 如需詳細資訊，請[參閱「挖的 .js」檔](http://knockoutjs.com/documentation/observables.html)，以取得各種系結的良好描述。

接下來，在 [新增產品] 表單上新增 [**提交**] 事件的系結：

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample9.html)]

這個系結會在視圖模型上呼叫 `create` 函式，以建立新的產品。

以下是系統管理視圖的完整程式碼：

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample10.cshtml)]

執行應用程式、使用系統管理員帳戶登入，然後按一下 [管理] 連結。 您應該會看到產品清單，而且能夠建立、更新或刪除產品。

> [!div class="step-by-step"]
> [上一頁](using-web-api-with-entity-framework-part-4.md)
> [下一頁](using-web-api-with-entity-framework-part-6.md)
