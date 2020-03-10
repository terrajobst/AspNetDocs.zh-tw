---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: ASP.NET Web API 2 中的屬性路由 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 7da1805d8a7066e82743dc9bd7e024cc9813ee89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554982"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a>ASP.NET Web API 2 中的屬性路由

由[Mike Wasson](https://github.com/MikeWasson)

*路由*是 Web API 與動作的 URI 相符的方式。 Web API 2 支援新類型的路由，稱為*屬性路由*。 如其名稱所示，屬性路由會使用屬性來定義路由。 屬性路由可讓您更充分掌控 Web API 中的 Uri。 例如，您可以輕鬆地建立描述資源階層的 Uri。

先前的路由樣式（稱為慣例型路由）仍受到完整支援。 事實上，您可以將這兩種技術結合在同一個專案中。

本主題說明如何啟用屬性路由，並說明屬性路由的各種選項。 如需使用屬性路由的端對端教學課程，請參閱[使用 WEB API 2 中的屬性路由建立 REST API](create-a-rest-api-with-attribute-routing.md)。

## <a name="prerequisites"></a>Prerequisites

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)社區、專業或企業版

或者，使用 NuGet 套件管理員來安裝必要的套件。 從 Visual Studio 的 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。 在 [套件管理員主控台] 視窗中輸入下列命令：

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a>為什麼要進行屬性路由？

第一版的 Web API 使用以*慣例為基礎*的路由。 在該類型的路由中，您會定義一或多個路由範本，基本上就是參數化字串。 當架構收到要求時，它會比對路由範本的 URI。 （如需以慣例為基礎之路由的詳細資訊，請參閱[ASP.NET Web API 中的路由](routing-in-aspnet-web-api.md)。

以慣例為基礎的路由的優點之一，是在單一位置定義範本，並在所有控制器上一致地套用路由規則。 可惜的是，以慣例為基礎的路由，讓您難以支援 RESTful Api 中常見的特定 URI 模式。 例如，資源通常包含子資源：客戶有訂單、電影具有執行者、書籍有作者等等。 建立反映這些關聯性的 Uri 是很自然的：

`/customers/1/orders`

這種類型的 URI 很容易使用以慣例為基礎的路由來建立。 雖然可以完成，但如果您有許多控制器或資源類型，則結果無法妥善調整。

使用屬性路由，為此 URI 定義路由是很簡單的。 您只需將屬性新增至控制器動作：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

以下是一些屬性路由變得很容易的其他模式。

**API 版本控制**

在此範例中，"/api/v1/products" 會路由傳送至不同的控制器，而不是 "/api/v2/products"。

`/api/v1/products`
`/api/v2/products`

**多載 URI 區段**

在此範例中，"1" 是訂單號碼，但 "pending" 對應至集合。

`/orders/1`
`/orders/pending`

**多個參數類型**

在此範例中，"1" 是訂單號碼，但 "2013/06/16" 指定日期。

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a>啟用屬性路由

若要啟用屬性路由，請在設定期間呼叫**MapHttpAttributeRoutes** 。 這個擴充方法是在**HttpConfigurationExtensions**類別中定義。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

屬性路由可以與以[慣例為基礎](routing-in-aspnet-web-api.md)的路由結合。 若要定義以慣例為基礎的路由，請呼叫**MapHttpRoute**方法。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

如需設定 Web API 的詳細資訊，請參閱設定[ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md)。

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a>注意：從 Web API 1 進行遷移

在 Web API 2 之前，Web API 專案範本會產生如下的程式碼：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

如果已啟用屬性路由，此程式碼將會擲回例外狀況。 如果您將現有的 Web API 專案升級為使用屬性路由，請務必將此設定程式碼更新為下列內容：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> 如需詳細資訊，請參閱[使用 ASP.NET 裝載來設定 WEB API](../advanced/configuring-aspnet-web-api.md#webhost)。

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a>新增路由屬性

以下是使用屬性定義的路由範例：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

客戶/{customerId}/訂單&quot; &quot;字串是路由的 URI 範本。 Web API 會嘗試將要求 URI 與範本比對。 在此範例中，「客戶」和「訂單」是常值區段，而「{customerId}」則是變數參數。 下列 Uri 會符合此範本：

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

您可以使用[條件約束](#constraints)來限制比對，如本主題稍後所述。

請注意，路由範本中的 &quot;{customerId}&quot; 參數符合方法中*customerId*參數的名稱。 當 Web API 叫用控制器動作時，它會嘗試系結路由參數。 例如，如果 URI 為 `http://example.com/customers/1/orders`，Web API 會嘗試將值 "1" 系結至動作中的*customerId*參數。

URI 範本可以有數個參數：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

任何沒有路由屬性的控制器方法都會使用以慣例為基礎的路由。 如此一來，您就可以將這兩種類型的路由結合在相同的專案中。

## <a name="http-methods"></a>HTTP 方法

Web API 也會根據要求的 HTTP 方法（GET、POST 等等）來選取動作。 根據預設，Web API 會使用控制器方法名稱的開頭，尋找不區分大小寫的相符。 例如，名為 `PutCustomers` 的控制器方法會符合 HTTP PUT 要求。

您可以使用下列任何屬性來裝飾方法，以覆寫此慣例：

- **HttpDelete**
- **[HttpGet]**
- **[HttpHead]**
- **HttpOptions**
- **[HttpPatch]**
- **HttpPost**
- **HttpPut**

下列範例會將 CreateBook 方法對應至 HTTP POST 要求。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

針對所有其他 HTTP 方法，包括非標準方法，請使用**AcceptVerbs**屬性，這會接受 HTTP 方法的清單。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a>路由首碼

通常，控制器中的路由都是以相同的前置詞開頭。 例如:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

您可以使用 **[RoutePrefix]** 屬性來設定整個控制器的通用前置詞：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

在 method 屬性上使用波狀符號（~）來覆寫路由前置詞：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

路由前置詞可以包含參數：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a>路由條件約束

路由條件約束可讓您限制路由範本中的參數相符的方式。 一般語法為 &quot;{parameter： constraint}&quot;。 例如:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

在這裡，只有在 URI 的 &quot;識別碼&quot; 區段是整數時，才會選取第一個路由。 否則，將會選擇第二個路由。

下表列出支援的條件約束。

| 條件約束 | 說明 | 範例 |
| --- | --- | --- |
| Alpha | 符合大寫或小寫拉丁字母字元（a-z、a-z） | {x:Alpha} |
| bool | 符合布林值。 | {x:bool} |
| datetime | 符合**日期時間**值。 | {x:datetime} |
| decimal | 符合十進位值。 | {x:decimal} |
| 雙線 | 符合64位的浮點值。 | x：double |
| FLOAT | 符合32位的浮點值。 | {x:float} |
| guid | 符合 GUID 值。 | {x:guid} |
| int | 符合32位的整數值。 | {x:int} |
| 長度 | 符合指定長度或指定長度範圍內的字串。 | {x:length （6）}{x:length （1，20）} |
| long | 符合64位的整數值。 | {x:long} |
| max | 符合具有最大值的整數。 | {x:max （10）} |
| 長度 | 符合長度上限的字串。 | {x:maxlength （10）} |
| min | 符合最小值的整數。 | {x:min （10）} |
| minlength | 符合長度最小的字串。 | {x:minlength （10）} |
| range | 符合某個值範圍內的整數。 | {x:range （10，50）} |
| regex | 符合正則運算式。 | {x:RegEx （^ \d{3}-\d{3}-\d{4}$）} |

請注意，某些條件約束（例如 &quot;min&quot;）接受括弧中的引數。 您可以將多個條件約束套用至參數，並以冒號分隔。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a>自訂路由限制式

您可以藉由執行**IHttpRouteConstraint**介面來建立自訂路由條件約束。 例如，下列條件約束會將參數限制為非零的整數值。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

下列程式碼顯示如何註冊條件約束：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

現在您可以在路由中套用條件約束：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

您也可以藉由執行**IInlineConstraintResolver**介面來取代整個**DefaultInlineConstraintResolver**類別。 這麼做會取代所有內建的條件約束，除非您的**IInlineConstraintResolver**特別加入它們。

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a>選擇性的 URI 參數和預設值

您可以藉由將問號新增至 route 參數，將 URI 參數設為選擇性。 如果路由參數是選擇性的，您必須定義 method 參數的預設值。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

在此範例中，`/api/books/locale/1033` 和 `/api/books/locale` 會傳回相同的資源。

或者，您也可以在路由範本中指定預設值，如下所示：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

這幾乎與上一個範例相同，但套用預設值時，行為稍有不同。

- 在第一個範例（"{lcid： int？}"）中，1033的預設值會直接指派給方法參數，因此參數會有這個確切的值。
- 在第二個範例（"{lcid： int = 1033}"）中，"1033" 的預設值會經過模型系結程式。 預設的模型系結器會將 "1033" 轉換為數值1033。 不過，您可以插入自訂模型系結器，這可能會執行一些不同的動作。

（在大部分的情況下，除非您的管線中有自訂模型系結器，否則這兩種形式會是相等的）。

<a id="route-names"></a>
## <a name="route-names"></a>路由名稱

在 Web API 中，每個路由都有一個名稱。 路由名稱適用于產生連結，因此您可以在 HTTP 回應中包含連結。

若要指定路由名稱，請在屬性上設定**name**屬性。 下列範例顯示如何設定路由名稱，以及如何在產生連結時使用路由名稱。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a>路由順序

當架構嘗試比對 URI 與路由時，會以特定順序評估路由。 若要指定順序，請設定 route 屬性的**order**屬性。 較低的值會先進行評估。 預設順序值為零。

以下是決定總計順序的方式：

1. 比較 route 屬性的**Order**屬性。
2. 查看路由範本中的每個 URI 區段。 針對每個區段，順序如下：

    1. 常值區段。
    2. 具有條件約束的路由參數。
    3. 沒有條件約束的路由參數。
    4. 具有條件約束的萬用字元參數區段。
    5. 沒有條件約束的萬用字元參數區段。
3. 如果是系結，路由會依路由範本的不區分大小寫序數位串比較（[OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)）排序。

以下是一個範例。 假設您定義下列控制器：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

這些路由的順序如下所示。

1. 訂單/詳細資料
2. 訂單/{id}
3. orders/{customerName}
4. 訂單/{\*日期}
5. 訂單/暫止

請注意，「詳細資料」是常值區段，而且會出現在 "{id}" 之前，但 "pending" 最後會出現，因為**Order**屬性是1。 （此範例假設沒有名為「詳細資料」或「擱置」的客戶。 一般來說，請嘗試避免不明確的路由。 在此範例中，`GetByCustomer` 的較佳路由範本是 "customers/{customerName}"）
