---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
title: 建立路由條件約束（C#） |Microsoft Docs
author: StephenWalther
description: 在本教學課程中，Stephen Walther 將示範如何使用正則運算式來建立路由條件約束，以控制瀏覽器要求如何符合路由。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 0bfd06b1-12d3-4fbb-9779-a82e5eb7fe7d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: 51ef859287b3424faf85f4a3606a220ab48a9466
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78582009"
---
# <a name="creating-a-route-constraint-c"></a>建立路由條件約束 (C#)

依[Stephen Walther](https://github.com/StephenWalther)

> 在本教學課程中，Stephen Walther 將示範如何使用正則運算式來建立路由條件約束，以控制瀏覽器要求如何符合路由。

您可以使用路由條件約束來限制符合特定路由的瀏覽器要求。 您可以使用正則運算式來指定路由條件約束。

例如，假設您已在 global.asax 檔案的 [清單 1] 中定義路由。

**清單 1-Global.asax.cs**

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample1.cs)]

[清單 1] 包含名為 Product 的路由。 您可以使用產品路線，將瀏覽器要求對應至 [清單 2] 中所包含的 ProductController。

**清單 2-Controllers\ProductController.cs**

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample2.cs)]

請注意，產品控制器所公開的詳細資料（）動作會接受名為 productId 的單一參數。 這個參數是整數參數。

清單1中定義的路由會符合下列任何 Url：

- /Product/23
- /Product/7

可惜的是，路由也會符合下列 Url：

- /Product/blah
- /Product/apple

由於 Details （）動作需要整數參數，因此，要求若包含整數值以外的專案，將會造成錯誤。 例如，如果您在瀏覽器中輸入 URL/Product/apple，則會出現 [圖 1] 中的錯誤頁面。

[![[新增專案] 對話方塊](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)

**圖 01**：查看頁面分解（[按一下以觀看完整大小的影像](creating-a-route-constraint-cs/_static/image2.png)）

您真正想要做的只是符合包含適當整數 productId 的 Url。 定義路由以限制符合路由的 Url 時，您可以使用條件約束。 [清單 3] 中已修改的產品路由包含僅符合整數的正則運算式條件約束。

**清單 3-Global.asax.cs**

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample3.cs)]

正則運算式 \d + 符合一或多個整數。 此條件約束會使產品路由符合下列 Url：

- /Product/3
- /Product/8999

但不是下列 Url：

- /Product/apple
- /Product

- 這些瀏覽器要求將由另一個路由處理，或者，如果沒有相符的路由，就會傳回「找*不到資源*」錯誤。

> [!div class="step-by-step"]
> [上一頁](creating-custom-routes-cs.md)
> [下一頁](creating-a-custom-route-constraint-cs.md)
