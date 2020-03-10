---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
title: 使用 UpdatePanel （C#）處理 Popup 控制項的回傳 |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 PopupControl 擴充項提供了一種簡單的方式，可在啟用任何其他控制項時觸發快顯。 必須特別小心 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1f68f59d-9c1e-4cf3-b304-c13ae6b7203e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 8b9e58d68b3d6c5d01ceaba6c01653e9574b541b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78612928"
---
# <a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-c"></a>處理有 UpdatePanel 的快顯視窗控制項回傳 (C#)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.cs.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2CS.pdf)

> AJAX 控制項工具組中的 PopupControl 擴充項提供了一種簡單的方式，可在啟用任何其他控制項時觸發快顯。 當回傳發生在這類快顯視窗內時，必須特別小心。

## <a name="overview"></a>概觀

AJAX 控制項工具組中的 PopupControl 擴充項提供了一種簡單的方式，可在啟用任何其他控制項時觸發快顯。 當回傳發生在這類快顯視窗內時，必須特別小心。

## <a name="steps"></a>步驟

當使用 `PopupControl` 與回傳時，`UpdatePanel` 可以防止回傳所造成的頁面重新整理。 下列標記會定義幾個重要的元素：

- `ScriptManager` 控制項，讓 ASP.NET AJAX 控制項工具組可以運作
- 兩個 `TextBox` 控制項都會觸發快顯視窗
- 將作為快顯的 `Panel` 控制項
- 在面板中，`Calendar` 控制項內嵌在 `UpdatePanel` 控制項內
- 兩個 `PopupControlExtender` 控制項，可將面板指派給文字方塊

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample1.aspx)]

請注意，已設定 `Calendar` 控制項的 `OnSelectionChanged` 屬性。 因此當使用者選取行事曆內的日期時，就會發生回傳，而且會執行伺服器端方法 `c1_SelectionChanged()`。 在該方法中，必須取出目前的日期，並將其寫回文字方塊。

的語法如下：首先，必須在頁面上產生 `PopupControlExtender` 的 proxy 物件。 ASP.NET AJAX Control 工具組提供 `GetProxyForCurrentPopup()` 方法。 這個方法傳回的物件支援 `Commit()` 方法，其會將值傳回給觸發快顯視窗的控制項（而不是觸發方法呼叫的控制項！）。 下列程式碼會提供選取的日期做為 `Commit()` 方法的引數，使程式碼將選取的日期寫回文字方塊：

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample2.aspx)]

現在當您按一下行事曆日期時，所選取的日期會出現在相關聯的文字方塊中，建立目前可在許多網站上找到的日期選擇器控制項。

[當使用者按一下文字方塊時，就會顯示行事曆 ![](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image1.png)

當使用者按一下文字方塊時，就會出現行事曆（[按一下以查看完整大小的影像](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image3.png)）

[![按一下日期會將它放在文字方塊中](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image4.png)

按一下日期會將它放在文字方塊中（[按一下以查看完整大小的影像](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image6.png)）

> [!div class="step-by-step"]
> [上一頁](using-multiple-popup-controls-cs.md)
> [下一頁](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
