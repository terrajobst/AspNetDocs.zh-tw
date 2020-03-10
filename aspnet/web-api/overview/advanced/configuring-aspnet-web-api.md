---
uid: web-api/overview/advanced/configuring-aspnet-web-api
title: 設定 ASP.NET Web API 2-ASP.NET 4。x
author: MikeWasson
description: 為 ASP.NET 4.x 設定 ASP.NET Web API 2： Configure settings，ASP.NET 4.x 裝載，OWIN 自我裝載，全域服務和前控制站設定。
ms.author: riande
ms.date: 03/31/2014
ms.custom: seoapril2019
ms.assetid: 9e10a700-8d91-4d2e-a31e-b8b569fe867c
msc.legacyurl: /web-api/overview/advanced/configuring-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 4f76728fa5e4602e35e1b7cb2d41b2245093cad8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557719"
---
# <a name="configuring-aspnet-web-api-2"></a>設定 ASP.NET Web API 2

由[Mike Wasson](https://github.com/MikeWasson)

本主題描述如何設定 ASP.NET Web API。

- [設定](#settings)
- [設定具有 ASP.NET 裝載的 Web API](#webhost)
- [使用 OWIN 自我裝載設定 Web API](#selfhost)
- [全域 Web API 服務](#services)
- [每一控制器設定](#percontrollerconfig)

<a id="settings"></a>
## <a name="configuration-settings"></a>組態設定

Web API 設定是在[HttpConfiguration](https://msdn.microsoft.com/library/system.web.http.httpconfiguration.aspx)類別中定義。

| 成員 | 說明 |
| --- | --- |
| **DependencyResolver** | 啟用控制器的相依性插入。 請參閱[使用 WEB API 相依性解析程式](dependency-injection.md)。 |
| **篩選** | 動作篩選條件。 |
| **格式化** | [媒體類型](../formats-and-model-binding/media-formatters.md)格式器。 |
| **IncludeErrorDetailPolicy** | 指定伺服器是否應該在 HTTP 回應訊息中包含錯誤詳細資料，例如例外狀況訊息和堆疊追蹤。 請參閱[IncludeErrorDetailPolicy](https://msdn.microsoft.com/library/system.web.http.includeerrordetailpolicy(v=vs.108))。 |
| **初始** | 執行**HttpConfiguration**最後初始化的函式。 |
| **MessageHandlers** | [HTTP 訊息處理常式](http-message-handlers.md)。 |
| **ParameterBindingRules** | 在控制器動作上系結參數的規則集合。 |
| **內容** | 一般屬性包。 |
| **路由** | 路由的集合。 請參閱[ASP.NET Web API 中的路由](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)。 |
| **服務** | 服務的集合。 請參閱[服務](#services)。 |

## <a name="prerequisites"></a>Prerequisites

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community、Professional 或 Enterprise 版。

<a id="webhost"></a>
## <a name="configuring-web-api-with-aspnet-hosting"></a>設定具有 ASP.NET 裝載的 Web API

在 ASP.NET 應用程式中，呼叫 GlobalConfiguration 來設定 Web API。在**應用程式\_Start**方法中[設定](https://msdn.microsoft.com/library/system.web.http.globalconfiguration.configure.aspx)。 **Configure**方法會採用具有**HttpConfiguration**類型之單一參數的委派。 執行委派內的所有設定。

以下是使用匿名委派的範例：

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample1.cs)]

在 Visual Studio 2017 中，如果您在 [**新增 ASP.NET 專案**] 對話方塊中選取 [web API]，[ASP.NET Web 應用程式] 專案範本會自動設定設定程式碼。

[![](configuring-aspnet-web-api/_static/image2.png)](configuring-aspnet-web-api/_static/image1.png)

專案範本會在應用程式\_開始 資料夾內建立名為 WebApiConfig.cs 的檔案。 這個程式碼檔案會定義委派，您應該在其中放置 Web API 設定程式碼。

![](configuring-aspnet-web-api/_static/image3.png)

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample2.cs?highlight=12)]

專案範本也會將從應用程式呼叫委派的程式碼加入 **\_啟動**。

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample3.cs?highlight=5)]

<a id="selfhost"></a>
## <a name="configuring-web-api-with-owin-self-hosting"></a>使用 OWIN 自我裝載設定 Web API

如果您是使用 OWIN 自我裝載，請建立新的**HttpConfiguration**實例。 在此實例上執行任何設定，然後將實例傳遞至**Owin. UseWebApi**擴充方法。

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample4.cs)]

本教學課程[使用 OWIN 至自我裝載 ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)顯示完整的步驟。

<a id="services"></a>
## <a name="global-web-api-services"></a>全域 Web API 服務

**HttpConfiguration**集合包含一組全域服務，可供 Web API 用來執行各種工作，例如控制器選取和內容協調。

> [!NOTE]
> **服務**集合不是服務探索或相依性插入的一般用途機制。 它只會儲存 Web API 架構已知的服務類型。

**服務**集合會使用一組預設的服務進行初始化，您可以提供自己的自訂執行。 有些服務支援多個實例，而其他則只能有一個實例。 （不過，您也可以在控制器層級提供服務; 請參閱[每個控制器](#percontrollerconfig)設定。

單一實例服務

| 服務 | 說明 |
| --- | --- |
| **IActionValueBinder** | 取得參數的系結。 |
| **IApiExplorer** | 取得應用程式所公開之 Api 的描述。 請參閱[建立 WEB API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)的說明頁面。 |
| **IAssembliesResolver** | 取得應用程式的元件清單。 請參閱[路由和動作選取](../web-api-routing-and-actions/routing-and-action-selection.md)。 |
| **IBodyModelValidator** | 驗證由媒體類型格式器從要求主體讀取的模型。 |
| **IContentNegotiator** | 執行內容交涉。 |
| **IDocumentationProvider** | 提供 Api 的檔。 預設值是 **null**。 請參閱[建立 WEB API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)的說明頁面。 |
| **IHostBufferPolicySelector** | 指出主機是否應緩衝 HTTP 訊息實體內文。 |
| **IHttpActionInvoker** | 叫用控制器動作。 請參閱[路由和動作選取](../web-api-routing-and-actions/routing-and-action-selection.md)。 |
| **IHttpActionSelector** | 選取控制器動作。 請參閱[路由和動作選取](../web-api-routing-and-actions/routing-and-action-selection.md)。 |
| **IHttpControllerActivator** | 啟用控制器。 請參閱[路由和動作選取](../web-api-routing-and-actions/routing-and-action-selection.md)。 |
| **IHttpControllerSelector** | 選取控制器。 請參閱[路由和動作選取](../web-api-routing-and-actions/routing-and-action-selection.md)。 |
| **IHttpControllerTypeResolver** | 提供應用程式中的 Web API 控制器類型清單。 請參閱[路由和動作選取](../web-api-routing-and-actions/routing-and-action-selection.md)。 |
| **ITraceManager** | 初始化追蹤架構。 請參閱[ASP.NET Web API 中的追蹤](../testing-and-debugging/tracing-in-aspnet-web-api.md)。 |
| **ITraceWriter** | 提供追蹤寫入器。 預設值為「無 op」追蹤寫入器。 請參閱[ASP.NET Web API 中的追蹤](../testing-and-debugging/tracing-in-aspnet-web-api.md)。 |
| **IModelValidatorCache** | 提供模型驗證程式的快取。 |

多重實例服務

|                 服務                 |                                                                                                              說明                                                                                                               |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <strong>IFilterProvider</strong>     |                                                                                           傳回控制器動作的篩選器清單。                                                                                           |
|  <strong>ModelBinderProvider</strong>   |                                                                                                傳回給定類型的模型系結器。                                                                                                |
| <strong>ModelMetadataProvider</strong>  |                                                                                                     提供模型的中繼資料。                                                                                                     |
| <strong>ModelValidatorProvider</strong> |                                                                                                   提供模型的驗證程式。                                                                                                    |
|  <strong>ValueProviderFactory</strong>  | 建立值提供者。 如需詳細資訊，請參閱 Mike 延遲的 blog 文章[如何在 WebAPI 中建立自訂值提供者](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx) |

若要將自訂的執行加入多重實例服務，請在**服務**集合上呼叫**add**或**Insert** ：

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample5.cs)]

若要將單一實例服務取代為自訂的執行，請在**服務**集合上呼叫**replace** ：

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample6.cs)]

<a id="percontrollerconfig"></a>
## <a name="per-controller-configuration"></a>每一控制器設定

您可以根據每個控制器來覆寫下列設定：

- 媒體類型格式器
- 參數系結規則
- 服務

若要這樣做，請定義可執行**IControllerConfiguration**介面的自訂屬性。 然後將屬性套用至控制器。

下列範例會使用自訂格式器來取代預設的媒體類型格式器。

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample7.cs)]

**IControllerConfiguration**方法採用兩個參數：

- **HttpControllerSettings**物件
- **HttpControllerDescriptor**物件

**HttpControllerDescriptor**包含控制器的描述，您可以在其中檢查資訊的用途（例如，區分兩個控制器）。

使用**HttpControllerSettings**物件來設定控制器。 此物件包含您可以根據每個控制器覆寫之設定參數的子集。 您不會變更的任何設定都會預設為全域**HttpConfiguration**物件。
