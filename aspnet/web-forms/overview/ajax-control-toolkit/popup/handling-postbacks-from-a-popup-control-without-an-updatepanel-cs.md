---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
title: 處理沒有 UpdatePanel 的快顯視窗控制項回傳（C#） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 PopupControl 擴充項提供了一種簡單的方式，可在啟用任何其他控制項時觸發快顯。 當 su 中發生回傳時 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25444121-5a72-4dac-8e50-ad2b7ac667af
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 9c4c59bb9dbd3e2ba2b3b81ecf76271f21673bce
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598755"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-c"></a>處理沒有 UpdatePanel 的快顯視窗控制項回傳 (C#)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)

> AJAX 控制項工具組中的 PopupControl 擴充項提供了一種簡單的方式，可在啟用任何其他控制項時觸發快顯。 當這類面板中發生回傳，而且頁面上有數個面板時，很難判斷已按下哪一個面板。

## <a name="overview"></a>概觀

AJAX 控制項工具組中的 PopupControl 擴充項提供了一種簡單的方式，可在啟用任何其他控制項時觸發快顯。 當這類面板中發生回傳，而且頁面上有數個面板時，很難判斷已按下哪一個面板。

## <a name="steps"></a>步驟

當您使用 `PopupControl` 進行回傳，但是沒有在頁面上有 `UpdatePanel` 時，控制項工具組不會提供方法來判斷哪個用戶端專案已觸發快顯視窗，進而導致回傳。 不過，小技巧提供此案例的因應措施。

首先，以下是基本設定：兩個文字方塊，兩者都會觸發相同的快顯視窗，也就是行事曆。 兩個 `PopupControlExtenders` 將文字方塊和快顯一起帶入。

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample1.aspx)]

基本概念是在 &lt;`form`&gt; 專案中加入隱藏的表單欄位，這些專案會保存啟動快顯視窗的文字方塊：

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample2.aspx)]

載入頁面時，JavaScript 程式碼會將事件處理常式新增至這兩個文字方塊：每當使用者按一下文字方塊時，其名稱就會寫入隱藏的表單欄位中：

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample3.html)]

在伺服器端程式碼中，必須讀取隱藏欄位的值。 由於隱藏的表單欄位很容易操作，因此必須使用允許清單驗證隱藏值的系統清單方法。 一旦識別出正確的文字方塊之後，就會將行事曆的日期寫入其中。

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample4.aspx)]

[當使用者按一下文字方塊時，就會顯示行事曆 ![](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image1.png)

當使用者按一下文字方塊時，就會出現行事曆（[按一下以查看完整大小的影像](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png)）

[![按一下日期會將它放在文字方塊中](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image4.png)

按一下日期會將它放在文字方塊中（[按一下以查看完整大小的影像](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png)）

> [!div class="step-by-step"]
> [上一頁](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
> [下一頁](using-multiple-popup-controls-vb.md)
