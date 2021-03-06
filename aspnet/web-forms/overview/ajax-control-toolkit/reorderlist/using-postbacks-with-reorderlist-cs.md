---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
title: 搭配 Reorderlist 回傳（C#）使用回傳 |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 Reorderlist 回傳控制項提供清單，讓使用者可以透過拖放方式重新排序。 每當重新排列清單時，就會有 po 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 70d5d106-b547-442c-a7fd-3492b3e3d646
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: f83201fc6fd458e730b6bb5ffee184d303b52e90
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78627229"
---
# <a name="using-postbacks-with-reorderlist-c"></a>使用具有 ReorderList 的回傳 (C#)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.cs.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4CS.pdf)

> AJAX 控制項工具組中的 Reorderlist 回傳控制項提供清單，讓使用者可以透過拖放方式重新排序。 每當重新排序清單時，回傳就會通知伺服器該變更。

## <a name="overview"></a>概觀

AJAX 控制項工具組中的 `ReorderList` 控制項提供一個清單，讓使用者可以透過拖放方式重新排序。 每當重新排序清單時，回傳就會通知伺服器該變更。

## <a name="steps"></a>步驟

`ReorderList` 控制項有幾個可能的資料來源。 其中一種是使用 `XmlDataSource` 控制項：

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample1.aspx)]

為了將此 XML 系結至 `ReorderList` 控制項並啟用回傳，必須設定下列屬性：

- `DataSourceID`：資料來源的識別碼
- `SortOrderField`：排序依據的屬性
- `AllowReorder`：是否允許使用者重新排序清單元素
- `PostBackOnReorder`：是否要在每次重新排列清單時建立回傳

以下是適當的控制項標記：

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample2.aspx)]

在 `ReorderList` 控制項內，可能會使用 `Eval()` 方法來系結資料來源中的特定資料：

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample3.aspx)]

在頁面上的任意位置上，標籤會保存最後一次發生重新排序時的資訊：

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample4.aspx)]

此標籤會以伺服器端程式碼中的文字填入，處理回傳：

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample5.aspx)]

最後，若要啟用 ASP.NET AJAX 和控制項工具組的功能，必須將 `ScriptManager` 控制項放在網頁上：

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample6.aspx)]

[![每個重新排列都會觸發回傳](using-postbacks-with-reorderlist-cs/_static/image2.png)](using-postbacks-with-reorderlist-cs/_static/image1.png)

每次重新排列都會觸發回傳（[按一下以查看完整大小的影像](using-postbacks-with-reorderlist-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [下一個](drag-and-drop-via-reorderlist-cs.md)
