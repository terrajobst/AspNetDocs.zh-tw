---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
title: 使用 CascadingDropDown 填滿清單（VB） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 CascadingDropDown 控制項會擴充 DropDownList 控制項，讓一個 DropDownList 中的變更載入 anoth 中的相關聯值 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 5236695e-5c70-4887-baee-0bfb0afb3448
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 8dd9ef8a4bdf705ba4451b7fd240e4de8618221c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536005"
---
# <a name="filling-a-list-using-cascadingdropdown-vb"></a>使用 CascadingDropDown 填滿清單 (VB)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)

> AJAX 控制項工具組中的 CascadingDropDown 控制項會擴充 DropDownList 控制項，讓一個 DropDownList 中的變更載入另一個 DropDownList 中的關聯值。 （例如，一個清單提供美國州的清單，而下一個清單則會填入該州的主要城市）。首先要解決的挑戰是使用這個控制項來實際填寫下拉式清單。

## <a name="overview"></a>概觀

AJAX 控制項工具組中的 CascadingDropDown 控制項會擴充 DropDownList 控制項，讓一個 DropDownList 中的變更載入另一個 DropDownList 中的關聯值。 （例如，一個清單提供美國州的清單，而下一個清單則會填入該州的主要城市）。首先要解決的挑戰是使用這個控制項來實際填寫下拉式清單。

## <a name="steps"></a>步驟

若要啟用 ASP.NET AJAX 和控制項工具組的功能，`ScriptManager` 控制項必須放在頁面上的任何位置（但在 `<form>` 元素內）：

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample1.aspx)]

然後，需要 DropDownList 控制項：

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample2.aspx)]

針對這份清單，會加入 CascadingDropDown 擴充項。 它會將非同步要求傳送至 web 服務，接著會傳回要顯示在清單中的專案清單。 若要讓此作業正常，必須設定下列 CascadingDropDown 屬性：

- `ServicePath`：傳遞清單專案之 web 服務的 URL
- `ServiceMethod`：傳遞清單專案的 Web 方法
- `TargetControlID`：下拉式清單的識別碼
- `Category`：呼叫時提交至 web 方法的類別資訊
- `PromptText`：從伺服器以非同步方式載入清單資料時顯示的文字

以下是 `CascadingDropDown` 元素的標記。 C#和 VB 的唯一差異在於關聯的 web 服務的名稱：

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample3.aspx)]

來自 `CascadingDropDown` 擴充項的 JavaScript 程式碼會呼叫具有下列簽章的 web 服務方法：

[!code-vb[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample4.vb)]

因此，重要的層面是方法必須傳回 `CascadingDropDownNameValue` 類型的陣列（由 ASP.NET AJAX 控制項工具組所定義）。 在 `CascadingDropDownNameValue` 的函式中，先列出清單專案的文字，然後再提供它的值，就像 `<option value="VALUE">NAME</option>` 會在 HTML 中這麼做一樣。 以下是一些範例資料：

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample5.aspx)]

在瀏覽器中載入頁面，會觸發清單填入三個廠商。

[系統會自動填入清單 ![](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)

系統會自動填入清單（[按一下以查看完整大小的影像](filling-a-list-using-cascadingdropdown-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一頁](using-auto-postback-with-cascadingdropdown-cs.md)
> [下一頁](using-cascadingdropdown-with-a-database-vb.md)
