---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
title: 動態控制 UpdatePanel 動畫（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 適用于 ... 的內容
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 5138b8fe-98ff-4e73-a00b-e263fc3ff11d
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
msc.type: authoredcontent
ms.openlocfilehash: 183974564764aab9c0d8a4e577995f3c444bf2d3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536201"
---
# <a name="dynamically-controlling-updatepanel-animations-c"></a>以動態方式控制 UpdatePanel 動畫 (C#)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.cs.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2CS.pdf)

> ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 對於 UpdatePanel 的內容，有一個特殊的擴充項會高度依賴動畫架構： UpdatePanelAnimation。 它也可以搭配 UpdatePanel 觸發程式一起使用。

## <a name="overview"></a>概觀

ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 針對 `UpdatePanel`的內容，有一個特殊的擴充項會高度依賴動畫架構： `UpdatePanelAnimation`。 它也可以搭配 `UpdatePanel` 觸發程式一起使用。

## <a name="steps"></a>步驟

第一個步驟通常是在頁面中包含 `ScriptManager`，以便載入 ASP.NET AJAX 程式庫，並使用控制項工具組：

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample1.aspx)]

此案例中的動畫將會套用至目前時間的顯示。 您可以使用 `Page_Load()` 方法將這項資訊寫入標籤，或（為了簡單起見）使用下列內嵌程式碼：

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample2.aspx)]

此外，也會建立觸發更新時間的按鈕：

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample3.aspx)]

然後，此程式碼會放入 `UpdatePanel` 元素的 `<ContentTemplate>` 區段中。 面板的 [`UpdateMode`] 屬性必須設定為 [`"Conditional"`]，因為只有觸發程式可以更新面板的內容。 在 `UpdatePanel`的 [`<Triggers>`] 區段中，會建立異步回傳觸發程式，並將其系結至按鈕的 `Click` 事件。 因此，如果使用者按一下按鈕，就會重新整理 `UpdatePanel`。 以下是 `UpdatePanel` 控制項的標記：

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample4.aspx)]

最後，必須設定 `UpdatePanelAnimationExtender`：將 `TargetControlID` 屬性設為面板的識別碼，並在擴充項內定義動畫。 淡入有意義，這會在更新的時間建立美觀的視覺效果。 您的擴充項標記可能如下所示：

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample5.aspx)]

在瀏覽器中執行檔案。 當您按一下按鈕時，目前的時間會顯示在面板中，而在一秒的期間內，一律會淡入。

[![目前的時間漸淡](dynamically-controlling-updatepanel-animations-cs/_static/image2.png)](dynamically-controlling-updatepanel-animations-cs/_static/image1.png)

目前時間已淡入（[按一下以觀看完整大小的影像](dynamically-controlling-updatepanel-animations-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [上一頁](animating-an-updatepanel-control-cs.md)
> [下一頁](adding-animation-to-a-control-vb.md)
