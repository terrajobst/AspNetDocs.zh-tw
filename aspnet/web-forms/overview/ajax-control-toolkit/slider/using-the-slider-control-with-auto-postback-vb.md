---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
title: 使用滑杆控制項搭配自動回傳（VB） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的滑杆控制項提供圖形滑杆，可以使用滑鼠來控制。 可以讓滑杆 autopost 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 41d1abba-97a5-4a45-9b44-d05624c19777
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
msc.type: authoredcontent
ms.openlocfilehash: e7a3286bcf7ca844f5dcfa4848c15e0bd4767c0f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78553561"
---
# <a name="using-the-slider-control-with-auto-postback-vb"></a>使用滑杆控制項搭配自動回傳（VB）

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)

> AJAX 控制項工具組中的滑杆控制項提供圖形滑杆，可以使用滑鼠來控制。 它的值變更後，可以讓滑杆 autopostback。

## <a name="overview"></a>概觀

AJAX 控制項工具組中的滑杆控制項提供圖形滑杆，可以使用滑鼠來控制。 它的值變更後，可以讓滑杆 autopostback。

## <a name="steps"></a>步驟

為了讓滑杆在變更時自動回傳，這兩個文字方塊都需要屬性 `AutoPostBack="true"`：將成為滑杆本身的文字方塊，以及保留滑杆位置的文字方塊。 以下是所需的標記：

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample1.aspx)]

ASP.NET AJAX 控制項工具組中的 `SliderExtender` 控制項，會將滑杆功能指派給這兩個文字方塊：

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample2.aspx)]

稍後會使用其他的 label 元素來通知使用者回傳：

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample3.aspx)]

最後，ASP.NET AJAX 的 `ScriptManager` 控制項會載入必要的 JavaScript，讓控制項工具組能夠正常執行：

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample4.aspx)]

現在滑杆回傳了;在伺服器端，此事件可能會被攔截並採取下列動作：

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample5.aspx)]

[移動滑杆的 ![會觸發回傳](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)

移動滑杆會觸發回傳（[按一下以觀看完整大小的影像](using-the-slider-control-with-auto-postback-vb/_static/image3.png)）

[![之後，這項變更的日期會寫入至標籤](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)

之後，這項變更的日期會寫入標籤（[按一下以查看完整大小的影像](using-the-slider-control-with-auto-postback-vb/_static/image6.png)）

> [!div class="step-by-step"]
> [上一頁](databinding-the-slider-control-cs.md)
> [下一頁](databinding-the-slider-control-vb.md)
