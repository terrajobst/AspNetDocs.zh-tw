---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
title: 從伺服器端修改動畫（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 動畫也可能是 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: addcf4aa-340a-460b-9c64-506424a1f725
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
msc.type: authoredcontent
ms.openlocfilehash: ebc311d1a931ad611d9556799c94440d41a9cf49
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575223"
---
# <a name="modifying-animations-from-the-server-side-vb"></a><span data-ttu-id="f248d-104">從伺服器端修改動畫（VB）</span><span class="sxs-lookup"><span data-stu-id="f248d-104">Modifying Animations From The Server Side (VB)</span></span>

<span data-ttu-id="f248d-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f248d-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f248d-106">[下載程式代碼](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="f248d-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)</span></span>

> <span data-ttu-id="f248d-107">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="f248d-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="f248d-108">伺服器端上的動畫也可能會變更</span><span class="sxs-lookup"><span data-stu-id="f248d-108">The animations may also be changed on the server-side</span></span>

## <a name="overview"></a><span data-ttu-id="f248d-109">概觀</span><span class="sxs-lookup"><span data-stu-id="f248d-109">Overview</span></span>

<span data-ttu-id="f248d-110">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="f248d-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="f248d-111">伺服器端上的動畫也可能會變更</span><span class="sxs-lookup"><span data-stu-id="f248d-111">The animations may also be changed on the server-side</span></span>

## <a name="steps"></a><span data-ttu-id="f248d-112">步驟</span><span class="sxs-lookup"><span data-stu-id="f248d-112">Steps</span></span>

<span data-ttu-id="f248d-113">首先，在頁面中包含 `ScriptManager`;然後，會載入 ASP.NET AJAX 程式庫，讓您能夠使用控制項工具組：</span><span class="sxs-lookup"><span data-stu-id="f248d-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample1.aspx)]

<span data-ttu-id="f248d-114">動畫將會套用至文字的面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f248d-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample2.aspx)]

<span data-ttu-id="f248d-115">在面板的相關聯 CSS 類別中，定義良好的背景色彩，同時設定面板的固定寬度：</span><span class="sxs-lookup"><span data-stu-id="f248d-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](modifying-animations-from-the-server-side-vb/samples/sample3.css)]

<span data-ttu-id="f248d-116">其餘的程式碼會在伺服器端執行，而且不會使用標記;相反地，它會使用程式碼來建立 `AnimationExtender` 控制項：</span><span class="sxs-lookup"><span data-stu-id="f248d-116">The rest of the code runs on the server-side and does not use markup; instead, it uses code to create the `AnimationExtender` control:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample4.aspx)]

<span data-ttu-id="f248d-117">不過，控制項工具組目前並未提供 API 存取權來建立個別的動畫。</span><span class="sxs-lookup"><span data-stu-id="f248d-117">However, the Control Toolkit currently does not provide an API access to create the individual animations.</span></span> <span data-ttu-id="f248d-118">不過，您可以將 `AnimationExtender`的動畫屬性設定為字串，其中包含以宣告方式指派動畫時所使用的 XML 標記。</span><span class="sxs-lookup"><span data-stu-id="f248d-118">It is however possible to set the `AnimationExtender`'s Animations property to a string containing the XML markup used when assigning the animations declaratively.</span></span> <span data-ttu-id="f248d-119">若要建立不能包含 `<Animations>` 元素的 XML，您可以使用 .NET Framework 的 XML 支援或，如下列程式碼所示，只需提供字串：</span><span class="sxs-lookup"><span data-stu-id="f248d-119">In order to create the XML which must not contain the `<Animations>` element you could use the .NET Framework's XML support or, as in the following code, just provide the string:</span></span>

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample5.vb)]

<span data-ttu-id="f248d-120">最後，將 `AnimationExtender` 控制項加入至目前頁面的 `<form runat="server">` 元素內，確保動畫已包含並執行：</span><span class="sxs-lookup"><span data-stu-id="f248d-120">Finally, add the `AnimationExtender` control to the current page, within the `<form runat="server">` element, making sure that the animation is included and runs:</span></span>

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample6.vb)]

<span data-ttu-id="f248d-121">[![使用伺服器端C#/VB 程式碼建立動畫](modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f248d-121">[![The animation is created using server-side C#/VB code](modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)</span></span>

<span data-ttu-id="f248d-122">動畫是使用伺服器端C#的/VB 程式碼（[按一下以查看完整大小的影像](modifying-animations-from-the-server-side-vb/_static/image3.png)）所建立</span><span class="sxs-lookup"><span data-stu-id="f248d-122">The animation is created using server-side C#/VB code ([Click to view full-size image](modifying-animations-from-the-server-side-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f248d-123">[上一頁](triggering-an-animation-in-another-control-vb.md)
> [下一頁](executing-animations-using-client-side-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="f248d-123">[Previous](triggering-an-animation-in-another-control-vb.md)
[Next](executing-animations-using-client-side-code-vb.md)</span></span>
