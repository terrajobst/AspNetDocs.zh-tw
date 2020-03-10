---
uid: aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
title: 使用 OWIN 和 Katana 的消費者入門 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 09/27/2013
ms.assetid: 6dae249f-5ac6-4f6e-bc49-13bcd5a54a70
msc.legacyurl: /aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
msc.type: authoredcontent
ms.openlocfilehash: 4dfd7b8ebb2bb48d7ef800fd522b79a7b4a045c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584669"
---
# <a name="getting-started-with-owin-and-katana"></a>開始使用 OWIN 與 Katana

由[Mike Wasson](https://github.com/MikeWasson)

[Open Web Interface for .net （OWIN）](http://owin.org/)會定義 .net Web 服務器和 Web 應用程式之間的抽象概念。 藉由將網頁伺服器與應用程式分離，OWIN 可讓您更輕鬆地建立中介軟體以進行 .NET web 程式開發。 此外，OWIN 可讓您更輕鬆地將 web 應用程式&#8212;移植到其他主機，例如，在 Windows 服務或其他進程中自我裝載。

OWIN 是一種由社區所擁有的規格，而不是實作為。 Katana project 是一組由 Microsoft 開發的開放原始碼 OWIN 元件。 如需 OWIN 和 Katana 的一般總覽，請參閱[專案 Katana 的總覽](an-overview-of-project-katana.md)。 在本文中，我將直接前往程式碼以開始著手。

本教學課程使用[Visual Studio 2013 候選版](https://go.microsoft.com/fwlink/?LinkId=306566)，但您也可以使用 Visual Studio 2012。 Visual Studio 2012 中有幾個步驟不同，我在下面說明。

## <a name="host-owin-in-iis"></a>IIS 中的主機 OWIN

在本節中，我們會在 IIS 中裝載 OWIN。 此選項可讓您彈性地複合性 OWIN 管線和 IIS 的成熟功能集。 使用此選項時，OWIN 應用程式會在 ASP.NET 要求管線中執行。

首先，建立新的 ASP.NET Web 應用程式專案。 （在 Visual Studio 2012 中，使用 ASP.NET 空白 Web 應用程式專案類型）。

![](getting-started-with-owin-and-katana/_static/image1.png)

在 [**新增 ASP.NET 專案**] 對話方塊中，選取 [**空白**] 範本。

![](getting-started-with-owin-and-katana/_static/image2.png)

### <a name="add-nuget-packages"></a>新增 NuGet 套件

接下來，新增所需的 NuGet 套件。 從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。 在 [套件管理員主控台] 視窗中，輸入下列命令：

`install-package Microsoft.Owin.Host.SystemWeb –Pre`

![](getting-started-with-owin-and-katana/_static/image3.png)

### <a name="add-a-startup-class"></a>新增啟動類別

接下來，新增 OWIN startup 類別。 在方案總管中，以滑鼠右鍵按一下專案並選取 [**加入**]，然後選取 [**新增專案**]。 在 [**加入新專案**] 對話方塊中，選取 [ **Owin 啟始類別**]。 如需設定 startup 類別的詳細資訊，請參閱[OWIN 啟動類別偵測](owin-startup-class-detection.md)。

![](getting-started-with-owin-and-katana/_static/image4.png)

將下列程式碼加入 `Startup1.Configuration` 方法：

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample1.cs?highlight=3)]

這段程式碼會將簡單的中介軟體新增至 OWIN 管線，並實作為接收**IOwinCoNtext**實例的函式。 當伺服器收到 HTTP 要求時，OWIN 管線會叫用中介軟體。 中介軟體會設定回應的內容類型，並寫入回應主體。

> [!NOTE]
> Visual Studio 2013 中提供 OWIN Startup 類別範本。 如果您使用 Visual Studio 2012，只要加入名為 `Startup1`的新空白類別，然後貼上下列程式碼：

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample2.cs)]

### <a name="run-the-application"></a>執行應用程式

按 F5 開始偵錯。 Visual Studio 將會開啟瀏覽器視窗來 `http://localhost:*port*/`。 此頁面看起來應該如下所示：

![](getting-started-with-owin-and-katana/_static/image5.png)

## <a name="self-host-owin-in-a-console-application"></a>主控台應用程式中的自我裝載 OWIN

在自訂進程中，將此應用程式從 IIS 裝載轉換為自我裝載是很容易的。 使用 IIS 裝載時，IIS 會同時做為 HTTP 伺服器和裝載服務的進程。 使用自我裝載時，您的應用程式會建立進程，並使用**HttpListener**類別做為 HTTP 伺服器。

在 Visual Studio 中，建立新的主控台應用程式。 在 [套件管理員主控台] 視窗中，輸入下列命令：

`Install-Package Microsoft.Owin.SelfHost -Pre`

將本教學課程的第1部分中的 `Startup1` 類別加入至專案。 您不需要修改這個類別。

依照下列方式，執行應用程式的 `Main` 方法。

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample3.cs)]

當您執行主控台應用程式時，伺服器會開始接聽 `http://localhost:9000`。 如果您在網頁瀏覽器中流覽至此位址，您會看到 [Hello world] 頁面。

![](getting-started-with-owin-and-katana/_static/image6.png)

## <a name="add-owin-diagnostics"></a>新增 OWIN 診斷

Owin 診斷套件包含的中介軟體會攔截未處理的例外狀況，並顯示包含錯誤詳細資料的 HTML 頁面。 此頁面的運作方式非常類似 ASP.NET 錯誤頁面，有時稱為「[黃色的死亡螢幕](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)」（YSOD）。 就像 YSOD，Katana 錯誤頁面在開發期間很有用，但在生產模式中將它停用是很好的作法。

若要在您的專案中安裝診斷套件，請在 [套件管理員主控台] 視窗中輸入下列命令：

`install-package Microsoft.Owin.Diagnostics –Pre`

變更 `Startup1.Configuration` 方法中的程式碼，如下所示：

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample4.cs?highlight=4,9-12)]

現在使用 CTRL + F5 來執行應用程式，而不進行任何偵測，因此 Visual Studio 不會在例外狀況時中斷。 應用程式的行為與之前相同，除非您流覽至 `http://localhost/fail`，此時應用程式會擲回例外狀況。 錯誤頁面中介軟體會攔截例外狀況，並顯示 HTML 頁面，其中包含錯誤的相關資訊。 您可以按一下索引標籤，以查看堆疊、查詢字串、cookie、要求標頭和 OWIN 環境變數。

![](getting-started-with-owin-and-katana/_static/image7.png)

## <a name="next-steps"></a>後續步驟

- [OWIN 啟動類別偵測](owin-startup-class-detection.md)
- [使用 OWIN 自我裝載 ASP.NET Web API](../../../web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)
- [使用 OWIN 自我裝載 SignalR](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)
