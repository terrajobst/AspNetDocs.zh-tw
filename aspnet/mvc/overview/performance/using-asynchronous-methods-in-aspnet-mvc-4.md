---
uid: mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4
title: 在 ASP.NET MVC 4 中使用非同步方法 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您如何使用適用于 Web 的 Visual Studio Express 2012 建立異步 ASP.NET MVC Web 應用程式的基本概念，這是免費的 。
ms.author: riande
ms.date: 06/06/2012
ms.assetid: a56572ba-81c3-47af-826d-941e9c4775ec
msc.legacyurl: /mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 15692b18fc112c4c6cce4d50a243a0e8d5fb52a4
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457748"
---
# <a name="using-asynchronous-methods-in-aspnet-mvc-4"></a>在 ASP.NET MVC 4 中使用非同步方法

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教學課程將教您使用[Visual Studio Express 2012 For web](https://www.microsoft.com/visualstudio/11)（這是免費版本的 Microsoft Visual Studio）建立異步 ASP.NET MVC Web 應用程式的基本概念。 您也可以使用[Visual Studio 2012](https://www.microsoft.com/visualstudio/11)。
> 
> 本教學課程的 github 上提供完整的範例[https://github.com/RickAndMSFT/Async-ASP.NET/](https://github.com/RickAndMSFT/Async-ASP.NET/)

結合[.net 4.5](https://msdn.microsoft.com/library/w0x726c2(VS.110).aspx)的 ASP.NET MVC 4[控制器](https://msdn.microsoft.com/library/system.web.mvc.controller(VS.108).aspx)類別，可讓您撰寫非同步動作方法，以傳回 Task 類型的物件， [&lt;ActionResult&gt;](https://msdn.microsoft.com/library/dd321424(VS.110).aspx)。 .NET Framework 4 引進了[一種非同步](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)程式設計概念，稱為工作，而 ASP.NET MVC 4[支援工作](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)。 **工作是以工作類型和**[[系統執行緒](https://msdn.microsoft.com/library/system.threading.tasks.aspx)] 命名空間中的相關類型來表示。 .NET Framework 4.5 是以具有[await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)和[async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)關鍵字的非同步支援為基礎，這些都是[使用工作物件，](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)而不是比先前的非同步方法更複雜。 [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)關鍵字是語法速記，表示程式碼段應該以非同步方式等候某個程式碼的其他部分。 [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)關鍵字代表一個提示，可讓您將方法標示為以工作為基礎的非同步方法。 **Await**、 **async**和**Task**物件的組合，可讓您更輕鬆地在 .net 4.5 中撰寫非同步程式碼。 非同步方法的新模型稱為以工作為*基礎的非同步模式* **（點**一下）。 本教學課程假設您已熟悉使用[await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)和[async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)關鍵字[和工作命名](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)空間的非同步程式設計。

如需有關使用[await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)和[async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)關鍵字和[工作命名空間](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)的詳細資訊，請參閱下列參考。

- [技術白皮書： .NET 中的非同步](https://go.microsoft.com/fwlink/?LinkId=204844)
- [Async/Await 常見問題](https://blogs.msdn.com/b/pfxteam/archive/2012/04/12/10293335.aspx)
- [Visual Studio 非同步程式設計](https://msdn.microsoft.com/vstudio/gg316360)

## <a id="HowRequestsProcessedByTP"></a>執行緒集區處理要求的方式

在 web 伺服器上，.NET Framework 會維護用來為 ASP.NET 要求提供服務的執行緒集區。 要求到達網頁伺服器時，集區中會分派一個執行緒來處理該要求。 如果要求是以同步方式處理，處理要求的執行緒就會在處理要求時忙碌，而且該執行緒無法服務另一個要求。   
  
這可能不是問題，因為執行緒集區的大小可以夠大，足以容納許多忙碌中的執行緒。 不過，執行緒集區中的執行緒數目有限（.NET 4.5 的預設最大值為5000）。 在高並行處理長時間執行之要求的大型應用程式中，所有可用的執行緒可能都很忙碌。 這種狀況稱為「執行緒耗盡」(Thread Starvation)。 當達到此條件時，web 伺服器會將要求排入佇列。 如果要求佇列已滿，web 伺服器會拒絕 HTTP 503 狀態的要求（伺服器太忙碌）。 CLR 執行緒集區對於新的執行緒插入有限制。 如果並行處理是暴增的（也就是說，您的網站可能突然收到大量的要求），而且所有可用的要求執行緒都忙碌，因為具有高延遲的後端呼叫，限制的執行緒插入速率可能會讓您的應用程式回應變得非常差。 此外，新增至執行緒集區的每個新執行緒都有額外負荷（例如 1 MB 的堆疊記憶體）。 使用同步方法來服務高延遲呼叫的 web 應用程式，其中線程集區會成長至 .NET 4.5 預設最大值5，000個執行緒會耗用大約 5 GB 的記憶體，而不是使用可服務相同要求的應用程式非同步方法和僅限50執行緒。 當您執行非同步工作時，不一定是使用執行緒。 例如，當您進行非同步 web 服務要求時，ASP.NET 將不會在**非同步**方法呼叫和**await**之間使用任何執行緒。 使用執行緒集區來服務具有高延遲的要求，可能會導致大量的記憶體耗用量和伺服器硬體的使用率不佳。

## <a name="processing-asynchronous-requests"></a>處理非同步要求

在啟動時看到大量並行要求或具有暴增負載的 web 應用程式（並行成長突然增加），讓 web 服務呼叫非同步增加應用程式的回應能力。 非同步要求所需的處理時間與同步要求相同。 如果要求發出 web 服務呼叫，需要兩秒的時間才能完成，則要求需要兩秒鐘的時間，不論是以同步或非同步方式執行。 不過，在非同步呼叫期間，執行緒在等候第一個要求完成時，不會遭到封鎖而無法回應其他要求。 因此，當有多個並行要求會叫用長時間執行的作業時，非同步要求會阻止要求佇列和執行緒集區成長。

## <a id="ChoosingSyncVasync"></a>選擇同步或非同步動作方法

本節列出何時使用同步或非同步動作方法的方針。 這些只是指導方針;個別檢查每個應用程式，以判斷非同步方法是否有助於效能。

一般而言，在下列情況下，請使用同步方法：

- 作業很簡單或執行時間短暫。
- 簡潔比效率重要。
- 作業主要都是 CPU 作業，而非需要耗用大量磁碟或網路的作業。 對受限於 CPU 的作業採用非同步動作並沒有好處，甚至會增加負擔。

一般而言，在下列情況下，請使用非同步方法：

- 您正在呼叫可透過非同步方法取用的服務，而且您使用的是 .NET 4.5 或更高版本。
- 作業受限於網路或 I/O，而非 CPU。
- 平行處理比簡化程式碼重要。
- 您想提供可讓使用者取消長期執行要求的機制。
- 當切換執行緒的好處高於內容切換的成本時。 一般來說，如果同步方法在不執行任何工作的情況下等候 ASP.NET 要求執行緒，您應該將方法設為非同步。 藉由讓呼叫非同步，ASP.NET 要求執行緒在等待 web 服務要求完成時，不會停止執行任何工作。
- 測試會顯示封鎖作業是網站效能的瓶頸，而 IIS 可以針對這些封鎖呼叫使用非同步方法來服務更多要求。

前述可下載的範例會說明如何有效地使用非同步動作方法。 所提供的範例是設計用來在使用 .NET 4.5 的 ASP.NET MVC 4 中提供非同步程式設計的簡單示範。 此範例不是為了在 ASP.NET MVC 中進行非同步程式設計的參考架構。 範例程式會呼叫[ASP.NET Web API](../../../web-api/index.md)方法，然後再呼叫工作[。延遲](https://msdn.microsoft.com/library/hh139096(VS.110).aspx)以模擬長時間執行的 Web 服務呼叫。 大部分的生產應用程式都不會顯示使用非同步動作方法的明顯好處。   
  
有些應用程式會要求所有動作方法都是非同步的。 有時候將一些同步動作方法轉換為非同步方法，對於所需的工作量而言可以提高最多效率。

## <a id="SampleApp"></a>範例應用程式

您可以從[GitHub](https://github.com/)網站上的[https://github.com/RickAndMSFT/Async-ASP.NET/](https://github.com/RickAndMSFT/Async-ASP.NET)下載範例應用程式。 存放庫是由三個專案所組成：

- *Mvc4Async*： ASP.NET MVC 4 專案，其中包含本教學課程中使用的程式碼。 它會對**WebAPIpgw**服務發出 Web API 呼叫。
- *WebAPIpgw*：用來執行 `Products, Gizmos and Widgets` 控制器的 ASP.NET MVC 4 Web API 專案。 它會提供*WebAppAsync*專案和*Mvc4Async*專案的資料。
- *WebAppAsync*：另一個教學課程中使用的 ASP.NET Web Forms 專案。

## <a id="GizmosSynch"></a>Gizmos 同步動作方法

 下列程式碼顯示用來顯示 gizmos 清單的 `Gizmos` 同步動作方法。 （在本文中，gizmo 是虛構的機械裝置）。 

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample1.cs)]

下列程式碼顯示 gizmo 服務的 `GetGizmos` 方法。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample2.cs)]

`GizmoService GetGizmos` 方法會將 URI 傳遞給 ASP.NET Web API HTTP 服務，以傳回 gizmos 資料的清單。 *WebAPIpgw*專案包含 `gizmos, widget` 和 `product` 控制器的 Web API 的執行。  
下圖顯示範例專案中的 gizmos 視圖。

![Gizmos](using-asynchronous-methods-in-aspnet-mvc-4/_static/image1.png)

## <a id="CreatingAsynchGizmos"></a>建立異步 Gizmos 動作方法

此範例使用新的[async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)和[await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)關鍵字（可在 .net 4.5 和 Visual Studio 2012 中取得），讓編譯器負責維護非同步程式設計所需的複雜轉換。 編譯器可讓您使用C#的同步控制流程結構來撰寫程式碼，而編譯器會自動套用使用回呼所需的轉換，以避免封鎖執行緒。

下列程式碼顯示 `Gizmos` 同步方法和 `GizmosAsync` 非同步方法。 如果您的瀏覽器支援[HTML 5 `<mark>` 元素](http://www.w3.org/wiki/HTML/Elements/mark)，您會在 `GizmosAsync` 的黃色醒目提示中看到變更。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample3.cs)]

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample4.cs?highlight=1,3,5)]

 已套用下列變更，以允許 `GizmosAsync` 非同步。

- 方法會以[async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)關鍵字標示，這會告訴編譯器為本文的部分產生回呼，並自動建立傳回的 `Task<ActionResult>`。
- &quot;非同步&quot; 附加至方法名稱。 不需要附加 "Async"，而是撰寫非同步方法時的慣例。
- 傳回類型已從 `ActionResult` 變更為 `Task<ActionResult>`。 `Task<ActionResult>` 的傳回類型代表進行中的工作，並提供方法的呼叫端，以及等候非同步作業完成的控制碼。 在此情況下，呼叫端是 web 服務。 `Task<ActionResult>` 代表進行中的工作，其結果為 `ActionResult.`
- [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)關鍵字已套用至 web 服務呼叫。
- 已呼叫非同步 web 服務 API （`GetGizmosAsync`）。

在 `GetGizmosAsync` 方法主體內，另一個非同步方法，`GetGizmosAsync` 呼叫。 `GetGizmosAsync` 立即傳回當資料可供使用時，最後會完成的 `Task<List<Gizmo>>`。 因為您不想要在擁有 gizmo 資料之前執行任何其他動作，所以程式碼會等候工作（使用**await**關鍵字）。 您只能在以**async**關鍵字標注的方法中使用**await**關鍵字。

**Await**關鍵字不會封鎖執行緒，直到工作完成為止。 它會將方法的其餘部分註冊為工作上的回呼，並立即傳回。 當等候的工作最後完成時，它會叫用該回呼，並繼續執行方法，並將其停止。 如需使用[await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)和[async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)關鍵字和[工作命名空間](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)的詳細資訊，請參閱[非同步參考](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/async)。

下列程式碼顯示 `GetGizmos` 和 `GetGizmosAsync` 方法。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample5.cs)]

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample6.cs?highlight=1,4-8)]

 非同步變更與上述**GizmosAsync**所做的變更類似。 

- 方法簽章是以[async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)關鍵字標注，傳回型別已變更為 `Task<List<Gizmo>>`，而*async*已附加至方法名稱。
- 會使用非同步[HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx)類別，而不是[WebClient](https://msdn.microsoft.com/library/system.net.webclient.aspx)類別。
- [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)關鍵字已套用至[HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx)非同步方法。

下圖顯示 [非同步 gizmo] 視圖。

![async](using-asynchronous-methods-in-aspnet-mvc-4/_static/image2.png)

Gizmos 資料的瀏覽器呈現方式與同步呼叫所建立的視圖相同。 唯一的差異在於，非同步版本在繁重的負載下可能會更有效率。

## <a id="Parallel"></a>平行執行多個作業

當動作必須執行數個獨立的作業時，非同步動作方法在同步方法上會有相當大的優勢。 在提供的範例中，同步方法 `PWG`（適用于產品、widget 和 Gizmos）會顯示三個 web 服務呼叫的結果，以取得產品、widget 和 Gizmos 的清單。 提供這些服務的[ASP.NET Web API](../../../web-api/index.md)專案會使用 [[延遲](https://msdn.microsoft.com/library/hh139096(VS.110).aspx)] 來模擬延遲或緩慢的網路呼叫。 當延遲時間設定為500毫秒時，非同步 `PWGasync` 方法會花上500毫秒來完成，而同步 `PWG` 版本則需要超過1500毫秒。 同步 `PWG` 方法會顯示在下列程式碼中。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample7.cs)]

非同步 `PWGasync` 方法會顯示在下列程式碼中。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample8.cs?highlight=1,3,12)]

下圖顯示從**PWGasync**方法傳回的視圖。

![pwgAsync](using-asynchronous-methods-in-aspnet-mvc-4/_static/image3.png)

## <a id="CancelToken"></a>使用解除標記

傳回 `Task<ActionResult>`的非同步動作方法是可取消的，而當[AsyncTimeout](https://msdn.microsoft.com/library/system.web.mvc.asynctimeoutattribute(VS.108).aspx)屬性提供一個參數時，則會接受[CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken(VS.110).aspx)參數。 下列程式碼顯示 `GizmosCancelAsync` 方法，其超時時間為150毫秒。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample9.cs?highlight=1-3,5,10)]

下列程式碼顯示 GetGizmosAsync 多載，它採用[CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken(VS.110).aspx)參數。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample10.cs)]

在提供的範例應用程式中，選取 [*取消權杖示範*] 連結會呼叫 `GizmosCancelAsync` 方法，並示範取消非同步呼叫。

## <a id="ServerConfig"></a>高平行存取/高延遲 Web 服務呼叫的伺服器設定

若要實現非同步 web 應用程式的優點，您可能需要對預設伺服器設定進行一些變更。 設定和壓力測試非同步 web 應用程式時，請記住下列事項。

- Windows 7、Windows Vista 及所有 Windows 用戶端作業系統最多可以有10個並行要求。 您需要 Windows Server 作業系統，才能在高負載下查看非同步方法的優點。
- 從提升許可權的命令提示字元，向 IIS 註冊 .NET 4.5：  
  %windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet\_regiis-i  
  請參閱[ASP.NET IIS 註冊工具（Aspnet\_regiis）](https://msdn.microsoft.com/library/k6h9cz8h.aspx)
- 您可能需要將[HTTP.sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture)佇列限制從預設值1000增加至5000。 如果設定太低，您可能會看到 HTTP.sys 拒絕要求，[其 HTTP 為](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture)503 狀態。 若要變更 HTTP.sys 佇列限制：

    - 開啟 [IIS 管理員]，然後流覽至 [應用程式集區] 窗格。
    - 以滑鼠右鍵按一下目標應用程式集區，然後選取 [ **Advanced Settings**]。  
        ![advanced](using-asynchronous-methods-in-aspnet-mvc-4/_static/image4.png)
    - 在 [**高級設定**] 對話方塊中，將 [*佇列長度*] 從1000變更為5000。  
        ![佇列長度](using-asynchronous-methods-in-aspnet-mvc-4/_static/image5.png)  
  
  請注意，在上述影像中，即使應用程式集區使用 .NET 4.5，.NET framework 仍會列為 v4.0。 若要瞭解這項差異，請參閱下列各項：

    - [.NET 版本控制和多目標-.NET 4.5 是就地升級至 .NET 4。0](http://www.hanselman.com/blog/NETVersioningAndMultiTargetingNET45IsAnInplaceUpgradeToNET40.aspx)
    - [如何將 IIS 應用程式或 AppPool 設定為使用 ASP.NET 3.5，而不是2。0](http://www.hanselman.com/blog/HowToSetAnIISApplicationOrAppPoolToUseASPNET35RatherThan20.aspx)
    - [.NET Framework 版本和相依性](https://msdn.microsoft.com/library/bb822049(VS.110).aspx)
- 如果您的應用程式使用 web 服務或 System.NET 透過 HTTP 與後端通訊，您可能需要增加[connectionmanagement 專案/maxconnection](https://msdn.microsoft.com/library/fb6y0fyc(VS.110).aspx)元素。 針對 ASP.NET 應用程式，這會受限於 Cpu 數目12倍的自動設定功能。 這表示在四個處理器上，您最多可以有12個 \* 4 = 48 個對 IP 端點的並行連線。 因為這會系結[至自動](https://msdn.microsoft.com/library/7w2sway1(VS.110).aspx)設定，在 ASP.NET 應用程式中增加 `maxconnection` 最簡單的方式，就是在*global.asax*檔案的 from `Application_Start` 方法中，以程式設計方式設定[ServicePointManager servicepointmanager.defaultconnectionlimit。](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit(VS.110).aspx) 如需範例，請參閱範例下載。
- 在 .NET 4.5 中， [MaxConcurrentRequestsPerCPU](https://blogs.msdn.com/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)的預設值應該是 [5000]。
