---
uid: mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
title: 如何：為 MVC 應用程式建立自訂 HTML Helper？ | Microsoft Docs
author: rick-anderson
description: 在這段影片中，Chris Pels 示範如何建立在 MVC 應用程式中，標準集內無法使用的自訂 HtmlHelper。 首先，範例 MVC 應用程式 。
ms.author: riande
ms.date: 12/11/2009
ms.assetid: 58b5eb15-4160-4ce2-ae70-6ba94262ea73
msc.legacyurl: /mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
msc.type: video
ms.openlocfilehash: 60953243d3038667e4f729b1394e68f0c9d7c178
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559042"
---
# <a name="how-do-i-create-a-custom-html-helper-for-an-mvc-application"></a>如何：為 MVC 應用程式建立自訂 HTML Helper？

依[Chris Pels](https://twitter.com/chrispels)

在這段影片中，Chris Pels 示範如何建立在 MVC 應用程式中，標準集內無法使用的自訂 HtmlHelper。 首先，會使用示範控制器和 view 來建立範例 MVC 應用程式，以測試自訂 HtmlHelper。 接下來，系統會使用公開函式建立模組，此方法是代表自訂 HtmlHelper 之執行的擴充方法。 自訂 helper 是用來在頁面中建立 `<img>` 標記，並接收數個輸入參數，包括影像標記的識別碼、url 和替代文字。 然後，會將邏輯新增至函式，以使用指定的資訊傳回已完成的 `<img>` 標記。 然後，在 [示範] 頁面上使用自訂 HtmlHelper 來顯示影像。 最後，自訂 HtmlHelper 會展開以包含多個「函數覆寫」，以提供更輕鬆地建立不同 `<img>` 標記的彈性。

[&#9654;觀看影片（18分鐘）](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-create-a-custom-html-helper-for-an-mvc-application)

> [!div class="step-by-step"]
> [上一頁](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
> [下一頁](how-do-i-work-with-model-binders-in-an-mvc-application.md)
