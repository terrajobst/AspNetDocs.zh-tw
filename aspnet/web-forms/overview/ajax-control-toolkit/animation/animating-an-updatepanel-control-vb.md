---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
title: 製作 UpdatePanel 控制項的動畫（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 適用于 ... 的內容
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4c306a2c-92b6-4904-b70b-365b847334fe
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
msc.type: authoredcontent
ms.openlocfilehash: d66dda923940a328c0757049c9d8bfa3b2d2b9fc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536334"
---
# <a name="animating-an-updatepanel-control-vb"></a>繪製 UpdatePanel 控制項的動畫 (VB)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.vb.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1VB.pdf)

> ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 對於 UpdatePanel 的內容，有一個特殊的擴充項會高度依賴動畫架構： UpdatePanelAnimation。 本教學課程說明如何設定 UpdatePanel 的這類動畫。

## <a name="overview"></a>概觀

ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 針對 `UpdatePanel`的內容，有一個特殊的擴充項會高度依賴動畫架構： `UpdatePanelAnimation`。 本教學課程說明如何設定 `UpdatePanel`的動畫。

## <a name="steps"></a>步驟

第一個步驟通常是在頁面中包含 `ScriptManager`，以便載入 ASP.NET AJAX 程式庫，並使用控制項工具組：

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample1.aspx)]

此案例中的動畫將會套用至位於 `UpdatePanel`的 ASP.NET `Wizard` web 控制項。 三個（任意）步驟提供足夠的選項來觸發回傳：

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample2.aspx)]

`UpdatePanelAnimationExtender` 控制項所需的標記與用於 `AnimationExtender`的標記非常類似。 在 [`TargetControlID`] 屬性中，我們提供 `UpdatePanel` 的 `ID` 以建立動畫;在 `UpdatePanelAnimationExtender` 控制項內，`<Animations>` 元素會保存動畫的 XML 標記。 不過，有一項差異：事件和事件處理常式的數量會與 `AnimationExtender`相較之下受到限制。 針對 `UpdatePanels`，其中只有兩個存在：

- 當 UpdatePanel 已更新時 `<OnUpdated>`
- 當 UpdatePanel 開始更新時 `<OnUpdating>`

在此案例中，`UpdatePanel` 的新內容（在回傳之後）應會淡入。 這是所需的標記：

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample3.aspx)]

現在，每當 UpdatePanel 中出現回傳時，面板的新內容就會順暢地淡入。

[![下一個 wizard 步驟會淡入](animating-an-updatepanel-control-vb/_static/image2.png)](animating-an-updatepanel-control-vb/_static/image1.png)

下一個 wizard 步驟已淡入（[按一下以觀看完整大小的影像](animating-an-updatepanel-control-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一頁](changing-an-animation-using-client-side-code-vb.md)
> [下一頁](dynamically-controlling-updatepanel-animations-vb.md)
