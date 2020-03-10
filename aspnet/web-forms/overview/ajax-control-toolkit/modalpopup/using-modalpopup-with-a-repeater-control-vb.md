---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-vb
title: 搭配重複使用 ModalPopup 與重複項控制項（VB） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 ModalPopup 控制項提供一個簡單的方式，讓您使用用戶端的方法來建立強制回應快顯視窗。 也可以使用此 contr 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0c8e74f1-b3ba-4ca9-a1c5-f5c4831a359a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 0966770f0218ca91ba7d25e7bf703bf7b005738e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613131"
---
# <a name="using-modalpopup-with-a-repeater-control-vb"></a><span data-ttu-id="cb626-104">使用 ModalPopup 與重複項控制項 (VB)</span><span class="sxs-lookup"><span data-stu-id="cb626-104">Using ModalPopup with a Repeater Control (VB)</span></span>

<span data-ttu-id="cb626-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="cb626-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="cb626-106">[下載程式代碼](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup2.vb.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="cb626-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup2.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup2VB.pdf)</span></span>

> <span data-ttu-id="cb626-107">AJAX 控制項工具組中的 ModalPopup 控制項提供一個簡單的方式，讓您使用用戶端的方法來建立強制回應快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="cb626-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="cb626-108">您也可以在中繼器中使用此控制項。</span><span class="sxs-lookup"><span data-stu-id="cb626-108">It is also possible to use this control within a repeater.</span></span>

## <a name="overview"></a><span data-ttu-id="cb626-109">概觀</span><span class="sxs-lookup"><span data-stu-id="cb626-109">Overview</span></span>

<span data-ttu-id="cb626-110">AJAX 控制項工具組中的 ModalPopup 控制項提供一個簡單的方式，讓您使用用戶端的方法來建立強制回應快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="cb626-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="cb626-111">您也可以在中繼器中使用此控制項。</span><span class="sxs-lookup"><span data-stu-id="cb626-111">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="cb626-112">步驟</span><span class="sxs-lookup"><span data-stu-id="cb626-112">Steps</span></span>

<span data-ttu-id="cb626-113">首先，需要資料來源。</span><span class="sxs-lookup"><span data-stu-id="cb626-113">First of all, a data source is required.</span></span> <span data-ttu-id="cb626-114">這個範例會使用 AdventureWorks 資料庫和 Microsoft SQL Server 2005 Express Edition。</span><span class="sxs-lookup"><span data-stu-id="cb626-114">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="cb626-115">資料庫是 Visual Studio 安裝（包含 express edition）的選擇性部分，而且也可在[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下個別下載。</span><span class="sxs-lookup"><span data-stu-id="cb626-115">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="cb626-116">AdventureWorks 資料庫是 SQL Server 2005 範例和範例資料庫的一部分（下載于[https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)）。</span><span class="sxs-lookup"><span data-stu-id="cb626-116">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="cb626-117">設定資料庫最簡單的方式，就是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)）並附加 `AdventureWorks.mdf` 資料庫檔案。</span><span class="sxs-lookup"><span data-stu-id="cb626-117">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span> <span data-ttu-id="cb626-118">在此範例中，我們假設 SQL Server 2005 Express Edition 的實例呼叫 `SQLEXPRESS` 並與 web 伺服器位於同一部電腦上;這也是預設設定。</span><span class="sxs-lookup"><span data-stu-id="cb626-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="cb626-119">如果您的安裝程式不同，則必須調整資料庫的連接資訊。</span><span class="sxs-lookup"><span data-stu-id="cb626-119">If your setup differs, you have to adapt the connection information for the database.</span></span> <span data-ttu-id="cb626-120">若要啟用 ASP.NET AJAX 和控制項工具組的功能，`ScriptManager` 控制項必須放在頁面上的任何位置（但在 `<form>` 元素內）：</span><span class="sxs-lookup"><span data-stu-id="cb626-120">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-vb/samples/sample1.aspx)]

<span data-ttu-id="cb626-121">然後，將資料來源加入至頁面。</span><span class="sxs-lookup"><span data-stu-id="cb626-121">Then, add a data source to the page.</span></span> <span data-ttu-id="cb626-122">為了使用有限數量的資料，我們只會在 AdventureWorks 資料庫的 [廠商] 資料表中選取前五個專案。</span><span class="sxs-lookup"><span data-stu-id="cb626-122">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="cb626-123">如果您使用 [Visual Studio 小幫手] 來建立資料來源，請注意，目前版本中的 bug 不會在資料表名稱（`Vendor`）前面加上 `Purchasing`的前置詞。</span><span class="sxs-lookup"><span data-stu-id="cb626-123">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="cb626-124">下列標記會顯示正確的語法：</span><span class="sxs-lookup"><span data-stu-id="cb626-124">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-vb/samples/sample2.aspx)]

<span data-ttu-id="cb626-125">接下來，新增可作為強制回應快顯視窗的面板。</span><span class="sxs-lookup"><span data-stu-id="cb626-125">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="cb626-126">它包含 `Button` 控制項，可再次關閉快顯視窗：</span><span class="sxs-lookup"><span data-stu-id="cb626-126">It contains a `Button` control to close the popup again:</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-vb/samples/sample3.aspx)]

<span data-ttu-id="cb626-127">若要在中繼器內進行快顯工作，`ModalPopupExtender` 控制項必須放在中繼器的 `<ItemTemplate>` 區段內。</span><span class="sxs-lookup"><span data-stu-id="cb626-127">In order to make the popup work within the repeater, the `ModalPopupExtender` control must be put within the `<ItemTemplate>` section of the repeater.</span></span> <span data-ttu-id="cb626-128">因此，面板會在中繼器外，但擴充項位於內部。</span><span class="sxs-lookup"><span data-stu-id="cb626-128">So the panel is outside the repeater, but the extender is inside.</span></span> <span data-ttu-id="cb626-129">以下是中繼器的標記：</span><span class="sxs-lookup"><span data-stu-id="cb626-129">Here is the markup for the repeater:</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-vb/samples/sample4.aspx)]

<span data-ttu-id="cb626-130">然後會顯示資料來源中的每個專案，並在其旁邊出現一個按鈕，以觸發強制回應快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="cb626-130">Then, every item in the data source is displayed with a button next to it that triggers the modal popup.</span></span>

<span data-ttu-id="cb626-131">[![可以為每個資料來源專案觸發強制回應快顯視窗](using-modalpopup-with-a-repeater-control-vb/_static/image2.png)](using-modalpopup-with-a-repeater-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="cb626-131">[![The modal popup can be triggered for every data source entry](using-modalpopup-with-a-repeater-control-vb/_static/image2.png)](using-modalpopup-with-a-repeater-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="cb626-132">可以為每個資料來源專案觸發強制回應快顯視窗（[按一下以查看完整大小的影像](using-modalpopup-with-a-repeater-control-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="cb626-132">The modal popup can be triggered for every data source entry ([Click to view full-size image](using-modalpopup-with-a-repeater-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cb626-133">[上一頁](launching-a-modal-popup-window-from-server-code-vb.md)
> [下一頁](handling-postbacks-from-a-modalpopup-vb.md)</span><span class="sxs-lookup"><span data-stu-id="cb626-133">[Previous](launching-a-modal-popup-window-from-server-code-vb.md)
[Next](handling-postbacks-from-a-modalpopup-vb.md)</span></span>
