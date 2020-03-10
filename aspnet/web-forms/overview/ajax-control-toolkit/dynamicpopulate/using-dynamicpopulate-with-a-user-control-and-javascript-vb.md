---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
title: 使用 DynamicPopulate 搭配使用者控制項和 JavaScript （VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的 DynamicPopulate 控制項會呼叫 web 服務（或頁面方法），並將產生的值填滿至 t ... 的目標控制項
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 778b9009-76f2-4665-940e-afc0e35bc917
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: ee5923ad6d8b101f689a0564aef8b1e0e00a7639
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613670"
---
# <a name="using-dynamicpopulate-with-a-user-control-and-javascript-vb"></a>使用具有使用者控制項的 DynamicPopulate 和 JavaScript (VB)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.vb.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2VB.pdf)

> ASP.NET AJAX 控制項工具組中的 DynamicPopulate 控制項會呼叫 web 服務（或頁面方法），並將產生的值填滿頁面上的目標控制項中，而不需要重新整理頁面。 您也可以使用自訂用戶端 JavaScript 程式碼來觸發填入。 不過，當擴充項位於使用者控制項時，必須特別小心。

## <a name="overview"></a>概觀

ASP.NET AJAX 控制項工具組中的 `DynamicPopulate` 控制項會呼叫 web 服務（或頁面方法），並將產生的值填滿頁面上的目標控制項中，而不需要重新整理頁面。 您也可以使用自訂用戶端 JavaScript 程式碼來觸發填入。 不過，當擴充項位於使用者控制項時，必須特別小心。

## <a name="steps"></a>步驟

首先，您需要一個 ASP.NET Web 服務，它會執行由 `DynamicPopulateExtender` 控制項呼叫的方法。 Web 服務會執行方法 `getDate()`，預期會有一個字串類型的引數，稱為 `contextKey`，因為 `DynamicPopulate` 控制項會傳送一個內容資訊給每個 web 服務呼叫。 以下程式碼（files `DynamicPopulate.vb.asmx`）會以下列三種格式的其中一種來抓取目前的日期：

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample1.aspx)]

在下一個步驟中，建立新的使用者控制項（`.ascx` 檔案），並在第一行中以下列宣告表示：

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample2.aspx)]

&lt;`label`&gt; 元素將用來顯示來自伺服器的資料。

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample3.aspx)]

此外，在使用者控制項檔案中，我們會使用三個選項按鈕，分別代表 web 服務支援的三種可能日期格式之一。 當使用者按一下其中一個選項按鈕時，瀏覽器將會執行 JavaScript 程式碼，如下所示：

[!code-powershell[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample4.ps1)]

此程式碼會存取 `DynamicPopulateExtender` （不擔心奇怪的識別碼，這將于稍後說明），並使用資料觸發動態擴展。 在目前選項按鈕的內容中，`this.value` 指的是 `format1`、`format2` 或 `format3` web 方法所預期的值。

使用者控制項中唯一缺少的東西，就是將選項按鈕連結至 web 服務的 `DynamicPopulateExtender` 控制項。

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample5.aspx)]

同樣地，您可能會注意到控制項中使用的奇怪識別碼： `mcd1$myDate`，而不是 `myDate`。 先前，用來 `mcd1_dpe1` 的 JavaScript 程式碼可存取 `DynamicPopulateExtender`，而不是 `dpe1`。此命名策略是在使用者控制項中使用 `DynamicPopulateExtender` 時的特殊需求。 此外，您必須以特定方式內嵌使用者控制項，才能讓它進行所有工作。 建立新的 ASP.NET 網頁，並為您剛執行的使用者控制項註冊標記前置詞：

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample6.aspx)]

然後，在新的頁面上包含 ASP.NET AJAX `ScriptManager` 控制項：

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample7.aspx)]

最後，將使用者控制項加入至頁面。 您只需要設定其 `ID` 屬性（當然也 `runat="server"`），但您也必須將它設定為特定名稱： `mcd1`，因為這是使用者控制項內用來使用 JavaScript 來存取它的前置詞。

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample8.aspx)]

就是這麼容易！ 頁面會如預期般運作：使用者按一下其中一個選項按鈕，工具組中的控制項就會呼叫 web 服務，並以所需的格式顯示目前的日期。

[![選項按鈕位於使用者控制項中](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image1.png)

選項按鈕位於使用者控制項（[按一下以查看完整大小的影像](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一篇](dynamically-populating-a-control-using-javascript-code-vb.md)
