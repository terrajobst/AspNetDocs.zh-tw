---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: 加入模型 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: c5525cfe940cadff5113c63eb0508d15697b5606
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78615749"
---
# <a name="adding-a-model"></a>新增模型

依[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [Tutorial Note](index.md)]

在本節中，您將新增一些類別來管理資料庫中的電影。 這些類別將會是 ASP.NET MVC 應用程式&quot; 部分的 &quot;模型。

您將使用稱為[Entity Framework](https://docs.microsoft.com/ef/)的 .NET Framework 資料存取技術，來定義和使用這些模型類別。 Entity Framework （通常稱為 EF）支援稱為*Code First*的開發範例。 Code First 可讓您藉由撰寫簡單的類別來建立模型物件。 （這些也稱為 POCO 類別，從 &quot;純舊 CLR 物件。&quot;）接著，您可以從類別中即時建立資料庫，以實現非常乾淨快速的開發工作流程。 如果您需要先建立資料庫，您仍然可以遵循此教學課程，以瞭解 MVC 和 EF 應用程式的開發。 接著，您可以遵循 Tom Fizmakens [ASP.NET](xref:visual-studio/overview/2013/aspnet-scaffolding-overview)樣板教學課程，其中涵蓋資料庫的第一種方法。

## <a name="adding-model-classes"></a>新增模型類別

在**方案總管**中，以滑鼠右鍵按一下 [*模型*] 資料夾，選取 [**新增**]，然後選取 [**類別**]。

![](adding-a-model/_static/image1.png)

輸入 &quot;電影&quot;的*類別*名稱。

將下列五個屬性新增至 `Movie` 類別：

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

我們會使用 `Movie` 類別來代表資料庫中的電影。 `Movie` 物件的每個實例都會對應至資料庫資料表中的資料列，而 `Movie` 類別的每個屬性都會對應到資料表中的資料行。

注意：若要使用 System.object 和相關類別，您必須安裝[Entity Framework NuGet 套件](https://www.nuget.org/packages/EntityFramework/)。 依照連結取得進一步的指示。

在相同的檔案中，新增下列 `MovieDBContext` 類別：

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

`MovieDBContext` 類別代表 Entity Framework 的電影資料庫內容，它會處理資料庫中的 `Movie` 類別實例的提取、儲存和更新。 `MovieDBContext` 衍生自 Entity Framework 所提供的 `DbContext` 基類。

為了能夠參考 `DbContext` 和 `DbSet`，您必須在檔案頂端新增下列 `using` 語句：

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

若要這麼做，您可以手動新增 using 語句，或將滑鼠停留在紅色曲線上，按一下 `Show potential fixes` 然後按一下 `using System.Data.Entity;`

![](adding-a-model/_static/image2.png)

注意：已移除數個未使用的 `using` 語句。 Visual Studio 會將未使用的相依性顯示為灰色。 若要移除未使用的相依性，您可以將滑鼠停留在灰色相依性上，按一下 `Show potential fixes` 然後按一下 **移除未使用**

![](adding-a-model/_static/image3.png)

我們終於加入了模型（MVC 中的 M）。 在下一節中，您將使用資料庫連接字串。

> [!div class="step-by-step"]
> [上一頁](adding-a-view.md)
> [下一頁](creating-a-connection-string.md)
