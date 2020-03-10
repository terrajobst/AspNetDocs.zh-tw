---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
title: 定位 ModalPopup （C#） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 ModalPopup 控制項提供一個簡單的方式，讓您使用用戶端的方法來建立強制回應快顯視窗。 但控制項不提供 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1caac9d0-e21e-49d6-a8ff-e563a736d6ca
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: 8034f5aeb5a1a80f1ea8cbc9d638f3dfb1a38706
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613222"
---
# <a name="positioning-a-modalpopup-c"></a>定位 ModalPopup (C#)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.cs.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4CS.pdf)

> AJAX 控制項工具組中的 ModalPopup 控制項提供一個簡單的方式，讓您使用用戶端的方法來建立強制回應快顯視窗。 不過，控制項並未提供可定位快顯的內建功能。

## <a name="overview"></a>概觀

AJAX 控制項工具組中的 ModalPopup 控制項提供一個簡單的方式，讓您使用用戶端的方法來建立強制回應快顯視窗。 不過，控制項並未提供可定位快顯的內建功能。

## <a name="steps"></a>步驟

為了啟用 ASP.NET AJAX 和控制項工具組的功能，`ScriptManager`。 控制項必須放在頁面上的任何位置（但在 `<form>` 元素中）：

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample1.aspx)]

接下來，新增可作為強制回應快顯視窗的面板。 按鈕可用來關閉快顯視窗：

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample2.aspx)]

每當快顯視窗顯示時，就會放在頁面中的特定位置。 針對這項工作，會建立用戶端 JavaScript 函式。 它會先嘗試存取面板。 如果成功，則會使用 CSS 和 JavaScript 設定面板的位置（變更快顯的位置）。 不過，`ModalPopupExtender` 控制項也會嘗試定位快顯視窗。 因此，JavaScript 程式碼會重複放置快顯，每十秒一次。

[!code-html[Main](positioning-a-modalpopup-cs/samples/sample3.html)]

如您所見，`setTimeout()` JavaScript 方法的傳回值會儲存在全域變數中。 這可讓您使用 `clearTimeout()` 方法，依需求停止重複的快顯視窗位置：

[!code-javascript[Main](positioning-a-modalpopup-cs/samples/sample4.js)]

接下來要做的就是讓瀏覽器在適當時呼叫這些函式。 按一下觸發面板的按鈕時，必須呼叫 `movePanel()` JavaScript 函式：

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample5.aspx)]

而 `stopMoving()` 函式會在快顯視窗關閉時進入播放狀態，這可以在 `ModalPopupExtender` 控制項中觸發：

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample6.aspx)]

[![強制回應快顯視窗出現在指定的位置](positioning-a-modalpopup-cs/_static/image2.png)](positioning-a-modalpopup-cs/_static/image1.png)

強制回應快顯視窗會出現在指定的位置（[按一下以查看完整大小的影像](positioning-a-modalpopup-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [上一頁](handling-postbacks-from-a-modalpopup-cs.md)
> [下一頁](launching-a-modal-popup-window-from-server-code-vb.md)
