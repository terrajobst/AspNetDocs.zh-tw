---
uid: web-api/overview/advanced/sending-html-form-data-part-1
title: 在 ASP.NET Web API 中傳送 HTML 表單資料：表單 urlencoded 資料-ASP.NET 4。x
author: MikeWasson
description: 本文說明如何將表單 urlencoded 資料張貼至 ASP.NET 4.x 的 Web API 控制器
ms.author: riande
ms.date: 06/15/2012
ms.custom: seoapril2019
ms.assetid: 585351c4-809a-4bf5-bcbe-35d624f565fe
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-1
msc.type: authoredcontent
ms.openlocfilehash: 7243069dbd8051b1374ed6e0112c273b8fe26f61
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557600"
---
# <a name="sending-html-form-data-in-aspnet-web-api-form-urlencoded-data"></a>在 ASP.NET Web API 中傳送 HTML 表單資料：表單 urlencoded 資料

由[Mike Wasson](https://github.com/MikeWasson)

## <a name="part-1-form-urlencoded-data"></a>第1部分：表單 urlencoded 資料

本文說明如何將表單 urlencoded 資料張貼至 Web API 控制器。

- [HTML 表單總覽](#overview_of_html_forms)
- [傳送複雜類型](#sending_complex_types)
- [透過 AJAX 傳送表單資料](#sending_form_data_via_ajax)
- [傳送簡單類型](#sending_simple_types)

> [!NOTE]
> [下載已完成的專案](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007)。

<a id="overview_of_html_forms"></a>
## <a name="overview-of-html-forms"></a>HTML 表單總覽

HTML 表單使用 GET 或 POST 將資料傳送至伺服器。 **Form**元素的**METHOD**屬性提供 HTTP 方法：

[!code-html[Main](sending-html-form-data-part-1/samples/sample1.html)]

預設方法為 GET。 如果表單使用 GET，則表單資料會在 URI 中編碼為查詢字串。 如果表單使用 POST，則表單資料會放在要求主體中。 針對張貼的資料， **enctype**屬性會指定要求主體的格式：

| enctype | 說明 |
| --- | --- |
| application/x-www-form-urlencoded | 表單資料會編碼成成對的名稱/值，類似于 URI 查詢字串。 這是 POST 的預設格式。 |
| 多部分/表單資料 | 表單資料會編碼為多部分 MIME 訊息。 如果您要將檔案上傳到伺服器，請使用此格式。 |

本文的第1部分探討 x-www-表單 urlencoded 格式。 [第2部分](sending-html-form-data-part-2.md)描述多部分 MIME。

<a id="sending_complex_types"></a>
## <a name="sending-complex-types"></a>傳送複雜類型

一般來說，您會傳送複雜型別，其中包含從數個表單控制項取得的值。 請考慮下列代表狀態更新的模型：

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample2.cs)]

以下是透過 POST 接受 `Update` 物件的 Web API 控制器。

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample3.cs)]

> [!NOTE]
> 此控制器使用以[動作為基礎的路由](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name)，因此路由範本為 &quot;api/{controller}/{action}/{id}&quot;。 用戶端會將資料張貼到 &quot;/api/updates/complex&quot;。

現在，我們將撰寫 HTML 表單，讓使用者提交狀態更新。

[!code-html[Main](sending-html-form-data-part-1/samples/sample4.html)]

請注意，表單上的 [**動作**] 屬性是控制器動作的 URI。 以下是在中輸入一些值的表單：

![](sending-html-form-data-part-1/_static/image1.png)

當使用者按一下 [提交] 時，瀏覽器會傳送類似下列的 HTTP 要求：

[!code-console[Main](sending-html-form-data-part-1/samples/sample5.cmd)]

請注意，要求本文包含表單資料，格式為名稱/值組。 Web API 會自動將名稱/值組轉換成 `Update` 類別的實例。

<a id="sending_form_data_via_ajax"></a>
## <a name="sending-form-data-via-ajax"></a>透過 AJAX 傳送表單資料

當使用者提交表單時，瀏覽器會離開目前頁面，並呈現回應訊息的本文。 當回應是 HTML 網頁時，這是正常的。 不過，使用 Web API，回應主體通常是空的或包含結構化的資料，例如 JSON。 在此情況下，使用 AJAX 要求來傳送表單資料會更有意義，讓頁面可以處理回應。

下列程式碼顯示如何使用 jQuery 張貼表單資料。

[!code-html[Main](sending-html-form-data-part-1/samples/sample6.html)]

JQuery **submit**函式會將表單動作取代為新的函式。 這會覆寫 [提交] 按鈕的預設行為。 序列化函式會將表單資料**序列化**成成對的名稱/值。 若要將表單資料傳送到伺服器，請呼叫 `$.post()`。

當要求完成時，`.success()` 或 `.error()` 處理常式會向使用者顯示適當的訊息。

![](sending-html-form-data-part-1/_static/image2.png)

<a id="sending_simple_types"></a>
## <a name="sending-simple-types"></a>傳送簡單類型

在先前的章節中，我們傳送了複雜型別，也就是將哪個 Web API 還原序列化為模型類別的實例。 您也可以傳送簡單的類型，例如字串。

> [!NOTE]
> 在傳送簡單型別之前，請考慮改為將值換成複雜型別。 這可讓您在伺服器端提供模型驗證的優點，並可讓您更輕鬆地視需要擴充模型。

傳送簡單類型的基本步驟相同，但有兩個細微的差異。 首先，在控制器中，您必須使用**FromBody**屬性裝飾參數名稱。

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample7.cs?highlight=3)]

根據預設，Web API 會嘗試從要求 URI 取得簡單的類型。 **FromBody**屬性會告知 Web API 從要求主體讀取值。

> [!NOTE]
> Web API 會讀取最多一次的回應本文，因此只有一個動作參數可以來自要求主體。 如果您需要從要求主體取得多個值，請定義複雜型別。

第二，用戶端必須以下列格式傳送值：

[!code-xml[Main](sending-html-form-data-part-1/samples/sample8.xml)]

具體而言，簡單類型的名稱/值組名稱部分必須是空的。 並非所有瀏覽器都支援 HTML 表單的此功能，但您會在腳本中建立此格式，如下所示：

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample9.js)]

以下是範例表單：

[!code-html[Main](sending-html-form-data-part-1/samples/sample10.html)]

以下是提交表單值的腳本。 與上一個腳本的唯一差異在於傳遞至**post**函式的引數。

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample11.js?highlight=2)]

您可以使用相同的方法來傳送簡單類型的陣列：

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample12.js)]

## <a name="additional-resources"></a>其他資源

[第2部分：檔案上傳和多部分 MIME](sending-html-form-data-part-2.md)
