---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
title: 具有 Entity Framework 4.0 Database First 和 ASP.NET 4 Web form 的消費者入門-第4部分 |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 來建立 ASP.NET Web Forms 應用程式。 範例應用程式為 。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: ceb9e60f-957c-4d25-9331-cc527de96a33
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
msc.type: authoredcontent
ms.openlocfilehash: eb75a76038466bf30738387ed4739687de1df944
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638163"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-4"></a>Entity Framework 4.0 Database First 和 ASP.NET 4 Web form 的消費者入門-第4部分

由[Tom 作者: dykstra](https://github.com/tdykstra)

> Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 4.0 和 Visual Studio 2010 來建立 ASP.NET Web Forms 應用程式。 如需教學課程系列的資訊，請參閱本[系列的第一個教學](the-entity-framework-and-aspnet-getting-started-part-1.md)課程

## <a name="working-with-related-data"></a>使用相關資料

在上一個教學課程中，您使用了 `EntityDataSource` 控制項來篩選、排序和分組資料。 在本教學課程中，您將會顯示及更新相關資料。

您將建立顯示講師清單的講師頁面。 當您選取講師時，您會看到該講師所教授的課程清單。 當您選取課程時，您會看到課程的詳細資料，以及在課程中註冊的學生清單。 您可以編輯講師姓名、雇用日期和辦公室指派。 Office 指派是您透過導覽屬性存取的個別實體集。

您可以將主要資料連結至標記或程式碼中的詳細資料。 在本教學課程的這個部分中，您將使用這兩種方法。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-4/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image1.png)

## <a name="displaying-and-updating-related-entities-in-a-gridview-control"></a>顯示和更新 GridView 控制項中的相關實體

建立名為*default.aspx*的新網頁，此網頁會使用*網站*主要頁面，並將下列標記新增至名為 `Content2`的 `Content` 控制項：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample1.aspx)]

此標記會建立一個 `EntityDataSource` 控制項，以選取講師並啟用更新。 `div` 元素會將標記設定為在左側轉譯，讓您稍後可以在右側新增資料行。

在 `EntityDataSource` 標記和結尾 `</div>` 標記之間，新增下列標記，以建立您將用於錯誤訊息的 `GridView` 控制項和 `Label` 控制項：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample2.aspx)]

此 `GridView` 控制項可讓您選取資料列、以淺灰色背景色彩反白顯示選取的資料列，並指定 `SelectedIndexChanged` 和 `Updating` 事件的處理常式（您稍後會建立）。 它也會指定 `DataKeyNames` 屬性的 `PersonID`，讓選取之資料列的索引鍵值可以傳遞至您稍後將新增的另一個控制項。

最後一個資料行包含講師的辦公室指派，其儲存在 `Person` 實體的導覽屬性中，因為它來自相關聯的實體。 請注意，`EditItemTemplate` 元素會指定 `Eval` 而不是 `Bind`，因為 `GridView` 控制項無法直接系結至導覽屬性，以便更新它們。 您將會在程式碼中更新辦公室指派。 若要這麼做，您需要 `TextBox` 控制項的參考，然後在 `TextBox` 控制項的 `Init` 事件中取得並儲存該專案。

遵循 `GridView` 控制項是用於錯誤訊息的 `Label` 控制項。 控制項的 `Visible` 屬性為 `false`，而 view 狀態為 off，只有在程式碼讓標籤顯示為回應錯誤時才會出現。

開啟*Instructors.aspx.cs*檔案，並新增下列 `using` 語句：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample3.cs)]

緊接在部分類別名稱宣告之後加入私用類別欄位，以保存 [office 指派] 文字方塊的參考。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample4.cs)]

為您稍後要加入程式碼的 `SelectedIndexChanged` 事件處理常式新增 stub。 此外，也請加入 office 指派 `TextBox` 控制項的 `Init` 事件的處理常式，讓您可以儲存 `TextBox` 控制項的參考。 您將使用此參考來取得使用者輸入的值，以便更新與導覽屬性相關聯的實體。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample5.cs)]

您將使用 `GridView` 控制項的 `Updating` 事件來更新相關聯 `OfficeAssignment` 實體的 `Location` 屬性。 為 `Updating` 事件新增下列處理常式：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample6.cs)]

這段程式碼會在使用者按一下 `GridView` 資料列中的 [**更新**] 時執行。 程式碼會使用 LINQ to Entities，以從事件引數中選取的資料列 `PersonID`，抓取與目前 `Person` 實體相關聯的 `OfficeAssignment` 實體。

然後，程式碼會根據 `InstructorOfficeTextBox` 控制項中的值，採取下列其中一個動作：

- 如果文字方塊具有值，而且沒有要更新的 `OfficeAssignment` 實體，則會建立一個。
- 如果文字方塊具有值，而且有 `OfficeAssignment` 實體，則會更新 `Location` 屬性值。
- 如果文字方塊是空的，且 `OfficeAssignment` 實體存在，則會刪除實體。

之後，它會將變更儲存至資料庫。 如果發生例外狀況，則會顯示錯誤訊息。

執行頁面。

[![Image02](the-entity-framework-and-aspnet-getting-started-part-4/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image3.png)

按一下 [**編輯**]，所有欄位都會變更為文字方塊。

[![Image03](the-entity-framework-and-aspnet-getting-started-part-4/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image5.png)

變更其中任何值，包括**辦公室指派**。 按一下 [**更新**]，您就會看到這些變更反映在清單中。

## <a name="displaying-related-entities-in-a-separate-control"></a>在不同的控制項中顯示相關實體

每位講師都可以教授一或多個課程，因此您將新增一個 `EntityDataSource` 控制項和一個 `GridView` 控制項，以列出與講師 `GridView` 控制項中所選講師相關聯的課程。 若要建立課程實體的標題和 `EntityDataSource` 控制項，請在錯誤訊息 `Label` 控制項和結尾 `</div>` 標記之間新增下列標記：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample7.aspx)]

`Where` 參數包含在 `InstructorsGridView` 控制項中選取資料列之講師的 `PersonID` 值。 `Where` 屬性包含子選擇命令，可從 `Course` 實體的 `People` 導覽屬性取得所有關聯的 `Person` 實體，只有在其中一個相關聯的 `Course` 實體包含選取的 `Person` 值時，才會選取 `PersonID` 實體。

若要建立 `GridView` 控制項，請在 `CoursesEntityDataSource` 控制項後面緊接著新增下列標記（在結尾 `</div>` 標記之前）：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample8.aspx)]

因為若未選取任何講師，將不會顯示任何課程，則會包含 `EmptyDataTemplate` 元素。

執行頁面。

[![Image04](the-entity-framework-and-aspnet-getting-started-part-4/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image7.png)

選取已指派一或多個課程的講師，而課程或課程則會出現在清單中。 （注意：雖然資料庫架構允許多個課程，但在資料庫提供的測試資料中，沒有任何講師實際有一個以上的課程。 您可以使用 [**伺服器總管**] 視窗或 [ *CoursesAdd* ] 頁面（您將在稍後的教學課程中加入），自行將課程新增至資料庫。

[![Image05](the-entity-framework-and-aspnet-getting-started-part-4/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image9.png)

`CoursesGridView` 控制項只會顯示一些課程欄位。 若要顯示課程的所有詳細資料，您將會在使用者選取的課程中使用 `DetailsView` 控制項。 在*default.aspx*中，于結尾 `</div>` 標籤後面新增下列標記（請確定您將此標記放在結尾 div 標記**之後**，而不是在它之前）：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample9.aspx)]

此標記會建立系結至 `Courses` 實體集的 `EntityDataSource` 控制項。 `Where` 屬性會使用課程 `GridView` 控制項中所選取資料列的 `CourseID` 值來選取課程。 標記會指定 `Selected` 事件的處理常式，稍後您會用來顯示學生成績，也就是階層中較低的另一個層級。

在*Instructors.aspx.cs*中，為 `CourseDetailsEntityDataSource_Selected` 方法建立下列 stub。 （您稍後會在本教學課程中填入此存根; 現在，您需要它，才能編譯和執行頁面。）

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample10.cs)]

執行頁面。

[![Image06](the-entity-framework-and-aspnet-getting-started-part-4/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image11.png)

一開始沒有任何課程詳細資料，因為沒有選取任何課程。 選取已指派課程的講師，然後選取課程以查看詳細資料。

[![Image07](the-entity-framework-and-aspnet-getting-started-part-4/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image13.png)

## <a name="using-the-entitydatasource-selected-event-to-display-related-data"></a>使用 EntityDataSource 的「選取」事件來顯示相關資料

最後，您想要顯示所選課程的所有已註冊學生和其成績。 若要這麼做，您將使用系結至課程 `DetailsView`之 `EntityDataSource` 控制項的 `Selected` 事件。

在*default.aspx*中，于 `DetailsView` 控制項之後加入下列標記：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample11.aspx)]

此標記會建立一個 `ListView` 控制項，其中顯示所選課程的學生清單及其成績。 沒有指定資料來源，因為您會在程式碼中將控制項進行 databind。 [`EmptyDataTemplate`] 元素會提供在未選取任何課程時顯示的訊息，在此情況下，沒有任何學生可顯示。 `LayoutTemplate` 元素會建立一個 HTML 資料表來顯示清單，而 `ItemTemplate` 則指定要顯示的資料行。 學生識別碼和學生的成績來自 `StudentGrade` 實體，而 student 名稱則來自 Entity Framework 在 `StudentGrade` 實體的 `Person` 導覽屬性中提供的 `Person` 實體。

在*Instructors.aspx.cs*中，以下列程式碼取代 stub 時 `CourseDetailsEntityDataSource_Selected` 方法：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample12.cs)]

這個事件的事件引數會以集合的形式提供選取的資料，如果未選取任何專案，則會有零個專案，如果選取了 `Course` 的實體，則會有一個專案。 如果選取了 `Course` 的實體，程式碼會使用 `First` 方法，將集合轉換成單一物件。 然後，它會從導覽屬性取得 `StudentGrade` 的實體、將其轉換成集合，並將 `GradesListView` 控制項系結至集合。

這就足以顯示成績，但是您想要確定在第一次顯示頁面時，以及每次未選取課程時，都會顯示空白資料範本中的訊息。 若要這麼做，請建立下列方法，這會從兩個位置呼叫：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample13.cs)]

從 `Page_Load` 方法呼叫這個新方法，以在第一次顯示頁面時顯示空白資料範本。 然後從 `InstructorsGridView_SelectedIndexChanged` 方法呼叫它，因為當選取講師時，就會引發該事件，這表示新課程會載入課程 `GridView` 控制項，而且尚未選取任何專案。 以下是兩個呼叫：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample14.cs)]

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample15.cs)]

執行頁面。

[![Image08](the-entity-framework-and-aspnet-getting-started-part-4/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image15.png)

選取已指派課程的講師，然後選取課程。

[![Image09](the-entity-framework-and-aspnet-getting-started-part-4/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image17.png)

您現在已經看過一些使用相關資料的方式。 在下列教學課程中，您將瞭解如何加入現有實體之間的關聯性、如何移除關聯性，以及如何加入與現有實體具有關聯性的新實體。

> [!div class="step-by-step"]
> [上一頁](the-entity-framework-and-aspnet-getting-started-part-3.md)
> [下一頁](the-entity-framework-and-aspnet-getting-started-part-5.md)
