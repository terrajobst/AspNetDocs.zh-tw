---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
title: 處理沒有 UpdatePanel (C#) 的快顯視窗控制項回傳 |Microsoft Docs
author: wenz
description: PopupControl 擴充項在 AJAX Control Toolkit 提供簡單的方式，來啟動任何其他控制項時，觸發快顯視窗。 當發生回傳時 su 中...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25444121-5a72-4dac-8e50-ad2b7ac667af
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 06713aaf84ecfa5a793c32e3762cb4790235bf8c
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59385991"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-c"></a><span data-ttu-id="317d6-104">處理沒有 UpdatePanel 的快顯視窗控制項回傳 (C#)</span><span class="sxs-lookup"><span data-stu-id="317d6-104">Handling Postbacks from A Popup Control Without an UpdatePanel (C#)</span></span>

<span data-ttu-id="317d6-105">藉由[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="317d6-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="317d6-106">[下載程式碼](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip)或[下載 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="317d6-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)</span></span>

> <span data-ttu-id="317d6-107">PopupControl 擴充項在 AJAX Control Toolkit 提供簡單的方式，來啟動任何其他控制項時，觸發快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="317d6-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="317d6-108">回傳，就會發生這類面板中，並在頁面上有數個面板時很難判斷按下的面板。</span><span class="sxs-lookup"><span data-stu-id="317d6-108">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>


## <a name="overview"></a><span data-ttu-id="317d6-109">總覽</span><span class="sxs-lookup"><span data-stu-id="317d6-109">Overview</span></span>

<span data-ttu-id="317d6-110">PopupControl 擴充項在 AJAX Control Toolkit 提供簡單的方式，來啟動任何其他控制項時，觸發快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="317d6-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="317d6-111">回傳，就會發生這類面板中，並在頁面上有數個面板時很難判斷按下的面板。</span><span class="sxs-lookup"><span data-stu-id="317d6-111">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="steps"></a><span data-ttu-id="317d6-112">步驟</span><span class="sxs-lookup"><span data-stu-id="317d6-112">Steps</span></span>

<span data-ttu-id="317d6-113">使用時`PopupControl`回傳，但無須`UpdatePanel`在頁面上，Control Toolkit 並未提供一個方式來判斷哪一個用戶端項目已觸發的快顯視窗接著造成回傳。</span><span class="sxs-lookup"><span data-stu-id="317d6-113">When using a `PopupControl` with a postback, but without having an `UpdatePanel` on the page, the Control Toolkit does not offer a way to determine which client element has triggered the popup which in turn caused the postback.</span></span> <span data-ttu-id="317d6-114">不過小秘訣提供此案例的因應措施。</span><span class="sxs-lookup"><span data-stu-id="317d6-114">However a small trick provides a workaround for this scenario.</span></span>

<span data-ttu-id="317d6-115">首先，以下是基本安裝： 這兩個觸發程序相同的快顯行事曆的兩個文字方塊。</span><span class="sxs-lookup"><span data-stu-id="317d6-115">First of all, here is the basic setup: two text boxes which both trigger the same popup, a calendar.</span></span> <span data-ttu-id="317d6-116">兩個`PopupControlExtenders`結合文字方塊和快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="317d6-116">Two `PopupControlExtenders` bring text boxes and popup together.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample1.aspx)]

<span data-ttu-id="317d6-117">基本構想是將隱藏的表單欄位中加入&lt; `form` &gt;保留啟動快顯文字方塊中的項目：</span><span class="sxs-lookup"><span data-stu-id="317d6-117">The basic idea is to add a hidden form field in the &lt;`form`&gt; element that holds the text box which launched the popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample2.aspx)]

<span data-ttu-id="317d6-118">載入頁面時，JavaScript 程式碼會在兩個文字方塊中加入事件處理常式：每當使用者按一下文字方塊上時，會將其名稱寫入隱藏的表單欄位：</span><span class="sxs-lookup"><span data-stu-id="317d6-118">When the page is loaded, JavaScript code adds an event handler to both text boxes: Whenever the user clicks on a text box, its name is written into the hidden form field:</span></span>

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample3.html)]

<span data-ttu-id="317d6-119">在伺服器端程式碼中，您必須讀取隱藏欄位的值。</span><span class="sxs-lookup"><span data-stu-id="317d6-119">In the server-side code, the value of the hidden field must be read.</span></span> <span data-ttu-id="317d6-120">隱藏的表單欄位是 trivial 操作，因為驗證隱藏的值的允許清單方法需要。</span><span class="sxs-lookup"><span data-stu-id="317d6-120">Since hidden form fields are trivial to manipulate, a whitelist approach to validate the hidden value is required.</span></span> <span data-ttu-id="317d6-121">一旦已識別正確的文字方塊中，從行事曆的日期會寫入到其中。</span><span class="sxs-lookup"><span data-stu-id="317d6-121">Once the correct text box has been identified, the date from the calendar is written into it.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample4.aspx)]


[![T<span data-ttu-id="317d6-122">他的行事曆會顯示當使用者按一下 [文字方塊]</span><span class="sxs-lookup"><span data-stu-id="317d6-122">he Calendar appears when the user clicks into the textbox]</span></span>(handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image1.png)

<span data-ttu-id="317d6-123">當使用者按一下文字方塊，即出現日曆 ([按一下以檢視完整大小的影像](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="317d6-123">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png))</span></span>


[![C<span data-ttu-id="317d6-124">按一下某個日期會將它放在文字方塊]</span><span class="sxs-lookup"><span data-stu-id="317d6-124">licking on a date puts it in the textbox]</span></span>(handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image4.png)

<span data-ttu-id="317d6-125">按一下某個日期將它放在文字方塊中 ([按一下以檢視完整大小的影像](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="317d6-125">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="317d6-126">[上一頁](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
> [下一頁](using-multiple-popup-controls-vb.md)</span><span class="sxs-lookup"><span data-stu-id="317d6-126">[Previous](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
[Next](using-multiple-popup-controls-vb.md)</span></span>
