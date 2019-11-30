---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-vb
title: 使用 JavaScript 程式碼以動態方式填入控制項（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的 DynamicPopulate 控制項會呼叫 web 服務（或頁面方法），並將產生的值填滿至 t ... 的目標控制項
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 90582e54-3e90-432a-9da5-689fb39ed56b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-vb
msc.type: authoredcontent
ms.openlocfilehash: b2bd5b1571ccebc9baa501b29743aecdb4543fb2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599197"
---
# <a name="dynamically-populating-a-control-using-javascript-code-vb"></a>使用 JavaScript 程式碼以動態方式填入控制項 (VB)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.vb.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1VB.pdf)

> ASP.NET AJAX 控制項工具組中的 DynamicPopulate 控制項會呼叫 web 服務（或頁面方法），並將產生的值填滿頁面上的目標控制項中，而不需要重新整理頁面。 您也可以使用自訂用戶端 JavaScript 程式碼來觸發填入。

## <a name="overview"></a>概觀

ASP.NET AJAX 控制項工具組中的 `DynamicPopulate` 控制項會呼叫 web 服務（或頁面方法），並將產生的值填滿頁面上的目標控制項中，而不需要重新整理頁面。 您也可以使用自訂用戶端 JavaScript 程式碼來觸發填入。

## <a name="steps"></a>步驟

首先，您需要一個 ASP.NET Web 服務，它會執行由 `DynamicPopulateExtender` 控制項呼叫的方法。 Web 服務會執行方法 `getDate()`，預期會有一個字串類型的引數，稱為 `contextKey`，因為 `DynamicPopulate` 控制項會傳送一個內容資訊給每個 web 服務呼叫。 以下程式碼（file `DynamicPopulate.vb.asmx`）會以下列三種格式的其中一種來抓取目前的日期：

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample1.aspx)]

在下一個步驟中，建立新的 ASP.NET 網站，並開始使用 ASP.NET AJAX ScriptManager 控制項：

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample2.aspx)]

然後，新增標籤控制項（例如，使用相同名稱的 HTML 控制項或 `<asp:Label />` web 控制項），稍後會顯示 web 服務呼叫的結果。

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample3.aspx)]

接下來，包含一個 `DynamicPopulateExtender` 控制項，並提供 web 服務資訊、目標控制項，但不是觸發擴展的控制項名稱，這會在稍後使用自訂 JavaScript 來完成：

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample4.aspx)]

現在到 JavaScript 部分。 ASP.NET AJAX 程式庫所定義的 `$find()` 函式會傳回 ASP.NET AJAX 控制項工具組（例如 `DynamicPopulateExtender`）之伺服器端物件的參考。 在目前的檔案中，`$find("dpe")` 會在頁面中傳回一個 `DynamicPopulateExtender` 控制項的參考。 它會公開稱為 `populate()` 的方法，以觸發動態擴展進程。 `populate()` 方法需要一個引數：將作為 `getDate()` web 方法引數的內容索引鍵。 比方說，`$find("dpe").populate("format1")` 會在標籤中填入以月-日格式表示的目前日期。

為了讓範例更有彈性，使用者現在可以選擇數種日期格式。 其中每一項都會顯示一個選項按鈕。 一旦使用者按一下選項按鈕，JavaScript 程式碼就會以選取的日期格式動態填入標籤。 這些選項按鈕如下：

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample5.aspx)]

請注意，在選項按鈕的內容中，JavaScript 運算式 `this.value` 指的是目前按鈕的值，這剛好是 `getDate()` 方法可以使用的相同資訊。

[![按一下按鈕，就會以指定的格式從伺服器抓取日期](dynamically-populating-a-control-using-javascript-code-vb/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-vb/_static/image1.png)

按一下按鈕，就會以指定的格式（[按一下以查看完整大小的影像](dynamically-populating-a-control-using-javascript-code-vb/_static/image3.png)），從伺服器抓取日期

> [!div class="step-by-step"]
> [上一頁](dynamically-populating-a-control-vb.md)
> [下一頁](using-dynamicpopulate-with-a-user-control-and-javascript-vb.md)
