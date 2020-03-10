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
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613509"
---
# <a name="allowing-only-certain-characters-in-a-text-box-vb"></a>文字方塊中只允許特定字元 (VB)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.vb.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0VB.pdf)

> ASP.NET 驗證控制項可以確保使用者輸入中只允許特定字元。 不過，這仍無法防止使用者輸入不正確字元，並嘗試提交表單。

## <a name="overview"></a>概觀

ASP.NET 驗證控制項可以確保使用者輸入中只允許特定字元。 不過，這仍無法防止使用者輸入不正確字元，並嘗試提交表單。

## <a name="steps"></a>步驟

ASP.NET AJAX 控制項工具組包含可延伸文字方塊的 `FilteredTextBox` 控制項。 一旦啟用，欄位中就只能輸入一組特定的字元。

為此，我們首先需要 ASP.NET AJAX `ScriptManager`，以載入 ASP.NET AJAX 控制項工具組也會使用的 JavaScript 程式庫：

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample1.aspx)]

然後，我們需要一個文字方塊：

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample2.aspx)]

最後，`FilteredTextBoxExtender` 控制項會負責限制允許使用者輸入的字元。 首先，將 `TargetControlID` 屬性設定為 `TextBox` 控制項的 `ID`。 然後，選擇其中一個可用的 `FilterType` 值：

- `Custom` 預設值;您必須提供有效字元的清單
- 僅 `LowercaseLetters` 小寫字母
- 僅 `Numbers` 位數
- 僅 `UppercaseLetters` 大寫字母

如果使用了 `Custom FilterType`，就必須設定 `ValidChars` 屬性，並提供可輸入的字元清單。 方法：如果您嘗試在文字方塊中貼上文字，則會移除所有不正確字元。

以下是只允許數位的 `FilteredTextBoxExtender` 控制項的標記（也可以使用 `FilterType="Numbers"`）：

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample3.aspx)]

執行頁面並嘗試輸入字母（若已啟用 JavaScript），它將無法運作;不過，數位會出現在頁面上。 但請注意，保護 `FilteredTextBox` 提供的不是專案符號證明：如果已啟用 JavaScript，則可能會在文字方塊中輸入任何資料，因此您必須使用其他驗證方法，例如 ASP。NET 的驗證控制項。

[僅可輸入 ![數位](allowing-only-certain-characters-in-a-text-box-vb/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-vb/_static/image1.png)

只能輸入數位（[按一下以觀看完整大小的影像](allowing-only-certain-characters-in-a-text-box-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一篇](allowing-only-certain-characters-in-a-text-box-cs.md)
