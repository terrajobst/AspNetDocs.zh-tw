---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-vb
title: 動態加入 [可折疊] 窗格（VB） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 [可折疊式] 控制項提供多個窗格，並允許使用者一次顯示其中一項。 面板通常會宣告為 w 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: fae968c9-1902-487d-b053-86a46dd52c3f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-vb
msc.type: authoredcontent
ms.openlocfilehash: be48db5ea3de4af46b0f864cc9e73d2f518294a4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607186"
---
# <a name="dynamically-adding-an-accordion-pane-vb"></a><span data-ttu-id="07fa5-104">動態新增 [可折疊式] 窗格（VB）</span><span class="sxs-lookup"><span data-stu-id="07fa5-104">Dynamically Adding An Accordion Pane (VB)</span></span>

<span data-ttu-id="07fa5-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="07fa5-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="07fa5-106">[下載程式代碼](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.vb.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="07fa5-106">[Download Code](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2VB.pdf)</span></span>

> <span data-ttu-id="07fa5-107">AJAX 控制項工具組中的 [可折疊式] 控制項提供多個窗格，並允許使用者一次顯示其中一項。</span><span class="sxs-lookup"><span data-stu-id="07fa5-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="07fa5-108">面板通常會在頁面本身內宣告，但伺服器端程式碼可以用來達到相同的結果。</span><span class="sxs-lookup"><span data-stu-id="07fa5-108">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="overview"></a><span data-ttu-id="07fa5-109">概觀</span><span class="sxs-lookup"><span data-stu-id="07fa5-109">Overview</span></span>

<span data-ttu-id="07fa5-110">AJAX 控制項工具組中的 [可折疊式] 控制項提供多個窗格，並允許使用者一次顯示其中一項。</span><span class="sxs-lookup"><span data-stu-id="07fa5-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="07fa5-111">面板通常會在頁面本身內宣告，但伺服器端程式碼可以用來達到相同的結果。</span><span class="sxs-lookup"><span data-stu-id="07fa5-111">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="steps"></a><span data-ttu-id="07fa5-112">步驟</span><span class="sxs-lookup"><span data-stu-id="07fa5-112">Steps</span></span>

<span data-ttu-id="07fa5-113">[可折疊] 控制項會公開所有重要的屬性給伺服器端程式碼。</span><span class="sxs-lookup"><span data-stu-id="07fa5-113">The Accordion control exposes all important properties to server-side code.</span></span> <span data-ttu-id="07fa5-114">除此之外，`Panes` 屬性也會授與組成可折疊性之窗格集合的存取權。</span><span class="sxs-lookup"><span data-stu-id="07fa5-114">Among other things, the `Panes` property grants access to the collection of panes that make up the Accordion.</span></span> <span data-ttu-id="07fa5-115">每個窗格都有 `AccordionPane`類型。</span><span class="sxs-lookup"><span data-stu-id="07fa5-115">Every pane there is of type `AccordionPane`.</span></span> <span data-ttu-id="07fa5-116">因此，建立這種窗格是很簡單的：</span><span class="sxs-lookup"><span data-stu-id="07fa5-116">It is therefore trivial to create such a pane:</span></span>

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample1.vb)]

<span data-ttu-id="07fa5-117">`AccordionPane` 的 `HeaderContainer` 屬性，可讓您存取窗格的標頭區段內的 ASP.NET 控制項;`AccordionPane` 的 `ContentContainer` 屬性會對窗格的 [內容] 區段執行相同的工作。</span><span class="sxs-lookup"><span data-stu-id="07fa5-117">The `HeaderContainer` property of `AccordionPane` provides access to the ASP.NET controls within the header section of the pane; the `ContentContainer` property of `AccordionPane` does the same for the content section of the pane.</span></span> <span data-ttu-id="07fa5-118">這可讓 ASP.NET 程式碼將內容新增至窗格：</span><span class="sxs-lookup"><span data-stu-id="07fa5-118">This allows ASP.NET code to add content to the panes:</span></span>

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample2.vb)]

<span data-ttu-id="07fa5-119">最後，您必須將窗格新增至可折疊的 `Panes` 集合：</span><span class="sxs-lookup"><span data-stu-id="07fa5-119">Finally, the pane(s) must be added to the `Panes` collection of the Accordion:</span></span>

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample3.vb)]

<span data-ttu-id="07fa5-120">以下是完整的伺服器端程式碼，它會將兩個窗格加入至 [可折疊] 控制項：</span><span class="sxs-lookup"><span data-stu-id="07fa5-120">Here is a complete server-side code that adds two panes to an Accordion control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-vb/samples/sample4.aspx)]

<span data-ttu-id="07fa5-121">唯一缺少的元素是可折疊性本身，這取決於 ASP.NET `ScriptManager` 控制項是否存在：</span><span class="sxs-lookup"><span data-stu-id="07fa5-121">The only missing element is the Accordion itself, which depends on the presence of the ASP.NET `ScriptManager` control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-vb/samples/sample5.aspx)]

<span data-ttu-id="07fa5-122">若要完成此範例，在 [可折疊] 控制項中參考的兩個 CSS 類別會提供瀏覽器的樣式資訊：</span><span class="sxs-lookup"><span data-stu-id="07fa5-122">To finish the example, the two CSS classes referenced in the Accordion control provide style information for the browser:</span></span>

[!code-css[Main](dynamically-adding-an-accordion-pane-vb/samples/sample6.css)]

<span data-ttu-id="07fa5-123">[![伺服器端程式碼會以動態方式新增可折疊的資料](dynamically-adding-an-accordion-pane-vb/_static/image2.png)](dynamically-adding-an-accordion-pane-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="07fa5-123">[![The data in the accordion was dynamically added by server-side code](dynamically-adding-an-accordion-pane-vb/_static/image2.png)](dynamically-adding-an-accordion-pane-vb/_static/image1.png)</span></span>

<span data-ttu-id="07fa5-124">伺服器端程式碼會以動態方式新增可折疊顯示的資料（[按一下以觀看完整大小的影像](dynamically-adding-an-accordion-pane-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="07fa5-124">The data in the accordion was dynamically added by server-side code ([Click to view full-size image](dynamically-adding-an-accordion-pane-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="07fa5-125">上一篇</span><span class="sxs-lookup"><span data-stu-id="07fa5-125">Previous</span></span>](databinding-to-an-accordion-vb.md)
