---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
title: 使用用戶端程式代碼執行動畫（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 動畫執行中 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0270e0df-6fde-4a8f-a2cb-2cacc55143f2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: b6ba1553b9c8c51d5d6ae1679e53f9cc1d17b769
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599646"
---
# <a name="executing-animations-using-client-side-code-c"></a>使用用戶端程式碼執行動畫 (C#)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.cs.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10CS.pdf)

> ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 也可以使用自訂用戶端 JavaScript 程式碼觸發動畫執行。

## <a name="overview"></a>概觀

ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 也可以使用自訂用戶端 JavaScript 程式碼觸發動畫執行。

## <a name="steps"></a>步驟

首先，在頁面中包含 `ScriptManager`;然後，會載入 ASP.NET AJAX 程式庫，讓您能夠使用控制項工具組：

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample1.aspx)]

動畫將會套用至文字的面板，如下所示：

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample2.aspx)]

在面板的相關聯 CSS 類別中，定義良好的背景色彩，同時設定面板的固定寬度：

[!code-css[Main](executing-animations-using-client-side-code-cs/samples/sample3.css)]

然後，將 `AnimationExtender` 新增至頁面，並提供 `ID`、`TargetControlID` 屬性和必要 `runat="server"`：

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample4.aspx)]

在 [`<Animations>`] 節點中，當使用者按一下面板後，使用 `<OnClick>` 來執行動畫。 新增要平行執行的兩個動畫：

[!code-xml[Main](executing-animations-using-client-side-code-cs/samples/sample5.xml)]

為了示範，這個動畫（以及使用控制項工具組所建立的任何其他動畫）會在頁面執行之後，使用 JavaScript 程式碼執行。 首先，我們需要 `AnimationExtender` 控制項的存取權。 ASP.NET AJAX 程式庫提供這項工作的 `$find()` 函式：

[!code-csharp[Main](executing-animations-using-client-side-code-cs/samples/sample6.cs)]

`AnimationExtender` 控制項會公開豐富的 API，包括名稱與 XML 標記中所用事件處理常式相同的方法： `OnClick()`、`OnLoad()`等等。 例如，`OnClick()` 方法的呼叫會在 `AnimationExtender` 控制項的 `<OnClick>` 元素內執行動畫：

[!code-javascript[Main](executing-animations-using-client-side-code-cs/samples/sample7.js)]

以下是完整載入頁面後，會模擬面板上按一下的完整用戶端 JavaScript 程式碼，請注意 `pageLoad()`，ASP.NET AJAX 會在頁面上載入所有包含的 JavaScript 程式庫之後，使用此名稱來呼叫。

[!code-html[Main](executing-animations-using-client-side-code-cs/samples/sample8.html)]

[![動畫立即執行，而不需按滑鼠按鍵](executing-animations-using-client-side-code-cs/_static/image2.png)](executing-animations-using-client-side-code-cs/_static/image1.png)

動畫會立即執行，而不需要按一下滑鼠（[按一下以觀看完整大小的影像](executing-animations-using-client-side-code-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [上一頁](modifying-animations-from-the-server-side-cs.md)
> [下一頁](changing-an-animation-using-client-side-code-cs.md)
