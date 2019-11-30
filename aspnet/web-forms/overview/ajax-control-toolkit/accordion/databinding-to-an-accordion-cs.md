---
uid: web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-cs
title: 資料系結至可C#折疊（） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 [可折疊式] 控制項提供多個窗格，並允許使用者一次顯示其中一項。 面板通常會宣告為 w 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 9c8f0054-e319-46f8-80c0-35b606d2fbd4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-cs
msc.type: authoredcontent
ms.openlocfilehash: 6c28cc958a1de9844627ae16175a5aed153993a8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607284"
---
# <a name="databinding-to-an-accordion-c"></a><span data-ttu-id="485aa-104">資料繫結至 Accordion (C#)</span><span class="sxs-lookup"><span data-stu-id="485aa-104">Databinding to an Accordion (C#)</span></span>

<span data-ttu-id="485aa-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="485aa-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="485aa-106">[下載程式代碼](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.cs.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="485aa-106">[Download Code](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1CS.pdf)</span></span>

> <span data-ttu-id="485aa-107">AJAX 控制項工具組中的 [可折疊式] 控制項提供多個窗格，並允許使用者一次顯示其中一項。</span><span class="sxs-lookup"><span data-stu-id="485aa-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="485aa-108">面板通常會在頁面本身內宣告，但系結至資料來源可提供更大的彈性。</span><span class="sxs-lookup"><span data-stu-id="485aa-108">Panels are usually declared within the page itself, but binding to a data source offers more flexibility.</span></span>

## <a name="overview"></a><span data-ttu-id="485aa-109">概觀</span><span class="sxs-lookup"><span data-stu-id="485aa-109">Overview</span></span>

<span data-ttu-id="485aa-110">AJAX 控制項工具組中的 [可折疊式] 控制項提供多個窗格，並允許使用者一次顯示其中一項。</span><span class="sxs-lookup"><span data-stu-id="485aa-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="485aa-111">面板通常會在頁面本身內宣告，但系結至資料來源可提供更大的彈性。</span><span class="sxs-lookup"><span data-stu-id="485aa-111">Panels are usually declared within the page itself, but binding to a data source offers more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="485aa-112">步驟</span><span class="sxs-lookup"><span data-stu-id="485aa-112">Steps</span></span>

<span data-ttu-id="485aa-113">首先，需要資料來源。</span><span class="sxs-lookup"><span data-stu-id="485aa-113">First of all, a data source is required.</span></span> <span data-ttu-id="485aa-114">這個範例會使用 AdventureWorks 資料庫和 Microsoft SQL Server 2005 Express Edition。</span><span class="sxs-lookup"><span data-stu-id="485aa-114">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="485aa-115">資料庫是 Visual Studio 安裝（包含 express edition）的選擇性部分，而且也可在[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下個別下載。</span><span class="sxs-lookup"><span data-stu-id="485aa-115">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="485aa-116">AdventureWorks 資料庫是 SQL Server 2005 範例和範例資料庫的一部分（下載于[https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)）。</span><span class="sxs-lookup"><span data-stu-id="485aa-116">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="485aa-117">設定資料庫最簡單的方式，就是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)）並附加 `AdventureWorks.mdf` 資料庫檔案。</span><span class="sxs-lookup"><span data-stu-id="485aa-117">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="485aa-118">在此範例中，我們假設 SQL Server 2005 Express Edition 的實例呼叫 `SQLEXPRESS` 並與 web 伺服器位於同一部電腦上;這也是預設設定。</span><span class="sxs-lookup"><span data-stu-id="485aa-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="485aa-119">如果您的安裝程式不同，則必須調整資料庫的連接資訊。</span><span class="sxs-lookup"><span data-stu-id="485aa-119">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="485aa-120">若要啟用 ASP.NET AJAX 和控制項工具組的功能，`ScriptManager` 控制項必須放在頁面上的任何位置（但在 `<form>` 元素內）：</span><span class="sxs-lookup"><span data-stu-id="485aa-120">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample1.aspx)]

<span data-ttu-id="485aa-121">然後，將資料來源加入至頁面。</span><span class="sxs-lookup"><span data-stu-id="485aa-121">Then, add a data source to the page.</span></span> <span data-ttu-id="485aa-122">為了使用有限數量的資料，我們只會在 AdventureWorks 資料庫的 [廠商] 資料表中選取前五個專案。</span><span class="sxs-lookup"><span data-stu-id="485aa-122">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="485aa-123">如果您使用 [Visual Studio 小幫手] 來建立資料來源，請注意，目前版本中的 bug 不會在資料表名稱（`Vendor`）前面加上 `Purchasing`的前置詞。</span><span class="sxs-lookup"><span data-stu-id="485aa-123">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="485aa-124">下列標記會顯示正確的語法：</span><span class="sxs-lookup"><span data-stu-id="485aa-124">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample2.aspx)]

<span data-ttu-id="485aa-125">請記住資料來源的名稱（ID）。</span><span class="sxs-lookup"><span data-stu-id="485aa-125">Remember the name (ID) of the data source.</span></span> <span data-ttu-id="485aa-126">接著，必須在 [可折疊] 控制項的 [`DataSourceID`] 屬性中使用此非常識別：</span><span class="sxs-lookup"><span data-stu-id="485aa-126">This very identification must then be used in the `DataSourceID` property of the Accordion control:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample3.aspx)]

<span data-ttu-id="485aa-127">在 [可折疊] 控制項中，您可以提供控制項各部分的範本，包括標頭（`<HeaderTemplate>`）和內容（`<ContentTemplate>`）。</span><span class="sxs-lookup"><span data-stu-id="485aa-127">Within the Accordion control, you can provide templates for various parts of the control, including the header (`<HeaderTemplate>`) and the content (`<ContentTemplate>`).</span></span> <span data-ttu-id="485aa-128">在這些元素內，只要使用 `DataBinder.Eval()` 方法，就能從資料來源輸出資料：</span><span class="sxs-lookup"><span data-stu-id="485aa-128">Within these elements, just output the data from the data source, using the `DataBinder.Eval()` method:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample4.aspx)]

<span data-ttu-id="485aa-129">載入頁面時，必須使用下列伺服器端程式碼，將資料來源系結至可折疊的：</span><span class="sxs-lookup"><span data-stu-id="485aa-129">When the page is loaded, the data source must be bound to the accordion with this server-side code:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample5.aspx)]

<span data-ttu-id="485aa-130">若要結束此範例，您需要定義在 [可折疊] 控制項（在其屬性 `HeaderCssClass` 和 `ContentCssClass`）中所參考的兩個 CSS 類別。</span><span class="sxs-lookup"><span data-stu-id="485aa-130">To conclude this sample, you need to define the two CSS classes that are referenced in the Accordion control (in its properties `HeaderCssClass` and `ContentCssClass`).</span></span> <span data-ttu-id="485aa-131">將下列標記放在頁面的 [`<head>`] 區段中：</span><span class="sxs-lookup"><span data-stu-id="485aa-131">Put the following markup in the `<head>` section of the page:</span></span>

[!code-css[Main](databinding-to-an-accordion-cs/samples/sample6.css)]

<span data-ttu-id="485aa-132">[![中的資料可直接來自資料來源](databinding-to-an-accordion-cs/_static/image2.png)](databinding-to-an-accordion-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="485aa-132">[![The data in the accordion comes directly from the data source](databinding-to-an-accordion-cs/_static/image2.png)](databinding-to-an-accordion-cs/_static/image1.png)</span></span>

<span data-ttu-id="485aa-133">可折疊中的資料直接來自資料來源（[按一下以查看完整大小的影像](databinding-to-an-accordion-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="485aa-133">The data in the accordion comes directly from the data source ([Click to view full-size image](databinding-to-an-accordion-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="485aa-134">下一步</span><span class="sxs-lookup"><span data-stu-id="485aa-134">Next</span></span>](dynamically-adding-an-accordion-pane-cs.md)
