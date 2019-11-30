---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
title: 動態加入可折疊式窗格C#（） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 [可折疊式] 控制項提供多個窗格，並允許使用者一次顯示其中一項。 面板通常會宣告為 w 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 66d88cfa-f26f-46b1-ad52-1c9e03c04a48
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
msc.type: authoredcontent
ms.openlocfilehash: 2834f56bd77c412923f4a8f382e670727f70eae4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607225"
---
# <a name="dynamically-adding-an-accordion-pane-c"></a>動態新增 [可折疊式C#] 窗格（）

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)

> AJAX 控制項工具組中的 [可折疊式] 控制項提供多個窗格，並允許使用者一次顯示其中一項。 面板通常會在頁面本身內宣告，但伺服器端程式碼可以用來達到相同的結果。

## <a name="overview"></a>概觀

AJAX 控制項工具組中的 [可折疊式] 控制項提供多個窗格，並允許使用者一次顯示其中一項。 面板通常會在頁面本身內宣告，但伺服器端程式碼可以用來達到相同的結果。

## <a name="steps"></a>步驟

[可折疊] 控制項會公開所有重要的屬性給伺服器端程式碼。 除此之外，`Panes` 屬性也會授與組成可折疊性之窗格集合的存取權。 每個窗格都有 `AccordionPane`類型。 因此，建立這種窗格是很簡單的：

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample1.cs)]

`AccordionPane` 的 `HeaderContainer` 屬性，可讓您存取窗格的標頭區段內的 ASP.NET 控制項;`AccordionPane` 的 `ContentContainer` 屬性會對窗格的 [內容] 區段執行相同的工作。 這可讓 ASP.NET 程式碼將內容新增至窗格：

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample2.cs)]

最後，您必須將窗格新增至可折疊的 `Panes` 集合：

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample3.cs)]

以下是完整的伺服器端程式碼，它會將兩個窗格加入至 [可折疊] 控制項：

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample4.aspx)]

唯一缺少的元素是可折疊性本身，這取決於 ASP.NET `ScriptManager` 控制項是否存在：

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample5.aspx)]

若要完成此範例，在 [可折疊] 控制項中參考的兩個 CSS 類別會提供瀏覽器的樣式資訊：

[!code-css[Main](dynamically-adding-an-accordion-pane-cs/samples/sample6.css)]

[![伺服器端程式碼會以動態方式新增可折疊的資料](dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)

伺服器端程式碼會以動態方式新增可折疊顯示的資料（[按一下以觀看完整大小的影像](dynamically-adding-an-accordion-pane-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [上一頁](databinding-to-an-accordion-cs.md)
> [下一頁](databinding-to-an-accordion-vb.md)
