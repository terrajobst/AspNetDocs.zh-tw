---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: ASP.NET Web API 中的路由 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557607"
---
# <a name="routing-in-aspnet-web-api"></a>ASP.NET Web API 中的路由

由[Mike Wasson](https://github.com/MikeWasson)

本文說明 ASP.NET Web API 如何將 HTTP 要求路由傳送至控制器。

> [!NOTE]
> 如果您熟悉 ASP.NET MVC，Web API 路由與 MVC 路由非常類似。 主要差異在於 Web API 會使用 HTTP 指令動詞，而不是 URI 路徑來選取動作。 您也可以在 Web API 中使用 MVC 樣式的路由。 本文不會假設您對 ASP.NET MVC 有任何瞭解。

## <a name="routing-tables"></a>路由表

在 ASP.NET Web API 中，*控制器*是處理 HTTP 要求的類別。 控制器的公用方法稱為*動作方法*或簡單的*動作*。 當 Web API 架構收到要求時，它會將要求路由傳送至動作。

為了判斷要叫用的動作，架構會使用*路由表*。 Web API 的 Visual Studio 專案範本會建立預設路由：

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

此路由是在*WebApiConfig.cs*檔案中定義，此檔案會放在*應用程式\_起始*目錄中：

![](routing-in-aspnet-web-api/_static/image1.png)

如需 `WebApiConfig` 類別的詳細資訊，請參閱設定[ASP.NET Web API](../advanced/configuring-aspnet-web-api.md)。

如果您自行裝載 Web API，您必須直接在 `HttpSelfHostConfiguration` 物件上設定路由表。 如需詳細資訊，請參閱[自我裝載 WEB API](../older-versions/self-host-a-web-api.md)。

路由表中的每個專案都包含一個*路由範本*。 Web API 的預設路由範本為 &quot;API/{controller}/{id}&quot;。 在此範本中，&quot;api&quot; 是常值路徑區段，而 {controller} 和 {id} 是預留位置變數。

當 Web API 架構收到 HTTP 要求時，它會嘗試比對路由表中的其中一個路由範本的 URI。 如果沒有符合的路由，用戶端會收到404錯誤。 例如，下列 Uri 符合預設路由：

- /api/contacts
- /api/contacts/1
- /api/products/gizmo1

不過，下列 URI 不相符，因為它缺少 &quot;api&quot; 區段：

- /contacts/1

> [!NOTE]
> 在路由中使用「api」的原因是為了避免與 ASP.NET MVC 路由發生衝突。 如此一來，您就可以讓 &quot;/contacts&quot; 移至 MVC 控制器，並 &quot;/api/contacts&quot; 移至 Web API 控制器。 當然，如果您不喜歡這種慣例，可以變更預設的路由表。

一旦找到相符的路由，Web API 就會選取控制器和動作：

- 若要尋找控制器，Web API 會將 &quot;控制器&quot; 新增至 *{controller}* 變數的值。
- 若要尋找此動作，Web API 會查看 HTTP 指令動詞，然後尋找名稱開頭為該 HTTP 動詞命令名稱的動作。 例如，使用 GET 要求時，Web API 會尋找前面加上 &quot;Get&quot;的動作，例如 &quot;GetContact&quot; 或 &quot;GetAllContacts&quot;。 此慣例僅適用于 GET、POST、PUT、DELETE、HEAD、OPTIONS 和 PATCH 動詞。 您可以使用控制器上的屬性來啟用其他 HTTP 動詞命令。 我們稍後會看到一個範例。
- 路由範本中的其他預留位置變數（例如 *{id}）* 會對應至動作參數。

讓我們看看以下範例。 假設您定義了下列控制器：

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

以下是一些可能的 HTTP 要求，以及針對每個要求叫用的動作：

| HTTP 指令動詞 | URI 路徑 | 動作 | 參數 |
| --- | --- | --- | --- |
| GET | api/產品 | Getallproductswithcategories | *無* |
| GET | api/產品/4 | GetProductById | 4 |
| 刪除 | api/產品/4 | DeleteProduct | 4 |
| POST | api/產品 | *（不符合）* |  |

請注意，URI 的 *{id}* 區段（如果有的話）會對應至動作的*id*參數。 在此範例中，控制器會定義兩個 GET 方法，一個具有*識別碼*參數，另一個不含參數。

此外，請注意 POST 要求將會失敗，因為控制器不會定義 &quot;Post ...&quot; 方法。

## <a name="routing-variations"></a>路由變化

上一節說明了 ASP.NET Web API 的基本路由機制。 本節說明一些變化。

### <a name="http-verbs"></a>HTTP 指令動詞

您可以使用下列其中一個屬性來裝飾動作方法，而不是使用 HTTP 指令動詞的命名慣例，以明確指定動作的 HTTP 動詞命令：

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

在下列範例中，`FindProduct` 方法會對應至 GET 要求：

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

若要允許某個動作有多個 HTTP 動詞命令，或允許 GET、PUT、POST、DELETE、HEAD、OPTIONS 和 PATCH 以外的 HTTP 動詞命令，請使用 `[AcceptVerbs]` 屬性，這會接受 HTTP 指令動詞的清單。

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a>依動作名稱路由

使用預設路由範本時，Web API 會使用 HTTP 指令動詞來選取動作。 不過，您也可以建立路由，其中動作名稱會包含在 URI 中：

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

在此路由範本中， *{action}* 參數會在控制器上命名動作方法。 使用這種路由模式時，請使用屬性來指定允許的 HTTP 動詞命令。 例如，假設您的控制器具有下列方法：

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

在此情況下，「api/產品/詳細資料/1」的 GET 要求會對應至 `Details` 方法。 這種路由樣式類似于 ASP.NET MVC，而且可能適用于 RPC 樣式的 API。

您可以使用 `[ActionName]` 屬性來覆寫動作名稱。 在下列範例中，有兩個動作會對應至 &quot;api/產品/縮圖/*識別碼*。其中一個支援 GET，另一個支援 POST：

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a>非動作

若要防止方法被叫用為動作，請使用 `[NonAction]` 屬性。 這會向架構指出方法不是動作，即使它會符合路由規則也一樣。

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a>進一步閱讀

本主題提供路由的高階觀點。 如需詳細資訊，請參閱[路由和動作選取](routing-and-action-selection.md)，其中描述架構如何比對路由的 URI、選取控制器，然後選取要叫用的動作。
