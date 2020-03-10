---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
title: 具有 Entity Framework 4.0 Database First 和 ASP.NET 4 Web form 的消費者入門-第5部分 |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 來建立 ASP.NET Web Forms 應用程式。 範例應用程式為 。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 24ad4379-3fb2-44dc-ba59-85fe0ffcb2ae
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
msc.type: authoredcontent
ms.openlocfilehash: 75328e67abb4295b619cac5423a9eb970942fff7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78527997"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-5"></a>Entity Framework 4.0 Database First 和 ASP.NET 4 Web form 的消費者入門-第5部分

由[Tom 作者: dykstra](https://github.com/tdykstra)

> Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 4.0 和 Visual Studio 2010 來建立 ASP.NET Web Forms 應用程式。 如需教學課程系列的資訊，請參閱本[系列的第一個教學](the-entity-framework-and-aspnet-getting-started-part-1.md)課程

## <a name="working-with-related-data-continued"></a>繼續使用相關資料

在上一個教學課程中，您開始使用 `EntityDataSource` 控制項來處理相關資料。 您在導覽屬性中顯示了多層級的階層和編輯的資料。 在本教學課程中，您將繼續使用相關的資料，方法是新增和刪除關聯性，以及加入與現有實體具有關聯性的新實體。

您將建立一個頁面，以加入指派給部門的課程。 部門已經存在，而當您建立新的課程時，您將會在這兩者與現有的部門之間建立關聯性。

[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image1.png)

您也會建立一個與多對多關聯性搭配運作的頁面，方法是將講師指派給課程（在您選取的兩個實體之間新增關聯性），或從課程中移除講師（移除您的兩個實體之間的關聯性。選取）。 在資料庫中，在講師和課程之間加入關聯性，會導致新的資料列加入至 `CourseInstructor` 關聯資料表;移除關聯性牽涉到刪除 `CourseInstructor` 關聯資料表中的資料列。 不過，您可以藉由設定導覽屬性在 Entity Framework 中執行此動作，而不需要明確地參考 `CourseInstructor` 資料表。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image3.png)

## <a name="adding-an-entity-with-a-relationship-to-an-existing-entity"></a>將具有關聯性的實體加入至現有實體

建立名為*CoursesAdd*的新網頁，此網頁會使用*網站*的主版頁面，並將下列標記新增至名為 `Content2`的 `Content` 控制項：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample1.aspx)]

此標記會建立一個 `EntityDataSource` 控制項，以選取可進行插入的課程，並指定 `Inserting` 事件的處理常式。 建立新的 `Course` 實體時，您將使用處理程式來更新 `Department` 導覽屬性。

標記也會建立用來加入新 `Course` 實體的 `DetailsView` 控制項。 標記會使用系結欄位來 `Course` 實體屬性。 您必須輸入 `CourseID` 值，因為這不是系統產生的識別碼欄位。 而是課程號碼，必須在課程建立時以手動方式指定。

您可以使用範本欄位做為 `Department` 導覽屬性，因為導覽屬性無法搭配 `BoundField` 控制項使用。 [範本] 欄位提供下拉式清單來選取部門。 因為您無法直接系結導覽屬性來更新它們，所以下拉式清單會使用 `Eval` 而不是 `Bind`，系結至 `Departments` 實體集。 您可以為 `DropDownList` 控制項的 `Init` 事件指定處理常式，以便儲存控制項的參考，供更新 `DepartmentID` 外鍵的程式碼使用。

在*CoursesAdd.aspx.cs*的部分類別宣告之後，新增類別欄位以保存 `DepartmentsDropDownList` 控制項的參考：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample2.cs)]

為 `DepartmentsDropDownList` 控制項的 `Init` 事件新增處理常式，以便儲存控制項的參考。 這可讓您取得使用者已輸入的值，並使用它來更新 `Course` 實體的 `DepartmentID` 值。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample3.cs)]

為 `DetailsView` 控制項的 `Inserting` 事件新增處理常式：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample4.cs)]

當使用者按一下 [`Insert`] 時，`Inserting` 事件會在插入新記錄之前引發。 處理常式中的程式碼會從 `DropDownList` 控制項取得 `DepartmentID`，並使用它來設定將用於 `Course` 實體之 `DepartmentID` 屬性的值。

Entity Framework 會負責將這個課程加入至相關聯 `Department` 實體的 `Courses` 導覽屬性。 它也會將部門新增至 `Course` 實體的 `Department` 導覽屬性。

執行頁面。

[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image5.png)

輸入識別碼、標題、信用額度數，然後選取部門，然後按一下 [**插入**]。

執行 [*課程 .aspx* ] 頁面，然後選取相同的部門以查看新的課程。

[![Image03](the-entity-framework-and-aspnet-getting-started-part-5/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image7.png)

## <a name="working-with-many-to-many-relationships"></a>使用多對多關聯性

`Courses` 實體集和 `People` 實體集之間的關聯性是多對多關聯性。 `Course` 實體具有名為 `People` 的導覽屬性，可包含零個、一個或多個相關的 `Person` 實體（代表指派給教學課程的講師）。 `Person` 實體具有名為 `Courses` 的導覽屬性，其中可包含零個、一個或多個相關的 `Course` 實體（代表講師指派給教授的課程）。 一個講師可能會教授多個課程，而一個課程可能會由多個講師教授。 在本逐步解說的這一節中，您將會藉由更新相關實體的導覽屬性，來新增和移除 `Person` 和 `Course` 實體之間的關聯性。

建立名為*InstructorsCourses*的新網頁，此網頁會使用*網站*的主版頁面，並將下列標記新增至名為 `Content2`的 `Content` 控制項：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample5.aspx)]

此標記會建立一個 `EntityDataSource` 控制項，以抓取講師的 `Person` 機構名稱和 `PersonID`。 `DropDrownList` 控制項系結至 `EntityDataSource` 控制項。 `DropDownList` 控制項會指定 `DataBound` 事件的處理常式。 您將使用此處理程式來 databind 顯示課程的兩個下拉式清單。

標記也會建立下列控制項群組，用來將課程指派給選取的講師：

- `DropDownList` 控制項，用於選取要指派的課程。 此控制項將會填入目前未指派給所選講師的課程。
- 用來起始指派的 `Button` 控制項。
- 當指派失敗時，用來顯示錯誤訊息的 `Label` 控制項。

最後，標記也會建立一組控制項，用來從選取的講師移除課程。

在*InstructorsCourses.aspx.cs*中，新增 using 語句：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample6.cs)]

新增方法來填入顯示課程的兩個下拉式清單：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample7.cs)]

此程式碼會從 `Courses` 實體集取得所有課程，並從所選講師的 `Person` 實體 `Courses` 導覽屬性取得課程。 接著，它會決定要指派給該講師的課程，並據此填入下拉式清單。

為 `Assign` 按鈕的 `Click` 事件新增處理常式：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample8.cs)]

此程式碼會取得所選講師的 `Person` 實體，取得所選課程的 `Course` 實體，並將選取的課程加入至講師 `Person` 實體的 [`Courses` 導覽] 屬性。 然後，它會將變更儲存到資料庫，並重新填入下拉式清單，以便立即看到結果。

為 `Remove` 按鈕的 `Click` 事件新增處理常式：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample9.cs)]

此程式碼會取得所選講師的 `Person` 實體，取得所選課程的 `Course` 實體，並從 `Person` 實體的 `Courses` 導覽屬性中移除選取的課程。 然後，它會將變更儲存到資料庫，並重新填入下拉式清單，以便立即看到結果。

將程式碼加入至 `Page_Load` 方法，以確保在沒有報告錯誤時看不到錯誤訊息，並為講師下拉式清單的 `DataBound` 和 `SelectedIndexChanged` 事件新增處理常式，以填入課程下拉式清單：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample10.cs)]

執行頁面。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image9.png)

選取講師。 [<strong>指派課程</strong>] 下拉式清單會顯示講師未教授的課程，而 [<strong>移除課程</strong>] 下拉式清單會顯示講師已指派給的課程。 在 [<strong>指派課程</strong>] 區段中，選取課程，然後按一下 [<strong>指派</strong>]。 課程移至 [<strong>移除課程</strong>] 下拉式清單。 在 [<strong>移除課程</strong>] 區段中選取課程，然後按一下 [<strong>移除</strong>]<em>。</em> 課程會移至 [<strong>指派課程</strong>] 下拉式清單。

您現在已經看過一些更多方式來處理相關資料。 在下列教學課程中，您將瞭解如何在資料模型中使用繼承，以改善應用程式的可維護性。

> [!div class="step-by-step"]
> [上一頁](the-entity-framework-and-aspnet-getting-started-part-4.md)
> [下一頁](the-entity-framework-and-aspnet-getting-started-part-6.md)
