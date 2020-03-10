---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
title: 建立互斥的核取方塊（VB） |Microsoft Docs
author: wenz
description: 只有一組選項可以選取時，通常會使用選項按鈕。 但有一個缺點，就是在選取群組中的一個選項按鈕之後,。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e9dd1d5a-a1db-4114-981d-6a91acb1d709
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
msc.type: authoredcontent
ms.openlocfilehash: f33936dd4d71f6bbf08f02966eefe44c8c152eba
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554009"
---
# <a name="creating-mutually-exclusive-checkboxes-vb"></a><span data-ttu-id="5e2c2-104">建立互斥的核取方塊 (VB)</span><span class="sxs-lookup"><span data-stu-id="5e2c2-104">Creating Mutually Exclusive Checkboxes (VB)</span></span>

<span data-ttu-id="5e2c2-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="5e2c2-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="5e2c2-106">[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="5e2c2-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)</span></span>

> <span data-ttu-id="5e2c2-107">只有一組選項可以選取時，通常會使用選項按鈕。</span><span class="sxs-lookup"><span data-stu-id="5e2c2-107">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="5e2c2-108">但有一個缺點：選取群組中的一個選項按鈕之後，就無法取消核取所有選項按鈕。</span><span class="sxs-lookup"><span data-stu-id="5e2c2-108">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="5e2c2-109">您可以隨時取消核取核取方塊，但不會互斥。</span><span class="sxs-lookup"><span data-stu-id="5e2c2-109">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="5e2c2-110">本教學課程提供兩種方法的最佳選擇：彼此互斥的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="5e2c2-110">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="overview"></a><span data-ttu-id="5e2c2-111">概觀</span><span class="sxs-lookup"><span data-stu-id="5e2c2-111">Overview</span></span>

<span data-ttu-id="5e2c2-112">只有一組選項可以選取時，通常會使用選項按鈕。</span><span class="sxs-lookup"><span data-stu-id="5e2c2-112">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="5e2c2-113">但有一個缺點：選取群組中的一個選項按鈕之後，就無法取消核取所有選項按鈕。</span><span class="sxs-lookup"><span data-stu-id="5e2c2-113">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="5e2c2-114">您可以隨時取消核取核取方塊，但不會互斥。</span><span class="sxs-lookup"><span data-stu-id="5e2c2-114">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="5e2c2-115">本教學課程提供兩種方法的最佳選擇：彼此互斥的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="5e2c2-115">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="steps"></a><span data-ttu-id="5e2c2-116">步驟</span><span class="sxs-lookup"><span data-stu-id="5e2c2-116">Steps</span></span>

<span data-ttu-id="5e2c2-117">ASP.NET AJAX Control 工具組包含 MutuallyExclusiveCheckBox 擴充項。</span><span class="sxs-lookup"><span data-stu-id="5e2c2-117">The ASP.NET AJAX Control Toolkit contains the MutuallyExclusiveCheckBox extender.</span></span> <span data-ttu-id="5e2c2-118">這可讓程式設計人員將任何核取方塊指派給組名（`Key` 屬性）。</span><span class="sxs-lookup"><span data-stu-id="5e2c2-118">This enables programmers to assign any checkbox to a group name (`Key` attribute).</span></span> <span data-ttu-id="5e2c2-119">從相同群組中的所有核取方塊，一次只能選取一個。</span><span class="sxs-lookup"><span data-stu-id="5e2c2-119">From all check boxes within the same group, only one may be selected at one time.</span></span>

<span data-ttu-id="5e2c2-120">讓我們從將兩個核取方塊放在新的 ASP.NET 網頁開始。</span><span class="sxs-lookup"><span data-stu-id="5e2c2-120">Let's start with putting two check boxes on a new ASP.NET page.</span></span> <span data-ttu-id="5e2c2-121">有更多，但其中兩個都足以展示原則：</span><span class="sxs-lookup"><span data-stu-id="5e2c2-121">There can be more, but two of them suffice to demonstrate the principle:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample1.aspx)]

<span data-ttu-id="5e2c2-122">對於這兩個核取方塊，MutuallyExclusiveCheckBoxExtender 控制項都必須放在頁面上。</span><span class="sxs-lookup"><span data-stu-id="5e2c2-122">For both checkboxes, a MutuallyExclusiveCheckBoxExtender control must be put on the page.</span></span> <span data-ttu-id="5e2c2-123">這兩個索引鍵屬性都必須具有相同的值，就像 [HTML] 選項按鈕元素的 [值] 屬性一樣，表示它們所屬的群組。</span><span class="sxs-lookup"><span data-stu-id="5e2c2-123">Both Key attributes need to have the same value, just as the value attributes of HTML radio button elements must be identical to denote the group they belong to.</span></span> <span data-ttu-id="5e2c2-124">擴充項的 TargetControlID 屬性會指向核取方塊的識別碼。</span><span class="sxs-lookup"><span data-stu-id="5e2c2-124">The TargetControlID property of the extender points to the ID of the check box.</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample2.aspx)]

<span data-ttu-id="5e2c2-125">最後，包含 ASP.NET AJAX 控制項工具組的所有元素所需的 ASP.NET AJAX `ScriptManager`：</span><span class="sxs-lookup"><span data-stu-id="5e2c2-125">Finally, include the ASP.NET AJAX `ScriptManager` which is required by all elements of the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample3.aspx)]

<span data-ttu-id="5e2c2-126">儲存並執行頁面：您可以勾選和取消核取這兩個核取方塊，不過，您無法同時選取這兩個核取方塊。</span><span class="sxs-lookup"><span data-stu-id="5e2c2-126">Save and run the page: You can check and uncheck both check boxes, however at no time can both check boxes be checked.</span></span>

<span data-ttu-id="5e2c2-127">[一次只能檢查一個核取方塊 ![](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5e2c2-127">[![Only one checkbox can be checked at a time](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)</span></span>

<span data-ttu-id="5e2c2-128">一次只能檢查一個核取方塊（[按一下以查看完整大小的影像](creating-mutually-exclusive-checkboxes-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="5e2c2-128">Only one checkbox can be checked at a time ([Click to view full-size image](creating-mutually-exclusive-checkboxes-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="5e2c2-129">上一篇</span><span class="sxs-lookup"><span data-stu-id="5e2c2-129">Previous</span></span>](creating-mutually-exclusive-checkboxes-cs.md)
