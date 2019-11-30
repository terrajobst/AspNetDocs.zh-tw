---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
title: 透過 Reorderlist 回傳（C#）拖放 |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 Reorderlist 回傳控制項提供清單，讓使用者可以透過拖放方式重新排序。 清單的目前順序應該是 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6350ee8e-11d6-4aff-b51c-942878014835
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: 2fc6d55a290cbb58bea36d8145d814e337bbd931
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611421"
---
# <a name="drag-and-drop-via-reorderlist-c"></a>透過 ReorderList 拖放 (C#)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)

> AJAX 控制項工具組中的 Reorderlist 回傳控制項提供清單，讓使用者可以透過拖放方式重新排序。 清單的目前順序應該保存在伺服器上。

## <a name="overview"></a>概觀

AJAX 控制項工具組中的 `ReorderList` 控制項提供一個清單，讓使用者可以透過拖放方式重新排序。 清單的目前順序應該保存在伺服器上。

## <a name="steps"></a>步驟

`ReorderList` 控制項支援將資料從資料庫系結至清單。 最棒的是，它也支援將清單元素順序的變更寫回資料存放區。

此範例使用 Microsoft SQL Server 2005 Express Edition 做為資料存放區。 資料庫是 Visual Studio 安裝的選擇性（和免費）部分，包含 express edition。 此外，也可在[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下個別下載。 在此範例中，我們假設 SQL Server 2005 Express Edition 的實例呼叫 `SQLEXPRESS` 並與 web 伺服器位於同一部電腦上;這也是預設設定。 如果您的安裝程式不同，則必須調整資料庫的連接資訊。

設定資料庫最簡單的方式是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ）。 連接到伺服器，按兩下 `Databases` 並建立新的資料庫（按一下滑鼠右鍵，然後選擇 [`New Database`]），稱為 [`Tutorials`]。

在此資料庫中，使用下列四個數據行建立名為 `AJAX` 的新資料表：

- `id` （primary key、integer、identity、not Null）
- `char` （char （1），Null）
- `description` （Varchar （50），Null）
- `position` （int，Null）

[![AJAX 資料表的版面配置](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)

AJAX 資料表的版面配置（[按一下以查看完整大小的影像](drag-and-drop-via-reorderlist-cs/_static/image3.png)）

接下來，在資料表中填入幾個值。 請注意，[`position`] 資料行會保存元素的排序次序。

[![AJAX 資料表中的初始資料](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)

AJAX 資料表中的初始資料（[按一下以查看完整大小的影像](drag-and-drop-via-reorderlist-cs/_static/image6.png)）

下一個步驟需要產生 `SqlDataSource` 控制項，以便與新的資料庫和其資料表進行通訊。 資料來源必須支援 `SELECT` 和 `UPDATE` SQL 命令。 當清單專案的順序之後變更時，`ReorderList` 控制項會自動將兩個值提交至資料來源的 `Update` 命令：新的位置和元素的識別碼。 因此，資料來源需要這兩個值的 `<UpdateParameters>` 區段：

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample1.aspx)]

`ReorderList` 控制項必須設定下列屬性：

- `AllowReorder`：是否可以重新排列清單專案
- `DataSourceID`：資料來源的識別碼
- `DataKeyField`：資料來源中的主要索引鍵資料行名稱
- `SortOrderField`：提供清單專案排序次序的資料來源資料行

在 [`<DragHandleTemplate>`] 和 [`<ItemTemplate>`] 區段中，可以微調清單的版面配置。 此外，您可以使用 `Eval()` 方法來進行資料系結，如下所示：

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample2.aspx)]

下列 CSS 樣式資訊（在 `ReorderList` 控制項的 [`<DragHandleTemplate>`] 區段中參考）可確保滑鼠指標停留在拖曳控點上方時，會適當地變更：

[!code-css[Main](drag-and-drop-via-reorderlist-cs/samples/sample3.css)]

最後，`ScriptManager` 控制項會為網頁初始化 ASP.NET AJAX：

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample4.aspx)]

在瀏覽器中執行此範例，並稍微重新排列清單專案。 然後，重載頁面，並（或）查看資料庫。 改變的位置已經過維護，而且也會反映在資料庫的 [`position`] 資料行中的值，而且不需要任何程式碼，只要使用標記即可。

[根據新的清單專案順序，![資料庫中的資料變更](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)

資料庫中的資料會根據新的清單專案順序而變更（[按一下以查看完整大小的影像](drag-and-drop-via-reorderlist-cs/_static/image9.png)）

> [!div class="step-by-step"]
> [上一頁](using-postbacks-with-reorderlist-cs.md)
> [下一頁](using-postbacks-with-reorderlist-vb.md)
