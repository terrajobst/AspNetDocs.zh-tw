---
uid: signalr/overview/deployment/using-signalr-with-azure-web-sites
title: 在 Azure App Service 中使用具有 Web Apps 的 SignalR |Microsoft Docs
author: bradygaster
description: 本檔說明如何設定在 Microsoft Azure 上執行的 SignalR 應用程式。 教學課程中所使用的軟體版本 Visual Studio 2013 或 Vis 。
ms.author: bradyg
ms.date: 07/01/2015
ms.assetid: 2a7517a0-b88c-4162-ade3-9bf6ca7062fd
msc.legacyurl: /signalr/overview/deployment/using-signalr-with-azure-web-sites
msc.type: authoredcontent
ms.openlocfilehash: 0e6a18bdbe9cc47e89b5a458753845afb53595f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558699"
---
# <a name="using-signalr-with-web-apps-in-azure-app-service"></a>在 Azure App Service 中搭配 Web 應用程式使用 SignalR

由[派翠克 Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本檔說明如何設定在 Microsoft Azure 上執行的 SignalR 應用程式。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)或 Visual Studio 2012
> - .NET 4.5
> - SignalR 第2版
> - 適用于 Visual Studio 2013 或2012的 Azure SDK 2。3
>
>
>
> ## <a name="questions-and-comments"></a>問題與意見
>
> 請留下有關您喜歡本教學課程的意見反應，以及我們可以在頁面底部的批註中改進的內容。 如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)、 [StackOverflow.com](http://stackoverflow.com/)或[Microsoft Azure 論壇](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform)。

## <a name="table-of-contents"></a>目錄

- [簡介](#introduction)
- [將 SignalR Web 應用程式部署至 Azure App Service](#deploying)
- [在 Azure App Service 上啟用 Websocket](#websocket)
- [使用 Azure Redis 快取背板](#backplane)
- [後續步驟](#nextsteps)

<a id="introduction"></a>
## <a name="introduction"></a>簡介

ASP.NET SignalR 可用來在伺服器與 web 或 .NET 用戶端之間帶入新的互動層級。 在 Azure 中託管時，SignalR 應用程式可以利用在雲端中執行的高可用性、可擴充且高效能的環境。

<a id="deploying"></a>
## <a name="deploying-a-signalr-web-app-to-azure-app-service"></a>將 SignalR Web 應用程式部署至 Azure App Service

SignalR 不會新增任何特定的複雜性，將應用程式部署至 Azure，而不是部署到內部部署伺服器。 使用 SignalR 的應用程式可以裝載于 Azure 中，而不需要變更設定或其他設定（不過，針對 Websocket 支援，請參閱下列[Azure App Service 上的啟用 websocket](#websocket) ）。在本教學課程中，您會將[消費者入門教學](../getting-started/tutorial-getting-started-with-signalr.md)課程中建立的應用程式部署至 Azure。

**必要條件**

- Visual Studio 2013。 如果您沒有 Visual Studio，則 Azure SDK 的安裝中會包含適用于 Web 的 Visual Studio 2013 Express。
- 適用于 Visual Studio 2012 的[AZURE sdk 2.3 for Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409)或[azure sdk 2.3](https://go.microsoft.com/fwlink/p/?linkid=323511)。
- 若要完成此教學課程，您需要 Azure 訂用帳戶。 您可以[啟用 MSDN 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)，或[註冊試用版訂用](https://azure.microsoft.com/pricing/free-trial/)帳戶。

### <a name="deploying-a-signalr-web-app-to-azure"></a>將 SignalR web 應用程式部署至 Azure

1. 完成[消費者入門教學](../getting-started/tutorial-getting-started-with-signalr.md)課程，或從程式[代碼庫](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)下載已完成的專案。
2. 在 Visual Studio 中，選取 [**組建**]、[**發佈 SignalR 交談**]。
3. 在 [發行 Web] 對話方塊中，選取 [Windows Azure 網站]。

    ![選取 Azure 網站](using-signalr-with-azure-web-sites/_static/image1.png)
4. 如果您尚未登入您的 Microsoft 帳戶，請按一下 [選取現有的網站] 對話方塊中的 [登**入**]，然後登入。

    ![選取現有的網站](using-signalr-with-azure-web-sites/_static/image2.png)    ![登入 Azure](using-signalr-with-azure-web-sites/_static/image3.png)
5. 在 [選取現有的網站] 對話方塊中，按一下 [**新增**]。

    ![新網站](using-signalr-with-azure-web-sites/_static/image4.png)
6. 在 [在 Windows Azure 上建立網站] 對話方塊中，輸入唯一的應用程式名稱。 在 [區域] 下拉式清單中選取最接近您的區域。 按一下 [建立]。

    ![Create site on Azure](using-signalr-with-azure-web-sites/_static/image5.png)
7. 在 [發行 Web] 對話方塊中，按一下 [**發佈**]。

    ![發行網站](using-signalr-with-azure-web-sites/_static/image6.png)
8. 當應用程式完成發佈時，Azure App Service Web Apps 中裝載的 SignalR Chat 應用程式將會在瀏覽器中開啟。

    ![在瀏覽器中開啟網站](using-signalr-with-azure-web-sites/_static/image7.png)

<a id="websocket"></a>
### <a name="enabling-websockets-on-azure-app-service-web-apps"></a>在 Azure App Service Web Apps 上啟用 Websocket

您必須在 web 應用程式中明確啟用 Websocket，才能在 SignalR 應用程式中使用。否則，將會使用其他通訊協定（如需詳細資訊，請參閱[傳輸和回退](../getting-started/introduction-to-signalr.md#transports)）。

若要在 Azure App Service Web Apps 上使用 Websocket，請在 Web 應用程式的 [設定] 區段中加以啟用。 若要這麼做，請在[Azure 管理入口網站](https://manage.windowsazure.com/)中開啟您的 web 應用程式，然後選取 [設定]。

![Configure (設定) 索引標籤](using-signalr-with-azure-web-sites/_static/image8.png)

在 [設定] 頁面頂端，確定您的 web 應用程式已使用 .NET 4.5。

![.NET framework 4.5 版設定](using-signalr-with-azure-web-sites/_static/image9.png)

在 [設定] 頁面的 [ **websocket** ] 設定中，選取 [**開啟**]。

![Websocket 設定：開啟](using-signalr-with-azure-web-sites/_static/image10.png)

在 [設定] 頁面的底部，選取 [**儲存**] 以儲存變更。

![儲存設定](using-signalr-with-azure-web-sites/_static/image11.png)

<a id="backplane"></a>
## <a name="using-the-azure-redis-cache-backplane"></a>使用 Azure Redis 快取背板

如果您的 web 應用程式使用多個實例，而且這些實例的使用者需要彼此互動（例如，在某個實例中建立的交談訊息可以連接到連線到其他實例的使用者），就必須在您的應用程式中實作為[Azure Redis 快取背板](../performance/scaleout-with-redis.md)。

<a id="nextsteps"></a>
## <a name="next-steps"></a>後續步驟

如需 Azure App Service 中 Web Apps 的詳細資訊，請參閱[Web Apps 總覽](https://azure.microsoft.com/documentation/articles/app-service-web-overview/)。
