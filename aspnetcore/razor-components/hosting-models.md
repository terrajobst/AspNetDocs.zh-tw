---
title: 裝載模型的 razor 元件
author: guardrex
description: 了解用戶端 Blazor 和裝載模型的伺服器端 ASP.NET Core Razor 元件。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/hosting-models
ms.openlocfilehash: d1e0c472d7d10eeb4cef0da735cf703c98dd1645
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042435"
---
# <a name="razor-components-hosting-models"></a>裝載模型的 razor 元件

藉由[Daniel Roth](https://github.com/danroth27)

Razor 元件是設計用來執行用戶端的 web 架構 WebAssembly 為基礎的.NET 執行階段上的瀏覽器中 (*Blazor*) 或 ASP.NET Core 中的伺服器端 (*ASP.NET Core Razor 元件*)。 無論裝載模型、 應用程式和元件模型*維持不變*。 這篇文章會討論可用的裝載模型。

## <a name="client-side-hosting-model"></a>用戶端裝載模型

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

Blazor 的主要裝載模型是在瀏覽器中的執行用戶端。 在此模型中，Blazor 應用程式、 其相依性，以及.NET 執行階段會下載至瀏覽器中。 應用程式會直接在瀏覽器 UI 執行緒上執行。 所有的 UI 更新及事件處理會發生相同的程序中。 應用程式資產可部署為使用任何網頁伺服器慣用的靜態檔案 (請參閱[主機和部署](xref:host-and-deploy/razor-components/index))。

![Blazor 用戶端：Blazor 應用程式會在瀏覽器 UI 執行緒上執行。](hosting-models/_static/client-side.png)

若要建立一個使用的用戶端的裝載模型的 Blazor 應用程式，請使用**Blazor**或 **（ASP.NET Core 裝載） 的 Blazor**專案範本 (`blazor`或`blazorhosted`範本時使用[dotnet 新](/dotnet/core/tools/dotnet-new)命令在命令提示字元)。 包含*blazor.webassembly.js*指令碼處理：

* 下載.NET 執行階段、 應用程式和其相依性。
* 要執行應用程式的執行階段初始化。

用戶端的裝載模型提供幾項優點。 用戶端 Blazor:

* 有任何的.NET 伺服器端相依性。
* 有豐富的互動式 UI。
* 充分利用用戶端資源和功能。
* 卸載工作從伺服器到用戶端。
* 支援離線案例。

有裝載用戶端的缺點。 用戶端 Blazor:

* 將應用程式限制的瀏覽器的功能。
* 需要支援用戶端硬體和軟體 （例如 WebAssembly 支援）。
* 具有較大的下載大小和較長載入時間的應用程式。
* 具有較少成熟的.NET 執行階段和工具支援 （例如，.NET Standard 的支援和偵錯的限制）。

Visual Studio 包含**Blazor (裝載 ASP.NET Core)** 建立 Blazor 應用程式執行 WebAssembly，而且裝載 ASP.NET Core 伺服器上的專案範本。 ASP.NET Core 應用程式提供給用戶端 Blazor 應用程式，但因不同的處理序。 用戶端 Blazor 應用程式可以透過使用 Web API 呼叫或 SignalR 連線的網路來與伺服器互動。

> [!IMPORTANT]
> 如果用戶端 Blazor 應用程式由裝載為 IIS 子應用程式的 ASP.NET Core 應用程式，停用繼承的 ASP.NET Core 模組處理常式。 Blazor 應用程式中設定的應用程式的基底路徑*index.html*檔案，以在 IIS 中設定子應用程式時使用的 IIS 別名。
>
> 如需詳細資訊，請參閱 <<c0> [ 應用程式基底路徑](xref:host-and-deploy/razor-components/index#app-base-path)。

## <a name="server-side-hosting-model"></a>伺服器端裝載模型

在 ASP.NET Core Razor 元件伺服器端裝載模型中，從 ASP.NET Core 應用程式中的伺服器上執行應用程式。 UI 更新、事件處理及 JavaScript 呼叫會透過 SignalR 連線處理。

![ASP.NET Core Razor 元件伺服器端：瀏覽器互動 （裝載 ASP.NET Core 應用程式內） 的應用程式伺服器上透過 SignalR 的連線。](hosting-models/_static/server-side.png)

若要建立一個使用的伺服器端的主控模型的 Razor 元件應用程式，請使用**Blazor （伺服器端 ASP.NET Core 中）** 範本 (`blazorserver`使用時[dotnet 新](/dotnet/core/tools/dotnet-new)在命令提示字元)。 將 ASP.NET Core 應用程式裝載 Razor 元件伺服器端應用程式，並設定 SignalR 端點的用戶端連線的位置。 ASP.NET Core 應用程式參考應用程式的`Startup`来加入類別：

* 伺服器端 Razor 元件服務。
* 應用程式，以在要求處理管線。

[!code-csharp[](hosting-models/samples_snapshot/Startup.cs?highlight=5,27)]

*Blazor.server.js*指令碼&dagger;會建立用戶端連線。 它是保存和還原應用程式狀態為 必要 （例如，如果遺失的網路連線） 的應用程式的責任。

伺服器端的主控模型會提供數個優點：

* 可讓您撰寫您的整個應用程式使用.NET 和C#使用的元件模型。
* 提供豐富的互動式風格，並避免不必要的頁面重新整理。
* 具有大幅縮小應用程式大小比用戶端 Blazor 應用程式，且速度更快載入。
* 元件的邏輯可以充分利用 server 功能，包括使用任何.NET Core 相容的 Api。
* 在.NET Core 上的伺服器上執行，讓現有的.NET 工具，例如偵錯時，如預期運作。
* 使用精簡型用戶端 （例如，不支援 WebAssembly 和資源的瀏覽器受限的裝置）。

有伺服器端裝載的缺點：

* 具有較高的延遲：每個使用者互動牽涉到的網路躍點。
* 提供任何離線的支援：如果用戶端連線失敗，應用程式會停止運作。
* 降低延展性：伺服器必須管理多個用戶端連線，並處理用戶端狀態。
* 需要 ASP.NET Core 伺服器以提供應用程式。 不使用伺服器 （例如，從 CDN) 的部署不可行。

&dagger;*Blazor.server.js*指令碼發行至下列路徑： *bin / {偵錯 |發行} / {目標 FRAMEWORK} /publish/ {應用程式名稱}。應用程式/dist/架構 （_f)*。
