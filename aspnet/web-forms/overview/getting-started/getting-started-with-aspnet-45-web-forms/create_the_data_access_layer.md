---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
title: 建立資料存取層 |Microsoft Docs
author: Erikre
description: 本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 為我們建立 ASP.NET Web Forms 應用程式的基本概念 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 0bbf7a6e-d7eb-4091-91e4-fff892777f32
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
msc.type: authoredcontent
ms.openlocfilehash: 0fcf050474a57be9ed53ec0783a6d6b7dde2bf4c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575756"
---
# <a name="create-the-data-access-layer"></a><span data-ttu-id="0bafd-103">建立資料存取層</span><span class="sxs-lookup"><span data-stu-id="0bafd-103">Create the Data Access Layer</span></span>

<span data-ttu-id="0bafd-104">依[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="0bafd-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="0bafd-105">[下載 Wingtip 玩具範例專案（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下載電子書（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="0bafd-105">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="0bafd-106">本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 建立 ASP.NET Web Forms 應用程式的基本概念。</span><span class="sxs-lookup"><span data-stu-id="0bafd-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="0bafd-107">本教學課程系列隨附有[ C#原始程式碼](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 專案。</span><span class="sxs-lookup"><span data-stu-id="0bafd-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>

<span data-ttu-id="0bafd-108">本教學課程說明如何使用 ASP.NET Web Forms 和 Entity Framework Code First，從資料庫建立、存取和審核資料。</span><span class="sxs-lookup"><span data-stu-id="0bafd-108">This tutorial describes how to create, access, and review data from a database using ASP.NET Web Forms and Entity Framework Code First.</span></span> <span data-ttu-id="0bafd-109">本教學課程是以上一個教學課程「建立專案」為基礎，屬於 Wingtip 玩具商店教學課程系列。</span><span class="sxs-lookup"><span data-stu-id="0bafd-109">This tutorial builds on the previous tutorial "Create the Project" and is part of the Wingtip Toy Store tutorial series.</span></span> <span data-ttu-id="0bafd-110">當您完成本教學課程時，您將會在專案的 [*模型*] 資料夾中，建立一組資料存取類別。</span><span class="sxs-lookup"><span data-stu-id="0bafd-110">When you've completed this tutorial, you will have built a group of data-access classes that are in the *Models* folder of the project.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="0bafd-111">您將瞭解的內容：</span><span class="sxs-lookup"><span data-stu-id="0bafd-111">What you'll learn:</span></span>

- <span data-ttu-id="0bafd-112">如何建立資料模型。</span><span class="sxs-lookup"><span data-stu-id="0bafd-112">How to create the data models.</span></span>
- <span data-ttu-id="0bafd-113">如何初始化和植入資料庫。</span><span class="sxs-lookup"><span data-stu-id="0bafd-113">How to initialize and seed the database.</span></span>
- <span data-ttu-id="0bafd-114">如何更新及設定應用程式以支援資料庫。</span><span class="sxs-lookup"><span data-stu-id="0bafd-114">How to update and configure the application to support the database.</span></span>

### <a name="these-are-the-features-introduced-in-the-tutorial"></a><span data-ttu-id="0bafd-115">這些是教學課程中引進的功能：</span><span class="sxs-lookup"><span data-stu-id="0bafd-115">These are the features introduced in the tutorial:</span></span>

- <span data-ttu-id="0bafd-116">Entity Framework Code First</span><span class="sxs-lookup"><span data-stu-id="0bafd-116">Entity Framework Code First</span></span>
- <span data-ttu-id="0bafd-117">LocalDB</span><span class="sxs-lookup"><span data-stu-id="0bafd-117">LocalDB</span></span>
- <span data-ttu-id="0bafd-118">資料註釋</span><span class="sxs-lookup"><span data-stu-id="0bafd-118">Data Annotations</span></span>

## <a name="creating-the-data-models"></a><span data-ttu-id="0bafd-119">建立資料模型</span><span class="sxs-lookup"><span data-stu-id="0bafd-119">Creating the Data Models</span></span>

<span data-ttu-id="0bafd-120">[Entity Framework](https://msdn.microsoft.com/data/aa937723)是物件關聯式對應（ORM）架構。</span><span class="sxs-lookup"><span data-stu-id="0bafd-120">[Entity Framework](https://msdn.microsoft.com/data/aa937723) is an object-relational mapping (ORM) framework.</span></span> <span data-ttu-id="0bafd-121">它可讓您以物件的形式使用關聯式資料，以排除通常需要撰寫的大部分資料存取程式碼。</span><span class="sxs-lookup"><span data-stu-id="0bafd-121">It lets you work with relational data as objects, eliminating most of the data-access code that you'd usually need to write.</span></span> <span data-ttu-id="0bafd-122">使用 Entity Framework，您可以使用[LINQ](https://msdn.microsoft.com/library/bb397926.aspx)發出查詢，然後將資料當作強型別物件來取得和操作。</span><span class="sxs-lookup"><span data-stu-id="0bafd-122">Using Entity Framework, you can issue queries using [LINQ](https://msdn.microsoft.com/library/bb397926.aspx), then retrieve and manipulate data as strongly typed objects.</span></span> <span data-ttu-id="0bafd-123">LINQ 提供查詢和更新資料的模式。</span><span class="sxs-lookup"><span data-stu-id="0bafd-123">LINQ provides patterns for querying and updating data.</span></span> <span data-ttu-id="0bafd-124">使用 Entity Framework 可讓您專注于建立應用程式的其餘部分，而不是專注于資料存取基本概念。</span><span class="sxs-lookup"><span data-stu-id="0bafd-124">Using Entity Framework allows you to focus on creating the rest of your application, rather than focusing on the data access fundamentals.</span></span> <span data-ttu-id="0bafd-125">稍後在本教學課程系列中，我們將示範如何使用資料來填入導覽和產品查詢。</span><span class="sxs-lookup"><span data-stu-id="0bafd-125">Later in this tutorial series, we'll show you how to use the data to populate navigation and product queries.</span></span>

<span data-ttu-id="0bafd-126">Entity Framework 支援稱為*Code First*的開發範例。</span><span class="sxs-lookup"><span data-stu-id="0bafd-126">Entity Framework supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="0bafd-127">Code First 可讓您使用類別來定義您的資料模型。</span><span class="sxs-lookup"><span data-stu-id="0bafd-127">Code First lets you define your data models using classes.</span></span> <span data-ttu-id="0bafd-128">類別是一種結構，可讓您將其他類型、方法和事件的變數群組在一起，以建立您自己的自訂類型。</span><span class="sxs-lookup"><span data-stu-id="0bafd-128">A class is a construct that enables you to create your own custom types by grouping together variables of other types, methods and events.</span></span> <span data-ttu-id="0bafd-129">您可以將類別對應至現有的資料庫，或使用它們來產生資料庫。</span><span class="sxs-lookup"><span data-stu-id="0bafd-129">You can map classes to an existing database or use them to generate a database.</span></span> <span data-ttu-id="0bafd-130">在本教學課程中，您將藉由撰寫資料模型類別來建立資料模型。</span><span class="sxs-lookup"><span data-stu-id="0bafd-130">In this tutorial, you'll create the data models by writing data model classes.</span></span> <span data-ttu-id="0bafd-131">然後，您可以讓 Entity Framework 從這些新的類別即時建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="0bafd-131">Then, you'll let Entity Framework create the database on the fly from these new classes.</span></span>

<span data-ttu-id="0bafd-132">首先，您會建立定義 Web form 應用程式之資料模型的實體類別。</span><span class="sxs-lookup"><span data-stu-id="0bafd-132">You will begin by creating the entity classes that define the data models for the Web Forms application.</span></span> <span data-ttu-id="0bafd-133">接著，您將建立一個內容類別來管理實體類別，並提供資料庫的資料存取權。</span><span class="sxs-lookup"><span data-stu-id="0bafd-133">Then you will create a context class that manages the entity classes and provides data access to the database.</span></span> <span data-ttu-id="0bafd-134">您也會建立將用來填入資料庫的初始化運算式類別。</span><span class="sxs-lookup"><span data-stu-id="0bafd-134">You will also create an initializer class that you will use to populate the database.</span></span>

### <a name="entity-framework-and-references"></a><span data-ttu-id="0bafd-135">Entity Framework 和參考</span><span class="sxs-lookup"><span data-stu-id="0bafd-135">Entity Framework and References</span></span>

<span data-ttu-id="0bafd-136">根據預設，當您使用**Web Forms**範本建立新的**ASP.NET Web 應用程式**時，會包含 Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="0bafd-136">By default, Entity Framework is included when you create a new **ASP.NET Web Application** using the **Web Forms** template.</span></span> <span data-ttu-id="0bafd-137">Entity Framework 可以安裝、卸載及更新為 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="0bafd-137">Entity Framework can be installed, uninstalled, and updated as a NuGet package.</span></span>

<span data-ttu-id="0bafd-138">此 NuGet 套件包含您專案內的下列**運行**時間元件：</span><span class="sxs-lookup"><span data-stu-id="0bafd-138">This NuGet package includes the following **runtime** assemblies within your project:</span></span>

- <span data-ttu-id="0bafd-139">EntityFramework-Entity Framework 使用的所有通用執行時間程式碼</span><span class="sxs-lookup"><span data-stu-id="0bafd-139">EntityFramework.dll – All the common runtime code used by Entity Framework</span></span>
- <span data-ttu-id="0bafd-140">EntityFramework-Entity Framework 的 Microsoft SQL Server 提供者</span><span class="sxs-lookup"><span data-stu-id="0bafd-140">EntityFramework.SqlServer.dll – The Microsoft SQL Server provider for Entity Framework</span></span>

### <a name="entity-classes"></a><span data-ttu-id="0bafd-141">實體類別</span><span class="sxs-lookup"><span data-stu-id="0bafd-141">Entity Classes</span></span>

<span data-ttu-id="0bafd-142">您建立用來定義資料架構的類別稱為「實體類別」（entity class）。</span><span class="sxs-lookup"><span data-stu-id="0bafd-142">The classes you create to define the schema of the data are called entity classes.</span></span> <span data-ttu-id="0bafd-143">如果您不熟悉資料庫設計，請將實體類別視為資料庫的資料表定義。</span><span class="sxs-lookup"><span data-stu-id="0bafd-143">If you're new to database design, think of the entity classes as table definitions of a database.</span></span> <span data-ttu-id="0bafd-144">類別中的每個屬性都會在資料庫的資料表中指定一個資料行。</span><span class="sxs-lookup"><span data-stu-id="0bafd-144">Each property in the class specifies a column in the table of the database.</span></span> <span data-ttu-id="0bafd-145">這些類別會在物件導向程式碼與資料庫的關聯式資料表結構之間，提供輕量的物件關聯式介面。</span><span class="sxs-lookup"><span data-stu-id="0bafd-145">These classes provide a lightweight, object-relational interface between object-oriented code and the relational table structure of the database.</span></span>

<span data-ttu-id="0bafd-146">在本教學課程中，您將從新增代表產品和類別架構的簡單實體類別開始。</span><span class="sxs-lookup"><span data-stu-id="0bafd-146">In this tutorial, you'll start out by adding simple entity classes representing the schemas for products and categories.</span></span> <span data-ttu-id="0bafd-147">Products 類別將包含每個產品的定義。</span><span class="sxs-lookup"><span data-stu-id="0bafd-147">The products class will contain definitions for each product.</span></span> <span data-ttu-id="0bafd-148">Product 類別的每個成員名稱將會是 `ProductID`、`ProductName`、`Description`、`ImagePath`、`UnitPrice`、`CategoryID`和 `Category`。</span><span class="sxs-lookup"><span data-stu-id="0bafd-148">The name of each of the members of the product class will be `ProductID`, `ProductName`, `Description`, `ImagePath`, `UnitPrice`, `CategoryID`, and `Category`.</span></span> <span data-ttu-id="0bafd-149">Category 類別將包含產品可屬於之每個類別的定義，例如汽車、船或平面。</span><span class="sxs-lookup"><span data-stu-id="0bafd-149">The category class will contain definitions for each category that a product can belong to, such as Car, Boat, or Plane.</span></span> <span data-ttu-id="0bafd-150">Category 類別的每個成員名稱將會是 `CategoryID`、`CategoryName`、`Description`和 `Products`。</span><span class="sxs-lookup"><span data-stu-id="0bafd-150">The name of each of the members of the category class will be `CategoryID`, `CategoryName`, `Description`, and `Products`.</span></span> <span data-ttu-id="0bafd-151">每個產品都屬於其中一個類別。</span><span class="sxs-lookup"><span data-stu-id="0bafd-151">Each product will belong to one of the categories.</span></span> <span data-ttu-id="0bafd-152">這些實體類別會加入至專案的 [現有*模型*] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="0bafd-152">These entity classes will be added to the project's existing *Models* folder.</span></span>

1. <span data-ttu-id="0bafd-153">在**方案總管**中，以滑鼠右鍵按一下 [*模型*] 資料夾，**然後選取 [** 新增 -&gt;**新專案**]。</span><span class="sxs-lookup"><span data-stu-id="0bafd-153">In **Solution Explorer**, right-click the *Models* folder and then select **Add** -&gt; **New Item**.</span></span> 

    ![建立資料存取層-新增專案功能表](create_the_data_access_layer/_static/image1.png)

   <span data-ttu-id="0bafd-155">隨即顯示 [ 新增項目] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0bafd-155">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="0bafd-156">在左側 [**已安裝**] 窗格中的 [**視覺效果C#**  ] 底下，選取 [程式**代碼**]。</span><span class="sxs-lookup"><span data-stu-id="0bafd-156">Under **Visual C#** from the **Installed** pane on the left, select **Code**.</span></span> 

    ![建立資料存取層-新增專案功能表](create_the_data_access_layer/_static/image2.png)
3. <span data-ttu-id="0bafd-158">從中間窗格選取 [**類別**]，並將此新類別命名為*Product.cs*。</span><span class="sxs-lookup"><span data-stu-id="0bafd-158">Select **Class** from the middle pane and name this new class *Product.cs*.</span></span>
4. <span data-ttu-id="0bafd-159">按一下 [加入]。</span><span class="sxs-lookup"><span data-stu-id="0bafd-159">Click **Add**.</span></span>  
   <span data-ttu-id="0bafd-160">新的類別檔案會顯示在編輯器中。</span><span class="sxs-lookup"><span data-stu-id="0bafd-160">The new class file is displayed in the editor.</span></span>
5. <span data-ttu-id="0bafd-161">將預設程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="0bafd-161">Replace the default code with the following code:</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample1.cs)]
6. <span data-ttu-id="0bafd-162">重複步驟1到4來建立另一個類別，不過，將新類別命名為*Category.cs* ，並將預設程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="0bafd-162">Create another class by repeating steps 1 through 4, however, name the new class *Category.cs* and replace the default code with the following code:</span></span>  

    [!code-csharp[Main](create_the_data_access_layer/samples/sample2.cs)]

<span data-ttu-id="0bafd-163">如先前所述，`Category` 類別代表應用程式設計用來銷售的產品類型（例如<a id="a"></a>&quot;Cars&quot;、&quot;Boats&quot;、&quot;Rockets&quot;等等），而 `Product` 類別則代表資料庫中的個別產品（玩具）。</span><span class="sxs-lookup"><span data-stu-id="0bafd-163">As previously mentioned, the `Category` class represents the type of product that the application is designed to sell (such as <a id="a"></a>&quot;Cars&quot;, &quot;Boats&quot;, &quot;Rockets&quot;, and so on), and the `Product` class represents the individual products (toys) in the database.</span></span> <span data-ttu-id="0bafd-164">`Product` 物件的每個實例都會對應到關係資料庫資料表中的一個資料列，而 Product 類別的每個屬性都會對應到關係資料庫資料表中的資料行。</span><span class="sxs-lookup"><span data-stu-id="0bafd-164">Each instance of a `Product` object will correspond to a row within a relational database table, and each property of the Product class will map to a column in the relational database table.</span></span> <span data-ttu-id="0bafd-165">稍後在本教學課程中，您將會檢查資料庫中包含的產品資料。</span><span class="sxs-lookup"><span data-stu-id="0bafd-165">Later in this tutorial, you'll review the product data contained in the database.</span></span>

### <a name="data-annotations"></a><span data-ttu-id="0bafd-166">資料註釋</span><span class="sxs-lookup"><span data-stu-id="0bafd-166">Data Annotations</span></span>

<span data-ttu-id="0bafd-167">您可能已經注意到，類別的某些成員有屬性指定成員的詳細資料，例如 `[ScaffoldColumn(false)]`。</span><span class="sxs-lookup"><span data-stu-id="0bafd-167">You may have noticed that certain members of the classes have attributes specifying details about the member, such as `[ScaffoldColumn(false)]`.</span></span> <span data-ttu-id="0bafd-168">這些是*資料批註*。</span><span class="sxs-lookup"><span data-stu-id="0bafd-168">These are *data annotations*.</span></span> <span data-ttu-id="0bafd-169">資料批註屬性可以描述如何驗證該成員的使用者輸入、指定其格式，以及指定在建立資料庫時模型化的方式。</span><span class="sxs-lookup"><span data-stu-id="0bafd-169">The data annotation attributes can describe how to validate user input for that member, to specify formatting for it, and to specify how it is modeled when the database is created.</span></span>

### <a name="context-class"></a><span data-ttu-id="0bafd-170">Context 類別</span><span class="sxs-lookup"><span data-stu-id="0bafd-170">Context Class</span></span>

<span data-ttu-id="0bafd-171">若要開始使用類別進行資料存取，您必須定義內容類別。</span><span class="sxs-lookup"><span data-stu-id="0bafd-171">To start using the classes for data access, you must define a context class.</span></span> <span data-ttu-id="0bafd-172">如先前所述，內容類別會管理實體類別（例如 `Product` 類別和 `Category` 類別），並提供資料庫的資料存取權。</span><span class="sxs-lookup"><span data-stu-id="0bafd-172">As mentioned previously, the context class manages the entity classes (such as the `Product` class and the `Category` class) and provides data access to the database.</span></span>

<span data-ttu-id="0bafd-173">此程式會將新C#的內容類別加入至 [*模型*] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="0bafd-173">This procedure adds a new C# context class to the *Models* folder.</span></span>

1. <span data-ttu-id="0bafd-174">以滑鼠右鍵按一下 [*模型*] 資料夾，**然後選取 [** 新增 -&gt;**新專案**]。</span><span class="sxs-lookup"><span data-stu-id="0bafd-174">Right-click the *Models* folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="0bafd-175">隨即顯示 [ 新增項目] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0bafd-175">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="0bafd-176">從中間窗格選取 [**類別**]，將其命名為*ProductCoNtext.cs* ，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="0bafd-176">Select **Class** from the middle pane, name it *ProductContext.cs* and click **Add**.</span></span>
3. <span data-ttu-id="0bafd-177">將包含在類別中的預設程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="0bafd-177">Replace the default code contained in the class with the following code:</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample3.cs)]

<span data-ttu-id="0bafd-178">這段程式碼會加入 `System.Data.Entity` 命名空間，讓您可以存取 Entity Framework 的所有核心功能，其中包括使用強型別物件來查詢、插入、更新和刪除資料的功能。</span><span class="sxs-lookup"><span data-stu-id="0bafd-178">This code adds the `System.Data.Entity` namespace so that you have access to all the core functionality of Entity Framework, which includes the capability to query, insert, update, and delete data by working with strongly typed objects.</span></span>

<span data-ttu-id="0bafd-179">`ProductContext` 類別代表 Entity Framework 的產品資料庫內容，它會處理資料庫中 `Product` 類別實例的提取、儲存和更新。</span><span class="sxs-lookup"><span data-stu-id="0bafd-179">The `ProductContext` class represents Entity Framework product database context, which handles fetching, storing, and updating `Product` class instances in the database.</span></span> <span data-ttu-id="0bafd-180">`ProductContext` 類別衍生自 Entity Framework 所提供的 `DbContext` 基類。</span><span class="sxs-lookup"><span data-stu-id="0bafd-180">The `ProductContext` class derives from the `DbContext` base class provided by Entity Framework.</span></span>

### <a name="initializer-class"></a><span data-ttu-id="0bafd-181">初始化運算式類別</span><span class="sxs-lookup"><span data-stu-id="0bafd-181">Initializer Class</span></span>

<span data-ttu-id="0bafd-182">您必須在第一次使用內容時，執行一些自訂邏輯來初始化資料庫。</span><span class="sxs-lookup"><span data-stu-id="0bafd-182">You will need to run some custom logic to initialize the database the first time the context is used.</span></span> <span data-ttu-id="0bafd-183">這可讓植入資料新增至資料庫，讓您可以立即顯示產品和類別。</span><span class="sxs-lookup"><span data-stu-id="0bafd-183">This will allow seed data to be added to the database so that you can immediately display products and categories.</span></span>

<span data-ttu-id="0bafd-184">此程式會將新C#的初始化運算式類別加入至 [*模型*] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="0bafd-184">This procedure adds a new C# initializer class to the *Models* folder.</span></span>

1. <span data-ttu-id="0bafd-185">在 [*模型*] 資料夾中建立另一個 `Class`，並將其命名為*ProductDatabaseInitializer.cs*。</span><span class="sxs-lookup"><span data-stu-id="0bafd-185">Create another `Class` in the *Models* folder and name it *ProductDatabaseInitializer.cs*.</span></span>
2. <span data-ttu-id="0bafd-186">將包含在類別中的預設程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="0bafd-186">Replace the default code contained in the class with the following code:</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample4.cs)]

<span data-ttu-id="0bafd-187">如您在上述程式碼中所見，當建立並初始化資料庫時，會覆寫並設定 `Seed` 屬性。</span><span class="sxs-lookup"><span data-stu-id="0bafd-187">As you can see from the above code, when the database is created and initialized, the `Seed` property is overridden and set.</span></span> <span data-ttu-id="0bafd-188">設定 [`Seed`] 屬性時，會使用類別和產品的值來填入資料庫。</span><span class="sxs-lookup"><span data-stu-id="0bafd-188">When the `Seed` property is set, the values from the categories and products are used to populate the database.</span></span> <span data-ttu-id="0bafd-189">如果您嘗試在建立資料庫之後修改上述程式碼來更新種子資料，當您執行 Web 應用程式時，將不會看到任何更新。</span><span class="sxs-lookup"><span data-stu-id="0bafd-189">If you attempt to update the seed data by modifying the above code after the database has been created, you won't see any updates when you run the Web application.</span></span> <span data-ttu-id="0bafd-190">原因是上述程式碼會使用 `DropCreateDatabaseIfModelChanges` 類別的執行來辨識模型（架構）在重設種子資料之前是否已經變更。</span><span class="sxs-lookup"><span data-stu-id="0bafd-190">The reason is the above code uses an implementation of the `DropCreateDatabaseIfModelChanges` class to recognize if the model (schema) has changed before resetting the seed data.</span></span> <span data-ttu-id="0bafd-191">如果 `Category` 和 `Product` 實體類別不會進行任何變更，則不會以種子資料重新初始化資料庫。</span><span class="sxs-lookup"><span data-stu-id="0bafd-191">If no changes are made to the `Category` and `Product` entity classes, the database will not be reinitialized with the seed data.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="0bafd-192">如果您想要在每次執行應用程式時重新建立資料庫，您可以使用 `DropCreateDatabaseAlways` 類別，而不是 `DropCreateDatabaseIfModelChanges` 類別。</span><span class="sxs-lookup"><span data-stu-id="0bafd-192">If you wanted the database to be recreated every time you ran the application, you could use the `DropCreateDatabaseAlways` class instead of the `DropCreateDatabaseIfModelChanges` class.</span></span> <span data-ttu-id="0bafd-193">不過，在此教學課程系列中，請使用 `DropCreateDatabaseIfModelChanges` 類別。</span><span class="sxs-lookup"><span data-stu-id="0bafd-193">However for this tutorial series, use the `DropCreateDatabaseIfModelChanges` class.</span></span>

<span data-ttu-id="0bafd-194">此時，在本教學課程中，您將會有一個 [*模型*] 資料夾，其中包含四個新類別和一個預設類別：</span><span class="sxs-lookup"><span data-stu-id="0bafd-194">At this point in this tutorial, you will have a *Models* folder with four new classes and one default class:</span></span>

![建立資料存取層-模型資料夾](create_the_data_access_layer/_static/image3.png)

### <a name="configuring-the-application-to-use-the-data-model"></a><span data-ttu-id="0bafd-196">設定應用程式以使用資料模型</span><span class="sxs-lookup"><span data-stu-id="0bafd-196">Configuring the Application to Use the Data Model</span></span>

<span data-ttu-id="0bafd-197">現在您已建立代表資料的類別，您必須將應用程式設定為使用類別。</span><span class="sxs-lookup"><span data-stu-id="0bafd-197">Now that you've created the classes that represent the data, you must configure the application to use the classes.</span></span> <span data-ttu-id="0bafd-198">在*global.asax*檔案中，您可以加入初始化模型的程式碼。</span><span class="sxs-lookup"><span data-stu-id="0bafd-198">In the *Global.asax* file, you add code that initializes the model.</span></span> <span data-ttu-id="0bafd-199">在 web.config*檔案*中，您可以新增資訊，告訴應用程式您將用來儲存新資料類別所表示之資料的資料庫。</span><span class="sxs-lookup"><span data-stu-id="0bafd-199">In the *Web.config* file you add information that tells the application what database you'll use to store the data that's represented by the new data classes.</span></span> <span data-ttu-id="0bafd-200">*Global.asax*檔案可以用來處理應用程式事件或方法。</span><span class="sxs-lookup"><span data-stu-id="0bafd-200">The *Global.asax* file can be used to handle application events or methods.</span></span> <span data-ttu-id="0bafd-201">Web.config*檔案*可讓您控制 ASP.NET Web 應用程式的設定。</span><span class="sxs-lookup"><span data-stu-id="0bafd-201">The *Web.config* file allows you to control the configuration of your ASP.NET web application.</span></span>

#### <a name="updating-the-globalasax-file"></a><span data-ttu-id="0bafd-202">更新 global.asax 檔案</span><span class="sxs-lookup"><span data-stu-id="0bafd-202">Updating the Global.asax file</span></span>

<span data-ttu-id="0bafd-203">若要在應用程式啟動時初始化資料模型，您將會更新*Global.asax.cs*檔中的 `Application_Start` 處理常式。</span><span class="sxs-lookup"><span data-stu-id="0bafd-203">To initialize the data models when the application starts, you will update the `Application_Start` handler in the *Global.asax.cs* file.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="0bafd-204">在方案總管中，您可以選取*global.asax*檔案或*Global.asax.cs*檔案，以編輯*Global.asax.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="0bafd-204">In Solution Explorer, you can select either the *Global.asax* file or the *Global.asax.cs* file to edit the *Global.asax.cs* file.</span></span>

1. <span data-ttu-id="0bafd-205">將下列以黃色反白顯示的程式碼新增至*Global.asax.cs*檔案中的 `Application_Start` 方法。</span><span class="sxs-lookup"><span data-stu-id="0bafd-205">Add the following code highlighted in yellow to the `Application_Start` method in the *Global.asax.cs* file.</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample5.cs?highlight=9-10,22-23)]

> [!NOTE] 
> 
> <span data-ttu-id="0bafd-206">在瀏覽器中觀看此教學課程系列時，您的瀏覽器必須支援 HTML5 來觀看以黃色醒目提示的程式碼。</span><span class="sxs-lookup"><span data-stu-id="0bafd-206">Your browser must support HTML5 to view the code highlighted in yellow when viewing this tutorial series in a browser.</span></span>

<span data-ttu-id="0bafd-207">如上述程式碼所示，當應用程式啟動時，應用程式會指定第一次存取資料時要執行的初始化運算式。</span><span class="sxs-lookup"><span data-stu-id="0bafd-207">As shown in the above code, when the application starts, the application specifies the initializer that will run during the first time the data is accessed.</span></span> <span data-ttu-id="0bafd-208">需要兩個額外的命名空間，才能存取 `Database` 物件和 `ProductDatabaseInitializer` 物件。</span><span class="sxs-lookup"><span data-stu-id="0bafd-208">The two additional namespaces are required to access the `Database` object and the `ProductDatabaseInitializer` object.</span></span>

 <span data-ttu-id="0bafd-209">修改 Web.config 檔案</span><span class="sxs-lookup"><span data-stu-id="0bafd-209">Modifying the Web.Config File</span></span> 

<span data-ttu-id="0bafd-210">雖然 Entity Framework Code First 會在資料庫填入種子資料時，于預設位置為您產生資料庫，但將您自己的連接資訊新增至您的應用程式，可讓您控制資料庫位置。</span><span class="sxs-lookup"><span data-stu-id="0bafd-210">Although Entity Framework Code First will generate a database for you in a default location when the database is populated with seed data, adding your own connection information to your application gives you control of the database location.</span></span> <span data-ttu-id="0bafd-211">您可以使用專案根目錄之應用*程式 web.config 檔案*中的連接字串，來指定這個資料庫連接。</span><span class="sxs-lookup"><span data-stu-id="0bafd-211">You specify this database connection using a connection string in the application's *Web.config* file at the root of the project.</span></span> <span data-ttu-id="0bafd-212">藉由加入新的連接字串，您可以將資料庫（*wingtiptoys*）的位置導向至應用程式的資料目錄（*應用程式\_資料*），而不是其預設位置。</span><span class="sxs-lookup"><span data-stu-id="0bafd-212">By adding a new connection string, you can direct the location of the database (*wingtiptoys.mdf*) to be built in the application's data directory (*App\_Data*), rather than its default location.</span></span> <span data-ttu-id="0bafd-213">進行這項變更可讓您在本教學課程稍後尋找及檢查資料庫檔案。</span><span class="sxs-lookup"><span data-stu-id="0bafd-213">Making this change will allow you to find and inspect the database file later in this tutorial.</span></span>

1. <span data-ttu-id="0bafd-214">在**方案總管**中，尋找並開啟*web.config 檔案*。</span><span class="sxs-lookup"><span data-stu-id="0bafd-214">In **Solution Explorer**, find and open the *Web.config* file.</span></span>
2. <span data-ttu-id="0bafd-215">將以黃色反白顯示的連接字串加入*web.config*檔案的 `<connectionStrings>` 區段，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0bafd-215">Add the connection string highlighted in yellow to the `<connectionStrings>` section of the *Web.config* file as follows:</span></span>  

    [!code-xml[Main](create_the_data_access_layer/samples/sample6.xml?highlight=4-7)]

<span data-ttu-id="0bafd-216">第一次執行應用程式時，它會在連接字串所指定的位置上建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="0bafd-216">When the application is run for the first time, it will build the database at the location specified by the connection string.</span></span> <span data-ttu-id="0bafd-217">但在執行應用程式之前，讓我們先建立它。</span><span class="sxs-lookup"><span data-stu-id="0bafd-217">But before running the application, let's build it first.</span></span>

## <a name="building-the-application"></a><span data-ttu-id="0bafd-218">建置應用程式</span><span class="sxs-lookup"><span data-stu-id="0bafd-218">Building the Application</span></span>

<span data-ttu-id="0bafd-219">若要確定您的 Web 應用程式的所有類別和變更都能正常執行，您應該建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="0bafd-219">To make sure that all the classes and changes to your Web application work, you should build the application.</span></span>

1. <span data-ttu-id="0bafd-220">從 [**調試**] 功能表中，選取 [**組建 WingtipToys**]。</span><span class="sxs-lookup"><span data-stu-id="0bafd-220">From the **Debug** menu, select **Build WingtipToys**.</span></span>  
 <span data-ttu-id="0bafd-221">[**輸出**] 視窗隨即顯示，如果一切順利，您就會看到 [*成功*] 訊息。</span><span class="sxs-lookup"><span data-stu-id="0bafd-221">The **Output** window is displayed, and if all went well, you see a *succeeded* message.</span></span>  

    ![建立資料存取層-輸出視窗](create_the_data_access_layer/_static/image4.png)

<span data-ttu-id="0bafd-223">如果您遇到錯誤，請重新檢查上述步驟。</span><span class="sxs-lookup"><span data-stu-id="0bafd-223">If you run into an error, re-check the above steps.</span></span> <span data-ttu-id="0bafd-224">[**輸出**] 視窗中的資訊會指出有問題的檔案，以及檔案中需要變更的位置。</span><span class="sxs-lookup"><span data-stu-id="0bafd-224">The information in the **Output** window will indicate which file has a problem and where in the file a change is required.</span></span> <span data-ttu-id="0bafd-225">這項資訊可讓您判斷在您的專案中，必須檢查和修正上述步驟的哪個部分。</span><span class="sxs-lookup"><span data-stu-id="0bafd-225">This information will enable you to determine what part of the above steps need to be reviewed and fixed in your project.</span></span>

## <a name="summary"></a><span data-ttu-id="0bafd-226">總結</span><span class="sxs-lookup"><span data-stu-id="0bafd-226">Summary</span></span>

<span data-ttu-id="0bafd-227">在此系列的本教學課程中，您已建立資料模型，以及新增將用來初始化和植入資料庫的程式碼。</span><span class="sxs-lookup"><span data-stu-id="0bafd-227">In this tutorial of the series you have created the data model, as well as, added the code that will be used to initialize and seed the database.</span></span> <span data-ttu-id="0bafd-228">您也已將應用程式設定為在應用程式執行時使用資料模型。</span><span class="sxs-lookup"><span data-stu-id="0bafd-228">You have also configured the application to use the data models when the application is run.</span></span>

<span data-ttu-id="0bafd-229">在下一個教學課程中，您將更新 UI、加入導覽，以及從資料庫中取出資料。</span><span class="sxs-lookup"><span data-stu-id="0bafd-229">In the next tutorial, you'll update the UI, add navigation, and retrieve data from the database.</span></span> <span data-ttu-id="0bafd-230">這會導致根據您在本教學課程中建立的實體類別自動建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="0bafd-230">This will result in the database being automatically created based on the entity classes that you created in this tutorial.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0bafd-231">其他資源</span><span class="sxs-lookup"><span data-stu-id="0bafd-231">Additional Resources</span></span>

<span data-ttu-id="0bafd-232">[Entity Framework 總覽](https://msdn.microsoft.com/library/bb399567.aspx) </span><span class="sxs-lookup"><span data-stu-id="0bafd-232">[Entity Framework Overview](https://msdn.microsoft.com/library/bb399567.aspx) </span></span>  
<span data-ttu-id="0bafd-233">[ADO.NET Entity Framework 的初學者指南](https://msdn.microsoft.com/data/ee712907) </span><span class="sxs-lookup"><span data-stu-id="0bafd-233">[Beginner's Guide to the ADO.NET Entity Framework](https://msdn.microsoft.com/data/ee712907) </span></span>  
<span data-ttu-id="0bafd-234">[使用 Entity Framework 進行 Code First 開發](http://www.msteched.com/2010/Europe/DEV212)（影片）</span><span class="sxs-lookup"><span data-stu-id="0bafd-234">[Code First Development with Entity Framework](http://www.msteched.com/2010/Europe/DEV212) (video)</span></span>   
<span data-ttu-id="0bafd-235">[Code First 關聯性流暢的 API](https://msdn.microsoft.com/data/hh134698) </span><span class="sxs-lookup"><span data-stu-id="0bafd-235">[Code First Relationships Fluent API](https://msdn.microsoft.com/data/hh134698) </span></span>  
[<span data-ttu-id="0bafd-236">Code First 資料批註</span><span class="sxs-lookup"><span data-stu-id="0bafd-236">Code First Data Annotations</span></span>](https://msdn.microsoft.com/data/gg193958)  
[<span data-ttu-id="0bafd-237">Entity Framework 的生產力改善</span><span class="sxs-lookup"><span data-stu-id="0bafd-237">Productivity Improvements for the Entity Framework</span></span>](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)

> [!div class="step-by-step"]
> <span data-ttu-id="0bafd-238">[上一頁](create-the-project.md)
> [下一頁](ui_and_navigation.md)</span><span class="sxs-lookup"><span data-stu-id="0bafd-238">[Previous](create-the-project.md)
[Next](ui_and_navigation.md)</span></span>
