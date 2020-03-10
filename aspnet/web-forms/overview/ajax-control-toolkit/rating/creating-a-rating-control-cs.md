---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
title: 建立評等控制項（C#） |Microsoft Docs
author: wenz
description: 許多網站（從電子商務到社區網站）提供使用者對文章或專案進行評分。 這通常需要一些編碼工作，但我們有 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 969fb28f-2bff-4fc4-b24a-27f5e2534a37
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
msc.type: authoredcontent
ms.openlocfilehash: c0bf793406e378321f54f0460031c526a0b41a02
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78612340"
---
# <a name="creating-a-rating-control-c"></a><span data-ttu-id="461af-104">建立評等控制項 (C#)</span><span class="sxs-lookup"><span data-stu-id="461af-104">Creating a Rating Control (C#)</span></span>

<span data-ttu-id="461af-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="461af-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="461af-106">[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="461af-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span></span>

> <span data-ttu-id="461af-107">許多網站（從電子商務到社區網站）提供使用者對文章或專案進行評分。</span><span class="sxs-lookup"><span data-stu-id="461af-107">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="461af-108">這通常需要一些程式碼撰寫工作，但我們會將控制工具組提供給我們的處置。</span><span class="sxs-lookup"><span data-stu-id="461af-108">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>

## <a name="overview"></a><span data-ttu-id="461af-109">概觀</span><span class="sxs-lookup"><span data-stu-id="461af-109">Overview</span></span>

<span data-ttu-id="461af-110">許多網站（從電子商務到社區網站）提供使用者對文章或專案進行評分。</span><span class="sxs-lookup"><span data-stu-id="461af-110">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="461af-111">這通常需要一些程式碼撰寫工作，但我們會將控制工具組提供給我們的處置。</span><span class="sxs-lookup"><span data-stu-id="461af-111">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>

## <a name="steps"></a><span data-ttu-id="461af-112">步驟</span><span class="sxs-lookup"><span data-stu-id="461af-112">Steps</span></span>

<span data-ttu-id="461af-113">首先，您需要（至少）兩種影像：一個用於已填滿的評等專案，另一個則用於空的評等專案。</span><span class="sxs-lookup"><span data-stu-id="461af-113">First of all, you need (at least) two kinds of images: one for a filled out rating item, and one for an empty rating item.</span></span> <span data-ttu-id="461af-114">評等專案通常是星星或笑臉。</span><span class="sxs-lookup"><span data-stu-id="461af-114">A rating item is usually a star or a smiley.</span></span> <span data-ttu-id="461af-115">在此案例中，您會在本教學課程的原始程式碼下載中找到三個檔案，笑臉和空白 .png 和 smiley-done。</span><span class="sxs-lookup"><span data-stu-id="461af-115">For this scenario, you find three files, smiley.png and empty.png and smiley-done.png as part of the source code downloads for this tutorial.</span></span>

<span data-ttu-id="461af-116">然後，建立新的 ASP.NET 檔案，並開始在其中加入 `ScriptManager` 控制項：</span><span class="sxs-lookup"><span data-stu-id="461af-116">Then, create a new ASP.NET file and start with adding a `ScriptManager` control to it:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample1.aspx)]

<span data-ttu-id="461af-117">然後，從 ASP.NET AJAX 控制項工具組加入 `Rating` 控制項。</span><span class="sxs-lookup"><span data-stu-id="461af-117">Then, add the `Rating` control from the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="461af-118">您必須針對此範例設定下列屬性：</span><span class="sxs-lookup"><span data-stu-id="461af-118">The following attributes need to be set for this example:</span></span>

- <span data-ttu-id="461af-119">`CurrentRating` 要使用的初始評等</span><span class="sxs-lookup"><span data-stu-id="461af-119">`CurrentRating` the initial rating to be used</span></span>
- <span data-ttu-id="461af-120">`MaxRating` 最大評等</span><span class="sxs-lookup"><span data-stu-id="461af-120">`MaxRating` the maximum rating</span></span>
- <span data-ttu-id="461af-121">`EmptyStarCssClass` 在評等專案（星號）為空白時所要使用的 CSS 類別</span><span class="sxs-lookup"><span data-stu-id="461af-121">`EmptyStarCssClass` the CSS class to use when a rating item ( star ) is empty</span></span>
- <span data-ttu-id="461af-122">`FilledStarCssClass` 填寫評等專案（星星）時要使用的 CSS 類別</span><span class="sxs-lookup"><span data-stu-id="461af-122">`FilledStarCssClass` the CSS class to use when a rating item ( star ) is filled out</span></span>
- <span data-ttu-id="461af-123">`StarCssClass` 要用於可見狀態的 CSS 類別</span><span class="sxs-lookup"><span data-stu-id="461af-123">`StarCssClass` the CSS class to use for a visible stat</span></span>
- <span data-ttu-id="461af-124">`WaitingStarCssClass` 在將星級評等傳送回伺服器時所要使用的 CSS 類別</span><span class="sxs-lookup"><span data-stu-id="461af-124">`WaitingStarCssClass` the CSS class to use while a star rating is sent back to the server</span></span>

<span data-ttu-id="461af-125">以下的標記會建立具有五個專案的評等控制項（smileys），一開始不填寫：</span><span class="sxs-lookup"><span data-stu-id="461af-125">And here is the markup which creates a rating control with five items (smileys) of which none is filled out initially:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample2.aspx)]

<span data-ttu-id="461af-126">這三個參考的 CSS 類別現在需要顯示適當的影像檔案，這很容易使用 CSS 來執行：</span><span class="sxs-lookup"><span data-stu-id="461af-126">The three referenced CSS classes now need to show the appropriate image files, which is easy to do using CSS:</span></span>

[!code-css[Main](creating-a-rating-control-cs/samples/sample3.css)]

<span data-ttu-id="461af-127">請確定您提供三個影像的寬度和高度，否則顯示的外觀可能會需要操作。</span><span class="sxs-lookup"><span data-stu-id="461af-127">Make sure that you provide the width and height of the three images, otherwise the display may look a bit messed up.</span></span>

<span data-ttu-id="461af-128">最後，評等的結果應該會向使用者顯示（或至少儲存在資料庫中）。</span><span class="sxs-lookup"><span data-stu-id="461af-128">Finally, the result of the rating should be displayed to the user (or, at least saved in a database).</span></span> <span data-ttu-id="461af-129">因此，請為文字訊息的輸出新增標籤，並使用 [提交] 按鈕將評等表單回傳至伺服器：</span><span class="sxs-lookup"><span data-stu-id="461af-129">So add a label for the output of a text message and a submit button to post back the rating form to the server:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample4.aspx)]

<span data-ttu-id="461af-130">在伺服器端程式碼中，透過其 `ID` 存取評等控制項，然後存取其 `CurrentRating` 屬性，這是所選評等專案的數目，在範例中是介於0和5之間的值。</span><span class="sxs-lookup"><span data-stu-id="461af-130">In the server-side code, access the Rating control via its `ID` and then access its `CurrentRating` property which is the number of the selected rating items, in our example a value between 0 and 5.</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample5.aspx)]

<span data-ttu-id="461af-131">儲存頁面，並將它載入瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="461af-131">Save the page and load it into your browser.</span></span> <span data-ttu-id="461af-132">當您將滑鼠停留在（一開始是空的）評等專案時，就會發生 JavaScript 效果：評等會變更。</span><span class="sxs-lookup"><span data-stu-id="461af-132">When you hover over the (initially empty) rating items, a JavaScript effect occurs: The rating changes.</span></span> <span data-ttu-id="461af-133">當您按一下一組星星時，會保留目前的評等。</span><span class="sxs-lookup"><span data-stu-id="461af-133">When you click on the set of stars, the current rating is retained.</span></span> <span data-ttu-id="461af-134">最後，當您提交表單時，伺服器端程式碼會輸出選取的評等。</span><span class="sxs-lookup"><span data-stu-id="461af-134">Finally, when you submit the form, the server-side code outputs the selected rating.</span></span>

<span data-ttu-id="461af-135">[![以最少的程式碼建立評等系統](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="461af-135">[![Creating a rating system with minimal code](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="461af-136">以最少的程式碼建立分級系統（[按一下以觀看完整大小的影像](creating-a-rating-control-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="461af-136">Creating a rating system with minimal code ([Click to view full-size image](creating-a-rating-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="461af-137">下一個</span><span class="sxs-lookup"><span data-stu-id="461af-137">Next</span></span>](creating-a-rating-control-vb.md)
