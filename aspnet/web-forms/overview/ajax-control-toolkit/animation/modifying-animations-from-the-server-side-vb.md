---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
title: 從伺服器端修改動畫（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 動畫也可能是 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: addcf4aa-340a-460b-9c64-506424a1f725
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
msc.type: authoredcontent
ms.openlocfilehash: ebc311d1a931ad611d9556799c94440d41a9cf49
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78597997"
---
# <a name="modifying-animations-from-the-server-side-vb"></a>從伺服器端修改動畫（VB）

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)

> ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 伺服器端上的動畫也可能會變更

## <a name="overview"></a>概觀

ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 伺服器端上的動畫也可能會變更

## <a name="steps"></a>步驟

首先，在頁面中包含 `ScriptManager`;然後，會載入 ASP.NET AJAX 程式庫，讓您能夠使用控制項工具組：

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample1.aspx)]

動畫將會套用至文字的面板，如下所示：

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample2.aspx)]

在面板的相關聯 CSS 類別中，定義良好的背景色彩，同時設定面板的固定寬度：

[!code-css[Main](modifying-animations-from-the-server-side-vb/samples/sample3.css)]

其餘的程式碼會在伺服器端執行，而且不會使用標記;相反地，它會使用程式碼來建立 `AnimationExtender` 控制項：

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample4.aspx)]

不過，控制項工具組目前並未提供 API 存取權來建立個別的動畫。 不過，您可以將 `AnimationExtender`的動畫屬性設定為字串，其中包含以宣告方式指派動畫時所使用的 XML 標記。 若要建立不能包含 `<Animations>` 元素的 XML，您可以使用 .NET Framework 的 XML 支援或，如下列程式碼所示，只需提供字串：

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample5.vb)]

最後，將 `AnimationExtender` 控制項加入至目前頁面的 `<form runat="server">` 元素內，確保動畫已包含並執行：

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample6.vb)]

[![使用伺服器端C#/VB 程式碼建立動畫](modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)

動畫是使用伺服器端C#的/VB 程式碼（[按一下以查看完整大小的影像](modifying-animations-from-the-server-side-vb/_static/image3.png)）所建立

> [!div class="step-by-step"]
> [上一頁](triggering-an-animation-in-another-control-vb.md)
> [下一頁](executing-animations-using-client-side-code-vb.md)
