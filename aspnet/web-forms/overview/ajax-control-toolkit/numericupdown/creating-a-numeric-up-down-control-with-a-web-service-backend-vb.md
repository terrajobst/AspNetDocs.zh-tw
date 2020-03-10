---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
title: 使用 Web 服務後端建立數值向上/向下控制項（VB） |Microsoft Docs
author: wenz
description: 不是讓使用者在核取方塊中輸入值，而是數值的向上/向下控制項（存在於 Windows 和其他作業系統上）可以證明更多的 c 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: afa59dfa-fef1-43d3-8fdd-aea3be36ed3c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
msc.type: authoredcontent
ms.openlocfilehash: 2bf6e1b27180589d39e308de62b5be1f47fa8fe2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78612991"
---
# <a name="creating-a-numeric-updown-control-with-a-web-service-backend-vb"></a>使用 Web 服務後端建立數值向上/向下控制項 (VB)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.vb.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1VB.pdf)

> 不是讓使用者在核取方塊中輸入值，而是由數值向上/向下控制項（存在於 Windows 和其他作業系統上）可能會證明更舒適。 根據預設，NumericUpDown 控制項一律會增加或減少1的值，但 web 服務會證明更多的彈性。

## <a name="overview"></a>概觀

不是讓使用者在核取方塊中輸入值，而是由數值向上/向下控制項（存在於 Windows 和其他作業系統上）可能會證明更舒適。 根據預設，`NumericUpDown` 控制項一律會增加或減少1的值，但 web 服務會證明更多的彈性。

## <a name="steps"></a>步驟

ASP.NET AJAX 控制項工具組包含 `NumericUpDown` 擴充項，會自動將兩個按鈕加入文字方塊中：一個用於增加其值，一個用於減少。 不過，控制項也支援 web 服務呼叫（或頁面方法呼叫）。 只要按一下 [向上] 或 [向下] 按鈕，JavaScript 程式碼就會連接到 web 伺服器，並在該處執行方法。 方法簽章如下所示：

[!code-vb[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample1.vb)]

`current` 引數是文字方塊中的目前值;`tag` 屬性是其他內容資料，可設定為 `NumericUpDown` 擴充項的屬性（但非必要）。

針對此範例，數值向上/向下控制項只能允許兩個的冪值：1、2、4、8、16、32、64等等。 因此，當使用者想要增加值時，所執行的方法必須是舊值的兩倍;另一個方法必須將值除以二。 以下是完整的 web 服務：

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample2.aspx)]

最後，建立新的 ASP.NET 網頁。 如同往常，您需要一個 `ScriptManager` 控制項、一個 `TextBox` 控制項和一個 `NumericUpDownExtender` 控制項。 對於後者，您必須提供 web 服務資訊：

- 下層 web 方法或頁面方法的 `ServiceDownMethod` 名稱
- 具有向下服務方法的 web 服務 `ServiceDownPath` 路徑;如果您使用頁面方法，則省略
- up web 方法或 page 方法的 `ServiceUpMethod` 名稱
- 使用 up 服務方法 `ServiceUpPath` web 服務的路徑;如果您使用頁面方法，則省略

以下是頁面的完整標記：

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample3.aspx)]

如果您執行頁面，請注意文字方塊中的值在您按一下上方按鈕時，一律會加倍，而當您按一下下方按鈕時，則會減半。

[僅 ![出現2乘冪的數位](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image1.png)

只有2乘冪的數位才會出現（[按一下以觀看完整大小的影像](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一篇](creating-a-numeric-up-down-control-with-a-web-service-backend-cs.md)
