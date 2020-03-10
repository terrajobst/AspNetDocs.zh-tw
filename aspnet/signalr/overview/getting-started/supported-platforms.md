---
uid: signalr/overview/getting-started/supported-platforms
title: 支援的平臺 |Microsoft Docs
author: bradygaster
description: 本文說明 SignalR 支援哪些用戶端和伺服器。
ms.author: bradyg
ms.date: 04/18/2018
ms.assetid: eac31beb-0f46-4afa-9def-e80904dea4f0
msc.legacyurl: /signalr/overview/getting-started/supported-platforms
msc.type: authoredcontent
ms.openlocfilehash: 89730e591bb94022d16fe1a78a4350b38e0bf7a4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558629"
---
# <a name="supported-platforms"></a>支援的平台

由[派翠克 Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文說明 SignalR 支援哪些用戶端和伺服器。 
> 
> ## <a name="questions-and-comments"></a>問題與意見
> 
> 請留下有關您喜歡本教學課程的意見反應，以及我們可以在頁面底部的批註中改進的內容。 如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。

在各種伺服器和用戶端設定下支援 SignalR。 此外，每個傳輸選項都有自己的一組需求;如果傳輸的系統需求無法使用，SignalR 會正常地容錯移轉到其他傳輸。 如需 SignalR 支援之傳輸的詳細資訊，請參閱[傳輸和回退](introduction-to-signalr.md#transports)。

## <a name="server-system-requirements"></a>伺服器系統需求

SignalR 伺服器元件可以裝載在各種不同的伺服器設定上。 本節說明支援的作業系統版本、.NET framework、網際網路資訊伺服器和其他元件。

### <a name="supported-server-operating-systems"></a>支援的伺服器作業系統

SignalR 伺服器元件可以裝載于下列伺服器或用戶端作業系統中。 請注意，若要讓 SignalR 使用 Websocket，必須要有 Windows Server 2012、Windows Server 2016 或 Windows 8 （WebSocket 可用於 Windows Azure 網站，只要網站的 .NET framework 版本設定為4.5，而且網站的[設定] 頁面）。

- Windows Server 2016
- Windows Server 2012
- Windows Server 2008 r2
- Windows 10
- Windows 8
- Windows 7
- Microsoft Azure

### <a name="supported-server-net-framework-version"></a>支援的伺服器 .NET Framework 版本

只有 .NET Framework 4.5 才支援 SignalR 2。 如需增強可靠性、相容性、穩定性和效能的更新，請參閱[建議的更新](#updates)一節。

### <a name="supported-server-iis-versions"></a>支援的伺服器 IIS 版本

當 SignalR 裝載于 IIS 時，會支援下列版本。 請注意，如果使用的是用戶端作業系統，例如用於開發（Windows 8 或 Windows 7），則不應使用完整版的 IIS 或 Cassini，因為將會有10個同時連接的限制，這會因為連線而很快到達是暫時性的，經常重新建立，而且不會在不再使用時立即處置。 IIS Express 應在用戶端作業系統上使用。

另請注意，若要讓 SignalR 使用 WebSocket，必須使用 IIS 8 或 IIS 8 Express，伺服器必須使用 Windows 8、Windows Server 2012 或更新版本，而且必須在 IIS 中啟用 WebSocket。 如需如何在 IIS 中啟用 WebSocket 的詳細資訊，請參閱[iis 8.0 WebSocket 通訊協定支援](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support)。

- IIS 8 或 IIS 8 Express。
- IIS 7 和7.5。 需要[無副檔名 url](https://support.microsoft.com/kb/980368)的支援。
- IIS 必須在整合模式中執行;不支援傳統模式。 如果 IIS 是使用伺服器傳送的事件傳輸，在傳統模式中執行，可能會有最多30秒的訊息延遲。
- 裝載應用程式必須在完全信任模式下執行。

## <a name="client-system-requirements"></a>用戶端系統需求

SignalR 可用於各種不同的用戶端平臺。 本節說明在網頁瀏覽器、Windows 桌面應用程式、Silverlight 應用程式和行動裝置上使用 SignalR 的系統需求。

### <a name="web-browsers"></a>網頁瀏覽器

SignalR 可用於各種 web 瀏覽器，但通常僅支援最新的兩個版本。

在瀏覽器中使用 SignalR 的應用程式必須使用 jQuery 版本1.6.4 或主要的較新版本（例如1.7.2、1.8.2 或1.9.1）。

SignalR 可用於下列瀏覽器：

- Microsoft Internet Explorer 8、9、10和11版。 支援新式、桌面和行動裝置版。
- Mozilla Firefox：目前的版本-1，Windows 和 Mac 版本。
- Google Chrome：目前版本-1，Windows 和 Mac 版本。
- Safari：目前的版本1，Mac 和 iOS 版本。
- Opera：目前的版本-1，僅限 Windows。
- Android 瀏覽器

除了需要特定的瀏覽器之外，SignalR 所使用的各種傳輸都有自己的需求。 下列設定支援下列傳輸：

<a id="browser"></a>

**網頁瀏覽器傳輸需求**

| Transport | Internet Explorer | Chrome （Windows 或 iOS） | Firefox | Safari （OSX 或 iOS） | Android |
| --- | --- | --- | --- | --- | --- |
| WebSockets | 10 + | 目前-1 | 目前-1 | 目前-1 | N/A |
| 伺服器傳送的事件 | N/A | 目前-1 | 目前-1 | 目前-1 | N/A |
| ForeverFrame | 8+ | N/A | N/A | N/A | 4.1 |
| 長時間輪詢 | 8+ | 目前-1 | 目前-1 | 目前-1 | 4.1 |

\*： 6 + 完整功能的必要項。

#### <a name="unsupported-browsers"></a>不支援的瀏覽器

雖然在舊版瀏覽器中*可能會*執行 SignalR，而不會有重大問題，但我們並不會主動測試 SignalR，而且通常不會修正可能出現在其中的 bug。

### <a name="windows-desktop-and-silverlight-applications"></a>Windows 桌面和 Silverlight 應用程式

除了在網頁瀏覽器中執行之外，SignalR 也可以裝載于獨立的 Windows 用戶端或 Silverlight 應用程式中。 Windows 桌面和 Silverlight SignalR 應用程式有下列系統需求。

- Windows XP SP3 或更新版本支援使用 .NET 4 的應用程式。
- Windows Vista 或更新版本支援使用 .NET Framework 4.5 的應用程式。

除了作業系統和 .NET framework 需求，可供 SignalR 使用的傳輸也具有自己的需求。 下列設定支援下列傳輸：

**Windows 桌面和 Silverlight 傳輸需求**

| Transport | .NET 應用程式 | Silverlight |
| --- | --- | --- |
| Web 通訊端 | Windows 8 + 和 .NET 4.5 + | N/A |
| 永久框架 | N/A | N/A |
| 伺服器傳送的事件 | .NET 4 + | 5 + |
| 長時間輪詢 | .NET 4 + | 5 + |

<a id="android"></a>

### <a name="windows-store-and-windows-phone-applications"></a>Windows 儲存和 Windows Phone 應用程式

SignalR 可用於 Windows Store 應用程式和 Windows Phone 8 應用程式。 下列設定支援下列傳輸：

**Windows 儲存和 Windows Phone 傳輸需求**

| Transport | Windows Store/.NET | Windows Store/JavaScript | Windows Phone/IE | Windows Phone/.NET |
| --- | --- | --- | --- | --- |
| WebSockets | N/A | Win8 + | 8+ | N/A |
| 永久框架 | N/A | Win8 + | 7.5+ | N/A |
| 伺服器傳送的事件 | Win8 + | N/A | N/A | 8+ |
| 長時間輪詢 | Win8 + | Win8 + | 7.5+ | 8+ |

<a id="updates"></a>

## <a name="recommended-updates"></a>建議的更新

以下是針對 SignalR 伺服器建議的更新：

- 您可以在[這裡](https://support.microsoft.com/kb/2750149)取得 .NET Framework 4.5 的更新。
- Microsoft 會定期發行 Qfe 以進行 ASP.NET。 這些應該套用為 [可用]。
