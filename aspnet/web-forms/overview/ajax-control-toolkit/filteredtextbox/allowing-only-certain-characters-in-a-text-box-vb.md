---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
title: 文字方塊中只允許特定字元（VB） |Microsoft Docs
author: wenz
description: ASP.NET 驗證控制項可以確保使用者輸入中只允許特定字元。 不過，這仍無法防止使用者輸入不正確 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 33af23f1-4016-4740-8fb2-37d1773452cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
msc.type: authoredcontent
ms.openlocfilehash: 895708ebecc30c5f35e6ecd0349604bb777cbd93
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74573962"
---
# <a name="allowing-only-certain-characters-in-a-text-box-vb"></a><span data-ttu-id="4f7a1-104">文字方塊中只允許特定字元 (VB)</span><span class="sxs-lookup"><span data-stu-id="4f7a1-104">Allowing Only Certain Characters in a Text Box (VB)</span></span>

<span data-ttu-id="4f7a1-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="4f7a1-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="4f7a1-106">[下載程式代碼](https://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.vb.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="4f7a1-106">[Download Code](https://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0VB.pdf)</span></span>

> <span data-ttu-id="4f7a1-107">ASP.NET 驗證控制項可以確保使用者輸入中只允許特定字元。</span><span class="sxs-lookup"><span data-stu-id="4f7a1-107">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="4f7a1-108">不過，這仍無法防止使用者輸入不正確字元，並嘗試提交表單。</span><span class="sxs-lookup"><span data-stu-id="4f7a1-108">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>

## <a name="overview"></a><span data-ttu-id="4f7a1-109">概觀</span><span class="sxs-lookup"><span data-stu-id="4f7a1-109">Overview</span></span>

<span data-ttu-id="4f7a1-110">ASP.NET 驗證控制項可以確保使用者輸入中只允許特定字元。</span><span class="sxs-lookup"><span data-stu-id="4f7a1-110">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="4f7a1-111">不過，這仍無法防止使用者輸入不正確字元，並嘗試提交表單。</span><span class="sxs-lookup"><span data-stu-id="4f7a1-111">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>

## <a name="steps"></a><span data-ttu-id="4f7a1-112">步驟</span><span class="sxs-lookup"><span data-stu-id="4f7a1-112">Steps</span></span>

<span data-ttu-id="4f7a1-113">ASP.NET AJAX 控制項工具組包含可延伸文字方塊的 `FilteredTextBox` 控制項。</span><span class="sxs-lookup"><span data-stu-id="4f7a1-113">The ASP.NET AJAX Control Toolkit contains the `FilteredTextBox` control which extends a text box.</span></span> <span data-ttu-id="4f7a1-114">一旦啟用，欄位中就只能輸入一組特定的字元。</span><span class="sxs-lookup"><span data-stu-id="4f7a1-114">Once activated, only a certain set of characters may be entered into the field.</span></span>

<span data-ttu-id="4f7a1-115">為此，我們首先需要 ASP.NET AJAX `ScriptManager`，以載入 ASP.NET AJAX 控制項工具組也會使用的 JavaScript 程式庫：</span><span class="sxs-lookup"><span data-stu-id="4f7a1-115">For this to work, we first need as usual the ASP.NET AJAX `ScriptManager` which loads the JavaScript libraries which are also used by the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample1.aspx)]

<span data-ttu-id="4f7a1-116">然後，我們需要一個文字方塊：</span><span class="sxs-lookup"><span data-stu-id="4f7a1-116">Then, we need a text box:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample2.aspx)]

<span data-ttu-id="4f7a1-117">最後，`FilteredTextBoxExtender` 控制項會負責限制允許使用者輸入的字元。</span><span class="sxs-lookup"><span data-stu-id="4f7a1-117">Finally, the `FilteredTextBoxExtender` control takes care of restricting the characters the user is allowed to type.</span></span> <span data-ttu-id="4f7a1-118">首先，將 `TargetControlID` 屬性設定為 `TextBox` 控制項的 `ID`。</span><span class="sxs-lookup"><span data-stu-id="4f7a1-118">First, set the `TargetControlID` attribute to the `ID` of the `TextBox` control.</span></span> <span data-ttu-id="4f7a1-119">然後，選擇其中一個可用的 `FilterType` 值：</span><span class="sxs-lookup"><span data-stu-id="4f7a1-119">Then, choose one of the available `FilterType` values:</span></span>

- <span data-ttu-id="4f7a1-120">`Custom` 預設值;您必須提供有效字元的清單</span><span class="sxs-lookup"><span data-stu-id="4f7a1-120">`Custom` default; you have to provide a list of valid chars</span></span>
- <span data-ttu-id="4f7a1-121">僅 `LowercaseLetters` 小寫字母</span><span class="sxs-lookup"><span data-stu-id="4f7a1-121">`LowercaseLetters` lowercase letters only</span></span>
- <span data-ttu-id="4f7a1-122">僅 `Numbers` 位數</span><span class="sxs-lookup"><span data-stu-id="4f7a1-122">`Numbers` digits only</span></span>
- <span data-ttu-id="4f7a1-123">僅 `UppercaseLetters` 大寫字母</span><span class="sxs-lookup"><span data-stu-id="4f7a1-123">`UppercaseLetters` uppercase letters only</span></span>

<span data-ttu-id="4f7a1-124">如果使用了 `Custom FilterType`，就必須設定 `ValidChars` 屬性，並提供可輸入的字元清單。</span><span class="sxs-lookup"><span data-stu-id="4f7a1-124">If the `Custom FilterType` is used, the `ValidChars` property must be set and provide a list of characters that may be typed.</span></span> <span data-ttu-id="4f7a1-125">方法：如果您嘗試在文字方塊中貼上文字，則會移除所有不正確字元。</span><span class="sxs-lookup"><span data-stu-id="4f7a1-125">By the way: if you try to paste text into the text box, all invalid chars are removed.</span></span>

<span data-ttu-id="4f7a1-126">以下是只允許數位的 `FilteredTextBoxExtender` 控制項的標記（也可以使用 `FilterType="Numbers"`）：</span><span class="sxs-lookup"><span data-stu-id="4f7a1-126">Here is the markup for the `FilteredTextBoxExtender` control that only allows digits (something that would also have been possible with `FilterType="Numbers"`):</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample3.aspx)]

<span data-ttu-id="4f7a1-127">執行頁面並嘗試輸入字母（若已啟用 JavaScript），它將無法運作;不過，數位會出現在頁面上。</span><span class="sxs-lookup"><span data-stu-id="4f7a1-127">Run the page and try to enter a letter if JavaScript is enabled, it will not work; digits however appear on the page.</span></span> <span data-ttu-id="4f7a1-128">但請注意，保護 `FilteredTextBox` 提供的不是專案符號證明：如果已啟用 JavaScript，則可能會在文字方塊中輸入任何資料，因此您必須使用其他驗證方法，例如 ASP。NET 的驗證控制項。</span><span class="sxs-lookup"><span data-stu-id="4f7a1-128">However note that the protection `FilteredTextBox` provides is not bullet-proof: If JavaScript is enabled, any data may be entered in the text box, so you have to use additional validation means, i.e. ASP.NET's validation controls.</span></span>

<span data-ttu-id="4f7a1-129">[僅可輸入 ![數位](allowing-only-certain-characters-in-a-text-box-vb/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4f7a1-129">[![Only digits may be entered](allowing-only-certain-characters-in-a-text-box-vb/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-vb/_static/image1.png)</span></span>

<span data-ttu-id="4f7a1-130">只能輸入數位（[按一下以觀看完整大小的影像](allowing-only-certain-characters-in-a-text-box-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="4f7a1-130">Only digits may be entered ([Click to view full-size image](allowing-only-certain-characters-in-a-text-box-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4f7a1-131">上一篇</span><span class="sxs-lookup"><span data-stu-id="4f7a1-131">Previous</span></span>](allowing-only-certain-characters-in-a-text-box-cs.md)
