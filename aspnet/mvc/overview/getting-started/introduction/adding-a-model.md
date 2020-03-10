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
# <a name="adding-a-model"></a><span data-ttu-id="a7fab-102">新增模型</span><span class="sxs-lookup"><span data-stu-id="a7fab-102">Adding a Model</span></span>

<span data-ttu-id="a7fab-103">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="a7fab-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [Tutorial Note](index.md)]

<span data-ttu-id="a7fab-104">在本節中，您將新增一些類別來管理資料庫中的電影。</span><span class="sxs-lookup"><span data-stu-id="a7fab-104">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="a7fab-105">這些類別將會是 ASP.NET MVC 應用程式&quot; 部分的 &quot;模型。</span><span class="sxs-lookup"><span data-stu-id="a7fab-105">These classes will be the &quot;model&quot; part of the ASP.NET MVC app.</span></span>

<span data-ttu-id="a7fab-106">您將使用稱為[Entity Framework](https://docs.microsoft.com/ef/)的 .NET Framework 資料存取技術，來定義和使用這些模型類別。</span><span class="sxs-lookup"><span data-stu-id="a7fab-106">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://docs.microsoft.com/ef/) to define and work with these model classes.</span></span> <span data-ttu-id="a7fab-107">Entity Framework （通常稱為 EF）支援稱為*Code First*的開發範例。</span><span class="sxs-lookup"><span data-stu-id="a7fab-107">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="a7fab-108">Code First 可讓您藉由撰寫簡單的類別來建立模型物件。</span><span class="sxs-lookup"><span data-stu-id="a7fab-108">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="a7fab-109">（這些也稱為 POCO 類別，從 &quot;純舊 CLR 物件。&quot;）接著，您可以從類別中即時建立資料庫，以實現非常乾淨快速的開發工作流程。</span><span class="sxs-lookup"><span data-stu-id="a7fab-109">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span> <span data-ttu-id="a7fab-110">如果您需要先建立資料庫，您仍然可以遵循此教學課程，以瞭解 MVC 和 EF 應用程式的開發。</span><span class="sxs-lookup"><span data-stu-id="a7fab-110">If you are required to create the database first, you can still follow this tutorial to learn about MVC and EF app development.</span></span> <span data-ttu-id="a7fab-111">接著，您可以遵循 Tom Fizmakens [ASP.NET](xref:visual-studio/overview/2013/aspnet-scaffolding-overview)樣板教學課程，其中涵蓋資料庫的第一種方法。</span><span class="sxs-lookup"><span data-stu-id="a7fab-111">You can then follow Tom Fizmakens [ASP.NET Scaffolding](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) tutorial, which covers the database first approach.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="a7fab-112">新增模型類別</span><span class="sxs-lookup"><span data-stu-id="a7fab-112">Adding Model Classes</span></span>

<span data-ttu-id="a7fab-113">在**方案總管**中，以滑鼠右鍵按一下 [*模型*] 資料夾，選取 [**新增**]，然後選取 [**類別**]。</span><span class="sxs-lookup"><span data-stu-id="a7fab-113">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="a7fab-114">輸入 &quot;電影&quot;的*類別*名稱。</span><span class="sxs-lookup"><span data-stu-id="a7fab-114">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="a7fab-115">將下列五個屬性新增至 `Movie` 類別：</span><span class="sxs-lookup"><span data-stu-id="a7fab-115">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="a7fab-116">我們會使用 `Movie` 類別來代表資料庫中的電影。</span><span class="sxs-lookup"><span data-stu-id="a7fab-116">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="a7fab-117">`Movie` 物件的每個實例都會對應至資料庫資料表中的資料列，而 `Movie` 類別的每個屬性都會對應到資料表中的資料行。</span><span class="sxs-lookup"><span data-stu-id="a7fab-117">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="a7fab-118">注意：若要使用 System.object 和相關類別，您必須安裝[Entity Framework NuGet 套件](https://www.nuget.org/packages/EntityFramework/)。</span><span class="sxs-lookup"><span data-stu-id="a7fab-118">Note: In order to use System.Data.Entity, and the related class, you need to install the [Entity Framework NuGet Package](https://www.nuget.org/packages/EntityFramework/).</span></span> <span data-ttu-id="a7fab-119">依照連結取得進一步的指示。</span><span class="sxs-lookup"><span data-stu-id="a7fab-119">Follow the link for further instructions.</span></span>

<span data-ttu-id="a7fab-120">在相同的檔案中，新增下列 `MovieDBContext` 類別：</span><span class="sxs-lookup"><span data-stu-id="a7fab-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

<span data-ttu-id="a7fab-121">`MovieDBContext` 類別代表 Entity Framework 的電影資料庫內容，它會處理資料庫中的 `Movie` 類別實例的提取、儲存和更新。</span><span class="sxs-lookup"><span data-stu-id="a7fab-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="a7fab-122">`MovieDBContext` 衍生自 Entity Framework 所提供的 `DbContext` 基類。</span><span class="sxs-lookup"><span data-stu-id="a7fab-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="a7fab-123">為了能夠參考 `DbContext` 和 `DbSet`，您必須在檔案頂端新增下列 `using` 語句：</span><span class="sxs-lookup"><span data-stu-id="a7fab-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="a7fab-124">若要這麼做，您可以手動新增 using 語句，或將滑鼠停留在紅色曲線上，按一下 `Show potential fixes` 然後按一下 `using System.Data.Entity;`</span><span class="sxs-lookup"><span data-stu-id="a7fab-124">You can do this by manually adding the using statement, or you can hover over the red squiggly lines, click `Show potential fixes` and click `using System.Data.Entity;`</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="a7fab-125">注意：已移除數個未使用的 `using` 語句。</span><span class="sxs-lookup"><span data-stu-id="a7fab-125">Note: Several unused `using` statements have been removed.</span></span> <span data-ttu-id="a7fab-126">Visual Studio 會將未使用的相依性顯示為灰色。</span><span class="sxs-lookup"><span data-stu-id="a7fab-126">Visual Studio will show unused dependencies as gray.</span></span> <span data-ttu-id="a7fab-127">若要移除未使用的相依性，您可以將滑鼠停留在灰色相依性上，按一下 `Show potential fixes` 然後按一下 **移除未使用**</span><span class="sxs-lookup"><span data-stu-id="a7fab-127">You can remove unused dependencies by hovering over the gray dependencies, click `Show potential fixes` and click **Remove Unused Usings.**</span></span>

![](adding-a-model/_static/image3.png)

<span data-ttu-id="a7fab-128">我們終於加入了模型（MVC 中的 M）。</span><span class="sxs-lookup"><span data-stu-id="a7fab-128">We've finally added a model (the M in MVC).</span></span> <span data-ttu-id="a7fab-129">在下一節中，您將使用資料庫連接字串。</span><span class="sxs-lookup"><span data-stu-id="a7fab-129">In the next section you'll work with the database connection string.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a7fab-130">[上一頁](adding-a-view.md)
> [下一頁](creating-a-connection-string.md)</span><span class="sxs-lookup"><span data-stu-id="a7fab-130">[Previous](adding-a-view.md)
[Next](creating-a-connection-string.md)</span></span>
