---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-2
title: 新增模型和控制器 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 88908ff8-51a9-40eb-931c-a8139128b680
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-2
msc.type: authoredcontent
ms.openlocfilehash: 57dacda421968f341284d89c9a3ad80040c16e25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557537"
---
# <a name="add-models-and-controllers"></a><span data-ttu-id="79a5d-102">新增模型與控制器</span><span class="sxs-lookup"><span data-stu-id="79a5d-102">Add Models and Controllers</span></span>

<span data-ttu-id="79a5d-103">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="79a5d-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="79a5d-104">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="79a5d-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="79a5d-105">在本節中，您將加入定義資料庫實體的模型類別。</span><span class="sxs-lookup"><span data-stu-id="79a5d-105">In this section, you will add model classes that define the database entities.</span></span> <span data-ttu-id="79a5d-106">接著，您將新增 Web API 控制器，在這些實體上執行 CRUD 作業。</span><span class="sxs-lookup"><span data-stu-id="79a5d-106">Then you will add Web API controllers that perform CRUD operations on those entities.</span></span>

## <a name="add-model-classes"></a><span data-ttu-id="79a5d-107">新增模型類別</span><span class="sxs-lookup"><span data-stu-id="79a5d-107">Add Model Classes</span></span>

<span data-ttu-id="79a5d-108">在本教學課程中，我們將使用「Code First」方法來建立資料庫，以 Entity Framework （EF）。</span><span class="sxs-lookup"><span data-stu-id="79a5d-108">In this tutorial, we'll create the database by using the "Code First" approach to Entity Framework (EF).</span></span> <span data-ttu-id="79a5d-109">使用 Code First，您可以C#撰寫對應至資料庫資料表的類別，而 EF 會建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="79a5d-109">With Code First, you write C# classes that correspond to database tables, and EF creates the database.</span></span> <span data-ttu-id="79a5d-110">（如需詳細資訊，請參閱[Entity Framework 開發方法](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf)）。</span><span class="sxs-lookup"><span data-stu-id="79a5d-110">(For more information, see [Entity Framework Development Approaches](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf).)</span></span>

<span data-ttu-id="79a5d-111">我們一開始會將領域物件定義為 Poco （純舊的 CLR 物件）。</span><span class="sxs-lookup"><span data-stu-id="79a5d-111">We start by defining our domain objects as POCOs (plain-old CLR objects).</span></span> <span data-ttu-id="79a5d-112">我們將建立下列 Poco：</span><span class="sxs-lookup"><span data-stu-id="79a5d-112">We will create the following POCOs:</span></span>

- <span data-ttu-id="79a5d-113">作者</span><span class="sxs-lookup"><span data-stu-id="79a5d-113">Author</span></span>
- <span data-ttu-id="79a5d-114">書籍</span><span class="sxs-lookup"><span data-stu-id="79a5d-114">Book</span></span>

<span data-ttu-id="79a5d-115">在方案總管中，以滑鼠右鍵按一下 [模型] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="79a5d-115">In Solution Explorer, right click the Models folder.</span></span> <span data-ttu-id="79a5d-116">選取 [**新增**]，然後選取 [**類別**]。</span><span class="sxs-lookup"><span data-stu-id="79a5d-116">Select **Add**, then select **Class**.</span></span> <span data-ttu-id="79a5d-117">將類別命名為 `Author`。</span><span class="sxs-lookup"><span data-stu-id="79a5d-117">Name the class `Author`.</span></span>

![](part-2/_static/image1.png)

<span data-ttu-id="79a5d-118">以下列程式碼取代 Author.cs 中的所有重複使用程式碼。</span><span class="sxs-lookup"><span data-stu-id="79a5d-118">Replace all of the boilerplate code in Author.cs with the following code.</span></span>

[!code-csharp[Main](part-2/samples/sample1.cs)]

<span data-ttu-id="79a5d-119">使用下列程式碼，新增名為 `Book`的另一個類別。</span><span class="sxs-lookup"><span data-stu-id="79a5d-119">Add another class named `Book`, with the following code.</span></span>

[!code-csharp[Main](part-2/samples/sample2.cs)]

<span data-ttu-id="79a5d-120">Entity Framework 將會使用這些模型來建立資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="79a5d-120">Entity Framework will use these models to create database tables.</span></span> <span data-ttu-id="79a5d-121">針對每個模型，`Id` 屬性會成為資料庫資料表的主鍵資料行。</span><span class="sxs-lookup"><span data-stu-id="79a5d-121">For each model, the `Id` property will become the primary key column of the database table.</span></span>

<span data-ttu-id="79a5d-122">在 Book 類別中，`AuthorId` 會在 `Author` 資料表中定義外鍵。</span><span class="sxs-lookup"><span data-stu-id="79a5d-122">In the Book class, the `AuthorId` defines a foreign key into the `Author` table.</span></span> <span data-ttu-id="79a5d-123">（為了簡單起見，我假設每一本書都有一位作者）。Book 類別也包含相關 `Author`的導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="79a5d-123">(For simplicity, I'm assuming that each book has a single author.) The book class also contains a navigation property to the related `Author`.</span></span> <span data-ttu-id="79a5d-124">您可以使用導覽屬性來存取程式碼中的相關 `Author`。</span><span class="sxs-lookup"><span data-stu-id="79a5d-124">You can use the navigation property to access the related `Author` in code.</span></span> <span data-ttu-id="79a5d-125">我更進一步瞭解第4部分中的導覽屬性，[處理實體](part-4.md)關聯。</span><span class="sxs-lookup"><span data-stu-id="79a5d-125">I say more about navigation properties in part 4, [Handling Entity Relations](part-4.md).</span></span>

## <a name="add-web-api-controllers"></a><span data-ttu-id="79a5d-126">新增 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="79a5d-126">Add Web API Controllers</span></span>

<span data-ttu-id="79a5d-127">在本節中，我們將新增支援 CRUD 作業（建立、讀取、更新和刪除）的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="79a5d-127">In this section, we'll add Web API controllers that support CRUD operations (create, read, update, and delete).</span></span> <span data-ttu-id="79a5d-128">控制器會使用 Entity Framework 來與資料庫層通訊。</span><span class="sxs-lookup"><span data-stu-id="79a5d-128">The controllers will use Entity Framework to communicate with the database layer.</span></span>

<span data-ttu-id="79a5d-129">首先，您可以刪除檔控制器/ValuesController。</span><span class="sxs-lookup"><span data-stu-id="79a5d-129">First, you can delete the file Controllers/ValuesController.cs.</span></span> <span data-ttu-id="79a5d-130">此檔案包含範例 Web API 控制器，但在本教學課程中，您不需要用到它。</span><span class="sxs-lookup"><span data-stu-id="79a5d-130">This file contains an example Web API controller, but you don't need it for this tutorial.</span></span>

![](part-2/_static/image2.png)

<span data-ttu-id="79a5d-131">接下來，建立專案。</span><span class="sxs-lookup"><span data-stu-id="79a5d-131">Next, build the project.</span></span> <span data-ttu-id="79a5d-132">Web API 樣板會使用反映來尋找模型類別，因此需要已編譯的元件。</span><span class="sxs-lookup"><span data-stu-id="79a5d-132">The Web API scaffolding uses reflection to find the model classes, so it needs the compiled assembly.</span></span>

<span data-ttu-id="79a5d-133">在方案總管中，以滑鼠右鍵按一下 [控制器] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="79a5d-133">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="79a5d-134">選取 [**新增**]，然後選取 [**控制器**]。</span><span class="sxs-lookup"><span data-stu-id="79a5d-134">Select **Add**, then select **Controller**.</span></span>

![](part-2/_static/image3.png)

<span data-ttu-id="79a5d-135">在 [**新增 Scaffold** ] 對話方塊中，選取 [具有動作的 Web API 2 控制器，使用 Entity Framework]。</span><span class="sxs-lookup"><span data-stu-id="79a5d-135">In the **Add Scaffold** dialog, select "Web API 2 Controller with actions, using Entity Framework".</span></span> <span data-ttu-id="79a5d-136">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="79a5d-136">Click **Add**.</span></span>

![](part-2/_static/image4.png)

<span data-ttu-id="79a5d-137">在 [**新增控制器**] 對話方塊中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="79a5d-137">In the **Add Controller** dialog, do the following:</span></span>

1. <span data-ttu-id="79a5d-138">在 [**模型類別**] 下拉式清單中，選取 [`Author`] 類別。</span><span class="sxs-lookup"><span data-stu-id="79a5d-138">In the **Model class** dropdown, select the `Author` class.</span></span> <span data-ttu-id="79a5d-139">（如果您沒有看到它列在下拉式清單中，請確定您已建立專案）。</span><span class="sxs-lookup"><span data-stu-id="79a5d-139">(If you don't see it listed in the dropdown, make sure that you built the project.)</span></span>
2. <span data-ttu-id="79a5d-140">勾選 [使用非同步控制器動作]。</span><span class="sxs-lookup"><span data-stu-id="79a5d-140">Check "Use async controller actions".</span></span>
3. <span data-ttu-id="79a5d-141">將控制器名稱保留 &quot;AuthorsController&quot;。</span><span class="sxs-lookup"><span data-stu-id="79a5d-141">Leave the controller name as &quot;AuthorsController&quot;.</span></span>
4. <span data-ttu-id="79a5d-142">按一下 [**資料內容類別**] 旁邊的加號（+）按鈕。</span><span class="sxs-lookup"><span data-stu-id="79a5d-142">Click plus (+) button next to **Data Context Class**.</span></span>

![](part-2/_static/image5.png)

<span data-ttu-id="79a5d-143">在 [**新增資料內容**] 對話方塊中，保留預設名稱，然後按一下 [**加入**]。</span><span class="sxs-lookup"><span data-stu-id="79a5d-143">In the **New Data Context** dialog, leave the default name and click **Add**.</span></span>

![](part-2/_static/image6.png)

<span data-ttu-id="79a5d-144">按一下 [**新增**] 以完成 [**新增控制器**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="79a5d-144">Click **Add** to complete the **Add Controller** dialog.</span></span> <span data-ttu-id="79a5d-145">對話方塊會將兩個類別新增至您的專案：</span><span class="sxs-lookup"><span data-stu-id="79a5d-145">The dialog adds two classes to your project:</span></span>

- <span data-ttu-id="79a5d-146">`AuthorsController` 定義 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="79a5d-146">`AuthorsController` defines a Web API controller.</span></span> <span data-ttu-id="79a5d-147">控制器會執行用戶端用來在作者清單上執行 CRUD 作業的 REST API。</span><span class="sxs-lookup"><span data-stu-id="79a5d-147">The controller implements the REST API that clients use to perform CRUD operations on the list of authors.</span></span>
- <span data-ttu-id="79a5d-148">`BookServiceContext` 在運行時間管理實體物件，其中包括以資料庫的資料填入物件、變更追蹤，以及將資料保存至資料庫。</span><span class="sxs-lookup"><span data-stu-id="79a5d-148">`BookServiceContext` manages entity objects during run time, which includes populating objects with data from a database, change tracking, and persisting data to the database.</span></span> <span data-ttu-id="79a5d-149">它繼承自 `DbContext`。</span><span class="sxs-lookup"><span data-stu-id="79a5d-149">It inherits from `DbContext`.</span></span>

![](part-2/_static/image7.png)

<span data-ttu-id="79a5d-150">此時，請重新建立專案。</span><span class="sxs-lookup"><span data-stu-id="79a5d-150">At this point, build the project again.</span></span> <span data-ttu-id="79a5d-151">現在，請執行相同的步驟，為 `Book` 實體新增 API 控制器。</span><span class="sxs-lookup"><span data-stu-id="79a5d-151">Now go through the same steps to add an API controller for `Book` entities.</span></span> <span data-ttu-id="79a5d-152">這次請選取模型類別的 [`Book`]，然後選取資料內容類別的現有 `BookServiceContext` 類別。</span><span class="sxs-lookup"><span data-stu-id="79a5d-152">This time, select `Book` for the model class, and select the existing `BookServiceContext` class for the data context class.</span></span> <span data-ttu-id="79a5d-153">（請勿建立新的資料內容）。按一下 [**新增**] 以新增控制器。</span><span class="sxs-lookup"><span data-stu-id="79a5d-153">(Don't create a new data context.) Click **Add** to add the controller.</span></span>

![](part-2/_static/image8.png)

> [!div class="step-by-step"]
> <span data-ttu-id="79a5d-154">[上一頁](part-1.md)
> [下一頁](part-3.md)</span><span class="sxs-lookup"><span data-stu-id="79a5d-154">[Previous](part-1.md)
[Next](part-3.md)</span></span>
