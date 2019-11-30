---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
title: 將動畫新增至控制項（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 本教學課程顯示如何 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0f1fc1f5-9dbd-44e7-931e-387d42f0342b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
msc.type: authoredcontent
ms.openlocfilehash: dd63157fe616c5f6874b7cca11f4ede15018df04
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607134"
---
# <a name="adding-animation-to-a-control-c"></a>將動畫新增至控制項 (C#)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)

> ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 本教學課程說明如何設定這種動畫。

## <a name="overview"></a>概觀

ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 本教學課程說明如何設定這種動畫。

## <a name="steps"></a>步驟

第一個步驟通常是在頁面中包含 `ScriptManager`，以便載入 ASP.NET AJAX 程式庫，並使用控制項工具組：

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample1.aspx)]

此案例中的動畫將會套用至文字的面板，如下所示：

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample2.aspx)]

面板的相關聯 CSS 類別會定義背景色彩和寬度：

[!code-css[Main](adding-animation-to-a-control-cs/samples/sample3.css)]

接下來，我們需要 `AnimationExtender`。 在提供 `ID` 和一般的 `runat="server"`之後，必須將 `TargetControlID` 屬性設定為控制項，以便在我們的案例中以動畫顯示（panel）：

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample4.aspx)]

整個動畫會使用 XML 語法以宣告方式套用，但目前並不完全支援 Visual Studio 的 IntelliSense。 根節點在此節點中 `<Animations>;`，允許數個事件來判斷動畫的執行時間：

- `OnClick` （滑鼠按一下）
- `OnHoverOut` （當滑鼠離開控制項時）
- `OnHoverOver` （當滑鼠停留在控制項上時，停止 `OnHoverOut` 動畫）
- `OnLoad` （載入頁面時）
- `OnMouseOut` （當滑鼠離開控制項時）
- `OnMouseOver` （當滑鼠停留在控制項上時，不會停止 `OnMouseOut` 動畫）

此架構隨附一組動畫，每一個都由自己的 XML 元素表示。 選擇如下：

- `<Color>` （變更色彩）
- `<FadeIn>` （淡入）
- `<FadeOut>` （淡出）
- `<Property>` （變更控制項的屬性）
- `<Pulse>` （pulsating）
- `<Resize>` （變更大小）
- `<Scale>` （按比例變更大小）

在此範例中，面板應淡出。動畫應需要1.5 秒（`Duration` 屬性），顯示每秒24個畫面格（動畫步驟）（`Fps` 屬性）。 以下是 `AnimationExtender` 控制項的完整標記：

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample5.aspx)]

當您執行此腳本時，會顯示面板並淡出一段半秒。

[![面板會淡出](adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)

此面板會淡出（[按一下以觀看完整大小的影像](adding-animation-to-a-control-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [下一步](executing-several-animations-at-the-same-time-cs.md)
