---
title: 偵錯 Razor 元件
author: guardrex
description: 了解如何偵錯 Blazor 和 Razor 元件的應用程式。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/debug
ms.openlocfilehash: fb7ddcf3ae40ec28a372adf724a293b375be28a1
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57034115"
---
# <a name="debug-razor-components"></a>偵錯 Razor 元件

[Daniel Roth](https://github.com/danroth27)

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

Razor 元件有一些*初期*偵錯上 WebAssembly 在 Chrome 中執行的用戶端 Blazor 應用程式的支援。 雖然這個初始的偵錯支援非常有限且 unpolished，它會顯示基本的偵錯基礎結構，以組成。

若要在 Chrome 中的用戶端 Blazor 應用程式進行偵錯：

* 建置 Blazor 應用程式`Debug`組態 （未發行的應用程式的預設值）。
* 在 Chrome 中 （版本 70 （含） 更新版本） 執行 Blazor 應用程式。
* 具有鍵盤焦點，應用程式 （不是在開發人員工具面板，您可能必須關閉較不容易產生混淆的偵錯經驗） 上，選取下列 Blazor 特定鍵盤快速鍵：
  * `Shift+Alt+D` 在 Windows/Linux 上
  * `Shift+Cmd+D` 在 macOS 上

執行 Chrome 偵錯 Blazor 應用程式啟用遠端偵錯。 如果已停用遠端偵錯，Chrome 會產生錯誤頁面。 [錯誤] 頁面會包含執行 Chrome 偵錯的連接埠開啟，讓 Blazor 偵錯 proxy 可以連線到應用程式的指示。 *關閉所有 Chrome 執行個體*並重新啟動 Chrome 的指示。

![Blazor 偵錯錯誤頁面](https://user-images.githubusercontent.com/1874516/43123091-01ec0796-8ed8-11e8-844c-23b4e6e9d069.png)

當 Chrome 執行啟用遠端偵錯時，偵錯的鍵盤快速鍵會開啟新的偵錯工具索引標籤。隨後，*來源*索引標籤會顯示在應用程式的.NET 組件清單。 展開每個組件，然後尋找 *.cs*/*.cshtml*來源檔案可供偵錯。 設定中斷點，請切換至應用程式的索引標籤上和中斷點使用，會叫用。 在中斷點後會叫用，單一步驟 (`F10`) 或繼續 (`F8`) 正常。

![Blazor 偵錯](https://user-images.githubusercontent.com/1874516/43123060-efb0b3b0-8ed7-11e8-9ea5-97aa34247a0b.png)

Blazor 提供偵錯 proxy 實作[Chrome DevTools 通訊協定](https://chromedevtools.github.io/devtools-protocol/)和擴大使用的通訊協定。NET 特有的資訊。 偵錯的鍵盤快速鍵按下時，則 Blazor 會將 Chrome DevTools 指向 proxy。 Proxy 連接到您要搜尋偵錯的瀏覽器視窗 (因此您不必啟用遠端偵錯)。

您可能會好奇為什麼我們不只是要使用瀏覽器來源對應。 來源對應允許將編譯過的檔案對應回其原始程式檔的瀏覽器。 不過，未對應 BlazorC#直接向 JS/WASM （至少還沒有）。 但是，Blazor 會在瀏覽器中的 IL 解譯，因此來源對應不相關。

請注意，偵錯工具功能**非常有限**。 您目前只可以：

* 設定及移除中斷點。
* 逐步執行程式碼] 或 [繼續 (`F8`)。
* 在 *區域變數*顯示中出現的任何區域變數的型別值`int`， `string`，和`bool`。
* 查看呼叫堆疊，包括 javascript 移到.NET 的 JavaScript 和.NET 的呼叫鏈結。

您*無法*:

* 觀察到的值不是任何區域變數`int`， `string`，或`bool`。
* 觀察到的任何類別屬性或欄位的值。
* 若要查看其值的變數將滑鼠停留
* 評估運算式，在主控台中。
* 在非同步呼叫之間的步驟。
* 執行其他大部分的一般偵錯案例。

開發的進一步的偵錯案例是持續進行的重點工程團隊。

## <a name="troubleshooting-tip"></a>疑難排解秘訣

如果您執行錯誤，可能有助於下列提示：

在 **偵錯工具**索引標籤上，開啟 開發人員工具，請在瀏覽器中。 在主控台中，執行`localStorage.clear()`移除任何中斷點。
