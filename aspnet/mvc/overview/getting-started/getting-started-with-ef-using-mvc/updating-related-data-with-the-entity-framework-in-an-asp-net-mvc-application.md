---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教學課程：在 ASP.NET MVC 應用程式中使用 EF 更新相關資料
description: 在本教學課程中，您將更新相關的資料。 對於大部分的關聯性，您可以藉由更新外鍵欄位或導覽屬性來完成這項作業。
author: tdykstra
ms.author: riande
ms.date: 01/19/2019
ms.topic: tutorial
ms.assetid: 7ba88418-5d0a-437d-b6dc-7c3816d4ec07
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 4d5f6447fdccefdcdf9497a9e94f23243302a0e1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616001"
---
# <a name="tutorial-update-related-data-with-ef-in-an-aspnet-mvc-app"></a>教學課程：在 ASP.NET MVC 應用程式中使用 EF 更新相關資料

在上一個教學課程中，您顯示了相關資料。 在本教學課程中，您將更新相關的資料。 對於大部分的關聯性，您可以藉由更新外鍵欄位或導覽屬性來完成這項作業。 針對多對多關聯性，Entity Framework 不會直接公開聯結資料表，因此您可以在適當的導覽屬性中新增和移除實體。

下列圖例顯示了您將操作的一些頁面。

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

![講師編輯課程](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

在本教學課程中，您已：

> [!div class="checklist"]
> * 自訂課程頁面
> * 將 office 新增到講師頁面
> * 將課程新增至講師頁面
> * 更新 DeleteConfirmed
> * 將辦公室位置和課程新增至 [新增] 頁面

## <a name="prerequisites"></a>Prerequisites

* [讀取相關資料](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="customize-courses-pages"></a>自訂課程頁面

當新的課程實體建立時，其必須要與現有的部門具有關聯性。 若要達成此目的，Scaffold 程式碼包含了控制器方法和 [建立] 和 [編輯] 檢視，當中包含了一個可選取部門的下拉式清單。 下拉式清單會設定 `Course.DepartmentID` 外鍵屬性，而這就是載入具有適當 `Department` 實體之 `Department` 導覽屬性的所有 Entity Framework 需求。 您將使用 Scaffold 程式碼，但會稍微對其進行一些變更以新增錯誤處理及排序下拉式清單。

在*CourseController.cs*中，刪除四個 `Create` 並 `Edit` 方法，並將其取代為下列程式碼：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,11-12,19-25,40,44,46,48-78)]

在檔案的開頭新增下列 `using` 語句：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

`PopulateDepartmentsDropDownList` 方法會取得依名稱排序的所有部門清單、建立下拉式清單的 `SelectList` 集合，並將集合傳遞至 `ViewBag` 屬性中的 view。 方法接受選擇性的 `selectedDepartment` 參數，可允許呼叫程式碼在呈現下拉式清單時指定選取的項目。 此視圖會將名稱 `DepartmentID` 傳遞給[DropDownList](../../older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md) helper，而協助專家會知道要在 `ViewBag` 物件中尋找名為 `DepartmentID`的 `SelectList`。

`HttpGet` `Create` 方法會呼叫 `PopulateDepartmentsDropDownList` 方法，而不會設定選取的專案，因為如果是新的課程，則尚未建立部門：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

`HttpGet` `Edit` 方法會根據已指派給所編輯之課程的部門識別碼，來設定選取的專案：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=12)]

`Create` 和 `Edit` 的 `HttpPost` 方法也包含程式碼，可在錯誤發生後重新顯示頁面時，設定選取的專案：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=6)]

這段程式碼可確保當頁面重新顯示時，如果出現錯誤訊息，則會保留選取的任何部門。

課程視圖已 scaffold [部門] 欄位的下拉式清單，但您不想要此欄位的 [DepartmentID] 標題，因此請將下列反白顯示的*Views\Course\Create.cshtml*檔案變更變更為 [標題]。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml?highlight=43)]

在*Views\Course\Edit.cshtml*中進行相同的變更。

一般來說，scaffolder 不會 scaffold 主鍵，因為索引鍵值是由資料庫所產生，而且無法變更，而且不是對使用者顯示有意義的值。 針對「課程」實體，scaffolder 的確包含 `CourseID` 欄位的文字方塊，因為它瞭解 `DatabaseGeneratedOption.None` 屬性工作表示使用者應該能夠輸入主要金鑰值。 但它並不瞭解，因為數位有意義，您想要在其他視圖中看到它，因此您需要手動新增。

在*Views\Course\Edit.cshtml*中，于 [**標題**] 欄位前面新增 [課程編號] 欄位。 因為它是主要金鑰，所以會顯示，但無法變更。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cshtml)]

[編輯] 視圖中的課程編號已經有一個隱藏欄位（`Html.HiddenFor` helper）。 新增 Html 時， *LabelFor* helper 並不會免除隱藏欄位的需求，因為它不會在使用者按一下 [編輯] 頁面上的 [**儲存**] 時，讓課程號碼包含在張貼的資料中。

在*Views\Course\Delete.cshtml*和*Views\Course\Details.cshtml*中，將部門名稱標題從「名稱」變更為「部門」，然後在 [**標題**] 欄位前面新增 [課程編號] 欄位。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cshtml?highlight=2,9-15)]

執行 [**建立**] 頁面（顯示 [課程索引] 頁面，然後按一下 [**建立新**的]）並輸入新課程的資料：

| 值 | 設定 |
| ----- | ------- |
| 數字 | 輸入*1000*。 |
| 標題 | 輸入*代數*。 |
| 學分 | 輸入*4*。 |
|部門 | 選取 [**數學**]。 |

按一下 [建立]。 [課程索引] 頁面隨即顯示，並將新課程加入清單中。 [索引] 頁面中的部門名稱來自於導覽屬性，顯示關聯性已正確建立。

執行 [**編輯**] 頁面（顯示課程 [索引] 頁面，然後按一下 [在課程中**編輯**]）。

變更頁面上的資料，然後按一下 [儲存]。 [課程索引] 頁面隨即顯示，其中包含更新的課程資料。

## <a name="add-office-to-instructors-page"></a>將 office 新增到講師頁面

當您編輯講師記錄時，您可能會想要更新講師的辦公室指派。 `Instructor` 實體與 `OfficeAssignment` 實體具有一對零或一關聯性，這表示您必須處理下列情況：

- 如果使用者清除辦公室指派，而且原先具有值，您就必須移除並刪除 `OfficeAssignment` 實體。
- 如果使用者輸入辦公室指派值，而且原先是空的，您就必須建立新的 `OfficeAssignment` 實體。
- 如果使用者變更辦公室指派的值，您必須變更現有 `OfficeAssignment` 實體中的值。

開啟*InstructorController.cs* ，並查看 `HttpGet` `Edit` 方法：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

此處的 scaffold 程式碼不是您想要的。 它會設定下拉式清單的資料，但您需要的是文字方塊。 以下列程式碼取代此方法：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs?highlight=7-10)]

此程式碼會卸載 `ViewBag` 語句，並為相關聯的 `OfficeAssignment` 實體新增積極式載入。 您無法使用 `Find` 方法執行積極式載入，因此會改為使用 `Where` 和 `Single` 方法來選取講師。

使用下列程式碼取代 `HttpPost` `Edit` 方法。 處理 office 指派更新的：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

`RetryLimitExceededException` 的參考需要 `using` 語句;若要新增它，請將滑鼠停留在 `RetryLimitExceededException`。 此時會出現下列訊息： ![ 重試例外狀況訊息](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)

選取 [**顯示可能的修正**]，然後**使用 [system.object** ]。

![解決重試例外狀況](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)

程式碼會執行下列操作：

- 將方法名稱變更為 `EditPost`，因為簽章現在與 `HttpGet` 方法相同（`ActionName` 屬性指定/Edit/URL 仍在使用中）。
- 針對 `Instructor` 導覽屬性使用積極式載入從資料庫中取得目前的 `OfficeAssignment` 實體。 這與您在 `HttpGet` `Edit` 方法中的做法相同。
- 使用從模型繫結器取得的值更新擷取的 `Instructor` 實體。 使用的[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx)多載可讓您將想要包含的屬性*列入*允許清單。 這可避免過度張貼，如[第二個教學](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)課程中所述。

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]
- 如果辦公室位置為空白，則會將 `Instructor.OfficeAssignment` 屬性設為 null，以便刪除 `OfficeAssignment` 資料表中的相關資料列。

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]
- 將變更儲存到資料庫。

在 [ *Views\Instructor\Edit.cshtml*] 中，于 [**雇用日期**] 欄位的 `div` 專案之後，新增欄位以編輯辦公室位置：

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml)]

執行頁面（選取 [**講師**] 索引標籤，然後按一下講師上的 [**編輯**]）。 變更 [辦公室位置]，然後按一下 [儲存]。

## <a name="add-courses-to-instructors-page"></a>將課程新增至講師頁面

講師可教授任何數量的課程。 現在您將藉由新增使用一組核取方塊來變更課程指派的功能，來增強講師 [編輯] 頁面。

`Course` 和 `Instructor` 實體之間的關聯性是多對多，這表示您無法直接存取聯結資料表中的外鍵屬性。 相反地，您可以在 `Instructor.Courses` 導覽屬性中新增和移除實體。

可讓您變更講師指派之課程的 UI 為一組核取方塊。 資料庫中每個課程的核取方塊都會顯示，而該名講師目前受指派的課程會已選取狀態顯示。 使用者可選取或清除核取方塊來變更課程指派。 如果課程數很大，您可能會想要使用不同的方法來呈現視圖中的資料，但是您會使用相同的方法來操作導覽屬性，以便建立或刪除關聯性。

若要針對核取方塊清單提供資料給檢視，您必須使用一個檢視模型類別。 在*viewmodel*資料夾中建立*AssignedCourseData.cs* ，並以下列程式碼取代現有的程式碼：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

在*InstructorController.cs*中，將 `HttpGet` `Edit` 方法取代為下列程式碼。 所做的變更已醒目標示。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs?highlight=9,12,20-35)]

程式碼會為 `Courses` 導覽屬性新增積極式載入，然後使用 `PopulateAssignedCourseData` 檢視模型類別來呼叫新的 `AssignedCourseData` 方法以提供資訊給核取方塊陣列。

`PopulateAssignedCourseData` 方法中的程式碼會讀取所有 `Course` 實體，以便使用 view model 類別載入課程清單。 針對每個課程，程式碼會檢查課程是否存在於講師的 `Courses` 導覽屬性中。 若要在檢查課程是否指派給講師時建立有效率的查閱，指派給講師的課程會放入[HashSet](https://msdn.microsoft.com/library/bb359438.aspx)集合中。 針對指派講師的課程，`Assigned` 屬性設定為 [`true`]。 檢視會使用這個屬性，來判斷哪一個核取方塊必須顯示為已選取。 最後，會將清單傳遞至 `ViewBag` 屬性中的 view。

接下來，新增當使用者按一下 [儲存] 時要執行的程式碼。 以下列程式碼取代 `EditPost` 方法，其會呼叫新的方法來更新 `Instructor` 實體的 `Courses` 導覽屬性。 所做的變更已醒目標示。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs?highlight=3,11,25,37,40-68)]

方法簽章現在與 `HttpGet` `Edit` 方法不同，因此方法名稱會從 `EditPost` 變更為 `Edit`。

由於此視圖沒有 `Course` 實體的集合，因此模型系結器無法自動更新 `Courses` 導覽屬性。 您不需要使用模型系結器來更新 `Courses` 導覽屬性，而是在新的 `UpdateInstructorCourses` 方法中這麼做。 因此您必須從模型繫結器中排除 `Courses` 屬性。 這不需要對呼叫[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx)的程式碼進行任何變更，因為您使用的是*允許清單*多載，而且 `Courses` 不在包含清單中。

如果未選取任何核取方塊，`UpdateInstructorCourses` 中的程式碼會使用空集合初始化 `Courses` 導覽屬性：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

程式碼會執行迴圈，尋訪資料庫中所有的課程，並檢查每個已指派給講師的課程，以及在檢視中選取的課程。 為了協助達成有效率的搜尋，後者的兩個集合會儲存在 `HashSet` 物件中。

若課程的核取方塊已被選取，但課程並未位於 `Instructor.Courses` 導覽屬性中，則課程便會新增至導覽屬性的集合中。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

若課程的核取方塊未被選取，但課程卻位於 `Instructor.Courses` 導覽屬性中，則課程便會從導覽屬性的集合中移除。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

在*Views\Instructor\Edit.cshtml*中，新增包含核取方塊陣列的**課程**欄位，方法是在 [`OfficeAssignment`] 欄位的 `div` 元素之後，以及 [**儲存**] 按鈕的 [`div`] 元素之前，新增下列程式碼：

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml)]

貼上程式碼之後，如果分行符號和縮排看起來不像在這裡執行，請手動修正所有內容，使其看起來像這裡所示。 縮排不一定要是完美的，但 `@</tr><tr>`、`@:<td>`、`@:</td>` 和 `@</tr>` 必須要如顯示般各自在獨立的一行上，否則您會接收到執行階段錯誤。

此程式碼會建立一個 HTML 表格，該表格中有三個資料行。 在每個資料行中，核取方塊的後方會是由課程號碼和標題組成的標題。 所有核取方塊都具有相同的名稱（"selectedCourses"），這會通知模型系結器將其視為群組。 當頁面張貼時，每個核取方塊的 `value` 屬性會設定為 `CourseID.` 的值，而模型系結器只會將陣列傳遞至控制器，其中只包含選取之核取方塊的 `CourseID` 值。

一開始呈現核取方塊時，指派給講師的課程會有 `checked` 的屬性（會將其顯示為已核取）。

變更課程指派之後，您會想要能夠在網站返回 [`Index`] 頁面時，確認變更。 因此，您必須將資料行加入該頁面中的資料表。 在這種情況下，您不需要使用 `ViewBag` 物件，因為您想要顯示的資訊已經在要當做模型傳遞至頁面之 `Instructor` 實體的 `Courses` 導覽屬性中。

在*Views\Instructor\Index.cshtml*中，于**Office**標題後面新增**課程**標題，如下列範例所示：

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml?highlight=6)]

然後緊接在 [office 位置詳細資料] 儲存格後面加入新的 [詳細資料] 資料格：

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml?highlight=7-14)]

執行 [**講師索引**] 頁面，查看指派給每位講師的課程。

按一下講師上的 [**編輯**] 以查看 [編輯] 頁面。

變更一些課程指派，然後按一下 [**儲存**]。 您所做的變更會反映在 [索引] 頁面上。

 注意：在這裡用來編輯講師課程資料的方法，在有數量有限的課程時也能正常運作。 針對更大的集合，將需要不同的 UI 和不同的更新方法。

## <a name="update-deleteconfirmed"></a>更新 DeleteConfirmed

在*InstructorController.cs*中，刪除 `DeleteConfirmed` 方法，並在其位置插入下列程式碼。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=5-8,12-18)]

此程式碼會進行下列變更：

- 如果將講師指派為任何部門的系統管理員，則會移除該部門的講師指派。 如果沒有這段程式碼，當您嘗試刪除指派為部門系統管理員的講師時，就會出現參考完整性錯誤。

這段程式碼不會處理一個講師指派為多個部門之系統管理員的案例。 在上一個教學課程中，您將新增程式碼，以防止發生該情況。

## <a name="add-office-location-and-courses-to-the-create-page"></a>將辦公室位置和課程新增至 [新增] 頁面

在*InstructorController.cs*中，刪除 `HttpGet` 並 `HttpPost` `Create` 方法，然後在其位置新增下列程式碼：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

這段程式碼類似于您在編輯方法中看到的內容，不同之處在于一開始不會選取任何課程。 `HttpGet` `Create` 方法不會呼叫 `PopulateAssignedCourseData` 方法，因為可能會有選取的課程，但為了在視圖中提供 `foreach` 迴圈的空集合（否則，view 程式碼會擲回 null 參考例外狀況）。

HttpPost Create 方法會在檢查驗證錯誤的範本程式碼之前，將每個選取的課程新增至課程導覽屬性，並將新的講師加入至資料庫。 即使發生模型錯誤，也會新增課程，以便在發生模型錯誤時（例如，使用者輸入不正確日期），因此當頁面重新顯示時，若出現錯誤訊息，則會自動還原已進行的任何課程選擇。

請注意，為了要能夠將課程新增到 `Courses` 導覽屬性，您必須將屬性以空集合初始化：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

作為在控制器程式碼中完成這項操作的替代方案，您可以在 Instructor 模型中藉由將屬性 getter 變更為在不存在時自動建立集合來完成，如以下範例所示：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample27.cs)]

若您使用這種方式修改了 `Courses` 屬性，您便可以移除控制器中的明確屬性初始化程式碼。

在*Views\Instructor\Create.cshtml*中，于 [雇用日期] 欄位之後和 [**提交**] 按鈕之前，新增 [辦公室位置] 文字方塊和課程核取方塊。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample28.cshtml)]

在您貼上程式碼之後，請修正分行符號和縮排，如同您先前針對 [編輯] 頁面所執行的步驟。

執行 [建立] 頁面並加入講師。

<a id="transactions"></a>

## <a name="handling-transactions"></a>處理交易

如[基本 CRUD 功能教學](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)課程中所述，根據預設，Entity Framework 會隱含地執行交易。 針對您需要更多控制的案例--例如，如果您想要包含在交易中于 Entity Framework 外部完成的作業，請參閱 MSDN 上的[使用交易](https://msdn.microsoft.com/data/dn456843)。

## <a name="get-the-code"></a>取得程式碼

[下載已完成的專案](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>其他資源

您可以在[ASP.NET 資料存取-建議的資源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。

## <a name="next-step"></a>後續步驟

在本教學課程中，您已：

> [!div class="checklist"]
> * 自訂課程頁面
> * 已將 office 新增至講師頁面
> * 已將課程新增到講師頁面
> * 已更新 DeleteConfirmed
> * 將辦公室位置和課程新增至 [建立] 頁面

請前進到下一篇文章，以瞭解如何執行非同步程式設計模型。
> [!div class="nextstepaction"]
> [非同步程式設計模型](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)
