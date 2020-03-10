---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: 使用 OWIN 自我裝載 ASP.NET Web API-ASP.NET 4。x
author: rick-anderson
description: 示範如何在主控台應用程式中裝載 ASP.NET Web API 的程式碼教學課程。
ms.author: riande
ms.date: 07/09/2013
ms.custom: seoapril2019
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: 872b931391a63ef82b96e5b264c070c0b5e9605d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556536"
---
# <a name="use-owin-to-self-host-aspnet-web-api"></a>使用 OWIN 自我裝載 ASP.NET Web API 

> 本教學課程示範如何使用 OWIN，在主控台應用程式中裝載 ASP.NET Web API，以自我裝載 Web API 架構。
>
> [Open Web Interface for .net](http://owin.org) （OWIN）會定義 .net Web 服務器和 Web 應用程式之間的抽象概念。 OWIN 會將 web 應用程式與伺服器分離，讓 OWIN 非常適合在 IIS 以外的進程中自我裝載 web 應用程式。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) 
> - Web API 5.2。7

> [!NOTE]
> 您可以在[github.com/aspnet/samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample)找到本教學課程的完整原始程式碼。

## <a name="create-a-console-application"></a>建立主控台應用程式

**在 [檔案**] 功能表上，按一下 [**新增**]，然後選取 [**專案**]。 從 [**已安裝**] 的 [**視覺C#效果**] 底下選取 [ **Windows 桌面**]，然後選取 **[主控台應用程式（.net Framework）** ] 將專案命名為 "OwinSelfhostSample"，然後選取 **[確定]** 。

[![](use-owin-to-self-host-web-api/_static/image7.png)](use-owin-to-self-host-web-api/_static/image7.png)

## <a name="add-the-web-api-and-owin-packages"></a>新增 Web API 和 OWIN 套件

從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。 在 [Package Manager Console] 視窗中，輸入下列命令：

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

這會安裝 WebAPI OWIN selfhost 套件和所有必要的 OWIN 套件。

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a>設定適用于自我裝載的 Web API

在方案總管中，以滑鼠右鍵按一下專案，然後選取 [**新增** / **類別**] 以加入新的類別。 將類別命名為 `Startup`。

![](use-owin-to-self-host-web-api/_static/image5.png)

以下列內容取代此檔案中的所有重複使用的程式碼：

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a>新增 Web API 控制器

接下來，新增 Web API 控制器類別。 在方案總管中，以滑鼠右鍵按一下專案，然後選取 [**新增** / **類別**] 以加入新的類別。 將類別命名為 `ValuesController`。

以下列內容取代此檔案中的所有重複使用的程式碼：

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-with-httpclient"></a>啟動 OWIN 主機，並使用 HttpClient 提出要求

以下列內容取代 Program.cs 檔案中的所有重複使用的程式碼：

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="run-the-application"></a>執行應用程式

若要執行應用程式，請在 Visual Studio 中按 F5。 輸出看起來應該如下所示：

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a>其他資源

[Katana 專案概觀](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[Azure 背景工作角色中的主機 ASP.NET Web API](host-aspnet-web-api-in-an-azure-worker-role.md)
