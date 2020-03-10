---
uid: aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: 使用 Visual Studio 的程式設計 ASP.NET Web Pages （Razor） |Microsoft Docs
author: Rick-Anderson
description: 本附錄說明您可以如何使用 Visual Studio 2010 或 Visual Web Developer 2010 Express，以 Razor 語法來程式 ASP.NET Web Pages。
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: 1a76098779d05912bf7bdf2de5fdce024770752c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78633508"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a>使用 Visual Studio 的程式設計 ASP.NET Web Pages （Razor）

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本文說明如何使用 Visual Studio 或 Visual Web Developer Express 來程式 ASP.NET Web Pages （Razor）網站。
>
> 您將學到什麼
>
> - 您需要安裝的內容（如果有的話），才能與您的 Visual Studio 版本中的 ASP.NET Web Pages 搭配使用。
> - 如何將 ASP.NET Web Pages 的支援新增至 Visual Web Developer 2010 Express。
> - 如何使用 Visual Studio 中的功能來處理 ASP.NET Razor 頁面，包括 IntelliSense 和偵錯工具。
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
>
>
> - ASP.NET Web Pages （Razor）3
> - Visual Studio 2013
> - WebMatrix 3
>
>
> 本教學課程也適用于 ASP.NET Web Pages 2、Visual Studio 2012、Visual Studio 2010 和 WebMatrix 2。

您可以使用 WebMatrix 或許多其他程式碼編輯器，利用 Razor 語法來設計 ASP.NET 網頁。 您也可以使用 Microsoft Visual Studio，這是功能完整的整合式開發環境（IDE），可提供一組強大的工具來建立許多類型的應用程式（而不只是網站）。 若要使用 ASP.NET Razor 頁面，您可以使用[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。

Visual Studio 為使用 ASP.NET Razor 網頁進行程式設計所提供的兩個特別有用的功能如下：

- *IntelliSense*。 Visual Studio 內建的 IntelliSense 功能比 WebMatrix 中的 IntelliSense 更全面。
- *偵錯工具*。 偵錯工具可讓您針對程式碼進行疑難排解，方法是停止執行中的程式、檢查變數，然後逐行執行程式碼。

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a>使用不同版本的 Visual Studio ASP.NET Web Pages

若要在 Visual Studio 2017 中開發 ASP.NET web 應用程式，請安裝**ASP.NET 和 網頁程式開發**工作負載。

Visual Studio 2012 和 Visual Studio 2013 包含 ASP.NET Web Pages 的支援。 （當您安裝 Visual Studio 時，會安裝支援 ASP.NET Web Pages 所需的套件）。

Visual Studio 2010 預設不包含 ASP.NET Web Pages 的支援。 若要使用 ASP.NET Web Pages 搭配 Visual Studio 2010，您必須安裝 ASP.NET MVC 封裝。 若要取得 ASP.NET Web Pages 2，請安裝 ASP.NET MVC 4。

下表摘要說明不同 Visual Studio 版本中 ASP.NET Web Pages 的支援。

|  | Visual Studio 2010 | Visual Studio 2012 | Visual Studio 2013 |
| --- | --- | --- | --- |
| **ASP.NET Web Pages 2** | 安裝 ASP.NET MVC 4 | 含 | 含 |
| **ASP.NET Web Pages 3** |  | 透過 NuGet 更新為 ASP.NET Web Pages 3 | 含 |

若要使用 Visual Studio 2010，請參閱[在 Visual Studio 2010 中安裝 ASP.NET Web Pages 的支援](#vs2010support)。

## <a name="launching-visual-studio-from-webmatrix"></a>從 WebMatrix 啟動 Visual Studio

如果您已在 WebMatrix 中啟動專案，並想要切換至 Visual Studio，WebMatrix 會提供一個按鈕，讓您輕鬆地在 Visual Studio 中開啟專案。 您必須在電腦上安裝 Visual Studio，才能啟用此按鈕。 下圖顯示 WebMatrix 中的按鈕。

![啟動 Visual Studio](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

當您按一下按鈕時，專案會以 Visual Studio 開啟。 您可以在 WebMatrix 與 Visual Studio 之間來回切換，而不會發生任何問題。 如果其他環境中有任何檔案已變更，而且需要重載以取得最新的變更，您將會收到通知。

## <a name="creating-aspnet-razor-site-in-visual-studio"></a>在 Visual Studio 中建立 ASP.NET Razor 網站

在 Visual Studio 中建立 ASP.NET Razor 網站：

1. 開啟 Visual Studio。
2. **在 [檔案**] 功能表中，按一下 [**新網站**]。

    ![建立新網站](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. 在 [**新網站**] 對話方塊中，選取要使用的語言（[ C#視覺效果] 或 [Visual Basic]）。
4. 選取 [ **ASP.NET 網站（Razor）** ] 範本。

    ![razor 網站](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. 按一下 [確定]。

您的新專案已存在，並已填入一些可協助您開始使用的預設網頁。

### <a name="using-intellisense"></a>Using IntelliSense

既然您已建立網站，就可以查看 IntelliSense 在 Visual Studio 中的運作方式。

1. 在您剛建立的網站中，開啟 [*預設的. cshtml* ] 頁面。
2. 在頁面中 `<h3>` 標記之後，輸入 `@ServerInfo.` （包括點）。 請注意 IntelliSense 如何在下拉式清單中顯示 `ServerInfo` helper 的可用方法。

    ![IntelliSense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. 從清單中選取 [`GetHtml`] 方法，然後按 Enter 鍵。 IntelliSense 會自動填入方法。 （如同中C#的任何方法，您必須在方法後面加上 `()` 字元）。`GetHtml` 方法的完整程式碼如下列範例所示：

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. 按 Ctrl + F5 執行頁面。 這是頁面在瀏覽器中顯示時的樣子：

    ![瀏覽器中的預設頁面](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. 關閉瀏覽器。

### <a name="using-the-debugger"></a>使用偵錯工具

1. 在預設的 [ *cshtml* ] 頁面頂端，以 `Page.Title`開頭的那一行之後，加入下列程式程式碼：

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. 在編輯器灰色邊界的程式碼左側，按一下這個新行的 [下一步]，以新增*中斷點*。 「中斷點」是一種標記，會告知偵錯工具在該時間點停止執行程式，讓您可以查看發生的狀況。

    ![設定中斷點](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. 移除對 `ServerInfo.GetHtml` 方法的呼叫，並在其位置加入 `@myTime` 變數的呼叫。 此呼叫會顯示新的程式程式碼所傳回的目前時間值。
4. 按 F5 以在偵錯工具中執行頁面。 頁面會在您設定的中斷點上停止。 下圖顯示在編輯器中，使用中斷點時頁面的外觀（以黃色表示）。

    ![調試中斷點](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. 在 [偵錯工具] 工具列中，按一下 [**逐步**執行] 按鈕（或按 F11）以執行下一行程式碼。 每當您按一下此按鈕時，就會將執行前移至下一行程式碼。

    ![[逐步執行] 按鈕](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. 藉由將滑鼠指標停留在其上方或檢查 [**區域變數**] 和 [**呼叫堆疊**] 視窗中顯示的值，檢查 `myTime` 變數的值。 Visual Studio 顯示變數的值。

    ![顯示時間值](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. 當您完成檢查變數並逐步執行程式碼時，請按 F5 繼續執行頁面，而不會在每一行停止。 當您完成逐步執行所有程式碼時，瀏覽器會顯示頁面。

若要深入瞭解偵錯工具，以及如何在 Visual Studio 中偵錯工具代碼，請參閱[逐步解說：在 Visual Web Developer 中偵測網頁](https://msdn.microsoft.com/library/z9e7w6cs.aspx)。

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a>在 ASP.NET MVC 專案中使用 Razor 搭配 Visual Studio

Razor 語法也廣泛用於 ASP.NET MVC 專案。 MVC 是一種功能強大、以模式為基礎的方式，可建立動態網站。 如果您的 ASP.NET Web Pages 網站變得難以維護，您可能會想要考慮將它轉換成 ASP.NET MVC 應用程式。 如需建立 MVC 應用程式的範例，請參閱[使用 ASP.NET MVC 5 消費者入門](../../../mvc/overview/getting-started/introduction/getting-started.md)。

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a>在 Visual Studio 2010 中安裝 ASP.NET Web Pages 的支援

本節說明如何安裝 Visual Web Developer Express 2010 和適用于 Visual Studio 的 ASP.NET Web Pages 工具。

1. 如果您還沒有 Web Platform Installer，請從下列 URL 下載：

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. 執行 Web Platform Installer。
3. 按一下 [**產品**] 索引標籤。

    ![WebPI 產品索引標籤](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. 搜尋**ASP.NET MVC 4** （適用于 ASP.NET Web Pages 2），然後按一下 [**新增**]。 這些產品包括用來建立 ASP.NET Razor 網站的 Visual Studio 工具。

    ![WebPi 安裝選項](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. 按一下 [**安裝**] 以完成安裝。
