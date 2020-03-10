---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-cs
title: 在文字方塊中只允許特定字元（C#） |Microsoft Docs
author: wenz
description: ASP.NET 驗證控制項可以確保使用者輸入中只允許特定字元。 不過，這仍無法防止使用者輸入不正確 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: fd2a1c52-d717-44af-8a61-67c8279bb26e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-cs
msc.type: authoredcontent
ms.openlocfilehash: d1e367becd574e31d24fca8545f76b1ed3c4d85e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554233"
---
# <a name="allowing-only-certain-characters-in-a-text-box-c"></a><span data-ttu-id="96654-104">文字方塊中只允許特定字元 (C#)</span><span class="sxs-lookup"><span data-stu-id="96654-104">Allowing Only Certain Characters in a Text Box (C#)</span></span>

<span data-ttu-id="96654-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="96654-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="96654-106">[下載程式代碼](https://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.cs.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="96654-106">[Download Code](https://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0CS.pdf)</span></span>

> <span data-ttu-id="96654-107">ASP.NET 驗證控制項可以確保使用者輸入中只允許特定字元。</span><span class="sxs-lookup"><span data-stu-id="96654-107">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="96654-108">不過，這仍無法防止使用者輸入不正確字元，並嘗試提交表單。</span><span class="sxs-lookup"><span data-stu-id="96654-108">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>

## <a name="overview"></a><span data-ttu-id="96654-109">概觀</span><span class="sxs-lookup"><span data-stu-id="96654-109">Overview</span></span>

<span data-ttu-id="96654-110">ASP.NET 驗證控制項可以確保使用者輸入中只允許特定字元。</span><span class="sxs-lookup"><span data-stu-id="96654-110">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="96654-111">不過，這仍無法防止使用者輸入不正確字元，並嘗試提交表單。</span><span class="sxs-lookup"><span data-stu-id="96654-111">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>

## <a name="steps"></a><span data-ttu-id="96654-112">步驟</span><span class="sxs-lookup"><span data-stu-id="96654-112">Steps</span></span>

<span data-ttu-id="96654-113">ASP.NET AJAX 控制項工具組包含可延伸文字方塊的 `FilteredTextBox` 控制項。</span><span class="sxs-lookup"><span data-stu-id="96654-113">The ASP.NET AJAX Control Toolkit contains the `FilteredTextBox` control which extends a text box.</span></span> <span data-ttu-id="96654-114">一旦啟用，欄位中就只能輸入一組特定的字元。</span><span class="sxs-lookup"><span data-stu-id="96654-114">Once activated, only a certain set of characters may be entered into the field.</span></span>

<span data-ttu-id="96654-115">為此，我們首先需要 ASP.NET AJAX `ScriptManager`，以載入 ASP.NET AJAX 控制項工具組也會使用的 JavaScript 程式庫：</span><span class="sxs-lookup"><span data-stu-id="96654-115">For this to work, we first need as usual the ASP.NET AJAX `ScriptManager` which loads the JavaScript libraries which are also used by the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample1.aspx)]

<span data-ttu-id="96654-116">然後，我們需要一個文字方塊：</span><span class="sxs-lookup"><span data-stu-id="96654-116">Then, we need a text box:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample2.aspx)]

<span data-ttu-id="96654-117">最後，`FilteredTextBoxExtender` 控制項會負責限制允許使用者輸入的字元。</span><span class="sxs-lookup"><span data-stu-id="96654-117">Finally, the `FilteredTextBoxExtender` control takes care of restricting the characters the user is allowed to type.</span></span> <span data-ttu-id="96654-118">首先，將 `TargetControlID` 屬性設定為 `TextBox` 控制項的 `ID`。</span><span class="sxs-lookup"><span data-stu-id="96654-118">First, set the `TargetControlID` attribute to the `ID` of the `TextBox` control.</span></span> <span data-ttu-id="96654-119">然後，選擇其中一個可用的 `FilterType` 值：</span><span class="sxs-lookup"><span data-stu-id="96654-119">Then, choose one of the available `FilterType` values:</span></span>

- <span data-ttu-id="96654-120">`Custom` 預設值;您必須提供有效字元的清單</span><span class="sxs-lookup"><span data-stu-id="96654-120">`Custom` default; you have to provide a list of valid chars</span></span>
- <span data-ttu-id="96654-121">僅 `LowercaseLetters` 小寫字母</span><span class="sxs-lookup"><span data-stu-id="96654-121">`LowercaseLetters` lowercase letters only</span></span>
- <span data-ttu-id="96654-122">僅 `Numbers` 位數</span><span class="sxs-lookup"><span data-stu-id="96654-122">`Numbers` digits only</span></span>
- <span data-ttu-id="96654-123">僅 `UppercaseLetters` 大寫字母</span><span class="sxs-lookup"><span data-stu-id="96654-123">`UppercaseLetters` uppercase letters only</span></span>

<span data-ttu-id="96654-124">如果使用了 `Custom FilterType`，就必須設定 `ValidChars` 屬性，並提供可輸入的字元清單。</span><span class="sxs-lookup"><span data-stu-id="96654-124">If the `Custom FilterType` is used, the `ValidChars` property must be set and provide a list of characters that may be typed.</span></span> <span data-ttu-id="96654-125">方法：如果您嘗試在文字方塊中貼上文字，則會移除所有不正確字元。</span><span class="sxs-lookup"><span data-stu-id="96654-125">By the way: if you try to paste text into the text box, all invalid chars are removed.</span></span>

<span data-ttu-id="96654-126">以下是只允許數位的 `FilteredTextBoxExtender` 控制項的標記（也可以使用 `FilterType="Numbers"`）：</span><span class="sxs-lookup"><span data-stu-id="96654-126">Here is the markup for the `FilteredTextBoxExtender` control that only allows digits (something that would also have been possible with `FilterType="Numbers"`):</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample3.aspx)]

<span data-ttu-id="96654-127">執行頁面並嘗試輸入字母（若已啟用 JavaScript），它將無法運作;不過，數位會出現在頁面上。</span><span class="sxs-lookup"><span data-stu-id="96654-127">Run the page and try to enter a letter if JavaScript is enabled, it will not work; digits however appear on the page.</span></span> <span data-ttu-id="96654-128">但請注意，保護 `FilteredTextBox` 提供的不是專案符號證明：如果已啟用 JavaScript，則可能會在文字方塊中輸入任何資料，因此您必須使用其他驗證方法，例如 ASP。NET 的驗證控制項。</span><span class="sxs-lookup"><span data-stu-id="96654-128">However note that the protection `FilteredTextBox` provides is not bullet-proof: If JavaScript is enabled, any data may be entered in the text box, so you have to use additional validation means, i.e. ASP.NET's validation controls.</span></span>

<span data-ttu-id="96654-129">[僅可輸入 ![數位](allowing-only-certain-characters-in-a-text-box-cs/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="96654-129">[![Only digits may be entered](allowing-only-certain-characters-in-a-text-box-cs/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-cs/_static/image1.png)</span></span>

<span data-ttu-id="96654-130">只能輸入數位（[按一下以觀看完整大小的影像](allowing-only-certain-characters-in-a-text-box-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="96654-130">Only digits may be entered ([Click to view full-size image](allowing-only-certain-characters-in-a-text-box-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="96654-131">下一個</span><span class="sxs-lookup"><span data-stu-id="96654-131">Next</span></span>](allowing-only-certain-characters-in-a-text-box-vb.md)
