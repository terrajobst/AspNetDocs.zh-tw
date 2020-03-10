---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
title: 從用戶端程式代碼操作 DropShadowC#屬性（） |Microsoft Docs
author: wenz
description: 自訂 DataList 的編輯介面
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c83ca3e6-c0bf-4158-a166-40c1ab0f33da
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 790f0d881e43518600968d6c175d4eaa53d0e5f9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613817"
---
# <a name="manipulating-dropshadow-properties-from-client-code-c"></a>從用戶端程式碼操作 DropShadow 屬性 (C#)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.cs.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2CS.pdf)

> AJAX 控制項工具組中的 DropShadow 控制項會擴充具有陰影的面板。 這個擴充項的屬性也可以使用用戶端 JavaScript 程式碼進行變更。

## <a name="overview"></a>概觀

AJAX 控制項工具組中的 DropShadow 控制項會擴充具有陰影的面板。 這個擴充項的屬性也可以使用用戶端 JavaScript 程式碼進行變更。

## <a name="steps"></a>步驟

程式碼會以包含一些文字的面板作為開頭：

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample1.aspx)]

相關聯的 CSS 類別讓面板具有良好的背景色彩：

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample2.css)]

新增 `DropShadowExtender` 以擴充具有投影效果的面板，不透明度設定為50%：

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample3.aspx)]

然後，ASP.NET AJAX `ScriptManager` 控制項可讓控制工具組正常執行：

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample4.aspx)]

另一個面板包含兩個 JavaScript 連結，用於設定陰影的不透明度：減號連結會減少陰影的不透明度，加號連結則會增加。

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample5.aspx)]

JavaScript 函數 `changeOpacity()` 接著必須先在頁面上尋找 `DropShadowExtender` 控制項。 ASP.NET AJAX 只會針對該工作定義 `$find()` 方法。 然後，`get_Opacity()` 方法會抓取目前的不透明度，`set_Opacity()` 方法會加以設定。 然後，JavaScript 程式碼會將目前的不透明度值放在 `<label>` 元素中：

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample6.html)]

[![用戶端上的不透明度已變更](manipulating-dropshadow-properties-from-client-code-cs/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-cs/_static/image1.png)

用戶端上的不透明度已變更（[按一下以觀看完整大小的影像](manipulating-dropshadow-properties-from-client-code-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [上一頁](adjusting-the-z-index-of-a-dropshadow-cs.md)
> [下一頁](adjusting-the-z-index-of-a-dropshadow-vb.md)
