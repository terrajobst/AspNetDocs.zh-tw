---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-vb
title: 調整 DropShadow 的 Z 索引（VB） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 DropShadow 控制項會擴充具有陰影的面板。 不過，此陰影有時會與其他控制項衝突，(.。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ecb004b5-82c0-44fb-bcaf-233fffac6195
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-vb
msc.type: authoredcontent
ms.openlocfilehash: 10495a9590ce1f25e9e3fa218ac5144268f50711
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613915"
---
# <a name="adjusting-the-z-index-of-a-dropshadow-vb"></a><span data-ttu-id="dde7e-104">調整 DropShadow 的 Z 軸索引 (VB)</span><span class="sxs-lookup"><span data-stu-id="dde7e-104">Adjusting the Z-Index of a DropShadow (VB)</span></span>

<span data-ttu-id="dde7e-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="dde7e-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="dde7e-106">[下載程式代碼](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.vb.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="dde7e-106">[Download Code](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1VB.pdf)</span></span>

> <span data-ttu-id="dde7e-107">AJAX 控制項工具組中的 DropShadow 控制項會擴充具有陰影的面板。</span><span class="sxs-lookup"><span data-stu-id="dde7e-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="dde7e-108">不過，此陰影有時會與其他控制項衝突，例如 [ASP.NET] 功能表控制項。</span><span class="sxs-lookup"><span data-stu-id="dde7e-108">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="dde7e-109">當功能表項目出現時，它會顯示在投影后方。</span><span class="sxs-lookup"><span data-stu-id="dde7e-109">When a menu entry pops up, it appears behind the drop shadow.</span></span>

## <a name="overview"></a><span data-ttu-id="dde7e-110">概觀</span><span class="sxs-lookup"><span data-stu-id="dde7e-110">Overview</span></span>

<span data-ttu-id="dde7e-111">AJAX 控制項工具組中的 DropShadow 控制項會擴充具有陰影的面板。</span><span class="sxs-lookup"><span data-stu-id="dde7e-111">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="dde7e-112">不過，此陰影有時會與其他控制項衝突，例如 [ASP.NET] 功能表控制項。</span><span class="sxs-lookup"><span data-stu-id="dde7e-112">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="dde7e-113">當功能表項目出現時，它會顯示在投影后方。</span><span class="sxs-lookup"><span data-stu-id="dde7e-113">When a menu entry pops up, it appears behind the drop shadow.</span></span>

## <a name="steps"></a><span data-ttu-id="dde7e-114">步驟</span><span class="sxs-lookup"><span data-stu-id="dde7e-114">Steps</span></span>

<span data-ttu-id="dde7e-115">程式碼會以面板本身開頭，其中包含足夠的文字，讓面板包含足夠的文字來顯示效果：</span><span class="sxs-lookup"><span data-stu-id="dde7e-115">The code commences with the Panel itself, containing enough text so that the panel contains enough text for the effect to be visible:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample1.aspx)]

<span data-ttu-id="dde7e-116">另一個面板會直接放在 `panelShadow` 面板之前。</span><span class="sxs-lookup"><span data-stu-id="dde7e-116">Another panel is placed directly before the `panelShadow` panel.</span></span> <span data-ttu-id="dde7e-117">它包含具有水準方向的功能表，因此功能表項目會出現在 [`dropShadow` 面板] 上方（或而不是：）：</span><span class="sxs-lookup"><span data-stu-id="dde7e-117">It contains a menu with horizontal orientation so that menu entries appear over (or rather: under) the `dropShadow` panel):</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample2.aspx)]

<span data-ttu-id="dde7e-118">然後，新增 `DropShadowExtender`，以使用投影效果擴充 `panelShadow` 面板：</span><span class="sxs-lookup"><span data-stu-id="dde7e-118">Then, the `DropShadowExtender` is added to extend the `panelShadow` panel with a drop shadow effect:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample3.aspx)]

<span data-ttu-id="dde7e-119">最後，ASP.NET AJAX `ScriptManager` 控制項可讓控制工具組正常執行：</span><span class="sxs-lookup"><span data-stu-id="dde7e-119">Finally, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample4.aspx)]

<span data-ttu-id="dde7e-120">當您執行此腳本時，功能表項目會出現在面板底下。</span><span class="sxs-lookup"><span data-stu-id="dde7e-120">When you run this script, the menu entries appear underneath the panel.</span></span> <span data-ttu-id="dde7e-121">不過，功能表會使用 CSS 類別 `panel` 您只需要定義兩個專案，讓元素出現在另一個面板的前方：</span><span class="sxs-lookup"><span data-stu-id="dde7e-121">However the menu uses the CSS class `panel` where you just have to define two things to make elements appear in front of the other panel:</span></span>

- <span data-ttu-id="dde7e-122">相對定位</span><span class="sxs-lookup"><span data-stu-id="dde7e-122">Relative positioning</span></span>
- <span data-ttu-id="dde7e-123">正 z-索引</span><span class="sxs-lookup"><span data-stu-id="dde7e-123">A positive z-index</span></span>

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample5.css)]

<span data-ttu-id="dde7e-124">然後，`DropShadowExtender` 控制項不會與 Menu 控制項有任何較長的衝突。</span><span class="sxs-lookup"><span data-stu-id="dde7e-124">Then, the `DropShadowExtender` control does not conflict any longer with the Menu control.</span></span>

<span data-ttu-id="dde7e-125">[![之前：不顯示功能表項目](adjusting-the-z-index-of-a-dropshadow-vb/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="dde7e-125">[![Before: The menu entry is not visible](adjusting-the-z-index-of-a-dropshadow-vb/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image1.png)</span></span>

<span data-ttu-id="dde7e-126">之前：不會顯示功能表項目（[按一下以查看完整大小的影像](adjusting-the-z-index-of-a-dropshadow-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="dde7e-126">Before: The menu entry is not visible ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-vb/_static/image3.png))</span></span>

<span data-ttu-id="dde7e-127">[![之後：功能表項目出現](adjusting-the-z-index-of-a-dropshadow-vb/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="dde7e-127">[![After: The menu entry appears](adjusting-the-z-index-of-a-dropshadow-vb/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image4.png)</span></span>

<span data-ttu-id="dde7e-128">之後：功能表項目隨即出現（[按一下以觀看完整大小的影像](adjusting-the-z-index-of-a-dropshadow-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="dde7e-128">After: The menu entry appears ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="dde7e-129">[上一頁](manipulating-dropshadow-properties-from-client-code-cs.md)
> [下一頁](manipulating-dropshadow-properties-from-client-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="dde7e-129">[Previous](manipulating-dropshadow-properties-from-client-code-cs.md)
[Next](manipulating-dropshadow-properties-from-client-code-vb.md)</span></span>
