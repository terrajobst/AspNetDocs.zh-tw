---
uid: web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-vb
title: 在中繼器中使用項 confirmbutton （VB） |Microsoft Docs
author: wenz
description: 當使用者按一下按鈕（包括 LinkButton 控制項）時，AJAX 控制項工具組中的項 confirmbutton 擴充項會建立 [是/否] 快顯視窗。 只有在是 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 18c31709-3f9d-4d93-8b01-f1356bf610b4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-vb
msc.type: authoredcontent
ms.openlocfilehash: 001233d866d8a731d93d6900f714cd2060f3d08c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613950"
---
# <a name="using-a-confirmbutton-in-a-repeater-vb"></a><span data-ttu-id="83b4b-104">在重複項中使用 ConfirmButton (VB)</span><span class="sxs-lookup"><span data-stu-id="83b4b-104">Using a ConfirmButton In a Repeater (VB)</span></span>

<span data-ttu-id="83b4b-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="83b4b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="83b4b-106">[下載程式代碼](https://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.vb.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="83b4b-106">[Download Code](https://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1VB.pdf)</span></span>

> <span data-ttu-id="83b4b-107">當使用者按一下按鈕（包括 LinkButton 控制項）時，AJAX 控制項工具組中的項 confirmbutton 擴充項會建立 [是/否] 快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="83b4b-107">The ConfirmButton extender in the AJAX Control Toolkit creates a Yes/No popup when the user clicks on a button (including LinkButton control).</span></span> <span data-ttu-id="83b4b-108">只有當您按一下 [是] 時，才會執行按鈕的動作，否則會取消。</span><span class="sxs-lookup"><span data-stu-id="83b4b-108">Only if Yes is clicked, the button's action is executed, otherwise cancelled.</span></span> <span data-ttu-id="83b4b-109">這也可以在中繼器中進行。</span><span class="sxs-lookup"><span data-stu-id="83b4b-109">This is also possible in a repeater.</span></span>

## <a name="overview"></a><span data-ttu-id="83b4b-110">概觀</span><span class="sxs-lookup"><span data-stu-id="83b4b-110">Overview</span></span>

<span data-ttu-id="83b4b-111">當使用者按一下按鈕（包括 LinkButton 控制項）時，AJAX 控制項工具組中的項 confirmbutton 擴充項會建立 [是/否] 快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="83b4b-111">The ConfirmButton extender in the AJAX Control Toolkit creates a Yes/No popup when the user clicks on a button (including LinkButton control).</span></span> <span data-ttu-id="83b4b-112">只有當您按一下 [是] 時，才會執行按鈕的動作，否則會取消。</span><span class="sxs-lookup"><span data-stu-id="83b4b-112">Only if Yes is clicked, the button's action is executed, otherwise cancelled.</span></span> <span data-ttu-id="83b4b-113">這也可以在中繼器中進行。</span><span class="sxs-lookup"><span data-stu-id="83b4b-113">This is also possible in a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="83b4b-114">步驟</span><span class="sxs-lookup"><span data-stu-id="83b4b-114">Steps</span></span>

<span data-ttu-id="83b4b-115">首先，需要資料來源。</span><span class="sxs-lookup"><span data-stu-id="83b4b-115">First of all, a data source is required.</span></span> <span data-ttu-id="83b4b-116">這個範例會使用 AdventureWorks 資料庫和 Microsoft SQL Server 2005 Express Edition。</span><span class="sxs-lookup"><span data-stu-id="83b4b-116">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="83b4b-117">資料庫是 Visual Studio 安裝（包含 express edition）的選擇性部分，而且也可在[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下個別下載。</span><span class="sxs-lookup"><span data-stu-id="83b4b-117">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="83b4b-118">AdventureWorks 資料庫是 SQL Server 2005 範例和範例資料庫的一部分（下載于[https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)）。</span><span class="sxs-lookup"><span data-stu-id="83b4b-118">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="83b4b-119">設定資料庫最簡單的方式，就是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)）並附加 `AdventureWorks.mdf` 資料庫檔案。</span><span class="sxs-lookup"><span data-stu-id="83b4b-119">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="83b4b-120">在此範例中，我們假設 SQL Server 2005 Express Edition 的實例呼叫 `SQLEXPRESS` 並與 web 伺服器位於同一部電腦上;這也是預設設定。</span><span class="sxs-lookup"><span data-stu-id="83b4b-120">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="83b4b-121">如果您的安裝程式不同，則必須調整資料庫的連接資訊。</span><span class="sxs-lookup"><span data-stu-id="83b4b-121">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="83b4b-122">若要啟用 ASP.NET AJAX 和控制項工具組的功能，`ScriptManager` 控制項必須放在頁面上的任何位置（但在 `<form>` 元素內）：</span><span class="sxs-lookup"><span data-stu-id="83b4b-122">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample1.aspx)]

<span data-ttu-id="83b4b-123">然後，需要資料來源。</span><span class="sxs-lookup"><span data-stu-id="83b4b-123">Then, a data source is required.</span></span> <span data-ttu-id="83b4b-124">為了簡單起見，只會抓取 AdventureWorks 「廠商」資料表中的前五個專案。</span><span class="sxs-lookup"><span data-stu-id="83b4b-124">For the sake of simplicity, only the first five entries in AdventureWorks' Vendors table are retrieved.</span></span> <span data-ttu-id="83b4b-125">請注意，使用 [Visual Studio wizard] 建立資料來源時，資料表名稱（`Vendors`）目前不會正確地加上 `Purchasing`的前置詞。</span><span class="sxs-lookup"><span data-stu-id="83b4b-125">Note that when using the Visual Studio wizard to create the data source, the table name (`Vendors`) is currently not correctly prefixed with `Purchasing`.</span></span> <span data-ttu-id="83b4b-126">下列標記是正確的：</span><span class="sxs-lookup"><span data-stu-id="83b4b-126">The following markup is the correct one:</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample2.aspx)]

<span data-ttu-id="83b4b-127">然後，可以在中繼器內使用此資料來源。</span><span class="sxs-lookup"><span data-stu-id="83b4b-127">This data source can then be used within a repeater.</span></span> <span data-ttu-id="83b4b-128">如同往常，`DataBinder.Eval()` 方法會從資料來源抓取資料。</span><span class="sxs-lookup"><span data-stu-id="83b4b-128">As usual, the `DataBinder.Eval()` method retrieves data from the data source.</span></span> <span data-ttu-id="83b4b-129">然後，`ConfirmButtonExtender` 控制項必須放在重複項的 [`<ItemTemplate>`] 區段內，才會顯示在資料來源中的每個專案。</span><span class="sxs-lookup"><span data-stu-id="83b4b-129">The `ConfirmButtonExtender` control must then be placed within the `<ItemTemplate>` section of the repeater so that it appears for every entry in the data source.</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample3.aspx)]

<span data-ttu-id="83b4b-130">[![[確認] 按鈕會出現在資料來源中的每個專案旁邊](using-a-confirmbutton-in-a-repeater-vb/_static/image2.png)](using-a-confirmbutton-in-a-repeater-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="83b4b-130">[![The confirm button appears next to each entry from the data source](using-a-confirmbutton-in-a-repeater-vb/_static/image2.png)](using-a-confirmbutton-in-a-repeater-vb/_static/image1.png)</span></span>

<span data-ttu-id="83b4b-131">[確認] 按鈕會出現在資料來源中的每個專案旁邊（[按一下以查看完整大小的影像](using-a-confirmbutton-in-a-repeater-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="83b4b-131">The confirm button appears next to each entry from the data source ([Click to view full-size image](using-a-confirmbutton-in-a-repeater-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="83b4b-132">上一篇</span><span class="sxs-lookup"><span data-stu-id="83b4b-132">Previous</span></span>](using-a-confirmbutton-in-a-repeater-cs.md)
