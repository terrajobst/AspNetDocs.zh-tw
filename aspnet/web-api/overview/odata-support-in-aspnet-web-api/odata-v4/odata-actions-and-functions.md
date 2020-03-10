---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
title: 使用 ASP.NET Web API 2.2 的 OData v4 中的動作和函式 |Microsoft Docs
author: MikeWasson
description: 在 OData 中，動作和函式是一種新增伺服器端行為的方法，不容易定義為實體上的 CRUD 作業。 本教學課程顯示如何 。
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 0e6fb03c-b16d-4bb0-ab0b-552bd2b6ece1
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
msc.type: authoredcontent
ms.openlocfilehash: f5af94e93e5b7f2351d40febbf1a468d635c9db1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556221"
---
# <a name="actions-and-functions-in-odata-v4-using-aspnet-web-api-22"></a>使用 ASP.NET Web API 2.2 的 OData v4 中的動作和函式

由[Mike Wasson](https://github.com/MikeWasson)

> 在 OData 中，動作和函式是一種新增伺服器端行為的方法，不容易定義為實體上的 CRUD 作業。 本教學課程說明如何使用 Web API 2.2，將動作和函式加入至 OData v4 端點。 本教學課程是[以使用 ASP.NET Web API 2 建立 OData V4 端點](create-an-odata-v4-endpoint.md)教學課程為基礎
>
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
>
> - Web API 2。2
> - OData v4
> - Visual Studio 2013 （[在此](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)下載 Visual Studio 2017）
> - .NET 4.5
>
> ## <a name="tutorial-versions"></a>教學課程版本
>
> 針對 OData 第3版，請參閱[ASP.NET Web API 2 中的 Odata 動作](../odata-v3/odata-actions.md)。

*動作*和函式之間的差異在於動作可以有副作用，而函式則*不會。* 動作和函數都可以傳回資料。 某些動作的用途包括：

- 複雜交易。
- 一次處理數個實體。
- 僅允許更新實體的特定屬性。
- 傳送不是實體的資料。

函數適用于傳回未直接對應至實體或集合的資訊。

動作（或函式）可以將單一實體或集合設為目標。 在 OData 術語中，這是系*結。* 您也可以將 &quot;未系結的&quot; 動作/函式，稱為服務上的靜態作業。

## <a name="example-adding-an-action"></a>範例：新增動作

讓我們定義一個動作來為產品評分。

> [!NOTE]
> 本教學課程是[以使用 ASP.NET Web API 2 建立 OData V4 端點](create-an-odata-v4-endpoint.md)教學課程為基礎

首先，加入 `ProductRating` 模型來代表評等。

[!code-csharp[Main](odata-actions-and-functions/samples/sample1.cs)]

此外，也請將**DbSet**新增至 `ProductsContext` 類別，以便 EF 在資料庫中建立評等資料表。

[!code-csharp[Main](odata-actions-and-functions/samples/sample2.cs)]

### <a name="add-the-action-to-the-edm"></a>將動作新增至 EDM

在 WebApiConfig.cs 中，新增下列程式碼：

[!code-csharp[Main](odata-actions-and-functions/samples/sample3.cs)]

**EntityTypeConfiguration**方法會將動作加入至 entity data MODEL （EDM）。 **參數**方法會為動作指定具類型的參數。

此程式碼也會設定 EDM 的命名空間。 命名空間很重要，因為動作的 URI 包含完整的動作名稱：

[!code-console[Main](odata-actions-and-functions/samples/sample4.cmd)]

> [!NOTE]
> 在一般的 IIS 設定中，此 URL 中的點會導致 IIS 傳回錯誤404。 您可以藉由將下列區段新增至 web.config 檔案來解決此問題：

[!code-xml[Main](odata-actions-and-functions/samples/sample5.xml)]

### <a name="add-a-controller-method-for-the-action"></a>新增動作的控制器方法

若要啟用 &quot;速率&quot; 動作，請將下列方法新增至 `ProductsController`：

[!code-csharp[Main](odata-actions-and-functions/samples/sample6.cs)]

請注意，方法名稱符合動作名稱。 **[HttpPost]** 屬性會指定方法是 HTTP POST 方法。

若要叫用動作，用戶端會傳送 HTTP POST 要求，如下所示：

[!code-console[Main](odata-actions-and-functions/samples/sample7.cmd)]

&quot;速率&quot; 動作會系結至產品實例，因此動作的 URI 是附加至實體 URI 的完整動作名稱。 （回想一下，我們將 EDM 命名空間設定為 &quot;ProductService&quot;，因此完整的動作名稱 &quot;ProductService。速率&quot;）。

要求的主體會將動作參數包含為 JSON 承載。 Web API 會自動將 JSON 承載轉換成**ODataActionParameters**物件，這只是參數值的字典。 使用此字典來存取控制器方法中的參數。

如果用戶端以錯誤的格式傳送動作參數， **ModelState**的值就是 false。 請在控制器方法中檢查此旗標，並在 [ **IsValid** ] 為 false 時傳回錯誤。

[!code-csharp[Main](odata-actions-and-functions/samples/sample8.cs)]

## <a name="example-adding-a-function"></a>範例：新增函式

現在讓我們加入 OData 函式，以傳回成本最高的產品。 如先前所述，第一個步驟是將函式新增至 EDM。 在 WebApiConfig.cs 中，新增下列程式碼。

[!code-csharp[Main](odata-actions-and-functions/samples/sample9.cs)]

在此情況下，函數會系結至 Products 集合，而不是個別的產品實例。 用戶端會藉由傳送 GET 要求來叫用函式：

[!code-console[Main](odata-actions-and-functions/samples/sample10.cmd)]

以下是此函式的控制器方法：

[!code-csharp[Main](odata-actions-and-functions/samples/sample11.cs)]

請注意，方法名稱符合函數名稱。 **[HttpGet]** 屬性會指定方法是 HTTP GET 方法。

以下是 HTTP 回應：

[!code-console[Main](odata-actions-and-functions/samples/sample12.cmd)]

## <a name="example-adding-an-unbound-function"></a>範例：加入未系結的函式

上一個範例是系結至集合的函式。 在下一個範例中，我們將建立*未*系結的函式。 未系結的函式會在服務上呼叫為靜態作業。 此範例中的函式會傳回指定郵遞區號的銷售稅額。

在 WebApiConfig 檔案中，將函式新增至 EDM：

[!code-csharp[Main](odata-actions-and-functions/samples/sample13.cs)]

請注意，我們會直接在**用**上呼叫**函數**，而不是實體類型或集合。 這會告知模型產生器函式已解除系結。

以下是可實作用函式的控制器方法：

[!code-csharp[Main](odata-actions-and-functions/samples/sample14.cs)]

您放置此方法的 Web API 控制器並不重要。 您可以將它放在 `ProductsController`中，或定義個別的控制器。 **[ODataRoute]** 屬性會定義函式的 URI 範本。

以下是用戶端要求範例：

[!code-console[Main](odata-actions-and-functions/samples/sample15.cmd)]

HTTP 回應：

[!code-console[Main](odata-actions-and-functions/samples/sample16.cmd)]
