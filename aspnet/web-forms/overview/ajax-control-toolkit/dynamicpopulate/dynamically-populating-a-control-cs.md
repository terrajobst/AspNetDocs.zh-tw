---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-cs
title: 以動態方式填入控制項C#（） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的 DynamicPopulate 控制項會呼叫 web 服務（或頁面方法），並將產生的值填滿至 t ... 的目標控制項
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e1fec43e-1daf-49d2-b0c7-7f1b930455cc
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 24f88e44e0f878127314774d4e8846f80133413e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78535802"
---
# <a name="dynamically-populating-a-control-c"></a>以動態方式填入控制項 (C#)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.cs.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0CS.pdf)

> ASP.NET AJAX 控制項工具組中的 DynamicPopulate 控制項會呼叫 web 服務（或頁面方法），並將產生的值填滿頁面上的目標控制項中，而不需要重新整理頁面。

## <a name="overview"></a>概觀

ASP.NET AJAX 控制項工具組中的 `DynamicPopulate` 控制項會呼叫 web 服務（或頁面方法），並將產生的值填滿頁面上的目標控制項中，而不需要重新整理頁面。 本教學課程會示範如何進行這種設定。

## <a name="steps"></a>步驟

首先，您需要 ASP.NET Web 服務，以執行 `DynamicPopulate`所呼叫的方法。 Web 服務類別需要在 `Microsoft.Web.Script.Services`內定義的 `ScriptService` 屬性;否則，ASP.NET AJAX 就無法為 web 服務建立用戶端 JavaScript proxy，而這是 `DynamicPopulate`所需的。

Web 方法必須預期會有一個字串類型的引數，稱為 `contextKey`，因為 `DynamicPopulate` 控制項會使用每個 web 服務呼叫來傳送一段內容資訊。 下列 web 服務會以 `contextKey` 引數所代表的格式傳回目前的日期：

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample1.aspx)]

Web 服務接著會儲存為 `DynamicPopulate.cs.asmx`。 或者，您也可以使用 `DynamicPopulate` 控制項，將 `getDate()` 方法實作為實際 ASP.NET 網頁中的頁面方法。

在下一個步驟中，建立新的 ASP.NET 檔案。 一如往常，第一個步驟是將 `ScriptManager` 包含在目前的頁面中，以載入 ASP.NET AJAX 程式庫並讓控制項工具組正常執行：

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample2.aspx)]

然後，新增標籤控制項（例如，使用相同名稱的 HTML 控制項或 &lt;`asp:Label` /&gt; web 控制項），稍後會顯示 web 服務呼叫的結果。

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample3.aspx)]

HTML 按鈕（html 控制項，因為我們不需要回傳至伺服器）會接著用來觸發動態擴展：

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample4.aspx)]

最後，我們需要 `DynamicPopulateExtender` 控制項來連接東西。 下列屬性將會設定（除了明顯的屬性外，`ID` 和 `runat`=`"server"`）：

- `TargetControlID` 從 web 服務呼叫中放置結果的位置
- web 服務 `ServicePath` 路徑（如果您想要使用頁面方法，則省略）
- web 方法或頁面方法的 `ServiceMethod` 名稱
- 要傳送至 web 服務的 `ContextKey` 內容資訊
- 觸發 web 服務呼叫的 `PopulateTriggerControlID` 元素
- `ClearContentsDuringUpdate` 是否要在 web 服務呼叫期間清空目標元素

如您所見，控制項需要一些資訊，但將所有內容都放入原處非常簡單。 以下是目前案例中，`DynamicPopulateExtender` 控制項的標記：

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample5.aspx)]

執行瀏覽器中的 [ASP.NET] 頁面，然後按一下 [] 按鈕。您將會收到目前的日期，格式為 [月-日]。

[![按一下按鈕，就會從伺服器抓取日期](dynamically-populating-a-control-cs/_static/image2.png)](dynamically-populating-a-control-cs/_static/image1.png)

按一下按鈕，就會從伺服器抓取日期（[按一下以查看完整大小的影像](dynamically-populating-a-control-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [下一個](dynamically-populating-a-control-using-javascript-code-cs.md)
