---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
title: 使用自動回傳與 CascadingDropDown （C#） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 CascadingDropDown 控制項會擴充 DropDownList 控制項，讓一個 DropDownList 中的變更載入 anoth 中的相關聯值 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6755d8d9-14be-4a1d-86e5-1a6110f3dea8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 8bccd716814e7de544798010cecbc148ec50b5cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78535949"
---
# <a name="using-auto-postback-with-cascadingdropdown-c"></a>使用自動回傳與 CascadingDropDown (C#)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.cs.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3CS.pdf)

> AJAX 控制項工具組中的 CascadingDropDown 控制項會擴充 DropDownList 控制項，讓一個 DropDownList 中的變更載入另一個 DropDownList 中的關聯值。 不過，使用 CascadingDropDown 控制項時，ASP。NET 的 DropDownList 控制項的 AutoPostBack 功能無法運作，因為以非同步方式將資料載入清單中會產生（不必要）回傳本身。 有了一些 JavaScript 程式碼，就可以避免這種效果。

## <a name="overview"></a>概觀

AJAX 控制項工具組中的 CascadingDropDown 控制項會擴充 DropDownList 控制項，讓一個 DropDownList 中的變更載入另一個 DropDownList 中的關聯值。 （例如，一個清單提供美國州的清單，而下一個清單則會填入該州的主要城市）。不過，使用 CascadingDropDown 控制項時，ASP。NET 的 DropDownList 控制項的 AutoPostBack 功能無法運作，因為以非同步方式將資料載入清單中會產生（不必要）回傳本身。 有了一些 JavaScript 程式碼，就可以避免這種效果。

## <a name="steps"></a>步驟

若要啟用 ASP.NET AJAX 和控制項工具組的功能，必須將 `ScriptManager` 控制項放在頁面上的任何位置（但在 &lt;`form`&gt; 專案中）：

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample1.aspx)]

然後，需要 DropDownList 控制項：

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample2.aspx)]

針對這份清單，會加入 CascadingDropDown 擴充項，並提供 web 服務 URL 和方法資訊：

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample3.aspx)]

然後，CascadingDropDown 擴充項會以非同步方式呼叫具有下列方法簽章的 web 服務：

[!code-csharp[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample4.cs)]

方法會傳回 CascadingDropDown 數值型別的陣列。 類型的函式需要先有清單專案的標題，然後才是值（HTML `value` 屬性）。

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample5.aspx)]

在瀏覽器中載入頁面，會在下拉式清單中填入三個廠商，第二個是預先選取的。 此外，ASP.NET 也會定義 `__doPostBack()` 的 JavaScript 方法。 載入頁面之後，此 JavaScript 呼叫就會新增至下拉式清單，但只有在其中有元素時才會加入。 如果清單中沒有任何專案，則控制項工具組目前正在載入它們，因此 JavaScript 程式碼會使用超時，並在半秒後再試一次。

[!code-html[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample6.html)]

如此一來，只有在清單中有實際元素，且使用者選取專案時，才會執行回傳。

[選取清單元素 ![會導致回傳](using-auto-postback-with-cascadingdropdown-cs/_static/image2.png)](using-auto-postback-with-cascadingdropdown-cs/_static/image1.png)

選取清單元素會導致回傳（[按一下以查看完整大小的影像](using-auto-postback-with-cascadingdropdown-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [上一頁](presetting-list-entries-with-cascadingdropdown-cs.md)
> [下一頁](filling-a-list-using-cascadingdropdown-vb.md)
