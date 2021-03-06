---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
title: 資料系結滑杆控制項（VB） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的滑杆控制項提供圖形滑杆，可以使用滑鼠來控制。 您可以系結目前的 positio 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4f3ba53f-d166-422d-b29c-403348057836
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 9c14373bdfdead9916950b8a1cf61f427f7ba50b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78627215"
---
# <a name="databinding-the-slider-control-vb"></a>資料繫結滑桿控制項 (VB)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.vb.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0VB.pdf)

> AJAX 控制項工具組中的滑杆控制項提供圖形滑杆，可以使用滑鼠來控制。 您可以將滑杆的目前位置系結至另一個 ASP.NET 控制項。

## <a name="overview"></a>概觀

AJAX 控制項工具組中的滑杆控制項提供圖形滑杆，可以使用滑鼠來控制。 您可以將滑杆的目前位置系結至另一個 ASP.NET 控制項。

## <a name="steps"></a>步驟

若要啟用 ASP.NET AJAX 和控制項工具組的功能，`ScriptManager` 控制項必須放在頁面上的任何位置（但在 `<form>` 元素內）：

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample1.aspx)]

接下來，將兩個 `TextBox` 控制項加入至頁面。 其中一個會轉換成圖形滑杆，另一個則會保存滑杆的位置。

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample2.aspx)]

下一個步驟已經是最後一個步驟。 ASP.NET AJAX 控制項工具組中的 `SliderExtender` 控制項會從第一個文字方塊移出一個滑杆，並在滑杆位置變更時自動更新第二個文字方塊。 `SliderExtender`的 `TargetControlID` 屬性必須設定為第一個文字方塊的識別碼，才能正常操作。`BoundControlID` 屬性必須設定為第二個文字方塊的識別碼。

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample3.aspx)]

如您在瀏覽器中所見，資料系結會雙向運作：在文字方塊中輸入新的值會更新滑杆的位置。 如果您將第二個文字方塊設為唯讀，您可以在文字欄位中加入弱式保護，讓使用者更難以手動更新該處的值。

[![滑杆和文字方塊已同步](databinding-the-slider-control-vb/_static/image2.png)](databinding-the-slider-control-vb/_static/image1.png)

滑杆和文字方塊已同步（[按一下以觀看完整大小的影像](databinding-the-slider-control-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一篇](using-the-slider-control-with-auto-postback-vb.md)
