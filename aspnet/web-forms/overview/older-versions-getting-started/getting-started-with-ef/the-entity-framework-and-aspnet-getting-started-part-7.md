---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
title: Entity Framework 4.0 Database First 和 ASP.NET 4 Web form 的消費者入門-第7部分 |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 來建立 ASP.NET Web Forms 應用程式。 範例應用程式為 。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: f8afb245-b705-419c-8790-0b295e90d5e2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
msc.type: authoredcontent
ms.openlocfilehash: 18d4b44c5e23fd6942c3adf48a33a5602e6df6d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78603429"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-7"></a><span data-ttu-id="939d9-104">Entity Framework 4.0 Database First 和 ASP.NET 4 Web form 的消費者入門-第7部分</span><span class="sxs-lookup"><span data-stu-id="939d9-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 7</span></span>

<span data-ttu-id="939d9-105">由[Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="939d9-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="939d9-106">Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 4.0 和 Visual Studio 2010 來建立 ASP.NET Web Forms 應用程式。</span><span class="sxs-lookup"><span data-stu-id="939d9-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="939d9-107">如需教學課程系列的資訊，請參閱本[系列的第一個教學](the-entity-framework-and-aspnet-getting-started-part-1.md)課程</span><span class="sxs-lookup"><span data-stu-id="939d9-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>

## <a name="using-stored-procedures"></a><span data-ttu-id="939d9-108">使用預存程序</span><span class="sxs-lookup"><span data-stu-id="939d9-108">Using Stored Procedures</span></span>

<span data-ttu-id="939d9-109">在上一個教學課程中，您已執行每個階層的資料表繼承模式。</span><span class="sxs-lookup"><span data-stu-id="939d9-109">In the previous tutorial you implemented a table-per-hierarchy inheritance pattern.</span></span> <span data-ttu-id="939d9-110">本教學課程將示範如何使用預存程式，對資料庫存取進行更多的控制。</span><span class="sxs-lookup"><span data-stu-id="939d9-110">This tutorial will show you how to use stored procedures to gain more control over database access.</span></span>

<span data-ttu-id="939d9-111">Entity Framework 可讓您指定它應該使用預存程式來存取資料庫。</span><span class="sxs-lookup"><span data-stu-id="939d9-111">The Entity Framework lets you specify that it should use stored procedures for database access.</span></span> <span data-ttu-id="939d9-112">針對任何實體類型，您可以指定用來建立、更新或刪除該類型實體的預存程式。</span><span class="sxs-lookup"><span data-stu-id="939d9-112">For any entity type, you can specify a stored procedure to use for creating, updating, or deleting entities of that type.</span></span> <span data-ttu-id="939d9-113">然後在資料模型中，您可以加入預存程式的參考，以便用來執行工作，例如，抓取實體集。</span><span class="sxs-lookup"><span data-stu-id="939d9-113">Then in the data model you can add references to stored procedures that you can use to perform tasks such as retrieving sets of entities.</span></span>

<span data-ttu-id="939d9-114">使用預存程式是資料庫存取的常見需求。</span><span class="sxs-lookup"><span data-stu-id="939d9-114">Using stored procedures is a common requirement for database access.</span></span> <span data-ttu-id="939d9-115">在某些情況下，資料庫管理員可能會要求所有的資料庫存取都必須經過預存程式，以確保安全性。</span><span class="sxs-lookup"><span data-stu-id="939d9-115">In some cases a database administrator may require that all database access go through stored procedures for security reasons.</span></span> <span data-ttu-id="939d9-116">在其他情況下，您可能會想要將商務邏輯建立到 Entity Framework 在更新資料庫時所使用的部分程式。</span><span class="sxs-lookup"><span data-stu-id="939d9-116">In other cases you may want to build business logic into some of the processes that the Entity Framework uses when it updates the database.</span></span> <span data-ttu-id="939d9-117">例如，每當刪除實體時，您可能會想要將它複製到封存資料庫。</span><span class="sxs-lookup"><span data-stu-id="939d9-117">For example, whenever an entity is deleted you might want to copy it to an archive database.</span></span> <span data-ttu-id="939d9-118">或者，每次更新資料列時，您可能會想要將資料列寫入記錄資料表中，以記錄進行變更的人員。</span><span class="sxs-lookup"><span data-stu-id="939d9-118">Or whenever a row is updated you might want to write a row to a logging table that records who made the change.</span></span> <span data-ttu-id="939d9-119">您可以在每次 Entity Framework 刪除實體或更新實體時所呼叫的預存程式中執行這類工作。</span><span class="sxs-lookup"><span data-stu-id="939d9-119">You can perform these kinds of tasks in a stored procedure that's called whenever the Entity Framework deletes an entity or updates an entity.</span></span>

<span data-ttu-id="939d9-120">如同在上一個教學課程中，您不會建立任何新的頁面。</span><span class="sxs-lookup"><span data-stu-id="939d9-120">As in the previous tutorial, you'll not create any new pages.</span></span> <span data-ttu-id="939d9-121">相反地，您會變更 Entity Framework 針對您已建立的某些頁面存取資料庫的方式。</span><span class="sxs-lookup"><span data-stu-id="939d9-121">Instead, you'll change the way the Entity Framework accesses the database for some of the pages you already created.</span></span>

<span data-ttu-id="939d9-122">在本教學課程中，您將在資料庫中建立預存程式，以插入 `Student` 和 `Instructor` 實體。</span><span class="sxs-lookup"><span data-stu-id="939d9-122">In this tutorial you'll create stored procedures in the database for inserting `Student` and `Instructor` entities.</span></span> <span data-ttu-id="939d9-123">您會將它們加入至資料模型，並指定 Entity Framework 應該使用它們來將 `Student` 和 `Instructor` 實體加入至資料庫。</span><span class="sxs-lookup"><span data-stu-id="939d9-123">You'll add them to the data model, and you'll specify that the Entity Framework should use them for adding `Student` and `Instructor` entities to the database.</span></span> <span data-ttu-id="939d9-124">您也會建立可用來抓取 `Course` 實體的預存程式。</span><span class="sxs-lookup"><span data-stu-id="939d9-124">You'll also create a stored procedure that you can use to retrieve `Course` entities.</span></span>

## <a name="creating-stored-procedures-in-the-database"></a><span data-ttu-id="939d9-125">在資料庫中建立預存程式</span><span class="sxs-lookup"><span data-stu-id="939d9-125">Creating Stored Procedures in the Database</span></span>

<span data-ttu-id="939d9-126">（如果您使用此教學課程可供下載之專案中的*School .mdf*檔案，則可以略過本節，因為預存程式已經存在）。</span><span class="sxs-lookup"><span data-stu-id="939d9-126">(If you're using the *School.mdf* file from the project available for download with this tutorial, you can skip this section because the stored procedures already exist.)</span></span>

<span data-ttu-id="939d9-127">在**伺服器總管**中，展開 [ *School*]，以滑鼠右鍵按一下 [**預存程式**]，然後選取 [**加入新的預存**程式]。</span><span class="sxs-lookup"><span data-stu-id="939d9-127">In **Server Explorer**, expand *School.mdf*, right-click **Stored Procedures**, and select **Add New Stored Procedure**.</span></span>

<span data-ttu-id="939d9-128">[![image15](the-entity-framework-and-aspnet-getting-started-part-7/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="939d9-128">[![image15](the-entity-framework-and-aspnet-getting-started-part-7/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image1.png)</span></span>

<span data-ttu-id="939d9-129">複製下列 SQL 語句，並將其貼入 [預存程式] 視窗中，並取代基本架構預存程式。</span><span class="sxs-lookup"><span data-stu-id="939d9-129">Copy the following SQL statements and paste them into the stored procedure window, replacing the skeleton stored procedure.</span></span>

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample1.sql)]

<span data-ttu-id="939d9-130">[![image14](the-entity-framework-and-aspnet-getting-started-part-7/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="939d9-130">[![image14](the-entity-framework-and-aspnet-getting-started-part-7/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image3.png)</span></span>

<span data-ttu-id="939d9-131">`Student` 實體具有四個屬性： `PersonID`、`LastName`、`FirstName`和 `EnrollmentDate`。</span><span class="sxs-lookup"><span data-stu-id="939d9-131">`Student` entities have four properties: `PersonID`, `LastName`, `FirstName`, and `EnrollmentDate`.</span></span> <span data-ttu-id="939d9-132">資料庫會自動產生識別碼值，而預存程式會接受其他三個參數。</span><span class="sxs-lookup"><span data-stu-id="939d9-132">The database generates the ID value automatically, and the stored procedure accepts parameters for the other three.</span></span> <span data-ttu-id="939d9-133">預存程式會傳回新資料列記錄索引鍵的值，讓 Entity Framework 可以追蹤它保留在記憶體中的實體版本。</span><span class="sxs-lookup"><span data-stu-id="939d9-133">The stored procedure returns the value of the new row's record key so that the Entity Framework can keep track of that in the version of the entity it keeps in memory.</span></span>

<span data-ttu-id="939d9-134">儲存並關閉 [預存程式] 視窗。</span><span class="sxs-lookup"><span data-stu-id="939d9-134">Save and close the stored procedure window.</span></span>

<span data-ttu-id="939d9-135">使用下列 SQL 語句，以相同的方式建立 `InsertInstructor` 預存程式：</span><span class="sxs-lookup"><span data-stu-id="939d9-135">Create an `InsertInstructor` stored procedure in the same manner, using the following SQL statements:</span></span>

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample2.sql)]

<span data-ttu-id="939d9-136">同時為 `Student` 和 `Instructor` 實體建立 `Update` 預存程式。</span><span class="sxs-lookup"><span data-stu-id="939d9-136">Create `Update` stored procedures for `Student` and `Instructor` entities also.</span></span> <span data-ttu-id="939d9-137">（資料庫已經有 `DeletePerson` 預存程式，可同時適用于 `Instructor` 和 `Student` 實體）。</span><span class="sxs-lookup"><span data-stu-id="939d9-137">(The database already has a `DeletePerson` stored procedure which will work for both `Instructor` and `Student` entities.)</span></span>

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample3.sql)]

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample4.sql)]

<span data-ttu-id="939d9-138">在本教學課程中，您將會對應每個實體類型的所有三個函式--insert、update 和 delete。</span><span class="sxs-lookup"><span data-stu-id="939d9-138">In this tutorial you'll map all three functions -- insert, update, and delete -- for each entity type.</span></span> <span data-ttu-id="939d9-139">Entity Framework 版本4可讓您只將其中一個或兩個函式對應至預存程式，而不需要對應其他函式，但有一個例外：如果您對應 update 函式，而不是 delete 函式，則 Entity Framework 會在您嘗試刪除實體。</span><span class="sxs-lookup"><span data-stu-id="939d9-139">The Entity Framework version 4 allows you to map just one or two of these functions to stored procedures without mapping the others, with one exception: if you map the update function but not the delete function, the Entity Framework will throw an exception when you attempt to delete an entity.</span></span> <span data-ttu-id="939d9-140">在 Entity Framework 版本3.5 中，您在對應預存程式中沒有這麼大的彈性：如果您對應了一個函式，則必須對應這三個函數。</span><span class="sxs-lookup"><span data-stu-id="939d9-140">In the Entity Framework version 3.5, you did not have this much flexibility in mapping stored procedures: if you mapped one function you were required to map all three.</span></span>

<span data-ttu-id="939d9-141">若要建立可讀取而不是更新資料的預存程式，請使用下列 SQL 語句建立一個選取所有 `Course` 實體的儲存程式：</span><span class="sxs-lookup"><span data-stu-id="939d9-141">To create a stored procedure that reads rather than updates data, create one that selects all `Course` entities, using the following SQL statements:</span></span>

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample5.sql)]

## <a name="adding-the-stored-procedures-to-the-data-model"></a><span data-ttu-id="939d9-142">將預存程式加入至資料模型</span><span class="sxs-lookup"><span data-stu-id="939d9-142">Adding the Stored Procedures to the Data Model</span></span>

<span data-ttu-id="939d9-143">預存程式現在已在資料庫中定義，但必須加入至資料模型，才能供 Entity Framework 使用。</span><span class="sxs-lookup"><span data-stu-id="939d9-143">The stored procedures are now defined in the database, but they must be added to the data model to make them available to the Entity Framework.</span></span> <span data-ttu-id="939d9-144">開啟*SchoolModel*，以滑鼠右鍵按一下設計介面，然後選取 [**從資料庫更新模型**]。</span><span class="sxs-lookup"><span data-stu-id="939d9-144">Open *SchoolModel.edmx*, right-click the design surface, and select **Update Model from Database**.</span></span> <span data-ttu-id="939d9-145">在 [**選擇您的資料庫物件**] 對話方塊的 [**加入**] 索引標籤中，展開 [**預存程式**]，選取新建立的預存程式和 `DeletePerson` 預存程式，然後按一下 **[完成**]。</span><span class="sxs-lookup"><span data-stu-id="939d9-145">In the **Add** tab of the **Choose Your Database Objects** dialog box, expand **Stored Procedures**, select the newly created stored procedures and the `DeletePerson` stored procedure, and then click **Finish**.</span></span>

<span data-ttu-id="939d9-146">[![image20](the-entity-framework-and-aspnet-getting-started-part-7/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="939d9-146">[![image20](the-entity-framework-and-aspnet-getting-started-part-7/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image5.png)</span></span>

## <a name="mapping-the-stored-procedures"></a><span data-ttu-id="939d9-147">對應預存程式</span><span class="sxs-lookup"><span data-stu-id="939d9-147">Mapping the Stored Procedures</span></span>

<span data-ttu-id="939d9-148">在 [資料模型設計師] 中，以滑鼠右鍵按一下 [`Student`] 實體，然後選取 [**預存程式對應**]。</span><span class="sxs-lookup"><span data-stu-id="939d9-148">In the data model designer, right-click the `Student` entity and select **Stored Procedure Mapping**.</span></span>

<span data-ttu-id="939d9-149">[![image21](the-entity-framework-and-aspnet-getting-started-part-7/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="939d9-149">[![image21](the-entity-framework-and-aspnet-getting-started-part-7/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image7.png)</span></span>

<span data-ttu-id="939d9-150">[**對應詳細資料**] 視窗隨即出現，您可以在其中指定 Entity Framework 應用來插入、更新和刪除此類型之實體的預存程式。</span><span class="sxs-lookup"><span data-stu-id="939d9-150">The **Mapping Details** window appears, in which you can specify stored procedures that the Entity Framework should use for inserting, updating, and deleting entities of this type.</span></span>

<span data-ttu-id="939d9-151">[![image22](the-entity-framework-and-aspnet-getting-started-part-7/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="939d9-151">[![image22](the-entity-framework-and-aspnet-getting-started-part-7/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image9.png)</span></span>

<span data-ttu-id="939d9-152">將**Insert**函數設定為**InsertStudent**。</span><span class="sxs-lookup"><span data-stu-id="939d9-152">Set the **Insert** function to **InsertStudent**.</span></span> <span data-ttu-id="939d9-153">此視窗會顯示預存程式參數的清單，每一個都必須對應至一個實體屬性。</span><span class="sxs-lookup"><span data-stu-id="939d9-153">The window shows a list of stored procedure parameters, each of which must be mapped to an entity property.</span></span> <span data-ttu-id="939d9-154">其中兩個會自動對應，因為名稱是相同的。</span><span class="sxs-lookup"><span data-stu-id="939d9-154">Two of these are mapped automatically because the names are the same.</span></span> <span data-ttu-id="939d9-155">沒有名為 `FirstName`的實體屬性，因此您必須手動從顯示可用實體屬性的下拉式清單中選取 [`FirstMidName`]。</span><span class="sxs-lookup"><span data-stu-id="939d9-155">There's no entity property named `FirstName`, so you must manually select `FirstMidName` from a drop-down list that shows available entity properties.</span></span> <span data-ttu-id="939d9-156">（這是因為您在第一個教學課程中，將 `FirstName` 屬性的名稱變更為 `FirstMidName`。）</span><span class="sxs-lookup"><span data-stu-id="939d9-156">(This is because you changed the name of the `FirstName` property to `FirstMidName` in the first tutorial.)</span></span>

<span data-ttu-id="939d9-157">[![image23](the-entity-framework-and-aspnet-getting-started-part-7/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="939d9-157">[![image23](the-entity-framework-and-aspnet-getting-started-part-7/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image11.png)</span></span>

<span data-ttu-id="939d9-158">在相同的 [**對應詳細資料**] 視窗中，將 `Update` 函式對應至 `UpdateStudent` 預存程式（請務必指定 `FirstMidName` 做為 `FirstName`的參數值，如同您在 `Insert` 預存程式中所做的）和 `Delete` 函數到 `DeletePerson` 預存程式。</span><span class="sxs-lookup"><span data-stu-id="939d9-158">In the same **Mapping Details** window, map the `Update` function to the `UpdateStudent` stored procedure (make sure you specify `FirstMidName` as the parameter value for `FirstName`, as you did for the `Insert` stored procedure) and the `Delete` function to the `DeletePerson` stored procedure.</span></span>

<span data-ttu-id="939d9-159">[![image01](the-entity-framework-and-aspnet-getting-started-part-7/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="939d9-159">[![image01](the-entity-framework-and-aspnet-getting-started-part-7/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image13.png)</span></span>

<span data-ttu-id="939d9-160">遵循相同的程式，將講師的插入、更新和刪除預存程式對應至 `Instructor` 實體。</span><span class="sxs-lookup"><span data-stu-id="939d9-160">Follow the same procedure to map the insert, update, and delete stored procedures for instructors to the `Instructor` entity.</span></span>

<span data-ttu-id="939d9-161">[![image02](the-entity-framework-and-aspnet-getting-started-part-7/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="939d9-161">[![image02](the-entity-framework-and-aspnet-getting-started-part-7/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image15.png)</span></span>

<span data-ttu-id="939d9-162">對於讀取而不是更新資料的預存程式，您可以使用 [**模型瀏覽器**] 視窗，將預存程式對應至它所傳回的實體類型。</span><span class="sxs-lookup"><span data-stu-id="939d9-162">For stored procedures that read rather than update data, you use the **Model Browser** window to map the stored procedure to the entity type it returns.</span></span> <span data-ttu-id="939d9-163">在 [資料模型設計師] 中，以滑鼠右鍵按一下設計介面，然後選取 [**模型瀏覽器**]。</span><span class="sxs-lookup"><span data-stu-id="939d9-163">In the data model designer, right-click the design surface and select **Model Browser**.</span></span> <span data-ttu-id="939d9-164">開啟 [ **SchoolModel** ] 節點，然後開啟 [**預存程式**] 節點。</span><span class="sxs-lookup"><span data-stu-id="939d9-164">Open the **SchoolModel.Store** node and then open the **Stored Procedures** node.</span></span> <span data-ttu-id="939d9-165">然後以滑鼠右鍵按一下 `GetCourses` 預存程式，然後選取 [**新增函數匯入**]。</span><span class="sxs-lookup"><span data-stu-id="939d9-165">Then right-click the `GetCourses` stored procedure and select **Add Function Import**.</span></span>

<span data-ttu-id="939d9-166">[![image24](the-entity-framework-and-aspnet-getting-started-part-7/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="939d9-166">[![image24](the-entity-framework-and-aspnet-getting-started-part-7/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image17.png)</span></span>

<span data-ttu-id="939d9-167">在 [**加入**函式匯入] 對話方塊中，于 [傳回選取**實體** **的集合**] 底下，選取 [`Course`] 做為傳回的實體類型。</span><span class="sxs-lookup"><span data-stu-id="939d9-167">In the **Add Function Import** dialog box, under **Returns a Collection Of** select **Entities**, and then select `Course` as the entity type returned.</span></span> <span data-ttu-id="939d9-168">完成後，按一下 [ **確定**]。</span><span class="sxs-lookup"><span data-stu-id="939d9-168">When you're done, click **OK**.</span></span> <span data-ttu-id="939d9-169">儲存並關閉 *.edmx*檔案。</span><span class="sxs-lookup"><span data-stu-id="939d9-169">Save and close the *.edmx* file.</span></span>

<span data-ttu-id="939d9-170">[![image25](the-entity-framework-and-aspnet-getting-started-part-7/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="939d9-170">[![image25](the-entity-framework-and-aspnet-getting-started-part-7/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image19.png)</span></span>

## <a name="using-insert-update-and-delete-stored-procedures"></a><span data-ttu-id="939d9-171">使用 Insert、Update 和 Delete 預存程式</span><span class="sxs-lookup"><span data-stu-id="939d9-171">Using Insert, Update, and Delete Stored Procedures</span></span>

<span data-ttu-id="939d9-172">插入、更新和刪除資料的預存程式會在您將其新增至資料模型並將它們對應至適當的實體之後，自動由 Entity Framework 使用。</span><span class="sxs-lookup"><span data-stu-id="939d9-172">Stored procedures to insert, update, and delete data are used by the Entity Framework automatically after you've added them to the data model and mapped them to the appropriate entities.</span></span> <span data-ttu-id="939d9-173">您現在可以執行*StudentsAdd* ，而且每次建立新的學生時，Entity Framework 都會使用 `InsertStudent` 預存程式，將新的資料列加入 `Student` 資料表。</span><span class="sxs-lookup"><span data-stu-id="939d9-173">You can now run the *StudentsAdd.aspx* page, and every time you create a new student, the Entity Framework will use the `InsertStudent` stored procedure to add the new row to the `Student` table.</span></span>

<span data-ttu-id="939d9-174">[![image03](the-entity-framework-and-aspnet-getting-started-part-7/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="939d9-174">[![image03](the-entity-framework-and-aspnet-getting-started-part-7/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image21.png)</span></span>

<span data-ttu-id="939d9-175">執行 [student *] 頁面，* 新的學生會出現在清單中。</span><span class="sxs-lookup"><span data-stu-id="939d9-175">Run the *Students.aspx* page and the new student appears in the list.</span></span>

<span data-ttu-id="939d9-176">[![image04](the-entity-framework-and-aspnet-getting-started-part-7/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="939d9-176">[![image04](the-entity-framework-and-aspnet-getting-started-part-7/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image23.png)</span></span>

<span data-ttu-id="939d9-177">變更名稱以確認更新函式可正常運作，然後刪除學生以確認 delete 函式可以運作。</span><span class="sxs-lookup"><span data-stu-id="939d9-177">Change the name to verify that the update function works, and then delete the student to verify that the delete function works.</span></span>

<span data-ttu-id="939d9-178">[![image05](the-entity-framework-and-aspnet-getting-started-part-7/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="939d9-178">[![image05](the-entity-framework-and-aspnet-getting-started-part-7/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image25.png)</span></span>

## <a name="using-select-stored-procedures"></a><span data-ttu-id="939d9-179">使用 Select 預存程式</span><span class="sxs-lookup"><span data-stu-id="939d9-179">Using Select Stored Procedures</span></span>

<span data-ttu-id="939d9-180">Entity Framework 不會自動執行 `GetCourses`的預存程式，而且您無法將它們與 `EntityDataSource` 控制項搭配使用。</span><span class="sxs-lookup"><span data-stu-id="939d9-180">The Entity Framework does not automatically run stored procedures such as `GetCourses`, and you cannot use them with the `EntityDataSource` control.</span></span> <span data-ttu-id="939d9-181">若要使用它們，您可以從程式碼呼叫它們。</span><span class="sxs-lookup"><span data-stu-id="939d9-181">To use them, you call them from code.</span></span>

<span data-ttu-id="939d9-182">開啟*InstructorsCourses.aspx.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="939d9-182">Open the *InstructorsCourses.aspx.cs* file.</span></span> <span data-ttu-id="939d9-183">`PopulateDropDownLists` 方法會使用 LINQ to entities 查詢來抓取所有課程實體，讓它可以在清單中執行迴圈，並判斷講師指派給哪一個或哪些未指派：</span><span class="sxs-lookup"><span data-stu-id="939d9-183">The `PopulateDropDownLists` method uses a LINQ-to-Entities query to retrieve all course entities so that it can loop through the list and determine which ones an instructor is assigned to and which ones are unassigned:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample6.cs)]

<span data-ttu-id="939d9-184">將此取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="939d9-184">Replace this with the following code:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample7.cs)]

<span data-ttu-id="939d9-185">此頁面現在會使用 `GetCourses` 預存程式來取出所有課程的清單。</span><span class="sxs-lookup"><span data-stu-id="939d9-185">The page now uses the `GetCourses` stored procedure to retrieve the list of all courses.</span></span> <span data-ttu-id="939d9-186">執行頁面，確認它的運作方式與之前相同。</span><span class="sxs-lookup"><span data-stu-id="939d9-186">Run the page to verify that it works as it did before.</span></span>

<span data-ttu-id="939d9-187">（根據 `ObjectContext` 預設設定，預存程式所抓取之實體的導覽屬性可能不會自動填入與這些實體相關的資料。</span><span class="sxs-lookup"><span data-stu-id="939d9-187">(Navigation properties of entities retrieved by a stored procedure might not be automatically populated with the data related to those entities, depending on `ObjectContext` default settings.</span></span> <span data-ttu-id="939d9-188">如需詳細資訊，請參閱 MSDN Library 中的[載入相關物件](https://msdn.microsoft.com/library/bb896272.aspx)。）</span><span class="sxs-lookup"><span data-stu-id="939d9-188">For more information, see [Loading Related Objects](https://msdn.microsoft.com/library/bb896272.aspx) in the MSDN Library.)</span></span>

<span data-ttu-id="939d9-189">在下一個教學課程中，您將瞭解如何使用動態資料功能，讓您更輕鬆地設計和測試資料格式和驗證規則。</span><span class="sxs-lookup"><span data-stu-id="939d9-189">In the next tutorial, you'll learn how to use Dynamic Data functionality to make it easier to program and test data formatting and validation rules.</span></span> <span data-ttu-id="939d9-190">您可以在資料模型中繼資料中指定這類規則，而不是在每個網頁規則上指定，而不是在每個頁面上都自動套用。</span><span class="sxs-lookup"><span data-stu-id="939d9-190">Instead of specifying on each web page rules such as data format strings and whether or not a field is required, you can specify such rules in data model metadata and they're automatically applied on every page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="939d9-191">[上一頁](the-entity-framework-and-aspnet-getting-started-part-6.md)
> [下一頁](the-entity-framework-and-aspnet-getting-started-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="939d9-191">[Previous](the-entity-framework-and-aspnet-getting-started-part-6.md)
[Next](the-entity-framework-and-aspnet-getting-started-part-8.md)</span></span>
