---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Katana 範例 |Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 1238f7d09492a6856d49dece5de75184ccfa4838
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584557"
---
# <a name="katana-samples"></a>Katana 範例

由[Microsoft](https://github.com/microsoft)

## <a name="katana-samples"></a>Katana 範例

**ASP.NET 路由範例** | [原始碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)  
在某些應用程式中，您會想要將 Asp.Net 路由表中的 OWIN 元件與非 OWIN 元件並存。 這個範例示範如何使用 MapOwinPath 和 MapOwinRoute 所提供的 RouteCollection 擴充方法。

**分支管線範例** | [原始碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)  
OWIN 要求處理管線不需要是線性的，它們可以透過不同的方式分支以處理要求。 這個範例示範如何根據要求路徑或其他要求資料（例如標頭）來建立分支管線。 這些元件可在 Owin nuget 套件中取得。

**自訂伺服器範例** | [原始碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer)   
顯示如何在自我裝載 OWIN 時使用自訂 OWIN 伺服器。

**內嵌範例** | [原始程式碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)  
有些 OWIN 伺服器可在您自己的進程中執行（&quot;自我裝載&quot;）。 這個範例示範如何使用 Owin 所提供的工具來啟動 OWIN 應用程式。

**HelloWorld 範例** | [原始碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)  
OWIN 是一種 HTTP 伺服器 API 抽象概念，可讓您跨各種伺服器進行應用程式可攜性。 這個範例會示範如何使用一些**簡單的包裝**函式來撰寫 Hello World 的應用程式，並在原始的 OWIN 抽象概念上執行，並在類似 ASP.NET 的 web 伺服器上執行。

**Hello World 原始 OWIN 範例** | [原始程式碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)  
這個範例會示範如何使用**原始**OWIN 抽象來撰寫 Hello World 應用程式，並在類似 Asp.Net 的 web 伺服器上執行。

**SignalR 範例** | [原始碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)  
說明如何使用 OWIN/Katana 自我裝載 SignalR。 如需自我裝載 SignalR 的詳細資訊，請參閱[教學課程： SignalR 自我裝載](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。

**靜態檔案範例** | [原始碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample)   
示範如何使用 OWIN/Katana 支援靜態檔案的 HTTP 要求。

**WEB API** | [原始碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi)   
這個範例示範如何在 IIS 中裝載 OWIN，以及如何將 Web API 新增至 OWIN 管線。

 | [原始程式碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample)的**Web 通訊端範例**   
示範如何使用[系統的 .net](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) websocket 類別，在 OWIN 中支援 Web 通訊端。
