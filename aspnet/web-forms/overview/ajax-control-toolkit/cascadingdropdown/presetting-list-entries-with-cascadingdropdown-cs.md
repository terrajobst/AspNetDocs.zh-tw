---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-cs
title: 使用 CascadingDropDown （C#）預設清單專案 |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 CascadingDropDown 控制項會擴充 DropDownList 控制項，讓一個 DropDownList 中的變更載入 anoth 中的相關聯值 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 04c79748-0f21-4a3b-aba5-e1ce3161c32e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 3bb4a51092534e6fddbd40f868c53c58d12eef2f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78597899"
---
# <a name="presetting-list-entries-with-cascadingdropdown-c"></a><span data-ttu-id="a5e3e-103">使用 CascadingDropDown 預設清單項目 (C#)</span><span class="sxs-lookup"><span data-stu-id="a5e3e-103">Presetting List Entries with CascadingDropDown (C#)</span></span>

<span data-ttu-id="a5e3e-104">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="a5e3e-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a5e3e-105">[下載程式代碼](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.cs.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingDropDown2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="a5e3e-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingDropDown2CS.pdf)</span></span>

> <span data-ttu-id="a5e3e-106">AJAX 控制項工具組中的 CascadingDropDown 控制項會擴充 DropDownList 控制項，讓一個 DropDownList 中的變更載入另一個 DropDownList 中的關聯值。</span><span class="sxs-lookup"><span data-stu-id="a5e3e-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="a5e3e-107">只要有一些程式碼，當資料已動態載入之後，就可以預先選取清單元素。</span><span class="sxs-lookup"><span data-stu-id="a5e3e-107">With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>

## <a name="overview"></a><span data-ttu-id="a5e3e-108">概觀</span><span class="sxs-lookup"><span data-stu-id="a5e3e-108">Overview</span></span>

<span data-ttu-id="a5e3e-109">AJAX 控制項工具組中的 CascadingDropDown 控制項會擴充 DropDownList 控制項，讓一個 DropDownList 中的變更載入另一個 DropDownList 中的關聯值。</span><span class="sxs-lookup"><span data-stu-id="a5e3e-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="a5e3e-110">（例如，一個清單提供美國州的清單，而下一個清單則會填入該州的主要城市）。只要有一些程式碼，當資料已動態載入之後，就可以預先選取清單元素。</span><span class="sxs-lookup"><span data-stu-id="a5e3e-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>

## <a name="steps"></a><span data-ttu-id="a5e3e-111">步驟</span><span class="sxs-lookup"><span data-stu-id="a5e3e-111">Steps</span></span>

<span data-ttu-id="a5e3e-112">若要啟用 ASP.NET AJAX 和控制項工具組的功能，`ScriptManager` 控制項必須放在頁面上的任何位置（但在 `<form>` 元素內）：</span><span class="sxs-lookup"><span data-stu-id="a5e3e-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample1.aspx)]

<span data-ttu-id="a5e3e-113">然後，需要 DropDownList 控制項：</span><span class="sxs-lookup"><span data-stu-id="a5e3e-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample2.aspx)]

<span data-ttu-id="a5e3e-114">針對這份清單，會加入 CascadingDropDown 擴充項，並提供 web 服務 URL 和方法資訊：</span><span class="sxs-lookup"><span data-stu-id="a5e3e-114">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample3.aspx)]

<span data-ttu-id="a5e3e-115">然後，CascadingDropDown 擴充項會以非同步方式呼叫具有下列方法簽章的 web 服務：</span><span class="sxs-lookup"><span data-stu-id="a5e3e-115">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-csharp[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample4.cs)]

<span data-ttu-id="a5e3e-116">方法會傳回 CascadingDropDown 數值型別的陣列。</span><span class="sxs-lookup"><span data-stu-id="a5e3e-116">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="a5e3e-117">類型的函式需要先有清單專案的標題，然後才是值（HTML `value` 屬性）。</span><span class="sxs-lookup"><span data-stu-id="a5e3e-117">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span> <span data-ttu-id="a5e3e-118">如果第三個引數設定為 true，則會在瀏覽器中自動選取清單元素。</span><span class="sxs-lookup"><span data-stu-id="a5e3e-118">If the third argument is set to true, the list element is automatically selected in the browser.</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample5.aspx)]

<span data-ttu-id="a5e3e-119">在瀏覽器中載入頁面，會在下拉式清單中填入三個廠商，第二個是預先選取的。</span><span class="sxs-lookup"><span data-stu-id="a5e3e-119">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span>

<span data-ttu-id="a5e3e-120">[![清單已自動填入和預先選取](presetting-list-entries-with-cascadingdropdown-cs/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a5e3e-120">[![The list is filled and preselected automatically](presetting-list-entries-with-cascadingdropdown-cs/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-cs/_static/image1.png)</span></span>

<span data-ttu-id="a5e3e-121">系統會自動填入並預先選取清單（[按一下以查看完整大小的影像](presetting-list-entries-with-cascadingdropdown-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="a5e3e-121">The list is filled and preselected automatically ([Click to view full-size image](presetting-list-entries-with-cascadingdropdown-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a5e3e-122">[上一頁](using-cascadingdropdown-with-a-database-cs.md)
> [下一頁](using-auto-postback-with-cascadingdropdown-cs.md)</span><span class="sxs-lookup"><span data-stu-id="a5e3e-122">[Previous](using-cascadingdropdown-with-a-database-cs.md)
[Next](using-auto-postback-with-cascadingdropdown-cs.md)</span></span>
