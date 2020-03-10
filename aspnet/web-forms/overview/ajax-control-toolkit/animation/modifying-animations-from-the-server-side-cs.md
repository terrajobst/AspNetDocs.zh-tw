---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-cs
title: 從伺服器端修改動畫（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 動畫也可能是 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b0abec39-a1c9-422d-ba9a-ef16f6185af8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-cs
msc.type: authoredcontent
ms.openlocfilehash: 0594efea9598a6c2461a72f789b5bd5f8ece23da
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598025"
---
# <a name="modifying-animations-from-the-server-side-c"></a><span data-ttu-id="cf4e1-104">從伺服器端修改動畫（C#）</span><span class="sxs-lookup"><span data-stu-id="cf4e1-104">Modifying Animations From The Server Side (C#)</span></span>

<span data-ttu-id="cf4e1-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="cf4e1-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="cf4e1-106">[下載程式代碼](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.cs.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="cf4e1-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9CS.pdf)</span></span>

> <span data-ttu-id="cf4e1-107">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="cf4e1-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="cf4e1-108">伺服器端上的動畫也可能會變更</span><span class="sxs-lookup"><span data-stu-id="cf4e1-108">The animations may also be changed on the server-side</span></span>

## <a name="overview"></a><span data-ttu-id="cf4e1-109">概觀</span><span class="sxs-lookup"><span data-stu-id="cf4e1-109">Overview</span></span>

<span data-ttu-id="cf4e1-110">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="cf4e1-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="cf4e1-111">伺服器端上的動畫也可能會變更</span><span class="sxs-lookup"><span data-stu-id="cf4e1-111">The animations may also be changed on the server-side</span></span>

## <a name="steps"></a><span data-ttu-id="cf4e1-112">步驟</span><span class="sxs-lookup"><span data-stu-id="cf4e1-112">Steps</span></span>

<span data-ttu-id="cf4e1-113">首先，在頁面中包含 `ScriptManager`;然後，會載入 ASP.NET AJAX 程式庫，讓您能夠使用控制項工具組：</span><span class="sxs-lookup"><span data-stu-id="cf4e1-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample1.aspx)]

<span data-ttu-id="cf4e1-114">動畫將會套用至文字的面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="cf4e1-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample2.aspx)]

<span data-ttu-id="cf4e1-115">在面板的相關聯 CSS 類別中，定義良好的背景色彩，同時設定面板的固定寬度：</span><span class="sxs-lookup"><span data-stu-id="cf4e1-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](modifying-animations-from-the-server-side-cs/samples/sample3.css)]

<span data-ttu-id="cf4e1-116">其餘的程式碼會在伺服器端執行，而且不會使用標記;相反地，它會使用程式碼來建立 `AnimationExtender` 控制項：</span><span class="sxs-lookup"><span data-stu-id="cf4e1-116">The rest of the code runs on the server-side and does not use markup; instead, it uses code to create the `AnimationExtender` control:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample4.aspx)]

<span data-ttu-id="cf4e1-117">不過，控制項工具組目前並未提供 API 存取權來建立個別的動畫。</span><span class="sxs-lookup"><span data-stu-id="cf4e1-117">However, the Control Toolkit currently does not provide an API access to create the individual animations.</span></span> <span data-ttu-id="cf4e1-118">不過，您可以將 `AnimationExtender`的動畫屬性設定為字串，其中包含以宣告方式指派動畫時所使用的 XML 標記。</span><span class="sxs-lookup"><span data-stu-id="cf4e1-118">It is however possible to set the `AnimationExtender`'s Animations property to a string containing the XML markup used when assigning the animations declaratively.</span></span> <span data-ttu-id="cf4e1-119">若要建立不能包含 `<Animations>` 元素的 XML，您可以使用 .NET Framework 的 XML 支援或，如下列程式碼所示，只需提供字串：</span><span class="sxs-lookup"><span data-stu-id="cf4e1-119">In order to create the XML which must not contain the `<Animations>` element you could use the .NET Framework's XML support or, as in the following code, just provide the string:</span></span>

[!code-css[Main](modifying-animations-from-the-server-side-cs/samples/sample5.css)]

<span data-ttu-id="cf4e1-120">最後，將 `AnimationExtender` 控制項加入至目前頁面的 `<form runat="server">` 元素內，確保動畫已包含並執行：</span><span class="sxs-lookup"><span data-stu-id="cf4e1-120">Finally, add the `AnimationExtender` control to the current page, within the `<form runat="server">` element, making sure that the animation is included and runs:</span></span>

[!code-html[Main](modifying-animations-from-the-server-side-cs/samples/sample6.html)]

<span data-ttu-id="cf4e1-121">[![使用伺服器端C#/VB 程式碼建立動畫](modifying-animations-from-the-server-side-cs/_static/image2.png)](modifying-animations-from-the-server-side-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="cf4e1-121">[![The animation is created using server-side C#/VB code](modifying-animations-from-the-server-side-cs/_static/image2.png)](modifying-animations-from-the-server-side-cs/_static/image1.png)</span></span>

<span data-ttu-id="cf4e1-122">動畫是使用伺服器端C#的/VB 程式碼（[按一下以查看完整大小的影像](modifying-animations-from-the-server-side-cs/_static/image3.png)）所建立</span><span class="sxs-lookup"><span data-stu-id="cf4e1-122">The animation is created using server-side C#/VB code ([Click to view full-size image](modifying-animations-from-the-server-side-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cf4e1-123">[上一頁](triggering-an-animation-in-another-control-cs.md)
> [下一頁](executing-animations-using-client-side-code-cs.md)</span><span class="sxs-lookup"><span data-stu-id="cf4e1-123">[Previous](triggering-an-animation-in-another-control-cs.md)
[Next](executing-animations-using-client-side-code-cs.md)</span></span>
