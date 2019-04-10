---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-cs
title: 只允許特定字元在文字方塊中 (C#) |Microsoft Docs
author: wenz
description: ASP.NET 驗證控制項可以確保只有特定字元允許在使用者輸入。 不過這仍無法防止使用者輸入不正確...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: fd2a1c52-d717-44af-8a61-67c8279bb26e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-cs
msc.type: authoredcontent
ms.openlocfilehash: 020f7bbe797a2c04f1ff97ea2056345028f700fb
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59407610"
---
# <a name="allowing-only-certain-characters-in-a-text-box-c"></a><span data-ttu-id="d1a0e-104">文字方塊中只允許特定字元 (C#)</span><span class="sxs-lookup"><span data-stu-id="d1a0e-104">Allowing Only Certain Characters in a Text Box (C#)</span></span>

<span data-ttu-id="d1a0e-105">藉由[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="d1a0e-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="d1a0e-106">[下載程式碼](http://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.cs.zip)或[下載 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="d1a0e-106">[Download Code](http://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0CS.pdf)</span></span>

> <span data-ttu-id="d1a0e-107">ASP.NET 驗證控制項可以確保只有特定字元允許在使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="d1a0e-107">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="d1a0e-108">不過這仍不會防止使用者輸入無效的字元，並嘗試送出表單。</span><span class="sxs-lookup"><span data-stu-id="d1a0e-108">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>


## <a name="overview"></a><span data-ttu-id="d1a0e-109">總覽</span><span class="sxs-lookup"><span data-stu-id="d1a0e-109">Overview</span></span>

<span data-ttu-id="d1a0e-110">ASP.NET 驗證控制項可以確保只有特定字元允許在使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="d1a0e-110">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="d1a0e-111">不過這仍不會防止使用者輸入無效的字元，並嘗試送出表單。</span><span class="sxs-lookup"><span data-stu-id="d1a0e-111">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>

## <a name="steps"></a><span data-ttu-id="d1a0e-112">步驟</span><span class="sxs-lookup"><span data-stu-id="d1a0e-112">Steps</span></span>

<span data-ttu-id="d1a0e-113">ASP.NET AJAX Control Toolkit 包含`FilteredTextBox`擴充文字方塊控制項。</span><span class="sxs-lookup"><span data-stu-id="d1a0e-113">The ASP.NET AJAX Control Toolkit contains the `FilteredTextBox` control which extends a text box.</span></span> <span data-ttu-id="d1a0e-114">一旦啟動後，只有特定的一組字元可能會輸入欄位。</span><span class="sxs-lookup"><span data-stu-id="d1a0e-114">Once activated, only a certain set of characters may be entered into the field.</span></span>

<span data-ttu-id="d1a0e-115">針對此目的，我們必須先如往常般 ASP.NET AJAX`ScriptManager`載入也會由 ASP.NET AJAX Control Toolkit 中的 JavaScript 程式庫：</span><span class="sxs-lookup"><span data-stu-id="d1a0e-115">For this to work, we first need as usual the ASP.NET AJAX `ScriptManager` which loads the JavaScript libraries which are also used by the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample1.aspx)]

<span data-ttu-id="d1a0e-116">然後，我們需要在文字方塊中：</span><span class="sxs-lookup"><span data-stu-id="d1a0e-116">Then, we need a text box:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample2.aspx)]

<span data-ttu-id="d1a0e-117">最後，`FilteredTextBoxExtender`控制項負責限制允許使用者輸入的字元。</span><span class="sxs-lookup"><span data-stu-id="d1a0e-117">Finally, the `FilteredTextBoxExtender` control takes care of restricting the characters the user is allowed to type.</span></span> <span data-ttu-id="d1a0e-118">首先，設定`TargetControlID`屬性設定為`ID`的`TextBox`控制項。</span><span class="sxs-lookup"><span data-stu-id="d1a0e-118">First, set the `TargetControlID` attribute to the `ID` of the `TextBox` control.</span></span> <span data-ttu-id="d1a0e-119">然後，選擇其中一個可用`FilterType`值：</span><span class="sxs-lookup"><span data-stu-id="d1a0e-119">Then, choose one of the available `FilterType` values:</span></span>

- `Custom` <span data-ttu-id="d1a0e-120">預設值;您必須提供一份有效的字元</span><span class="sxs-lookup"><span data-stu-id="d1a0e-120">default; you have to provide a list of valid chars</span></span>
- `LowercaseLetters` <span data-ttu-id="d1a0e-121">只有小寫字母</span><span class="sxs-lookup"><span data-stu-id="d1a0e-121">lowercase letters only</span></span>
- `Numbers` <span data-ttu-id="d1a0e-122">只有數字</span><span class="sxs-lookup"><span data-stu-id="d1a0e-122">digits only</span></span>
- `UppercaseLetters` <span data-ttu-id="d1a0e-123">大寫英文字母</span><span class="sxs-lookup"><span data-stu-id="d1a0e-123">uppercase letters only</span></span>

<span data-ttu-id="d1a0e-124">如果`Custom FilterType`使用時，`ValidChars`屬性必須設定，並提供一份可能輸入的字元。</span><span class="sxs-lookup"><span data-stu-id="d1a0e-124">If the `Custom FilterType` is used, the `ValidChars` property must be set and provide a list of characters that may be typed.</span></span> <span data-ttu-id="d1a0e-125">順便一提： 如果您嘗試將文字貼到文字方塊中，會移除所有無效的字元。</span><span class="sxs-lookup"><span data-stu-id="d1a0e-125">By the way: if you try to paste text into the text box, all invalid chars are removed.</span></span>

<span data-ttu-id="d1a0e-126">以下是標記`FilteredTextBoxExtender`只允許數字的控制項 (也會使用的項目`FilterType="Numbers"`):</span><span class="sxs-lookup"><span data-stu-id="d1a0e-126">Here is the markup for the `FilteredTextBoxExtender` control that only allows digits (something that would also have been possible with `FilterType="Numbers"`):</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample3.aspx)]

<span data-ttu-id="d1a0e-127">執行頁面並嘗試輸入字母，如果已啟用 JavaScript，它將無法運作;數字，不過會出現在頁面上。</span><span class="sxs-lookup"><span data-stu-id="d1a0e-127">Run the page and try to enter a letter if JavaScript is enabled, it will not work; digits however appear on the page.</span></span> <span data-ttu-id="d1a0e-128">不過請注意，保護`FilteredTextBox`提供不是項目符號的使用期限：如果已啟用 JavaScript，任何資料可能會在文字方塊中輸入，因此您必須使用額外的驗證方法，也就是 ASP。NET 的驗證控制項。</span><span class="sxs-lookup"><span data-stu-id="d1a0e-128">However note that the protection `FilteredTextBox` provides is not bullet-proof: If JavaScript is enabled, any data may be entered in the text box, so you have to use additional validation means, i.e. ASP.NET's validation controls.</span></span>


[![O<span data-ttu-id="d1a0e-129">可能會輸入只有數字]</span><span class="sxs-lookup"><span data-stu-id="d1a0e-129">nly digits may be entered]</span></span>(allowing-only-certain-characters-in-a-text-box-cs/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-cs/_static/image1.png)

<span data-ttu-id="d1a0e-130">可能會輸入只有數字 ([按一下以檢視完整大小的影像](allowing-only-certain-characters-in-a-text-box-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="d1a0e-130">Only digits may be entered ([Click to view full-size image](allowing-only-certain-characters-in-a-text-box-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="d1a0e-131">下一步</span><span class="sxs-lookup"><span data-stu-id="d1a0e-131">Next</span></span>](allowing-only-certain-characters-in-a-text-box-vb.md)
