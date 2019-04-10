---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
title: 使用具有 reorderlist 的回傳 (C#) |Microsoft Docs
author: wenz
description: 在 AJAX Control Toolkit reorderlist 的回傳控制項提供使用者透過拖放來重新排列的清單。 已重新排列清單，每當 po...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 70d5d106-b547-442c-a7fd-3492b3e3d646
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: 6f8f74b74080104980e1db866d695fe7c6d9d5fc
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59393349"
---
# <a name="using-postbacks-with-reorderlist-c"></a>使用具有 ReorderList 的回傳 (C#)

藉由[Christian Wenz](https://github.com/wenz)

[下載程式碼](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.cs.zip)或[下載 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4CS.pdf)

> 在 AJAX Control Toolkit reorderlist 的回傳控制項提供使用者透過拖放來重新排列的清單。 已重新排列清單，每當回傳會通知變更的伺服器。


## <a name="overview"></a>總覽

`ReorderList` AJAX Control Toolkit 中的控制項提供使用者透過拖放來重新排列的清單。 已重新排列清單，每當回傳會通知變更的伺服器。

## <a name="steps"></a>步驟

有數個可能的資料來源`ReorderList`控制項。 其中一個是使用`XmlDataSource`控制項：

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample1.aspx)]

若要繫結至這個 XML`ReorderList`必須設定控制項，並啟用回傳中，下列屬性：

- `DataSourceID`:資料來源的識別碼
- `SortOrderField`:要排序的屬性
- `AllowReorder`:是否要允許使用者重新排列清單項目
- `PostBackOnReorder`:是否要建立回傳，每當重新排列清單

以下是控制項的適當標記：

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample2.aspx)]

內`ReorderList`控制項，從資料來源的特定資料可能會繫結使用`Eval()`方法：

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample3.aspx)]

在頁面上的任意位置，標籤會包含的資訊，最後重新調整順序發生：

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample4.aspx)]

此標籤會填入處理回傳的伺服器端程式碼中的文字：

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample5.aspx)]

最後，若要啟動的 ASP.NET AJAX Control Toolkit 中，功能`ScriptManager`控制項必須放在頁面上：

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample6.aspx)]


[![E除此之外，每個重新排列觸發回傳](using-postbacks-with-reorderlist-cs/_static/image2.png)](using-postbacks-with-reorderlist-cs/_static/image1.png)

每個重新排列觸發回傳 ([按一下以檢視完整大小的影像](using-postbacks-with-reorderlist-cs/_static/image3.png))

> [!div class="step-by-step"]
> [下一步](drag-and-drop-via-reorderlist-cs.md)
