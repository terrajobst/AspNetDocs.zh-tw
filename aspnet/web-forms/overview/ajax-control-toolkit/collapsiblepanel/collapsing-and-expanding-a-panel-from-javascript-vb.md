---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
title: 從 JavaScript 折迭和展開面板（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的 CollapsiblePanel 控制項會擴充一個面板，並提供它可折迭其內容並將其展開的功能 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 298789b4-2964-49f5-a0a8-d4dbeb9ff2c2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: aa9779c65fb587193dbabde55cc6900283ce239d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78535844"
---
# <a name="collapsing-and-expanding-a-panel-from-javascript-vb"></a>從 JavaScript 摺疊與展開面板 (VB)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.vb.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1VB.pdf)

> ASP.NET AJAX 控制項工具組中的 CollapsiblePanel 控制項會擴充一個面板，並為它提供可折迭其內容並重新展開它的功能。 這兩個動作也可以從自訂 JavaScript 程式碼觸發。

## <a name="overview"></a>概觀

ASP.NET AJAX 控制項工具組中的 CollapsiblePanel 控制項會擴充一個面板，並為它提供可折迭其內容並重新展開它的功能。 這兩個動作也可以從自訂 JavaScript 程式碼觸發。

## <a name="steps"></a>步驟

首先，建立新的 ASP.NET 網頁，並在一個 `<form>` 元素內包含 `ScriptManager`。 這會載入控制項工具組所需的 ASP.NET AJAX 程式庫：

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample1.aspx)]

然後，建立具有一些文字的面板，以便看到折迭/展開效果：

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample2.aspx)]

如您所見，面板會參考此處顯示的 CSS 類別（基本上會定義背景色彩和麵板的寬度）：

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample3.css)]

`CollapsiblePanelExtender` 控制項需要 `TargetControlID` 屬性，讓工具組知道在要求時要折迭或展開哪個面板：

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample4.aspx)]

可惜的是，擴充專案前不會公開用於折迭或展開面板的特定 API，但是某些未記載的方法將會執行。 首先，將三個 HTML 按鈕新增至頁面，然後觸發用戶端 JavaScript 來折迭或展開面板的內容：

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample5.aspx)]

在用戶端 JavaScript 程式碼中（以 `<script type="text/javascript">`開始），必須使用 `$find()` 方法來存取 `CollapsiblePanelExtender`。 `$find("cpe")` 會傳回它的參考。 從這裡開始，特定方法將可解決手邊的工作。

開啟（展開）面板的方法會被呼叫 `_doOpen()`;下列程式碼會在按一下第一個按鈕時，執行呼叫的 `doOpen()` 函式：

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample6.js)]

若要關閉或折迭面板，必須執行 `_doClose()` 方法。 因此，當使用者按一下第二個按鈕時，會呼叫下列 JavaScript 程式碼：

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample7.js)]

第三個按鈕會切換面板的狀態：從折迭到展開，反之亦然。 `CollapsiblePanelExtender` 會公開 `toggle()` 方法，這完全是：反轉面板的狀態。 不過還有另一種方法（在內部由 `toggle()` 方法使用）： `CollapsiblePanelExtender()` 的 `get_Collapsed()` 方法會告訴我們面板是否已折迭。 根據此函數的傳回值，面板會展開（`_doOpen()` 方法）或折迭（`_doClose()`）方法：

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample8.js)]

[![第三個按鈕會變更面板的狀態：從 [已折迭] 到 [已展開] 和 [上一頁]](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image1.png)

第三個按鈕會變更面板的狀態：從 [折迭] 到 [已展開] 和 [上一頁] （[按一下以查看完整大小的影像](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一篇](collapsing-and-expanding-a-panel-from-javascript-cs.md)
