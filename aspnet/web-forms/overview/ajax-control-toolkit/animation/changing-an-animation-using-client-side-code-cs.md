---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
title: 使用用戶端程式代碼變更動畫（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 動畫也可以 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2bfbc5cc-f942-44b7-a62d-a29520f1da9a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 84fc2d6646b89cfabb2193cdfca59462d6d7ef16
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606960"
---
# <a name="changing-an-animation-using-client-side-code-c"></a>使用用戶端程式碼變更動畫 (C#)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)

> ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 您也可以使用自訂用戶端 JavaScript 程式碼來變更動畫。

## <a name="overview"></a>概觀

ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 您也可以使用自訂用戶端 JavaScript 程式碼來變更動畫。

## <a name="steps"></a>步驟

首先，在頁面中包含 `ScriptManager`;然後，會載入 ASP.NET AJAX 程式庫，讓您能夠使用控制項工具組：

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample1.aspx)]

動畫將會套用至文字的面板，如下所示：

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample2.aspx)]

在面板的相關聯 CSS 類別中，定義良好的背景色彩，同時設定面板的固定寬度：

[!code-css[Main](changing-an-animation-using-client-side-code-cs/samples/sample3.css)]

實際的動畫是由 HTML 按鈕啟動：

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample4.aspx)]

然後，將 `AnimationExtender` 新增至頁面，並提供 `ID`、`TargetControlID` 屬性和必要 `runat="server"`：

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample5.aspx)]

請注意，`AnimationExtender` 控制項內沒有 `<Animations>` 節點。 自訂 JavaScript 程式碼是用來提供要與控制項搭配使用的動畫。

就像 `AnimationExtender`的伺服器 API 一樣，也沒有簡單的方法可以將動畫指派給擴充項。 不過，擴充項會公開數個方法來讀取和寫入以各種事件（`OnClick`、`OnLoad`等等）註冊的動畫。 以下是一些範例：

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

`get_*()` 函式的傳回值格式和 `set_*()` 函數的引數格式為 JSON 字串，提供 XML 標記的物件標記法。 目前，沒有任何方法可以在中傳遞物件，但可以從指定的動畫（`get_OnXXXBehavior()` 方法）讀取物件。

以下是 JSON 字串（不含分隔的引號和格式），代表按鈕所觸發的動畫，但會以動畫顯示面板的方式來調整其大小，並同時淡出它：

[!code-json[Main](changing-an-animation-using-client-side-code-cs/samples/sample6.json)]

下列 JavaScript 程式碼會將此 JSON descripting 指派給目前擴充項的 `OnClick` 動畫，並加以執行：

[!code-html[Main](changing-an-animation-using-client-side-code-cs/samples/sample7.html)]

[![動畫立即執行，而不需按下滑鼠（且標記非常少）](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)

動畫會立即執行，而不需要按一下滑鼠（而且標記很少）（[按一下即可觀看完整大小的影像](changing-an-animation-using-client-side-code-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [上一頁](executing-animations-using-client-side-code-cs.md)
> [下一頁](animating-an-updatepanel-control-cs.md)
