---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-3
title: 具有 Entity Framework 4.0 Database First 和 ASP.NET 4 Web form 的消費者入門-第3部分 |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 來建立 ASP.NET Web Forms 應用程式。 範例應用程式為 。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: ccdc3f8c-2568-40a7-8f8b-3c23d2e05388
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-3
msc.type: authoredcontent
ms.openlocfilehash: 88debb11a9157dce9ff000b1cb459b876dbceaf3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78643245"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-3"></a>Entity Framework 4.0 Database First 和 ASP.NET 4 Web form 的消費者入門-第3部分

由[Tom 作者: dykstra](https://github.com/tdykstra)

> Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 4.0 和 Visual Studio 2010 來建立 ASP.NET Web Forms 應用程式。 如需教學課程系列的資訊，請參閱本[系列的第一個教學](the-entity-framework-and-aspnet-getting-started-part-1.md)課程

## <a name="filtering-ordering-and-grouping-data"></a>篩選、排序和分組資料

在上一個教學課程中，您使用了 [`EntityDataSource`] 控制項來顯示和編輯資料。 在本教學課程中，您將會篩選、排序和分組資料。 當您藉由設定 `EntityDataSource` 控制項的屬性來執行此動作時，語法會與其他資料來源控制項不同。 不過您會發現，您可以使用 `QueryExtender` 控制項，將這些差異降到最低。

您將變更 [student] 頁面來*篩選學生、* 依名稱排序，以及搜尋 [名稱]。 您也會變更 [*課程 .aspx* ] 頁面，以顯示所選部門的課程，並依名稱搜尋課程。 最後，您會將學生統計資料新增至*About .aspx*頁面。

[![Image02](the-entity-framework-and-aspnet-getting-started-part-3/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image1.png)

[![Image11](the-entity-framework-and-aspnet-getting-started-part-3/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image3.png)

[![Image10](the-entity-framework-and-aspnet-getting-started-part-3/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image5.png)

[![Image14](the-entity-framework-and-aspnet-getting-started-part-3/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image7.png)

## <a name="using-the-entitydatasource-where-property-to-filter-data"></a>使用 EntityDataSource "Where" 屬性來篩選資料

開啟您在上一個教學課程中建立的 [*學生 .aspx* ] 頁面。 如目前所設定，頁面中的 `GridView` 控制項會顯示來自 `People` 實體集的所有名稱。 不過，您只想要顯示學生，您可以藉由選取 `Person` 具有非 null 註冊日期的實體來尋找。

切換至 [**設計**視圖]，然後選取 [`EntityDataSource`] 控制項。 在 [屬性] 視窗中，將 `Where` 屬性設定為 `it.EnrollmentDate is not null`。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-3/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image9.png)

您在 `EntityDataSource` 控制項的 `Where` 屬性中所使用的語法是 Entity SQL。 Entity SQL 與 Transact-sql 類似，但它是針對與實體（而非資料庫物件）使用而自訂的。 在運算式 `it.EnrollmentDate is not null`中，`it` 一字代表查詢所傳回之實體的參考。 因此，`it.EnrollmentDate` 指的是 `EntityDataSource` 控制項傳回之 `Person` 實體的 `EnrollmentDate` 屬性。

執行頁面。 學生清單現在只包含學生。 （沒有任何資料列顯示在沒有註冊日期的位置）。

[![Image02](the-entity-framework-and-aspnet-getting-started-part-3/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image11.png)

## <a name="using-the-entitydatasource-orderby-property-to-order-data"></a>使用 EntityDataSource "OrderBy" 屬性來排序資料

當第一次顯示此清單時，您也會想要依名稱排序。 在 [**設計**視圖] 中仍開啟 [student *] 頁面，* `EntityDataSource` 並在 [**屬性**] 視窗中，將 [ **OrderBy** ] 屬性設定為 [`it.LastName`]。

[![Image05](the-entity-framework-and-aspnet-getting-started-part-3/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image13.png)

執行頁面。 學生清單現在依姓氏排序。

[![Image04](the-entity-framework-and-aspnet-getting-started-part-3/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image15.png)

## <a name="using-a-control-parameter-to-set-the-where-property"></a>使用控制項參數來設定 "Where" 屬性

如同其他資料來源控制項，您可以將參數值傳遞給 `Where` 屬性。 在您于本教學課程的第2部分中建立的 [.aspx] 頁面上，您可以使用這個方法來顯示與使用者從下拉式清單中選取之部門相關聯的課程 *。*

開啟 [*課程*]，並切換至 [**設計**視圖]。 將第二個 `EntityDataSource` 控制項新增至頁面，並將其命名為 `CoursesEntityDataSource`。 將它連接到 `SchoolEntities` 模型，然後選取 [`Courses`] 做為**EntitySetName**值。

在 [**屬性**] 視窗中，按一下 [ **Where** ] 屬性方塊中的省略號。 （請確定在使用 [**屬性**] 視窗之前，仍選取了 [`CoursesEntityDataSource`] 控制項）。

[![Image06](the-entity-framework-and-aspnet-getting-started-part-3/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image17.png)

[**運算式編輯器**] 對話方塊隨即顯示。 在此對話方塊中，選取 **[根據提供的參數自動產生 Where 運算式**]，然後按一下 [**加入參數**]。 將參數命名為 `DepartmentID`，選取 [**控制項**] 做為 [**參數來源**] 值，然後選取 [ **DepartmentsDropDownList** ] 作為**ControlID**值。

[![Image07](the-entity-framework-and-aspnet-getting-started-part-3/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image19.png)

按一下 [**顯示高級屬性**]，然後在 [**運算式編輯器**] 對話方塊的 [**屬性**] 視窗中，將 [`Type`] 屬性變更為 [`Int32`]。

[![Image15](the-entity-framework-and-aspnet-getting-started-part-3/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image21.png)

完成後，按一下 [ **確定**]。

在下拉式清單下方，將 [`GridView`] 控制項加入至頁面，並將其命名為 `CoursesGridView`。 將它連接到 `CoursesEntityDataSource` 資料來源控制項，按一下 [重新整理**架構**]，按一下 [**編輯資料行**]，然後移除 [`DepartmentID`] 資料行。 `GridView` 控制項標記與下列範例類似。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample1.aspx)]

當使用者在下拉式清單中變更選取的部門時，您會想要自動變更相關聯課程的清單。 若要進行這項操作，請選取下拉式清單，然後在 [**屬性**] 視窗中，將 [`AutoPostBack`] 屬性設定為 [`True`]。

[![Image08](the-entity-framework-and-aspnet-getting-started-part-3/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image23.png)

現在您已完成使用設計工具，請切換至**來源**視圖，並將 `CoursesEntityDataSource` 控制項的 [`ConnectionString`] 和 [`DefaultContainer` 名稱] 屬性取代為 `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"` 屬性。 當您完成時，控制項的標記看起來會如下列範例所示。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample2.aspx)]

執行頁面，並使用下拉式清單來選取不同的部門。 只有所選部門所提供的課程會顯示在 [`GridView`] 控制項中。

[![Image09](the-entity-framework-and-aspnet-getting-started-part-3/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image25.png)

## <a name="using-the-entitydatasource-groupby-property-to-group-data"></a>使用 EntityDataSource "GroupBy" 屬性來分組資料

假設 Contoso 大學想要在 [關於] 頁面上放入一些學生主體統計資料。 具體而言，它會想要依註冊的日期來顯示學生數目的明細。

開啟 [*關於 .aspx*]，然後在**原始**檔視圖中，將 `BodyContent` 控制項的現有內容取代為 `h2` 標記之間的「學生主體統計資料」：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample3.aspx)]

在標題後面，加入 `EntityDataSource` 控制項，並將其命名為 `StudentStatisticsEntityDataSource`。 將它連接到 `SchoolEntities`，選取 [`People`] 實體集，然後在嚮導中保持不變的 [**選取**] 方塊。 在 [**屬性**] 視窗中設定下列屬性：

- 若只要篩選學生，請將 `Where` 屬性設定為 [`it.EnrollmentDate is not null`]。
- 若要依據註冊日期將結果分組，請將 `GroupBy` 屬性設定為 [`it.EnrollmentDate`]。
- 若要選取註冊日期和學生數目，請將 [`Select`] 屬性設定為 [`it.EnrollmentDate, Count(it.EnrollmentDate) AS NumberOfStudents`]。
- 若要依註冊日期排序結果，請將 `OrderBy` 屬性設為 `it.EnrollmentDate`。

在 [**來源**視圖] 中，將 [`ConnectionString`] 和 [`DefaultContainer` 名稱] 屬性取代為 `ContextTypeName` 屬性。 `EntityDataSource` 控制項標記現在與下列範例類似。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample4.aspx)]

除了指定目前實體的 `it` 關鍵字以外，`Select`、`GroupBy`和 `Where` 屬性的語法類似 Transact-sql。

新增下列標記來建立 `GridView` 控制項，以顯示資料。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample5.aspx)]

執行頁面以查看顯示註冊日期的學生數目清單。

[![Image10](the-entity-framework-and-aspnet-getting-started-part-3/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image27.png)

## <a name="using-the-queryextender-control-for-filtering-and-ordering"></a>使用 QueryExtender 控制項進行篩選和排序

`QueryExtender` 控制項提供在標記中指定篩選和排序的方法。 語法與您所使用的資料庫管理系統（DBMS）無關。 它通常也獨立于 Entity Framework，但您用於導覽屬性的語法對於 Entity Framework 而言是唯一的。

在本教學課程的這個部分中，您將使用 `QueryExtender` 控制項來篩選和排序資料，而其中一個 order by 欄位會是導覽屬性。

（如果您想要使用程式碼而非標記來擴充 `EntityDataSource` 控制項自動產生的查詢，您可以藉由處理 `QueryCreated` 事件來執行此動作。 這也是 `QueryExtender` 控制項擴充 `EntityDataSource` 控制項查詢的方式）。

開啟 [*課程 .aspx* ] 頁面，然後在您先前加入的標記底下，插入下列標記以建立標題、輸入搜尋字串的文字方塊、搜尋按鈕，以及系結至 `Courses` 實體集的 `EntityDataSource` 控制項。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample6.aspx)]

請注意，`EntityDataSource` 控制項的 `Include` 屬性已設定為 [`Department`]。 在資料庫中，`Course` 資料表不包含部門名稱;它包含 `DepartmentID` 外鍵資料行。 如果您直接查詢資料庫，若要取得部門名稱和課程資料，您必須聯結 `Course` 和 `Department` 資料表。 藉由將 [`Include`] 屬性設定為 [`Department`]，您可以指定 Entity Framework 在取得 `Course` 實體時，應執行取得相關 `Department` 實體的工作。 然後 `Department` 實體會儲存在 `Course` 實體的 `Department` 導覽屬性中。 （根據預設，資料模型設計工具所產生的 `SchoolEntities` 類別會在需要時，會抓取相關資料，而且您已將資料來源控制項系結至該類別，因此不需要設定 `Include` 屬性。 不過，設定它會改善頁面的效能，因為否則 Entity Framework 會對資料庫進行個別的呼叫，以抓取 `Course` 實體和相關 `Department` 實體的資料）。

在您剛建立的 `EntityDataSource` 控制項之後，插入下列標記以建立系結至該 `EntityDataSource` 控制項的 `QueryExtender` 控制項。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample7.aspx)]

`SearchExpression` 專案指定您想要選取標題與文字方塊中輸入的值相符的課程。 因為 `SearchType` 屬性會指定 `StartsWith`，所以只會比較文字方塊中輸入的字元數。

`OrderByExpression` 元素指定結果集將依部門名稱內的課程標題排序。 請注意指定部門名稱的方式： `Department.Name`。 由於 `Course` 實體與 `Department` 實體之間的關聯是一對一的，因此 `Department` 導覽屬性會包含 `Department` 實體。 （如果這是一對多關聯性，屬性會包含集合）。若要取得部門名稱，您必須指定 `Department` 實體的 `Name` 屬性。

最後，新增 `GridView` 控制項以顯示課程清單：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample8.aspx)]

第一個資料行是範本欄位，會顯示部門名稱。 資料系結運算式會指定 `Department.Name`，就像您在 `QueryExtender` 控制項中所看到的一樣。

執行頁面。 初始顯示會依部門和課程標題顯示所有課程的清單。

[![Image11](the-entity-framework-and-aspnet-getting-started-part-3/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image29.png)

輸入 "m"，然後按一下 [**搜尋**]，以查看標題開頭為 "m" 的所有課程（搜尋不區分大小寫）。

[![Image12](the-entity-framework-and-aspnet-getting-started-part-3/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image31.png)

## <a name="using-the-like-operator-to-filter-data"></a>使用 "Like" 運算子來篩選資料

您可以使用 `Like` 控制項的 `EntityDataSource` 屬性中的 `Where` 運算子，來達到與 `QueryExtender` 控制項的 `StartsWith`、`Contains`和 `EndsWith` 搜尋類型類似的效果。 在本教學課程的這個部分中，您將瞭解如何使用 `Like` 運算子依名稱搜尋學生。

在**原始**檔視圖中開啟*student。* 在 `GridView` 控制項之後，加入下列標記：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample9.aspx)]

此標記類似于您稍早所見的，但 `Where` 屬性值除外。 `Where` 運算式的第二個部分會定義子字串搜尋（`LIKE %FirstMidName% or LIKE %LastName%`），以搜尋文字方塊中所輸入之名稱的名字和姓氏。

執行頁面。 一開始您會看到所有學生，因為 `StudentName` 參數的預設值為 "%"。

[![Image13](the-entity-framework-and-aspnet-getting-started-part-3/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image33.png)

在文字方塊中輸入字母 "g"，然後按一下 [**搜尋**]。 您會在名字或姓氏看到有 "g" 的學生清單。

[![Image14](the-entity-framework-and-aspnet-getting-started-part-3/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image35.png)

您現在已從個別資料表顯示、更新、篩選、排序和分組資料。 在下一個教學課程中，您將開始使用相關資料（主版詳細案例）。

> [!div class="step-by-step"]
> [上一頁](the-entity-framework-and-aspnet-getting-started-part-2.md)
> [下一頁](the-entity-framework-and-aspnet-getting-started-part-4.md)
