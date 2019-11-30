---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
title: 搭配重複使用 HoverMenu 與重複項C#控制項（） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 HoverMenu 控制項提供簡單的快顯視窗效果：當滑鼠指標停留在專案上方時，快顯視窗會出現在 specifi 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e7700e7b-edc3-4183-a713-70e507cc7490
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 3e38b91d837c65191d4b3797fa31ef6112a1f070
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606699"
---
# <a name="using-hovermenu-with-a-repeater-control-c"></a><span data-ttu-id="4ffcc-103">使用 HoverMenu 與重複項控制項 (C#)</span><span class="sxs-lookup"><span data-stu-id="4ffcc-103">Using HoverMenu with a Repeater Control (C#)</span></span>

<span data-ttu-id="4ffcc-104">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="4ffcc-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="4ffcc-105">[下載程式代碼](https://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="4ffcc-105">[Download Code](https://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)</span></span>

> <span data-ttu-id="4ffcc-106">AJAX 控制項工具組中的 HoverMenu 控制項提供簡單的快顯視窗效果：當滑鼠指標停留在專案上時，快顯視窗會出現在指定的位置。</span><span class="sxs-lookup"><span data-stu-id="4ffcc-106">The HoverMenu control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="4ffcc-107">您也可以在中繼器中使用此控制項。</span><span class="sxs-lookup"><span data-stu-id="4ffcc-107">It is also possible to use this control within a repeater.</span></span>

## <a name="overview"></a><span data-ttu-id="4ffcc-108">概觀</span><span class="sxs-lookup"><span data-stu-id="4ffcc-108">Overview</span></span>

<span data-ttu-id="4ffcc-109">AJAX 控制項工具組中的 `HoverMenu` 控制項提供簡單的快顯視窗效果：當滑鼠指標停留在專案上時，快顯視窗會出現在指定的位置。</span><span class="sxs-lookup"><span data-stu-id="4ffcc-109">The `HoverMenu` control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="4ffcc-110">您也可以在中繼器中使用此控制項。</span><span class="sxs-lookup"><span data-stu-id="4ffcc-110">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="4ffcc-111">步驟</span><span class="sxs-lookup"><span data-stu-id="4ffcc-111">Steps</span></span>

<span data-ttu-id="4ffcc-112">首先，需要資料來源。</span><span class="sxs-lookup"><span data-stu-id="4ffcc-112">First of all, a data source is required.</span></span> <span data-ttu-id="4ffcc-113">這個範例會使用 AdventureWorks 資料庫和 Microsoft SQL Server 2005 Express Edition。</span><span class="sxs-lookup"><span data-stu-id="4ffcc-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="4ffcc-114">資料庫是 Visual Studio 安裝（包含 express edition）的選擇性部分，而且也可在[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下個別下載。</span><span class="sxs-lookup"><span data-stu-id="4ffcc-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="4ffcc-115">AdventureWorks 資料庫是 SQL Server 2005 範例和範例資料庫的一部分（下載于[https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)）。</span><span class="sxs-lookup"><span data-stu-id="4ffcc-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="4ffcc-116">設定資料庫最簡單的方式，就是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)）並附加 `AdventureWorks.mdf` 資料庫檔案。</span><span class="sxs-lookup"><span data-stu-id="4ffcc-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="4ffcc-117">在此範例中，我們假設 SQL Server 2005 Express Edition 的實例呼叫 `SQLEXPRESS` 並與 web 伺服器位於同一部電腦上;這也是預設設定。</span><span class="sxs-lookup"><span data-stu-id="4ffcc-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="4ffcc-118">如果您的安裝程式不同，則必須調整資料庫的連接資訊。</span><span class="sxs-lookup"><span data-stu-id="4ffcc-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="4ffcc-119">若要啟用 ASP.NET AJAX 和控制項工具組的功能，`ScriptManager` 控制項必須放在頁面上的任何位置（但在 `<form>` 元素內）：</span><span class="sxs-lookup"><span data-stu-id="4ffcc-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample1.aspx)]

<span data-ttu-id="4ffcc-120">然後，將資料來源加入至頁面。</span><span class="sxs-lookup"><span data-stu-id="4ffcc-120">Then, add a data source to the page.</span></span> <span data-ttu-id="4ffcc-121">為了使用有限數量的資料，我們只會在 AdventureWorks 資料庫的 [廠商] 資料表中選取前五個專案。</span><span class="sxs-lookup"><span data-stu-id="4ffcc-121">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="4ffcc-122">如果您使用 [Visual Studio 小幫手] 來建立資料來源，請注意，目前版本中的 bug 不會在資料表名稱（`Vendor`）前面加上 `Purchasing`的前置詞。</span><span class="sxs-lookup"><span data-stu-id="4ffcc-122">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="4ffcc-123">下列標記會顯示正確的語法：</span><span class="sxs-lookup"><span data-stu-id="4ffcc-123">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample2.aspx)]

<span data-ttu-id="4ffcc-124">接下來，新增可作為強制回應快顯視窗的面板：</span><span class="sxs-lookup"><span data-stu-id="4ffcc-124">Next, add a panel which serves as the modal popup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample3.aspx)]

<span data-ttu-id="4ffcc-125">`HoverMenuExtender` 現在就開始了。</span><span class="sxs-lookup"><span data-stu-id="4ffcc-125">Now, the `HoverMenuExtender` comes into play.</span></span> <span data-ttu-id="4ffcc-126">因此，資料來源中的每個專案都會取得自己的快顯視窗，而擴充項必須放在中繼器的 `<ItemTemplate>` 區段內。</span><span class="sxs-lookup"><span data-stu-id="4ffcc-126">So that every element in the data source gets its own popup, the extender must be put within the repeater's `<ItemTemplate>` section.</span></span> <span data-ttu-id="4ffcc-127">標記如下：</span><span class="sxs-lookup"><span data-stu-id="4ffcc-127">Here is the markup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample4.aspx)]

<span data-ttu-id="4ffcc-128">現在，資料來源中的每個專案都會在延遲50毫秒（`PopDelay` 屬性）之後，于右側顯示快顯視窗（`PopupPosition` 屬性）。</span><span class="sxs-lookup"><span data-stu-id="4ffcc-128">Now every item in the data source displays a popup to the right (`PopupPosition` attribute) after a delay of 50 milliseconds (`PopDelay` attribute).</span></span>

<span data-ttu-id="4ffcc-129">[![在重複項中的每個專案旁邊都會出現暫留功能表](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4ffcc-129">[![The hover menu appears next to each item in the repeater](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="4ffcc-130">[暫留] 功能表會顯示在 [中繼器] 中的每個專案旁邊（[按一下以查看完整大小的影像](using-hovermenu-with-a-repeater-control-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="4ffcc-130">The hover menu appears next to each item in the repeater ([Click to view full-size image](using-hovermenu-with-a-repeater-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4ffcc-131">下一步</span><span class="sxs-lookup"><span data-stu-id="4ffcc-131">Next</span></span>](using-hovermenu-with-a-repeater-control-vb.md)
