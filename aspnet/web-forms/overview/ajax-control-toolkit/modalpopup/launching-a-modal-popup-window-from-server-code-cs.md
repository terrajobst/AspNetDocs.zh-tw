---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-cs
title: 從伺服器程式碼啟動強制回應快顯視窗C#（） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 ModalPopup 控制項提供一個簡單的方式，讓您使用用戶端的方法來建立強制回應快顯視窗。 不過，有些案例需要 t 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2f67d8ef-73ca-447d-a0cc-6e3168431e6a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-cs
msc.type: authoredcontent
ms.openlocfilehash: fec0ce2cdd24333f65201301718440e1a09d930e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613292"
---
# <a name="launching-a-modal-popup-window-from-server-code-c"></a>從伺服器程式碼啟動強制回應快顯視窗 (C#)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.cs.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1CS.pdf)

> AJAX 控制項工具組中的 ModalPopup 控制項提供一個簡單的方式，讓您使用用戶端的方法來建立強制回應快顯視窗。 不過，有些情況需要在伺服器端觸發強制回應快顯視窗。

## <a name="overview"></a>概觀

AJAX 控制項工具組中的 ModalPopup 控制項提供一個簡單的方式，讓您使用用戶端的方法來建立強制回應快顯視窗。 不過，有些情況需要在伺服器端觸發強制回應快顯視窗。

## <a name="steps"></a>步驟

首先，必須要有 ASP.NET 按鈕 web 控制項，才能示範 ModalPopup 控制項的運作方式。 在新頁面上的 &lt;表單&gt; 元素中加入這類按鈕：

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample1.aspx)]

然後，您需要您想要建立之快顯的標記。 將它定義為 `<asp:Panel>` 控制項，並確定它包含按鈕控制項。 ModalPopup 控制項提供讓這類按鈕關閉快顯視窗的功能;否則，沒有任何簡單的方法可以讓它消失。

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample2.aspx)]

接下來，從 ASP.NET AJAX 工具組將 ModalPopup 控制項新增至頁面。 設定載入控制項的按鈕屬性、使其消失的按鈕，以及實際快顯視窗的識別碼。

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample3.aspx)]

如同所有以 ASP.NET AJAX 為基礎的網頁，需要腳本管理員，才能為不同的目標瀏覽器載入必要的 JavaScript 程式庫：

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample4.aspx)]

在瀏覽器中執行範例。 當您按一下按鈕時，就會出現強制回應快顯視窗。 若要使用伺服器端程式碼達到相同的效果，則需要新的按鈕：

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample5.aspx)]

如您所見，按一下按鈕會產生回傳，並在伺服器上執行 `ServerButton_Click()` 方法。 在這個方法中，稱為 `launchModal()` 的 JavaScript 函式會執行成精確的，一旦載入頁面，就會執行 JavaScript 函式：

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample6.aspx)]

`launchModal()` 的工作是要顯示 ModalPopup。 一旦載入完整的 HTML 頁面，就會執行 `launchModal()` 函式。 不過，目前尚未完全載入 ASP.NET AJAX 架構。 因此，`launchModal()` 函數只會設定一個變數，ModalPopup 控制項稍後必須顯示：

[!code-html[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample7.html)]

`pageLoad()` JavaScript 函式是一種特殊函式，會在 ASP.NET AJAX 完全載入後執行。 因此，我們將程式碼加入此函式以顯示 ModalPopup 控制項，但只有在之前呼叫過 `launchModal()`：

[!code-javascript[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample8.js)]

`$find()` 函式會在頁面上尋找名為的專案，而且需要伺服器端識別碼做為參數。 因此，`$find("mpe")` 會傳回 ModalPopup 控制項的用戶端標記法;其 `show()` 方法會讓快顯視窗出現。

[當按一下其中一個按鈕時，就會出現強制回應快顯視窗 ![](launching-a-modal-popup-window-from-server-code-cs/_static/image2.png)](launching-a-modal-popup-window-from-server-code-cs/_static/image1.png)

按一下其中一個按鈕時，就會出現強制回應快顯視窗（[按一下以查看完整大小的影像](launching-a-modal-popup-window-from-server-code-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [下一個](using-modalpopup-with-a-repeater-control-cs.md)
