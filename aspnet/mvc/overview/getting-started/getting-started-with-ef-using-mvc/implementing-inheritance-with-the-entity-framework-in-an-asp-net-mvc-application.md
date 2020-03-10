---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教學課程：在 ASP.NET MVC 5 應用程式中使用 EF 執行繼承
description: 本教學課程將示範如何在資料模型中實作繼承。
author: tdykstra
ms.author: riande
ms.date: 01/21/2019
ms.topic: tutorial
ms.assetid: 08834147-77ec-454a-bb7a-d931d2a40dab
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 73a01ed47b0935a1a9734c197377470defb1fe36
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583059"
---
# <a name="tutorial-implement-inheritance-with-ef-in-an-aspnet-mvc-5-app"></a><span data-ttu-id="e97f4-103">教學課程：在 ASP.NET MVC 5 應用程式中使用 EF 執行繼承</span><span class="sxs-lookup"><span data-stu-id="e97f4-103">Tutorial: Implement Inheritance with EF in an ASP.NET MVC 5 app</span></span>

<span data-ttu-id="e97f4-104">在上一個教學課程中，您已處理並行例外狀況。</span><span class="sxs-lookup"><span data-stu-id="e97f4-104">In the previous tutorial you handled concurrency exceptions.</span></span> <span data-ttu-id="e97f4-105">本教學課程將示範如何在資料模型中實作繼承。</span><span class="sxs-lookup"><span data-stu-id="e97f4-105">This tutorial will show you how to implement inheritance in the data model.</span></span>

<span data-ttu-id="e97f4-106">在物件導向程式設計中，您可以使用[繼承](http://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming))來加速程式[代碼重複使用](http://en.wikipedia.org/wiki/Code_reuse)。</span><span class="sxs-lookup"><span data-stu-id="e97f4-106">In object-oriented programming, you can use [inheritance](http://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)) to facilitate [code reuse](http://en.wikipedia.org/wiki/Code_reuse).</span></span> <span data-ttu-id="e97f4-107">在本教學課程中，您將變更 `Instructor` 和 `Student` 類別，讓它們衍生自 `Person` 基底類別，而此基底類別包含講師和學生通用的屬性，例如 `LastName`。</span><span class="sxs-lookup"><span data-stu-id="e97f4-107">In this tutorial, you'll change the `Instructor` and `Student` classes so that they derive from a `Person` base class which contains properties such as `LastName` that are common to both instructors and students.</span></span> <span data-ttu-id="e97f4-108">您不會新增或變更任何網頁，但是您將變更一些程式碼，這些變更將會自動反映在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="e97f4-108">You won't add or change any web pages, but you'll change some of the code and those changes will be automatically reflected in the database.</span></span>

<span data-ttu-id="e97f4-109">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="e97f4-109">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e97f4-110">瞭解如何將繼承對應至資料庫</span><span class="sxs-lookup"><span data-stu-id="e97f4-110">Learn to map inheritance to database</span></span>
> * <span data-ttu-id="e97f4-111">建立 Person 類別</span><span class="sxs-lookup"><span data-stu-id="e97f4-111">Create the Person class</span></span>
> * <span data-ttu-id="e97f4-112">更新 Instructor 和 Student</span><span class="sxs-lookup"><span data-stu-id="e97f4-112">Update Instructor and Student</span></span>
> * <span data-ttu-id="e97f4-113">將 Person 新增至模型</span><span class="sxs-lookup"><span data-stu-id="e97f4-113">Add Person to the Model</span></span>
> * <span data-ttu-id="e97f4-114">建立和更新遷移</span><span class="sxs-lookup"><span data-stu-id="e97f4-114">Create and Update Migrations</span></span>
> * <span data-ttu-id="e97f4-115">測試實作</span><span class="sxs-lookup"><span data-stu-id="e97f4-115">Test the implementation</span></span>
> * <span data-ttu-id="e97f4-116">部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="e97f4-116">Deploy to Azure</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e97f4-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e97f4-117">Prerequisites</span></span>

* [<span data-ttu-id="e97f4-118">處理並行</span><span class="sxs-lookup"><span data-stu-id="e97f4-118">Handling Concurrency</span></span>](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="map-inheritance-to-database"></a><span data-ttu-id="e97f4-119">將繼承對應至資料庫</span><span class="sxs-lookup"><span data-stu-id="e97f4-119">Map inheritance to database</span></span>

<span data-ttu-id="e97f4-120">`School` 資料模型中的 `Instructor` 和 `Student` 類別有數個相同的屬性：</span><span class="sxs-lookup"><span data-stu-id="e97f4-120">The `Instructor` and `Student` classes in the `School` data model have several properties that are identical:</span></span>

![Student_and_Instructor_classes](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="e97f4-122">假設您想要針對 `Instructor` 和 `Student` 實體所共用的屬性消除多餘的程式碼。</span><span class="sxs-lookup"><span data-stu-id="e97f4-122">Suppose you want to eliminate the redundant code for the properties that are shared by the `Instructor` and `Student` entities.</span></span> <span data-ttu-id="e97f4-123">或者，您想要撰寫服務，以便用來格式化名稱，而無需在意名稱是來自講師還是學生。</span><span class="sxs-lookup"><span data-stu-id="e97f4-123">Or you want to write a service that can format names without caring whether the name came from an instructor or a student.</span></span> <span data-ttu-id="e97f4-124">您可以建立只包含這些共用屬性的 `Person` 基類，然後讓 `Instructor` 和 `Student` 實體繼承自該基類，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="e97f4-124">You could create a `Person` base class which contains only those shared properties, then make the `Instructor` and `Student` entities inherit from that base class, as shown in the following illustration:</span></span>

![Student_and_Instructor_classes_deriving_from_Person_class](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="e97f4-126">有幾種方式可以在資料庫中表示此繼承結構。</span><span class="sxs-lookup"><span data-stu-id="e97f4-126">There are several ways this inheritance structure could be represented in the database.</span></span> <span data-ttu-id="e97f4-127">您可以有一個 `Person` 的資料表，其中包含單一資料表中的學生和講師的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e97f4-127">You could have a `Person` table that includes information about both students and instructors in a single table.</span></span> <span data-ttu-id="e97f4-128">有些資料行僅適用于講師（`HireDate`），部分僅供學生（`EnrollmentDate`）使用，部分至（`LastName`，`FirstName`）。</span><span class="sxs-lookup"><span data-stu-id="e97f4-128">Some of the columns could apply only to instructors (`HireDate`), some only to students (`EnrollmentDate`), some to both (`LastName`, `FirstName`).</span></span> <span data-ttu-id="e97f4-129">一般而言，您會有一個*鑒別*子資料行，以指出每個資料列所代表的類型。</span><span class="sxs-lookup"><span data-stu-id="e97f4-129">Typically, you'd have a *discriminator* column to indicate which type each row represents.</span></span> <span data-ttu-id="e97f4-130">例如，鑑別子資料行的 "Instructor" 代表講師，而 "Student" 代表學生。</span><span class="sxs-lookup"><span data-stu-id="e97f4-130">For example, the discriminator column might have "Instructor" for instructors and "Student" for students.</span></span>

![每 hierarchy_example 一個資料表](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="e97f4-132">從單一資料庫資料表產生實體繼承結構的這種模式稱為「*每個階層的資料表*」（TPH）繼承。</span><span class="sxs-lookup"><span data-stu-id="e97f4-132">This pattern of generating an entity inheritance structure from a single database table is called *table-per-hierarchy* (TPH) inheritance.</span></span>

<span data-ttu-id="e97f4-133">替代方法是讓資料庫看起來更像繼承結構。</span><span class="sxs-lookup"><span data-stu-id="e97f4-133">An alternative is to make the database look more like the inheritance structure.</span></span> <span data-ttu-id="e97f4-134">例如，您可以只有 `Person` 資料表中的 [名稱] 欄位，而且有不同的 `Instructor` 和 `Student` 資料表與日期欄位。</span><span class="sxs-lookup"><span data-stu-id="e97f4-134">For example, you could have only the name fields in the `Person` table and have separate `Instructor` and `Student` tables with the date fields.</span></span>

![每 type_inheritance 一個資料表](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="e97f4-136">為每個實體類別建立資料庫資料表的這種模式，稱為「*每一類型的資料表*」（TPT）繼承。</span><span class="sxs-lookup"><span data-stu-id="e97f4-136">This pattern of making a database table for each entity class is called *table per type* (TPT) inheritance.</span></span>

<span data-ttu-id="e97f4-137">還有另一個選項是將所有的非抽象類型對應至個別資料表。</span><span class="sxs-lookup"><span data-stu-id="e97f4-137">Yet another option is to map all non-abstract types to individual tables.</span></span> <span data-ttu-id="e97f4-138">類別的所有屬性 (包括繼承的屬性) 都會對應至對應資料表的資料行。</span><span class="sxs-lookup"><span data-stu-id="e97f4-138">All properties of a class, including inherited properties, map to columns of the corresponding table.</span></span> <span data-ttu-id="e97f4-139">這個模式稱為一實體類一表 (TPC) 繼承。</span><span class="sxs-lookup"><span data-stu-id="e97f4-139">This pattern is called Table-per-Concrete Class (TPC) inheritance.</span></span> <span data-ttu-id="e97f4-140">如果您已如先前所示，對 `Person`、`Student`和 `Instructor` 類別執行 TPC 繼承，`Student` 和 `Instructor` 資料表在執行繼承之後看起來不會與之前相同。</span><span class="sxs-lookup"><span data-stu-id="e97f4-140">If you implemented TPC inheritance for the `Person`, `Student`, and `Instructor` classes as shown earlier, the `Student` and `Instructor` tables would look no different after implementing inheritance than they did before.</span></span>

<span data-ttu-id="e97f4-141">TPC 和 TPH 繼承模式通常會在 Entity Framework 中提供比 TPT 繼承模式更好的效能，因為 TPT 模式可能會導致複雜的聯結查詢。</span><span class="sxs-lookup"><span data-stu-id="e97f4-141">TPC and TPH inheritance patterns generally deliver better performance in the Entity Framework than TPT inheritance patterns, because TPT patterns can result in complex join queries.</span></span>

<span data-ttu-id="e97f4-142">本教學課程將示範如何實作 TPH 繼承。</span><span class="sxs-lookup"><span data-stu-id="e97f4-142">This tutorial demonstrates how to implement TPH inheritance.</span></span> <span data-ttu-id="e97f4-143">TPH 是 Entity Framework 中的預設繼承模式，因此您只需要建立 `Person` 類別，將 `Instructor` 和 `Student` 類別變更為衍生自 `Person`，將新類別新增至 `DbContext`，並建立遷移。</span><span class="sxs-lookup"><span data-stu-id="e97f4-143">TPH is the default inheritance pattern in the Entity Framework, so all you have to do is create a `Person` class, change the `Instructor` and `Student` classes to derive from `Person`, add the new class to the `DbContext`, and create a migration.</span></span> <span data-ttu-id="e97f4-144">（如需如何執行其他繼承模式的相關資訊，請參閱 MSDN Entity Framework 檔中的[對應每一類型的資料表（TPT）繼承](https://msdn.microsoft.com/data/jj591617#2.5)和[對應每個具體的資料表類別（TPC）繼承](https://msdn.microsoft.com/data/jj591617#2.6)。</span><span class="sxs-lookup"><span data-stu-id="e97f4-144">(For information about how to implement the other inheritance patterns, see [Mapping the Table-Per-Type (TPT) Inheritance](https://msdn.microsoft.com/data/jj591617#2.5) and [Mapping the Table-Per-Concrete Class (TPC) Inheritance](https://msdn.microsoft.com/data/jj591617#2.6) in the MSDN Entity Framework documentation.)</span></span>

## <a name="create-the-person-class"></a><span data-ttu-id="e97f4-145">建立 Person 類別</span><span class="sxs-lookup"><span data-stu-id="e97f4-145">Create the Person class</span></span>

<span data-ttu-id="e97f4-146">在 [*模型*] 資料夾中，建立*Person.cs* ，並將範本程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="e97f4-146">In the *Models* folder, create *Person.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="update-instructor-and-student"></a><span data-ttu-id="e97f4-147">更新 Instructor 和 Student</span><span class="sxs-lookup"><span data-stu-id="e97f4-147">Update Instructor and Student</span></span>

<span data-ttu-id="e97f4-148">現在更新*Instructor.cs*和*Student.cs* ，以繼承*Person.sc*的值。</span><span class="sxs-lookup"><span data-stu-id="e97f4-148">Now update the *Instructor.cs* and *Student.cs* to inherit values from the *Person.sc*.</span></span>

<span data-ttu-id="e97f4-149">在*Instructor.cs*中，從 `Person` 類別衍生 `Instructor` 類別，並移除 [索引鍵] 和 [名稱] 欄位。</span><span class="sxs-lookup"><span data-stu-id="e97f4-149">In *Instructor.cs*, derive the `Instructor` class from the `Person` class and remove the key and name fields.</span></span> <span data-ttu-id="e97f4-150">程式碼看起來應該如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="e97f4-150">The code will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="e97f4-151">對*Student.cs*進行類似的變更。</span><span class="sxs-lookup"><span data-stu-id="e97f4-151">Make similar changes to *Student.cs*.</span></span> <span data-ttu-id="e97f4-152">`Student` 類別看起來會如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="e97f4-152">The `Student` class will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="add-person-to-the-model"></a><span data-ttu-id="e97f4-153">將 Person 新增至模型</span><span class="sxs-lookup"><span data-stu-id="e97f4-153">Add Person to the Model</span></span>

<span data-ttu-id="e97f4-154">在*SchoolCoNtext.cs*中，加入 `Person` 實體類型的 `DbSet` 屬性：</span><span class="sxs-lookup"><span data-stu-id="e97f4-154">In *SchoolContext.cs*, add a `DbSet` property for the `Person` entity type:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="e97f4-155">這就是 Entity Framework 為了設定單表繼承而必須執行的所有工作。</span><span class="sxs-lookup"><span data-stu-id="e97f4-155">This is all that the Entity Framework needs in order to configure table-per-hierarchy inheritance.</span></span> <span data-ttu-id="e97f4-156">如您所見，當資料庫更新時，它會有一個 `Person` 資料表來取代 `Student` 和 `Instructor` 資料表。</span><span class="sxs-lookup"><span data-stu-id="e97f4-156">As you'll see, when the database is updated, it will have a `Person` table in place of the `Student` and `Instructor` tables.</span></span>

## <a name="create-and-update-migrations"></a><span data-ttu-id="e97f4-157">建立和更新遷移</span><span class="sxs-lookup"><span data-stu-id="e97f4-157">Create and Update Migrations</span></span>

<span data-ttu-id="e97f4-158">在 [套件管理員主控台] （PMC）中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="e97f4-158">In the Package Manager Console (PMC), enter the following command:</span></span>

`Add-Migration Inheritance`

<span data-ttu-id="e97f4-159">在 PMC 中執行 `Update-Database` 命令。</span><span class="sxs-lookup"><span data-stu-id="e97f4-159">Run the `Update-Database` command in the PMC.</span></span> <span data-ttu-id="e97f4-160">此時，此命令將會失敗，因為我們有遷移不知道如何處理的現有資料。</span><span class="sxs-lookup"><span data-stu-id="e97f4-160">The command will fail at this point because we have existing data that migrations doesn't know how to handle.</span></span> <span data-ttu-id="e97f4-161">您會收到類似下列的錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="e97f4-161">You get an error message like the following one:</span></span>

> <span data-ttu-id="e97f4-162">*無法捨棄物件 ' dbo。講師 '，因為它是由 FOREIGN KEY 條件約束所參考。*</span><span class="sxs-lookup"><span data-stu-id="e97f4-162">*Could not drop object 'dbo.Instructor' because it is referenced by a FOREIGN KEY constraint.*</span></span>

<span data-ttu-id="e97f4-163">開啟 *[遷移]\&lt; 時間戳記&gt;\_Inheritance.cs* ，並以下列程式碼取代 `Up` 方法：</span><span class="sxs-lookup"><span data-stu-id="e97f4-163">Open *Migrations\&lt;timestamp&gt;\_Inheritance.cs* and replace the `Up` method with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

<span data-ttu-id="e97f4-164">此程式碼負責下列資料庫更新工作：</span><span class="sxs-lookup"><span data-stu-id="e97f4-164">This code takes care of the following database update tasks:</span></span>

- <span data-ttu-id="e97f4-165">移除指向 Student 資料表的外部索引鍵條件約束和索引。</span><span class="sxs-lookup"><span data-stu-id="e97f4-165">Removes foreign key constraints and indexes that point to the Student table.</span></span>
- <span data-ttu-id="e97f4-166">將 Instructor 資料表重新命名為 Person，並對其進行所需的變更來儲存 Student 資料：</span><span class="sxs-lookup"><span data-stu-id="e97f4-166">Renames the Instructor table as Person and makes changes needed for it to store Student data:</span></span>

    - <span data-ttu-id="e97f4-167">針對學生新增可為 null 的 EnrollmentDate。</span><span class="sxs-lookup"><span data-stu-id="e97f4-167">Adds nullable EnrollmentDate for students.</span></span>
    - <span data-ttu-id="e97f4-168">新增 Discriminator 資料行，以指出資料列適用於學生或講師。</span><span class="sxs-lookup"><span data-stu-id="e97f4-168">Adds Discriminator column to indicate whether a row is for a student or an instructor.</span></span>
    - <span data-ttu-id="e97f4-169">使 HireDate 成為可為 Null，因為學生資料列不會有雇用日期。</span><span class="sxs-lookup"><span data-stu-id="e97f4-169">Makes HireDate nullable since student rows won't have hire dates.</span></span>
    - <span data-ttu-id="e97f4-170">新增暫存欄位，它將用來更新指向學生的外部索引鍵。</span><span class="sxs-lookup"><span data-stu-id="e97f4-170">Adds a temporary field that will be used to update foreign keys that point to students.</span></span> <span data-ttu-id="e97f4-171">當您將學生複製到 Person 資料表時，他們會取得新的主要金鑰值。</span><span class="sxs-lookup"><span data-stu-id="e97f4-171">When you copy students into the Person table they'll get new primary key values.</span></span>
- <span data-ttu-id="e97f4-172">將 Student 資料表中的資料複製到 Person 資料表。</span><span class="sxs-lookup"><span data-stu-id="e97f4-172">Copies data from the Student table into the Person table.</span></span> <span data-ttu-id="e97f4-173">這會導致學生獲指派新的主索引鍵值。</span><span class="sxs-lookup"><span data-stu-id="e97f4-173">This causes students to get assigned new primary key values.</span></span>
- <span data-ttu-id="e97f4-174">修正指向學生的外部索引鍵值。</span><span class="sxs-lookup"><span data-stu-id="e97f4-174">Fixes foreign key values that point to students.</span></span>
- <span data-ttu-id="e97f4-175">重新建立外部索引鍵條件約束和索引，現在將它們指向 Person 資料表。</span><span class="sxs-lookup"><span data-stu-id="e97f4-175">Re-creates foreign key constraints and indexes, now pointing them to the Person table.</span></span>

<span data-ttu-id="e97f4-176">(如果您使用 GUID 而不是整數作為主索引鍵類型，學生的主索引鍵值將無需變更，而且可能已省略其中幾個步驟。)</span><span class="sxs-lookup"><span data-stu-id="e97f4-176">(If you had used GUID instead of integer as the primary key type, the student primary key values wouldn't have to change, and several of these steps could have been omitted.)</span></span>

<span data-ttu-id="e97f4-177">再次執行 `update-database` 命令。</span><span class="sxs-lookup"><span data-stu-id="e97f4-177">Run the `update-database` command again.</span></span>

<span data-ttu-id="e97f4-178">（在生產系統中，您會對 Down 方法進行相對應的變更，以防您必須使用它來返回先前的資料庫版本。</span><span class="sxs-lookup"><span data-stu-id="e97f4-178">(In a production system you would make corresponding changes to the Down method in case you ever had to use that to go back to the previous database version.</span></span> <span data-ttu-id="e97f4-179">在本教學課程中，您將不會使用向下方法）。</span><span class="sxs-lookup"><span data-stu-id="e97f4-179">For this tutorial you won't be using the Down method.)</span></span>

> [!NOTE]
> <span data-ttu-id="e97f4-180">當您遷移資料並進行架構變更時，可能會收到其他錯誤。</span><span class="sxs-lookup"><span data-stu-id="e97f4-180">It's possible to get other errors when migrating data and making schema changes.</span></span> <span data-ttu-id="e97f4-181">如果您收到無法解決的遷移錯誤，可以藉由變更*web.config*檔案中的連接字串或刪除資料庫來繼續進行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="e97f4-181">If you get migration errors you can't resolve, you can continue with the tutorial by changing the connection string in the *Web.config* file or by deleting the database.</span></span> <span data-ttu-id="e97f4-182">最簡單的方法是*在 web.config 檔案*中重新命名資料庫。</span><span class="sxs-lookup"><span data-stu-id="e97f4-182">The simplest approach is to rename the database in the *Web.config* file.</span></span> <span data-ttu-id="e97f4-183">例如，將資料庫名稱變更為 ContosoUniversity2，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="e97f4-183">For example, change the database name to ContosoUniversity2 as shown in the following example:</span></span>
>
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.xml?highlight=2)]
>
> <span data-ttu-id="e97f4-184">使用新的資料庫時，沒有可遷移的資料，而且 `update-database` 命令較可能會在沒有錯誤的情況下完成。</span><span class="sxs-lookup"><span data-stu-id="e97f4-184">With a new database, there is no data to migrate, and the `update-database` command is much more likely to complete without errors.</span></span> <span data-ttu-id="e97f4-185">如需有關如何刪除資料庫的指示，請參閱[如何從 Visual Studio 2012 卸載資料庫](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)。</span><span class="sxs-lookup"><span data-stu-id="e97f4-185">For instructions on how to delete the database, see [How to Drop a Database from Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span></span> <span data-ttu-id="e97f4-186">如果您採用此方法來繼續進行本教學課程，請略過本教學課程結尾的部署步驟，或部署到新的網站和資料庫。</span><span class="sxs-lookup"><span data-stu-id="e97f4-186">If you take this approach in order to continue with the tutorial, skip the deployment step at the end of this tutorial or deploy to a new site and database.</span></span> <span data-ttu-id="e97f4-187">如果您將更新部署至已部署至的相同網站，則 EF 會在執行自動遷移時收到相同的錯誤。</span><span class="sxs-lookup"><span data-stu-id="e97f4-187">If you deploy an update to the same site you've been deploying to already, EF will get the same error there when it runs migrations automatically.</span></span> <span data-ttu-id="e97f4-188">如果您想要針對遷移錯誤進行疑難排解，最佳資源是其中一個 Entity Framework 論壇或 StackOverflow.com。</span><span class="sxs-lookup"><span data-stu-id="e97f4-188">If you want to troubleshoot a migrations error, the best resource is one of the Entity Framework forums or StackOverflow.com.</span></span>

## <a name="test-the-implementation"></a><span data-ttu-id="e97f4-189">測試實作</span><span class="sxs-lookup"><span data-stu-id="e97f4-189">Test the implementation</span></span>

<span data-ttu-id="e97f4-190">執行網站並嘗試各種頁面。</span><span class="sxs-lookup"><span data-stu-id="e97f4-190">Run the site and try various pages.</span></span> <span data-ttu-id="e97f4-191">一切項目的運作與之前一樣。</span><span class="sxs-lookup"><span data-stu-id="e97f4-191">Everything works the same as it did before.</span></span>

<span data-ttu-id="e97f4-192">在**伺服器總管中，** 依序展開 [**資料 Connections\SchoolCoNtext** ] 和 [**資料表]** ，您會看到 [ **Student** ] 和 [**講師**] 資料表已由 [ **Person** ] 資料表取代。</span><span class="sxs-lookup"><span data-stu-id="e97f4-192">In **Server Explorer,** expand **Data Connections\SchoolContext** and then **Tables**, and you see that the **Student** and **Instructor** tables have been replaced by a **Person** table.</span></span> <span data-ttu-id="e97f4-193">展開 [ **Person** ] 資料表，您就會看到它擁有所有用在**學生**和**講師**資料表中的資料行。</span><span class="sxs-lookup"><span data-stu-id="e97f4-193">Expand the **Person** table and you see that it has all of the columns that used to be in the **Student** and **Instructor** tables.</span></span>

<span data-ttu-id="e97f4-194">以滑鼠右鍵按一下 Person 資料表，然後按一下 [顯示資料表資料] 以查看鑑別子資料行。</span><span class="sxs-lookup"><span data-stu-id="e97f4-194">Right-click the Person table, and then click **Show Table Data** to see the discriminator column.</span></span>

<span data-ttu-id="e97f4-195">下圖說明新 School 資料庫的結構：</span><span class="sxs-lookup"><span data-stu-id="e97f4-195">The following diagram illustrates the structure of the new School database:</span></span>

![School_database_diagram](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="e97f4-197">部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="e97f4-197">Deploy to Azure</span></span>

<span data-ttu-id="e97f4-198">本節要求您已完成本教學課程系列的[第3部分、排序、篩選和分頁](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)中的選擇性將**應用程式部署至 Azure**一節。</span><span class="sxs-lookup"><span data-stu-id="e97f4-198">This section requires you to have completed the optional **Deploying the app to Azure** section in [Part 3, Sorting, Filtering, and Paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md) of this tutorial series.</span></span> <span data-ttu-id="e97f4-199">如果您藉由刪除本機專案中的資料庫來解決了遷移錯誤，請略過此步驟;或者，建立新的網站和資料庫，並部署到新的環境。</span><span class="sxs-lookup"><span data-stu-id="e97f4-199">If you had migrations errors that you resolved by deleting the database in your local project, skip this step; or create a new site and database, and deploy to the new environment.</span></span>

1. <span data-ttu-id="e97f4-200">在 Visual Studio 的 [方案總管] 中以滑鼠右鍵按一下專案，再選取內容功能表中的 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="e97f4-200">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>

2. <span data-ttu-id="e97f4-201">按一下 [發行]。</span><span class="sxs-lookup"><span data-stu-id="e97f4-201">Click **Publish**.</span></span>

    <span data-ttu-id="e97f4-202">Web 應用程式會在您的預設瀏覽器中開啟。</span><span class="sxs-lookup"><span data-stu-id="e97f4-202">The Web app opens in your default browser.</span></span>

3. <span data-ttu-id="e97f4-203">測試應用程式以確認其運作正常。</span><span class="sxs-lookup"><span data-stu-id="e97f4-203">Test the application to verify it's working.</span></span>

    <span data-ttu-id="e97f4-204">當您第一次執行存取資料庫的頁面時，Entity Framework 會執行所有需要的遷移 `Up` 方法，使資料庫與目前的資料模型保持在最新狀態。</span><span class="sxs-lookup"><span data-stu-id="e97f4-204">The first time you run a page that accesses the database, the Entity Framework runs all of the migrations `Up` methods required to bring the database up to date with the current data model.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="e97f4-205">取得程式碼</span><span class="sxs-lookup"><span data-stu-id="e97f4-205">Get the code</span></span>

[<span data-ttu-id="e97f4-206">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="e97f4-206">Download Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="e97f4-207">其他資源</span><span class="sxs-lookup"><span data-stu-id="e97f4-207">Additional resources</span></span>

<span data-ttu-id="e97f4-208">您可以在[ASP.NET 資料存取-建議的資源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。</span><span class="sxs-lookup"><span data-stu-id="e97f4-208">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

<span data-ttu-id="e97f4-209">如需有關這個和其他繼承結構的詳細資訊，請參閱 MSDN 上的[TPT 繼承模式](https://msdn.microsoft.com/data/jj618293)和[TPH 繼承模式](https://msdn.microsoft.com/data/jj618292)。</span><span class="sxs-lookup"><span data-stu-id="e97f4-209">For more information about this and other inheritance structures, see [TPT Inheritance Pattern](https://msdn.microsoft.com/data/jj618293) and [TPH Inheritance Pattern](https://msdn.microsoft.com/data/jj618292) on MSDN.</span></span> <span data-ttu-id="e97f4-210">在下一個教學課程中，您將了解如何處理各種相對進階的 Entity Framework 案例。</span><span class="sxs-lookup"><span data-stu-id="e97f4-210">In the next tutorial you'll see how to handle a variety of relatively advanced Entity Framework scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e97f4-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e97f4-211">Next steps</span></span>

<span data-ttu-id="e97f4-212">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="e97f4-212">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e97f4-213">瞭解如何將繼承對應至資料庫</span><span class="sxs-lookup"><span data-stu-id="e97f4-213">Learned to map inheritance to database</span></span>
> * <span data-ttu-id="e97f4-214">建立 Person 類別</span><span class="sxs-lookup"><span data-stu-id="e97f4-214">Created the Person class</span></span>
> * <span data-ttu-id="e97f4-215">更新 Instructor 和 Student</span><span class="sxs-lookup"><span data-stu-id="e97f4-215">Updated Instructor and Student</span></span>
> * <span data-ttu-id="e97f4-216">已將人員新增至模型</span><span class="sxs-lookup"><span data-stu-id="e97f4-216">Added Person to the Model</span></span>
> * <span data-ttu-id="e97f4-217">建立和更新遷移</span><span class="sxs-lookup"><span data-stu-id="e97f4-217">Created and Update Migrations</span></span>
> * <span data-ttu-id="e97f4-218">測試實作</span><span class="sxs-lookup"><span data-stu-id="e97f4-218">Tested the implementation</span></span>
> * <span data-ttu-id="e97f4-219">已部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="e97f4-219">Deployed to Azure</span></span>

<span data-ttu-id="e97f4-220">前往下一篇文章，以瞭解當您超越開發使用 Entity Framework Code First 的 ASP.NET web 應用程式的基本概念時，可以注意的主題。</span><span class="sxs-lookup"><span data-stu-id="e97f4-220">Advance to the next article to learn about topics that are useful to be aware of when you go beyond the basics of developing ASP.NET web applications that use Entity Framework Code First.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="e97f4-221">進階 Entity Framework 案例</span><span class="sxs-lookup"><span data-stu-id="e97f4-221">Advanced Entity Framework Scenarios</span></span>](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
