---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
title: 在 ASP.NET MVC 應用程式中執行存放庫和工作單位模式（9/10） |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio ... 來建立 ASP.NET MVC 4 應用程式。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 44761193-04ba-4990-9f90-145d3c10a716
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 18de9b125ee5d10795b9ce1a366918dadf4fc4e3
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595235"
---
# <a name="implementing-the-repository-and-unit-of-work-patterns-in-an-aspnet-mvc-application-9-of-10"></a>在 ASP.NET MVC 應用程式中執行存放庫和工作單位模式（9/10）

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載已完成的專案](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。 如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 您可以從一開始就開始本教學課程系列，或[下載本章節的入門專案](building-the-ef5-mvc4-chapter-downloads.md)，並從這裡開始。
> 
> > [!NOTE] 
> > 
> > 如果您遇到無法解決的問題，請[下載完整的章節](building-the-ef5-mvc4-chapter-downloads.md)並嘗試重現您的問題。 您通常可以藉由比較您的程式碼與已完成的程式碼，來找出問題的解決方法。 如需瞭解一些常見錯誤以及如何解決問題，請參閱[錯誤和](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)因應措施。

在上一個教學課程中，您使用了繼承來減少 `Student` 和 `Instructor` 實體類別中的重複程式碼。 在本教學課程中，您會看到一些使用存放庫和 CRUD 作業單元模式的方式。 如同在上一個教學課程中，您將會變更程式碼與您已建立的頁面，而不是建立新頁面的方式。

## <a name="the-repository-and-unit-of-work-patterns"></a>儲存機制和工作單位模式

儲存機制和工作單位模式的目的是要在應用程式的資料存取層與商務邏輯層之間建立抽象層。 實作這些模式可協助隔離您的應用程式與資料存放區中的變更，並可促進自動化單元測試或測試驅動開發 (TDD)。

在本教學課程中，您將為每個實體類型執行存放庫類別。 針對 `Student` 實體類型，您將建立存放庫介面和儲存機制類別。 當您具現化控制器中的存放庫時，您將會使用介面，讓控制器接受任何可執行存放庫介面之物件的參考。 當控制器在 web 伺服器下執行時，它會接收與 Entity Framework 搭配運作的存放庫。 當控制器在單元測試類別下執行時，它會接收使用儲存之資料的儲存機制，您可以輕鬆地操作以進行測試，例如記憶體中的集合。

稍後在本教學課程中，您將使用多個儲存機制和工作單位類別，做為 `Course` 控制器中的 `Course` 和 `Department` 實體類型。 工作單位類別會藉由建立所有儲存機制所共用的單一資料庫內容類別，來協調多個存放庫的工作。 如果您想要能夠執行自動化單元測試，您可以使用與 `Student` 存放庫相同的方式，為這些類別建立和使用介面。 不過，為了讓教學課程保持簡單，您將建立並使用這些沒有介面的類別。

下圖顯示相較于不使用存放庫或工作單位模式的情況，與控制器和內容類別別之間的關聯性進行概念化的一種方式。

![Repository_pattern_diagram](https://asp.net/media/2578149/Windows-Live-Writer_8c4963ba1fa3_CE3B_Repository_pattern_diagram_1df790d3-bdf2-4c11-9098-946ddd9cd884.png)

您不會在本教學課程系列中建立單元測試。 如需使用儲存機制模式之 MVC 應用程式的 TDD 簡介，請參閱[逐步解說：搭配使用 TDD 與 ASP.NET MVC](https://msdn.microsoft.com/library/ff847525.aspx)。 如需存放庫模式的詳細資訊，請參閱下列資源：

- MSDN 上[的存放庫模式](https://msdn.microsoft.com/library/ff649690.aspx)。
- 在 Entity Framework 的 team blog 上[使用 Entity Framework 4.0 的存放庫和工作單位模式](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx)。
- [Agile Entity Framework 4](http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-1-model-and-poco-classes/) Julie Lerman 的 blog 上的一系列文章。
- 在 Dan Wahlin 的 blog 上，[建立一眼 HTML5/JQuery 應用程式的帳戶](https://weblogs.asp.net/dwahlin/archive/2011/08/15/building-the-account-at-a-glance-html5-jquery-application.aspx)。

> [!NOTE]
> 有許多方法可以執行存放庫和工作單位模式。 您可以使用具有或不含工作單位類別的儲存機制類別。 您可以針對所有實體類型，或針對每個類型來執行單一存放庫。 如果您針對每個類型執行一個，則可以使用不同的類別、泛型基類和衍生類別，或是抽象基類和衍生類別。 您可以在存放庫中包含商務邏輯，或將其限制為數據存取邏輯。 您也可以使用[idbset 會](https://msdn.microsoft.com/library/gg679233(v=vs.103).aspx)介面（而不是您的實體集的[DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx)類型），將抽象層建立到資料庫內容類別中。 本教學課程中所示的抽象層的執行方法是您可以考慮的一個選項，而不是所有案例和環境的建議。

## <a name="creating-the-student-repository-class"></a>建立 Student 存放庫類別

在*DAL*資料夾中，建立名為*IStudentRepository.cs*的類別檔案，並以下列程式碼取代現有的程式碼：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample1.cs)]

此程式碼會宣告一組典型的 CRUD 方法，包括兩個讀取方法：一個會傳回所有 `Student` 實體，另一個則會依識別碼尋找單一 `Student` 實體。

在*DAL*資料夾中，建立名為*StudentRepository.cs* file 的類別檔案。 將現有的程式碼取代為下列程式碼，以執行 `IStudentRepository` 介面：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample2.cs)]

資料庫內容定義于類別變數中，而此函式需要呼叫物件傳入內容的實例：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample3.cs)]

您可以在存放庫中具現化新的內容，但如果您在一個控制器中使用多個存放庫，每個都有不同的內容。 稍後您將在 `Course` 控制器中使用多個存放庫，您會看到工作單位類別如何確保所有存放庫都使用相同的內容。

儲存機制會依照您稍早在控制器中看到的方式來執行[IDisposable](https://msdn.microsoft.com/library/system.idisposable.aspx)和處置資料庫內容，而其 CRUD 方法會以您稍早所見的相同方式呼叫資料庫內容。

## <a name="change-the-student-controller-to-use-the-repository"></a>變更學生控制器以使用存放庫

在*StudentController.cs*中，將類別中目前的程式碼取代為下列程式碼。 所做的變更已醒目標示。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=13-18,44,75,77,102-103,120,137-138,159,172-174,186)]

控制器現在會針對執行 `IStudentRepository` 介面（而非內容類別）的物件宣告類別變數：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample5.cs)]

預設的（無參數）處理常式會建立新的內容實例，而選擇性的函式可讓呼叫者傳入內容實例。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample6.cs)]

（如果您使用的是相依性*插入*或 DI，則不需要預設的函式，因為 DI 軟體會確保一律會提供正確的存放庫物件）。

在 CRUD 方法中，現在會呼叫儲存機制，而不是內容：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample7.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample8.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample9.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample10.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample11.cs)]

而 `Dispose` 方法現在會處置存放庫，而不是內容：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample12.cs)]

執行網站，然後按一下 [**學生**] 索引標籤。

![Students_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image1.png)

此頁面的外觀和運作方式與您變更程式碼以使用存放庫之前一樣，而其他學生頁面也會運作相同。 不過，控制器的 `Index` 方法進行篩選和排序的方式有一項重要的差異。 這個方法的原始版本包含下列程式碼：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample13.cs?highlight=1)]

更新的 `Index` 方法包含下列程式碼：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=1)]

只有反白顯示的程式碼才會變更。

在程式碼的原始版本中，`students` 會輸入為 `IQueryable` 物件。 查詢不會傳送到資料庫，直到使用 `ToList`之類的方法將它轉換成集合，直到索引視圖存取學生模型為止。 上述原始程式碼中的 `Where` 方法，會成為傳送至資料庫之 SQL 查詢中的 `WHERE` 子句。 這也表示，只有選取的實體會由資料庫傳回。 不過，由於將 `context.Students` 變更為 `studentRepository.GetStudents()`，因此在此語句之後的 `students` 變數是包含資料庫中所有學生的 `IEnumerable` 集合。 套用 `Where` 方法的最終結果是相同的，但現在工作是在 web 伺服器的記憶體中執行，而不是由資料庫完成。 對於傳回大量資料的查詢，這可能會沒有效率。

> [!TIP]
> 
> **IQueryable 與 IEnumerable 的比較**
> 
> 如這裡所示來執行存放庫之後，即使您在**搜尋**方塊中輸入東西，傳送給 SQL Server 的查詢還是會傳回所有學生資料列，因為它不包含您的搜尋條件：
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image2.png)
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample15.sql)]
> 
> 此查詢會傳回所有學生資料，因為存放庫執行查詢時，不會知道搜尋條件。 在 `IEnumerable` 集合上呼叫 `ToPagedList` 方法時，會在記憶體中排序、套用搜尋準則，以及選取要分頁的資料子集（僅顯示3個數據列）。
> 
> 在舊版的程式碼（在您執行存放庫之前）中，如果在 `IQueryable` 物件上呼叫 `ToPagedList`，則查詢不會傳送到資料庫，直到您套用搜尋條件為止。
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image3.png)
> 
> 在 `IQueryable` 物件上呼叫 ToPagedList 時，傳送至 SQL Server 的查詢會指定搜尋字串，因此只會傳回符合搜尋條件的資料列，而且不需要在記憶體中進行任何篩選。
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample16.sql)]
> 
> （下列教學課程說明如何檢查傳送至 SQL Server 的查詢）。

下一節將示範如何執行存放庫方法，讓您指定資料庫應執行此工作。

您現在已在控制器和 Entity Framework 資料庫內容之間建立抽象層。 如果您要使用此應用程式執行自動化單元測試，您可以在單元測試專案中建立替代的儲存機制類別，以進行 `IStudentRepository` *。* 這個模擬儲存機制類別可以操控記憶體內部集合來測試控制器函式，而不是呼叫內容來讀取和寫入資料。

## <a name="implement-a-generic-repository-and-a-unit-of-work-class"></a>執行一般儲存機制和工作單位類別

建立每個實體類型的存放庫類別可能會產生許多多餘的程式碼，而且可能會產生部分更新。 例如，假設您必須更新兩個不同的實體類型，做為相同交易的一部分。 如果每個都使用個別的資料庫內容實例，則可能會成功，另一個則可能失敗。 將多餘的程式碼減到最少的方法之一，就是使用一般存放庫，另一種方法是確保所有儲存機制都使用相同的資料庫內容（因此協調所有更新）是使用工作單位類別。

在本教學課程的這一節中，您將建立 `GenericRepository` 類別和 `UnitOfWork` 類別，並在 `Course` 控制器中使用它們來存取 `Department` 和 `Course` 實體集。 如先前所述，為了讓教學課程的這個部分簡單明瞭，您不會為這些類別建立介面。 但是，如果您要使用它們來加速 TDD，通常會使用與 `Student` 存放庫相同的方式來執行介面。

### <a name="create-a-generic-repository"></a>建立一般存放庫

在*DAL*資料夾中，建立*GenericRepository.cs* ，並將現有的程式碼取代為下列程式碼：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample17.cs)]

類別變數是針對資料庫內容，以及存放庫已具現化之實體集的宣告：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample18.cs)]

此函式會接受資料庫內容實例，並初始化實體集變數：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample19.cs)]

`Get` 方法會使用 lambda 運算式來允許呼叫程式碼指定篩選準則和用來排序結果的資料行，而字串參數可讓呼叫者提供以逗號分隔的導覽屬性清單，以供立即載入：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample20.cs)]

程式碼 `Expression<Func<TEntity, bool>> filter` 表示呼叫端將根據 `TEntity` 型別提供 lambda 運算式，而此運算式會傳回布林值。 例如，如果為 `Student` 實體類型具現化存放庫，則呼叫方法中的程式碼可能會為 `filter` 參數指定 `student => student.LastName == "Smith`&quot;。

程式碼 `Func<IQueryable<TEntity>, IOrderedQueryable<TEntity>> orderBy` 也表示呼叫端會提供 lambda 運算式。 但是在此情況下，運算式的輸入是 `TEntity` 類型的 `IQueryable` 物件。 運算式會傳回該 `IQueryable` 物件的已排序版本。 例如，如果為 `Student` 實體類型具現化存放庫，則呼叫方法中的程式碼可能會指定 `orderBy` 參數的 `q => q.OrderBy(s => s.LastName)`。

`Get` 方法中的程式碼會建立 `IQueryable` 物件，然後套用篩選條件運算式（如果有的話）：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample21.cs)]

接下來，它會在剖析逗號分隔清單之後套用立即載入運算式：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample22.cs)]

最後，它會套用 `orderBy` 運算式（如果有的話），並傳回結果。否則，它會傳回未排序查詢的結果：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample23.cs)]

當您呼叫 `Get` 方法時，您可以對方法所傳回的 `IEnumerable` 集合進行篩選和排序，而不是提供這些函式的參數。 但是排序和篩選工作會在 web 伺服器的記憶體中完成。 藉由使用這些參數，您可以確保工作是由資料庫執行，而不是 web 伺服器。 另一個替代方式是建立特定實體類型的衍生類別，並加入特殊的 `Get` 方法，例如 `GetStudentsInNameOrder` 或 `GetStudentsByName`。 不過，在複雜的應用程式中，這可能會產生大量的這類衍生類別和特殊方法，這可能是更多工具來維護。

`GetByID`、`Insert`和 `Update` 方法中的程式碼，與您在非泛型存放庫中看到的類似。 （您不會在 `GetByID` 簽章中提供積極的載入參數，因為您無法使用 `Find` 方法執行積極式載入）。

`Delete` 的方法會提供兩個多載：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample24.cs)]

其中一個可讓您只傳入要刪除之實體的識別碼，另一個則採用實體實例。 如您在[處理並行](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)處理教學課程中所見，針對並行處理，您需要一個 `Delete` 方法，以使用包含追蹤屬性之原始值的實體實例。

這個一般存放庫會處理一般 CRUD 需求。 當特定實體類型具有特殊需求（例如更複雜的篩選或排序）時，您可以建立具有該類型之其他方法的衍生類別。

## <a name="creating-the-unit-of-work-class"></a>建立工作單位類別

工作單位類別有一個用途：為了確保當您使用多個存放庫時，它們會共用單一資料庫內容。 如此一來，當工作單位完成時，您就可以在該內容實例上呼叫 `SaveChanges` 方法，並確保所有相關的變更都將會協調。 類別所需的全部都是 `Save` 方法和每個存放庫的屬性。 每個存放庫屬性都會傳回已使用與其他存放庫實例相同的資料庫內容實例具現化的存放庫實例。

在*DAL*資料夾中，建立名為*UnitOfWork.cs*的類別檔案，並以下列程式碼取代範本程式碼：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample25.cs)]

此程式碼會建立資料庫內容和每個存放庫的類別變數。 若為 `context` 變數，則會具現化新的內容：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample26.cs)]

每個存放庫屬性都會檢查存放庫是否已經存在。 如果不是，則會具現化存放庫，並傳入內容實例。 因此，所有存放庫都會共用相同的內容實例。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample27.cs)]

`Save` 方法會在資料庫內容上呼叫 `SaveChanges`。

就像在類別變數中具現化資料庫內容的任何類別一樣，`UnitOfWork` 類別會執行 `IDisposable` 並處置內容。

### <a name="changing-the-course-controller-to-use-the-unitofwork-class-and-repositories"></a>變更課程式控制制器以使用 UnitOfWork 類別和存放庫

以下列程式碼取代您目前在*CourseController.cs*中擁有的程式碼：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample28.cs?highlight=15,20,22,31,54-55,70,85-86,101-102,122-124,130)]

此程式碼會新增 `UnitOfWork` 類別的類別變數。 （如果您在這裡使用介面，就不會在這裡初始化變數; 相反地，您會實作為 `Student` 儲存機制的兩個參數模式）。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample29.cs)]

在類別的其餘部分中，資料庫內容的所有參考都會以適當存放庫的參考取代，並使用 `UnitOfWork` 屬性來存取存放庫。 `Dispose` 方法會處置 `UnitOfWork` 實例。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample30.cs)]

執行網站，然後按一下 [**課程**] 索引標籤。

![Courses_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image4.png)

頁面的外觀和運作方式與變更之前相同，而其他課程也相同。

## <a name="summary"></a>總結

您現在已同時執行存放庫和工作單位模式。 您已使用 lambda 運算式做為一般存放庫中的方法參數。 如需如何搭配 `IQueryable` 物件使用這些運算式的詳細資訊，請參閱 MSDN Library 中的[IQueryable （t）介面（system.string）](https://msdn.microsoft.com/library/bb351562.aspx) 。 在下一個教學課程中，您將瞭解如何處理一些先進的案例。

您可以在[ASP.NET 資料存取內容對應](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。

> [!div class="step-by-step"]
> [上一頁](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [下一頁](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
