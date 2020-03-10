---
uid: mvc/overview/getting-started/introduction/creating-a-connection-string
title: 建立連接字串並使用 SQL Server LocalDB |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 6127804d-c1a9-414d-8429-7f3dd0f56e97
msc.legacyurl: /mvc/overview/getting-started/introduction/creating-a-connection-string
msc.type: authoredcontent
ms.openlocfilehash: 20781ad760d3a0e4559ec4c7e18528f3686dcc02
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78615665"
---
# <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>建立連接字串以及使用 SQL Server LocalDB

依[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [Tutorial Note](index.md)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>建立連接字串以及使用 SQL Server LocalDB

您所建立的 `MovieDBContext` 類別會處理連接到資料庫的工作，並將 `Movie` 物件對應至資料庫記錄。 不過，您可能會問的一個問題，就是如何指定要連接的資料庫。 您實際上不需要指定要使用的資料庫，Entity Framework 會預設為使用[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)。 在本節中，我們會在應用*程式的 web.config*檔案中明確新增連接字串。

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)是輕量版的 SQL Server Express 資料庫引擎，會視需要啟動並在使用者模式中執行。 LocalDB 會在 SQL Server Express 的特殊執行模式下執行，可讓您使用資料庫做為 *.mdf*檔案。 LocalDB 資料庫檔案通常會保留在 Web 專案的*應用程式\_Data*資料夾中。

不建議在生產 web 應用程式中使用 SQL Server Express。 LocalDB 不應用於具有 web 應用程式的生產環境，因為它不是設計來與 IIS 搭配使用。 不過，您可以輕鬆地將 LocalDB 資料庫移轉至 SQL Server 或 SQL Azure。

在 Visual Studio 2017 中，預設會隨 Visual Studio 安裝 LocalDB。

根據預設，Entity Framework 會尋找名為的連接字串，與物件內容類別（此專案的`MovieDBContext`）相同。 如需詳細資訊，請參閱[ASP.NET Web 應用程式的 SQL Server 連接字串](https://msdn.microsoft.com/library/jj653752.aspx)。

開啟應用*程式根目錄 web.config*檔案，如下所示。 （不是*Views*資料夾中*的 web.config 檔案*）。

![](creating-a-connection-string/_static/image1.png)

尋找 `<connectionStrings>` 元素：

![](creating-a-connection-string/_static/image2.png)

將下列連接字串新增*至 web.config 檔案*中的 `<connectionStrings>` 元素。

[!code-xml[Main](creating-a-connection-string/samples/sample1.xml)]

下列範例會顯示已新增連接字串的*web.config*檔案的一部分：

[!code-xml[Main](creating-a-connection-string/samples/sample2.xml)]

這兩個連接字串非常類似。 第一個連接字串的名稱為 `DefaultConnection`，並用於成員資格資料庫，以控制可以存取應用程式的人員。 您已新增的連接字串會指定名為*Movie .mdf*的 LocalDB 資料庫，位於*應用程式\_Data*資料夾中。 我們不會在本教學課程中使用成員資格資料庫，如需有關成員資格、驗證和安全性的詳細資訊，請參閱我的教學課程[使用驗證和 SQL DB 建立 ASP.NET MVC 應用程式並部署至 Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。

連接字串的名稱必須符合[DbCoNtext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)類別的名稱。

[!code-csharp[Main](creating-a-connection-string/samples/sample3.cs?highlight=15)]

您實際上不需要加入 `MovieDBContext` 連接字串。 如果您未指定連接字串，Entity Framework 會在使用者目錄中建立具有[DbCoNtext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)類別之完整名稱的 LocalDB 資料庫（在此案例中為 `MvcMovie.Models.MovieDBContext`）。 只要有，您就可以將資料庫命名為任何您喜歡的名稱 *。MDF*尾碼。 例如，我們可以將資料庫命名為*MyFilms*。

接下來，您將建立新的 `MoviesController` 類別，您可以用它來顯示電影資料，並允許使用者建立新的電影清單。

> [!div class="step-by-step"]
> [上一頁](adding-a-model.md)
> [下一頁](accessing-your-models-data-from-a-controller.md)
