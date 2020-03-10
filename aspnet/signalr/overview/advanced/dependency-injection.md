---
uid: signalr/overview/advanced/dependency-injection
title: SignalR 中的相依性插入 |Microsoft Docs
author: bradygaster
description: 本主題中使用的軟體版本 Visual Studio 2013 .NET 4.5 SignalR 第2版本主題的先前版本，以取得舊版的相關資訊 。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: a14121ae-02cf-4024-8af0-9dd0dc810690
msc.legacyurl: /signalr/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 52978b10b6c131ac8eff4535216cc60b43fdf3de
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78537328"
---
# <a name="dependency-injection-in-signalr"></a>SignalR 中的相依性插入

由[Mike Wasson](https://github.com/MikeWasson)， [Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a>本主題中使用的軟體版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR 第2版
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>本主題的先前版本
>
> 如需舊版 SignalR 的詳細資訊，請參閱[SignalR 較舊的版本](../older-versions/index.md)。
>
> ## <a name="questions-and-comments"></a>問題與意見
>
> 請留下有關您喜歡本教學課程的意見反應，以及我們可以在頁面底部的批註中改進的內容。 如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。

相依性插入是一種方法，可移除物件之間的硬式編碼相依性，讓您更輕鬆地取代物件的相依性，以進行測試（使用模擬物件）或變更執行時間行為。 本教學課程說明如何在 SignalR hub 上執行相依性插入。 它也會示範如何搭配 SignalR 使用 IoC 容器。 IoC 容器是用於相依性插入的一般架構。

## <a name="what-is-dependency-injection"></a>什麼是相依性插入？

如果您已經熟悉相依性插入，請略過本節。

相依性*插入*（DI）是一種模式，物件不負責建立自己的相依性。 以下是激勵 DI 的簡單範例。 假設您有一個需要記錄訊息的物件。 您可能會定義記錄介面：

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

在您的物件中，您可以建立 `ILogger` 來記錄訊息：

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

這是可行的，但不是最佳的設計。 如果您想要將 `FileLogger` 取代為另一個 `ILogger` 執行，則必須修改 `SomeComponent`。 假設有很多其他物件使用 `FileLogger`，您必須加以變更。 或者，如果您決定讓 `FileLogger` 單一，您也必須在整個應用程式中進行變更。

較好的方法是將 `ILogger` 「插入」物件，例如，藉由使用「方法」引數：

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

現在，物件不負責選取要使用的 `ILogger`。 您可以切換 `ILogger` 的執行，而不需要變更相依于它的物件。

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

此模式稱為「[函數化插入](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)」。 另一個模式是 setter 插入，您可以在其中透過 setter 方法或屬性來設定相依性。

## <a name="simple-dependency-injection-in-signalr"></a>SignalR 中的簡單相依性插入

請考慮[使用 SignalR](../getting-started/tutorial-getting-started-with-signalr.md)的教學課程消費者入門的聊天應用程式。 以下是來自該應用程式的中樞類別：

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

假設您想要將聊天訊息儲存在伺服器上，然後再傳送它們。 您可以定義可抽象化此功能的介面，並使用 DI 將介面插入 `ChatHub` 類別。

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

唯一的問題是，SignalR 應用程式不會直接建立中樞;SignalR 會為您建立這些專案。 根據預設，SignalR 會預期中樞類別具有無參數的函式。 不過，您可以輕鬆地註冊函式來建立中樞實例，並使用此函數來執行 DI。 藉由呼叫**GlobalHost. DependencyResolver**註冊函式。

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

現在，每當 SignalR 需要建立 `ChatHub` 實例時，就會叫用這個匿名函數。

## <a name="ioc-containers"></a>IoC 容器

先前的程式碼適用于簡單的案例。 但是您仍然必須撰寫下列內容：

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

在具有許多相依性的複雜應用程式中，您可能需要撰寫許多此「接線」程式碼。 這個程式碼可能很難維護，特別是當相依性已嵌套時。 這也很難進行單元測試。

其中一個解決方案是使用 IoC 容器。 IoC 容器是負責管理相依性的軟體元件。您會向容器註冊類型，然後使用容器來建立物件。 容器會自動將相依性關聯到圖形。 許多 IoC 容器也可讓您控制物件存留期和範圍之類的專案。

> [!NOTE]
> 「IoC」代表「反轉控制」，這是架構呼叫應用程式程式碼的一般模式。 IoC 容器會為您構造物件，這會「反轉」一般控制流程。

## <a name="using-ioc-containers-in-signalr"></a>在 SignalR 中使用 IoC 容器

聊天應用程式可能太容易受益于 IoC 容器。 相反地，讓我們來看一下[StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample)範例。

StockTicker 範例會定義兩個主要類別：

- `StockTickerHub`：中樞類別，它會管理用戶端連接。
- `StockTicker`：保存股票價格並定期更新它們的單一專案。

`StockTickerHub` 會保存 `StockTicker` singleton 的參考，而 `StockTicker` 則會保存 `StockTickerHub`的**IHubConnectionCoNtext**參考。 它會使用此介面與 `StockTickerHub` 實例進行通訊。 （如需詳細資訊，請參閱[使用 ASP.NET SignalR 進行伺服器廣播](../getting-started/tutorial-server-broadcast-with-signalr.md)。）

我們可以使用 IoC 容器來全集這些相依性。 首先，讓我們來簡化 `StockTickerHub` 和 `StockTicker` 類別。 在下列程式碼中，我已將不需要的元件加上批註。

從 `StockTickerHub`中移除無參數的函式。 相反地，我們一律會使用 DI 來建立中樞。

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

針對 StockTicker，移除單一實例。 稍後，我們將使用 IoC 容器來控制 StockTicker 存留期。 此外，請將此函式設為公用。

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

接下來，我們可以藉由建立 `StockTicker`的介面來重構程式碼。 我們將使用這個介面，將 `StockTickerHub` 與 `StockTicker` 類別分離。

Visual Studio 使這種重構變得簡單。 開啟檔案 StockTicker.cs，以滑鼠右鍵按一下 `StockTicker` 類別宣告，然後選取 [**重構**...]**解壓縮介面**。

![](dependency-injection/_static/image1.png)

在 [**解壓縮介面**] 對話方塊中，按一下 [**全選**]。 其他部分保留預設值。 按一下 [確定]。

![](dependency-injection/_static/image2.png)

Visual Studio 會建立名為 `IStockTicker`的新介面，而且也會變更 `StockTicker` 衍生自 `IStockTicker`。

開啟檔案 IStockTicker.cs，並將介面變更為 [**公用**]。

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

在 `StockTickerHub` 類別中，將 `StockTicker` 的兩個實例變更為 `IStockTicker`：

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

建立 `IStockTicker` 介面並不是絕對必要，但我想要示範 DI 如何協助減少應用程式中元件之間的耦合。

## <a name="add-the-ninject-library"></a>新增 Ninject 程式庫

有許多適用于 .NET 的開放原始碼 IoC 容器。 在本教學課程中，我將使用[Ninject](http://www.ninject.org/)。 （其他熱門程式庫包括[Castle Windsor](http://www.castleproject.org/)、 [Spring.Net](http://www.springframework.net/)、 [Autofac](https://code.google.com/p/autofac/)、 [Unity](https://github.com/unitycontainer/unity)和[StructureMap](http://docs.structuremap.net)）。

使用 NuGet 套件管理員來安裝[Ninject 程式庫](https://nuget.org/packages/Ninject/3.0.1.10)。 在 Visual Studio 中，從 [**工具**] 功能表選取 [ **NuGet 套件管理員**] > [**套件管理員主控台**]。 在 [Package Manager Console] 視窗中，輸入下列命令：

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a>取代 SignalR 相依性解析程式

若要在 SignalR 內使用 Ninject，請建立衍生自**DefaultDependencyResolver**的類別。

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

這個類別會覆寫**DefaultDependencyResolver**的**GetService**和**GetServices**方法。 SignalR 會呼叫這些方法，在執行時間建立各種物件，包括中樞實例，以及 SignalR 在內部使用的各種服務。

- **GetService**方法會建立類型的單一實例。 覆寫此方法以呼叫 Ninject 核心的**TryGet**方法。 如果該方法傳回 null，則會切換回預設解析程式。
- **GetServices**方法會建立指定之型別的物件集合。 覆寫此方法，以將來自 Ninject 的結果與預設解析程式的結果串連。

## <a name="configure-ninject-bindings"></a>設定 Ninject 系結

現在，我們將使用 Ninject 來宣告型別系結。

開啟您應用程式的 Startup.cs 類別（您可以根據 `readme.txt`中的套件指示手動建立，或是將驗證新增至您的專案而建立）。 在 `Startup.Configuration` 方法中，建立 Ninject 呼叫*核心*的 Ninject 容器。

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

建立自訂相依性解析程式的實例：

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

建立 `IStockTicker` 的系結，如下所示：

[!code-csharp[Main](dependency-injection/samples/sample17.cs)]

這段程式碼會說兩件事。 首先，每當應用程式需要 `IStockTicker`時，核心就應該建立 `StockTicker`的實例。 第二，`StockTicker` 類別應該是建立成單一物件的。 Ninject 會建立一個物件的實例，並針對每個要求傳回相同的實例。

建立**IHubConnectionCoNtext**的系結，如下所示：

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

此程式碼會建立一個會傳回**IHubConnection**的匿名函式。 只有在建立 `IStockTicker` 實例時， **WhenInjectedInto**方法才會告訴 Ninject 使用此函數。 原因是，SignalR 會在內部建立**IHubConnectionCoNtext**實例，而我們不想要覆寫 SignalR 建立它們的方式。 此函式僅適用于我們的 `StockTicker` 類別。

藉由新增中樞設定，將相依性解析程式傳遞至**MapSignalR**方法：

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

使用新的參數更新範例啟動類別中的 ConfigureSignalR 方法：

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

現在 SignalR 會使用**MapSignalR**中指定的解析程式，而不是預設的解析程式。

以下是 `Startup.Configuration`的完整程式代碼清單。

[!code-csharp[Main](dependency-injection/samples/sample21.cs)]

若要在 Visual Studio 中執行 StockTicker 應用程式，請按 F5。 在瀏覽器視窗中，流覽至 [`http://localhost:*port*/SignalR.Sample/StockTicker.html`]。

![](dependency-injection/_static/image3.png)

應用程式與之前的功能完全相同。 （如需說明，請參閱[使用 ASP.NET SignalR 的伺服器廣播](../getting-started/tutorial-server-broadcast-with-signalr.md)。）我們尚未變更此行為;只是讓程式碼更容易測試、維護和發展。
