---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
title: 使用 Entity Framework 4.0 和 ObjectDataSource 控制項，第3部分：排序和篩選 |Microsoft Docs
author: tdykstra
description: 本教學課程系列是以 Entity Framework 4.0 教學課程系列的消費者入門所建立的 Contoso 大學 web 應用程式為基礎。 I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 2990bd10-590d-43d5-9529-6b503ce5455d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
msc.type: authoredcontent
ms.openlocfilehash: 603120864528b9a5ff81214270eb9a7f1b68b347
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78631667"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-3-sorting-and-filtering"></a>使用 Entity Framework 4.0 和 ObjectDataSource 控制項，第3部分：排序和篩選

由[Tom 作者: dykstra](https://github.com/tdykstra)

> 本教學課程系列是[以 Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started)教學課程系列的消費者入門所建立的 Contoso 大學 web 應用程式為基礎。 如果您未完成先前的教學課程，做為本教學課程的起點，您可以下載您所建立[的應用程式](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)。 您也可以下載完整的教學課程系列所建立[的應用程式](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)。 如果您有關于教學課程的問題，可以將其張貼到[ASP.NET Entity Framework 論壇](https://forums.asp.net/1227.aspx)。

在上一個教學課程中，您已在使用 Entity Framework 和 `ObjectDataSource` 控制項的多層式 web 應用程式中，實作為存放庫模式。 本教學課程說明如何進行排序和篩選，以及處理主版詳細資料案例。 您將會在 [*部門 .aspx* ] 頁面中加入下列增強功能：

- 允許使用者依名稱選取部門的文字方塊。
- 方格中所顯示之每個部門的課程清單。
- 按一下資料行標題來排序的功能。

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)

## <a name="adding-the-ability-to-sort-gridview-columns"></a>新增排序 GridView 資料行的功能

開啟 [*部門 .aspx* ] 頁面，並將 `SortParameterName="sortExpression"` 屬性加入至名為 `DepartmentsObjectDataSource`的 `ObjectDataSource` 控制項。 （稍後您將建立使用名為 `sortExpression`之參數的 `GetDepartments` 方法）。控制項開頭標記的標記現在與下列範例類似。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample1.aspx)]

將 `AllowSorting="true"` 屬性加入 `GridView` 控制項的開頭標記。 控制項開頭標記的標記現在與下列範例類似。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample2.aspx)]

在*Departments.aspx.cs*中，從 `Page_Load` 方法呼叫 `GridView` 控制項的 `Sort` 方法，以設定預設排序次序：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample3.cs)]

您可以在商務邏輯類別或儲存機制類別中加入排序或篩選的程式碼。 如果您在商務邏輯類別中執行此動作，則會在從資料庫抓取資料後完成排序或篩選工作，因為商務邏輯類別正在使用儲存機制所傳回的 `IEnumerable` 物件。 如果您在存放庫類別中加入排序和篩選程式代碼，並在 LINQ 運算式或物件查詢轉換成 `IEnumerable` 物件之前執行它，則您的命令會傳遞到資料庫進行處理，這通常會更有效率。 在本教學課程中，您將會以導致資料庫完成處理的方式（也就是在存放庫中）來執行排序和篩選。

若要加入排序功能，您必須將新的方法加入至存放庫介面和存放庫類別，以及商務邏輯類別。 在*ISchoolRepository.cs*檔案中，加入一個新的 `GetDepartments` 方法，它會使用 `sortExpression` 參數來排序傳回的部門清單：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample4.cs)]

`sortExpression` 參數將會指定要排序的資料行以及排序方向。

將新方法的程式碼新增至*SchoolRepository.cs*檔案：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample5.cs)]

變更現有的無參數 `GetDepartments` 方法以呼叫新的方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample6.cs)]

在測試專案中，將下列新方法新增至*MockSchoolRepository.cs*：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample7.cs)]

如果您要建立相依于此方法並傳回已排序清單的任何單元測試，您必須先排序清單，再將它傳回。 您不會在本教學課程中建立像這樣的測試，因此方法可以只傳回未排序的部門清單。

在*SchoolBL.cs*檔案中，將下列新方法新增至商務邏輯類別：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample8.cs)]

此程式碼會將排序參數傳遞至存放庫方法。

執行 [*部門 .aspx* ] 頁面。

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)

您現在可以按一下任何資料行標題，依該資料行排序。 如果資料行已經排序，按一下標題會反轉排序方向。

## <a name="adding-a-search-box"></a>新增搜尋方塊

在本節中，您將加入搜尋文字方塊、使用控制項參數將它連結至 `ObjectDataSource` 控制項，以及將方法加入商務邏輯類別以支援篩選。

開啟 [*部門 .aspx* ] 頁面，並在標題和第一個 `ObjectDataSource` 控制項之間加入下列標記：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample9.aspx)]

在名為 `DepartmentsObjectDataSource`的 `ObjectDataSource` 控制項中，執行下列動作：

- 為名為 `nameSearchString` 的參數新增 `SelectParameters` 專案，以取得 `SearchTextBox` 控制項中輸入的值。
- 將 `SelectMethod` 屬性值變更為 `GetDepartmentsByName`。 （您稍後會建立此方法）。

`ObjectDataSource` 控制項的標記現在與下列範例類似：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample10.aspx)]

在*ISchoolRepository.cs*中，新增同時採用 `sortExpression` 和 `nameSearchString` 參數的 `GetDepartmentsByName` 方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample11.cs)]

在*SchoolRepository.cs*中，新增下列新方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample12.cs)]

這段程式碼會使用 `Where` 方法來選取包含搜尋字串的專案。 如果搜尋字串是空的，則會選取所有記錄。 請注意，當您在像這樣的一個語句中同時指定方法呼叫（`Include`，然後 `OrderBy`，然後 `Where`），`Where` 方法一律必須是最後一個。

變更使用 `sortExpression` 參數的現有 `GetDepartments` 方法，以呼叫新的方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample13.cs)]

在測試專案的*MockSchoolRepository.cs*中，新增下列新方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample14.cs)]

在*SchoolBL.cs*中，新增下列新方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample15.cs)]

執行 [*部門 .aspx* ] 頁面並輸入搜尋字串，以確定選取邏輯可以運作。 將文字方塊保留空白，然後嘗試進行搜尋，以確保會傳回所有記錄。

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)

## <a name="adding-a-details-column-for-each-grid-row"></a>為每個格線列加入詳細資料行

接下來，您想要查看方格右側儲存格中顯示之每個部門的所有課程。 若要這麼做，您將使用嵌套的 `GridView` 控制項，並將它從 `Department` 實體的 `Courses` 導覽屬性中的資料進行 databind。

開啟 *部門 .aspx* ，然後在 `GridView` 控制項的標記中，指定 `RowDataBound` 事件的處理常式。 控制項開頭標記的標記現在與下列範例類似。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample16.aspx)]

在 [`Administrator` 範本] 欄位之後加入新的 `TemplateField` 元素：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample17.aspx)]

此標記會建立一個嵌套的 `GridView` 控制項，以顯示課程清單的課程編號和標題。 它不會指定資料來源，因為您會將它以 `RowDataBound` 處理常式中的程式碼進行 databind。

開啟*Departments.aspx.cs* ，並新增下列 `RowDataBound` 事件的處理常式：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample18.cs)]

此程式碼會從事件引數取得 `Department` 實體、將 `Courses` 導覽屬性轉換為 `List` 集合，並將嵌套的 `GridView` 將至集合。

開啟*SchoolRepository.cs*檔案，並在您于 `GetDepartmentsByName` 方法中建立的物件查詢中呼叫 `Include` 方法，以指定 `Courses` 導覽屬性的積極式載入。 `GetDepartmentsByName` 方法中的 `return` 語句現在與下列範例類似。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample19.cs)]

執行頁面。 除了您稍早新增的排序和篩選功能之外，GridView 控制項現在會顯示每個部門的嵌套課程詳細資料。

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)

這會完成排序、篩選和主版詳細資料案例的簡介。 在下一個教學課程中，您將瞭解如何處理平行存取。

> [!div class="step-by-step"]
> [上一頁](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
> [下一頁](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)
