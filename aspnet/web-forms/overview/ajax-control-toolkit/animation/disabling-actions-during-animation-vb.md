---
uid: web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
title: 動畫期間停用動作（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 它也支援動作 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a86c0276-6481-46ee-8b4f-8c2009399ee9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
msc.type: authoredcontent
ms.openlocfilehash: 4924d4f70099255b930d53f6a72e810be7a47485
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536236"
---
# <a name="disabling-actions-during-animation-vb"></a>動畫播放期間停用動作 (VB)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.vb.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7VB.pdf)

> ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 它也支援動作，例如滑鼠點擊。 不過，當滑鼠按一下啟動動畫時，最好在動畫期間停用滑鼠點按動作。

## <a name="overview"></a>概觀

ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 它也支援動作，例如滑鼠點擊。 不過，當滑鼠按一下啟動動畫時，最好在動畫期間停用滑鼠點按動作。

## <a name="steps"></a>步驟

首先，在頁面中包含 `ScriptManager`;然後，會載入 ASP.NET AJAX 程式庫，讓您能夠使用控制項工具組：

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample1.aspx)]

動畫將會套用至 HTML 按鈕，如下所示：

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample2.aspx)]

請注意，HTML 控制項是用來取代 Web 控制項，因為我們不想要讓按鈕建立回傳。它應該只為我們啟動用戶端動畫。

然後，將 `AnimationExtender` 新增至頁面，並提供 `ID`、`TargetControlID` 屬性和必要 `runat="server"`：

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample3.aspx)]

在 [`<Animations>`] 節點內，`<OnClick>` 是用來處理滑鼠點按的右元素。 不過，在動畫期間也可以按一下按鈕。 `<EnableAction>` 元素可以處理這一點。 設定 `Enabled="false"` 會停用按鈕作為動畫的一部分。 由於我們使用數個個別的動畫（停用按鈕和實際的動畫），因此需要 `<Parallel>` 元素，將單一動畫一併放到一個。 以下是 `AnimationExtender`的完整標記：

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample4.aspx)]

您也可以使用清單結尾的下列 XML 元素，在動畫之後重新啟用 [到] 按鈕：

[!code-xml[Main](disabling-actions-during-animation-vb/samples/sample5.xml)]

不過在給定的案例中，這會很無用，因為按鈕會淡出，而且在動畫結束時看不到。

[![在動畫執行時立即停用按鈕](disabling-actions-during-animation-vb/_static/image2.png)](disabling-actions-during-animation-vb/_static/image1.png)

動畫執行時，按鈕會立即停用（[按一下以觀看完整大小的影像](disabling-actions-during-animation-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一頁](animating-in-response-to-user-interaction-vb.md)
> [下一頁](triggering-an-animation-in-another-control-vb.md)
