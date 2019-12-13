---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
title: 調整 DropShadow 的 Z 索引（C#） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 DropShadow 控制項會擴充具有陰影的面板。 不過，此陰影有時會與其他控制項衝突，(.。。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 14133833-e518-4347-87b9-6b6f71f14a77
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
msc.type: authoredcontent
ms.openlocfilehash: 12bc7f0430f1f30ff964cd9547ee1e9b0aa7423c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574333"
---
# <a name="adjusting-the-z-index-of-a-dropshadow-c"></a>調整 DropShadow 的 Z 軸索引 (C#)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.cs.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1CS.pdf)

> AJAX 控制項工具組中的 DropShadow 控制項會擴充具有陰影的面板。 不過，此陰影有時會與其他控制項衝突，例如 [ASP.NET] 功能表控制項。 當功能表項目出現時，它會顯示在投影后方。

## <a name="overview"></a>總覽

AJAX 控制項工具組中的 DropShadow 控制項會擴充具有陰影的面板。 不過，此陰影有時會與其他控制項衝突，例如 [ASP.NET] 功能表控制項。 當功能表項目出現時，它會顯示在投影后方。

## <a name="steps"></a>步驟

程式碼會以面板本身開頭，其中包含足夠的文字，讓面板包含足夠的文字來顯示效果：

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample1.aspx)]

另一個面板會直接放在 `panelShadow` 面板之前。 它包含具有水準方向的功能表，因此功能表項目會出現在 [`dropShadow` 面板] 上方（或而不是：）：

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample2.aspx)]

然後，新增 `DropShadowExtender`，以使用投影效果擴充 `panelShadow` 面板：

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample3.aspx)]

最後，ASP.NET AJAX `ScriptManager` 控制項可讓控制工具組正常執行：

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample4.aspx)]

當您執行此腳本時，功能表項目會出現在面板底下。 不過，功能表會使用 CSS 類別 `panel` 您只需要定義兩個專案，讓元素出現在另一個面板的前方：

- 相對定位
- 正 z-索引

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample5.css)]

然後，`DropShadowExtender` 控制項不會與 Menu 控制項有任何較長的衝突。

[![之前：看不到功能表項目](adjusting-the-z-index-of-a-dropshadow-cs/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image1.png)

之前：看不到功能表項目（[按一下以觀看完整大小的影像](adjusting-the-z-index-of-a-dropshadow-cs/_static/image3.png)）

[![之後：功能表項目隨即出現](adjusting-the-z-index-of-a-dropshadow-cs/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image4.png)

之後：功能表項目隨即出現（[按一下以觀看完整大小的影像](adjusting-the-z-index-of-a-dropshadow-cs/_static/image6.png)）

> [!div class="step-by-step"]
> [下一步](manipulating-dropshadow-properties-from-client-code-cs.md)
