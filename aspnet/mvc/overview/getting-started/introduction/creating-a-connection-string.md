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
# <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="c244a-102">建立連接字串以及使用 SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="c244a-102">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="c244a-103">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="c244a-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [Tutorial Note](index.md)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="c244a-104">建立連接字串以及使用 SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="c244a-104">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="c244a-105">您所建立的 `MovieDBContext` 類別會處理連接到資料庫的工作，並將 `Movie` 物件對應至資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="c244a-105">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="c244a-106">不過，您可能會問的一個問題，就是如何指定要連接的資料庫。</span><span class="sxs-lookup"><span data-stu-id="c244a-106">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="c244a-107">您實際上不需要指定要使用的資料庫，Entity Framework 會預設為使用[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)。</span><span class="sxs-lookup"><span data-stu-id="c244a-107">You don't actually have to specify which database to use, Entity Framework will default to using [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span></span> <span data-ttu-id="c244a-108">在本節中，我們會在應用*程式的 web.config*檔案中明確新增連接字串。</span><span class="sxs-lookup"><span data-stu-id="c244a-108">In this section we'll explicitly add a connection string in the *Web.config* file of the application.</span></span>

## <a name="sql-server-express-localdb"></a><span data-ttu-id="c244a-109">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="c244a-109">SQL Server Express LocalDB</span></span>

<span data-ttu-id="c244a-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)是輕量版的 SQL Server Express 資料庫引擎，會視需要啟動並在使用者模式中執行。</span><span class="sxs-lookup"><span data-stu-id="c244a-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) is a lightweight version of the SQL Server Express Database Engine that starts on demand and runs in user mode.</span></span> <span data-ttu-id="c244a-111">LocalDB 會在 SQL Server Express 的特殊執行模式下執行，可讓您使用資料庫做為 *.mdf*檔案。</span><span class="sxs-lookup"><span data-stu-id="c244a-111">LocalDB runs in a special execution mode of SQL Server Express that enables you to work with databases as *.mdf* files.</span></span> <span data-ttu-id="c244a-112">LocalDB 資料庫檔案通常會保留在 Web 專案的*應用程式\_Data*資料夾中。</span><span class="sxs-lookup"><span data-stu-id="c244a-112">Typically, LocalDB database files are kept in the *App\_Data* folder of a web project.</span></span>

<span data-ttu-id="c244a-113">不建議在生產 web 應用程式中使用 SQL Server Express。</span><span class="sxs-lookup"><span data-stu-id="c244a-113">SQL Server Express is not recommended for use in production web applications.</span></span> <span data-ttu-id="c244a-114">LocalDB 不應用於具有 web 應用程式的生產環境，因為它不是設計來與 IIS 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="c244a-114">LocalDB in particular should not be used for production with a web application because it is not designed to work with IIS.</span></span> <span data-ttu-id="c244a-115">不過，您可以輕鬆地將 LocalDB 資料庫移轉至 SQL Server 或 SQL Azure。</span><span class="sxs-lookup"><span data-stu-id="c244a-115">However, a LocalDB database can be easily migrated to SQL Server or SQL Azure.</span></span>

<span data-ttu-id="c244a-116">在 Visual Studio 2017 中，預設會隨 Visual Studio 安裝 LocalDB。</span><span class="sxs-lookup"><span data-stu-id="c244a-116">In Visual Studio 2017, LocalDB is installed by default with Visual Studio.</span></span>

<span data-ttu-id="c244a-117">根據預設，Entity Framework 會尋找名為的連接字串，與物件內容類別（此專案的`MovieDBContext`）相同。</span><span class="sxs-lookup"><span data-stu-id="c244a-117">By default, the Entity Framework looks for a connection string named the same as the object context class (`MovieDBContext` for this project).</span></span> <span data-ttu-id="c244a-118">如需詳細資訊，請參閱[ASP.NET Web 應用程式的 SQL Server 連接字串](https://msdn.microsoft.com/library/jj653752.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c244a-118">For more information see [SQL Server Connection Strings for ASP.NET Web Applications](https://msdn.microsoft.com/library/jj653752.aspx).</span></span>

<span data-ttu-id="c244a-119">開啟應用*程式根目錄 web.config*檔案，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c244a-119">Open the application root *Web.config* file shown below.</span></span> <span data-ttu-id="c244a-120">（不是*Views*資料夾中*的 web.config 檔案*）。</span><span class="sxs-lookup"><span data-stu-id="c244a-120">(Not the *Web.config* file in the *Views* folder.)</span></span>

![](creating-a-connection-string/_static/image1.png)

<span data-ttu-id="c244a-121">尋找 `<connectionStrings>` 元素：</span><span class="sxs-lookup"><span data-stu-id="c244a-121">Find the `<connectionStrings>` element:</span></span>

![](creating-a-connection-string/_static/image2.png)

<span data-ttu-id="c244a-122">將下列連接字串新增*至 web.config 檔案*中的 `<connectionStrings>` 元素。</span><span class="sxs-lookup"><span data-stu-id="c244a-122">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample1.xml)]

<span data-ttu-id="c244a-123">下列範例會顯示已新增連接字串的*web.config*檔案的一部分：</span><span class="sxs-lookup"><span data-stu-id="c244a-123">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample2.xml)]

<span data-ttu-id="c244a-124">這兩個連接字串非常類似。</span><span class="sxs-lookup"><span data-stu-id="c244a-124">The two connection strings are very similar.</span></span> <span data-ttu-id="c244a-125">第一個連接字串的名稱為 `DefaultConnection`，並用於成員資格資料庫，以控制可以存取應用程式的人員。</span><span class="sxs-lookup"><span data-stu-id="c244a-125">The first connection string is named `DefaultConnection` and is used for the membership database to control who can access the application.</span></span> <span data-ttu-id="c244a-126">您已新增的連接字串會指定名為*Movie .mdf*的 LocalDB 資料庫，位於*應用程式\_Data*資料夾中。</span><span class="sxs-lookup"><span data-stu-id="c244a-126">The connection string you've added specifies a LocalDB database named *Movie.mdf* located in the *App\_Data* folder.</span></span> <span data-ttu-id="c244a-127">我們不會在本教學課程中使用成員資格資料庫，如需有關成員資格、驗證和安全性的詳細資訊，請參閱我的教學課程[使用驗證和 SQL DB 建立 ASP.NET MVC 應用程式並部署至 Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。</span><span class="sxs-lookup"><span data-stu-id="c244a-127">We won't use the membership database in this tutorial, for more information on membership, authentication and security, see my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span>

<span data-ttu-id="c244a-128">連接字串的名稱必須符合[DbCoNtext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)類別的名稱。</span><span class="sxs-lookup"><span data-stu-id="c244a-128">The name of the connection string must match the name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class.</span></span>

[!code-csharp[Main](creating-a-connection-string/samples/sample3.cs?highlight=15)]

<span data-ttu-id="c244a-129">您實際上不需要加入 `MovieDBContext` 連接字串。</span><span class="sxs-lookup"><span data-stu-id="c244a-129">You don't actually need to add the `MovieDBContext` connection string.</span></span> <span data-ttu-id="c244a-130">如果您未指定連接字串，Entity Framework 會在使用者目錄中建立具有[DbCoNtext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)類別之完整名稱的 LocalDB 資料庫（在此案例中為 `MvcMovie.Models.MovieDBContext`）。</span><span class="sxs-lookup"><span data-stu-id="c244a-130">If you don't specify a connection string, Entity Framework will create a LocalDB database in the users directory with the fully qualified name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class (in this case `MvcMovie.Models.MovieDBContext`).</span></span> <span data-ttu-id="c244a-131">只要有，您就可以將資料庫命名為任何您喜歡的名稱 *。MDF*尾碼。</span><span class="sxs-lookup"><span data-stu-id="c244a-131">You can name the database anything you like, as long as it has the *.MDF* suffix.</span></span> <span data-ttu-id="c244a-132">例如，我們可以將資料庫命名為*MyFilms*。</span><span class="sxs-lookup"><span data-stu-id="c244a-132">For example, we could name the database *MyFilms.mdf*.</span></span>

<span data-ttu-id="c244a-133">接下來，您將建立新的 `MoviesController` 類別，您可以用它來顯示電影資料，並允許使用者建立新的電影清單。</span><span class="sxs-lookup"><span data-stu-id="c244a-133">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c244a-134">[上一頁](adding-a-model.md)
> [下一頁](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="c244a-134">[Previous](adding-a-model.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
