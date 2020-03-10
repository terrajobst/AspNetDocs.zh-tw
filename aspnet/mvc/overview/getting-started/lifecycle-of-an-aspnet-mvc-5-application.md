---
uid: mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
title: ASP.NET MVC 5 應用程式的生命週期 |Microsoft Docs
author: cephalin
description: 下載 PDF 檔，以圖表 ASP.NET MVC 5 應用程式的生命週期。 本生命週期檔提供 MVC 生命週期的高階觀點 。
ms.author: riande
ms.date: 02/28/2014
ms.assetid: 9c1e3a75-b644-4480-8326-11300b1ec4b3
msc.legacyurl: /mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
msc.type: authoredcontent
ms.openlocfilehash: f4a9b3fb61552b070db11fba617b5627fcd71cd5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78582198"
---
# <a name="lifecycle-of-an-aspnet-mvc-5-application"></a>ASP.NET MVC 5 應用程式生命週期

依[Cephas Lin](https://github.com/cephalin)

[下載 PDF 檔](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)

在這裡，您可以下載一份 PDF 檔，它會將每個 ASP.NET MVC 5 應用程式的生命週期，從接收 HTTP 要求，到將 HTTP 回應傳送回用戶端。 它是設計來做為 ASP.NET MVC 新手的教育工具，也是針對需要深入瞭解應用程式特定層面的人員所做的參考。 PDF 檔具有下列功能：

- 相關的[HttpApplication](https://msdn.microsoft.com/library/system.web.httpapplication.aspx)階段，可協助您瞭解 MVC 與[ASP.NET 應用程式生命週期](https://msdn.microsoft.com/library/bb470252.aspx)的整合位置。
- MVC 應用程式生命週期的高階觀點，您可以在其中瞭解每個 MVC 應用程式在要求處理管線中傳遞的主要階段。  
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image1.jpg)
- 詳細資料檢視，顯示向下切入要求處理管線的詳細資料。 您可以比較高階視圖和詳細資料檢視，查看如何將生命週期詳細資料收集到各種階段。 [下載 PDF](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)以查看較大的視圖。
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image2.jpg)
- 在要求處理管線中，[控制器](https://msdn.microsoft.com/library/system.web.mvc.controller.aspx)物件上所有可覆寫方法的位置和用途。 您不一定需要覆寫任何一種方法，但請務必瞭解其在應用程式生命週期中的角色，讓您可以在適當的生命週期階段針對您想要的效果撰寫程式碼。
- 放大的圖表會顯示每個篩選類型（驗證、授權、動作和結果）的叫用方式。
- 從詳細資料檢視中每個感興趣的點連結到有用的文章或 blog。

## <a name="next-steps"></a>後續步驟

這份檔是否符合您的需求？ 歡迎您提供寶貴的意見。 如果您對應用程式中的 ASP.NET MVC 生命週期有任何疑問， [Stackoverflow](http://stackoverflow.com/help)和[ASP.NET MVC 論壇](https://forums.asp.net/1146.aspx)是很棒的地方。 請在 twitter 上追蹤[我](https://twitter.com/Cephas_MSFT)的最新教學課程，以取得更新。
