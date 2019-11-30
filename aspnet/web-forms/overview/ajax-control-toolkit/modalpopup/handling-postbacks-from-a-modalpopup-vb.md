---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
title: 處理來自 ModalPopup 的回傳（VB） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 ModalPopup 控制項提供一個簡單的方式，讓您使用用戶端的方法來建立強制回應快顯視窗。 當 pos 時，必須特別注意
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f70ac2b3-900f-40fa-858f-ab057904506b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: df0b71b3e336a0d230869623473bdac24b3dd07b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606644"
---
# <a name="handling-postbacks-from-a-modalpopup-vb"></a>處理來自 ModalPopup 的回傳 (VB)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.vb.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3VB.pdf)

> AJAX 控制項工具組中的 ModalPopup 控制項提供一個簡單的方式，讓您使用用戶端的方法來建立強制回應快顯視窗。 從快顯視窗內建立回傳時，必須特別小心。

## <a name="overview"></a>概觀

AJAX 控制項工具組中的 ModalPopup 控制項提供一個簡單的方式，讓您使用用戶端的方法來建立強制回應快顯視窗。 從快顯視窗內建立回傳時，必須特別小心。

## <a name="steps"></a>步驟

若要啟用 ASP.NET AJAX 和控制項工具組的功能，`ScriptManager` 控制項必須放在頁面上的任何位置（但在 `<form>` 元素內）：

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample1.aspx)]

接下來，新增可作為強制回應快顯視窗的面板。 使用者可以在那裡輸入名稱和電子郵件地址。 按鈕可用來關閉快顯視窗並儲存資訊。 請注意，[`OnClick`] 屬性已設定為按一下這個按鈕時，就會發生回傳：

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample2.aspx)]

頁面本身包含兩個標籤，以取得完全相同的資訊：名稱和電子郵件地址。 按鈕可用來觸發強制回應快顯視窗：

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample3.aspx)]

若要顯示快顯視窗，請加入 `ModalPopupExtender` 控制項。 將 `PopupControlID` 屬性設為面板的識別碼，並 `TargetControlID` 至按鈕的識別碼：

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample4.aspx)]

現在只要按一下強制回應快顯視窗中的 [`Save`] 按鈕，就會執行伺服器端 `SaveData()` 方法。 在這裡，您可以將輸入的資料儲存在資料存放區中。 為了簡單起見，新資料只會輸出在標籤中：

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample5.vb)]

此外，強制回應快顯視窗中的 textbox 控制項應該填入目前的名稱和電子郵件。 不過，只有在沒有發生回傳時，才需要這麼做。 如果有回傳，ASP.NET viewstate 功能會自動以適當的值填滿文字方塊。

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample6.vb)]

[![強制回應快顯視窗會導致回傳](handling-postbacks-from-a-modalpopup-vb/_static/image2.png)](handling-postbacks-from-a-modalpopup-vb/_static/image1.png)

強制回應快顯視窗會導致回傳（[按一下以查看完整大小的影像](handling-postbacks-from-a-modalpopup-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一頁](using-modalpopup-with-a-repeater-control-vb.md)
> [下一頁](positioning-a-modalpopup-vb.md)
