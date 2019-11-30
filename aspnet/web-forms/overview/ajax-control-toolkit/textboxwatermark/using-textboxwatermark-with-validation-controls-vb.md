---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
title: 使用 TextBoxWatermark 與驗證控制項（VB） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 TextBoxWatermark 控制項會擴充一個文字方塊，讓文字顯示在方塊中。 當使用者按一下方塊時，我 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e6c2cb98-f745-4bc8-973a-813879c8a891
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 141cae26c9e52be510e2a5a8f816cbac977dcf3d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74597250"
---
# <a name="using-textboxwatermark-with-validation-controls-vb"></a>使用 TextBoxWatermark 與驗證控制項 (VB)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.vb.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2VB.pdf)

> AJAX 控制項工具組中的 TextBoxWatermark 控制項會擴充一個文字方塊，讓文字顯示在方塊中。 當使用者按一下方塊時，就會清空。 如果使用者離開方塊而不輸入文字，預先填入的文字就會重新出現。 這可能會與相同頁面上的 ASP.NET 驗證控制項衝突，但這些問題可能會受到克服。

## <a name="overview"></a>概觀

AJAX 控制項工具組中的 `TextBoxWatermark` 控制項會擴充一個文字方塊，讓文字顯示在方塊中。 當使用者按一下方塊時，就會清空。 如果使用者離開方塊而不輸入文字，預先填入的文字就會重新出現。 這可能會與相同頁面上的 ASP.NET 驗證控制項衝突，但這些問題可能會受到克服。

## <a name="steps"></a>步驟

範例的基本設定如下所示：使用 `TextBoxWatermarkExtender` 控制項浮水印 `TextBox` 控制項。 按鈕會觸發回傳，稍後會用來觸發頁面上的驗證控制項。 此外，也需要 `ScriptManager` 控制項來初始化 ASP.NET AJAX：

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample1.aspx)]

現在加入一個 `RequiredFieldValidator` 控制項，它會在提交表單時，檢查欄位中是否有文字。 驗證程式的 `InitialValue` 屬性必須設定為 `TextBoxWatermarkExtender` 控制項中所使用的相同值：提交表單時，未變更的文字方塊值是其中的浮水印值：

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample2.aspx)]

不過，此方法有一個問題：如果用戶端停用 JavaScript，則文字欄位不會預先填入浮水印文字，因此 `RequiredFieldValidator` 不會觸發錯誤訊息。 因此，需要第二個 `RequiredFieldValidator` 控制項，以檢查空的文字方塊（省略 `InitialValue` 屬性）。

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample3.aspx)]

由於這兩個驗證程式都是使用 `Display`=`"Dynamic"`，因此使用者無法區別兩個驗證程式引發的視覺外觀;相反地，它似乎只有其中一個。

最後，新增一些伺服器端程式碼，以便在沒有驗證器發出錯誤訊息時，輸出欄位中的文字：

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample4.aspx)]

[![驗證程式抱怨欄位中沒有文字](using-textboxwatermark-with-validation-controls-vb/_static/image2.png)](using-textboxwatermark-with-validation-controls-vb/_static/image1.png)

驗證程式抱怨欄位中沒有文字（[按一下以查看完整大小的影像](using-textboxwatermark-with-validation-controls-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一篇](using-textboxwatermark-in-a-formview-vb.md)
