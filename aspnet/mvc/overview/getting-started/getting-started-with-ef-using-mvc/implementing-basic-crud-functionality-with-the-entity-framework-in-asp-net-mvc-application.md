---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
title: 教學課程：使用 ASP.NET MVC 中的 Entity Framework 來執行 CRUD 功能 |Microsoft Docs
description: 檢查及自訂 MVC 架構在控制器和 views 中自動建立的建立、讀取、更新、刪除（CRUD）程式碼。
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: a2f70ba4-83d1-4002-9255-24732726c4f2
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9ed388543dd54d209ff2a0b92df4f7659962582c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583157"
---
# <a name="tutorial-implement-crud-functionality-with-the-entity-framework-in-aspnet-mvc"></a>教學課程：使用 ASP.NET MVC 中的 Entity Framework 來執行 CRUD 功能

在[上一個教學](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)課程中，您建立了一個 MVC 應用程式，它會使用 ENTITY FRAMEWORK （EF）6和 SQL Server LocalDB 來儲存和顯示資料。 在本教學課程中，您會檢查和自訂 MVC 架構在控制器和 views 中為您自動建立的建立、讀取、更新、刪除（CRUD）程式碼。

> [!NOTE]
> 實作儲存機制模式，以在您的控制器及資料存取層之間建立抽象層是一種非常常見的做法。 為了讓這些教學課程保持簡單且專注于教學如何使用 EF 6，它們不會使用存放庫。 如需如何執行存放庫的資訊，請參閱[ASP.NET 資料存取內容地圖](../../../../whitepapers/aspnet-data-access-content-map.md)。

以下是您所建立網頁的範例：

![[學生詳細資料] 頁面的螢幕擷取畫面。](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image1.png)

![學生 [建立] 頁面的螢幕擷取畫面。](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image2.png)

![學生的 [刪除] 頁面的螢幕擷取畫面。](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image3.png)

在本教學課程中，您已：

> [!div class="checklist"]
> * 建立詳細資料頁面
> * 更新 [建立] 頁面
> * 更新 HttpPost Edit 方法
> * 更新 [刪除] 頁面
> * 關閉資料庫連線
> * 處理交易

## <a name="prerequisites"></a>Prerequisites

* [建立 Entity Framework 資料模型](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)

## <a name="create-a-details-page"></a>建立詳細資料頁面

學生 `Index` 頁面的 scaffold 程式碼會省略 `Enrollments` 屬性，因為該屬性會保存一個集合。 在 [`Details`] 頁面中，您會在 HTML 資料表中顯示集合的內容。

在*Controllers\StudentController.cs*中，`Details` 視圖的動作方法會使用[Find](https://msdn.microsoft.com/library/gg696418(v=VS.103).aspx)方法來取出單一 `Student` 實體。

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample1.cs)]

金鑰值會當做 `id` 參數傳遞至方法，並來自 [索引] 頁面上 [**詳細**資料] 超連結中的*路由資料*。

### <a name="tip-route-data"></a>提示：**路由資料**

路由資料是模型系結器在路由表中指定的 URL 區段中找到的資料。 例如，預設路由會指定 `controller`、`action`和 `id` 區段：

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample2.cs?highlight=3)]

在下列 URL 中，預設路由會將 `Instructor` 為 `controller`，`Index` 做為 `action`，1則做為 `id`;這些是路由資料值。

`http://localhost:1230/Instructor/Index/1?courseID=2021`

`?courseID=2021` 是查詢字串值。 如果您傳遞 `id` 做為查詢字串值，模型系結器也可以使用：

`http://localhost:1230/Instructor/Index?id=1&CourseID=2021`

這些 Url 是由 Razor 視圖中的 `ActionLink` 語句所建立。 在下列程式碼中，`id` 參數符合預設路由，因此 `id` 會加入至路由資料。

[!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample3.cshtml)]

在下列程式碼中，`courseID` 不符合預設路由中的參數，因此會將它新增為查詢字串。

[!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample4.cshtml)]

### <a name="to-create-the-details-page"></a>若要建立詳細資料頁面

1. 開啟*Views\Student\Details.cshtml*。

   每個欄位都會使用 `DisplayFor` helper 來顯示，如下列範例所示：

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample5.cshtml)]

2. 在 [`EnrollmentDate`] 欄位之後，以及緊接在結尾 `</dl>` 標記之前，新增反白顯示的程式碼以顯示註冊清單，如下列範例所示：

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample6.cshtml?highlight=8-29)]

    當您貼上程式碼之後，如果代碼縮排錯誤，請按**ctrl**+**K**， **ctrl**+**D**來格式化它。

    此程式碼會以迴圈逐一巡覽 `Enrollments` 導覽屬性中的實體。 針對屬性中的每個 `Enrollment` 實體，它會顯示課程標題和等級。 課程標題會從儲存在 `Enrollments` 實體之 `Course` 導覽屬性中的 `Course` 實體中抓取。 這項資料會在需要時自動從資料庫中取出。 換句話說，您在這裡使用的是消極式載入。 您未指定 `Courses` 導覽屬性的*積極式載入*，因此不會在獲得學生的相同查詢中抓取註冊。 相反地，當您第一次嘗試存取 `Enrollments` 導覽屬性時，會將新的查詢傳送至資料庫，以取得資料。 您可以在本系列稍後的[閱讀相關資料](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)教學課程中深入瞭解消極式載入和積極式載入。

3. 啟動程式（**Ctrl**+**F5**），選取 [**學生**] 索引標籤，然後按一下 [Alexander Carson] 的 [**詳細資料**] 連結，以開啟 [詳細資料] 頁面。 （如果您按**Ctrl**+**F5** ，而*Details*檔案已開啟，則會收到 HTTP 400 錯誤。 這是因為 Visual Studio 嘗試執行詳細資料頁面，但無法從指定要顯示之學生的連結中取得。 如果發生這種情況，請從 URL 移除 "Student/Details"，然後再試一次，或關閉瀏覽器，以滑鼠**按右鍵專案，然後按一下 [** **在瀏覽器中 > 視圖**]）。

    您會看到所選學生的課程和成績清單。

4. 關閉瀏覽器。

## <a name="update-the-create-page"></a>更新 [建立] 頁面

1. 在*Controllers\StudentController.cs*中，將 <xref:System.Web.Mvc.HttpPostAttribute> `Create` 動作方法取代為下列程式碼。 此程式碼會新增 `try-catch` 區塊，並從 scaffold 方法的 <xref:System.Web.Mvc.BindAttribute> 屬性移除 `ID`：

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample7.cs?highlight=3,5-6,13-18)]

    此程式碼會將 ASP.NET MVC 模型系結器所建立的 `Student` 實體加入 `Students` 實體集，然後將變更儲存至資料庫。 *模型*系結器指的是 ASP.NET 的 MVC 功能，可讓您更輕鬆地使用表單所提交的資料;模型系結器會將已張貼的表單值轉換成 CLR 類型，並將它們傳遞至參數中的動作方法。 在此情況下，模型系結器會使用 `Form` 集合中的屬性值，為您具現化 `Student` 實體。

    您已從系結屬性中移除 `ID`，因為 `ID` 是 SQL Server 會在插入資料列時自動設定的主要索引鍵值。 使用者的輸入未設定 `ID` 值。

    <a id="overpost"></a>

    ### <a name="security-warning---the-validateantiforgerytoken-attribute-helps-prevent-cross-site-request-forgery-attacks-it-requires-a-corresponding-htmlantiforgerytoken-statement-in-the-view-which-youll-see-later"></a>安全性警告-`ValidateAntiForgeryToken` 屬性有助於防止[跨網站偽造要求](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md)攻擊。 它在視圖中需要有對應的 `Html.AntiForgeryToken()` 語句，稍後您會看到。

    `Bind` 屬性是在建立案例中保護不會*過度張貼*的一種方式。 例如，假設 `Student` 實體包含您不想要讓此網頁設定的 `Secret` 屬性。

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample8.cs?highlight=7)]

    即使網頁上沒有 `Secret` 欄位，駭客也可以使用[fiddler](http://fiddler2.com/home)之類的工具，或是撰寫一些 JavaScript，以張貼 `Secret` 的表單值。 如果沒有 <xref:System.Web.Mvc.BindAttribute> 屬性會限制模型系結器在建立 `Student` 實例時所使用的欄位<em>，</em>模型系結器會收取該 `Secret` 的表單值，並使用它來建立 `Student` 實體實例。 則無論駭客在 `Secret` 表單欄位中指定了什麼值，該值都會更新到您的資料庫中。 下圖顯示 fiddler 工具將 [`Secret`] 欄位（值為 "OverPost"）新增至張貼的表單值。

    ![](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image5.png)

    "OverPost" 的值會成功新增到插入資料列的 `Secret` 屬性中，即使您沒有要讓網頁設定該屬性。

    最佳做法是使用 `Include` 參數搭配 `Bind` 屬性來將欄位*列入白名單*。 您也可以使用 `Exclude` 參數，將您要排除的欄位*列入*封鎖清單。 `Include` 的原因較安全，因為當您將新的屬性加入至實體時，新的欄位不會自動受到 `Exclude` 清單的保護。

    您可以在編輯案例中避免防止大量指派，方法是先從資料庫讀取實體，然後呼叫 `TryUpdateModel`，傳入明確允許的屬性清單。 這是在這些教學課程中使用的方法。

    另一種避免許多開發人員慣用的防止大量指派的方法，就是使用視圖模型，而不是透過模型系結的實體類別。 意即僅在檢視模型中包含您想要更新的屬性。 一旦 MVC 模型系結器完成，請將視圖模型屬性複製到實體實例，並選擇性地使用[AutoMapper](http://automapper.org/)之類的工具。 使用 db。在實體實例上的專案，將其狀態設定為 [未變更]，然後設定屬性（"PropertyName"）。在視圖模型所包含的每個實體屬性上，IsModified 為 true。 這個方法可同時運用在編輯及建立案例中。

    除了 `Bind` 屬性以外，`try-catch` 區塊是您對 scaffold 程式碼所做的唯一變更。 若在儲存變更時捕捉到衍生自 <xref:System.Data.DataException> 的例外狀況，則會顯示一般錯誤訊息。 <xref:System.Data.DataException> 例外狀況有時候是因為某些外部因素造成的，而非程式設計上的錯誤，因此系統會建議使用者再試一次。 雖然在此範例中並未實作，但生產環境品質的應用程式應記錄例外狀況。 如需詳細資訊，請參閱**監視及遙測 (使用 Azure 建置現實世界的雲端應用程式)** 中的[深入解析記錄檔](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log)一節。

    *Views\Student\Create.cshtml*中的程式碼類似于您在*詳細資料*中所看到的內容，不同之處在于，`EditorFor` 和 `ValidationMessageFor` helper 會用於每個欄位，而不是 `DisplayFor`。 以下是相關的程式碼：

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample9.cshtml)]

    *Create. cshtml*也包含 `@Html.AntiForgeryToken()`，其可與控制器中的 `ValidateAntiForgeryToken` 屬性搭配使用，以協助防止[跨網站偽造要求](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md)攻擊。

    *Create. cshtml*中不需要進行任何變更。

2. 啟動程式、選取 [**學生**] 索引標籤，**然後按一下 [新建]** ，以執行頁面。

3. 輸入名稱和不正確日期，然後按一下 [**建立**] 以查看錯誤訊息。

    這是您預設會取得的伺服器端驗證。 在稍後的教學課程中，您將瞭解如何新增屬性來產生用戶端驗證的程式碼。 下列反白顯示的程式碼顯示**Create**方法中的模型驗證檢查。

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample10.cs?highlight=1)]

4. 將日期變更為有效的值，然後按一下 [建立] 來在 [索引] 頁面上查看新增的學生。

5. 關閉瀏覽器。

## <a name="update-httppost-edit-method"></a>更新 HttpPost 編輯方法

1. 使用下列程式碼取代 <xref:System.Web.Mvc.HttpPostAttribute> `Edit` 動作方法：

   [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample11.cs)]

   > [!NOTE]
   > 在*Controllers\StudentController.cs*中，`HttpGet Edit` 方法（沒有 `HttpPost` 屬性的方法）會使用 `Find` 方法來抓取選取的 `Student` 實體，如同您在 `Details` 方法中所見。 您不需要變更這個方法。

   這些變更會執行安全性最佳作法，以避免[防止大量指派](#overpost)，scaffolder 會產生 `Bind` 屬性，並將模型系結器所建立的實體新增至具有修改旗標的實體集。 不再建議該程式碼，因為 `Bind` 屬性會清除 `Include` 參數中未列出之欄位中的任何預先存在的資料。 在未來，將會更新 MVC 控制器 scaffolder，使其不會產生編輯方法的 `Bind` 屬性。

   新的程式碼會讀取現有的實體，並呼叫 <xref:System.Web.Mvc.Controller.TryUpdateModel%2A>，以在張貼的表單資料中更新使用者輸入的欄位。 Entity Framework 的自動變更追蹤會在實體上設定[EntityState](<xref:System.Data.EntityState.Modified>)旗標。 呼叫[SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx)方法時，<xref:System.Data.EntityState.Modified> 旗標會使 ENTITY FRAMEWORK 建立 SQL 語句以更新資料庫資料列。 系統會忽略[並行衝突](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)，而且會更新資料庫資料列的所有資料行，包括使用者未變更的欄位。 （稍後的教學課程會示範如何處理並行衝突，如果您只想要在資料庫中更新個別的欄位，您可以將實體設定為[EntityState](<xref:System.Data.EntityState.Unchanged>) ，並將個別欄位設定為[EntityState. Modified](<xref:System.Data.EntityState.Modified>)）。

   若要避免防止大量指派，您要由 [編輯] 頁面更新的欄位會在 `TryUpdateModel` 參數的白名單中。 雖然目前沒有額外保護的欄位，但列出您希望模型繫結器繫結的欄位可確保您於未來將欄位新增到資料模型中時，新增的欄位會自動獲得保護，直到您明確的在這裡新增它們為止。

   由於這些變更的結果，HttpPost Edit 方法的方法簽章與 HttpGet edit 方法相同。因此，您已將方法重新命名為 EditPost。

   > [!TIP]
   >
   > **實體狀態和 Attach 和 SaveChanges 方法**
   >
   > 資料庫內容會追蹤實體在記憶體中是否與其在資料庫中相對應的資料列保持同步，並且此項資訊會決定當您呼叫 `SaveChanges` 方法時會發生什麼事情。 例如，當您將新實體傳遞至[Add](https://msdn.microsoft.com/library/system.data.entity.dbset.add(v=vs.103).aspx)方法時，該實體的狀態會設定為 `Added`。 然後，當您呼叫[SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx)方法時，資料庫內容就會發出 SQL `INSERT` 命令。
   >
   > 實體可能處於下列其中一種[狀態](xref:System.Data.EntityState)：
   >
   > - `Added` 實體尚未存在於資料庫中。 `SaveChanges` 的方法必須發出 `INSERT` 語句。
   > - `Unchanged` `SaveChanges` 方法針對這個實體不需要進行任何動作。 當您從資料庫讀取一個實體時，實體便會以此狀態開始。
   > - `Modified` 實體中一部分或全部的屬性值已經過修改。 `SaveChanges` 的方法必須發出 `UPDATE` 語句。
   > - `Deleted` 實體已遭標示刪除。 `SaveChanges` 的方法必須發出 `DELETE` 語句。
   > - `Detached` 實體未獲得資料庫內容追蹤。
   >
   > 在桌面應用程式中，狀態變更通常會自動進行設定。 在桌上型電腦類型的應用程式中，您會讀取實體並對其部分屬性值進行變更。 這會使得其實體狀態自動變更為 `Modified`。 然後，當您呼叫 `SaveChanges`時，Entity Framework 會產生 SQL `UPDATE` 語句，只更新您所變更的實際屬性。
   >
   > Web apps 中斷連線的本質不允許此連續順序。 在呈現頁面之後，會處置讀取實體的[DbCoNtext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) 。 呼叫 `HttpPost` `Edit` 動作方法時，會提出新的要求，而且您會有新的[DbCoNtext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)實例，因此您必須手動將實體狀態設定為 `Modified.` 然後當您呼叫 `SaveChanges`時，Entity Framework 會更新資料庫資料列的所有資料行，因為內容無法得知您變更的屬性。
   >
   > 如果您想要 SQL `Update` 語句僅更新使用者實際變更的欄位，您可以用某種方式儲存原始值（例如隱藏欄位），以便在呼叫 `HttpPost` `Edit` 方法時使用它們。 接著，您可以使用原始值來建立 `Student` 實體、以該實體的原始版本呼叫 `Attach` 方法、將實體的值更新為新的值，然後呼叫 `SaveChanges.` 以取得詳細資訊，請參閱[實體狀態和 SaveChanges](/ef/ef6/saving/change-tracking/entity-state)和[本機資料](/ef/ef6/querying/local-data)。

   *Views\Student\Edit.cshtml*中的 HTML 和 Razor 程式碼類似于您在*Create. cshtml*中看到的內容，而且不需要進行任何變更。

2. 啟動程式、選取 [**學生**] 索引標籤，然後按一下 [**編輯**] 超連結，以執行頁面。

3. 變更一部分的資料，然後按一下 [儲存]。 您會在 [索引] 頁面中看到變更的資料。

4. 關閉瀏覽器。

## <a name="update-the-delete-page"></a>更新 [刪除] 頁面

在*Controllers\StudentController.cs*中，<xref:System.Web.Mvc.HttpGetAttribute> `Delete` 方法的範本程式碼會使用 `Find` 方法來抓取選取的 `Student` 實體，如同您在 `Details` 和 `Edit` 方法中所見。 然而，若要在呼叫 `SaveChanges` 失敗時實作自訂錯誤訊息，您需要將一些功能新增至此方法及其對應的檢視。

如同您在更新及建立作業中所看到的，刪除作業需要兩個動作方法。 回應 GET 要求所呼叫的方法會顯示一個視圖，讓使用者有機會核准或取消刪除作業。 若使用者核准，則便會建立 POST 要求。 發生這種情況時，會呼叫 `HttpPost` `Delete` 方法，然後該方法會實際執行刪除作業。

您會將 `try-catch` 區塊新增至 <xref:System.Web.Mvc.HttpPostAttribute> `Delete` 方法，以處理資料庫更新時可能發生的任何錯誤。 如果發生錯誤，<xref:System.Web.Mvc.HttpPostAttribute> `Delete` 方法會呼叫 <xref:System.Web.Mvc.HttpGetAttribute> `Delete` 方法，並將指出發生錯誤的參數傳遞給它。 <xref:System.Web.Mvc.HttpGetAttribute> `Delete` 方法接著會重新顯示確認頁面，並顯示錯誤訊息，讓使用者有機會取消或再試一次。

1. 將 <xref:System.Web.Mvc.HttpGetAttribute> `Delete` 動作方法取代為下列程式碼，以管理錯誤報表：

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample12.cs?highlight=1,7-10)]

    此程式碼會接受[選擇性的參數](https://msdn.microsoft.com/library/dd264739.aspx)，指出在無法儲存變更之後是否呼叫了方法。 呼叫 `HttpGet` `Delete` 方法時，如果沒有先前的失敗，就會 `false` 此參數。 當 `HttpPost` `Delete` 方法呼叫它來回應資料庫更新錯誤時，會 `true` 參數，並將錯誤訊息傳遞給視圖。

2. 將 <xref:System.Web.Mvc.HttpPostAttribute> `Delete` 動作方法（名為 `DeleteConfirmed`）取代為下列程式碼，以執行實際的刪除作業並捕捉任何資料庫更新錯誤。

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample13.cs)]

    此程式碼會抓取選取的實體，然後呼叫[Remove](https://msdn.microsoft.com/library/system.data.entity.dbset.remove(v=vs.103).aspx)方法，將實體的狀態設定為 `Deleted`。 呼叫 `SaveChanges` 時，會產生 SQL `DELETE` 命令。 您也將動作方法的名稱從 `DeleteConfirmed` 變更為 `Delete`。 名為 `HttpPost` 的 scaffold 程式碼 `Delete` 方法 `DeleteConfirmed`，為 `HttpPost` 方法提供唯一的簽章。 （CLR 需要多載的方法，才能有不同的方法參數）。簽章是唯一的，您可以使用 MVC 慣例，並將相同的名稱用於 `HttpPost` 和 `HttpGet` delete 方法。

    如果提升高容量應用程式的效能是一項優先考慮，您可以使用下列程式碼取代呼叫 `Find` 和 `Remove` 方法的程式程式碼，以避免不必要的 SQL 查詢抓取資料列：

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample14.cs)]

    此程式碼會只使用主要索引鍵值來具現化 `Student` 實體，然後將實體狀態設定為 `Deleted`。 這便是 Entity Framework 要刪除實體所需要的一切資訊。

    如先前所述，`HttpGet` `Delete` 方法不會刪除資料。 執行刪除作業以回應 GET 要求（也就是，執行任何編輯作業、建立作業或任何其他變更資料的作業）會造成安全性風險。 如需詳細資訊，請參閱[ASP.NET MVC Tip #46-不要使用刪除連結，因為它們會](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)在 Stephen Walther 的 blog 上建立安全性漏洞。

3. 在*Views\Student\Delete.cshtml*中，于 [`h2`] 標題和 [`h3`] 標題之間新增錯誤訊息，如下列範例所示：

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample15.cshtml?highlight=2)]

4. 啟動程式、選取 [**學生**] 索引標籤，然後按一下 [**刪除**] 超連結，以執行頁面。

5. 在顯示**您確定要刪除此專案**的頁面上，選擇 [**刪除**]。

    [索引] 頁面會顯示，但不含已刪除的學生。 （您會在[並行教學](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)課程中看到錯誤處理常式代碼的範例）。

## <a name="close-database-connections"></a>關閉資料庫連線

若要關閉資料庫連接，並儘快釋放其保留的資源，請在完成時處置內容實例。 這就是為什麼 scaffold 程式碼會在*StudentController.cs*中的 `StudentController` 類別結尾提供[Dispose](https://msdn.microsoft.com/library/system.idisposable.dispose(v=vs.110).aspx)方法，如下列範例所示：

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample16.cs)]

基底 `Controller` 類別已經實 `IDisposable` 介面，因此此程式碼只會將覆寫加入至 `Dispose(bool)` 方法，以明確處置內容實例。

## <a name="handle-transactions"></a>處理交易

根據預設，Entity Framework 隱含性的實作了交易。 在您對多個資料列或資料表進行變更，然後呼叫 `SaveChanges`的情況下，Entity Framework 會自動確保所有變更都成功或全部失敗。 若有些變更已先完成，之後卻發生錯誤，則這些變更都會自動進行復原。 針對您需要更多控制&mdash;例如，如果您想要在交易中包含在 Entity Framework 外部完成的作業&mdash;請參閱[使用交易](/ef/ef6/saving/transactions)。

## <a name="get-the-code"></a>取得程式碼

[下載已完成的專案](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>其他資源

您現在有一組完整的頁面，可為 `Student` 實體執行簡單的 CRUD 作業。 您使用 MVC helper 來產生資料欄位的 UI 元素。 如需 MVC helper 的詳細資訊，請參閱使用 HTML 協助程式轉譯[表單](/previous-versions/aspnet/dd410596(v=vs.98))（這篇文章是針對 mvc 3，但仍與 mvc 5 有關）。

您可以在[ASP.NET 資料存取-建議的資源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 EF 6 資源的連結。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已：

> [!div class="checklist"]
> * 建立詳細資料頁面
> * 更新 [建立] 頁面
> * 已更新 HttpPost Edit 方法
> * 更新 [刪除] 頁面
> * 關閉資料庫連線
> * 已處理的交易

前進到下一篇文章，以瞭解如何將排序、篩選和分頁加入至專案。
> [!div class="nextstepaction"]
> [排序、篩選與分頁](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
