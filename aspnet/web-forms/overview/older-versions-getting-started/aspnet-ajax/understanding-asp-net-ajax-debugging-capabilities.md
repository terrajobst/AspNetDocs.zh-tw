---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-debugging-capabilities
title: 瞭解 ASP.NET AJAX 調試功能 |Microsoft Docs
author: scottcate
description: Debug 程式碼的功能是每位開發人員都應該在其利器中擁有的技能，不論他們使用的技術為何。 雖然許多開發人員都是 。
ms.author: riande
ms.date: 03/28/2008
ms.assetid: 7f9380c6-19f7-4c82-a019-916ec6dffc9c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-debugging-capabilities
msc.type: authoredcontent
ms.openlocfilehash: 08ced380f3551407d757524dbc84b5feeeb5482b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78629504"
---
# <a name="understanding-aspnet-ajax-debugging-capabilities"></a>了解 ASP.NET AJAX 偵錯功能

由[Scott Cate](https://github.com/scottcate)

[下載 PDF](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial06_Debugging_MS_Ajax_Applications_cs.pdf)

> Debug 程式碼的功能是每位開發人員都應該在其利器中擁有的技能，不論他們使用的技術為何。 雖然許多開發人員習慣使用 Visual Studio .NET 或 Web Developer Express 來進行使用 VB.NET 或C#程式碼的 ASP.NET 應用程式，但卻不知道它也非常適合用來偵測用戶端程式代碼（例如 JavaScript）。 用來進行 .NET 應用程式的相同類型技術也可以套用至啟用 AJAX 的應用程式，並更明確地 ASP.NET AJAX 應用程式。

## <a name="debugging-aspnet-ajax-applications"></a>ASP.NET AJAX 應用程式的偵錯工具

Dan Wahlin

Debug 程式碼的功能是每位開發人員都應該在其利器中擁有的技能，不論他們使用的技術為何。 不需要說，瞭解有哪些不同的偵錯工具選項可以在專案上節省大量時間，甚至可能會有一些難題。 雖然許多開發人員習慣使用 Visual Studio .NET 或 Web Developer Express 來進行使用 VB.NET 或C#程式碼的 ASP.NET 應用程式，但卻不知道它也非常適合用來偵測用戶端程式代碼（例如 JavaScript）。 用來進行 .NET 應用程式的相同類型技術也可以套用至啟用 AJAX 的應用程式，並更明確地 ASP.NET AJAX 應用程式。

在本文中，您將瞭解如何使用 Visual Studio 2008 和數個其他工具來進行 ASP.NET AJAX 應用程式的 debug，以快速找出錯誤和其他問題。 本討論將包含有關啟用 Internet Explorer 6 或更新版本以進行偵錯工具的資訊，使用 Visual Studio 2008 和腳本瀏覽器來逐步執行程式碼，以及使用其他免費工具，例如 Web 開發 Helper。 您也將瞭解如何使用名為 Firebug 的延伸模組，在 Firefox 中進行 ASP.NET AJAX 應用程式的 debug，讓您直接在瀏覽器中執行 JavaScript 程式碼，而不需要任何其他工具。 最後，您將會引進 ASP.NET AJAX 程式庫中的類別，協助進行各種偵錯工具工作，例如追蹤和程式碼判斷提示語句。

在您嘗試在 Internet Explorer 中流覽頁面之前，您必須執行幾個基本步驟，才能讓它進行偵錯工具。 讓我們看看一些必須執行才能開始使用的基本設定需求。

## <a name="configuring-internet-explorer-for-debugging"></a>設定 Internet Explorer 以進行偵錯工具

大部分的人都不感興趣看到在使用 Internet Explorer 流覽的網站上遇到的 JavaScript 問題。 事實上，即使使用者看到錯誤訊息，也不知道該怎麼辦。 因此，瀏覽器預設會關閉偵錯工具選項。 不過，在您開發新的 AJAX 應用程式時，將偵錯工具轉換成，並將它當作使用，是非常直接的。

若要啟用調試功能，請移至 Internet Explorer 功能表上的 [工具] [網際網路選項]，然後選取 [Advanced] 索引標籤。在 [流覽] 區段中，確定未核取下列專案：

- 停用腳本調試（Internet Explorer）
- 停用腳本調試（其他）

雖然不是必要的，但如果您嘗試對應用程式進行錯用，您可能會想要讓頁面中的任何 JavaScript 錯誤立即可見且顯而易見。 您可以藉由核取 [顯示每個腳本錯誤的通知] 核取方塊，以強制顯示所有錯誤與訊息方塊。 雖然這是在開發應用程式時開啟的絕佳選項，但如果您只是要流覽其他網站，可能很快就會變得很麻煩，因為遇到 JavaScript 錯誤的機率很好。

[圖 1] 顯示 Internet Explorer [advanced] 對話方塊在正確設定以進行偵錯工具後應看到的外觀。

[![設定 Internet Explorer 以進行偵錯工具。](understanding-asp-net-ajax-debugging-capabilities/_static/image2.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image1.png)

**圖 1**：設定 Internet Explorer 以進行偵錯工具。  （[按一下以查看完整大小的影像](understanding-asp-net-ajax-debugging-capabilities/_static/image3.png)）

開啟偵錯工具後，您會看到新的功能表項目出現在名為 [腳本偵錯工具] 的 [View] 功能表中。 它有兩個可用的選項，包括在下一個語句中開啟和中斷。 選取 [開啟] 時，系統會提示您在 Visual Studio 2008 中進行頁面的偵錯工具（請注意，Visual Web Developer Express 也可以用來進行偵錯工具）。 如果 Visual Studio .NET 目前正在執行，您可以選擇使用該實例或建立新的實例。 當選取 [在下一個語句中斷] 時，系統會提示您在執行 JavaScript 程式碼時，將頁面進行偵錯工具。 如果 JavaScript 程式碼在頁面的 onLoad 事件中執行，您可以重新整理頁面，以觸發「偵錯工具」會話。 如果在按一下按鈕之後執行 JavaScript 程式碼，則在按一下按鈕之後，就會立即執行偵錯工具。

> [!NOTE]
> 如果您是在啟用使用者存取控制（UAC）的 Windows Vista 上執行，而且 Visual Studio 2008 設定為以系統管理員身分執行，則當系統提示您附加時，Visual Studio 將無法附加至進程。 若要解決此問題，請先啟動 Visual Studio，然後使用該實例來進行 debug。

雖然下一節將示範如何直接從 Visual Studio 2008 內進行 ASP.NET AJAX 頁面的偵錯工具，但使用 Internet Explorer 腳本偵錯工具選項在頁面已開啟，而您想要更完整地進行檢查時，是很有用的。

## <a name="debugging-with-visual-studio-2008"></a>使用 Visual Studio 2008 進行調試

Visual Studio 2008 提供了偵錯工具功能，讓世界各地的開發人員依賴每日來進行 .NET 應用程式的 debug。 內建的偵錯工具可讓您逐步執行程式碼、查看物件資料、監看特定變數、監視呼叫堆疊，再加上更多。 除了偵錯工具 VB.NET 或C#程式碼之外，偵錯工具也有助於對 ASP.NET AJAX 應用程式進行檢查，並可讓您逐行執行 JavaScript 程式碼。 後面的詳細資料著重于可用來對用戶端腳本檔案進行偵錯工具的技術，而不是提供語篇使用 Visual Studio 2008 來對應用程式進行整體的處理。

在 Visual Studio 2008 中，可以透過數種不同的方式來啟動偵錯工具的處理常式。 首先，您可以使用上一節中所述的 Internet Explorer 腳本偵錯工具選項。 當頁面已經載入瀏覽器中，而且您想要開始對它進行調試時，這項功能就很好用。 或者，您也可以在方案總管中的 .aspx 頁面上按一下滑鼠右鍵，然後從功能表中選取 [設定為起始頁]。 如果您習慣進行 ASP.NET 網頁的調試，則您可能會在之前完成此作業。 按下 F5 之後，就可以調試頁面。 不過，雖然您通常可以在 VB.NET 或C#程式碼中的任何位置設定中斷點，但 JavaScript 的情況並不一定，因為您會在下一步看到。

*內嵌與外部腳本*

Visual Studio 2008 偵錯工具會將 JavaScript 內嵌在與外部 JavaScript 檔案不同的頁面中。 使用外部腳本檔案時，您可以開啟檔案，並在您選擇的任何一行上設定中斷點。 按一下 [程式碼編輯器] 視窗左側的灰色紙匣區域，即可設定中斷點。 當 JavaScript 使用 `<script>` 標籤直接內嵌到頁面時，按一下灰色的紙匣區域中的設定中斷點並不是選項。 嘗試在內嵌腳本的程式程式碼上設定中斷點，會產生指出「這不是中斷點的有效位置」的警告。

若要解決這個問題，您可以將程式碼移到外部 .js 檔案，然後使用 &lt;腳本&gt; 標記的 src 屬性來參考它：

[!code-html[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample1.html)]

如果將程式碼移到外部檔案不是一個選項，或是需要的工作不太值得這麼做，該怎麼辦？ 當您無法使用編輯器來設定中斷點時，您可以將偵錯工具語句直接加入您想要開始進行偵錯工具的程式碼中。 您也可以使用 ASP.NET AJAX 程式庫中提供的 Sys.databases 類別來強制開始進行調試。 您將會在本文稍後進一步瞭解 Sys.databases 類別。

[清單 1] 顯示使用 `debugger` 關鍵字的範例。 這個範例會強制偵錯工具在進行 update 函式的呼叫之前中斷。

**[清單 1]。使用偵錯工具關鍵字來強制 Visual Studio .NET 偵錯工具中斷。**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample2.js)]

一旦叫用偵錯工具語句，系統會提示您使用 Visual Studio .NET 來將頁面進行 debug，並且可以開始逐步執行程式碼。 執行此動作時，您可能會遇到存取頁面中所使用之 ASP.NET AJAX library 腳本檔案的問題，讓我們來看一下如何使用 Visual Studio。NET 的腳本瀏覽器。

## <a name="using-visual-studio-net-windows-to-debug"></a>使用 Visual Studio 的 .NET 視窗進行 Debug

啟動 debug 會話並開始使用預設的 F11 鍵來逐步執行程式碼之後，您可能會遇到如 [圖 2] 所示的錯誤對話方塊，除非頁面中使用的所有腳本檔案都已開啟且可供進行偵錯工具。

[當沒有可用於進行偵錯工具的原始程式碼時，會顯示 ![錯誤 對話方塊。](understanding-asp-net-ajax-debugging-capabilities/_static/image5.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image4.png)

**圖 2**：沒有可用來進行偵錯工具的原始程式碼時，所顯示的錯誤對話方塊。  （[按一下以查看完整大小的影像](understanding-asp-net-ajax-debugging-capabilities/_static/image6.png)）

這個對話方塊會顯示，因為 Visual Studio .NET 並不確定如何取得頁面所參考之部分腳本的原始程式碼。 雖然這一開始可能很令人沮喪，但還是有一個簡單的修正方法。 當您啟動 debug 會話並叫用中斷點之後，請移至 [Visual Studio 2008] 功能表上的 [Debug Windows Script Explorer] 視窗，或使用 Ctrl + Alt + N 熱鍵。

> [!NOTE]
> 如果您看不到列出的 [腳本瀏覽器] 功能表，請移至 [**工具**] > 在 [Visual Studio .net] 功能表上**自訂** > **命令**。 在 [類別] 區段中找出 [ **Debug** ] 專案，然後按一下它以顯示所有可用的功能表項目。 在 [命令] 清單中，向下流覽至 [腳本瀏覽器]，然後將它拖曳到稍早所述的 [Debug Windows] 功能表上。 如此一來，每當您執行 Visual Studio .NET 時，都可以使用 [腳本瀏覽器] 功能表項目。

[腳本瀏覽器] 可以用來查看頁面中使用的所有腳本，並在程式碼編輯器中開啟它們。 開啟 [腳本瀏覽器] 之後，按兩下目前正在進行調試的 .aspx 頁面，在程式碼編輯器視窗中開啟它。 對腳本瀏覽器中顯示的所有其他腳本執行相同的動作。 在程式碼視窗中開啟所有腳本之後，您可以按 F11 鍵（並使用其他的 debug 快速鍵）來逐步執行程式碼。 [圖 3] 顯示腳本瀏覽器的範例。 它會列出目前正在進行調試的檔案（示範 .aspx）以及兩個自訂腳本，以及由 ASP.NET AJAX ScriptManager 動態插入至頁面的兩個腳本。

[![[腳本] Explorer 可讓您輕鬆存取頁面中使用的腳本。](understanding-asp-net-ajax-debugging-capabilities/_static/image8.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image7.png)

[**圖 3**] [腳本瀏覽器] 可讓您輕鬆存取頁面中使用的腳本。  （[按一下以查看完整大小的影像](understanding-asp-net-ajax-debugging-capabilities/_static/image9.png)）

當您逐步執行頁面中的程式碼時，也可以使用數個其他視窗來提供有用的資訊。 例如，您可以使用 [區域變數] 視窗來查看頁面中使用之不同變數的值，[即時運算] 視窗會評估特定的變數或條件，並查看輸出。 您也可以使用 [輸出] 視窗來查看使用 Sys.databases. Debug 函式（將于本文稍後說明）或 Internet Explorer 的 writeln 函數所寫出的追蹤語句。

當您使用偵錯工具逐步執行程式碼時，您可以將滑鼠停留在程式碼中的變數上，以查看其所指派的值。 不過，當您將滑鼠停留在指定的 JavaScript 變數上時，腳本偵錯工具偶爾不會顯示任何專案。 若要查看值，請反白顯示您嘗試在 [程式碼編輯器] 視窗中看到的語句或變數，然後將滑鼠移至其上方。 雖然這項技術在每種情況下都不適用，但是您可以在不需要查看不同的調試視窗（例如 [區域變數] 視窗）中查看值。

示範這裡所討論的一些功能的影片教學課程，可以在[http://www.xmlforasp.net](http://www.xmlforasp.net)觀看。

## <a name="debugging-with-web-development-helper"></a>使用 Web 開發 Helper 進行偵錯工具

雖然 Visual Studio 2008 （和 Visual Web Developer Express 2008）是功能強大的偵錯工具，但還有其他選項可供使用，而且較輕量。 其中一個要發行的最新工具是 Web 開發 Helper。 Microsoft 的 Nikhil Kothari （Microsoft 的其中一個關鍵 ASP.NET AJAX 架構設計人員）撰寫了這項絕佳的工具，可從簡單的偵錯工具執行許多不同的工作，以查看 HTTP 要求和回應訊息。 您可以在[http://projects.nikhilk.net/Projects/WebDevHelper.aspx](http://projects.nikhilk.net/Projects/WebDevHelper.aspx)下載 Web 開發協助程式。

Web 開發協助程式可以直接在 Internet Explorer 內部使用，方便您使用。 其啟動方式是從 Internet Explorer 功能表中選取 [工具] [Web 開發 Helper]。 這會在瀏覽器的下半部開啟工具，這很好用，因為您不需要離開瀏覽器來執行數項工作，例如 HTTP 要求和回應訊息記錄。 [圖 4] 顯示 Web 開發 Helper 的外觀。

[![Web 開發 Helper](understanding-asp-net-ajax-debugging-capabilities/_static/image11.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image10.png)

**圖 4**： Web 開發 Helper （[按一下以觀看完整大小的影像](understanding-asp-net-ajax-debugging-capabilities/_static/image12.png)）

Web 開發 helper 不是您將用來逐行執行程式碼的工具，如同 Visual Studio 2008。 不過，它可以用來查看追蹤輸出、輕鬆評估腳本中的變數，或是探索 JSON 物件內的資料。 它也非常適合用來查看傳遞至 ASP.NET AJAX 頁面和伺服器的資料。

在 Internet Explorer 中開啟 Web 開發 Helper 之後，必須從 Web 開發 Helper 功能表選取 [腳本] [啟用腳本]，以啟用腳本的偵錯工具，如 [圖 4] 稍早所示。 這可讓工具攔截在執行頁面時所發生的錯誤。 它也可讓您輕鬆存取頁面中輸出的追蹤訊息。 若要在頁面中查看追蹤資訊或執行指令碼命令以測試不同的函式，請從 Web 開發 Helper 功能表選取 [腳本] [顯示腳本主控台]。 這可讓您存取 [命令] 視窗和簡單的 [即時運算] 視窗。

*查看追蹤訊息和 JSON 物件資料*

[即時運算] 視窗可用來執行指令碼命令，或甚至載入或儲存用來測試頁面中不同功能的腳本。 [命令] 視窗會顯示所要查看的頁面所寫出的追蹤或 debug 訊息。 [清單 2] 顯示如何使用 Internet Explorer 的 writeln 函數撰寫追蹤訊息。

**[清單 2]。使用 Debug 類別寫出用戶端追蹤訊息。**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample3.js)]

如果 LastName 屬性包含 Doe 的值，Web 開發協助程式會在腳本主控台的命令視窗中顯示「Person name： Doe」訊息（假設已啟用偵錯工具）。 Web 開發協助程式也會在頁面中新增最上層的 debugService 物件，以用來寫出追蹤資訊或查看 JSON 物件的內容。 [清單 3] 顯示使用 debugService 類別之 trace 函數的範例。

**[清單 3]。使用 Web 開發 Helper 的 debugService 類別來撰寫追蹤訊息。**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample4.js)]

DebugService 類別有一個不錯的功能，就是即使在 Internet Explorer 中未啟用「偵測」，也能讓您在 Web 開發 Helper 執行時輕鬆地存取追蹤資料，這也是很好的。 當此工具不是用來對頁面進行 debug 時，將會忽略 trace 語句，因為呼叫 debugService 將會傳回 false。

DebugService 類別也可讓您使用 Web 開發 Helper 的 [偵測器] 視窗來查看 JSON 物件資料。 [清單 4] 會建立包含人員資料的簡單 JSON 物件。 建立物件之後，會呼叫 debugService 類別的檢查函式，以允許以視覺化方式檢查 JSON 物件。

**[清單 4]。使用 debugService 函數來查看 JSON 物件資料。**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample5.js)]

在頁面中或透過 [即時運算] 視窗呼叫 GetPerson （）函式，會導致 [物件偵測器] 對話方塊視窗出現，如 [圖 5] 所示。 您可以藉由反白顯示物件內的屬性，變更 [值] 文字方塊中顯示的值，然後按一下 [更新] 連結，以動態方式變更。 使用物件偵測器可讓您直接查看 JSON 物件資料，並實驗將不同的值套用至屬性。

*調試錯誤*

除了允許顯示追蹤資料和 JSON 物件之外，Web 開發 helper 也可以協助在頁面中偵測錯誤。 如果發生錯誤，系統會提示您繼續進行下一行程式碼，或對腳本進行偵錯工具（請參閱 [圖 6]）。 [腳本錯誤] 對話方塊視窗會顯示完整的呼叫堆疊以及行號，讓您可以輕鬆地識別問題在腳本中的位置。

[![使用 [物件偵測器] 視窗來查看 JSON 物件。](understanding-asp-net-ajax-debugging-capabilities/_static/image14.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image13.png)

**圖 5**：使用 [物件偵測器] 視窗來查看 JSON 物件。  （[按一下以查看完整大小的影像](understanding-asp-net-ajax-debugging-capabilities/_static/image15.png)）

選取 [偵錯工具] 選項可讓您直接在 Web 開發 Helper 的 [即時運算] 視窗中執行腳本語句，以查看變數的值、寫出 JSON 物件，再加上更多。 如果再次執行觸發錯誤的相同動作，而且電腦上有 Visual Studio 2008，系統會提示您啟動 debug 會話，讓您可以逐步執行程式程式碼，如前一節所討論。

[![Web 開發 Helper 的腳本錯誤對話方塊](understanding-asp-net-ajax-debugging-capabilities/_static/image17.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image16.png)

**圖 6**： Web 開發 Helper 的腳本錯誤對話方塊（[按一下以查看完整大小的影像](understanding-asp-net-ajax-debugging-capabilities/_static/image18.png)）

*檢查要求和回應訊息*

在調試 ASP.NET AJAX 頁面時，查看頁面與伺服器之間傳送的要求和回應訊息通常會很有用。 在訊息內查看內容可讓您查看是否傳遞了適當的資料，以及訊息的大小。 Web 開發 Helper 提供絕佳的 HTTP 訊息記錄器功能，可讓您輕鬆地以原始文字或更容易閱讀的格式來查看資料。

若要查看 ASP.NET AJAX 要求和回應訊息，必須啟用 HTTP 記錄器，方法是從 Web 開發 Helper 功能表選取 [HTTP] [啟用 HTTP 記錄]。 啟用之後，您可以在 HTTP 記錄檢視器中查看從目前頁面傳送的所有訊息，方法是選取 [HTTP] [顯示 HTTP 記錄] 來存取。

雖然查看每個要求/回應訊息中所傳送的原始文字確實有用（以及 Web 開發 Helper 中的選項），但通常更容易以更圖形化的格式來查看訊息資料。 啟用 HTTP 記錄並記錄訊息之後，您可以按兩下 HTTP 記錄檢視器中的訊息，以查看訊息資料。 這麼做可讓您查看所有與訊息相關聯的標頭，以及實際的訊息內容。 [圖 7] 顯示在 [HTTP 記錄檔檢視器] 視窗中查看的要求訊息和回應訊息的範例。

[![使用 HTTP 記錄檢視器來查看要求和回應訊息資料。](understanding-asp-net-ajax-debugging-capabilities/_static/image20.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image19.png)

**圖 7**：使用 HTTP 記錄檢視器來查看要求和回應訊息資料。  （[按一下以查看完整大小的影像](understanding-asp-net-ajax-debugging-capabilities/_static/image21.png)）

HTTP 記錄檢視器會自動剖析 JSON 物件，並使用樹狀檢視加以顯示，讓您快速且輕鬆地查看物件的屬性資料。 當 UpdatePanel 在 ASP.NET AJAX 頁面中使用時，檢視器會將訊息的每個部分細分為個別元件，如 [圖 8] 所示。 這是很棒的功能，可讓您更輕鬆地查看和瞭解訊息中的內容，與查看原始訊息資料相較之下。

[![使用 HTTP 記錄檢視器所查看的 UpdatePanel 回應訊息。](understanding-asp-net-ajax-debugging-capabilities/_static/image23.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image22.png)

**圖 8**：使用 HTTP 記錄檢視器查看的 UpdatePanel 回應訊息。  （[按一下以查看完整大小的影像](understanding-asp-net-ajax-debugging-capabilities/_static/image24.png)）

除了 Web 開發 Helper 以外，還有其他幾項工具可用來查看要求和回應訊息。 另一個不錯的選項是 Fiddler，可在[http://www.fiddlertool.com](http://www.fiddlertool.com)免費使用。 雖然這裡不會討論 Fiddler，但當您需要徹底檢查訊息標頭和資料時，這也是個不錯的選項。

## <a name="debugging-with-firefox-and-firebug"></a>使用 Firefox 和 Firebug 進行調試

雖然 Internet Explorer 仍然是最普遍使用的瀏覽器，但 Firefox 之類的其他瀏覽器也變得很熱門，而且使用的也越來越多。 因此，您會想要在 Firefox 和 Internet Explorer 中查看和檢查 ASP.NET AJAX 頁面，以確保您的應用程式能正常運作。 雖然 Firefox 無法直接系結至 Visual Studio 2008 以進行偵錯工具，但它有一個稱為 Firebug 的擴充功能，可用來對頁面進行偵錯工具。 Firebug 可以免費下載，方法是前往[http://www.getfirebug.com](http://www.getfirebug.com)。

Firebug 提供全功能的偵錯工具環境，可用來逐行執行程式碼、存取頁面中使用的所有腳本、查看 DOM 結構、顯示 CSS 樣式，甚至追蹤頁面中發生的事件。 安裝之後，您可以從 Firefox 功能表中選取 [工具] [Firebug] [開啟 Firebug] 來存取 Firebug。 就像 Web 開發 Helper 一樣，Firebug 會直接在瀏覽器中使用，不過它也可以當做獨立的應用程式使用。

一旦 Firebug 執行，不論腳本是否內嵌在頁面中，都可以在 JavaScript 檔案的任何一行上設定中斷點。 若要設定中斷點，請先載入您想要在 Firefox 中進行 debug 的適當頁面。 載入頁面之後，請從 Firebug 的 [腳本] 下拉式清單中選取要進行 debug 的腳本。 頁面所使用的所有腳本都會顯示出來。 若要設定中斷點，您可以在 Firebug 的灰色紙匣區域中按一下中斷點所在的行，就像您在 Visual Studio 2008 中所做的一樣。

在 Firebug 中設定中斷點之後，您可以執行必要的動作來執行需要進行調試的腳本，例如按一下按鈕或重新整理瀏覽器以觸發 onLoad 事件。 執行會在包含中斷點的行上自動停止。 [圖 9] 顯示 Firebug 中已觸發中斷點的範例。

[![在 Firebug 中處理中斷點。](understanding-asp-net-ajax-debugging-capabilities/_static/image26.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image25.png)

**圖 9**：處理 Firebug 中的中斷點。  （[按一下以查看完整大小的影像](understanding-asp-net-ajax-debugging-capabilities/_static/image27.png)）

到達中斷點之後，您就可以使用箭號按鈕逐步執行、不進入或跳過程式碼。 當您逐步執行程式碼時，腳本變數會顯示在偵錯工具的右側部分，讓您可以查看值並向下切入至物件。 Firebug 也包含 [呼叫堆疊] 下拉式清單，可讓您查看腳本的執行步驟，而這會導致目前正在進行調試的一行。

Firebug 也包含一個主控台視窗，可以用來測試不同的腳本語句、評估變數及查看追蹤輸出。 您可以按一下 [Firebug] 視窗頂端的 [主控台] 索引標籤來存取它。 您也可以按一下 [檢查] 索引標籤，「檢查」要進行調試的頁面，以查看其 DOM 結構和內容。當您將滑鼠停留在 [偵測器] 視窗中顯示的不同 DOM 元素上方時，頁面的適當部分將會反白顯示，讓您可以輕鬆地查看該專案在頁面中的使用位置。 與指定專案相關聯的屬性值可以變更為「即時」，以實驗將不同的寬度、樣式等專案套用至元素。 這是很好的功能，可讓您不需要在原始程式碼編輯器和 Firefox 瀏覽器之間持續切換，以查看簡單的變更對頁面的影響。

[圖 10] 顯示在頁面中使用 DOM 偵測器來尋找名為 txtCountry 的 textbox 的範例。 Firebug 偵測器也可以用來查看頁面中使用的 CSS 樣式，以及追蹤滑鼠移動、按鈕點擊等事件。

[![使用 Firebug 的 DOM 偵測器。](understanding-asp-net-ajax-debugging-capabilities/_static/image29.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image28.png)

**圖 10**：使用 FIREBUG 的 DOM 偵測器。  （[按一下以查看完整大小的影像](understanding-asp-net-ajax-debugging-capabilities/_static/image30.png)）

Firebug 提供了輕量的方法，可直接在 Firefox 中快速地對頁面進行偵錯工具，以及檢查頁面內的不同元素的絕佳工具。

## <a name="debugging-support-in-aspnet-ajax"></a>ASP.NET AJAX 中的調試支援

ASP.NET AJAX library 包含許多不同的類別，可用來簡化將 AJAX 功能新增至網頁的程式。 您可以使用這些類別來尋找頁面中的專案，並進行操作、加入新的控制項、呼叫 Web 服務，甚至處理事件。 ASP.NET AJAX 程式庫也包含類別，可以用來增強偵錯工具頁面的處理常式。 在本節中，您將會介紹 Sys.databases 類別，並瞭解如何在應用程式中使用它。

*使用 Sys.databases 類別*

Sys.databases 類別（位於 Sys 命名空間中的 JavaScript 類別）可以用來執行數個不同的函式，包括撰寫追蹤輸出、執行程式碼判斷提示和強制程式碼失敗，以便進行調試。 它廣泛用於 ASP.NET AJAX 程式庫的 debug 檔案（安裝于 C:\Program Files\Microsoft ASP. NET\ASP.NET 2.0 AJAX Extensions\v1.0.61025\MicrosoftAjaxLibrary\System.Web.Extensions\1.0.61025.0）以執行條件式測試（所謂的判斷提示），可確保參數正確地傳遞至函式，該物件包含預期的資料並寫入追蹤語句。

Sys.databases 類別會公開數個不同的函數，可用來處理追蹤、程式碼判斷提示或失敗，如 [表 1] 所示。

**[表 1]。Sys.databases 類別函式。**

| **函式名稱** | **說明** |
| --- | --- |
| assert （條件、訊息、displayCaller） | 判斷條件參數為 true 的判斷提示。 如果要測試的條件為 false，則會使用訊息方塊來顯示訊息參數值。 如果 displayCaller 參數為 true，此方法也會顯示呼叫端的相關資訊。 |
| clearTrace() | 清除追蹤作業的語句輸出。 |
| 失敗（訊息） | 導致程式停止執行，並中斷偵錯工具。 Message 參數可以用來提供失敗的原因。 |
| 追蹤（訊息） | 將 message 參數寫入追蹤輸出。 |
| traceDump （object，name） | 以可讀取的格式輸出物件的資料。 Name 參數可以用來提供追蹤傾印的標籤。 預設會寫出要傾印之物件內的任何子物件。 |

用戶端追蹤的使用方式與 ASP.NET 中可用的追蹤功能大致相同。 它可讓您輕鬆看到不同的訊息，而不會中斷應用程式的流程。 [清單 5] 顯示使用 Sys.databases 函數寫入追蹤記錄檔的範例。 此函式只會採用應該寫出做為參數的訊息。

**[清單 5]。使用 Sys.databases 函數。**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample6.js)]

如果您執行 [清單 5] 中顯示的程式碼，就不會在頁面中看到任何追蹤輸出。 若要查看此功能，唯一的方法是使用 Visual Studio .NET、Web 開發 Helper 或 Firebug 中提供的主控台視窗。 如果您想要在頁面中查看追蹤輸出，您必須加入 TextArea 標記並為其提供 TraceConsole 的識別碼，如下所示：

[!code-html[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample7.html)]

頁面中的任何 Sys.databases 語句都會寫入到 TraceConsole 區。

如果您想要查看包含在 JSON 物件中的資料，您可以使用 Sys.databases 類別的 traceDump 函數。 此函式採用兩個參數，包括應傾印到追蹤主控台的物件，以及可用於識別追蹤輸出中物件的名稱。 [清單 6] 顯示使用 traceDump 函數的範例。

**[清單 6]。使用 traceDump 函數。**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample8.js)]

[圖 11] 顯示呼叫 traceDump 函數的輸出。 請注意，除了寫出 Person 物件的資料外，它也會寫出位址子物件的資料。

除了追蹤，Sys.databases 類別也可以用來執行程式碼判斷提示。 判斷提示可用來測試應用程式在執行時是否符合特定條件。 ASP.NET AJAX 程式庫腳本的 debug 版本包含數個判斷提示語句，可用於測試各種不同的條件。

[清單 7] 顯示使用 Sys.databases 函數來測試條件的範例。 在更新 Person 物件之前，程式碼會測試位址物件是否為 null。

[traceDump 函數的 ![輸出。](understanding-asp-net-ajax-debugging-capabilities/_static/image32.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image31.png)

**圖 11**： traceDump 函數的輸出。  （[按一下以查看完整大小的影像](understanding-asp-net-ajax-debugging-capabilities/_static/image33.png)）

**[清單 7]。使用 debug. assert 函數。**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample9.js)]

傳遞了三個參數，包括要評估的條件、判斷提示傳回 false 時要顯示的訊息，以及是否應該顯示呼叫端的相關資訊。 在判斷提示失敗的情況下，如果第三個參數為 true，則會顯示訊息，以及呼叫端資訊。 [圖 12] 顯示在 [清單 7] 中顯示的判斷提示失敗時，所顯示的 [失敗] 對話方塊範例。

要涵蓋的最後一個函式是 Sys.databases. Debug。 fail。 當您想要強制程式碼在腳本中的特定行上失敗時，可以新增 Sys.databases，而不是 JavaScript 應用程式中通常使用的偵錯工具語句。 Sys.databases 函式會接受代表失敗原因的單一字串參數，如下所示：

[!code-css[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample10.css)]

[![Sys.databases 失敗訊息。](understanding-asp-net-ajax-debugging-capabilities/_static/image35.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image34.png)

**圖 12**： sys.databases 失敗訊息。  （[按一下以查看完整大小的影像](understanding-asp-net-ajax-debugging-capabilities/_static/image36.png)）

當腳本執行時遇到 Sys.databases 失敗語句時，message 參數的值將會顯示在 debug 應用程式的主控台中，例如 Visual Studio 2008，而且系統會提示您進行應用程式的偵錯工具。 當您無法在內嵌腳本上設定 Visual Studio 2008 的中斷點，但想要讓程式碼在特定行上停止，以便檢查變數的值時，這種情況會非常有用。

*瞭解 ScriptManager 控制項的 ScriptMode 屬性*

ASP.NET AJAX library 包含預設安裝于 C:\Program Files\Microsoft ASP. NET\ASP.NET 2.0 AJAX Extensions\v1.0.61025\MicrosoftAjaxLibrary\System.Web.Extensions\1.0.61025.0 的 debug 和 release 腳本版本。 Debug 腳本的格式正確、容易閱讀，而且有數個 Sys.databases。判斷提示會散佈在其中，而釋放腳本會移除空白字元，並謹慎使用 Sys.databases 類別，將其整體大小降到最低。

加入至 ASP.NET AJAX 頁面的 ScriptManager 控制項會讀取 web.config 中的編譯專案的 debug 屬性，以決定要載入的程式庫腳本版本。 不過，您可以藉由變更 ScriptMode 屬性來控制是否已載入 debug 或 release 腳本（程式庫腳本或您自己的自訂腳本）。 ScriptMode 會接受 ScriptMode 列舉，其成員包括 Auto、Debug、Release 和 Inherit。

ScriptMode 預設為 Auto 的值，這表示 ScriptManager 會檢查 web.config 中的 debug 屬性。當 debug 為 false 時，ScriptManager 會載入 ASP.NET AJAX library 腳本的發行版本。 當 debug 為 true 時，將會載入腳本的 debug 版本。 將 [ScriptMode] 屬性變更為 [發行] 或 [Debug]，將會強制 ScriptManager 載入適當的腳本，而不論 Debug 屬性在 web.config 中的值為何。[清單 8] 顯示使用 ScriptManager 控制項從 ASP.NET AJAX 程式庫載入偵錯工具腳本的範例。

[**清單 8]。使用 ScriptManager 載入調試腳本**。

[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample11.aspx)]

您也可以使用 ScriptManager 的 [腳本] 屬性以及 ScriptReference 元件（如 [清單 9] 所示），載入您自己的自訂腳本的不同版本（debug 或 release）。

**[清單 9]。使用 ScriptManager 載入自訂腳本。**

[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample12.aspx)]

> [!NOTE]
> 如果您要使用 ScriptReference 元件載入自訂腳本，您必須在腳本的底部新增下列程式碼，以在腳本完成載入時通知 ScriptManager：

[!code-csharp[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample13.cs)]

[清單 9] 所示的程式碼會告訴 ScriptManager 尋找 Person 腳本的 debug 版本，讓它自動尋找 Person，而不是 Person。 如果找不到. debug .js 檔案，將會引發錯誤。

如果您想要根據 ScriptManager 控制項上設定的 ScriptMode 屬性值來載入自訂腳本的 debug 或 release 版本，您可以將 ScriptReference 控制項的 ScriptMode 屬性設定為 [繼承]。 這會根據 ScriptManager 的 ScriptMode 屬性載入適當版本的自訂腳本，如 [清單 10] 所示。 由於 ScriptManager 控制項的 ScriptMode 屬性設定為 Debug，因此會在頁面中載入並使用 debug.exe 腳本。

**[清單 10]。從 ScriptManager 繼承自訂腳本的 ScriptMode。**

[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample14.aspx)]

適當地使用 ScriptMode 屬性，可讓您更輕鬆地對應用程式進行 debug 錯，並簡化整體流程。 ASP.NET AJAX 程式庫的版本腳本很容易逐步執行和閱讀，因為已移除程式碼格式設定，而將 debug 腳本特別用於進行調試。

## <a name="conclusion"></a>結論

Microsoft 的 ASP.NET AJAX 技術提供堅實的基礎，可讓您建立具備 AJAX 功能的應用程式，以增強使用者的整體體驗。 不過，與任何程式設計技術一樣，也一定會發生錯誤和其他應用程式問題。 瞭解可用的各種調試選項可以節省大量時間，並導致更穩定的產品。

在本文中，您已介紹了數種不同的技術來進行 ASP.NET AJAX 頁面的偵錯工具，包括包含 Visual Studio 2008、Web 開發 Helper 和 Firebug 的 Internet Explorer。 這些工具可以簡化整體的偵錯工具，因為您可以存取變數資料、逐行流覽程式碼，以及查看追蹤語句。 除了所討論的不同偵錯工具之外，您也會看到 ASP.NET AJAX 程式庫的 Sys.databases 類別如何在應用程式中使用，以及如何使用 ScriptManager 類別來載入腳本的 Debug 或 release 版本。

## <a name="bio"></a>生物

Dan Wahlin （Microsoft 最有價值的 ASP.NET 和 XML Web 服務專家）是 .NET 開發講師和架構顧問，位於介面技術訓練（[www.interfacett.com）](http://www.interfacett.com)。 Dan 成立了 XML for ASP.NET 開發人員網站（[www.XMLforASP.NET](http://www.XMLforASP.NET)），它是在 INETA 說話者的部門，並在幾場會議中發表。 Dan 共同撰寫的專業 Windows DNA （Wrox）、ASP.NET：秘訣、教學課程和程式碼（Sam）、ASP.NET 1.1 Insider 解決方案、Professional ASP.NET 2.0 AJAX （Wrox）、ASP.NET 2.0 MVP 的駭客和撰寫的 XML for ASP.NET 開發人員（Sam）。 當他不寫程式碼、文章或書籍時，Dan 就能在他的妻子和小孩中撰寫和錄製音樂，以及玩高爾夫球和籃球。

Scott Cate 自1997起開始使用 Microsoft Web 技術，而這是 myKB.com （[www.myKB.com](http://www.myKB.com)）的總裁，他專門撰寫以 ASP.NET 為基礎的應用程式，著重于知識庫軟體解決方案。 Scott 可以透過電子郵件聯絡，位於[scott.cate@myKB.com](mailto:scott.cate@myKB.com)或他的[ScottCate.com](http://ScottCate.com)的 blog

> [!div class="step-by-step"]
> [上一篇](understanding-asp-net-ajax-web-services.md)
