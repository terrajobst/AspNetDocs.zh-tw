---
uid: web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
title: ASP.NET Web API 2 中的追蹤 |Microsoft Docs
author: MikeWasson
description: 顯示如何在 ASP.NET Web API 中啟用追蹤。
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 66a837e9-600b-4b72-97a9-19804231c64a
msc.legacyurl: /web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: a01acb649556d06ab9828ceab0fcbdf363bbc0d1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598550"
---
# <a name="tracing-in-aspnet-web-api-2"></a>ASP.NET Web API 2 中的追蹤

由[Mike Wasson](https://github.com/MikeWasson)

> 當您嘗試進行 web 應用程式的調試時，不會有一組不錯的追蹤記錄。 本教學課程說明如何在 ASP.NET Web API 中啟用追蹤。 您可以使用這項功能，追蹤 Web API 架構在叫用您的控制器之前和之後所執行的工作。 您也可以使用它來追蹤您自己的程式碼。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) （也適用于 Visual Studio 2015）
> - Web API 2
> - [WebApi. 追蹤](http://www.nuget.org/packages/Microsoft.AspNet.WebApi.Tracing)

## <a name="enable-systemdiagnostics-tracing-in-web-api"></a>在 Web API 中啟用系統診斷追蹤

首先，我們會建立新的 ASP.NET Web 應用程式專案。 在 Visual Studio 中，從 **[檔案**] 功能表選取 [**新增** > **專案**]。 在 [**範本**]**底下，選取**[ **ASP.NET web 應用程式**]。

[![](tracing-in-aspnet-web-api/_static/image2.png)](tracing-in-aspnet-web-api/_static/image1.png)

選擇 [Web API] 專案範本。

[![](tracing-in-aspnet-web-api/_static/image4.png)](tracing-in-aspnet-web-api/_static/image3.png)

從 [**工具**] 功能表中，依序選取 [ **NuGet 套件管理員**] 和 [**套件管理主控台**]。

在 [套件管理員主控台] 視窗中，輸入下列命令。

[!code-console[Main](tracing-in-aspnet-web-api/samples/sample1.cmd)]

第一個命令會安裝最新的 Web API 追蹤封裝。 它也會更新核心 Web API 套件。 第二個命令會將 WebApi. WebHost 套件更新為最新版本。

> [!NOTE]
> 如果您想要以特定版本的 Web API 為目標，請在安裝追蹤套件時使用-Version 旗標。

開啟應用程式\_[開始] 資料夾中的檔案 WebApiConfig.cs。 將下列程式碼新增至**Register**方法。

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample2.cs?highlight=6)]

此程式碼會將[SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx)類別新增至 Web API 管線。 **SystemDiagnosticsTraceWriter**類別會將追蹤寫入至[system.object](https://msdn.microsoft.com/library/system.diagnostics.trace)。

若要查看追蹤，請在偵錯工具中執行應用程式。 在瀏覽器中，瀏覽至 `/api/values`。

![](tracing-in-aspnet-web-api/_static/image5.png)

追蹤語句會寫入 Visual Studio 的 [輸出] 視窗中。 （從 [ **View** ] 功能表選取 [**輸出**]）。

[![](tracing-in-aspnet-web-api/_static/image7.png)](tracing-in-aspnet-web-api/_static/image6.png)

因為**SystemDiagnosticsTraceWriter**會將追蹤寫入至**system.webserver**，所以您可以註冊其他追蹤接聽項;例如，將追蹤寫入記錄檔。 如需追蹤寫入器的詳細資訊，請參閱 MSDN 上的[追蹤](https://msdn.microsoft.com/library/4y5y10s7.aspx)接聽項主題。

### <a name="configuring-systemdiagnosticstracewriter"></a>設定 SystemDiagnosticsTraceWriter

下列程式碼顯示如何設定追蹤寫入器。

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample3.cs)]

有兩個設定可供您控制：

- IsVerbose：如果為 false，則每個追蹤都包含最少的資訊。 若為 true，追蹤會包含詳細資訊。
- MinimumLevel：設定最小追蹤層級。 追蹤層級（依序）為 Debug、Info、警告、Error 和嚴重。

## <a name="adding-traces-to-your-web-api-application"></a>將追蹤新增至您的 Web API 應用程式

新增追蹤寫入器可讓您立即存取 Web API 管線所建立的追蹤。 您也可以使用追蹤寫入器來追蹤您自己的程式碼：

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample4.cs)]

若要取得追蹤寫入器，請呼叫**HttpConfiguration。 GetTraceWriter**。 在控制器上，此方法可透過**ApiController**屬性來存取。

若要撰寫追蹤，您可以直接呼叫**ITraceWriter**方法，但是[ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx)類別會定義一些較容易瞭解的擴充方法。 例如，上面顯示的**Info**方法會建立具有追蹤層級**資訊**的追蹤。

## <a name="web-api-tracing-infrastructure"></a>Web API 追蹤基礎結構

本節說明如何撰寫 Web API 的自訂追蹤寫入器。

WebApi. 追蹤套件是以 Web API 中更通用的追蹤基礎結構來建立。 除了使用 WebApi，您也可以插入一些其他的追蹤/記錄程式庫，例如[NLog](http://nlog-project.org/)或[log4net](http://logging.apache.org/log4net/)。

若要收集追蹤，請執行**ITraceWriter**介面。 以下是一個簡單的範例：

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample5.cs)]

**ITraceWriter**方法會建立追蹤。 呼叫者會指定分類和追蹤層級。 類別可以是任何使用者定義的字串。 您的**追蹤**執行應該會進行下列動作：

1. 建立新的**TraceRecord**。 使用要求、類別和追蹤層級將它初始化，如下所示。 這些值是由呼叫端提供。
2. 叫用*traceAction*委派。 在此委派中，呼叫端應該填入**TraceRecord**的其餘部分。
3. 使用您喜歡的任何記錄技術來撰寫**TraceRecord**。 此處顯示的範例只會呼叫**system.object**。

## <a name="setting-the-trace-writer"></a>設定追蹤寫入器

若要啟用追蹤，您必須設定 Web API 以使用您的**ITraceWriter**執行。 您可以透過**HttpConfiguration**物件來執行此動作，如下列程式碼所示：

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample6.cs)]

只有一個追蹤寫入器可以處於作用中狀態。 根據預設，Web API 會設定不會執行任何作業的 &quot;無 op&quot; 追蹤。 （&quot;無作業&quot; 追蹤存在，因此追蹤程式碼不需要在寫入追蹤之前檢查追蹤寫入器是否為**null** ）。

## <a name="how-web-api-tracing-works"></a>Web API 追蹤的運作方式

Web API 中的追蹤會使用*外觀*模式：當啟用追蹤時，Web API 會使用執行追蹤呼叫的類別來包裝要求管線的各個部分。

例如，選取控制器時，管線會使用**IHttpControllerSelector**介面。 啟用追蹤之後，管線會插入一個可執行**IHttpControllerSelector**的類別，但會呼叫實際執行的：

![Web API 追蹤會使用面板模式。](tracing-in-aspnet-web-api/_static/image8.png)

這項設計的優點包括：

- 如果您沒有新增追蹤寫入器，追蹤元件就不會具現化，而且不會影響效能。
- 如果您使用自己的自訂執行來取代預設服務（例如**IHttpControllerSelector** ），則不會影響追蹤，因為追蹤是由包裝函式物件進行。

您也可以取代預設的**ITraceManager**服務，將整個 Web API 追蹤架構取代成您自己的自訂架構：

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample7.cs)]

執行**ITraceManager** ，將您的追蹤系統初始化。 請注意，這會取代*整個*追蹤架構，包括 Web API 內建的所有追蹤程式碼。
