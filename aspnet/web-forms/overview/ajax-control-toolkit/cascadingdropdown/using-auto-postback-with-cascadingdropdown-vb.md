---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-vb
title: 使用自動回傳與 CascadingDropDown （VB） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 CascadingDropDown 控制項會擴充 DropDownList 控制項，讓一個 DropDownList 中的變更載入 anoth 中的相關聯值 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0b34f7f6-a0cc-4b9f-9761-643fb0bb3ece
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 5dea23a20aba00af5109f05f18365b89e409a131
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574448"
---
# <a name="using-auto-postback-with-cascadingdropdown-vb"></a><span data-ttu-id="4caee-103">使用自動回傳與 CascadingDropDown (VB)</span><span class="sxs-lookup"><span data-stu-id="4caee-103">Using Auto-Postback with CascadingDropDown (VB)</span></span>

<span data-ttu-id="4caee-104">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="4caee-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="4caee-105">[下載程式代碼](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.vb.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="4caee-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3VB.pdf)</span></span>

> <span data-ttu-id="4caee-106">AJAX 控制項工具組中的 CascadingDropDown 控制項會擴充 DropDownList 控制項，讓一個 DropDownList 中的變更載入另一個 DropDownList 中的關聯值。</span><span class="sxs-lookup"><span data-stu-id="4caee-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="4caee-107">不過，使用 CascadingDropDown 控制項時，ASP。NET 的 DropDownList 控制項的 AutoPostBack 功能無法運作，因為以非同步方式將資料載入清單中會產生（不必要）回傳本身。</span><span class="sxs-lookup"><span data-stu-id="4caee-107">However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="4caee-108">有了一些 JavaScript 程式碼，就可以避免這種效果。</span><span class="sxs-lookup"><span data-stu-id="4caee-108">With some JavaScript code, this effect can be avoided.</span></span>

## <a name="overview"></a><span data-ttu-id="4caee-109">概觀</span><span class="sxs-lookup"><span data-stu-id="4caee-109">Overview</span></span>

<span data-ttu-id="4caee-110">AJAX 控制項工具組中的 CascadingDropDown 控制項會擴充 DropDownList 控制項，讓一個 DropDownList 中的變更載入另一個 DropDownList 中的關聯值。</span><span class="sxs-lookup"><span data-stu-id="4caee-110">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="4caee-111">（例如，一個清單提供美國州的清單，而下一個清單則會填入該州的主要城市）。不過，使用 CascadingDropDown 控制項時，ASP。NET 的 DropDownList 控制項的 AutoPostBack 功能無法運作，因為以非同步方式將資料載入清單中會產生（不必要）回傳本身。</span><span class="sxs-lookup"><span data-stu-id="4caee-111">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="4caee-112">有了一些 JavaScript 程式碼，就可以避免這種效果。</span><span class="sxs-lookup"><span data-stu-id="4caee-112">With some JavaScript code, this effect can be avoided.</span></span>

## <a name="steps"></a><span data-ttu-id="4caee-113">步驟</span><span class="sxs-lookup"><span data-stu-id="4caee-113">Steps</span></span>

<span data-ttu-id="4caee-114">若要啟用 ASP.NET AJAX 和控制項工具組的功能，必須將 `ScriptManager` 控制項放在頁面上的任何位置（但在 &lt;`form`&gt; 專案中）：</span><span class="sxs-lookup"><span data-stu-id="4caee-114">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample1.aspx)]

<span data-ttu-id="4caee-115">然後，需要 DropDownList 控制項：</span><span class="sxs-lookup"><span data-stu-id="4caee-115">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample2.aspx)]

<span data-ttu-id="4caee-116">針對這份清單，會加入 CascadingDropDown 擴充項，並提供 web 服務 URL 和方法資訊：</span><span class="sxs-lookup"><span data-stu-id="4caee-116">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample3.aspx)]

<span data-ttu-id="4caee-117">然後，CascadingDropDown 擴充項會以非同步方式呼叫具有下列方法簽章的 web 服務：</span><span class="sxs-lookup"><span data-stu-id="4caee-117">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-vb[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample4.vb)]

<span data-ttu-id="4caee-118">方法會傳回 CascadingDropDown 數值型別的陣列。</span><span class="sxs-lookup"><span data-stu-id="4caee-118">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="4caee-119">類型的函式需要先有清單專案的標題，然後才是值（HTML `value` 屬性）。</span><span class="sxs-lookup"><span data-stu-id="4caee-119">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample5.aspx)]

<span data-ttu-id="4caee-120">在瀏覽器中載入頁面，會在下拉式清單中填入三個廠商，第二個是預先選取的。</span><span class="sxs-lookup"><span data-stu-id="4caee-120">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span> <span data-ttu-id="4caee-121">此外，ASP.NET 也會定義 `__doPostBack()` 的 JavaScript 方法。</span><span class="sxs-lookup"><span data-stu-id="4caee-121">Also, ASP.NET defines the `__doPostBack()` JavaScript method.</span></span> <span data-ttu-id="4caee-122">載入頁面之後，此 JavaScript 呼叫就會新增至下拉式清單，但只有在其中有元素時才會加入。</span><span class="sxs-lookup"><span data-stu-id="4caee-122">Once the page has been loaded, this JavaScript call is added to the dropdown list, but only if there are elements in it.</span></span> <span data-ttu-id="4caee-123">如果清單中沒有任何專案，則控制項工具組目前正在載入它們，因此 JavaScript 程式碼會使用超時，並在半秒後再試一次。</span><span class="sxs-lookup"><span data-stu-id="4caee-123">If there are no elements in the list, the Control Toolkit is currently loading them, so the JavaScript code uses a timeout and tries again in a half second.</span></span>

[!code-html[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample6.html)]

<span data-ttu-id="4caee-124">如此一來，只有在清單中有實際元素，且使用者選取專案時，才會執行回傳。</span><span class="sxs-lookup"><span data-stu-id="4caee-124">This way, a postback is only executed when there are actually elements in the list and the user selects an entry.</span></span>

<span data-ttu-id="4caee-125">[選取清單元素 ![會導致回傳](using-auto-postback-with-cascadingdropdown-vb/_static/image2.png)](using-auto-postback-with-cascadingdropdown-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4caee-125">[![Selecting a list element causes a postback](using-auto-postback-with-cascadingdropdown-vb/_static/image2.png)](using-auto-postback-with-cascadingdropdown-vb/_static/image1.png)</span></span>

<span data-ttu-id="4caee-126">選取清單元素會導致回傳（[按一下以查看完整大小的影像](using-auto-postback-with-cascadingdropdown-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="4caee-126">Selecting a list element causes a postback ([Click to view full-size image](using-auto-postback-with-cascadingdropdown-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4caee-127">上一篇</span><span class="sxs-lookup"><span data-stu-id="4caee-127">Previous</span></span>](presetting-list-entries-with-cascadingdropdown-vb.md)
