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
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457241"
---
# <a name="adding-a-model-vb"></a><span data-ttu-id="6b2d9-103">新增模型 (VB)</span><span class="sxs-lookup"><span data-stu-id="6b2d9-103">Adding a Model (VB)</span></span>

<span data-ttu-id="6b2d9-104">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="6b2d9-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="6b2d9-105">本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，這是 Microsoft Visual Studio 的免費版本。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="6b2d9-106">開始之前，請先確定您已安裝下列必要條件。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="6b2d9-107">您可以按一下下列連結來安裝所有這些專案： [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="6b2d9-108">或者，您可以使用下列連結個別安裝必要條件：</span><span class="sxs-lookup"><span data-stu-id="6b2d9-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="6b2d9-109">Visual Studio Web Developer Express SP1 必要條件</span><span class="sxs-lookup"><span data-stu-id="6b2d9-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="6b2d9-110">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="6b2d9-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="6b2d9-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（執行時間 + 工具支援）</span><span class="sxs-lookup"><span data-stu-id="6b2d9-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="6b2d9-112">如果您使用 Visual Studio 2010，而不是 Visual Web Developer 2010，請按一下下列連結來安裝必要條件： [Visual Studio 2010 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="6b2d9-113">本主題提供具有 VB.NET 原始程式碼的 Visual Web Developer 專案。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="6b2d9-114">[下載 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="6b2d9-115">如果您想C#要的話，請切換到本教學課程的[ C#版本](../cs/adding-a-model.md)。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-115">If you prefer C#, switch to the [C# version](../cs/adding-a-model.md) of this tutorial.</span></span>

## <a name="adding-a-model"></a><span data-ttu-id="6b2d9-116">新增模型</span><span class="sxs-lookup"><span data-stu-id="6b2d9-116">Adding a Model</span></span>

<span data-ttu-id="6b2d9-117">在本節中，您將新增一些類別來管理資料庫中的電影。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-117">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="6b2d9-118">這些類別會是 ASP.NET MVC 應用程式的「模型」部分。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-118">These classes will be the "model" part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="6b2d9-119">您將使用稱為 Entity Framework 的 .NET Framework 資料存取技術，來定義和使用這些模型類別。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-119">You'll use a .NET Framework data-access technology known as the Entity Framework to define and work with these model classes.</span></span> <span data-ttu-id="6b2d9-120">Entity Framework （通常稱為 EF）支援稱為*Code First*的開發範例。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-120">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="6b2d9-121">Code First 可讓您藉由撰寫簡單的類別來建立模型物件。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-121">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="6b2d9-122">（這些也稱為 POCO 類別，來自「純舊 CLR 物件」）。接著，您可以從類別中即時建立資料庫，以實現非常乾淨快速的開發工作流程。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-122">(These are also known as POCO classes, from "plain-old CLR objects.") You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="6b2d9-123">新增模型類別</span><span class="sxs-lookup"><span data-stu-id="6b2d9-123">Adding Model Classes</span></span>

<span data-ttu-id="6b2d9-124">在**方案總管**中，以滑鼠右鍵按一下 [*模型*] 資料夾，選取 [**新增**]，然後選取 [**類別**]。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-124">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="6b2d9-125">將類別命名為「電影」。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-125">Name the class "Movie".</span></span>

<span data-ttu-id="6b2d9-126">將下列五個屬性新增至 `Movie` 類別：</span><span class="sxs-lookup"><span data-stu-id="6b2d9-126">Add the following five properties to the `Movie` class:</span></span>

[!code-vb[Main](adding-a-model/samples/sample1.vb)]

<span data-ttu-id="6b2d9-127">我們會使用 `Movie` 類別來代表資料庫中的電影。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-127">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="6b2d9-128">`Movie` 物件的每個實例都會對應至資料庫資料表中的資料列，而 `Movie` 類別的每個屬性都會對應到資料表中的資料行。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-128">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="6b2d9-129">在相同的檔案中，新增下列 `MovieDBContext` 類別：</span><span class="sxs-lookup"><span data-stu-id="6b2d9-129">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-vb[Main](adding-a-model/samples/sample2.vb)]

<span data-ttu-id="6b2d9-130">`MovieDBContext` 類別代表 Entity Framework 的電影資料庫內容，它會處理資料庫中的 `Movie` 類別實例的提取、儲存和更新。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-130">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="6b2d9-131">`MovieDBContext` 衍生自 Entity Framework 所提供的 `DbContext` 基類。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-131">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span> <span data-ttu-id="6b2d9-132">如需 `DbContext` 和 `DbSet`的詳細資訊，請參閱[Entity Framework 的生產力改進](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-132">For more information about `DbContext` and `DbSet`, see [Productivity Improvements for the Entity Framework](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).</span></span>

<span data-ttu-id="6b2d9-133">為了能夠參考 `DbContext` 和 `DbSet`，您必須在檔案頂端新增下列 `imports` 語句：</span><span class="sxs-lookup"><span data-stu-id="6b2d9-133">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `imports` statement at the top of the file:</span></span>

[!code-vb[Main](adding-a-model/samples/sample3.vb)]

<span data-ttu-id="6b2d9-134">完整的*Movie .vb*檔案如下所示。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-134">The complete *Movie.vb* file is shown below.</span></span>

[!code-vb[Main](adding-a-model/samples/sample4.vb)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a><span data-ttu-id="6b2d9-135">建立連接字串並使用 SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="6b2d9-135">Creating a Connection String and Working with SQL Server Compact</span></span>

<span data-ttu-id="6b2d9-136">您所建立的 `MovieDBContext` 類別會處理連接到資料庫的工作，並將 `Movie` 物件對應至資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-136">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="6b2d9-137">不過，您可能會問的一個問題，就是如何指定要連接的資料庫。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-137">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="6b2d9-138">您*會在應用程式的 web.config*檔案中加入連接資訊來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-138">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="6b2d9-139">開啟應用*程式根目錄的 web.config 檔案*。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-139">Open the application root *Web.config* file.</span></span> <span data-ttu-id="6b2d9-140">（不是*Views*資料夾中*的 web.config 檔案*）。下圖顯示*web.config*檔案;開啟以紅色圈出的*web.config*檔案。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-140">(Not the *Web.config* file in the *Views* folder.) The image below show both *Web.config* files; open the *Web.config* file circled in red.</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="6b2d9-141">將下列連接字串新增*至 web.config 檔案*中的 `<connectionStrings>` 元素。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-141">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="6b2d9-142">下列範例會顯示已新增連接字串的*web.config*檔案的一部分：</span><span class="sxs-lookup"><span data-stu-id="6b2d9-142">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

<span data-ttu-id="6b2d9-143">這小段的程式碼和 XML 就是您需要撰寫的所有專案，以便在資料庫中呈現及儲存電影資料。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-143">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="6b2d9-144">接下來，您將建立新的 `MoviesController` 類別，您可以用它來顯示電影資料，並允許使用者建立新的電影清單。</span><span class="sxs-lookup"><span data-stu-id="6b2d9-144">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6b2d9-145">[上一頁](adding-a-view.md)
> [下一頁](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="6b2d9-145">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
