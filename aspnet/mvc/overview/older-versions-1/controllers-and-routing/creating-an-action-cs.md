---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
title: 建立動作（C#） |Microsoft Docs
author: microsoft
description: 瞭解如何將新動作新增至 ASP.NET MVC 控制器。 瞭解方法的需求是動作。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: cb33b28c-3025-4bd1-a1fa-eaa3af7bb56f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
msc.type: authoredcontent
ms.openlocfilehash: ebba935383819935ad85c95245666f4eaf6a0dca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78582051"
---
# <a name="creating-an-action-c"></a>建立動作 (C#)

由[Microsoft](https://github.com/microsoft)

> 瞭解如何將新動作新增至 ASP.NET MVC 控制器。 瞭解方法的需求是動作。

本教學課程的目的是要說明如何建立新的控制器動作。 您會瞭解動作方法的需求。 您也將瞭解如何防止方法公開為動作。

## <a name="adding-an-action-to-a-controller"></a>將動作新增至控制器

您可以藉由將新的方法加入至控制器，將新的動作新增至控制器。 例如，[清單 1] 中的控制器包含名為 Index （）的動作，以及名為 SayHello （）的動作。 這兩種方法都會公開為動作。

**清單 1-Controllers\HomeController.cs**

[!code-csharp[Main](creating-an-action-cs/samples/sample1.cs)]

若要以動作的形式公開至 universe，方法必須符合特定需求：

- 此方法必須是公用的。
- 方法不可以是靜態方法。
- 方法不可以是擴充方法。
- 方法不可以是函數、getter 或 setter。
- 方法不能有開放式泛型型別。
- 方法不是控制器基類的方法。
- 方法不能包含**ref**或**out**參數。

請注意，控制器動作的傳回型別沒有任何限制。 控制器動作可以傳回字串、DateTime、Random 類別的實例，或 void。 ASP.NET MVC 架構會將不是動作結果的任何傳回型別轉換成字串，並將字串轉譯為瀏覽器。

當您將任何不違反這些需求的方法新增至控制器時，該方法會公開為控制器動作。 請注意這裡。 連線到網際網路的任何人都可以叫用控制器動作。 例如，請不要建立 DeleteMyWebsite （）控制器動作。

## <a name="preventing-a-public-method-from-being-invoked"></a>防止叫用公用方法

如果您需要在控制器類別中建立公用方法，而且不想要將方法公開為控制器動作，則可以使用 [請以 nonaction] 屬性來避免叫用此方法。 例如，[清單 2] 中的控制器包含名為 CompanySecrets （）的公用方法，它會以 [請以 nonaction] 屬性裝飾。

**清單 2-Controllers\WorkController.cs**

[!code-csharp[Main](creating-an-action-cs/samples/sample2.cs)]

如果您嘗試藉由在瀏覽器的網址列中輸入/Work/CompanySecrets 來叫用 CompanySecrets （）控制器動作，則會收到 [圖 1] 中的錯誤訊息。

[![叫用請以 nonaction 方法](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)

**圖 01**：叫用請以 nonaction 方法（[按一下以查看完整大小的影像](creating-an-action-cs/_static/image2.png)）

> [!div class="step-by-step"]
> [上一頁](creating-a-controller-cs.md)
> [下一頁](asp-net-mvc-routing-overview-vb.md)
