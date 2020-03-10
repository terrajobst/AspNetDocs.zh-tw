---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
title: 使用 CascadingDropDown 預設清單專案（VB） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 CascadingDropDown 控制項會擴充 DropDownList 控制項，讓一個 DropDownList 中的變更載入 anoth 中的相關聯值 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ec61ced7-bbca-4bdd-aa3b-80878f295181
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 58d675993777f9dcbe0ce1890a60046c91ee8907
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78597927"
---
# <a name="presetting-list-entries-with-cascadingdropdown-vb"></a>使用 CascadingDropDown 預設清單項目 (VB)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.vb.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/CascadingDropDown2VB.pdf)

> AJAX 控制項工具組中的 CascadingDropDown 控制項會擴充 DropDownList 控制項，讓一個 DropDownList 中的變更載入另一個 DropDownList 中的關聯值。 只要有一些程式碼，當資料已動態載入之後，就可以預先選取清單元素。

## <a name="overview"></a>概觀

AJAX 控制項工具組中的 CascadingDropDown 控制項會擴充 DropDownList 控制項，讓一個 DropDownList 中的變更載入另一個 DropDownList 中的關聯值。 （例如，一個清單提供美國州的清單，而下一個清單則會填入該州的主要城市）。只要有一些程式碼，當資料已動態載入之後，就可以預先選取清單元素。

## <a name="steps"></a>步驟

若要啟用 ASP.NET AJAX 和控制項工具組的功能，`ScriptManager` 控制項必須放在頁面上的任何位置（但在 `<form>` 元素內）：

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample1.aspx)]

然後，需要 DropDownList 控制項：

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample2.aspx)]

針對這份清單，會加入 CascadingDropDown 擴充項，並提供 web 服務 URL 和方法資訊：

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample3.aspx)]

然後，CascadingDropDown 擴充項會以非同步方式呼叫具有下列方法簽章的 web 服務：

[!code-vb[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample4.vb)]

方法會傳回 CascadingDropDown 數值型別的陣列。 類型的函式需要先有清單專案的標題，然後才是值（HTML `value` 屬性）。 如果第三個引數設定為 true，則會在瀏覽器中自動選取清單元素。

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample5.aspx)]

在瀏覽器中載入頁面，會在下拉式清單中填入三個廠商，第二個是預先選取的。

[![清單已自動填入和預先選取](presetting-list-entries-with-cascadingdropdown-vb/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-vb/_static/image1.png)

系統會自動填入並預先選取清單（[按一下以查看完整大小的影像](presetting-list-entries-with-cascadingdropdown-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一頁](using-cascadingdropdown-with-a-database-vb.md)
> [下一頁](using-auto-postback-with-cascadingdropdown-vb.md)
