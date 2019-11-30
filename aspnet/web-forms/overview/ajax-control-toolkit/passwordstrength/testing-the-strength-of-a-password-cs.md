---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
title: 測試密碼強度（C#） |Microsoft Docs
author: wenz
description: 密碼幾乎都是必要的，因此延遲的使用者通常會選擇容易中斷的簡單密碼。 ASP 中的 PasswordStrength 控制項。N 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: cb4afbae-9b8f-483d-9729-476d4b9f85fc
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
msc.type: authoredcontent
ms.openlocfilehash: e55eab9feebc18f39dd40c59cfb423208296b6c5
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598867"
---
# <a name="testing-the-strength-of-a-password-c"></a><span data-ttu-id="63d2a-104">測試密碼強度 (C#)</span><span class="sxs-lookup"><span data-stu-id="63d2a-104">Testing the Strength of a Password (C#)</span></span>

<span data-ttu-id="63d2a-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="63d2a-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="63d2a-106">[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="63d2a-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)</span></span>

> <span data-ttu-id="63d2a-107">密碼幾乎都是必要的，因此延遲的使用者通常會選擇容易中斷的簡單密碼。</span><span class="sxs-lookup"><span data-stu-id="63d2a-107">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="63d2a-108">ASP.NET AJAX 控制項工具組中的 PasswordStrength 控制項可以檢查密碼的有效程度。</span><span class="sxs-lookup"><span data-stu-id="63d2a-108">The PasswordStrength control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="overview"></a><span data-ttu-id="63d2a-109">概觀</span><span class="sxs-lookup"><span data-stu-id="63d2a-109">Overview</span></span>

<span data-ttu-id="63d2a-110">密碼幾乎都是必要的，因此延遲的使用者通常會選擇容易中斷的簡單密碼。</span><span class="sxs-lookup"><span data-stu-id="63d2a-110">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="63d2a-111">ASP.NET AJAX 控制項工具組中的 `PasswordStrength` 控制項可以檢查密碼的有效程度。</span><span class="sxs-lookup"><span data-stu-id="63d2a-111">The `PasswordStrength` control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="steps"></a><span data-ttu-id="63d2a-112">步驟</span><span class="sxs-lookup"><span data-stu-id="63d2a-112">Steps</span></span>

<span data-ttu-id="63d2a-113">`PasswordStrength` 控制項會擴充一個文字方塊，並檢查其中的密碼是否夠好。</span><span class="sxs-lookup"><span data-stu-id="63d2a-113">The `PasswordStrength` control extends a text box and checks whether the password in it is good enough.</span></span> <span data-ttu-id="63d2a-114">它透過屬性提供了豐富的選項;以下只是其中一部分：</span><span class="sxs-lookup"><span data-stu-id="63d2a-114">It offers a wealth of options via attributes; here are just some of them:</span></span>

- <span data-ttu-id="63d2a-115">`MinimumNumericCharacters` 密碼中所需的最小數位字元數</span><span class="sxs-lookup"><span data-stu-id="63d2a-115">`MinimumNumericCharacters` minimum number of numeric characters required in the password</span></span>
- <span data-ttu-id="63d2a-116">`MinimumSymbolCharacters` 密碼中所需的最小符號字元數（不是字母和數位）</span><span class="sxs-lookup"><span data-stu-id="63d2a-116">`MinimumSymbolCharacters` minimum number of symbol characters (not letters and digits) required in the password</span></span>
- <span data-ttu-id="63d2a-117">`PreferredPasswordLength` 密碼的最小長度</span><span class="sxs-lookup"><span data-stu-id="63d2a-117">`PreferredPasswordLength` minimum length of the password</span></span>
- <span data-ttu-id="63d2a-118">`RequiresUpperAndLowerCaseCharacters` 密碼是否必須同時使用大寫和小寫字元</span><span class="sxs-lookup"><span data-stu-id="63d2a-118">`RequiresUpperAndLowerCaseCharacters` whether the password needs to use both uppercase and lowercase characters</span></span>

<span data-ttu-id="63d2a-119">`StrengthIndicatorType` 提供如何以文字（值 `"Text"`）或一種進度列（值 `"BarIndicator"`）來呈現密碼強度的資訊。</span><span class="sxs-lookup"><span data-stu-id="63d2a-119">The `StrengthIndicatorType` provides the information how to present the strength of the password, as text (value `"Text"`) or as a kind of progress bar (value `"BarIndicator"`).</span></span> <span data-ttu-id="63d2a-120">在 [`DisplayPosition`] 屬性中，您可以設定資訊的顯示位置。</span><span class="sxs-lookup"><span data-stu-id="63d2a-120">In the `DisplayPosition` attribute, you configure where the information appears.</span></span> <span data-ttu-id="63d2a-121">以下是完整的範例，包括 ASP.NET AJAX `ScriptManager` 控制項、`PasswordStrength` 控制項，當然還有一個文字方塊，使用者可以在其中輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="63d2a-121">Here is a complete example, including the ASP.NET AJAX `ScriptManager` control, the `PasswordStrength` control and of course a text box where the user may enter a password.</span></span> <span data-ttu-id="63d2a-122">為了示範，第二個表單欄位是一般文字欄位，而不是密碼欄位，讓您可以在開發期間看到您要輸入的內容。</span><span class="sxs-lookup"><span data-stu-id="63d2a-122">For the sake of demonstration, the latter form field is a regular text field and not a password field so that you can see during development what you are typing.</span></span>

[!code-aspx[Main](testing-the-strength-of-a-password-cs/samples/sample1.aspx)]

<span data-ttu-id="63d2a-123">執行頁面並輸入離開：只有在您輸入小寫字母、大寫字母、數位和符號之後，密碼才會被視為 unbreakable。</span><span class="sxs-lookup"><span data-stu-id="63d2a-123">Run the page and type away: Only after you have entered lowercase letters, uppercase letters, digits and symbols, the password is deemed as unbreakable .</span></span>

<span data-ttu-id="63d2a-124">[![現在密碼是（相當的）](testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="63d2a-124">[![Now the password is (quite) good](testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)</span></span>

<span data-ttu-id="63d2a-125">現在密碼是（相當的）好（[按一下以觀看完整大小的影像](testing-the-strength-of-a-password-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="63d2a-125">Now the password is (quite) good ([Click to view full-size image](testing-the-strength-of-a-password-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="63d2a-126">下一步</span><span class="sxs-lookup"><span data-stu-id="63d2a-126">Next</span></span>](testing-the-strength-of-a-password-vb.md)
