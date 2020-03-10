---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-3
title: 使用 Code First 移轉來植入資料庫 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 76e2013a-65b7-488c-834d-9448ecea378e
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-3
msc.type: authoredcontent
ms.openlocfilehash: 257bd06848adb949330856cc71eeb3d685e9d036
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557453"
---
# <a name="use-code-first-migrations-to-seed-the-database"></a>使用 Code First 移轉來植入資料庫

由[Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://github.com/MikeWasson/BookService)

在本節中，您將使用 EF 中的[Code First 移轉](https://msdn.microsoft.com/data/jj591621)，將測試資料植入資料庫。

從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。 在 [Package Manager Console] 視窗中，輸入下列命令：

[!code-console[Main](part-3/samples/sample1.cmd)]

此命令會將名為「遷移」的資料夾新增至專案，再加上 [遷移] 資料夾中名為 Configuration.cs 的程式碼檔案。

![](part-3/_static/image1.png)

開啟 Configuration.cs 檔案。 新增下列**using**語句。

[!code-csharp[Main](part-3/samples/sample2.cs)]

然後將下列程式碼新增至**設定 Seed**方法：

[!code-csharp[Main](part-3/samples/sample3.cs)]

在 [套件管理員主控台] 視窗中，輸入下列命令：

[!code-console[Main](part-3/samples/sample4.cmd)]

第一個命令會產生用來建立資料庫的程式碼，而第二個命令會執行該程式碼。 資料庫會使用[LocalDB](https://msdn.microsoft.com/library/hh510202.aspx)在本機建立。

![](part-3/_static/image2.png)

## <a name="explore-the-api-optional"></a>探索 API （選擇性）

按 F5 以在偵錯模式中執行應用程式。 Visual Studio 會開始 IIS Express 並執行您的 web 應用程式。 Visual Studio 接著會啟動瀏覽器，並開啟應用程式的首頁。

當 Visual Studio 執行 Web 專案時，它會指派通訊埠編號。 在下圖中，埠號碼為50524。 當您執行應用程式時，您會看到不同的埠號碼。

![](part-3/_static/image3.png)

首頁會使用 ASP.NET MVC 來執行。 頁面頂端有一個顯示「API」的連結。 此連結會將您帶入 Web API 的自動產生說明頁面。 （若要瞭解如何產生此說明頁面，以及如何將您自己的檔新增至頁面，請參閱[建立 ASP.NET Web API 的說明頁面](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md)。）您可以按一下 [說明] 頁面連結，以查看有關 API 的詳細資料，包括要求和回應格式。

![](part-3/_static/image4.png)

此 API 會啟用資料庫上的 CRUD 作業。 以下摘要說明 API。

| 作者 |  |
| --- | -- |
| 取得 api/作者 | 取得所有作者。 |
| 取得 api/作者/{id} | 依識別碼取得作者。 |
| 張貼/api/authors | 建立新的作者。 |
| PUT/api/authors/{id} | 更新現有的作者。 |
| 刪除/api/authors/{id} | 刪除作者。 |

| 書籍 |  |
| --- | -- |
| 取得/api/books | 取得所有書籍。 |
| 取得/api/books/{id} | 依識別碼取得書籍。 |
| 張貼/api/books | 建立新書籍。 |
| PUT/api/books/{id} | 更新現有的書籍。 |
| 刪除/api/books/{id} | 刪除書籍。 |

## <a name="view-the-database-optional"></a>查看資料庫（選擇性）

當您執行 [更新-資料庫] 命令時，EF 會建立資料庫並呼叫 `Seed` 方法。 當您在本機執行應用程式時，EF 會使用[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)。 您可以在 Visual Studio 中查看資料庫。 從 [檢視] 功能表選取 [SQL Server 物件總管]。

![](part-3/_static/image5.png)

在 [**連接到伺服器**] 對話方塊的 [**伺服器名稱**] 編輯方塊中，輸入 "（localdb） \v11.0"。 將 [**驗證**] 選項保留為 [Windows 驗證]。 按一下 **[Connect]** (連線)。

![](part-3/_static/image6.png)

Visual Studio 會連接到 LocalDB，並在 [SQL Server 物件總管] 視窗中顯示現有的資料庫。 您可以展開節點，以查看 EF 所建立的資料表。

![](part-3/_static/image7.png)

若要查看資料，請以滑鼠右鍵按一下資料表，然後選取 [**查看資料**]。

![](part-3/_static/image8.png)

下列螢幕擷取畫面顯示 [書籍] 資料表的結果。 請注意，EF 已填入具有種子資料的資料庫，且資料表包含作者資料表的外鍵。

![](part-3/_static/image9.png)

> [!div class="step-by-step"]
> [上一頁](part-2.md)
> [下一頁](part-4.md)
