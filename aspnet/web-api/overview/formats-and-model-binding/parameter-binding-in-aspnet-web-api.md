---
uid: web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
title: ASP.NET Web API 中的參數系結-ASP.NET 4。x
author: MikeWasson
description: 描述 Web API 如何系結參數，以及如何在 ASP.NET 4.x 中自訂系結程式。
ms.author: riande
ms.date: 07/11/2013
ms.custom: seoapril2019
ms.assetid: e42c8388-04ed-4341-9fdb-41b1b4c06320
msc.legacyurl: /web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 464cb9b45dc0b62c4da38b7cf612934808854d32
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557194"
---
# <a name="parameter-binding-in-aspnet-web-api"></a>ASP.NET Web API 中的參數系結

由[Mike Wasson](https://github.com/MikeWasson)

[!INCLUDE[](~/includes/coreWebAPI.md)]

本文說明 Web API 如何系結參數，以及如何自訂系結程式。 當 Web API 呼叫控制器上的方法時，它必須設定參數的值，這是一個稱為*binding*的進程。

根據預設，Web API 會使用下列規則來系結參數：

- 如果參數是「簡單」類型，Web API 會嘗試從 URI 取得值。 簡單類型包括 .NET[基本類型](https://msdn.microsoft.com/library/system.type.isprimitive.aspx)（**int**、 **bool**、 **double**等等），加上**TimeSpan**、 **DateTime**、 **Guid**、 **decimal**和**string**，*再加上*具有可從字串轉換之類型轉換器的任何類型。 （稍後會有關于類型轉換器的詳細資訊）。
- 針對複雜類型，Web API 會嘗試使用[媒體類型格式](media-formatters.md)器，從訊息本文中讀取值。

例如，以下是典型的 Web API 控制器方法：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample1.cs)]

*Id*參數是 &quot;簡單&quot; 類型，因此 Web API 會嘗試從要求 URI 取得值。 *Item*參數是複雜型別，因此 Web API 會使用媒體類型格式器來讀取來自要求主體的值。

為了從 URI 取得值，Web API 會在路由資料和 URI 查詢字串中尋找。 當路由系統剖析 URI 並使其符合路由時，就會填入路由資料。 如需詳細資訊，請參閱[路由和動作選取](../web-api-routing-and-actions/routing-and-action-selection.md)。

在本文的其餘部分，我將示範如何自訂模型系結程式。 不過，如果是複雜類型，請考慮盡可能使用媒體類型格式器。 HTTP 的主要原則是在訊息本文中傳送資源，使用內容協商來指定資源的標記法。 媒體類型格式器是專為此目的而設計的。

## <a name="using-fromuri"></a>使用 [FromUri]

若要強制 Web API 從 URI 讀取複雜型別，請將 **[FromUri]** 屬性加入至參數。 下列範例會定義 `GeoPoint` 型別，以及可從 URI 取得 `GeoPoint` 的控制器方法。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample2.cs)]

用戶端可以將緯度和經度值放在查詢字串中，而 Web API 會使用它們來建立 `GeoPoint`。 例如:

`http://localhost/api/values/?Latitude=47.678558&Longitude=-122.130989`

## <a name="using-frombody"></a>使用 [FromBody]

若要強制 Web API 從要求主體讀取簡單的類型，請將 **[FromBody]** 屬性加入至參數：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample3.cs)]

在此範例中，Web API 會使用媒體類型格式器來讀取要求主體中的*名稱*值。 以下是範例用戶端要求。

[!code-console[Main](parameter-binding-in-aspnet-web-api/samples/sample4.cmd)]

當參數具有 [FromBody] 時，Web API 會使用 Content-type 標頭來選取格式器。 在此範例中，內容類型為 &quot;application/json&quot;，而要求本文是原始 JSON 字串（而不是 JSON 物件）。

最多隻能有一個參數讀取訊息本文。 這將無法正常執行：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample5.cs)]

此規則的原因是要求主體可能儲存在只能讀取一次的非緩衝資料流程中。

## <a name="type-converters"></a>類型轉換器

您可以藉由建立**TypeConverter**並提供字串轉換，讓 web api 將類別視為簡單類型（因此 web api 會嘗試從 URI 系結）。

下列程式碼顯示代表地理點的 `GeoPoint` 類別，加上從字串轉換成 `GeoPoint` 實例的**TypeConverter** 。 `GeoPoint` 類別會以 **[TypeConverter]** 屬性裝飾，以指定類型轉換器。 （此範例是由 Mike 延遲的 blog 文章所靈感，[如何在 MVC/WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)中系結至動作簽章中的自訂物件）。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample6.cs)]

Web API 現在會將 `GeoPoint` 視為簡單的類型，這表示它會嘗試從 URI 系結 `GeoPoint` 參數。 您不需要在參數上包含 **[FromUri]** 。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample7.cs)]

用戶端可以使用如下的 URI 叫用方法：

`http://localhost/api/values/?location=47.678558,-122.130989`

## <a name="model-binders"></a>模型繫結器

比類型轉換器更有彈性的選項是建立自訂模型系結器。 使用模型系結器時，您可以存取來自路由資料的 HTTP 要求、動作描述和原始值等專案。

若要建立模型系結器，請執行**IModelBinder**介面。 這個介面會定義單一方法**BindModel**：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample8.cs)]

以下是 `GeoPoint` 物件的模型系結器。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample9.cs)]

模型系結器會從*值提供者*取得原始輸入值。 這種設計會分隔兩個不同的功能：

- 值提供者會接受 HTTP 要求，並填入索引鍵/值組的字典。
- 模型系結器會使用這個字典來填入模型。

Web API 中的預設值提供者會從路由資料和查詢字串中取得值。 例如，如果 URI 為 `http://localhost/api/values/1?location=48,-122`，則值提供者會建立下列機碼值組：

- 識別碼 = &quot;1&quot;
- location = &quot;48122&quot;

（我假設預設路由範本，也就是 &quot;api/{controller}/{id}&quot;）。

要系結的參數名稱會儲存在**ModelBindingCoNtext. ModelName**屬性中。 模型系結器會在字典中尋找具有此值的索引鍵。 如果值存在，而且可以轉換成 `GeoPoint`，則模型系結器會將系結值指派給**ModelBindingCoNtext 模型**屬性。

請注意，模型系結器並不限於簡單的類型轉換。 在此範例中，模型系結器會先在已知位置的資料表中尋找，如果失敗，則會使用類型轉換。

**設定模型系結器**

有數種方式可以設定模型系結器。 首先，您可以將 **[ModelBinder]** 屬性加入至參數。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample10.cs)]

您也可以將 **[ModelBinder]** 屬性加入至類型。 Web API 會針對該類型的所有參數使用指定的模型系結器。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample11.cs)]

最後，您可以將模型系結器提供者加入至**HttpConfiguration**。 模型系結器提供者只是建立模型系結器的 factory 類別。 您可以藉由衍生自[ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx)類別來建立提供者。 不過，如果您的模型系結器會處理單一型別，則使用專為此用途而設計的內建**SimpleModelBinderProvider**會比較容易。 下列程式碼示範如何執行這項操作。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample12.cs)]

使用模型系結提供者時，您仍然需要將 **[ModelBinder]** 屬性加入至參數，以告知 Web API 應該使用模型系結器，而不是媒體類型格式器。 但現在您不需要在屬性中指定模型系結器的類型：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample13.cs)]

## <a name="value-providers"></a>值提供者

我說過，模型系結器會從值提供者取得值。 若要撰寫自訂值提供者，請執行**IValueProvider**介面。 以下是從要求中的 cookie 提取值的範例：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample14.cs)]

您也必須藉由衍生自**ValueProviderFactory**類別，來建立值提供者 factory。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample15.cs)]

將值提供者 factory 新增至**HttpConfiguration** ，如下所示。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample16.cs)]

Web API 會撰寫所有的值提供者，因此當模型系結器呼叫**ValueProvider**時，模型系結器會從第一個值提供者接收能夠產生它的值。

或者，您可以使用**ValueProvider**屬性，在參數層級設定值提供者 factory，如下所示：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample17.cs)]

這會告知 Web API 使用模型系結搭配指定的值提供者 factory，而不是使用任何其他已註冊的值提供者。

## <a name="httpparameterbinding"></a>HttpParameterBinding

模型系結器是較通用機制的特定實例。 如果您查看 **[ModelBinder]** 屬性，您會看到它衍生自抽象的**ParameterBindingAttribute**類別。 這個類別會定義單一方法**getbindingexpression**，它會傳回**HttpParameterBinding**物件：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample18.cs)]

**HttpParameterBinding**會負責將參數系結至值。 在 **[ModelBinder]** 的案例中，屬性會傳回使用**IModelBinder**執行實際系結的**HttpParameterBinding**實值。 您也可以執行自己的**HttpParameterBinding**。

例如，假設您想要從 `if-match` 取得 Etag，並在要求中 `if-none-match` 標頭。 首先，我們會定義一個類別來代表 Etag。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample19.cs)]

我們也會定義列舉，指出是否要從 `if-match` 標頭或 `if-none-match` 標頭取得 ETag。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample20.cs)]

以下**HttpParameterBinding**會從所需的標頭取得 ETag，並將其系結至 etag 類型的參數：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample21.cs)]

**ExecuteBindingAsync**方法會執行系結。 在此方法中，將系結參數值新增至**HttpActionCoNtext**中的**ActionArgument**字典。

> [!NOTE]
> 如果您的**ExecuteBindingAsync**方法會讀取要求訊息的主體，請覆寫**WillReadBody**屬性以傳回 true。 要求主體可能是只能讀取一次的未緩衝資料流程，因此 Web API 會強制執行一個規則，其中最多隻能有一個系結讀取訊息本文。

若要套用自訂**HttpParameterBinding**，您可以定義衍生自**ParameterBindingAttribute**的屬性。 針對 `ETagParameterBinding`，我們將定義兩個屬性，一個用於 `if-match` 標頭，另一個用於 `if-none-match` 標頭。 兩者都是衍生自抽象基類。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample22.cs)]

以下是使用 `[IfNoneMatch]` 屬性的控制器方法。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample23.cs)]

除了**ParameterBindingAttribute**之外，還有另一個加入自訂**HttpParameterBinding**的勾點。 在**HttpConfiguration**物件上， **ParameterBindingRules**屬性是類型（**HttpParameterDescriptor** -&gt; **HttpParameterBinding**）之匿名函式的集合。 例如，您可以新增規則，GET 方法上的任何 ETag 參數都會使用 `ETagParameterBinding` 搭配 `if-none-match`：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample24.cs)]

函式應該會針對不適用系結的參數傳回 `null`。

## <a name="iactionvaluebinder"></a>IActionValueBinder

整個參數系結程式是由可插入的服務（ **IActionValueBinder**）所控制。 **IActionValueBinder**的預設執行會執行下列動作：

1. 在參數上尋找**ParameterBindingAttribute** 。 這包括 **[FromBody]** 、 **[FromUri]** 和 **[ModelBinder]** ，或自訂屬性。
2. 否則，請針對傳回非 null **HttpParameterBinding**的函式，尋找**HttpConfiguration. ParameterBindingRules** 。
3. 否則，請使用我先前所述的預設規則。 

    - 如果參數類型為 "simple" 或具有類型轉換器，請從 URI 進行系結。 這相當於將 **[FromUri]** 屬性放在參數上。
    - 否則，請嘗試從訊息本文中讀取參數。 這相當於將 **[FromBody]** 放在參數上。

如有需要，您可以將整個**IActionValueBinder**服務取代為自訂的執行。

## <a name="additional-resources"></a>其他資源

[自訂參數系結範例](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/CustomParameterBinding)

Mike 的停止寫了一系列有關 Web API 參數系結的絕佳 blog 文章：

- [Web API 如何進行參數系結](https://blogs.msdn.com/b/jmstall/archive/2012/04/16/how-webapi-does-parameter-binding.aspx)
- [Web API 的 MVC 樣式參數系結](https://blogs.msdn.com/b/jmstall/archive/2012/04/18/mvc-style-parameter-binding-for-webapi.aspx)
- [如何在 MVC/Web API 中系結至動作簽章中的自訂物件](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)
- [如何在 Web API 中建立自訂值提供者](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)
- [幕後的 Web API 參數系結](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)
