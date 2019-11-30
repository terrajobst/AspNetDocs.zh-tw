---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
title: 測試密碼強度（VB） |Microsoft Docs
author: wenz
description: 密碼幾乎都是必要的，因此延遲的使用者通常會選擇容易中斷的簡單密碼。 ASP 中的 PasswordStrength 控制項。N 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 9215a37f-3133-4887-8ed2-3689f3a53551
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
msc.type: authoredcontent
ms.openlocfilehash: b614e1788eeafc175dd792ec6d3e4619f9ea2b7a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606266"
---
# <a name="testing-the-strength-of-a-password-vb"></a>測試密碼強度 (VB)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.vb.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0VB.pdf)

> 密碼幾乎都是必要的，因此延遲的使用者通常會選擇容易中斷的簡單密碼。 ASP.NET AJAX 控制項工具組中的 PasswordStrength 控制項可以檢查密碼的有效程度。

## <a name="overview"></a>概觀

密碼幾乎都是必要的，因此延遲的使用者通常會選擇容易中斷的簡單密碼。 ASP.NET AJAX 控制項工具組中的 `PasswordStrength` 控制項可以檢查密碼的有效程度。

## <a name="steps"></a>步驟

`PasswordStrength` 控制項會擴充一個文字方塊，並檢查其中的密碼是否夠好。 它透過屬性提供了豐富的選項;以下只是其中一部分：

- `MinimumNumericCharacters` 密碼中所需的最小數位字元數
- `MinimumSymbolCharacters` 密碼中所需的最小符號字元數（不是字母和數位）
- `PreferredPasswordLength` 密碼的最小長度
- `RequiresUpperAndLowerCaseCharacters` 密碼是否必須同時使用大寫和小寫字元

`StrengthIndicatorType` 提供如何以文字（值 `"Text"`）或一種進度列（值 `"BarIndicator"`）來呈現密碼強度的資訊。 在 [`DisplayPosition`] 屬性中，您可以設定資訊的顯示位置。 以下是完整的範例，包括 ASP.NET AJAX `ScriptManager` 控制項、`PasswordStrength` 控制項，當然還有一個文字方塊，使用者可以在其中輸入密碼。 為了示範，第二個表單欄位是一般文字欄位，而不是密碼欄位，讓您可以在開發期間看到您要輸入的內容。

[!code-aspx[Main](testing-the-strength-of-a-password-vb/samples/sample1.aspx)]

執行頁面並輸入離開：只有在您輸入小寫字母、大寫字母、數位和符號之後，密碼才會被視為 unbreakable。

[![現在密碼是（相當的）](testing-the-strength-of-a-password-vb/_static/image2.png)](testing-the-strength-of-a-password-vb/_static/image1.png)

現在密碼是（相當的）好（[按一下以觀看完整大小的影像](testing-the-strength-of-a-password-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一篇](testing-the-strength-of-a-password-cs.md)
