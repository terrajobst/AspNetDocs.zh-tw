---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 以 ASP.NET MVC 應用程式中的 Entity Framework 更新相關資料（6/10） |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio ... 來建立 ASP.NET MVC 4 應用程式。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 7871dc05-2750-470f-8b4c-3a52511949bc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: d29cb172d642b67947b461d1a7e55d01872bb8c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579818"
---
# <a name="updating-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-6-of-10"></a>以 ASP.NET MVC 應用程式中的 Entity Framework 更新相關資料（6/10）

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載已完成的專案](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。 如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 您可以從一開始就開始本教學課程系列，或[下載本章節的入門專案](building-the-ef5-mvc4-chapter-downloads.md)，並從這裡開始。
> 
> > [!NOTE] 
> > 
> > 如果您遇到無法解決的問題，請[下載完整的章節](building-the-ef5-mvc4-chapter-downloads.md)並嘗試重現您的問題。 您通常可以藉由比較您的程式碼與已完成的程式碼，來找出問題的解決方法。 如需瞭解一些常見錯誤以及如何解決問題，請參閱[錯誤和](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)因應措施。

在上一個教學課程中，您顯示了相關資料;在本教學課程中，您將更新相關的資料。 對於大部分的關聯性，您可以藉由更新適當的外鍵欄位來完成這項作業。 針對多對多關聯性，Entity Framework 不會直接公開聯結資料表，因此您必須明確地在適當的導覽屬性中加入和移除實體。

下列圖例顯示了您將操作的頁面。

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="customize-the-create-and-edit-pages-for-courses"></a>自訂 Courses 的 [建立] 和 [編輯] 頁面

當新的課程實體建立時，其必須要與現有的部門具有關聯性。 若要達成此目的，Scaffold 程式碼包含了控制器方法和 [建立] 和 [編輯] 檢視，當中包含了一個可選取部門的下拉式清單。 下拉式清單會設定 `Course.DepartmentID` 外鍵屬性，而這就是載入具有適當 `Department` 實體之 `Department` 導覽屬性的所有 Entity Framework 需求。 您將使用 Scaffold 程式碼，但會稍微對其進行一些變更以新增錯誤處理及排序下拉式清單。

在*CourseController.cs*中，刪除四個 `Edit` 並 `Create` 方法，並將其取代為下列程式碼：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,10,13-14,21-27,34,41,44-45,52-58,62-68)]

`PopulateDepartmentsDropDownList` 方法會取得依名稱排序的所有部門清單、建立下拉式清單的 `SelectList` 集合，並將集合傳遞至 `ViewBag` 屬性中的 view。 方法接受選擇性的 `selectedDepartment` 參數，可允許呼叫程式碼在呈現下拉式清單時指定選取的項目。 此視圖會將名稱 `DepartmentID` 傳遞給[`DropDownList` helper](../working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md)，而協助專家會知道要在 `ViewBag` 物件中尋找名為 `DepartmentID`的 `SelectList`。

`HttpGet` `Create` 方法會呼叫 `PopulateDepartmentsDropDownList` 方法，而不會設定選取的專案，因為如果是新的課程，則尚未建立部門：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

`HttpGet` `Edit` 方法會根據已指派給所編輯之課程的部門識別碼，來設定選取的專案：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

`Create` 和 `Edit` 的 `HttpPost` 方法也包含程式碼，可在錯誤發生後重新顯示頁面時，設定選取的專案：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

這段程式碼可確保當頁面重新顯示時，如果出現錯誤訊息，則會保留選取的任何部門。

在*Views\Course\Create.cshtml*中，新增反白顯示的程式碼，以在 [**標題**] 欄位之前建立新的課程編號欄位。 如先前的教學課程中所述，預設不會 scaffold 主鍵欄位，但此主鍵有意義，因此您希望使用者能夠輸入索引鍵值。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=17-23)]

在 [ *Views\Course\Edit.cshtml*]、[ *Views\Course\Delete.cshtml*] 和 [ *Views\Course\Details.cshtml*] 中，于 [**標題**] 欄位前面新增 [課程編號] 欄位。 因為它是主要金鑰，所以會顯示，但無法變更。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

執行 [**建立**] 頁面（顯示 [課程索引] 頁面，然後按一下 [**建立新**的]）並輸入新課程的資料：

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

按一下 [建立]。 [課程索引] 頁面隨即顯示，並將新課程加入清單中。 [索引] 頁面中的部門名稱來自於導覽屬性，顯示關聯性已正確建立。

![Course_Index_page_showing_new_course](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

執行 [**編輯**] 頁面（顯示課程 [索引] 頁面，然後按一下 [在課程中**編輯**]）。

![Course_edit_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

變更頁面上的資料，然後按一下 [儲存]。 [課程索引] 頁面隨即顯示，其中包含更新的課程資料。

## <a name="adding-an-edit-page-for-instructors"></a>新增講師的編輯頁面

當您編輯講師記錄時，您可能會想要更新講師的辦公室指派。 `Instructor` 實體與 `OfficeAssignment` 實體具有一對零或一關聯性，這表示您必須處理下列情況：

- 如果使用者清除辦公室指派，而且原先具有值，您就必須移除並刪除 `OfficeAssignment` 實體。
- 如果使用者輸入辦公室指派值，而且原先是空的，您就必須建立新的 `OfficeAssignment` 實體。
- 如果使用者變更辦公室指派的值，您必須變更現有 `OfficeAssignment` 實體中的值。

開啟*InstructorController.cs* ，並查看 `HttpGet` `Edit` 方法：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

此處的 scaffold 程式碼不是您想要的。 它會設定下拉式清單的資料，但您需要的是文字方塊。 以下列程式碼取代此方法：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

此程式碼會卸載 `ViewBag` 語句，並為相關聯的 `OfficeAssignment` 實體新增積極式載入。 您無法使用 `Find` 方法執行積極式載入，因此會改為使用 `Where` 和 `Single` 方法來選取講師。

使用下列程式碼取代 `HttpPost` `Edit` 方法。 處理 office 指派更新的：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

程式碼會執行下列操作：

- 針對 `Instructor` 導覽屬性使用積極式載入從資料庫中取得目前的 `OfficeAssignment` 實體。 這與您在 `HttpGet` `Edit` 方法中的做法相同。
- 使用從模型繫結器取得的值更新擷取的 `Instructor` 實體。 使用的[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx)多載可讓您將想要包含的屬性*列入*允許清單。 這可避免過度張貼，如[第二個教學](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)課程中所述。

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]
- 如果辦公室位置為空白，則會將 `Instructor.OfficeAssignment` 屬性設為 null，以便刪除 `OfficeAssignment` 資料表中的相關資料列。

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]
- 將變更儲存到資料庫。

在 [ *Views\Instructor\Edit.cshtml*] 中，于 [**雇用日期**] 欄位的 `div` 專案之後，新增欄位以編輯辦公室位置：

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml)]

執行頁面（選取 [**講師**] 索引標籤，然後按一下講師上的 [**編輯**]）。 變更 [辦公室位置]，然後按一下 [儲存]。

![Changing_the_office_location](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

## <a name="adding-course-assignments-to-the-instructor-edit-page"></a>將課程指派加入至講師 [編輯] 頁面

講師可教授任何數量的課程。 現在您將藉由使用核取方塊群組，新增變更課程指派的能力來強化 Instructor [編輯] 頁面，如以下螢幕擷取畫面所示：

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

`Course` 和 `Instructor` 實體之間的關聯性是多對多，這表示您沒有聯結資料表的直接存取權。 相反地，您會在 `Instructor.Courses` 導覽屬性中加入和移除實體。

可讓您變更講師指派之課程的 UI 為一組核取方塊。 資料庫中每個課程的核取方塊都會顯示，而該名講師目前受指派的課程會已選取狀態顯示。 使用者可選取或清除核取方塊來變更課程指派。 如果課程數很大，您可能會想要使用不同的方法來呈現視圖中的資料，但是您會使用相同的方法來操作導覽屬性，以便建立或刪除關聯性。

若要針對核取方塊清單提供資料給檢視，您必須使用一個檢視模型類別。 在*viewmodel*資料夾中建立*AssignedCourseData.cs* ，並以下列程式碼取代現有的程式碼：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

在*InstructorController.cs*中，將 `HttpGet` `Edit` 方法取代為下列程式碼。 所做的變更已醒目標示。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=5,8,12-27)]

程式碼會為 `Courses` 導覽屬性新增積極式載入，然後使用 `PopulateAssignedCourseData` 檢視模型類別來呼叫新的 `AssignedCourseData` 方法以提供資訊給核取方塊陣列。

`PopulateAssignedCourseData` 方法中的程式碼會讀取所有 `Course` 實體，以便使用 view model 類別載入課程清單。 針對每個課程，程式碼會檢查課程是否存在於講師的 `Courses` 導覽屬性中。 若要在檢查課程是否指派給講師時建立有效率的查閱，指派給講師的課程會放入[HashSet](https://msdn.microsoft.com/library/bb359438.aspx)集合中。 針對指派講師的課程，`Assigned` 屬性設定為 [`true`]。 檢視會使用這個屬性，來判斷哪一個核取方塊必須顯示為已選取。 最後，會將清單傳遞至 `ViewBag` 屬性中的 view。

接下來，新增當使用者按一下 [儲存] 時要執行的程式碼。 使用下列程式碼來取代 `HttpPost` `Edit` 方法，其會呼叫新的方法來更新 `Instructor` 實體的 `Courses` 導覽屬性。 所做的變更已醒目標示。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs?highlight=3,7,20,33,37-65)]

由於此視圖沒有 `Course` 實體的集合，因此模型系結器無法自動更新 `Courses` 導覽屬性。 您不需要使用模型系結器來更新課程導覽屬性，而是在新的 `UpdateInstructorCourses` 方法中這麼做。 因此您必須從模型繫結器中排除 `Courses` 屬性。 這不需要對呼叫[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx)的程式碼進行任何變更，因為您使用的是*允許清單*多載，而且 `Courses` 不在包含清單中。

如果未選取任何核取方塊，`UpdateInstructorCourses` 中的程式碼會使用空集合初始化 `Courses` 導覽屬性：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

程式碼會執行迴圈，尋訪資料庫中所有的課程，並檢查每個已指派給講師的課程，以及在檢視中選取的課程。 為了協助達成有效率的搜尋，後者的兩個集合會儲存在 `HashSet` 物件中。

若課程的核取方塊已被選取，但課程並未位於 `Instructor.Courses` 導覽屬性中，則課程便會新增至導覽屬性的集合中。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

若課程的核取方塊未被選取，但課程卻位於 `Instructor.Courses` 導覽屬性中，則課程便會從導覽屬性的集合中移除。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

在*Views\Instructor\Edit.cshtml*中，于 [`OfficeAssignment`] 欄位的 `div` 元素後面新增下列反白顯示的程式碼，以新增包含核取方塊陣列的**課程**欄位：

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml?highlight=51-73)]

此程式碼會建立一個 HTML 表格，該表格中有三個資料行。 在每個資料行中，核取方塊的後方會是由課程號碼和標題組成的標題。 所有核取方塊都具有相同的名稱（"selectedCourses"），這會通知模型系結器將其視為群組。 當頁面張貼時，每個核取方塊的 `value` 屬性會設定為 `CourseID.` 的值，而模型系結器只會將陣列傳遞至控制器，其中只包含選取之核取方塊的 `CourseID` 值。

一開始呈現核取方塊時，指派給講師的課程會有 `checked` 的屬性（會將其顯示為已核取）。

變更課程指派之後，您會想要能夠在網站返回 [`Index`] 頁面時，確認變更。 因此，您必須將資料行加入該頁面中的資料表。 在這種情況下，您不需要使用 `ViewBag` 物件，因為您想要顯示的資訊已經在要當做模型傳遞至頁面之 `Instructor` 實體的 `Courses` 導覽屬性中。

在*Views\Instructor\Index.cshtml*中，于**Office**標題後面新增**課程**標題，如下列範例所示：

[!code-html[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html?highlight=7)]

然後緊接在 [office 位置詳細資料] 儲存格後面加入新的 [詳細資料] 資料格：

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=19,50-57)]

執行 [**講師索引**] 頁面，查看指派給每位講師的課程：

![Instructor_index_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

按一下講師上的 [**編輯**] 以查看 [編輯] 頁面。

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

變更一些課程指派，然後按一下 [**儲存**]。 您所做的變更會反映在 [索引] 頁面上。

 注意：在有有限數目的課程時，用來編輯講師課程資料的方法會很有用。 針對更大的集合，將需要不同的 UI 和不同的更新方法。  

## <a name="update-the-delete-method"></a>更新 Delete 方法

變更 HttpPost Delete 方法中的程式碼，以便在刪除講師時刪除 office 指派記錄（如果有的話）：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs?highlight=6,10)]

如果您嘗試刪除以系統管理員身分指派給部門的講師，您會收到參考完整性錯誤。 請參閱[本教學課程的最新版本](../../getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)，以取得其他程式碼，以自動將講師從指派為系統管理員的任何部門中移除。

## <a name="summary"></a>總結

您現在已完成本簡介以使用相關資料。 到目前為止，在這些教學課程中，您已完成完整的 CRUD 作業，但尚未處理並行問題。 下一個教學課程將介紹並行處理的主題、說明用來處理它的選項，以及對您已為一個實體類型撰寫的 CRUD 程式碼新增並行處理。

您可以在[本系列的最後一個教學](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)課程結尾處找到其他 Entity Framework 資源的連結。

> [!div class="step-by-step"]
> [上一頁](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [下一頁](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
