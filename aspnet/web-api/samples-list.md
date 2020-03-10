---
uid: web-api/samples-list
title: Web API 範例清單-ASP.NET 4。x
author: rick-anderson
description: ASP.NET 4.x 的 ASP.NET Web API 範例清單
ms.author: riande
ms.date: 09/18/2012
ms.custom: seoapril2019
ms.assetid: 8cbd9d7f-7027-4390-b098-cb81a63ecd6f
msc.legacyurl: /web-api/samples-list
msc.type: content
ms.openlocfilehash: 24368fc80e7fc3c840f1f1f9accf13fa15a06c1b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598459"
---
# <a name="web-api-samples-list"></a>Web API 範例清單

## <a name="httpclient-samples"></a>HttpClient 範例

**Bing 翻譯範例** | [VS 2012 來源](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/BingTranslateSample)

示範如何使用**HttpClient**類別呼叫[Microsoft Translator 服務](https://msdn.microsoft.com/library/ff512419.aspx)。 Microsoft Translator 服務 API 需要 OAuth 權杖，應用程式會針對每個對 Translator 服務提出的要求，將要求傳送至 Azure 權杖伺服器，藉此取得。 權杖伺服器的結果會送到傳送至轉譯服務的要求中。 執行此範例之前，您必須[從 Azure Marketplace 取得應用程式金鑰](https://msdn.microsoft.com/library/hh454950.aspx)，並填入 AccessTokenMessageHandler 範例類別中的資訊。

**Google Maps 範例** | [詳細描述](https://blogs.msdn.com/b/henrikn/archive/2012/02/17/downloading-a-google-map-to-local-file.aspx) | [VS 2012 來源](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/GoogleMapsSample)

使用**HttpClient**從[Google Maps API](https://developers.google.com/maps/)下載 Redmond，WA 的地圖，將其儲存為本機檔案，並開啟預設的影像檢視器。

**Twitter 用戶端範例** |  | [VS 2012 來源](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/TwitterSample)的[詳細描述](https://blogs.msdn.com/b/henrikn/archive/2012/02/16/extending-httpclient-with-oauth-to-access-twitter.aspx)

說明如何使用**HttpClient**撰寫簡單的 Twitter 用戶端。 此範例會使用**HttpMessageHandler** ，將 OAuth 驗證資訊插入傳出的**HttpRequestMessage**中。 Twitter 的結果是使用 JSON.NET 來讀取。 執行此範例之前，您必須[從 Twitter 取得應用程式金鑰](https://dev.twitter.com/)，並填寫 OAuthMessageHandler 範例類別中的資訊。

**全球銀行範例** |  | [vs 2010 來源](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/WorldBankSample/Net40) | [與2012來源](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/WorldBankSample/Net45)的[詳細描述](https://blogs.msdn.com/b/henrikn/archive/2012/02/16/httpclient-is-here.aspx)

示範如何使用 JSON.NET 來剖析結果，以從 World Bank 資料網站取出資料。

## <a name="web-api-samples"></a>Web API 範例

**具有 ASP.NET Web API** | [VS 2012 來源](overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)的消費者入門

說明如何建立支援 HTTP GET 要求的基本 Web API。 包含[第一個 ASP.NET Web API](overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)教學課程的原始程式碼。

**ASP.NET Web API JavaScript 案例-**  | [與2012來源](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)的批註

示範如何使用 ASP.NET Web API 來建立支援瀏覽器用戶端的 Web Api，並可使用 jQuery 輕鬆地呼叫。

**連絡人管理員** | [VS 2010 來源](https://code.msdn.microsoft.com/Contact-Manager-Web-API-0e8e373d)

這個範例會使用 ASP.NET Web API 來建立簡單的連絡人管理員應用程式。 應用程式是由 ASP.NET MVC 應用程式所使用的連絡人管理員 Web API 所組成，而 Windows Phone 應用程式則是用來顯示和管理連絡人清單。

**批次處理範例** | [詳細描述](http://trocolate.wordpress.com/2012/07/19/mitigate-issue-260-in-batching-scenario/) | [VS 2012 來源](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/BatchSample)

示範如何在 ASP.NET 內執行 HTTP 批次處理。 批次處理包含將多個 HTTP 要求放在單一 MIME 多部分實體主體中，然後以 HTTP POST 的形式傳送到伺服器。 要求會個別處理，而回應會放在另一個 MIME 多部分實體主體中，並傳回給用戶端。

**內容控制器範例** |  | [vs 2010 來源](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/ContentControllerSample/Net40) | [與2012來源](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/ContentControllerSample/Net45)的[詳細描述](https://blogs.msdn.com/b/henrikn/archive/2012/02/24/async-actions-in-asp-net-web-api.aspx)

示範如何使用資料流程以非同步方式讀取和寫入要求和回應實體。 範例控制器有兩個動作：一個 PUT 動作，會以非同步方式讀取要求實體本文，並將其儲存在本機檔案中，以及可傳回本機檔案內容的 GET 動作。

**自訂群組件解析程式範例** | [VS 2012 來源](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomAssemblyResolverSample)

說明如何修改 ASP.NET Web API，以支援從動態載入的程式庫元件探索控制器。 此範例會執行自訂**IAssembliesResolver** ，其會呼叫預設的實作為，然後將程式庫元件新增至預設結果。

**自訂媒體類型格式器範例** |  | [VS 2010 來源](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomMediaTypeFormatterSample)的[詳細描述](https://blogs.msdn.com/b/henrikn/archive/2012/04/23/using-cookies-with-asp-net-web-api.aspx)

示範如何使用**BufferedMediaTypeFormatter**基類來建立自訂媒體類型格式器。 這個基類適用于主要使用同步讀取和寫入作業的格式器。 除了顯示媒體類型格式器之外，此範例也會示範如何將它註冊為應用程式**HttpConfiguration**的一部分，藉以進行連結。 請注意，您也可以直接使用**MediaTypeFormatter**基類，針對主要使用非同步讀取和寫入作業的格式器。

**自訂參數**系結範例 |  | [VS 2010 來源](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomParameterBinding)的[詳細描述](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)

示範如何自訂參數系結程式，這是判斷要求中的資訊如何系結至動作參數的程式。 在此範例中，主控制器有四個動作：

1. BindPrincipal 顯示如何從自訂泛型主體系結 IPrincipal 參數，而不是從 HTTP GET message 系結。
2. BindCustomComplexTypeFromUriOrBody 顯示如何系結複雜型別參數，這可能來自于訊息內文或 HTTP POST 訊息的要求 URI;
3. BindCustomComplexTypeFromUriWithRenamedProperty 顯示如何使用已重新命名的屬性（來自 HTTP POST 訊息的要求 URI）來系結複雜型別參數;
4. PostMultipleParametersFromBody 顯示如何從 POST 訊息的主體系結多個參數;

檔案**上傳範例** |  | [VS 2012 來源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/FileUploadSample)的[詳細描述](https://blogs.msdn.com/b/henrikn/archive/2012/03/01/file-upload-and-asp-net-web-api.aspx)

示範如何使用 MIME 多元件檔案上傳將檔案上傳至**ApiController** ，以及如何使用**ProgressNotificationHandler**設定**HttpClient**的進度通知。 控制器會以非同步方式讀取 HTML 檔案上傳的內容，並將一或多個內文部分寫入本機檔案。 回應包含上傳檔案（或檔案）的相關資訊。

檔案**上傳至 Azure Blob 存放區範例** | [詳細描述](https://blogs.msdn.com/b/yaohuang1/archive/2012/07/02/asp-net-web-api-and-azure-blob-storage.aspx) | [VS 2012 來源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/AzureBlobsFileUploadSample)

這個範例與檔案上傳範例類似，但它不會將上傳的檔案儲存在本機磁片上，而是使用[Windows AZURE SDK for .net](https://www.windowsazure.com/develop/net/)以非同步方式將檔案上傳至[Azure Blob 存放區](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)。 它也會提供一種機制，列出目前存在於[Azure Blob 儲存體容器](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)中的 blob。 您可以嘗試針對隨附于 Azure SDK **Azure 儲存體模擬器**執行的範例。 如果您有[Azure 儲存體帳戶](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)，您也可以對實際的儲存體服務執行。

**Http 訊息處理常式管線範例** |  | [VS 2010 來源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/HttpMessageHandlerPipelineSample)的[詳細描述](https://blogs.msdn.com/b/henrikn/archive/2012/08/07/httpclient-httpclienthandler-and-httpwebrequesthandler.aspx)

示範如何在用戶端（**HttpClient**）和伺服器（ASP.NET Web API）上連接**HttpMessageHandler**實例。 在此範例中，會在用戶端和伺服器上使用相同的處理常式。 雖然在這兩個地方都不會同時執行相同的處理常式，但在用戶端和伺服器端上，物件模型都是一樣的。

**JSON 上傳範例** | [VS 2012 來源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/JsonUploadSample)

示範如何在**ApiController**上傳和下載 JSON。 此範例會使用最少的**ApiController** ，並使用**HttpClient**來存取它。

**混合範例** |  | [VS 2012 來源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MashupSample)的[詳細描述](https://blogs.msdn.com/b/henrikn/archive/2012/03/03/async-mashups-using-asp-net-web-api.aspx)

示範如何從**ApiController**動作內部以非同步方式存取多個遠端網站。 每次叫用動作時，都會以非同步方式執行要求，因此不會封鎖任何執行緒。

**記憶體追蹤範例** | [詳細描述](https://blogs.msdn.com/b/roncain/archive/2012/04/12/tracing-in-asp-net-web-api.aspx) | [VS 2010 來源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MemoryTracingSample)

這個範例專案會建立 Nuget 封裝，以將自訂記憶體中的追蹤寫入器安裝到 ASP.NET Web API 應用程式中。

**MongoDB 範例** |  | [VS 2012 來源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MongoSample)的[詳細描述](https://blogs.msdn.com/b/henrikn/archive/2012/02/19/using-web-api-with-mongodb.aspx)

示範如何使用 MongoDB 做為**ApiController**的持續性存放區，並使用儲存機制模式。

**回應主體處理器範例** | [VS 2012 來源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/ResponseEntityProcessorSample)

示範如何將回應實體（也就是 HTTP 回應主體）複製到本機檔案，再將它傳送至用戶端，並以非同步方式對該檔案執行額外的處理。 此範例會執行包裝回應實體的**HttpMessageHandler** ，其會將本身以一般方式寫入輸出，並將其寫到本機檔案。

**上傳 XDocument 範例** | [詳細描述](https://blogs.msdn.com/b/henrikn/archive/2012/02/17/push-and-pull-streams-using-httpclient.aspx) | [VS 2012 來源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/UploadXDocumentSample)

示範如何使用**PushStreamContent**和**HttpClient**將 XDocument 上傳至**ApiController** 。

 | [VS 2010 來源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/ValidationSample)的**驗證範例**

顯示如何在 ASP.NET WebAPI 中的模型上使用驗證屬性，以驗證 HTTP 要求的內容。 示範如何將屬性標示為必要，如何使用架構定義和自訂驗證屬性來標注您的模型，以及如何針對不正確模型狀態傳回錯誤回應。

**Web Form 範例** | [詳細描述](https://blogs.msdn.com/b/henrikn/archive/2012/02/23/using-asp-net-web-api-with-asp-net-web-forms.aspx) | [VS 2010 來源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/WebFormSample)

顯示加入至 Web Forms 專案的 ApiController。

**[RestBugs 範例](https://github.com/howarddierking/RestBugs)**

RestBugs 是簡單的錯誤追蹤應用程式，示範如何使用 ASP.NET Web API 和新的 HTTP 用戶端程式庫來建立超媒體驅動的系統。 此範例會使用 ASP.NET Web API，同時包含用戶端和伺服器的執行。 伺服器會使用自訂的 Razor 格式器來產生資源標記法。 此範例也提供 node.js 伺服器，說明使用超媒體設計來將用戶端和伺服器分離的優點。
