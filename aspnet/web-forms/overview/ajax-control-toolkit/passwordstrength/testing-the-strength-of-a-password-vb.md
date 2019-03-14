---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
title: 測試 (VB) 的密碼強度 |Microsoft Docs
author: wenz
description: 因此，延遲使用者通常會選擇簡單的密碼，也就是輕而易舉地突破，則幾乎任何地方，需要密碼。 在此 ASP 中 PasswordStrength 控制項。N...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 9215a37f-3133-4887-8ed2-3689f3a53551
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
msc.type: authoredcontent
ms.openlocfilehash: db4b2a6bbdb0716442b104c03d0c4138bf60f9be
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57027995"
---
<a name="testing-the-strength-of-a-password-vb"></a><span data-ttu-id="2c8f5-104">測試密碼強度 (VB)</span><span class="sxs-lookup"><span data-stu-id="2c8f5-104">Testing the Strength of a Password (VB)</span></span>
====================
<span data-ttu-id="2c8f5-105">藉由[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="2c8f5-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="2c8f5-106">[下載程式碼](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.vb.zip)或[下載 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="2c8f5-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0VB.pdf)</span></span>

> <span data-ttu-id="2c8f5-107">因此，延遲使用者通常會選擇簡單的密碼，也就是輕而易舉地突破，則幾乎任何地方，需要密碼。</span><span class="sxs-lookup"><span data-stu-id="2c8f5-107">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="2c8f5-108">PasswordStrength 控制項在 ASP.NET AJAX Control Toolkit 可以檢查是好的密碼。</span><span class="sxs-lookup"><span data-stu-id="2c8f5-108">The PasswordStrength control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>


## <a name="overview"></a><span data-ttu-id="2c8f5-109">總覽</span><span class="sxs-lookup"><span data-stu-id="2c8f5-109">Overview</span></span>

<span data-ttu-id="2c8f5-110">因此，延遲使用者通常會選擇簡單的密碼，也就是輕而易舉地突破，則幾乎任何地方，需要密碼。</span><span class="sxs-lookup"><span data-stu-id="2c8f5-110">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="2c8f5-111">`PasswordStrength` ASP.NET AJAX Control Toolkit 中的控制項可以檢查是好的密碼。</span><span class="sxs-lookup"><span data-stu-id="2c8f5-111">The `PasswordStrength` control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="steps"></a><span data-ttu-id="2c8f5-112">步驟</span><span class="sxs-lookup"><span data-stu-id="2c8f5-112">Steps</span></span>

<span data-ttu-id="2c8f5-113">`PasswordStrength`擴充文字方塊控制項，並檢查密碼是否夠好。</span><span class="sxs-lookup"><span data-stu-id="2c8f5-113">The `PasswordStrength` control extends a text box and checks whether the password in it is good enough.</span></span> <span data-ttu-id="2c8f5-114">它提供豐富的屬性，透過的選項以下是只是某些：</span><span class="sxs-lookup"><span data-stu-id="2c8f5-114">It offers a wealth of options via attributes; here are just some of them:</span></span>

- <span data-ttu-id="2c8f5-115">`MinimumNumericCharacters` 密碼所需的數字字元的最小數目</span><span class="sxs-lookup"><span data-stu-id="2c8f5-115">`MinimumNumericCharacters` minimum number of numeric characters required in the password</span></span>
- <span data-ttu-id="2c8f5-116">`MinimumSymbolCharacters` 密碼所需的符號字元 （不字母和數字） 最小的數目</span><span class="sxs-lookup"><span data-stu-id="2c8f5-116">`MinimumSymbolCharacters` minimum number of symbol characters (not letters and digits) required in the password</span></span>
- <span data-ttu-id="2c8f5-117">`PreferredPasswordLength` 最小密碼長度</span><span class="sxs-lookup"><span data-stu-id="2c8f5-117">`PreferredPasswordLength` minimum length of the password</span></span>
- <span data-ttu-id="2c8f5-118">`RequiresUpperAndLowerCaseCharacters` 密碼是否必須使用大寫和小寫字元</span><span class="sxs-lookup"><span data-stu-id="2c8f5-118">`RequiresUpperAndLowerCaseCharacters` whether the password needs to use both uppercase and lowercase characters</span></span>

<span data-ttu-id="2c8f5-119">`StrengthIndicatorType`提供的資訊如何呈現的強度的密碼，以文字 (值`"Text"`) 或為類型的進度列 (值`"BarIndicator"`)。</span><span class="sxs-lookup"><span data-stu-id="2c8f5-119">The `StrengthIndicatorType` provides the information how to present the strength of the password, as text (value `"Text"`) or as a kind of progress bar (value `"BarIndicator"`).</span></span> <span data-ttu-id="2c8f5-120">在 `DisplayPosition`屬性，您將設定資訊出現的位置。</span><span class="sxs-lookup"><span data-stu-id="2c8f5-120">In the `DisplayPosition` attribute, you configure where the information appears.</span></span> <span data-ttu-id="2c8f5-121">以下是完整的範例，包括 ASP.NET AJAX`ScriptManager`控制項，`PasswordStrength`控制項，當然還有使用者可以在其中輸入密碼 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="2c8f5-121">Here is a complete example, including the ASP.NET AJAX `ScriptManager` control, the `PasswordStrength` control and of course a text box where the user may enter a password.</span></span> <span data-ttu-id="2c8f5-122">為了示範，後者的表單欄位是規則的文字欄位並不是密碼欄位，讓您可以查看在開發期間您輸入的內容。</span><span class="sxs-lookup"><span data-stu-id="2c8f5-122">For the sake of demonstration, the latter form field is a regular text field and not a password field so that you can see during development what you are typing.</span></span>

[!code-aspx[Main](testing-the-strength-of-a-password-vb/samples/sample1.aspx)]

<span data-ttu-id="2c8f5-123">執行此頁面，並立即輸入：只輸入小寫字母、 大寫字母、 數字和符號之後，密碼已被視為為永不中斷。</span><span class="sxs-lookup"><span data-stu-id="2c8f5-123">Run the page and type away: Only after you have entered lowercase letters, uppercase letters, digits and symbols, the password is deemed as unbreakable .</span></span>


<span data-ttu-id="2c8f5-124">[![現在是 （挺） 好用的密碼](testing-the-strength-of-a-password-vb/_static/image2.png)](testing-the-strength-of-a-password-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2c8f5-124">[![Now the password is (quite) good](testing-the-strength-of-a-password-vb/_static/image2.png)](testing-the-strength-of-a-password-vb/_static/image1.png)</span></span>

<span data-ttu-id="2c8f5-125">現在，密碼是 （挺） 好用的 ([按一下以檢視完整大小的影像](testing-the-strength-of-a-password-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="2c8f5-125">Now the password is (quite) good ([Click to view full-size image](testing-the-strength-of-a-password-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="2c8f5-126">上一步</span><span class="sxs-lookup"><span data-stu-id="2c8f5-126">Previous</span></span>](testing-the-strength-of-a-password-cs.md)