---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
title: 建立互斥的核取方塊C#（） |Microsoft Docs
author: wenz
description: 只有一組選項可以選取時，通常會使用選項按鈕。 但有一個缺點，就是在選取群組中的一個選項按鈕之後,。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 8e11b813-ba0d-4c29-b0f8-f65db6dbef1e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
msc.type: authoredcontent
ms.openlocfilehash: ddc154601752cc856f00dd4f3207952ab7e0e3e0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613068"
---
# <a name="creating-mutually-exclusive-checkboxes-c"></a>建立互斥的核取方塊 (C#)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.cs.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0CS.pdf)

> 只有一組選項可以選取時，通常會使用選項按鈕。 但有一個缺點：選取群組中的一個選項按鈕之後，就無法取消核取所有選項按鈕。 您可以隨時取消核取核取方塊，但不會互斥。 本教學課程提供兩種方法的最佳選擇：彼此互斥的核取方塊。

## <a name="overview"></a>概觀

只有一組選項可以選取時，通常會使用選項按鈕。 但有一個缺點：選取群組中的一個選項按鈕之後，就無法取消核取所有選項按鈕。 您可以隨時取消核取核取方塊，但不會互斥。 本教學課程提供兩種方法的最佳選擇：彼此互斥的核取方塊。

## <a name="steps"></a>步驟

ASP.NET AJAX Control 工具組包含 MutuallyExclusiveCheckBox 擴充項。 這可讓程式設計人員將任何核取方塊指派給組名（`Key` 屬性）。 從相同群組中的所有核取方塊，一次只能選取一個。

讓我們從將兩個核取方塊放在新的 ASP.NET 網頁開始。 有更多，但其中兩個都足以展示原則：

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample1.aspx)]

對於這兩個核取方塊，MutuallyExclusiveCheckBoxExtender 控制項都必須放在頁面上。 這兩個索引鍵屬性都必須具有相同的值，就像 [HTML] 選項按鈕元素的 [值] 屬性一樣，表示它們所屬的群組。 擴充項的 TargetControlID 屬性會指向核取方塊的識別碼。

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample2.aspx)]

最後，包含 ASP.NET AJAX 控制項工具組的所有元素所需的 ASP.NET AJAX `ScriptManager`：

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample3.aspx)]

儲存並執行頁面：您可以勾選和取消核取這兩個核取方塊，不過，您無法同時選取這兩個核取方塊。

[一次只能檢查一個核取方塊 ![](creating-mutually-exclusive-checkboxes-cs/_static/image2.png)](creating-mutually-exclusive-checkboxes-cs/_static/image1.png)

一次只能檢查一個核取方塊（[按一下以查看完整大小的影像](creating-mutually-exclusive-checkboxes-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [下一個](creating-mutually-exclusive-checkboxes-vb.md)
