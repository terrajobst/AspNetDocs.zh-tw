---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: 瞭解 ASP.NET MVC 執行程式 |Microsoft Docs
author: microsoft
description: 瞭解 ASP.NET MVC 架構如何逐步處理瀏覽器要求。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 28940947253e0af43886cf1231f8aaf4615526cc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541514"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a>了解 ASP.NET MVC 執行程序

由[Microsoft](https://github.com/microsoft)

> 瞭解 ASP.NET MVC 架構如何逐步處理瀏覽器要求。

ASP.NET MVC 型 Web 應用程式的要求會先通過**UrlRoutingModule**物件，也就是 HTTP 模組。 此模組會剖析該要求並執行路由選取。 **UrlRoutingModule**物件會選取符合目前要求的第一個路由物件。 （路由物件是可執行**RouteBase**的類別，通常是**路由**類別的實例）。如果沒有符合的路由， **UrlRoutingModule**物件就不會執行任何工作，而且會讓要求回到一般的 ASP.NET 或 IIS 要求處理。

從選取的**路由**物件中， **UrlRoutingModule**物件會取得與**路由**物件相關聯的**IRouteHandler**物件。 一般來說，在 MVC 應用程式中，這會是**MvcRouteHandler**的實例。 **IRouteHandler**實例會建立**IHttpHandler**物件，並將它傳遞至**IHttpCoNtext**物件。 根據預設，MVC 的**IHttpHandler**實例是**MvcHandler**物件。 **MvcHandler**物件接著會選取最後會處理要求的控制器。

> [!NOTE]
> 當 ASP.NET MVC Web 應用程式在 IIS 7.0 中執行時，MVC 專案不需要副檔名。 然而，在 IIS 6.0 中，處理常式需要您將 .mvc 副檔名對應至 ASP.NET ISAPI DLL。

模組和處理常式是 ASP.NET MVC 架構的進入點。 它們會執行下列動作：

- 選取 MVC Web 應用程式中適當的控制器。
- 取得特定控制器執行個體。
- 呼叫控制器的**Execute**方法。

下列列出 MVC Web 專案的執行階段：

- 接收應用程式的第一個要求 

    - 在 global.asax 檔案中，**路由**物件會新增至**RouteTable**物件。
- 執行路由 

    - **UrlRoutingModule**模組會使用**RouteTable**集合中的第一個相符**路由**物件來建立**RouteData**物件，然後用它來建立**RequestCoNtext** （**IHttpCoNtext**）物件。
- 建立 MVC 要求處理常式 

    - **MvcRouteHandler**物件會建立**MvcHandler**類別的實例，並將它傳遞至**RequestCoNtext**實例。
- 建立控制器 

    - **MvcHandler**物件會使用**RequestCoNtext**實例來識別**IControllerFactory**物件（通常是**DefaultControllerFactory**類別的實例），以使用建立控制器實例。
- 執行控制器- **MvcHandler**實例會呼叫控制器 s**執行**方法。 |
- 叫用動作 

    - 大部分的控制器會繼承自**控制器**基類。 對於執行這項操作的控制器而言，與控制器相關聯的**ControllerActionInvoker**物件會決定要呼叫控制器類別的哪一個動作方法，然後再呼叫該方法。
- 執行結果 

    - 一般動作方法可能會接收使用者輸入、準備適當的回應資料，然後藉由傳回結果類型來執行結果。 可以執行的內建結果類型包括下列各項： **ViewResult** （它會轉譯視圖，而是最常用的結果類型）、 **RedirectToRouteResult**、 **RedirectResult**、 **ContentResult**、 **JsonResult**和**EmptyResult**。
