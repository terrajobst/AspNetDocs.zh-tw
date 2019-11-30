---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
title: 動態加入可折疊式窗格C#（） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 [可折疊式] 控制項提供多個窗格，並允許使用者一次顯示其中一項。 面板通常會宣告為 w 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 66d88cfa-f26f-46b1-ad52-1c9e03c04a48
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
msc.type: authoredcontent
ms.openlocfilehash: 2834f56bd77c412923f4a8f382e670727f70eae4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607225"
---
# <a name="dynamically-adding-an-accordion-pane-c"></a><span data-ttu-id="a8e28-104">動態新增 [可折疊式C#] 窗格（）</span><span class="sxs-lookup"><span data-stu-id="a8e28-104">Dynamically Adding An Accordion Pane (C#)</span></span>

<span data-ttu-id="a8e28-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="a8e28-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a8e28-106">[下載程式代碼](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="a8e28-106">[Download Code](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)</span></span>

> <span data-ttu-id="a8e28-107">AJAX 控制項工具組中的 [可折疊式] 控制項提供多個窗格，並允許使用者一次顯示其中一項。</span><span class="sxs-lookup"><span data-stu-id="a8e28-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="a8e28-108">面板通常會在頁面本身內宣告，但伺服器端程式碼可以用來達到相同的結果。</span><span class="sxs-lookup"><span data-stu-id="a8e28-108">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="overview"></a><span data-ttu-id="a8e28-109">概觀</span><span class="sxs-lookup"><span data-stu-id="a8e28-109">Overview</span></span>

<span data-ttu-id="a8e28-110">AJAX 控制項工具組中的 [可折疊式] 控制項提供多個窗格，並允許使用者一次顯示其中一項。</span><span class="sxs-lookup"><span data-stu-id="a8e28-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="a8e28-111">面板通常會在頁面本身內宣告，但伺服器端程式碼可以用來達到相同的結果。</span><span class="sxs-lookup"><span data-stu-id="a8e28-111">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="steps"></a><span data-ttu-id="a8e28-112">步驟</span><span class="sxs-lookup"><span data-stu-id="a8e28-112">Steps</span></span>

<span data-ttu-id="a8e28-113">[可折疊] 控制項會公開所有重要的屬性給伺服器端程式碼。</span><span class="sxs-lookup"><span data-stu-id="a8e28-113">The Accordion control exposes all important properties to server-side code.</span></span> <span data-ttu-id="a8e28-114">除此之外，`Panes` 屬性也會授與組成可折疊性之窗格集合的存取權。</span><span class="sxs-lookup"><span data-stu-id="a8e28-114">Among other things, the `Panes` property grants access to the collection of panes that make up the Accordion.</span></span> <span data-ttu-id="a8e28-115">每個窗格都有 `AccordionPane`類型。</span><span class="sxs-lookup"><span data-stu-id="a8e28-115">Every pane there is of type `AccordionPane`.</span></span> <span data-ttu-id="a8e28-116">因此，建立這種窗格是很簡單的：</span><span class="sxs-lookup"><span data-stu-id="a8e28-116">It is therefore trivial to create such a pane:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample1.cs)]

<span data-ttu-id="a8e28-117">`AccordionPane` 的 `HeaderContainer` 屬性，可讓您存取窗格的標頭區段內的 ASP.NET 控制項;`AccordionPane` 的 `ContentContainer` 屬性會對窗格的 [內容] 區段執行相同的工作。</span><span class="sxs-lookup"><span data-stu-id="a8e28-117">The `HeaderContainer` property of `AccordionPane` provides access to the ASP.NET controls within the header section of the pane; the `ContentContainer` property of `AccordionPane` does the same for the content section of the pane.</span></span> <span data-ttu-id="a8e28-118">這可讓 ASP.NET 程式碼將內容新增至窗格：</span><span class="sxs-lookup"><span data-stu-id="a8e28-118">This allows ASP.NET code to add content to the panes:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample2.cs)]

<span data-ttu-id="a8e28-119">最後，您必須將窗格新增至可折疊的 `Panes` 集合：</span><span class="sxs-lookup"><span data-stu-id="a8e28-119">Finally, the pane(s) must be added to the `Panes` collection of the Accordion:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample3.cs)]

<span data-ttu-id="a8e28-120">以下是完整的伺服器端程式碼，它會將兩個窗格加入至 [可折疊] 控制項：</span><span class="sxs-lookup"><span data-stu-id="a8e28-120">Here is a complete server-side code that adds two panes to an Accordion control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample4.aspx)]

<span data-ttu-id="a8e28-121">唯一缺少的元素是可折疊性本身，這取決於 ASP.NET `ScriptManager` 控制項是否存在：</span><span class="sxs-lookup"><span data-stu-id="a8e28-121">The only missing element is the Accordion itself, which depends on the presence of the ASP.NET `ScriptManager` control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample5.aspx)]

<span data-ttu-id="a8e28-122">若要完成此範例，在 [可折疊] 控制項中參考的兩個 CSS 類別會提供瀏覽器的樣式資訊：</span><span class="sxs-lookup"><span data-stu-id="a8e28-122">To finish the example, the two CSS classes referenced in the Accordion control provide style information for the browser:</span></span>

[!code-css[Main](dynamically-adding-an-accordion-pane-cs/samples/sample6.css)]

<span data-ttu-id="a8e28-123">[![伺服器端程式碼會以動態方式新增可折疊的資料](dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a8e28-123">[![The data in the accordion was dynamically added by server-side code](dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)</span></span>

<span data-ttu-id="a8e28-124">伺服器端程式碼會以動態方式新增可折疊顯示的資料（[按一下以觀看完整大小的影像](dynamically-adding-an-accordion-pane-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="a8e28-124">The data in the accordion was dynamically added by server-side code ([Click to view full-size image](dynamically-adding-an-accordion-pane-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a8e28-125">[上一頁](databinding-to-an-accordion-cs.md)
> [下一頁](databinding-to-an-accordion-vb.md)</span><span class="sxs-lookup"><span data-stu-id="a8e28-125">[Previous](databinding-to-an-accordion-cs.md)
[Next](databinding-to-an-accordion-vb.md)</span></span>
