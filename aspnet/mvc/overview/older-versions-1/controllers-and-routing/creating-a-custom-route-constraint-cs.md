---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-cs
title: 建立自訂路由條件約束C#（） |Microsoft Docs
author: StephenWalther
description: Stephen Walther 會示範如何建立自訂路由條件約束。 我們會實一個簡單的自訂條件約束，以防止路由符合
ms.author: riande
ms.date: 02/16/2009
ms.assetid: a4f4bf4e-abcc-4650-8f43-527e48b52fe6
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: 98d5839e3d2623665770ccc5689c28f9eb29c8f6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601448"
---
# <a name="creating-a-custom-route-constraint-c"></a>建立自訂的路由條件約束 (C#)

依[Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther 會示範如何建立自訂路由條件約束。 我們會執行簡單的自訂條件約束，以防止在來自遠端電腦的瀏覽器要求時比對路由。

本教學課程的目的是要示範如何建立自訂路由條件約束。 自訂路由條件約束可讓您避免比對路由，除非符合某些自訂條件。

在本教學課程中，我們會建立 Localhost 路由條件約束。 Localhost 路由條件約束只符合從本機電腦提出的要求。 跨網際網路的遠端要求不相符。

您可以藉由執行 IRouteConstraint 介面來執行自訂路由條件約束。 這是一個非常簡單的介面，可描述單一方法：

[!code-csharp[Main](creating-a-custom-route-constraint-cs/samples/sample1.cs)]

方法會傳回布林值。 如果您傳回 false，與條件約束相關聯的路由就不會符合瀏覽器要求。

[清單 1] 中包含 Localhost 條件約束。

**清單 1-LocalhostConstraint.cs**

[!code-csharp[Main](creating-a-custom-route-constraint-cs/samples/sample2.cs)]

[清單 1] 中的條件約束會利用 HttpRequest 類別所公開的 IsLocal 屬性。 當要求的 IP 位址是127.0.0.1，或要求的 IP 與伺服器的 IP 位址相同時，此屬性會傳回 true。

在 global.asax 檔案中定義的路由內，您可以使用自訂條件約束。 [清單 2] 中的 global.asax 檔案使用 Localhost 條件約束，以防止任何人要求系統管理頁面，除非他們從本機伺服器提出要求。 例如，從遠端伺服器進行/Admin/DeleteAll 的要求將會失敗。

**清單 2-global.asax**

[!code-csharp[Main](creating-a-custom-route-constraint-cs/samples/sample3.cs)]

Localhost 條件約束會用於管理路由的定義中。 此路由不會與遠端瀏覽器要求相符。 不過，請注意，global.asax 中定義的其他路由可能符合相同的要求。 請務必瞭解，條件約束會防止特定路由符合要求，而不是在 global.asax 檔案中定義的所有路由。

請注意，預設路由已從 [清單 2] 中的 global.asax 檔案加上批註。 如果您包含預設路由，則預設路由會符合管理控制器的要求。 在此情況下，即使遠端使用者的要求不符合管理路由，仍然可以叫用管理控制器的動作。

> [!div class="step-by-step"]
> [上一頁](creating-a-route-constraint-cs.md)
> [下一頁](asp-net-mvc-controller-overview-vb.md)
