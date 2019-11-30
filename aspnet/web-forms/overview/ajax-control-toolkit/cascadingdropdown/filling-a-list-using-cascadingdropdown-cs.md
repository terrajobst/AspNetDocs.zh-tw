---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
title: 使用 CascadingDropDown （C#）填入清單 |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 CascadingDropDown 控制項會擴充 DropDownList 控制項，讓一個 DropDownList 中的變更載入 anoth 中的相關聯值 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f949aafa-fe57-43b0-b722-f0dd33a900be
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: b5e9874fb5b6d3e55c8af5b85d12bf1ffacc116b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574825"
---
# <a name="filling-a-list-using-cascadingdropdown-c"></a><span data-ttu-id="168c9-103">使用 CascadingDropDown 填滿清單 (C#)</span><span class="sxs-lookup"><span data-stu-id="168c9-103">Filling a List Using CascadingDropDown (C#)</span></span>

<span data-ttu-id="168c9-104">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="168c9-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="168c9-105">[下載程式代碼](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="168c9-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)</span></span>

> <span data-ttu-id="168c9-106">AJAX 控制項工具組中的 CascadingDropDown 控制項會擴充 DropDownList 控制項，讓一個 DropDownList 中的變更載入另一個 DropDownList 中的關聯值。</span><span class="sxs-lookup"><span data-stu-id="168c9-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="168c9-107">（例如，一個清單提供美國州的清單，而下一個清單則會填入該州的主要城市）。首先要解決的挑戰是使用這個控制項來實際填寫下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="168c9-107">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="overview"></a><span data-ttu-id="168c9-108">概觀</span><span class="sxs-lookup"><span data-stu-id="168c9-108">Overview</span></span>

<span data-ttu-id="168c9-109">AJAX 控制項工具組中的 CascadingDropDown 控制項會擴充 DropDownList 控制項，讓一個 DropDownList 中的變更載入另一個 DropDownList 中的關聯值。</span><span class="sxs-lookup"><span data-stu-id="168c9-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="168c9-110">（例如，一個清單提供美國州的清單，而下一個清單則會填入該州的主要城市）。首先要解決的挑戰是使用這個控制項來實際填寫下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="168c9-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="steps"></a><span data-ttu-id="168c9-111">步驟</span><span class="sxs-lookup"><span data-stu-id="168c9-111">Steps</span></span>

<span data-ttu-id="168c9-112">若要啟用 ASP.NET AJAX 和控制項工具組的功能，`ScriptManager` 控制項必須放在頁面上的任何位置（但在 `<form>` 元素內）：</span><span class="sxs-lookup"><span data-stu-id="168c9-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample1.aspx)]

<span data-ttu-id="168c9-113">然後，需要 DropDownList 控制項：</span><span class="sxs-lookup"><span data-stu-id="168c9-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample2.aspx)]

<span data-ttu-id="168c9-114">針對這份清單，會加入 CascadingDropDown 擴充項。</span><span class="sxs-lookup"><span data-stu-id="168c9-114">For this list, a CascadingDropDown extender is added.</span></span> <span data-ttu-id="168c9-115">它會將非同步要求傳送至 web 服務，接著會傳回要顯示在清單中的專案清單。</span><span class="sxs-lookup"><span data-stu-id="168c9-115">It will send an asynchronous request to a web service which will then return a list of entries to be displayed in the list.</span></span> <span data-ttu-id="168c9-116">若要讓此作業正常，必須設定下列 CascadingDropDown 屬性：</span><span class="sxs-lookup"><span data-stu-id="168c9-116">For this to work, the following CascadingDropDown attributes need to be set:</span></span>

- <span data-ttu-id="168c9-117">`ServicePath`：傳遞清單專案之 web 服務的 URL</span><span class="sxs-lookup"><span data-stu-id="168c9-117">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="168c9-118">`ServiceMethod`：傳遞清單專案的 Web 方法</span><span class="sxs-lookup"><span data-stu-id="168c9-118">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="168c9-119">`TargetControlID`：下拉式清單的識別碼</span><span class="sxs-lookup"><span data-stu-id="168c9-119">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="168c9-120">`Category`：呼叫時提交至 web 方法的類別資訊</span><span class="sxs-lookup"><span data-stu-id="168c9-120">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="168c9-121">`PromptText`：從伺服器以非同步方式載入清單資料時顯示的文字</span><span class="sxs-lookup"><span data-stu-id="168c9-121">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>

<span data-ttu-id="168c9-122">以下是 `CascadingDropDown` 元素的標記。</span><span class="sxs-lookup"><span data-stu-id="168c9-122">Here is the markup for the `CascadingDropDown` element.</span></span> <span data-ttu-id="168c9-123">C#和 VB 的唯一差異在於關聯的 web 服務的名稱：</span><span class="sxs-lookup"><span data-stu-id="168c9-123">The only difference between C# and VB is the name of the associated web service:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample3.aspx)]

<span data-ttu-id="168c9-124">來自 `CascadingDropDown` 擴充項的 JavaScript 程式碼會呼叫具有下列簽章的 web 服務方法：</span><span class="sxs-lookup"><span data-stu-id="168c9-124">The JavaScript code coming from the `CascadingDropDown` extender calls a web service method with the following signature:</span></span>

[!code-csharp[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample4.cs)]

<span data-ttu-id="168c9-125">因此，重要的層面是方法必須傳回 `CascadingDropDownNameValue` 類型的陣列（由 ASP.NET AJAX 控制項工具組所定義）。</span><span class="sxs-lookup"><span data-stu-id="168c9-125">So the important aspect is that the method needs to return an array of type `CascadingDropDownNameValue` (defined by the ASP.NET AJAX Control Toolkit).</span></span> <span data-ttu-id="168c9-126">在 `CascadingDropDownNameValue` 的函式中，先列出清單專案的文字，然後再提供它的值，就像 `<option value="VALUE">NAME</option>` 會在 HTML 中這麼做一樣。</span><span class="sxs-lookup"><span data-stu-id="168c9-126">In the `CascadingDropDownNameValue` constructor, first the list entry's text and then its value must be provided, just as `<option value="VALUE">NAME</option>` would do in HTML.</span></span> <span data-ttu-id="168c9-127">以下是一些範例資料：</span><span class="sxs-lookup"><span data-stu-id="168c9-127">Here is some sample data:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample5.aspx)]

<span data-ttu-id="168c9-128">在瀏覽器中載入頁面，會觸發清單填入三個廠商。</span><span class="sxs-lookup"><span data-stu-id="168c9-128">Loading the page in the browser will trigger the list to be filled with three vendors.</span></span>

<span data-ttu-id="168c9-129">[系統會自動填入清單 ![](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="168c9-129">[![The list is filled automatically](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)</span></span>

<span data-ttu-id="168c9-130">系統會自動填入清單（[按一下以查看完整大小的影像](filling-a-list-using-cascadingdropdown-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="168c9-130">The list is filled automatically ([Click to view full-size image](filling-a-list-using-cascadingdropdown-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="168c9-131">下一步</span><span class="sxs-lookup"><span data-stu-id="168c9-131">Next</span></span>](using-cascadingdropdown-with-a-database-cs.md)
