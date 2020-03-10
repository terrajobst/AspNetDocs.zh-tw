---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
title: 新增模型（VB） |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，也就是 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: b3aa7720-5c78-4ca2-baef-9a52234fb7ce
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: e69d59aed4d74f08f1c653c4965b128c4dbe20ff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78540520"
---
# <a name="adding-a-model-vb"></a>新增模型 (VB)

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，這是 Microsoft Visual Studio 的免費版本。 開始之前，請先確定您已安裝下列必要條件。 您可以按一下下列連結來安裝所有這些專案： [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，您可以使用下列連結個別安裝必要條件：
> 
> - [Visual Studio Web Developer Express SP1 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（執行時間 + 工具支援）
> 
> 如果您使用 Visual Studio 2010，而不是 Visual Web Developer 2010，請按一下下列連結來安裝必要條件： [Visual Studio 2010 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 本主題提供具有 VB.NET 原始程式碼的 Visual Web Developer 專案。 [下載 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果您想C#要的話，請切換到本教學課程的[ C#版本](../cs/adding-a-model.md)。

## <a name="adding-a-model"></a>新增模型

在本節中，您將新增一些類別來管理資料庫中的電影。 這些類別會是 ASP.NET MVC 應用程式的「模型」部分。

您將使用稱為 Entity Framework 的 .NET Framework 資料存取技術，來定義和使用這些模型類別。 Entity Framework （通常稱為 EF）支援稱為*Code First*的開發範例。 Code First 可讓您藉由撰寫簡單的類別來建立模型物件。 （這些也稱為 POCO 類別，來自「純舊 CLR 物件」）。接著，您可以從類別中即時建立資料庫，以實現非常乾淨快速的開發工作流程。

## <a name="adding-model-classes"></a>新增模型類別

在**方案總管**中，以滑鼠右鍵按一下 [*模型*] 資料夾，選取 [**新增**]，然後選取 [**類別**]。

![](adding-a-model/_static/image1.png)

將類別命名為「電影」。

將下列五個屬性新增至 `Movie` 類別：

[!code-vb[Main](adding-a-model/samples/sample1.vb)]

我們會使用 `Movie` 類別來代表資料庫中的電影。 `Movie` 物件的每個實例都會對應至資料庫資料表中的資料列，而 `Movie` 類別的每個屬性都會對應到資料表中的資料行。

在相同的檔案中，新增下列 `MovieDBContext` 類別：

[!code-vb[Main](adding-a-model/samples/sample2.vb)]

`MovieDBContext` 類別代表 Entity Framework 的電影資料庫內容，它會處理資料庫中的 `Movie` 類別實例的提取、儲存和更新。 `MovieDBContext` 衍生自 Entity Framework 所提供的 `DbContext` 基類。 如需 `DbContext` 和 `DbSet`的詳細資訊，請參閱[Entity Framework 的生產力改進](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)。

為了能夠參考 `DbContext` 和 `DbSet`，您必須在檔案頂端新增下列 `imports` 語句：

[!code-vb[Main](adding-a-model/samples/sample3.vb)]

完整的*Movie .vb*檔案如下所示。

[!code-vb[Main](adding-a-model/samples/sample4.vb)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a>建立連接字串並使用 SQL Server Compact

您所建立的 `MovieDBContext` 類別會處理連接到資料庫的工作，並將 `Movie` 物件對應至資料庫記錄。 不過，您可能會問的一個問題，就是如何指定要連接的資料庫。 您*會在應用程式的 web.config*檔案中加入連接資訊來執行此動作。

開啟應用*程式根目錄的 web.config 檔案*。 （不是*Views*資料夾中*的 web.config 檔案*）。下圖顯示*web.config*檔案;開啟以紅色圈出的*web.config*檔案。

![](adding-a-model/_static/image2.png)

將下列連接字串新增*至 web.config 檔案*中的 `<connectionStrings>` 元素。

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

下列範例會顯示已新增連接字串的*web.config*檔案的一部分：

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

這小段的程式碼和 XML 就是您需要撰寫的所有專案，以便在資料庫中呈現及儲存電影資料。

接下來，您將建立新的 `MoviesController` 類別，您可以用它來顯示電影資料，並允許使用者建立新的電影清單。

> [!div class="step-by-step"]
> [上一頁](adding-a-view.md)
> [下一頁](accessing-your-models-data-from-a-controller.md)
