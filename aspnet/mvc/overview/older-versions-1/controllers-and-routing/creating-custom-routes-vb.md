---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
title: 建立自訂路由（VB） |Microsoft Docs
author: microsoft
description: 瞭解如何將自訂路由新增至 ASP.NET MVC 應用程式。 在本教學課程中，您將瞭解如何修改 global.asax 檔案中的預設路由表。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 6ac5758b-6199-42af-adcb-21954b864951
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
msc.type: authoredcontent
ms.openlocfilehash: 22b44e9e575c9d404881a23ee735bb0c8b7109e1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601294"
---
# <a name="creating-custom-routes-vb"></a>建立自訂路由 (VB)

由[Microsoft](https://github.com/microsoft)

> 瞭解如何將自訂路由新增至 ASP.NET MVC 應用程式。 在本教學課程中，您將瞭解如何修改 global.asax 檔案中的預設路由表。

在本教學課程中，您將瞭解如何將自訂路由新增至 ASP.NET MVC 應用程式。 您將瞭解如何使用自訂路由來修改 global.asax 檔案中的預設路由表。

在 ASP.NET MVC 應用程式中，預設路由表會正常執行。 不過，您可能會發現您有特殊的路由需求。 在此情況下，您可以建立自訂路由。

例如，假設您要建立一個 blog 應用程式。 您可能會想要處理傳入的要求，如下所示：

/Archive/12-25-2009

當使用者輸入此要求時，您會想要傳回對應于日期12/25/2009 的 blog 專案。 若要處理這種類型的要求，您必須建立自訂路由。

[清單 1] 中的 global.asax 檔案包含新的自訂路由，名為 Blog，它會處理類似/Archive/*專案日期*的要求。

**清單 1-global.asax （含自訂路由）**

[!code-vb[Main](creating-custom-routes-vb/samples/sample1.vb)]

您新增至路由表的路由順序很重要。 新的自訂 Blog 路由會在現有的預設路由之前新增。 如果您反轉順序，則預設路由一律會呼叫，而不是自訂路由。

自訂的 Blog 路由會符合任何以/Archive/. 開頭的要求 因此，它會符合下列所有 Url：

- /Archive/12-25-2009

- /Archive/10-6-2004

- /Archive/apple

自訂路由會將傳入要求對應至名為 Archive 的控制器，並叫用 Entry （）動作。 呼叫 Entry （）方法時，會將專案日期當做名為 entryDate 的參數傳遞。

您可以在 [清單 2] 中使用與控制器的 Blog 自訂路由。

**清單 2-ArchiveController .vb**

[!code-vb[Main](creating-custom-routes-vb/samples/sample2.vb)]

請注意，[清單 2] 中的 Entry （）方法會接受 DateTime 類型的參數。 MVC 架構很聰明，可以將 URL 中的輸入日期自動轉換成日期時間值。 如果 URL 中的 entry date 參數無法轉換成 DateTime，則會引發錯誤（請參閱 [圖 1]）。

**圖 1-轉換參數時發生的錯誤**

[![[新增專案] 對話方塊](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)

**圖 01**：轉換參數時發生錯誤（[按一下以觀看完整大小的影像](creating-custom-routes-vb/_static/image2.png)）

## <a name="summary"></a>總結

本教學課程的目的是要示範如何建立自訂路由。 您已瞭解如何將自訂路由新增至代表 blog 專案之 global.asax 檔案中的路由表。 我們已討論如何將 blog 專案的要求對應至名為 ArchiveController 的控制器，以及名為 Entry （）的控制器動作。

> [!div class="step-by-step"]
> [上一頁](asp-net-mvc-controller-overview-vb.md)
> [下一頁](creating-a-route-constraint-vb.md)
