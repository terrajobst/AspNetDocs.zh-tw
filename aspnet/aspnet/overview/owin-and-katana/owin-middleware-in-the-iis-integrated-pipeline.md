---
uid: aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline
title: IIS 整合式管線中的 OWIN 中介軟體 |Microsoft Docs
author: Praburaj
description: 本文說明如何在 IIS 整合式管線中執行 OWIN 中介軟體元件（OMCs），以及如何設定 OMC 執行所在的管線事件。 您應該 。
ms.author: riande
ms.date: 11/07/2013
ms.assetid: d031c021-33c2-45a5-bf9f-98f8fa78c2ab
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline
msc.type: authoredcontent
ms.openlocfilehash: 7d157fb6bd9e2ae9b55af41ef06c1eb5e6310ce1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78617135"
---
# <a name="owin-middleware-in-the-iis-integrated-pipeline"></a>IIS 整合式管線中的 OWIN 中介軟體

[Praburaj Thiagarajan](https://github.com/Praburaj)， [Rick Anderson](https://twitter.com/RickAndMSFT)

> 本文說明如何在 IIS 整合式管線中執行 OWIN 中介軟體元件（OMCs），以及如何設定 OMC 執行所在的管線事件。 閱讀本教學課程之前，您應該先參閱專案 Katana 和[OWIN 啟動類別偵測](owin-startup-class-detection.md)[的總覽](an-overview-of-project-katana.md)。 本教學課程是由 Rick Anderson （ [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ）、Chris Ross、Praburaj Thiagarajan 和 Howard Dierking （ [@howard\_Dierking](https://twitter.com/howard_dierking) ）撰寫。

雖然[OWIN](an-overview-of-project-katana.md)中介軟體元件（OMCs）主要是設計成在伺服器中立的管線中執行，但也可以在 IIS 整合管線中執行 OMC （ ***不*支援傳統模式**）。 藉由從套件管理員主控台（PMC）安裝下列套件，可以在 IIS 整合式管線中進行 OMC：

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample1.cmd)]

這表示所有的應用程式架構（即使尚未在 IIS 和 System.web 以外執行的架構）都可以受益于現有的 OWIN 中介軟體元件。 

> [!NOTE]
> Visual Studio 2013 中新的身分識別系統（例如： Cookie、Microsoft 帳戶、Google、Facebook、Twitter、[持有人權杖](http://self-issued.info/docs/draft-ietf-oauth-v2-bearer.html)、OAuth、授權伺服器、JWT、Azure Active Directory 和 Active directory federation services）隨附的所有 `Microsoft.Owin.Security.*` 套件都會撰寫為 OMCs，而且可以用於自我裝載和 IIS 裝載的案例。

## <a name="how-owin-middleware-executes-in-the-iis-integrated-pipeline"></a>OWIN 中介軟體如何在 IIS 整合式管線中執行

針對 OWIN 主控台應用程式，使用[啟動](owin-startup-class-detection.md)設定所建立的應用程式管線，是由使用 `IAppBuilder.Use` 方法來新增元件的順序所設定。 也就是說， [Katana](an-overview-of-project-katana.md)執行時間中的 OWIN 管線會依照其使用 `IAppBuilder.Use`註冊的順序來處理 OMCs。 在 IIS 整合式管線中，要求管線是由已訂閱一組預先定義之管線事件（例如[BeginRequest](https://msdn.microsoft.com/library/system.web.httpapplication.beginrequest.aspx)、 [AuthenticateRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)、 [AuthorizeRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx)等）的[HttpModules](https://msdn.microsoft.com/library/ms178468(v=vs.85).aspx)所組成。

如果我們比較 OMC 與 ASP.NET 世界中的[HttpModule](https://msdn.microsoft.com/library/zec9k340(v=vs.85).aspx) ，則必須向正確的預先定義管線事件註冊 OMC。 例如，當要求進入管線中的[AuthenticateRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)階段時，HttpModule `MyModule` 會被叫用：

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample2.cs?highlight=10)]

為了讓 OMC 參與這項相同的事件型執行排序， [Katana](an-overview-of-project-katana.md)執行時間程式碼會掃描[啟動](owin-startup-class-detection.md)設定，並將每個中介軟體元件訂閱到整合式管線事件。 例如，下列 OMC 和註冊程式碼可讓您查看中介軟體元件的預設事件註冊。 （如需有關建立 OWIN 啟動類別的詳細指示，請參閱[OWIN 啟動類別偵測](owin-startup-class-detection.md)）。

1. 建立空白的 web 應用程式專案，並將其命名為**owin2**。
2. 從 [套件管理員主控台] （PMC）中，執行下列命令： 

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample3.cmd)]
3. 新增 `OWIN Startup Class`，並將其命名為 `Startup`。 將產生的程式碼取代為下列內容（變更會反白顯示）：  

    [!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample4.cs?highlight=5-7,15-36)]
4. 按 F5 以執行應用程式。

啟動設定會設定具有三個中間件元件的管線，前兩個會顯示診斷資訊，而最後一個則會回應事件（也會顯示診斷資訊）。 `PrintCurrentIntegratedPipelineStage` 方法會顯示此中介軟體叫用所在的整合式管線事件和訊息。 [輸出] 視窗會顯示下列內容：

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample5.cmd)]

根據預設，Katana 執行時間會將每個 OWIN 中介軟體元件對應到[PreExecuteRequestHandler](https://msdn.microsoft.com/library/system.web.httpapplication.prerequesthandlerexecute.aspx) ，而這會對應到 IIS 管線事件[PreRequestHandlerExecute](https://msdn.microsoft.com/library/system.web.httpapplication.prerequesthandlerexecute.aspx)。

## <a name="stage-markers"></a>階段標記

您可以使用 `IAppBuilder UseStageMarker()` 擴充方法，將 OMCs 標示為在管線的特定階段執行。 若要在特定階段執行一組中介軟體元件，請在註冊過程中，于最後一個元件之後插入階段標記。 您可以在管線的哪一個階段執行中介軟體，以及訂單元件必須執行的規則（本教學課程稍後會說明這些規則）。 將 `UseStageMarker` 方法新增至 `Configuration` 程式碼，如下所示：

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample6.cs?highlight=13,19)]

`app.UseStageMarker(PipelineStage.Authenticate)` 呼叫會設定所有先前註冊的中介軟體元件（在此案例中為我們的兩個診斷元件），以在管線的驗證階段執行。 最後一個中介軟體元件（顯示診斷和回應要求）會在 `ResolveCache` 階段執行（ [ResolveRequestCache](https://msdn.microsoft.com/library/system.web.httpapplication.resolverequestcache.aspx)事件）。

按 F5 以執行應用程式。[輸出] 視窗會顯示下列內容：

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample7.cmd)]

## <a name="stage-marker-rules"></a>階段標記規則

Owin 中介軟體元件（OMC）可以設定為在下列 OWIN 管線階段事件中執行：

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample8.cs)]

1. 根據預設，OMCs 會在最後一個事件（`PreHandlerExecute`）上執行。 這就是為什麼我們的第一個範例程式碼會顯示「PreExecuteRequestHandler」。
2. 您可以使用 `app.UseStageMarker` 方法，在 `PipelineStage` 列舉中列出的 OWIN 管線的任何階段，註冊要在先前執行的 OMC。
3. OWIN 管線和 IIS 管線會進行排序，因此 `app.UseStageMarker` 的呼叫必須是順序。 您無法將事件處理常式設定為在向註冊的最後一個事件之前的事件 `app.UseStageMarker`。 例如，*在呼叫之後*：

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample9.cmd)]

   將不會接受 `app.UseStageMarker` 傳遞 `Authenticate` 或 `PostAuthenticate` 的呼叫，也不會擲回任何例外狀況。 OMCs 會在最新階段執行，預設為 `PreHandlerExecute`。 階段標記是用來讓它們在稍早的時間執行。 如果您不按照順序指定階段標記，我們會四捨五入到先前的標記。 換句話說，新增階段標記會顯示「執行不晚于階段 X」。 OMC 會在 OWIN 管線中于其後面新增的最早階段標記執行。
4. 呼叫 `app.UseStageMarker` 獲勝的最早階段。 例如，如果您從先前的範例切換 `app.UseStageMarker` 呼叫的順序：

    [!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample10.cs?highlight=13,19)]

   [輸出] 視窗將會顯示： 

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample11.cmd)]

   OMCs 全都會在 `AuthenticateRequest` 階段中執行，因為最後一個 OMC 已向 `Authenticate` 事件註冊，而 `Authenticate` 事件在所有其他事件之前。
