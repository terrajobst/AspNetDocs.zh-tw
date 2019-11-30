---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
title: 處理沒有 UpdatePanel 的快顯視窗控制項回傳（VB） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 PopupControl 擴充項提供了一種簡單的方式，可在啟用任何其他控制項時觸發快顯。 當 su 中發生回傳時 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a0b9186c-0912-4fff-916a-6d17e696a50b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: aaecf77c1d25f2c99ef4e9948d79fc01b837169b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611707"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-vb"></a><span data-ttu-id="c68f8-104">處理沒有 UpdatePanel 的快顯視窗控制項回傳 (VB)</span><span class="sxs-lookup"><span data-stu-id="c68f8-104">Handling Postbacks from A Popup Control Without an UpdatePanel (VB)</span></span>

<span data-ttu-id="c68f8-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="c68f8-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c68f8-106">[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="c68f8-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)</span></span>

> <span data-ttu-id="c68f8-107">AJAX 控制項工具組中的 PopupControl 擴充項提供了一種簡單的方式，可在啟用任何其他控制項時觸發快顯。</span><span class="sxs-lookup"><span data-stu-id="c68f8-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="c68f8-108">當這類面板中發生回傳，而且頁面上有數個面板時，很難判斷已按下哪一個面板。</span><span class="sxs-lookup"><span data-stu-id="c68f8-108">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="overview"></a><span data-ttu-id="c68f8-109">概觀</span><span class="sxs-lookup"><span data-stu-id="c68f8-109">Overview</span></span>

<span data-ttu-id="c68f8-110">AJAX 控制項工具組中的 PopupControl 擴充項提供了一種簡單的方式，可在啟用任何其他控制項時觸發快顯。</span><span class="sxs-lookup"><span data-stu-id="c68f8-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="c68f8-111">當這類面板中發生回傳，而且頁面上有數個面板時，很難判斷已按下哪一個面板。</span><span class="sxs-lookup"><span data-stu-id="c68f8-111">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="steps"></a><span data-ttu-id="c68f8-112">步驟</span><span class="sxs-lookup"><span data-stu-id="c68f8-112">Steps</span></span>

<span data-ttu-id="c68f8-113">當您使用 `PopupControl` 進行回傳，但是沒有在頁面上有 `UpdatePanel` 時，控制項工具組不會提供方法來判斷哪個用戶端專案已觸發快顯視窗，進而導致回傳。</span><span class="sxs-lookup"><span data-stu-id="c68f8-113">When using a `PopupControl` with a postback, but without having an `UpdatePanel` on the page, the Control Toolkit does not offer a way to determine which client element has triggered the popup which in turn caused the postback.</span></span> <span data-ttu-id="c68f8-114">不過，小技巧提供此案例的因應措施。</span><span class="sxs-lookup"><span data-stu-id="c68f8-114">However a small trick provides a workaround for this scenario.</span></span>

<span data-ttu-id="c68f8-115">首先，以下是基本設定：兩個文字方塊，兩者都會觸發相同的快顯視窗，也就是行事曆。</span><span class="sxs-lookup"><span data-stu-id="c68f8-115">First of all, here is the basic setup: two text boxes which both trigger the same popup, a calendar.</span></span> <span data-ttu-id="c68f8-116">兩個 `PopupControlExtenders` 將文字方塊和快顯一起帶入。</span><span class="sxs-lookup"><span data-stu-id="c68f8-116">Two `PopupControlExtenders` bring text boxes and popup together.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample1.aspx)]

<span data-ttu-id="c68f8-117">基本概念是在 &lt;`form`&gt; 專案中加入隱藏的表單欄位，這些專案會保存啟動快顯視窗的文字方塊：</span><span class="sxs-lookup"><span data-stu-id="c68f8-117">The basic idea is to add a hidden form field in the &lt;`form`&gt; element that holds the text box which launched the popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample2.aspx)]

<span data-ttu-id="c68f8-118">載入頁面時，JavaScript 程式碼會將事件處理常式新增至這兩個文字方塊：每當使用者按一下文字方塊時，其名稱就會寫入隱藏的表單欄位中：</span><span class="sxs-lookup"><span data-stu-id="c68f8-118">When the page is loaded, JavaScript code adds an event handler to both text boxes: Whenever the user clicks on a text box, its name is written into the hidden form field:</span></span>

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample3.html)]

<span data-ttu-id="c68f8-119">在伺服器端程式碼中，必須讀取隱藏欄位的值。</span><span class="sxs-lookup"><span data-stu-id="c68f8-119">In the server-side code, the value of the hidden field must be read.</span></span> <span data-ttu-id="c68f8-120">由於隱藏的表單欄位很容易操作，因此必須使用允許清單驗證隱藏值的白名單方法。</span><span class="sxs-lookup"><span data-stu-id="c68f8-120">Since hidden form fields are trivial to manipulate, a whitelist approach to validate the hidden value is required.</span></span> <span data-ttu-id="c68f8-121">一旦識別出正確的文字方塊之後，就會將行事曆的日期寫入其中。</span><span class="sxs-lookup"><span data-stu-id="c68f8-121">Once the correct text box has been identified, the date from the calendar is written into it.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample4.aspx)]

<span data-ttu-id="c68f8-122">[當使用者按一下文字方塊時，就會顯示行事曆 ![](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c68f8-122">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)</span></span>

<span data-ttu-id="c68f8-123">當使用者按一下文字方塊時，就會出現行事曆（[按一下以查看完整大小的影像](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="c68f8-123">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png))</span></span>

<span data-ttu-id="c68f8-124">[![按一下日期會將它放在文字方塊中](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="c68f8-124">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)</span></span>

<span data-ttu-id="c68f8-125">按一下日期會將它放在文字方塊中（[按一下以查看完整大小的影像](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="c68f8-125">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="c68f8-126">上一篇</span><span class="sxs-lookup"><span data-stu-id="c68f8-126">Previous</span></span>](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)
