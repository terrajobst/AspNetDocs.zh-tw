---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
title: 處理來自 ModalPopup 的回傳（VB） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 ModalPopup 控制項提供一個簡單的方式，讓您使用用戶端的方法來建立強制回應快顯視窗。 當 pos 時，必須特別注意
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f70ac2b3-900f-40fa-858f-ab057904506b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: df0b71b3e336a0d230869623473bdac24b3dd07b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78621524"
---
# <a name="handling-postbacks-from-a-modalpopup-vb"></a><span data-ttu-id="aaec4-104">處理來自 ModalPopup 的回傳 (VB)</span><span class="sxs-lookup"><span data-stu-id="aaec4-104">Handling Postbacks from a ModalPopup (VB)</span></span>

<span data-ttu-id="aaec4-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="aaec4-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="aaec4-106">[下載程式代碼](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.vb.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="aaec4-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3VB.pdf)</span></span>

> <span data-ttu-id="aaec4-107">AJAX 控制項工具組中的 ModalPopup 控制項提供一個簡單的方式，讓您使用用戶端的方法來建立強制回應快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="aaec4-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="aaec4-108">從快顯視窗內建立回傳時，必須特別小心。</span><span class="sxs-lookup"><span data-stu-id="aaec4-108">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="overview"></a><span data-ttu-id="aaec4-109">概觀</span><span class="sxs-lookup"><span data-stu-id="aaec4-109">Overview</span></span>

<span data-ttu-id="aaec4-110">AJAX 控制項工具組中的 ModalPopup 控制項提供一個簡單的方式，讓您使用用戶端的方法來建立強制回應快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="aaec4-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="aaec4-111">從快顯視窗內建立回傳時，必須特別小心。</span><span class="sxs-lookup"><span data-stu-id="aaec4-111">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="aaec4-112">步驟</span><span class="sxs-lookup"><span data-stu-id="aaec4-112">Steps</span></span>

<span data-ttu-id="aaec4-113">若要啟用 ASP.NET AJAX 和控制項工具組的功能，`ScriptManager` 控制項必須放在頁面上的任何位置（但在 `<form>` 元素內）：</span><span class="sxs-lookup"><span data-stu-id="aaec4-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample1.aspx)]

<span data-ttu-id="aaec4-114">接下來，新增可作為強制回應快顯視窗的面板。</span><span class="sxs-lookup"><span data-stu-id="aaec4-114">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="aaec4-115">使用者可以在那裡輸入名稱和電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="aaec4-115">There, the user can enter a name and an email address.</span></span> <span data-ttu-id="aaec4-116">按鈕可用來關閉快顯視窗並儲存資訊。</span><span class="sxs-lookup"><span data-stu-id="aaec4-116">A button is used to close the popup and save the information.</span></span> <span data-ttu-id="aaec4-117">請注意，[`OnClick`] 屬性已設定為按一下這個按鈕時，就會發生回傳：</span><span class="sxs-lookup"><span data-stu-id="aaec4-117">Note that the `OnClick` attribute is set so that a postback occurs when this button is clicked:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample2.aspx)]

<span data-ttu-id="aaec4-118">頁面本身包含兩個標籤，以取得完全相同的資訊：名稱和電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="aaec4-118">The page itself consists of two labels for exactly the same information: name and email address.</span></span> <span data-ttu-id="aaec4-119">按鈕可用來觸發強制回應快顯視窗：</span><span class="sxs-lookup"><span data-stu-id="aaec4-119">A button is used to trigger the modal popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample3.aspx)]

<span data-ttu-id="aaec4-120">若要顯示快顯視窗，請加入 `ModalPopupExtender` 控制項。</span><span class="sxs-lookup"><span data-stu-id="aaec4-120">In order to make the popup appear, add the `ModalPopupExtender` control.</span></span> <span data-ttu-id="aaec4-121">將 `PopupControlID` 屬性設為面板的識別碼，並 `TargetControlID` 至按鈕的識別碼：</span><span class="sxs-lookup"><span data-stu-id="aaec4-121">Set the `PopupControlID` attribute to the panel's ID and `TargetControlID` to the button's ID:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample4.aspx)]

<span data-ttu-id="aaec4-122">現在只要按一下強制回應快顯視窗中的 [`Save`] 按鈕，就會執行伺服器端 `SaveData()` 方法。</span><span class="sxs-lookup"><span data-stu-id="aaec4-122">Now whenever the `Save` button within the modal popup is clicked, the server-side `SaveData()` method is executed.</span></span> <span data-ttu-id="aaec4-123">在這裡，您可以將輸入的資料儲存在資料存放區中。</span><span class="sxs-lookup"><span data-stu-id="aaec4-123">There, you could save the entered data in a data store.</span></span> <span data-ttu-id="aaec4-124">為了簡單起見，新資料只會輸出在標籤中：</span><span class="sxs-lookup"><span data-stu-id="aaec4-124">For the sake of simplicity, the new data is just output in the label:</span></span>

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample5.vb)]

<span data-ttu-id="aaec4-125">此外，強制回應快顯視窗中的 textbox 控制項應該填入目前的名稱和電子郵件。</span><span class="sxs-lookup"><span data-stu-id="aaec4-125">Also, the textbox controls within the modal popup should be filled with the current name and email.</span></span> <span data-ttu-id="aaec4-126">不過，只有在沒有發生回傳時，才需要這麼做。</span><span class="sxs-lookup"><span data-stu-id="aaec4-126">However this is only necessary when no postback occurs.</span></span> <span data-ttu-id="aaec4-127">如果有回傳，ASP.NET viewstate 功能會自動以適當的值填滿文字方塊。</span><span class="sxs-lookup"><span data-stu-id="aaec4-127">If there is a postback, the ASP.NET viewstate feature will automatically fill the textboxes with the appropriate values.</span></span>

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample6.vb)]

<span data-ttu-id="aaec4-128">[![強制回應快顯視窗會導致回傳](handling-postbacks-from-a-modalpopup-vb/_static/image2.png)](handling-postbacks-from-a-modalpopup-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="aaec4-128">[![The modal popup causes a postback](handling-postbacks-from-a-modalpopup-vb/_static/image2.png)](handling-postbacks-from-a-modalpopup-vb/_static/image1.png)</span></span>

<span data-ttu-id="aaec4-129">強制回應快顯視窗會導致回傳（[按一下以查看完整大小的影像](handling-postbacks-from-a-modalpopup-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="aaec4-129">The modal popup causes a postback ([Click to view full-size image](handling-postbacks-from-a-modalpopup-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="aaec4-130">[上一頁](using-modalpopup-with-a-repeater-control-vb.md)
> [下一頁](positioning-a-modalpopup-vb.md)</span><span class="sxs-lookup"><span data-stu-id="aaec4-130">[Previous](using-modalpopup-with-a-repeater-control-vb.md)
[Next](positioning-a-modalpopup-vb.md)</span></span>
