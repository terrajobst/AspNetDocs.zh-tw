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
# <a name="drag-and-drop-via-reorderlist-c"></a><span data-ttu-id="90309-104">透過 ReorderList 拖放 (C#)</span><span class="sxs-lookup"><span data-stu-id="90309-104">Drag and Drop via ReorderList (C#)</span></span>

<span data-ttu-id="90309-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="90309-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="90309-106">[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="90309-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)</span></span>

> <span data-ttu-id="90309-107">AJAX 控制項工具組中的 Reorderlist 回傳控制項提供清單，讓使用者可以透過拖放方式重新排序。</span><span class="sxs-lookup"><span data-stu-id="90309-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="90309-108">清單的目前順序應該保存在伺服器上。</span><span class="sxs-lookup"><span data-stu-id="90309-108">The current order of the list shall be persisted on the server.</span></span>

## <a name="overview"></a><span data-ttu-id="90309-109">概觀</span><span class="sxs-lookup"><span data-stu-id="90309-109">Overview</span></span>

<span data-ttu-id="90309-110">AJAX 控制項工具組中的 `ReorderList` 控制項提供一個清單，讓使用者可以透過拖放方式重新排序。</span><span class="sxs-lookup"><span data-stu-id="90309-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="90309-111">清單的目前順序應該保存在伺服器上。</span><span class="sxs-lookup"><span data-stu-id="90309-111">The current order of the list shall be persisted on the server.</span></span>

## <a name="steps"></a><span data-ttu-id="90309-112">步驟</span><span class="sxs-lookup"><span data-stu-id="90309-112">Steps</span></span>

<span data-ttu-id="90309-113">`ReorderList` 控制項支援將資料從資料庫系結至清單。</span><span class="sxs-lookup"><span data-stu-id="90309-113">The `ReorderList` control supports binding data from a database to the list.</span></span> <span data-ttu-id="90309-114">最棒的是，它也支援將清單元素順序的變更寫回資料存放區。</span><span class="sxs-lookup"><span data-stu-id="90309-114">Best of all, it also supports writing changes to the order of the list element back to the data store.</span></span>

<span data-ttu-id="90309-115">此範例使用 Microsoft SQL Server 2005 Express Edition 做為資料存放區。</span><span class="sxs-lookup"><span data-stu-id="90309-115">This sample uses Microsoft SQL Server 2005 Express Edition as the data store.</span></span> <span data-ttu-id="90309-116">資料庫是 Visual Studio 安裝的選擇性（和免費）部分，包含 express edition。</span><span class="sxs-lookup"><span data-stu-id="90309-116">The database is an optional (and free) part of a Visual Studio installation, including express edition.</span></span> <span data-ttu-id="90309-117">此外，也可在[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下個別下載。</span><span class="sxs-lookup"><span data-stu-id="90309-117">It is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="90309-118">在此範例中，我們假設 SQL Server 2005 Express Edition 的實例呼叫 `SQLEXPRESS` 並與 web 伺服器位於同一部電腦上;這也是預設設定。</span><span class="sxs-lookup"><span data-stu-id="90309-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="90309-119">如果您的安裝程式不同，則必須調整資料庫的連接資訊。</span><span class="sxs-lookup"><span data-stu-id="90309-119">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="90309-120">設定資料庫最簡單的方式是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ）。</span><span class="sxs-lookup"><span data-stu-id="90309-120">The easiest way to set up the database is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span></span> <span data-ttu-id="90309-121">連接到伺服器，按兩下 `Databases` 並建立新的資料庫（按一下滑鼠右鍵，然後選擇 [`New Database`]），稱為 [`Tutorials`]。</span><span class="sxs-lookup"><span data-stu-id="90309-121">Connect to the server, double-click on `Databases` and create a new database (right-click and choose `New Database`) called `Tutorials`.</span></span>

<span data-ttu-id="90309-122">在此資料庫中，使用下列四個數據行建立名為 `AJAX` 的新資料表：</span><span class="sxs-lookup"><span data-stu-id="90309-122">In this database, create a new table called `AJAX` with the following four columns:</span></span>

- <span data-ttu-id="90309-123">`id` （primary key、integer、identity、not Null）</span><span class="sxs-lookup"><span data-stu-id="90309-123">`id` (primary key, integer, identity, not NULL)</span></span>
- <span data-ttu-id="90309-124">`char` （char （1），Null）</span><span class="sxs-lookup"><span data-stu-id="90309-124">`char` (char(1), NULL)</span></span>
- <span data-ttu-id="90309-125">`description` （Varchar （50），Null）</span><span class="sxs-lookup"><span data-stu-id="90309-125">`description` (varchar(50), NULL)</span></span>
- <span data-ttu-id="90309-126">`position` （int，Null）</span><span class="sxs-lookup"><span data-stu-id="90309-126">`position` (int, NULL)</span></span>

<span data-ttu-id="90309-127">[![AJAX 資料表的版面配置](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="90309-127">[![The layout of the AJAX table](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)</span></span>

<span data-ttu-id="90309-128">AJAX 資料表的版面配置（[按一下以查看完整大小的影像](drag-and-drop-via-reorderlist-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="90309-128">The layout of the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image3.png))</span></span>

<span data-ttu-id="90309-129">接下來，在資料表中填入幾個值。</span><span class="sxs-lookup"><span data-stu-id="90309-129">Next, fill the table with a couple of values.</span></span> <span data-ttu-id="90309-130">請注意，[`position`] 資料行會保存元素的排序次序。</span><span class="sxs-lookup"><span data-stu-id="90309-130">Note that the `position` column holds the sort order of the elements.</span></span>

<span data-ttu-id="90309-131">[![AJAX 資料表中的初始資料](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="90309-131">[![The initial data in the AJAX table](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)</span></span>

<span data-ttu-id="90309-132">AJAX 資料表中的初始資料（[按一下以查看完整大小的影像](drag-and-drop-via-reorderlist-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="90309-132">The initial data in the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image6.png))</span></span>

<span data-ttu-id="90309-133">下一個步驟需要產生 `SqlDataSource` 控制項，以便與新的資料庫和其資料表進行通訊。</span><span class="sxs-lookup"><span data-stu-id="90309-133">The next step requires to generate an `SqlDataSource` control to communicate with the new database and its table.</span></span> <span data-ttu-id="90309-134">資料來源必須支援 `SELECT` 和 `UPDATE` SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="90309-134">The data source must support the `SELECT` and `UPDATE` SQL commands.</span></span> <span data-ttu-id="90309-135">當清單專案的順序之後變更時，`ReorderList` 控制項會自動將兩個值提交至資料來源的 `Update` 命令：新的位置和元素的識別碼。</span><span class="sxs-lookup"><span data-stu-id="90309-135">When the order of the list elements is later changed, the `ReorderList` control automatically submits two values to the data source's `Update` command: the new position and the ID of the element.</span></span> <span data-ttu-id="90309-136">因此，資料來源需要這兩個值的 `<UpdateParameters>` 區段：</span><span class="sxs-lookup"><span data-stu-id="90309-136">Therefore, the data source needs an `<UpdateParameters>` section for these two values:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample1.aspx)]

<span data-ttu-id="90309-137">`ReorderList` 控制項必須設定下列屬性：</span><span class="sxs-lookup"><span data-stu-id="90309-137">The `ReorderList` control needs to set the following attributes:</span></span>

- <span data-ttu-id="90309-138">`AllowReorder`：是否可以重新排列清單專案</span><span class="sxs-lookup"><span data-stu-id="90309-138">`AllowReorder`: Whether the list items may be rearranged</span></span>
- <span data-ttu-id="90309-139">`DataSourceID`：資料來源的識別碼</span><span class="sxs-lookup"><span data-stu-id="90309-139">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="90309-140">`DataKeyField`：資料來源中的主要索引鍵資料行名稱</span><span class="sxs-lookup"><span data-stu-id="90309-140">`DataKeyField`: The name of the primary key column in the data source</span></span>
- <span data-ttu-id="90309-141">`SortOrderField`：提供清單專案排序次序的資料來源資料行</span><span class="sxs-lookup"><span data-stu-id="90309-141">`SortOrderField`: The data source column that provides the sort order for the list items</span></span>

<span data-ttu-id="90309-142">在 [`<DragHandleTemplate>`] 和 [`<ItemTemplate>`] 區段中，可以微調清單的版面配置。</span><span class="sxs-lookup"><span data-stu-id="90309-142">In the `<DragHandleTemplate>` and `<ItemTemplate>` sections, the layout of the list can be fine-tuned.</span></span> <span data-ttu-id="90309-143">此外，您可以使用 `Eval()` 方法來進行資料系結，如下所示：</span><span class="sxs-lookup"><span data-stu-id="90309-143">Also, databinding is possible using the `Eval()` method, as seen here:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample2.aspx)]

<span data-ttu-id="90309-144">下列 CSS 樣式資訊（在 `ReorderList` 控制項的 [`<DragHandleTemplate>`] 區段中參考）可確保滑鼠指標停留在拖曳控點上方時，會適當地變更：</span><span class="sxs-lookup"><span data-stu-id="90309-144">The following CSS style information (referenced in the `<DragHandleTemplate>` section of the `ReorderList` control) makes sure that the mouse pointer changes appropriately when it hovers over the drag handle:</span></span>

[!code-css[Main](drag-and-drop-via-reorderlist-cs/samples/sample3.css)]

<span data-ttu-id="90309-145">最後，`ScriptManager` 控制項會為網頁初始化 ASP.NET AJAX：</span><span class="sxs-lookup"><span data-stu-id="90309-145">Finally, a `ScriptManager` control initializes ASP.NET AJAX for the page:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample4.aspx)]

<span data-ttu-id="90309-146">在瀏覽器中執行此範例，並稍微重新排列清單專案。</span><span class="sxs-lookup"><span data-stu-id="90309-146">Run this example in the browser and rearrange the list items a bit.</span></span> <span data-ttu-id="90309-147">然後，重載頁面，並（或）查看資料庫。</span><span class="sxs-lookup"><span data-stu-id="90309-147">Then, reload the page and/or have a look at the database.</span></span> <span data-ttu-id="90309-148">改變的位置已經過維護，而且也會反映在資料庫的 [`position`] 資料行中的值，而且不需要任何程式碼，只要使用標記即可。</span><span class="sxs-lookup"><span data-stu-id="90309-148">The altered positions have been maintained and are also reflected by the values in the `position` column in the database and that all without any code, just by using markup.</span></span>

<span data-ttu-id="90309-149">[根據新的清單專案順序，![資料庫中的資料變更](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="90309-149">[![The data in the database changes according to the new list item order](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)</span></span>

<span data-ttu-id="90309-150">資料庫中的資料會根據新的清單專案順序而變更（[按一下以查看完整大小的影像](drag-and-drop-via-reorderlist-cs/_static/image9.png)）</span><span class="sxs-lookup"><span data-stu-id="90309-150">The data in the database changes according to the new list item order ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image9.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="90309-151">[上一頁](using-postbacks-with-reorderlist-cs.md)
> [下一頁](using-postbacks-with-reorderlist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="90309-151">[Previous](using-postbacks-with-reorderlist-cs.md)
[Next](using-postbacks-with-reorderlist-vb.md)</span></span>
