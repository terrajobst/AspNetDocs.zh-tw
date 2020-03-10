---
uid: web-api/overview/error-handling/exception-handling
title: ASP.NET Web API 中的例外狀況處理-ASP.NET 4。x
author: MikeWasson
description: ''
ms.author: riande
ms.date: 03/12/2012
ms.custom: seoapril2019
ms.assetid: cbebeb37-2594-41f2-b71a-f4f26520d512
msc.legacyurl: /web-api/overview/error-handling/exception-handling
msc.type: authoredcontent
ms.openlocfilehash: dbdbab6aefec840e2fec9e9cd33f3d124093750e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622315"
---
# <a name="exception-handling-in-aspnet-web-api"></a>ASP.NET Web API 中的例外狀況處理

由[Mike Wasson](https://github.com/MikeWasson)

本文描述 ASP.NET Web API 中的錯誤和例外狀況處理。

- [HttpResponseException](#httpresponserexception)
- [例外狀況篩選條件](#exception_filters)
- [註冊例外狀況篩選準則](#registering_exception_filters)
- [HttpError](#httperror)

<a id="httpresponserexception"></a>
## <a name="httpresponseexception"></a>HttpResponseException

如果 Web API 控制器擲回未攔截的例外狀況，會發生什麼情況？ 根據預設，大部分的例外狀況會轉譯為 HTTP 回應，狀態碼為500、內部伺服器錯誤。

**HttpResponseException**類型是特殊案例。 這個例外狀況會傳回您在例外狀況函數中指定的任何 HTTP 狀態碼。 例如，如果*id*參數無效，下列方法會傳回404，但找不到。

[!code-csharp[Main](exception-handling/samples/sample1.cs)]

若要更充分掌控回應，您也可以建立整個回應訊息，並將它包含在**HttpResponseException 中：** 

[!code-csharp[Main](exception-handling/samples/sample2.cs)]

<a id="exception_filters"></a>
## <a name="exception-filters"></a>例外狀況篩選條件

您可以藉由撰寫*例外狀況篩選準則*來自訂 Web API 處理例外狀況的方式。 當控制器方法擲回*不*是**HttpResponseException**例外狀況的任何未處理例外狀況時，就會執行例外狀況篩選。 **HttpResponseException**類型是特殊案例，因為它是特別針對傳回 HTTP 回應而設計的。

例外狀況篩選準則會執行**IExceptionFilter**介面。 撰寫例外狀況篩選器的最簡單方式是衍生自**ExceptionFilterAttribute**類別，並覆寫**OnException**方法。

> [!NOTE]
> ASP.NET Web API 中的例外狀況篩選準則類似于 ASP.NET MVC。 不過，它們會分別在不同的命名空間和函式中宣告。 特別是，在 MVC 中使用的**system.web.mvc.handleerrorattribute class**類別不會處理 Web API 控制器所擲回的例外狀況。

以下是將**NotImplementedException**例外狀況轉換成 HTTP 狀態碼501的篩選準則，而不是實作為：

[!code-csharp[Main](exception-handling/samples/sample3.cs)]

**HttpActionExecutedCoNtext**物件的**Response**屬性包含將傳送至用戶端的 HTTP 回應訊息。

<a id="registering_exception_filters"></a>
## <a name="registering-exception-filters"></a>註冊例外狀況篩選準則

有數種方式可以註冊 Web API 例外狀況篩選︰

- 透過動作
- 透過控制器
- 全域

若要將篩選套用至特定動作，請在動作中新增篩選來做為屬性︰

[!code-csharp[Main](exception-handling/samples/sample4.cs)]

若要將篩選套用至控制器上的所有動作，請將篩選準則新增為控制器類別的屬性：

[!code-csharp[Main](exception-handling/samples/sample5.cs)]

若要將篩選準則全域套用至所有 Web API 控制器，請將篩選準則的實例新增至**GlobalConfiguration**集合。 此集合中的例外狀況篩選會套用至任何 Web API 控制器動作。

[!code-csharp[Main](exception-handling/samples/sample6.cs)]

如果您使用 ASP.NET MVC 4 Web 應用程式 專案範本來建立專案，請將您的 Web API 設定程式碼放在 `WebApiConfig` 類別中，此類別位於應用程式\_啟動 資料夾中：

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

<a id="httperror"></a>
## <a name="httperror"></a>HttpError

**HttpError**物件會提供一致的方式，在回應主體中傳回錯誤資訊。 下列範例示範如何在回應主體中傳回 HTTP 狀態碼404（找不到）和**HttpError** 。

[!code-csharp[Main](exception-handling/samples/sample8.cs)]

**CreateErrorResponse**是在**HttpRequestMessageExtensions**類別中定義的擴充方法。 就內部而言， **CreateErrorResponse**會建立**HttpError**實例，然後建立包含**HttpError**的**HttpResponseMessage** 。

在此範例中，如果方法成功，它會傳回 HTTP 回應中的產品。 但是，如果找不到要求的產品，則 HTTP 回應會在要求主體中包含**HttpError** 。 回應可能如下所示：

[!code-console[Main](exception-handling/samples/sample9.cmd)]

請注意，在此範例中， **HttpError**已序列化為 JSON。 使用**HttpError**的其中一個優點是，它會經歷與任何其他強型別模型相同的[內容協調](../formats-and-model-binding/content-negotiation.md)和序列化程式。

### <a name="httperror-and-model-validation"></a>HttpError 和模型驗證

若要進行模型驗證，您可以將模型狀態傳遞至**CreateErrorResponse**，以在回應中包含驗證錯誤：

[!code-csharp[Main](exception-handling/samples/sample10.cs)]

這個範例可能會傳回下列回應：

[!code-console[Main](exception-handling/samples/sample11.cmd)]

如需模型驗證的詳細資訊，請參閱[ASP.NET Web API 中的模型驗證](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)。

### <a name="using-httperror-with-httpresponseexception"></a>搭配使用 HttpError 與 HttpResponseException

先前的範例會從控制器動作傳回**HttpResponseMessage**訊息，但是您也可以使用**HttpResponseException**來傳回**HttpError**。 這可讓您在正常的成功情況下傳回強型別模型，而如果發生錯誤，仍然會傳回**HttpError** ：

[!code-csharp[Main](exception-handling/samples/sample12.cs)]
