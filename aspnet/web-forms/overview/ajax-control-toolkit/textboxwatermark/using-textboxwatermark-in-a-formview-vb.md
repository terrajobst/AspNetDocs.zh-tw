---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-vb
title: 在 FormView 中使用 TextBoxWatermark （VB） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 TextBoxWatermark 控制項會擴充一個文字方塊，讓文字顯示在方塊中。 當使用者按一下方塊時，我 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 41497361-7fba-4825-b36c-f58d79522a88
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-vb
msc.type: authoredcontent
ms.openlocfilehash: 1dd17ed57383680122c4ca613ca71f6682dec40e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598325"
---
# <a name="using-textboxwatermark-in-a-formview-vb"></a><span data-ttu-id="c1742-104">在 FormView 中使用 TextBoxWatermark (VB)</span><span class="sxs-lookup"><span data-stu-id="c1742-104">Using TextBoxWatermark in a FormView (VB)</span></span>

<span data-ttu-id="c1742-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="c1742-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c1742-106">[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.vb.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="c1742-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1VB.pdf)</span></span>

> <span data-ttu-id="c1742-107">AJAX 控制項工具組中的 TextBoxWatermark 控制項會擴充一個文字方塊，讓文字顯示在方塊中。</span><span class="sxs-lookup"><span data-stu-id="c1742-107">The TextBoxWatermark control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="c1742-108">當使用者按一下方塊時，就會清空。</span><span class="sxs-lookup"><span data-stu-id="c1742-108">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="c1742-109">如果使用者離開方塊而不輸入文字，預先填入的文字就會重新出現。</span><span class="sxs-lookup"><span data-stu-id="c1742-109">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="c1742-110">這也可以在 FormView 控制項內使用。</span><span class="sxs-lookup"><span data-stu-id="c1742-110">This is also possible within a FormView control.</span></span>

## <a name="overview"></a><span data-ttu-id="c1742-111">概觀</span><span class="sxs-lookup"><span data-stu-id="c1742-111">Overview</span></span>

<span data-ttu-id="c1742-112">AJAX 控制項工具組中的 `TextBoxWatermark` 控制項會擴充一個文字方塊，讓文字顯示在方塊中。</span><span class="sxs-lookup"><span data-stu-id="c1742-112">The `TextBoxWatermark` control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="c1742-113">當使用者按一下方塊時，就會清空。</span><span class="sxs-lookup"><span data-stu-id="c1742-113">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="c1742-114">如果使用者離開方塊而不輸入文字，預先填入的文字就會重新出現。</span><span class="sxs-lookup"><span data-stu-id="c1742-114">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="c1742-115">這也可以在 `FormView` 控制項內進行。</span><span class="sxs-lookup"><span data-stu-id="c1742-115">This is also possible within a `FormView` control.</span></span>

## <a name="steps"></a><span data-ttu-id="c1742-116">步驟</span><span class="sxs-lookup"><span data-stu-id="c1742-116">Steps</span></span>

<span data-ttu-id="c1742-117">首先，需要資料來源。</span><span class="sxs-lookup"><span data-stu-id="c1742-117">First of all, a data source is required.</span></span> <span data-ttu-id="c1742-118">這個範例會使用 AdventureWorks 資料庫和 Microsoft SQL Server 2005 Express Edition。</span><span class="sxs-lookup"><span data-stu-id="c1742-118">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="c1742-119">資料庫是 Visual Studio 安裝（包含 express edition）的選擇性部分，而且也可在[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下個別下載。</span><span class="sxs-lookup"><span data-stu-id="c1742-119">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="c1742-120">AdventureWorks 資料庫是 SQL Server 2005 範例和範例資料庫的一部分（下載于[https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)）。</span><span class="sxs-lookup"><span data-stu-id="c1742-120">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="c1742-121">設定資料庫最簡單的方式，就是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)）並附加 `AdventureWorks.mdf` 資料庫檔案。</span><span class="sxs-lookup"><span data-stu-id="c1742-121">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="c1742-122">在此範例中，我們假設 SQL Server 2005 Express Edition 的實例呼叫 `SQLEXPRESS` 並與 web 伺服器位於同一部電腦上;這也是預設設定。</span><span class="sxs-lookup"><span data-stu-id="c1742-122">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="c1742-123">如果您的安裝程式不同，則必須調整資料庫的連接資訊。</span><span class="sxs-lookup"><span data-stu-id="c1742-123">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="c1742-124">若要啟用 ASP.NET AJAX 和控制項工具組的功能，`ScriptManager` 控制項必須放在頁面上的任何位置（但在 `<form>` 元素內）：</span><span class="sxs-lookup"><span data-stu-id="c1742-124">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample1.aspx)]

<span data-ttu-id="c1742-125">然後，將資料來源加入至支援 `DELETE`、`INSERT` 和 `UPDATE` SQL 語句的頁面。</span><span class="sxs-lookup"><span data-stu-id="c1742-125">Then, add a data source to the page which supports the `DELETE`, `INSERT` and `UPDATE` SQL statements.</span></span> <span data-ttu-id="c1742-126">如果您使用 [Visual Studio 小幫手] 來建立資料來源，請注意，目前版本中的 bug 不會在資料表名稱（`Vendor`）前面加上 `Purchasing`的前置詞。</span><span class="sxs-lookup"><span data-stu-id="c1742-126">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="c1742-127">下列標記會顯示正確的語法：</span><span class="sxs-lookup"><span data-stu-id="c1742-127">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample2.aspx)]

<span data-ttu-id="c1742-128">請記住資料來源的名稱（`ID`），因為它將在 `FormView` 控制項的 `DataSourceID` 屬性中使用。</span><span class="sxs-lookup"><span data-stu-id="c1742-128">Remember the name (`ID`) of the data source, since it will be used in the `DataSourceID` property of the `FormView` control.</span></span> <span data-ttu-id="c1742-129">`FormView` 的 [`<InsertItemTemplate>`] 區段包含 [`TextBoxWatermarkExtender`] 控制項所延伸的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="c1742-129">The `<InsertItemTemplate>` section of the `FormView` contains a textbox which is extended by the `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="c1742-130">請確定擴充項位於範本中，而不在其外部。</span><span class="sxs-lookup"><span data-stu-id="c1742-130">Make sure that the extender resides within the template and not outside of it.</span></span>

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample3.aspx)]

<span data-ttu-id="c1742-131">現在當使用者變更為 `FormView` 控制項的插入模式時，新廠商的文字欄位會預先填入 `TextBoxWatermarkExtender` 控制項。</span><span class="sxs-lookup"><span data-stu-id="c1742-131">Now when the user changes into the insert mode of the `FormView` control, the text field for the new vendor is prefilled thanks to the `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="c1742-132">在文字方塊內按一下可讓填充文字消失。</span><span class="sxs-lookup"><span data-stu-id="c1742-132">A click inside the textbox lets the filler text disappear.</span></span>

<span data-ttu-id="c1742-133">[![欄位中的浮水印來自于擴充項](using-textboxwatermark-in-a-formview-vb/_static/image2.png)](using-textboxwatermark-in-a-formview-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c1742-133">[![The watermark in the field comes from the extender](using-textboxwatermark-in-a-formview-vb/_static/image2.png)](using-textboxwatermark-in-a-formview-vb/_static/image1.png)</span></span>

<span data-ttu-id="c1742-134">欄位中的浮水印來自于擴充項（[按一下以查看完整大小的影像](using-textboxwatermark-in-a-formview-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="c1742-134">The watermark in the field comes from the extender ([Click to view full-size image](using-textboxwatermark-in-a-formview-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c1742-135">[上一頁](using-textboxwatermark-with-validation-controls-cs.md)
> [下一頁](using-textboxwatermark-with-validation-controls-vb.md)</span><span class="sxs-lookup"><span data-stu-id="c1742-135">[Previous](using-textboxwatermark-with-validation-controls-cs.md)
[Next](using-textboxwatermark-with-validation-controls-vb.md)</span></span>
