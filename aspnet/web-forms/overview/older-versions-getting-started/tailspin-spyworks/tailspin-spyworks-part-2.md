---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
title: 第2部分：資料存取層 |Microsoft Docs
author: JoeStagner
description: 本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。 第2部分涵蓋加入資料存取層。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5a9d5429-d70b-411c-8474-f42cf7ef8a2b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
msc.type: authoredcontent
ms.openlocfilehash: 342d2c54dfba5d052570e890f85dcf9739f9884f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78573245"
---
# <a name="part-2-data-access-layer"></a>第2部分：資料存取層

依[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks 示範為 .NET 平臺建立功能強大、可擴充的應用程式有多麼簡單。 它會說明如何使用 ASP.NET 4 中的絕佳新功能來建立線上商店，包括購物、結帳和管理。
> 
> 本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。 第2部分涵蓋加入資料存取層。

## <a id="_Toc260221668"></a>加入資料存取層

我們的電子商務應用程式將取決於兩個資料庫。

針對客戶資訊，我們將使用標準 ASP.NET 成員資格資料庫。 針對我們的購物車和產品目錄，我們將會執行 SQL Express 資料庫，如下所示。

![](tailspin-spyworks-part-2/_static/image1.jpg)

在應用程式的應用程式中建立資料庫（Commerce .mdf）\_Data 資料夾中，我們可以使用 .NET Entity Framework 繼續建立我們的資料存取層。

我們將建立名為「資料\_存取」的資料夾，並以滑鼠右鍵按一下該資料夾，然後選取 [新增專案]。

在 [已安裝的範本] 專案中，然後選取 [ADO.NET 實體資料模型] 輸入 EDM\_Commerce .edmx 作為名稱，然後按一下 [新增] 按鈕。

![](tailspin-spyworks-part-2/_static/image2.jpg)

選擇 [從資料庫產生]。

![](tailspin-spyworks-part-2/_static/image1.png)

![](tailspin-spyworks-part-2/_static/image2.png)

![](tailspin-spyworks-part-2/_static/image3.png)

![](tailspin-spyworks-part-2/_static/image3.jpg)

儲存並建立。

現在，我們已準備好新增我們的第一個功能– [產品類別] 功能表。

> [!div class="step-by-step"]
> [上一頁](tailspin-spyworks-part-1.md)
> [下一頁](tailspin-spyworks-part-3.md)
