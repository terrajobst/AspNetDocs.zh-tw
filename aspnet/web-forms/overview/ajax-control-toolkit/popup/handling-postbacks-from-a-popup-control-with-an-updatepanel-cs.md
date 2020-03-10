---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
title: 使用 UpdatePanel （C#）處理 Popup 控制項的回傳 |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 PopupControl 擴充項提供了一種簡單的方式，可在啟用任何其他控制項時觸發快顯。 必須特別小心 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1f68f59d-9c1e-4cf3-b304-c13ae6b7203e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 8b9e58d68b3d6c5d01ceaba6c01653e9574b541b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78612928"
---
# <a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-c"></a><span data-ttu-id="c0ed7-104">處理有 UpdatePanel 的快顯視窗控制項回傳 (C#)</span><span class="sxs-lookup"><span data-stu-id="c0ed7-104">Handling Postbacks from A Popup Control With an UpdatePanel (C#)</span></span>

<span data-ttu-id="c0ed7-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="c0ed7-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c0ed7-106">[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.cs.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="c0ed7-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2CS.pdf)</span></span>

> <span data-ttu-id="c0ed7-107">AJAX 控制項工具組中的 PopupControl 擴充項提供了一種簡單的方式，可在啟用任何其他控制項時觸發快顯。</span><span class="sxs-lookup"><span data-stu-id="c0ed7-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="c0ed7-108">當回傳發生在這類快顯視窗內時，必須特別小心。</span><span class="sxs-lookup"><span data-stu-id="c0ed7-108">Special care has to be taken when a postback occurs within such a popup.</span></span>

## <a name="overview"></a><span data-ttu-id="c0ed7-109">概觀</span><span class="sxs-lookup"><span data-stu-id="c0ed7-109">Overview</span></span>

<span data-ttu-id="c0ed7-110">AJAX 控制項工具組中的 PopupControl 擴充項提供了一種簡單的方式，可在啟用任何其他控制項時觸發快顯。</span><span class="sxs-lookup"><span data-stu-id="c0ed7-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="c0ed7-111">當回傳發生在這類快顯視窗內時，必須特別小心。</span><span class="sxs-lookup"><span data-stu-id="c0ed7-111">Special care has to be taken when a postback occurs within such a popup.</span></span>

## <a name="steps"></a><span data-ttu-id="c0ed7-112">步驟</span><span class="sxs-lookup"><span data-stu-id="c0ed7-112">Steps</span></span>

<span data-ttu-id="c0ed7-113">當使用 `PopupControl` 與回傳時，`UpdatePanel` 可以防止回傳所造成的頁面重新整理。</span><span class="sxs-lookup"><span data-stu-id="c0ed7-113">When using a `PopupControl` with a postback, an `UpdatePanel` can prevent the page refresh caused by the postback.</span></span> <span data-ttu-id="c0ed7-114">下列標記會定義幾個重要的元素：</span><span class="sxs-lookup"><span data-stu-id="c0ed7-114">The following markup defines a couple of important elements:</span></span>

- <span data-ttu-id="c0ed7-115">`ScriptManager` 控制項，讓 ASP.NET AJAX 控制項工具組可以運作</span><span class="sxs-lookup"><span data-stu-id="c0ed7-115">A `ScriptManager` control so that the ASP.NET AJAX Control Toolkit works</span></span>
- <span data-ttu-id="c0ed7-116">兩個 `TextBox` 控制項都會觸發快顯視窗</span><span class="sxs-lookup"><span data-stu-id="c0ed7-116">Two `TextBox` controls which will both trigger a popup</span></span>
- <span data-ttu-id="c0ed7-117">將作為快顯的 `Panel` 控制項</span><span class="sxs-lookup"><span data-stu-id="c0ed7-117">A `Panel` control that will serve as the popup</span></span>
- <span data-ttu-id="c0ed7-118">在面板中，`Calendar` 控制項內嵌在 `UpdatePanel` 控制項內</span><span class="sxs-lookup"><span data-stu-id="c0ed7-118">Within the panel, a `Calendar` control is embedded within an `UpdatePanel` control</span></span>
- <span data-ttu-id="c0ed7-119">兩個 `PopupControlExtender` 控制項，可將面板指派給文字方塊</span><span class="sxs-lookup"><span data-stu-id="c0ed7-119">Two `PopupControlExtender` controls that assign the panel to the text boxes</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample1.aspx)]

<span data-ttu-id="c0ed7-120">請注意，已設定 `Calendar` 控制項的 `OnSelectionChanged` 屬性。</span><span class="sxs-lookup"><span data-stu-id="c0ed7-120">Note that the `OnSelectionChanged` attribute of the `Calendar` control is set.</span></span> <span data-ttu-id="c0ed7-121">因此當使用者選取行事曆內的日期時，就會發生回傳，而且會執行伺服器端方法 `c1_SelectionChanged()`。</span><span class="sxs-lookup"><span data-stu-id="c0ed7-121">So when the user selects a date within the calendar, a postback occurs and the server-side method `c1_SelectionChanged()` is executed.</span></span> <span data-ttu-id="c0ed7-122">在該方法中，必須取出目前的日期，並將其寫回文字方塊。</span><span class="sxs-lookup"><span data-stu-id="c0ed7-122">Within that method, the current date must be retrieved and written back to the textbox.</span></span>

<span data-ttu-id="c0ed7-123">的語法如下：首先，必須在頁面上產生 `PopupControlExtender` 的 proxy 物件。</span><span class="sxs-lookup"><span data-stu-id="c0ed7-123">The syntax for that is as follows: First of all, a proxy object for the `PopupControlExtender` on the page must be generated.</span></span> <span data-ttu-id="c0ed7-124">ASP.NET AJAX Control 工具組提供 `GetProxyForCurrentPopup()` 方法。</span><span class="sxs-lookup"><span data-stu-id="c0ed7-124">The ASP.NET AJAX Control Toolkit offers the `GetProxyForCurrentPopup()` method.</span></span> <span data-ttu-id="c0ed7-125">這個方法傳回的物件支援 `Commit()` 方法，其會將值傳回給觸發快顯視窗的控制項（而不是觸發方法呼叫的控制項！）。</span><span class="sxs-lookup"><span data-stu-id="c0ed7-125">The object this method returns supports the `Commit()` method which sends a value back to the control that triggered the popup (not the control that triggered the method call!).</span></span> <span data-ttu-id="c0ed7-126">下列程式碼會提供選取的日期做為 `Commit()` 方法的引數，使程式碼將選取的日期寫回文字方塊：</span><span class="sxs-lookup"><span data-stu-id="c0ed7-126">The following code provides the selected date as the argument for the `Commit()` method, causing the code to write the selected date back to the text box:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample2.aspx)]

<span data-ttu-id="c0ed7-127">現在當您按一下行事曆日期時，所選取的日期會出現在相關聯的文字方塊中，建立目前可在許多網站上找到的日期選擇器控制項。</span><span class="sxs-lookup"><span data-stu-id="c0ed7-127">Now whenever you click on a calendar date, the selected date appears in the associated text box, creating a date picker control that can currently be found on many websites.</span></span>

<span data-ttu-id="c0ed7-128">[當使用者按一下文字方塊時，就會顯示行事曆 ![](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c0ed7-128">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image1.png)</span></span>

<span data-ttu-id="c0ed7-129">當使用者按一下文字方塊時，就會出現行事曆（[按一下以查看完整大小的影像](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="c0ed7-129">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image3.png))</span></span>

<span data-ttu-id="c0ed7-130">[![按一下日期會將它放在文字方塊中](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="c0ed7-130">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image4.png)</span></span>

<span data-ttu-id="c0ed7-131">按一下日期會將它放在文字方塊中（[按一下以查看完整大小的影像](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="c0ed7-131">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c0ed7-132">[上一頁](using-multiple-popup-controls-cs.md)
> [下一頁](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)</span><span class="sxs-lookup"><span data-stu-id="c0ed7-132">[Previous](using-multiple-popup-controls-cs.md)
[Next](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)</span></span>
