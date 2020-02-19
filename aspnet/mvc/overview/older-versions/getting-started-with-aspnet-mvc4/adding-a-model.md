---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
title: 加入模型 |Microsoft Docs
author: Rick-Anderson
description: 注意：本教學課程的更新版本可在這裡使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更容易遵循和示範 。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 53db72da-e0b9-44d9-b60b-6e6988c00b28
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: a9851d93dde495814f67fa0c807d3534f5f0d8ef
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457800"
---
# <a name="adding-a-model"></a>新增模型

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > 本教學課程的更新版本可在[這裡](../../getting-started/introduction/getting-started.md)取得，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。 它更安全、更容易遵循，並示範更多功能。

在本節中，您將新增一些類別來管理資料庫中的電影。 這些類別會是 ASP.NET MVC 應用程式&quot; 部分的 &quot;模型。

您將使用稱為[Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx)的 .NET Framework 資料存取技術，來定義和使用這些模型類別。 Entity Framework （通常稱為 EF）支援稱為*Code First*的開發範例。 Code First 可讓您藉由撰寫簡單的類別來建立模型物件。 （這些也稱為 POCO 類別，從 &quot;純舊 CLR 物件。&quot;）接著，您可以從類別中即時建立資料庫，以實現非常乾淨快速的開發工作流程。

## <a name="adding-model-classes"></a>新增模型類別

在**方案總管**中，以滑鼠右鍵按一下 [*模型*] 資料夾，選取 [**新增**]，然後選取 [**類別**]。

![](adding-a-model/_static/image1.png)

輸入 &quot;電影&quot;的*類別*名稱。

將下列五個屬性新增至 `Movie` 類別：

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

我們會使用 `Movie` 類別來代表資料庫中的電影。 `Movie` 物件的每個實例都會對應至資料庫資料表中的資料列，而 `Movie` 類別的每個屬性都會對應到資料表中的資料行。

在相同的檔案中，新增下列 `MovieDBContext` 類別：

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

`MovieDBContext` 類別代表 Entity Framework 的電影資料庫內容，它會處理資料庫中的 `Movie` 類別實例的提取、儲存和更新。 `MovieDBContext` 衍生自 Entity Framework 所提供的 `DbContext` 基類。

為了能夠參考 `DbContext` 和 `DbSet`，您必須在檔案頂端新增下列 `using` 語句：

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

完整的*Movie.cs*檔案如下所示。 （已移除數個不需要的 using 語句）。

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>建立連接字串以及使用 SQL Server LocalDB

您所建立的 `MovieDBContext` 類別會處理連接到資料庫的工作，並將 `Movie` 物件對應至資料庫記錄。 不過，您可能會問的一個問題，就是如何指定要連接的資料庫。 您*會在應用程式的 web.config*檔案中加入連接資訊來執行此動作。

開啟應用*程式根目錄的 web.config 檔案*。 （不是*Views*資料夾中*的 web.config 檔案*）。開啟以紅色*概述的 web.config 檔案。*

![](adding-a-model/_static/image2.png)

將下列連接字串新增*至 web.config 檔案*中的 `<connectionStrings>` 元素。

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

下列範例會顯示已新增連接字串的*web.config*檔案的一部分：

[!code-xml[Main](adding-a-model/samples/sample6.xml?highlight=6-9)]

這小段的程式碼和 XML 就是您需要撰寫的所有專案，以便在資料庫中呈現及儲存電影資料。

接下來，您將建立新的 `MoviesController` 類別，您可以用它來顯示電影資料，並允許使用者建立新的電影清單。

> [!div class="step-by-step"]
> [上一頁](adding-a-view.md)
> [下一頁](accessing-your-models-data-from-a-controller.md)
