---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: 使用商務規則驗證建立模型 |Microsoft Docs
author: microsoft
description: 步驟3顯示如何建立可用於查詢和更新 NerdDinner 應用程式資料庫的模型。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: 6ebf1b71c089229ba9139ff7dc788b8978724046
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541661"
---
# <a name="build-a-model-with-business-rule-validations"></a><span data-ttu-id="33a2d-103">使用商務規則驗證建置模型</span><span class="sxs-lookup"><span data-stu-id="33a2d-103">Build a Model with Business Rule Validations</span></span>

<span data-ttu-id="33a2d-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="33a2d-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="33a2d-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="33a2d-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="33a2d-106">這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md)課程的步驟3，逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="33a2d-106">This is step 3 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="33a2d-107">步驟3顯示如何建立可用於查詢和更新 NerdDinner 應用程式資料庫的模型。</span><span class="sxs-lookup"><span data-stu-id="33a2d-107">Step 3 shows how to create a model that we can use to both query and update the database for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="33a2d-108">如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。</span><span class="sxs-lookup"><span data-stu-id="33a2d-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-3-building-the-model"></a><span data-ttu-id="33a2d-109">NerdDinner 步驟3：建立模型</span><span class="sxs-lookup"><span data-stu-id="33a2d-109">NerdDinner Step 3: Building the Model</span></span>

<span data-ttu-id="33a2d-110">在模型視圖控制器架構中，「模型」一詞指的是代表應用程式資料的物件，以及整合驗證和商務規則的對應領域邏輯。</span><span class="sxs-lookup"><span data-stu-id="33a2d-110">In a model-view-controller framework the term "model" refers to the objects that represent the data of the application, as well as the corresponding domain logic that integrates validation and business rules with it.</span></span> <span data-ttu-id="33a2d-111">此模型的方式很多，以 MVC 為基礎之應用程式的「核心」，我們將在稍後以根本上驅動它的行為。</span><span class="sxs-lookup"><span data-stu-id="33a2d-111">The model is in many ways the "heart" of an MVC-based application, and as we'll see later fundamentally drives the behavior of it.</span></span>

<span data-ttu-id="33a2d-112">ASP.NET MVC 架構支援使用任何資料存取技術，而開發人員可以從各種豐富的 .NET 資料選項中進行選擇，以執行其模型，包括： LINQ to Entities、LINQ to SQL、NHibernate、LLBLGen Pro、SubSonic、WilsonORM，或只是原始 ADO。NET Datareader 或資料集。</span><span class="sxs-lookup"><span data-stu-id="33a2d-112">The ASP.NET MVC framework supports using any data access technology, and developers can choose from a variety of rich .NET data options to implement their models including: LINQ to Entities, LINQ to SQL, NHibernate, LLBLGen Pro, SubSonic, WilsonORM, or just raw ADO.NET DataReaders or DataSets.</span></span>

<span data-ttu-id="33a2d-113">針對我們的 NerdDinner 應用程式，我們將使用 LINQ to SQL 來建立簡單的模型，使其相當於我們的資料庫設計，並加入一些自訂驗證邏輯和商務規則。</span><span class="sxs-lookup"><span data-stu-id="33a2d-113">For our NerdDinner application we are going to use LINQ to SQL to create a simple model that corresponds fairly closely to our database design, and adds some custom validation logic and business rules.</span></span> <span data-ttu-id="33a2d-114">接著，我們將會執行存放庫類別，協助從應用程式的其餘部分來抽象化資料持續性的執行，並讓我們輕鬆地對其進行單元測試。</span><span class="sxs-lookup"><span data-stu-id="33a2d-114">We will then implement a repository class that helps abstract away the data persistence implementation from the rest of the application, and enables us to easily unit test it.</span></span>

### <a name="linq-to-sql"></a><span data-ttu-id="33a2d-115">LINQ to SQL</span><span class="sxs-lookup"><span data-stu-id="33a2d-115">LINQ to SQL</span></span>

<span data-ttu-id="33a2d-116">LINQ to SQL 是在 .NET 3.5 中隨附的 ORM （物件關聯式對應程式）。</span><span class="sxs-lookup"><span data-stu-id="33a2d-116">LINQ to SQL is an ORM (object relational mapper) that ships as part of .NET 3.5.</span></span>

<span data-ttu-id="33a2d-117">LINQ to SQL 提供簡單的方法，將資料庫資料表對應至我們可以撰寫程式碼的 .NET 類別。</span><span class="sxs-lookup"><span data-stu-id="33a2d-117">LINQ to SQL provides an easy way to map database tables to .NET classes we can code against.</span></span> <span data-ttu-id="33a2d-118">針對我們的 NerdDinner 應用程式，我們將使用它，將資料庫內的 Dinners 和 RSVP 資料表對應至晚餐和 RSVP 類別。</span><span class="sxs-lookup"><span data-stu-id="33a2d-118">For our NerdDinner application we'll use it to map the Dinners and RSVP tables within our database to Dinner and RSVP classes.</span></span> <span data-ttu-id="33a2d-119">Dinners 和 RSVP 資料表的資料行將會對應至晚餐和 RSVP 類別的屬性。</span><span class="sxs-lookup"><span data-stu-id="33a2d-119">The columns of the Dinners and RSVP tables will correspond to properties on the Dinner and RSVP classes.</span></span> <span data-ttu-id="33a2d-120">每個晚餐和 RSVP 物件將代表資料庫中 Dinners 或 RSVP 資料表內的個別資料列。</span><span class="sxs-lookup"><span data-stu-id="33a2d-120">Each Dinner and RSVP object will represent a separate row within the Dinners or RSVP tables in the database.</span></span>

<span data-ttu-id="33a2d-121">LINQ to SQL 可讓我們避免必須手動建立 SQL 語句，以使用資料庫資料來抓取和更新晚餐和 RSVP 物件。</span><span class="sxs-lookup"><span data-stu-id="33a2d-121">LINQ to SQL allows us to avoid having to manually construct SQL statements to retrieve and update Dinner and RSVP objects with database data.</span></span> <span data-ttu-id="33a2d-122">相反地，我們會定義晚餐和 RSVP 類別、它們如何對應到資料庫，以及它們之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="33a2d-122">Instead, we'll define the Dinner and RSVP classes, how they map to/from the database, and the relationships between them.</span></span> <span data-ttu-id="33a2d-123">然後 LINQ to SQL 會負責產生適當的 SQL 執行邏輯，以便在我們互動和使用時于執行時間使用。</span><span class="sxs-lookup"><span data-stu-id="33a2d-123">LINQ to SQL will then takes care of generating the appropriate SQL execution logic to use at runtime when we interact and use them.</span></span>

<span data-ttu-id="33a2d-124">我們可以使用 VB 和C#中的 LINQ 語言支援，撰寫表達查詢，從資料庫中取出晚餐和 RSVP 物件。</span><span class="sxs-lookup"><span data-stu-id="33a2d-124">We can use the LINQ language support within VB and C# to write expressive queries that retrieve Dinner and RSVP objects from the database.</span></span> <span data-ttu-id="33a2d-125">這會減少我們需要撰寫的資料程式碼數量，並可讓我們建立真正整潔的應用程式。</span><span class="sxs-lookup"><span data-stu-id="33a2d-125">This minimizes the amount of data code we need to write, and allows us to build really clean applications.</span></span>

### <a name="adding-linq-to-sql-classes-to-our-project"></a><span data-ttu-id="33a2d-126">將 LINQ to SQL 類別加入至專案</span><span class="sxs-lookup"><span data-stu-id="33a2d-126">Adding LINQ to SQL Classes to our project</span></span>

<span data-ttu-id="33a2d-127">首先，以滑鼠右鍵按一下專案中的 [模型] 資料夾，然後選取 [新增 **-&gt;新專案**] 功能表命令：</span><span class="sxs-lookup"><span data-stu-id="33a2d-127">We'll begin by right-clicking on the "Models" folder within our project, and select the **Add-&gt;New Item** menu command:</span></span>

![](build-a-model-with-business-rule-validations/_static/image1.png)

<span data-ttu-id="33a2d-128">這會顯示 [加入新專案] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="33a2d-128">This will bring up the "Add New Item" dialog.</span></span> <span data-ttu-id="33a2d-129">我們會依「資料」分類進行篩選，並選取其中的「LINQ to SQL 類別」範本：</span><span class="sxs-lookup"><span data-stu-id="33a2d-129">We'll filter by the "Data" category and select the "LINQ to SQL Classes" template within it:</span></span>

![](build-a-model-with-business-rule-validations/_static/image2.png)

<span data-ttu-id="33a2d-130">我們會將專案命名為 "NerdDinner"，然後按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="33a2d-130">We'll name the item "NerdDinner" and click the "Add" button.</span></span> <span data-ttu-id="33a2d-131">Visual Studio 會在 \Models 目錄下新增 NerdDinner，然後開啟 [LINQ to SQL 物件關聯式設計工具]：</span><span class="sxs-lookup"><span data-stu-id="33a2d-131">Visual Studio will add a NerdDinner.dbml file under our \Models directory, and then open the LINQ to SQL object relational designer:</span></span>

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a><span data-ttu-id="33a2d-132">使用 LINQ to SQL 建立資料模型類別</span><span class="sxs-lookup"><span data-stu-id="33a2d-132">Creating Data Model Classes with LINQ to SQL</span></span>

<span data-ttu-id="33a2d-133">LINQ to SQL 可以讓我們從現有的資料庫架構快速建立資料模型類別。</span><span class="sxs-lookup"><span data-stu-id="33a2d-133">LINQ to SQL enables us to quickly create data model classes from existing database schema.</span></span> <span data-ttu-id="33a2d-134">為此，我們會在伺服器總管中開啟 NerdDinner 資料庫，並選取我們想要在其中建立模型的資料表：</span><span class="sxs-lookup"><span data-stu-id="33a2d-134">To-do this we'll open the NerdDinner database in the Server Explorer, and select the Tables we want to model in it:</span></span>

![](build-a-model-with-business-rule-validations/_static/image4.png)

<span data-ttu-id="33a2d-135">然後，我們可以將資料表拖曳到 LINQ to SQL 設計工具介面上。</span><span class="sxs-lookup"><span data-stu-id="33a2d-135">We can then drag the tables onto the LINQ to SQL designer surface.</span></span> <span data-ttu-id="33a2d-136">當我們這麼做時 LINQ to SQL 會使用資料表的架構（具有對應至資料庫資料表資料行的類別屬性），自動建立晚餐和 RSVP 類別：</span><span class="sxs-lookup"><span data-stu-id="33a2d-136">When we do this LINQ to SQL will automatically create Dinner and RSVP classes using the schema of the tables (with class properties that map to the database table columns):</span></span>

![](build-a-model-with-business-rule-validations/_static/image5.png)

<span data-ttu-id="33a2d-137">根據預設，LINQ to SQL 設計工具會在根據資料庫架構建立類別時，自動「pluralizes」資料表和資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="33a2d-137">By default the LINQ to SQL designer automatically "pluralizes" table and column names when it creates classes based on a database schema.</span></span> <span data-ttu-id="33a2d-138">例如：上述範例中的 "Dinners" 資料表會產生「晚餐」類別。</span><span class="sxs-lookup"><span data-stu-id="33a2d-138">For example: the "Dinners" table in our example above resulted in a "Dinner" class.</span></span> <span data-ttu-id="33a2d-139">此類別命名可協助讓我們的模型與 .NET 命名慣例保持一致，而且通常會發現設計工具的修正很方便（尤其是在加入許多資料表時）。</span><span class="sxs-lookup"><span data-stu-id="33a2d-139">This class naming helps make our models consistent with .NET naming conventions, and I usually find that having the designer fix this up convenient (especially when adding lots of tables).</span></span> <span data-ttu-id="33a2d-140">不過，如果您不喜歡設計工具所產生之類別或屬性的名稱，您可以一律覆寫它，並將它變更為您想要的任何名稱。</span><span class="sxs-lookup"><span data-stu-id="33a2d-140">If you don't like the name of a class or property that the designer generates, though, you can always override it and change it to any name you want.</span></span> <span data-ttu-id="33a2d-141">若要這麼做，您可以在設計工具內以內嵌方式編輯實體/屬性名稱，或透過屬性方格加以修改。</span><span class="sxs-lookup"><span data-stu-id="33a2d-141">You can do this either by editing the entity/property name in-line within the designer or by modifying it via the property grid.</span></span>

<span data-ttu-id="33a2d-142">根據預設，LINQ to SQL 設計工具也會檢查資料表的主鍵/外鍵關聯性，而且根據它們會在其建立的不同模型類別之間自動建立預設的「關聯性關聯」。</span><span class="sxs-lookup"><span data-stu-id="33a2d-142">By default the LINQ to SQL designer also inspects the primary key/foreign key relationships of the tables, and based on them automatically creates default "relationship associations" between the different model classes it creates.</span></span> <span data-ttu-id="33a2d-143">例如，當我們將 [Dinners] 和 [RSVP] 資料表拖曳至 LINQ to SQL 設計工具時，這兩個之間的一對多關聯性關聯是根據 RSVP 資料表具有 Dinners 資料表的外鍵的事實所推斷（這是由設計工具）：</span><span class="sxs-lookup"><span data-stu-id="33a2d-143">For example, when we dragged the Dinners and RSVP tables onto the LINQ to SQL designer a one-to-many relationship association between the two was inferred based on the fact that the RSVP table had a foreign-key to the Dinners table (this is indicated by the arrow in the designer):</span></span>

![](build-a-model-with-business-rule-validations/_static/image6.png)

<span data-ttu-id="33a2d-144">上述關聯會導致 LINQ to SQL 將強型別「晚餐」屬性新增至 RSVP 類別，讓開發人員用來存取與指定之 RSVP 相關聯的晚餐。</span><span class="sxs-lookup"><span data-stu-id="33a2d-144">The above association will cause LINQ to SQL to add a strongly typed "Dinner" property to the RSVP class that developers can use to access the Dinner associated with a given RSVP.</span></span> <span data-ttu-id="33a2d-145">它也會導致晚餐類別具有 "RSVPs" 集合屬性，讓開發人員能夠抓取和更新與特定晚餐相關聯的 RSVP 物件。</span><span class="sxs-lookup"><span data-stu-id="33a2d-145">It will also cause the Dinner class to have a "RSVPs" collection property that enables developers to retrieve and update RSVP objects associated with a particular Dinner.</span></span>

<span data-ttu-id="33a2d-146">當我們建立新的 RSVP 物件，並將它新增至晚餐的 RSVPs 集合時，您可以在下方查看 Visual Studio 內的 intellisense 範例。</span><span class="sxs-lookup"><span data-stu-id="33a2d-146">Below you can see an example of intellisense within Visual Studio when we create a new RSVP object and add it to a Dinner's RSVPs collection.</span></span> <span data-ttu-id="33a2d-147">請注意，LINQ to SQL 如何在晚餐物件上自動新增 "RSVPs" 集合：</span><span class="sxs-lookup"><span data-stu-id="33a2d-147">Notice how LINQ to SQL automatically added a "RSVPs" collection on the Dinner object:</span></span>

![](build-a-model-with-business-rule-validations/_static/image7.png)

<span data-ttu-id="33a2d-148">藉由將「RSVP」物件新增至晚餐的 RSVPs 集合，我們會告訴 LINQ to SQL 在資料庫中建立晚餐和「RSVP」資料列之間的外鍵關聯性：</span><span class="sxs-lookup"><span data-stu-id="33a2d-148">By adding the RSVP object to the Dinner's RSVPs collection we are telling LINQ to SQL to associate a foreign-key relationship between the Dinner and the RSVP row in our database:</span></span>

![](build-a-model-with-business-rule-validations/_static/image8.png)

<span data-ttu-id="33a2d-149">如果您不喜歡設計工具模型化或命名為數據表關聯的方式，您可以覆寫它。</span><span class="sxs-lookup"><span data-stu-id="33a2d-149">If you don't like how the designer has modeled or named a table association, you can override it.</span></span> <span data-ttu-id="33a2d-150">只要在設計工具中按一下 [關聯] 箭號，然後透過屬性方格存取其屬性，即可重新命名、刪除或修改它。</span><span class="sxs-lookup"><span data-stu-id="33a2d-150">Just click on the association arrow within the designer and access its properties via the property grid to rename, delete or modify it.</span></span> <span data-ttu-id="33a2d-151">不過，針對我們的 NerdDinner 應用程式，預設關聯規則適用于我們所建立的資料模型類別，而我們只會使用預設行為。</span><span class="sxs-lookup"><span data-stu-id="33a2d-151">For our NerdDinner application, though, the default association rules work well for the data model classes we are building and we can just use the default behavior.</span></span>

### <a name="nerddinnerdatacontext-class"></a><span data-ttu-id="33a2d-152">NerdDinnerDataCoNtext 類別</span><span class="sxs-lookup"><span data-stu-id="33a2d-152">NerdDinnerDataContext Class</span></span>

<span data-ttu-id="33a2d-153">Visual Studio 會自動建立 .NET 類別，以代表使用 LINQ to SQL 設計工具所定義的模型和資料庫關聯性。</span><span class="sxs-lookup"><span data-stu-id="33a2d-153">Visual Studio will automatically create .NET classes that represent the models and database relationships defined using the LINQ to SQL designer.</span></span> <span data-ttu-id="33a2d-154">針對加入至方案中的每個 LINQ to SQL 設計工具檔案，也會產生 LINQ to SQL DataCoNtext 類別。</span><span class="sxs-lookup"><span data-stu-id="33a2d-154">A LINQ to SQL DataContext class is also generated for each LINQ to SQL designer file added to the solution.</span></span> <span data-ttu-id="33a2d-155">因為我們將 LINQ to SQL 類別專案命名為 "NerdDinner"，所以所建立的 DataCoNtext 類別將稱為 "NerdDinnerDataCoNtext"。</span><span class="sxs-lookup"><span data-stu-id="33a2d-155">Because we named our LINQ to SQL class item "NerdDinner", the DataContext class created will be called "NerdDinnerDataContext".</span></span> <span data-ttu-id="33a2d-156">這個 NerdDinnerDataCoNtext 類別是我們將與資料庫互動的主要方式。</span><span class="sxs-lookup"><span data-stu-id="33a2d-156">This NerdDinnerDataContext class is the primary way we will interact with the database.</span></span>

<span data-ttu-id="33a2d-157">我們的 NerdDinnerDataCoNtext 類別會公開兩個屬性： "Dinners" 和 "RSVPs"，代表我們在資料庫中建立模型的兩個數據表。</span><span class="sxs-lookup"><span data-stu-id="33a2d-157">Our NerdDinnerDataContext class exposes two properties - "Dinners" and "RSVPs" - that represent the two tables we modeled within the database.</span></span> <span data-ttu-id="33a2d-158">我們可以使用C# ，針對這些屬性撰寫 LINQ 查詢，從資料庫查詢和取出晚餐和 RSVP 物件。</span><span class="sxs-lookup"><span data-stu-id="33a2d-158">We can use C# to write LINQ queries against those properties to query and retrieve Dinner and RSVP objects from the database.</span></span>

<span data-ttu-id="33a2d-159">下列程式碼示範如何具現化 NerdDinnerDataCoNtext 物件，並對其執行 LINQ 查詢，以取得未來發生的 Dinners 序列。</span><span class="sxs-lookup"><span data-stu-id="33a2d-159">The following code demonstrates how to instantiate a NerdDinnerDataContext object and perform a LINQ query against it to obtain a sequence of Dinners that occur in the future.</span></span> <span data-ttu-id="33a2d-160">Visual Studio 在撰寫 LINQ 查詢時提供完整的 intellisense，而從它傳回的物件則是強型別，也支援 intellisense：</span><span class="sxs-lookup"><span data-stu-id="33a2d-160">Visual Studio provides full intellisense when writing the LINQ query, and the objects returned from it are strongly-typed and also support intellisense:</span></span>

![](build-a-model-with-business-rule-validations/_static/image9.png)

<span data-ttu-id="33a2d-161">除了可讓我們查詢晚餐和 RSVP 物件之外，NerdDinnerDataCoNtext 也會自動追蹤我們後續對我們透過它取得的晚餐和 RSVP 物件所做的任何變更。</span><span class="sxs-lookup"><span data-stu-id="33a2d-161">In addition to allowing us to query for Dinner and RSVP objects, a NerdDinnerDataContext also automatically tracks any changes we subsequently make to the Dinner and RSVP objects we retrieve through it.</span></span> <span data-ttu-id="33a2d-162">我們可以使用這種功能，輕鬆地將變更儲存回資料庫，而不需要撰寫任何明確的 SQL 更新程式碼。</span><span class="sxs-lookup"><span data-stu-id="33a2d-162">We can use this functionality to easily save the changes back to the database - without having to write any explicit SQL update code.</span></span>

<span data-ttu-id="33a2d-163">例如，下列程式碼示範如何使用 LINQ 查詢來抓取資料庫中的單一晚餐物件、更新兩個晚餐屬性，然後將變更儲存回資料庫：</span><span class="sxs-lookup"><span data-stu-id="33a2d-163">For example, the code below demonstrates how to use a LINQ query to retrieve a single Dinner object from the database, update two of the Dinner properties, and then save the changes back to the database:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

<span data-ttu-id="33a2d-164">上述程式碼中的 NerdDinnerDataCoNtext 物件會自動追蹤我們從中取得的晚餐物件所做的屬性變更。</span><span class="sxs-lookup"><span data-stu-id="33a2d-164">The NerdDinnerDataContext object in the code above automatically tracked the property changes made to the Dinner object we retrieved from it.</span></span> <span data-ttu-id="33a2d-165">當我們呼叫 "SubmitChanges （）" 方法時，它會對資料庫執行適當的 SQL "UPDATE" 語句，以保存更新後的值。</span><span class="sxs-lookup"><span data-stu-id="33a2d-165">When we called the "SubmitChanges()" method, it will execute an appropriate SQL "UPDATE" statement to the database to persist the updated values back.</span></span>

### <a name="creating-a-dinnerrepository-class"></a><span data-ttu-id="33a2d-166">建立 DinnerRepository 類別</span><span class="sxs-lookup"><span data-stu-id="33a2d-166">Creating a DinnerRepository Class</span></span>

<span data-ttu-id="33a2d-167">針對小型應用程式，有時可以讓控制器直接針對 LINQ to SQL DataCoNtext 類別進行處理，並在控制器內內嵌 LINQ 查詢。</span><span class="sxs-lookup"><span data-stu-id="33a2d-167">For small applications it is sometimes fine to have Controllers work directly against a LINQ to SQL DataContext class, and embed LINQ queries within the Controllers.</span></span> <span data-ttu-id="33a2d-168">不過隨著應用程式變得更大，這種方法會變得很麻煩，而無法進行維護和測試。</span><span class="sxs-lookup"><span data-stu-id="33a2d-168">As applications get larger, though, this approach becomes cumbersome to maintain and test.</span></span> <span data-ttu-id="33a2d-169">它也會導致我們將相同的 LINQ 查詢複製到多個位置。</span><span class="sxs-lookup"><span data-stu-id="33a2d-169">It can also lead to us duplicating the same LINQ queries in multiple places.</span></span>

<span data-ttu-id="33a2d-170">可以讓應用程式更容易維護和測試的方法之一，就是使用「存放庫」模式。</span><span class="sxs-lookup"><span data-stu-id="33a2d-170">One approach that can make applications easier to maintain and test is to use a "repository" pattern.</span></span> <span data-ttu-id="33a2d-171">儲存機制類別可協助封裝資料查詢和持續性邏輯，並抽象化應用程式中資料持續性的執行細節。</span><span class="sxs-lookup"><span data-stu-id="33a2d-171">A repository class helps encapsulate data querying and persistence logic, and abstracts away the implementation details of the data persistence from the application.</span></span> <span data-ttu-id="33a2d-172">除了讓應用程式程式碼更簡潔，使用儲存機制模式可讓您更輕鬆地在未來變更資料儲存區，而且它可以協助對應用程式進行單元測試，而不需要實際的資料庫。</span><span class="sxs-lookup"><span data-stu-id="33a2d-172">In addition to making application code cleaner, using a repository pattern can make it easier to change data storage implementations in the future, and it can help facilitate unit testing an application without requiring a real database.</span></span>

<span data-ttu-id="33a2d-173">針對我們的 NerdDinner 應用程式，我們將定義具有下列簽章的 DinnerRepository 類別：</span><span class="sxs-lookup"><span data-stu-id="33a2d-173">For our NerdDinner application we'll define a DinnerRepository class with the below signature:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

<span data-ttu-id="33a2d-174">*注意：在本章稍後，我們將從這個類別解壓縮 IDinnerRepository 介面，並在我們的控制器上啟用相依性插入。從開始，我們將開始簡單明瞭，只是直接使用 DinnerRepository 類別。*</span><span class="sxs-lookup"><span data-stu-id="33a2d-174">*Note: Later in this chapter we'll extract an IDinnerRepository interface from this class and enable dependency injection with it on our Controllers. To begin with, though, we are going to start simple and just work directly with the DinnerRepository class.*</span></span>

<span data-ttu-id="33a2d-175">若要執行這個類別，我們要以滑鼠右鍵按一下 [模型] 資料夾，然後選擇 [**加入-&gt;新專案**] 功能表命令。</span><span class="sxs-lookup"><span data-stu-id="33a2d-175">To implement this class we'll right-click on our "Models" folder and choose the **Add-&gt;New Item** menu command.</span></span> <span data-ttu-id="33a2d-176">在 [新增專案] 對話方塊中，我們將選取 "Class" 範本，並將檔案命名為 "DinnerRepository.cs"：</span><span class="sxs-lookup"><span data-stu-id="33a2d-176">Within the "Add New Item" dialog we'll select the "Class" template and name the file "DinnerRepository.cs":</span></span>

![](build-a-model-with-business-rule-validations/_static/image10.png)

<span data-ttu-id="33a2d-177">然後，我們可以使用下列程式碼來執行我們的 DinnerRepository 類別：</span><span class="sxs-lookup"><span data-stu-id="33a2d-177">We can then implement our DinnerRepository class using the code below:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a><span data-ttu-id="33a2d-178">使用 DinnerRepository 類別來抓取、更新、插入及刪除</span><span class="sxs-lookup"><span data-stu-id="33a2d-178">Retrieving, Updating, Inserting and Deleting using the DinnerRepository class</span></span>

<span data-ttu-id="33a2d-179">既然我們已經建立了 DinnerRepository 類別，接下來就讓我們來看幾個程式碼範例，示範我們可以用它來執行的一般工作：</span><span class="sxs-lookup"><span data-stu-id="33a2d-179">Now that we've created our DinnerRepository class, let's look at a few code examples that demonstrate common tasks we can do with it:</span></span>

#### <a name="querying-examples"></a><span data-ttu-id="33a2d-180">查詢範例</span><span class="sxs-lookup"><span data-stu-id="33a2d-180">Querying Examples</span></span>

<span data-ttu-id="33a2d-181">下列程式碼會使用 DinnerID 值來抓取單一晚餐：</span><span class="sxs-lookup"><span data-stu-id="33a2d-181">The code below retrieves a single Dinner using the DinnerID value:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

<span data-ttu-id="33a2d-182">下列程式碼會抓取所有即將推出的 dinners 和迴圈：</span><span class="sxs-lookup"><span data-stu-id="33a2d-182">The code below retrieves all upcoming dinners and loops over them:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a><span data-ttu-id="33a2d-183">插入和更新範例</span><span class="sxs-lookup"><span data-stu-id="33a2d-183">Insert and Update Examples</span></span>

<span data-ttu-id="33a2d-184">下列程式碼示範如何新增兩個新的 dinners。</span><span class="sxs-lookup"><span data-stu-id="33a2d-184">The code below demonstrates adding two new dinners.</span></span> <span data-ttu-id="33a2d-185">儲存機制的新增/修改不會認可到資料庫，直到在其上呼叫 "Save （）" 方法為止。</span><span class="sxs-lookup"><span data-stu-id="33a2d-185">Additions/modifications to the repository aren't committed to the database until the "Save()" method is called on it.</span></span> <span data-ttu-id="33a2d-186">LINQ to SQL 會自動包裝資料庫交易中的所有變更–因此，所有變更都會發生，或在存放庫儲存時都不會這麼做：</span><span class="sxs-lookup"><span data-stu-id="33a2d-186">LINQ to SQL automatically wraps all changes in a database transaction – so either all changes happen or none of them do when our repository saves:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

<span data-ttu-id="33a2d-187">下列程式碼會抓取現有的晚餐物件，並修改其上的兩個屬性。</span><span class="sxs-lookup"><span data-stu-id="33a2d-187">The code below retrieves an existing Dinner object, and modifies two properties on it.</span></span> <span data-ttu-id="33a2d-188">在我們的存放庫中呼叫 "Save （）" 方法時，會將變更認可回資料庫：</span><span class="sxs-lookup"><span data-stu-id="33a2d-188">The changes are committed back to the database when the "Save()" method is called on our repository:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

<span data-ttu-id="33a2d-189">下列程式碼會抓取晚餐，然後在其中加上一個 RSVP。</span><span class="sxs-lookup"><span data-stu-id="33a2d-189">The code below retrieves a dinner and then adds an RSVP to it.</span></span> <span data-ttu-id="33a2d-190">它會使用 LINQ to SQL 為我們建立的晚餐物件上的 RSVPs 集合來執行這項操作（因為資料庫中的兩個之間有主鍵/外鍵關聯性）。</span><span class="sxs-lookup"><span data-stu-id="33a2d-190">It does this using the RSVPs collection on the Dinner object that LINQ to SQL created for us (because there is a primary-key/foreign-key relationship between the two in the database).</span></span> <span data-ttu-id="33a2d-191">在存放庫上呼叫 "Save （）" 方法時，此變更會保存回資料庫，做為新的 RSVP 資料表資料列：</span><span class="sxs-lookup"><span data-stu-id="33a2d-191">This change is persisted back to the database as a new RSVP table row when the "Save()" method is called on the repository:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a><span data-ttu-id="33a2d-192">刪除範例</span><span class="sxs-lookup"><span data-stu-id="33a2d-192">Delete Example</span></span>

<span data-ttu-id="33a2d-193">下列程式碼會抓取現有的晚餐物件，然後將其標示為已刪除。</span><span class="sxs-lookup"><span data-stu-id="33a2d-193">The code below retrieves an existing Dinner object, and then marks it to be deleted.</span></span> <span data-ttu-id="33a2d-194">在存放庫上呼叫 "Save （）" 方法時，它會將刪除認可回資料庫：</span><span class="sxs-lookup"><span data-stu-id="33a2d-194">When the "Save()" method is called on the repository it will commit the delete back to the database:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a><span data-ttu-id="33a2d-195">整合驗證和商務規則邏輯與模型類別</span><span class="sxs-lookup"><span data-stu-id="33a2d-195">Integrating Validation and Business Rule Logic with Model Classes</span></span>

<span data-ttu-id="33a2d-196">整合驗證和商務規則邏輯是任何可搭配資料使用之應用程式的重要部分。</span><span class="sxs-lookup"><span data-stu-id="33a2d-196">Integrating validation and business rule logic is a key part of any application that works with data.</span></span>

#### <a name="schema-validation"></a><span data-ttu-id="33a2d-197">結構描述驗證</span><span class="sxs-lookup"><span data-stu-id="33a2d-197">Schema Validation</span></span>

<span data-ttu-id="33a2d-198">當模型類別是使用 LINQ to SQL 設計工具來定義時，資料模型類別中屬性（property）的資料類型會對應至資料庫資料表的資料類型。</span><span class="sxs-lookup"><span data-stu-id="33a2d-198">When model classes are defined using the LINQ to SQL designer, the datatypes of the properties in the data model classes correspond to the datatypes of the database table.</span></span> <span data-ttu-id="33a2d-199">例如：如果 Dinners 資料表中的 "EventDate" 資料行是 "datetime"，則 LINQ to SQL 所建立的資料模型類別會是 "DateTime" 類型（內建的 .NET 資料類型）。</span><span class="sxs-lookup"><span data-stu-id="33a2d-199">For example: if the "EventDate" column in the Dinners table is a "datetime", the data model class created by LINQ to SQL will be of type "DateTime" (which is a built-in .NET datatype).</span></span> <span data-ttu-id="33a2d-200">這表示如果您嘗試從程式碼指派整數或布林值給它，就會發生編譯錯誤，如果您嘗試在執行時間將不正確字串型別隱含轉換成它，就會自動引發錯誤。</span><span class="sxs-lookup"><span data-stu-id="33a2d-200">This means you will get compile errors if you attempt to assign an integer or boolean to it from code, and it will raise an error automatically if you attempt to implicitly convert a non-valid string type to it at runtime.</span></span>

<span data-ttu-id="33a2d-201">當您使用字串時，LINQ to SQL 也會自動為您處理已植入的 SQL 值，這可在使用時協助保護您免于遭受 SQL 插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="33a2d-201">LINQ to SQL will also automatically handles escaping SQL values for you when using strings - which helps protect you against SQL injection attacks when using it.</span></span>

#### <a name="validation-and-business-rule-logic"></a><span data-ttu-id="33a2d-202">驗證和商務規則邏輯</span><span class="sxs-lookup"><span data-stu-id="33a2d-202">Validation and Business Rule Logic</span></span>

<span data-ttu-id="33a2d-203">架構驗證非常適合做為第一個步驟，但很少會用到。</span><span class="sxs-lookup"><span data-stu-id="33a2d-203">Schema validation is useful as a first step, but is rarely sufficient.</span></span> <span data-ttu-id="33a2d-204">大部分的真實案例都需要能夠指定更豐富的驗證邏輯，以跨越多個屬性、執行程式碼，而且通常會知道模型的狀態（例如，它是在/updated/deleted 中建立，還是在網域特定的狀態（例如「封存」）內。</span><span class="sxs-lookup"><span data-stu-id="33a2d-204">Most real-world scenarios require the ability to specify richer validation logic that can span multiple properties, execute code, and often have awareness of a model's state (for example: is it being created /updated/deleted, or within a domain-specific state like "archived").</span></span> <span data-ttu-id="33a2d-205">您可以使用各種不同的模式和架構來定義和套用驗證規則至模型類別，而且有數個 .NET 架構的架構，可以用來協助進行這項工作。</span><span class="sxs-lookup"><span data-stu-id="33a2d-205">There are a variety of different patterns and frameworks that can be used to define and apply validation rules to model classes, and there are several .NET based frameworks out there that can be used to help with this.</span></span> <span data-ttu-id="33a2d-206">您幾乎可以在 ASP.NET MVC 應用程式中使用其中任何一個。</span><span class="sxs-lookup"><span data-stu-id="33a2d-206">You can use pretty much any of them within ASP.NET MVC applications.</span></span>

<span data-ttu-id="33a2d-207">基於我們的 NerdDinner 應用程式的目的，我們將使用相當簡單且直接向前的模式，在我們的晚餐模型物件上公開 IsValid 屬性和 GetRuleViolations （）方法。</span><span class="sxs-lookup"><span data-stu-id="33a2d-207">For the purposes of our NerdDinner application, we'll use a relatively simple and straight-forward pattern where we expose an IsValid property and a GetRuleViolations() method on our Dinner model object.</span></span> <span data-ttu-id="33a2d-208">[IsValid] 屬性會根據驗證和商務規則是否有效而傳回 true 或 false。</span><span class="sxs-lookup"><span data-stu-id="33a2d-208">The IsValid property will return true or false depending on whether the validation and business rules are all valid.</span></span> <span data-ttu-id="33a2d-209">GetRuleViolations （）方法會傳回任何規則錯誤的清單。</span><span class="sxs-lookup"><span data-stu-id="33a2d-209">The GetRuleViolations() method will return a list of any rule errors.</span></span>

<span data-ttu-id="33a2d-210">我們會在專案中加入「部分類別」，為晚餐模型實行 IsValid 和 GetRuleViolations （）。</span><span class="sxs-lookup"><span data-stu-id="33a2d-210">We'll implement IsValid and GetRuleViolations() for our Dinner model by adding a "partial class" to our project.</span></span> <span data-ttu-id="33a2d-211">部分類別可以用來將方法/屬性/事件新增至 VS 設計工具所維護的類別（例如，LINQ to SQL 設計工具所產生的晚餐類別），並協助避免使用我們的程式碼因為各家工具。</span><span class="sxs-lookup"><span data-stu-id="33a2d-211">Partial classes can be used to add methods/properties/events to classes maintained by a VS designer (like the Dinner class generated by the LINQ to SQL designer) and help avoid the tool from messing with our code.</span></span> <span data-ttu-id="33a2d-212">我們可以在 [\Models] 資料夾上按一下滑鼠右鍵，然後選取 [加入新專案] 功能表命令，將新的部分類別加入至專案中。</span><span class="sxs-lookup"><span data-stu-id="33a2d-212">We can add a new partial class to our project by right-clicking on the \Models folder, and then select the "Add New Item" menu command.</span></span> <span data-ttu-id="33a2d-213">然後，我們可以選擇 [新增專案] 對話方塊中的「類別」範本，並將其命名為 Dinner.cs。</span><span class="sxs-lookup"><span data-stu-id="33a2d-213">We can then choose the "Class" template within the "Add New Item" dialog and name it Dinner.cs.</span></span>

![](build-a-model-with-business-rule-validations/_static/image11.png)

<span data-ttu-id="33a2d-214">按一下 [新增] 按鈕會將 Dinner.cs 檔案加入至專案，並在 IDE 中開啟它。</span><span class="sxs-lookup"><span data-stu-id="33a2d-214">Clicking the "Add" button will add a Dinner.cs file to our project and open it within the IDE.</span></span> <span data-ttu-id="33a2d-215">然後，我們可以使用下列程式碼來執行基本的規則/驗證強制架構：</span><span class="sxs-lookup"><span data-stu-id="33a2d-215">We can then implement a basic rule/validation enforcement framework using the below code:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

<span data-ttu-id="33a2d-216">關於上述程式碼的一些注意事項：</span><span class="sxs-lookup"><span data-stu-id="33a2d-216">A few notes about the above code:</span></span>

- <span data-ttu-id="33a2d-217">晚餐類別前面會加上 "partial" 關鍵字，這表示包含在其中的程式碼將會與 LINQ to SQL 設計工具所產生/維護的類別結合，並編譯成單一類別。</span><span class="sxs-lookup"><span data-stu-id="33a2d-217">The Dinner class is prefaced with a "partial" keyword – which means the code contained within it will be combined with the class generated/maintained by the LINQ to SQL designer and compiled into a single class.</span></span>
- <span data-ttu-id="33a2d-218">RuleViolation 類別是我們將加入至專案的協助程式類別，可讓我們提供有關規則違規的更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="33a2d-218">The RuleViolation class is a helper class we'll add to the project that allows us to provide more details about a rule violation.</span></span>
- <span data-ttu-id="33a2d-219">GetRuleViolations （）方法會使我們的驗證和商務規則進行評估（我們將在稍後加以執行）。</span><span class="sxs-lookup"><span data-stu-id="33a2d-219">The Dinner.GetRuleViolations() method causes our validation and business rules to be evaluated (we'll implement them shortly).</span></span> <span data-ttu-id="33a2d-220">然後，它會傳回一系列的 RuleViolation 物件，以提供有關任何規則錯誤的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="33a2d-220">It then returns back a sequence of RuleViolation objects that provide more details about any rule errors.</span></span>
- <span data-ttu-id="33a2d-221">晚餐. IsValid 屬性提供便利的 helper 屬性，指出晚餐物件是否有任何作用中的 RuleViolations。</span><span class="sxs-lookup"><span data-stu-id="33a2d-221">The Dinner.IsValid property provides a convenient helper property that indicates whether the Dinner object has any active RuleViolations.</span></span> <span data-ttu-id="33a2d-222">開發人員可以隨時使用晚餐物件主動檢查它（而且不會引發例外狀況）。</span><span class="sxs-lookup"><span data-stu-id="33a2d-222">It can be proactively checked by a developer using the Dinner object at anytime (and does not raise an exception).</span></span>
- <span data-ttu-id="33a2d-223">OnValidate （）部分方法是 LINQ to SQL 提供的勾點，可讓我們在晚餐物件即將保存在資料庫中時收到通知。</span><span class="sxs-lookup"><span data-stu-id="33a2d-223">The Dinner.OnValidate() partial method is a hook that LINQ to SQL provides that allows us to be notified anytime the Dinner object is about to be persisted within the database.</span></span> <span data-ttu-id="33a2d-224">上述的 OnValidate （）執行可確保晚餐在儲存前不會 RuleViolations。</span><span class="sxs-lookup"><span data-stu-id="33a2d-224">Our OnValidate() implementation above ensures that the Dinner has no RuleViolations before it is saved.</span></span> <span data-ttu-id="33a2d-225">如果它處於無效狀態，會引發例外狀況，這會導致 LINQ to SQL 中止交易。</span><span class="sxs-lookup"><span data-stu-id="33a2d-225">If it is in an invalid state it raises an exception, which will cause LINQ to SQL to abort the transaction.</span></span>

<span data-ttu-id="33a2d-226">這種方法提供了簡單的架構，讓我們可以將驗證和商務規則整合到其中。</span><span class="sxs-lookup"><span data-stu-id="33a2d-226">This approach provides a simple framework that we can integrate validation and business rules into.</span></span> <span data-ttu-id="33a2d-227">現在，讓我們將下列規則新增至我們的 GetRuleViolations （）方法：</span><span class="sxs-lookup"><span data-stu-id="33a2d-227">For now let's add the below rules to our GetRuleViolations() method:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

<span data-ttu-id="33a2d-228">我們使用的「yield return」功能C#來傳回任何 RuleViolations 的序列。</span><span class="sxs-lookup"><span data-stu-id="33a2d-228">We are using the "yield return" feature of C# to return a sequence of any RuleViolations.</span></span> <span data-ttu-id="33a2d-229">前六個規則檢查，只是在晚餐上強制字串屬性不能是 null 或空白。</span><span class="sxs-lookup"><span data-stu-id="33a2d-229">The first six rule checks above simply enforce that string properties on our Dinner cannot be null or empty.</span></span> <span data-ttu-id="33a2d-230">最後一個規則比較有趣，而且會呼叫 PhoneValidator IsValidNumber （） helper 方法，我們可以將其新增至專案，以確認 ContactPhone 數位格式符合晚餐的國家/地區。</span><span class="sxs-lookup"><span data-stu-id="33a2d-230">The last rule is a little more interesting, and calls a PhoneValidator.IsValidNumber() helper method that we can add to our project to verify that the ContactPhone number format matches the Dinner's country.</span></span>

<span data-ttu-id="33a2d-231">我們可以使用。NET 的正則運算式支援，可實現這種電話驗證支援。</span><span class="sxs-lookup"><span data-stu-id="33a2d-231">We can use .NET's regular expression support to implement this phone validation support.</span></span> <span data-ttu-id="33a2d-232">以下是一個簡單的 PhoneValidator 實作為，我們可以新增至我們的專案，讓我們新增國家特定的 Regex 模式檢查：</span><span class="sxs-lookup"><span data-stu-id="33a2d-232">Below is a simple PhoneValidator implementation that we can add to our project that enables us to add country-specific Regex pattern checks:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a><span data-ttu-id="33a2d-233">處理驗證和商務邏輯違規</span><span class="sxs-lookup"><span data-stu-id="33a2d-233">Handling Validation and Business Logic Violations</span></span>

<span data-ttu-id="33a2d-234">既然我們已新增上述驗證和商務規則程式碼，每當我們嘗試建立或更新晚餐時，就會評估並強制執行我們的驗證邏輯規則。</span><span class="sxs-lookup"><span data-stu-id="33a2d-234">Now that we've added the above validation and business rule code, any time we try to create or update a Dinner, our validation logic rules will be evaluated and enforced.</span></span>

<span data-ttu-id="33a2d-235">開發人員可以撰寫如下的程式碼，以主動判斷晚餐物件是否有效，並抓取其中的所有違規清單，而不引發任何例外狀況：</span><span class="sxs-lookup"><span data-stu-id="33a2d-235">Developers can write code like below to proactively determine if a Dinner object is valid, and retrieve a list of all violations in it without raising any exceptions:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

<span data-ttu-id="33a2d-236">如果我們嘗試以不正確狀態儲存晚餐，當我們在 DinnerRepository 上呼叫 Save （）方法時，就會引發例外狀況。</span><span class="sxs-lookup"><span data-stu-id="33a2d-236">If we attempt to save a Dinner in an invalid state, an exception will be raised when we call the Save() method on the DinnerRepository.</span></span> <span data-ttu-id="33a2d-237">這是因為 LINQ to SQL 會在儲存晚餐的變更之前，自動呼叫 OnValidate （）部分方法，而且我們已將程式碼新增至 OnValidate （），以在晚餐中存在任何規則違規時引發例外狀況。</span><span class="sxs-lookup"><span data-stu-id="33a2d-237">This occurs because LINQ to SQL automatically calls our Dinner.OnValidate() partial method before it saves the Dinner's changes, and we added code to Dinner.OnValidate() to raise an exception if any rule violations exist in the Dinner.</span></span> <span data-ttu-id="33a2d-238">我們可以攔截這個例外狀況，並被動抓取要修正的違規清單：</span><span class="sxs-lookup"><span data-stu-id="33a2d-238">We can catch this exception and reactively retrieve a list of the violations to fix:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

<span data-ttu-id="33a2d-239">因為我們的驗證和商務規則是在模型層內執行，而不是在 UI 層內，所以會套用到應用程式內的所有案例並加以使用。</span><span class="sxs-lookup"><span data-stu-id="33a2d-239">Because our validation and business rules are implemented within our model layer, and not within the UI layer, they will be applied and used across all scenarios within our application.</span></span> <span data-ttu-id="33a2d-240">我們稍後可以變更或新增商務規則，並讓所有與晚餐物件搭配使用的程式碼都能接受它們。</span><span class="sxs-lookup"><span data-stu-id="33a2d-240">We can later change or add business rules and have all code that works with our Dinner objects honor them.</span></span>

<span data-ttu-id="33a2d-241">有彈性可以在一處變更商務規則，而不需要在整個應用程式和 UI 邏輯中進行這些變更，而是撰寫完善的應用程式，以及 MVC 架構有助於鼓勵的優點。</span><span class="sxs-lookup"><span data-stu-id="33a2d-241">Having the flexibility to change business rules in one place, without having these changes ripple throughout the application and UI logic, is a sign of a well-written application, and a benefit that an MVC framework helps encourage.</span></span>

### <a name="next-step"></a><span data-ttu-id="33a2d-242">後續步驟</span><span class="sxs-lookup"><span data-stu-id="33a2d-242">Next Step</span></span>

<span data-ttu-id="33a2d-243">我們現在有一個模型，可以用來查詢和更新我們的資料庫。</span><span class="sxs-lookup"><span data-stu-id="33a2d-243">We've now got a model that we can use to both query and update our database.</span></span>

<span data-ttu-id="33a2d-244">現在讓我們在專案中新增一些控制器和視圖，供我們用來建立其周圍的 HTML UI 體驗。</span><span class="sxs-lookup"><span data-stu-id="33a2d-244">Let's now add some controllers and views to the project that we can use to build an HTML UI experience around it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="33a2d-245">[上一頁](create-a-database.md)
> [下一頁](use-controllers-and-views-to-implement-a-listingdetails-ui.md)</span><span class="sxs-lookup"><span data-stu-id="33a2d-245">[Previous](create-a-database.md)
[Next](use-controllers-and-views-to-implement-a-listingdetails-ui.md)</span></span>
