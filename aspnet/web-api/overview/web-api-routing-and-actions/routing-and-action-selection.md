---
uid: web-api/overview/web-api-routing-and-actions/routing-and-action-selection
title: ASP.NET Web API 中的路由和動作選取 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 12/14/2018
ms.assetid: bcf2d223-cb7f-411e-be05-f43e96a14015
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-and-action-selection
msc.type: authoredcontent
ms.openlocfilehash: 62114e56fb29e80c93b82dcb78ce2bc2a123a83b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554884"
---
# <a name="routing-and-action-selection-in-aspnet-web-api"></a>ASP.NET Web API 中的路由和動作選取

由[Mike Wasson](https://github.com/MikeWasson)

本文說明 ASP.NET Web API 如何將 HTTP 要求路由至控制器上的特定動作。

> [!NOTE]
> 如需路由的高階總覽，請參閱[ASP.NET Web API 中的路由](routing-in-aspnet-web-api.md)。

本文將探討路由程式的詳細資料。 如果您建立 Web API 專案，併發現某些要求不會以您預期的方式路由傳送，希望本文有助。

路由有三個主要階段：

1. 符合路由範本的 URI。
2. 選取控制器。
3. 選取動作。

您可以使用自己的自訂行為來取代進程的某些部分。 在本文中，我將說明預設行為。 最後，我會注意到您可以自訂行為的地方。

## <a name="route-templates"></a>路由範本

路由範本看起來類似 URI 路徑，但它可以有預留位置值，以大括弧表示：

[!code-csharp[Main](routing-and-action-selection/samples/sample1.ps1)]

當您建立路由時，可以為部分或所有預留位置提供預設值：

[!code-csharp[Main](routing-and-action-selection/samples/sample2.cs)]

您也可以提供條件約束，以限制 URI 區段可以符合預留位置的方式：

[!code-csharp[Main](routing-and-action-selection/samples/sample3.js)]

架構會嘗試將 URI 路徑中的區段與範本比對。 範本中的常值必須完全相符。 除非您指定條件約束，否則預留位置會符合任何值。 架構不符合 URI 的其他部分，例如主機名稱或查詢參數。 架構會選取路由表中符合 URI 的第一個路由。

有兩個特殊的預留位置： "{controller}" 和 "{action}"。

- "{controller}" 提供控制器的名稱。
- "{action}" 提供動作的名稱。 在 Web API 中，一般的慣例是省略 "{action}"。

### <a name="defaults"></a>預設值

如果您提供預設值，則路由會符合遺漏這些區段的 URI。 例如:

[!code-csharp[Main](routing-and-action-selection/samples/sample4.cs)]

Uri `http://localhost/api/products/all`，`http://localhost/api/products` 符合先前的路由。 在後面的 URI 中，遺漏的 `{category}` 區段會被指派預設值 `all`。

### <a name="route-dictionary"></a>路由字典

如果架構找到 URI 的相符項，它會建立一個包含每個預留位置值的字典。 這些索引鍵是預留位置名稱，不包含大括弧。 值取自 URI 路徑，或來自預設值。 字典會儲存在**IHttpRouteData**物件中。

在此路由比對階段期間，特殊的 "{controller}" 和 "{action}" 預留位置的處理方式就像其他預留位置一樣。 它們只會與其他值一起儲存在字典中。

預設值可以是選擇性的**RouteParameter**。 如果將此值指派給預留位置，此值就不會加入至路由字典。 例如:

[!code-csharp[Main](routing-and-action-selection/samples/sample5.cs)]

對於 URI 路徑「api/產品」，路由字典會包含：

- 控制器：「產品」
- 類別：「全部」

不過，對於「api/產品/玩具/123」，路由字典將包含：

- 控制器：「產品」
- 類別：「玩具」
- 識別碼： "123"

預設值也可以包含不會出現在路由範本中任何位置的值。 如果路由符合，該值會儲存在字典中。 例如:

[!code-csharp[Main](routing-and-action-selection/samples/sample6.cs)]

如果 URI 路徑為 "api/root/8"，則字典會包含兩個值：

- 控制器：「客戶」
- 識別碼： "8"

## <a name="selecting-a-controller"></a>選取控制器

控制器選取會由**IHttpControllerSelector. SelectController**方法處理。 這個方法會採用**HttpRequestMessage**實例，並傳回**HttpControllerDescriptor**。 預設的執行是由**DefaultHttpControllerSelector**類別所提供。 這個類別會使用簡單的演算法：

1. 查看索引鍵 "controller" 的路由字典。
2. 取得此索引鍵的值，然後附加字串 "Controller" 以取得控制器類型名稱。
3. 尋找此類型名稱為的 Web API 控制器。

例如，如果路由字典包含機碼值組 "controller" = "products"，則控制器類型為 "Productscontroller.cs"。 如果沒有相符的類型或多個相符專案，架構會將錯誤傳回給用戶端。

在步驟3中， **DefaultHttpControllerSelector**會使用**IHttpControllerTypeResolver**介面來取得 Web API 控制器類型的清單。 **IHttpControllerTypeResolver**的預設執行會傳回（a）實**IHttpController**的所有公用類別，（b）不是抽象的，而（c）的名稱會以 "Controller" 結尾。

## <a name="action-selection"></a>動作選取

選取控制器之後，架構會藉由呼叫**IHttpActionSelector. SelectAction**方法來選取動作。 這個方法會採用**system.web.HTTP.controllers.HTTPcontrollercoNtext** ，並傳回**HttpActionDescriptor**。

預設的執行是由**ApiControllerActionSelector**類別所提供。 若要選取動作，它會查看下列內容：

- 要求的 HTTP 方法。
- 路由範本中的 "{action}" 預留位置（如果有的話）。
- 控制器上動作的參數。

在查看選取演算法之前，我們必須先瞭解控制器動作的一些相關事項。

**控制器上的哪些方法會被視為「動作」？** 選取動作時，架構只會查看控制器上的公用實例方法。 此外，它也排除了「[特殊名稱](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname)」方法（例如，多載、事件、運算子多載等等），以及繼承自**ApiController**類別的方法。

**HTTP 方法。** 架構只會選擇符合要求之 HTTP 方法的動作，如下所示：

1. 您可以使用屬性指定 HTTP 方法： **AcceptVerbs**、 **HttpDelete**、 **HttpGet**、 **HttpHead**、 **HttpOptions**、 **HttpPatch**、 **HttpPost**或**HttpPut**。
2. 否則，如果控制器方法的名稱開頭為 "Get"、"Post"、"Put"、"Delete"、"Head"、"Options" 或 "Patch"，則依照慣例，動作會支援該 HTTP 方法。
3. 如果以上皆非，則方法支援 POST。

**參數系結。** 參數系結是 Web API 為參數建立值的方式。 以下是參數系結的預設規則：

- 簡單類型取自 URI。
- 複雜型別取自要求主體。

簡單類型包括所有[.NET Framework](https://msdn.microsoft.com/library/system.type.isprimitive)基本型別，加上**DateTime**、 **Decimal**、 **Guid**、 **String**和**TimeSpan**。 針對每個動作，最多隻能有一個參數讀取要求主體。

> [!NOTE]
> 您可以覆寫預設的系結規則。 請參閱幕後[的 WebAPI 參數](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)系結。

在該背景中，以下是動作選取演算法。

1. 在控制器上建立符合 HTTP 要求方法的所有動作清單。
2. 如果路由字典有「動作」專案，請移除名稱不符合此值的動作。
3. 請嘗試比對動作參數與 URI，如下所示： 

    1. 針對每個動作，取得簡單類型的參數清單，其中系結會從 URI 取得參數。 排除選擇性參數。
    2. 從這份清單中，嘗試尋找每個參數名稱的相符項，不論是在路由字典中，或在 URI 查詢字串中。 相符專案不區分大小寫，且不會相依于參數順序。
    3. 選取動作，其中清單中的每個參數在 URI 中都有相符的。
    4. 如果有更多動作符合這些準則，請挑選其中一個包含最多參數的相符專案。
4. 忽略具有 **[請以 nonaction]** 屬性的動作。

步驟 #3 可能是最令人困惑的。 基本概念是，參數可以從 URI、要求主體或自訂系結取得其值。 對於來自 URI 的參數，我們想要確保 URI 實際上包含該參數的值，不論是在路徑中（透過路由字典）或是在查詢字串中。

例如，請考慮下列動作：

[!code-csharp[Main](routing-and-action-selection/samples/sample7.cs)]

*Id*參數會系結至 URI。 因此，此動作只能符合在路由字典或查詢字串中包含 "id" 值的 URI。

選擇性參數是例外狀況，因為它們是選擇性的。 對於選擇性參數，如果系結無法從 URI 取得值，則為 OK。

複雜類型是因不同原因而產生的例外狀況。 複雜型別只能透過自訂系結系結至 URI。 但是在這種情況下，架構無法事先知道參數是否會系結至特定的 URI。 若要找出，必須叫用系結。 選取演算法的目標是在叫用任何系結之前，從靜態描述中選取動作。 因此，複雜類型會從比對演算法中排除。

選取動作之後，就會叫用所有參數系結。

摘要:

- 動作必須符合要求的 HTTP 方法。
- 動作名稱必須符合路由字典中的「動作」專案（如果有的話）。
- 對於動作的每個參數，如果從 URI 取得參數，則必須在路由字典或 URI 查詢字串中找到參數名稱。 （已排除具有複雜類型的選擇性參數和參數）。
- 嘗試比對最多的參數數目。 最佳比對可能是沒有參數的方法。

## <a name="extended-example"></a>擴充範例

料

[!code-csharp[Main](routing-and-action-selection/samples/sample8.cs)]

控制器:

[!code-csharp[Main](routing-and-action-selection/samples/sample9.cs)]

HTTP 要求：

[!code-console[Main](routing-and-action-selection/samples/sample10.cmd)]

### <a name="route-matching"></a>路由符合

URI 符合名為 "DefaultApi" 的路由。 路由字典包含下列專案：

- 控制器：「產品」
- 識別碼： "1"

路由字典不包含查詢字串參數 "version" 和 "details"，但是在動作選取期間仍會考慮這些專案。

### <a name="controller-selection"></a>控制器選取

從路由字典中的「控制器」專案，控制器類型為 `ProductsController`。

### <a name="action-selection"></a>動作選取

HTTP 要求是 GET 要求。 支援 GET 的控制器動作包括 `GetAll`、`GetById`和 `FindProductsByName`。 路由字典未包含 "action" 的專案，因此不需要符合動作名稱。

接下來，我們會嘗試比對動作的參數名稱，只查看 [取得] 動作。

| 動作 | 要比對的參數 |
| --- | --- |
| `GetAll` | 無 |
| `GetById` | "id" |
| `FindProductsByName` | 檔案名 |

請注意，不會考慮 `GetById` 的*version*參數，因為它是選擇性參數。

`GetAll` 的方法符合完整。 `GetById` 方法也會符合，因為路由字典包含 "id"。 `FindProductsByName` 的方法不相符。

`GetById` 方法會勝出，因為它符合一個參數，而不是 `GetAll`的參數。 使用下列參數值叫用方法：

- *識別碼*= 1
- *版本*= 1。5

請注意，即使*版本*不是用在選取演算法中，參數的值還是來自 URI 查詢字串。

## <a name="extension-points"></a>擴充點

Web API 會為路由程式的某些部分提供延伸模組點。

| 介面 | 說明 |
| --- | --- |
| **IHttpControllerSelector** | 選取控制器。 |
| **IHttpControllerTypeResolver** | 取得控制器類型的清單。 **DefaultHttpControllerSelector**會從這份清單中選擇控制器類型。 |
| **IAssembliesResolver** | 取得專案元件的清單。 **IHttpControllerTypeResolver**介面會使用這份清單來尋找控制器類型。 |
| **IHttpControllerActivator** | 建立新的控制器實例。 |
| **IHttpActionSelector** | 選取動作。 |
| **IHttpActionInvoker** | 叫用動作。 |

若要為上述任何介面提供您自己的執行，請在**HttpConfiguration**物件上使用**Services**集合：

[!code-csharp[Main](routing-and-action-selection/samples/sample11.cs)]
