---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教學課程：在 ASP.NET MVC 應用程式中使用 EF 讀取相關資料
description: 在本教學課程中，您將讀取並顯示相關資料，也就是 Entity Framework 載入導覽屬性的資料。
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 18cdd896-8ed9-4547-b143-114711e3eafb
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: d804c8dd45ad131949260c85d9d9c6683bfe9646
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445656"
---
# <a name="tutorial-read-related-data-with-ef-in-an-aspnet-mvc-app"></a>教學課程：在 ASP.NET MVC 應用程式中使用 EF 讀取相關資料

在上一個教學課程中，您已完成 School 資料模型。 在本教學課程中，您將讀取並顯示相關資料，也就是 Entity Framework 載入導覽屬性的資料。

下列圖例顯示了您將操作的頁面。

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

[下載已完成的專案](https://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)

> Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 6 Code First 和 Visual Studio 來建立 ASP.NET MVC 5 應用程式。 如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。

在本教學課程中，您將：

> [!div class="checklist"]
> * 了解如何載入相關資料
> * 建立 Courses 頁面
> * 建立 Instructors 頁面

## <a name="prerequisites"></a>先決條件

* [建立更複雜的資料模型](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)

## <a name="learn-how-to-load-related-data"></a>了解如何載入相關資料

Entity Framework 可以透過數種方式將相關資料載入至實體的導覽屬性：

- *消極式載入*。 第一次讀取實體時，不會擷取相關資料。 不過，第一次嘗試存取導覽屬性時，將會自動擷取該導覽屬性所需的資料。 這會導致多個查詢傳送至資料庫，一個用於實體本身，而每次必須取得實體的相關資料。 `DbContext` 類別預設會啟用消極式載入。

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- *積極式載入*。 讀取實體時，將會同時擷取其相關資料。 這通常會導致單一聯結查詢，其可擷取所有需要的資料。 您可以使用 `Include` 方法來指定積極式載入。

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- *明確式載入*。 這類似于消極式載入，不同之處在于您在程式碼中明確地取得相關資料。當您存取導覽屬性時，不會自動進行此動作。 您可以手動載入相關資料，方法是取得實體的物件狀態管理員專案，並針對保留單一實體的屬性呼叫[集合](https://msdn.microsoft.com/library/gg696220(v=vs.103).aspx)、[載入](https://msdn.microsoft.com/library/gg679166(v=vs.103).aspx)方法。 （在下列範例中，如果您想要載入 [系統管理員] 導覽屬性，請將 `Collection(x => x.Courses)` 取代為 `Reference(x => x.Administrator)`）。通常只有在您關閉延遲載入時，才會使用明確載入。

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

因為它們不會立即取得屬性值，所以消極式載入和明確載入也稱為*延後載入*。

### <a name="performance-considerations"></a>效能考量

如果您知道擷取的每個實體需要相關資料，積極式載入通常可以提供最佳效能，因為傳送至資料庫的單一查詢通常比所擷取每個實體的個別查詢更有效率。 例如，在上述範例中，假設每個部門都有十個相關課程。 積極式載入範例只會產生單一（聯結）查詢，以及對資料庫的單一往返行程。 消極式載入和明確載入範例都會導致十個查詢，以及11個對資料庫的往返。 當延遲很高時，資料庫的額外來回行程對效能特別不利。

另一方面，在某些情況下，延遲載入會更有效率。 積極式載入可能會產生非常複雜的聯結，因此 SQL Server 無法有效率地處理。 或者，如果您只需要針對所處理的一組實體子集存取實體的導覽屬性，則消極式載入的執行效果可能較佳，因為積極式載入會抓取比您所需更多的資料。 如果效能嚴重不足，最好先測試這兩種方式的效能，才能做出最好的選擇。

消極式載入可以遮罩會造成效能問題的程式碼。 例如，未指定積極式或明確載入，但處理大量實體並在每個反復專案中使用多個導覽屬性的程式碼，可能會非常沒有效率（因為有許多對資料庫的來回行程）。 在使用內部部署 SQL server 執行良好開發的應用程式，可能會在因為延遲和延遲載入增加而移至 Azure SQL Database 時，發生效能問題。 使用實際的測試負載來分析資料庫查詢，可協助您判斷延遲載入是否合適。 如需詳細資訊，請參閱[揭密 Entity Framework 策略：載入相關資料](https://msdn.microsoft.com/magazine/hh205756.aspx)和[使用 Entity Framework，以減少 SQL Azure 的網路延遲](https://msdn.microsoft.com/magazine/gg309181.aspx)。

### <a name="disable-lazy-loading-before-serialization"></a>序列化前停用消極式載入

如果您在序列化期間讓消極式載入保持啟用狀態，您最後可以查詢的資料會比您預期的還要多。 序列化通常會藉由存取類型實例上的每個屬性來運作。 屬性存取會觸發消極式載入，而那些延遲載入的實體也會序列化。 然後，序列化程式會存取延遲載入之實體的每個屬性，可能會導致更多的延遲載入和序列化。 若要避免這個回合鏈回應，請在序列化實體之前，關閉延遲載入。

序列化也可能會因為 Entity Framework 所使用的 proxy 類別而複雜，如[Advanced 案例教學](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#proxies)課程中所述。

避免序列化問題的其中一種方法是序列化資料傳輸物件（Dto），而不是實體物件，如[使用 WEB API 與 Entity Framework](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-5.md)教學課程中所示。

如果您不使用 Dto，您可以停用消極式載入，並藉由[停用 proxy 建立](https://msdn.microsoft.com/data/jj592886.aspx)來避免 proxy 問題。

以下是停用消極式載入的一些其他[方法](https://msdn.microsoft.com/data/jj574232)：

- 針對特定導覽屬性，當您宣告屬性時，請省略 `virtual` 關鍵字。
- 針對所有導覽屬性，將 `LazyLoadingEnabled` 設定為 `false`，將下列程式碼放入內容類別的函式中：

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="create-a-courses-page"></a>建立 Courses 頁面

`Course` 實體包含一個導覽屬性，其中包含課程所指派之部門的 `Department` 實體。 若要在課程清單中顯示所指派部門的名稱，您需要從 `Course.Department` 導覽屬性中的 `Department` 實體取得 [`Name`] 屬性。

使用您稍早針對 `Student` 控制器執行的 Entity Framework scaffolder，為 `Course` 實體類型建立名為 `CourseController` （非 CoursesController）的控制器，方法是使用**具有 views 的 MVC 5 控制器**的相同選項：

| 設定 | 值 |
| ------- | ----- |
| 模型類別 | 選取 **[課程] （ContosoUniversity）** 。 |
| 資料內容類別 | 選取 **[SchoolCoNtext （ContosoUniversity）** ]。 |
| 控制器名稱 | 輸入*CourseController*。 同樣地，不是以*s* *CoursesController* 。 當您選取 [**課程（ContosoUniversity）** ] 時，會自動填入 [**控制器名稱**] 值。 您必須變更此值。 |

保留其他預設值，並加入控制器。

開啟*Controllers\CourseController.cs* ，並查看 `Index` 方法：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

自動 Scaffolding 已使用 `Department` 方法，針對 `Include` 導覽屬性指定積極式載入。

開啟*Views\Course\Index.cshtml* ，並將範本程式碼取代為下列程式碼。 所做的變更已醒目標示：

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,7,14-16,23-25,31-33,40-42)]

您已對包含 Scaffold 的程式碼進行下列變更：

- 已將標題從 [**索引**] 變更為 [**課程**]。
- 新增顯示  **屬性值的 [編號]** `CourseID` 資料行。 根據預設，主要金鑰不會 scaffold，因為它們通常對一般使用者來說毫無意義。 不過，在此情況下主索引鍵有意義，因此您想要顯示它。
- 將 [**部門**] 資料行移至右側，並變更其標題。 Scaffolder 正確地選擇要從 `Department` 實體顯示 `Name` 屬性，但在課程頁面中，資料行標題應該是**部門**，而不是**名稱**。

請注意，對於 [部門] 資料行，scaffold 程式碼會顯示載入 `Department` 導覽屬性之 `Department` 實體的 `Name` 屬性：

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=2)]

執行頁面（選取 Contoso 大學首頁上的 [**課程**] 索引標籤），以查看具有部門名稱的清單。

## <a name="create-an-instructors-page"></a>建立 Instructors 頁面

在本節中，您將建立 `Instructor` 實體的控制器和視圖，以便顯示講師頁面。 此頁面將以下列方式讀取和顯示相關資料：

- 講師清單會顯示來自 `OfficeAssignment` 實體的相關資料。 `Instructor` 與 `OfficeAssignment` 實體具有一對零或一關聯性。 您將針對 `OfficeAssignment` 的實體使用積極式載入。 如上所述，當您需要主要資料表中所有擷取資料列的相關資料時，積極式載入通常更有效率。 在此情況下，您可能想要顯示所有已呈現講師的辦公室指派。
- 當使用者選取講師時，將會顯示相關的 `Course` 實體。 `Instructor` 與 `Course` 實體具有多對多關聯性。 您將針對 `Course` 實體和其相關的 `Department` 實體使用積極式載入。 在此情況下，消極式載入可能會更有效率，因為您只需要所選講師的課程。 不過，這個範例會示範如何在本身處於導覽屬性內的實體中，針對導覽屬性使用積極式載入。
- 當使用者選取課程時，會顯示來自 `Enrollments` 實體集的相關資料。 `Course` 與 `Enrollment` 實體具有一對多關聯性。 您將為 `Enrollment` 實體和其相關的 `Student` 實體新增明確的載入。 （不需要明確載入，因為已啟用消極式載入，但這會顯示如何執行明確載入）。

### <a name="create-a-view-model-for-the-instructor-index-view"></a>建立講師索引視圖的視圖模型

講師頁面會顯示三個不同的資料表。 因此，您將建立包含三個屬性的檢視模型，每個保留其中一個資料表的資料。

在*viewmodel*資料夾中，建立*InstructorIndexData.cs* ，並將現有的程式碼取代為下列程式碼：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="create-the-instructor-controller-and-views"></a>建立講師控制器和 Views

使用 EF 讀取/寫入動作來建立 `InstructorController` （非 InstructorsController）控制器：

| 設定 | 值 |
| ------- | ----- |
| 模型類別 | 選取 **[講師（ContosoUniversity）** ]。 |
| 資料內容類別 | 選取 **[SchoolCoNtext （ContosoUniversity）** ]。 |
| 控制器名稱 | 輸入*InstructorController*。 同樣地，不是以*s* *InstructorsController* 。 當您選取 [**課程（ContosoUniversity）** ] 時，會自動填入 [**控制器名稱**] 值。 您必須變更此值。 |

保留其他預設值，並加入控制器。

開啟*Controllers\InstructorController.cs* ，並加入 `ViewModels` 命名空間的 `using` 語句：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

`Index` 方法中的 scaffold 程式碼只會針對 `OfficeAssignment` 導覽屬性指定積極式載入：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

將 `Index` 方法取代為下列程式碼，以載入其他相關資料，並將其放在視圖模型中：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

方法會接受選擇性的路由資料（`id`）和查詢字串參數（`courseID`），以提供所選講師和所選課程的識別碼值，並將所有必要的資料傳遞給視圖。 這些參數由頁面上的**選取**超連結提供。

此程式碼是從建立檢視模型的執行個體，並將其置於講師清單開始。 此程式碼會針對 `Instructor.OfficeAssignment` 和 `Instructor.Courses` 導覽屬性指定積極式載入。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs?highlight=3-4)]

第二個 `Include` 方法會載入課程，而針對載入的每個課程，會針對 `Course.Department` 導覽屬性進行積極式載入。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

如先前所述，不需要積極式載入，但會完成以改善效能。 由於此視圖一律需要 `OfficeAssignment` 實體，因此在相同的查詢中提取該專案會更有效率。 當您在網頁中選取講師時，需要 `Course` 實體，因此，只有在選取的課程比 [沒有] 時，才會顯示 [僅限消極式載入]。

如果選取了講師識別碼，則會從視圖模型中的講師清單中抓取選取的講師。 然後會從該講師的 `Courses` 導覽屬性中，使用 `Course` 實體載入視圖模型的 `Courses` 屬性。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

`Where` 方法會傳回集合，但在此情況下，傳遞至該方法的準則只會傳回單一 `Instructor` 的實體。 `Single` 方法會將集合轉換成單一 `Instructor` 實體，讓您存取該實體的 `Courses` 屬性。

當您知道集合只會有一個專案時，您可以在集合上使用[單一](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx)方法。 如果傳遞給它的集合是空的或有一個以上的專案，`Single` 方法會擲回例外狀況。 替代方案是[SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx)，如果集合是空的，則會傳回預設值（在此案例中為`null`）。 不過，在此情況下，仍然會導致例外狀況（嘗試尋找 `null` 參考上的 `Courses` 屬性），而例外狀況訊息則不會清楚指出問題的原因。 當您呼叫 `Single` 方法時，您也可以傳入 `Where` 條件，而不是分別呼叫 `Where` 方法：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]

而非：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

接下來，如果已選取課程，則會從檢視模型的課程清單中擷取選取的課程。 然後，視圖模型的 `Enrollments` 屬性會與該課程 `Enrollments` 導覽屬性中的 `Enrollment` 實體一併載入。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

### <a name="modify-the-instructor-index-view"></a>修改講師索引視圖

在*Views\Instructor\Index.cshtml*中，將範本程式碼取代為下列程式碼。 所做的變更已醒目標示：

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1,4,14-18,21,23-28,38-43,45)]

您已對現有程式碼進行下列變更：

- 已將模型類別變更為 `InstructorIndexData`。
- 已將頁面標題從**索引**變更為**講師**。
- 已新增 [ **Office** ] 資料行，只有在 `item.OfficeAssignment` 不是 null 時，才會顯示 `item.OfficeAssignment.Location`。 （因為這是一對零或一種關聯性，所以可能不會有相關的 `OfficeAssignment` 實體）。

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]
- 新增程式碼，以動態方式將 `class="success"` 新增至所選講師的 `tr` 元素。 這會使用[啟動](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap)程式類別設定所選取資料列的背景色彩。

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]
- 在每個資料列的其他連結前面加上標示為 [**選取**] 的新 `ActionLink`，這會導致選取的講師識別碼傳送至 `Index` 方法。

執行應用程式，然後選取 [**講師**] 索引標籤。當沒有相關的 `OfficeAssignment` 實體時，此頁面會顯示相關 `OfficeAssignment` 實體的 `Location` 屬性和空的資料表單元格。

在*Views\Instructor\Index.cshtml*檔案中，于結尾 `table` 專案（在檔案結尾）後面，加入下列程式碼。 當選取講師時，此程式碼會顯示與講師相關的課程。

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

此程式碼會讀取檢視模型的 `Courses` 屬性以顯示課程清單。 它也會提供 `Select` 超連結，將所選課程的識別碼傳送至 `Index` 動作方法。

執行頁面，然後選取講師。 現在您會看到一個方格，其中顯示指派給所選取講師的課程，而且在每個課程中，您可以看到指派的部門名稱。

在您剛才新增的程式碼區塊之後，新增下列程式碼。 這會在選取課程時，顯示已註冊該課程的學生清單。

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

此程式碼會閱讀檢視模型的 `Enrollments` 屬性，以顯示課程中註冊的學生清單。

執行頁面，然後選取講師。 接著選取課程，以查看已註冊學生和其年級的清單。

### <a name="adding-explicit-loading"></a>新增明確載入

開啟*InstructorController.cs* ，並查看 `Index` 方法如何取得所選課程的註冊清單：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

當您抓取講師清單時，您已針對 `Courses` 導覽屬性和每個課程的 `Department` 屬性指定積極式載入。 然後將 `Courses` 集合放在視圖模型中，現在您就可以從該集合中的一個實體存取 `Enrollments` 導覽屬性。 因為您未指定 `Course.Enrollments` 導覽屬性的積極式載入，所以該屬性中的資料會因為消極式載入而出現在頁面中。

如果您停用消極式載入，而未以其他方式變更程式碼，則不論該課程實際擁有多少註冊，`Enrollments` 屬性都會是 null。 在這種情況下，若要載入 `Enrollments` 屬性，您必須指定積極式載入或明確載入。 您已經瞭解如何執行積極式載入。 若要查看明確載入的範例，請以下列程式碼取代 `Index` 方法，這會明確載入 `Enrollments` 屬性。 變更的程式碼會反白顯示。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs?highlight=20-31)]

取得選取的 `Course` 實體之後，新的程式碼會明確載入該課程的 `Enrollments` 導覽屬性：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

然後，它會明確載入每個 `Enrollment` 實體的相關 `Student` 實體：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

請注意，您可以使用 `Collection` 方法載入集合屬性，但對於只保存一個實體的屬性，您可以使用 `Reference` 方法。

立即執行 [講師索引] 頁面，您會看到頁面上顯示的內容沒有任何差異，雖然您已變更資料的抓取方式。

## <a name="get-the-code"></a>取得程式碼

[下載已完成的專案](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>其他資源

您可以在[ASP.NET 資料存取-建議的資源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您將：

> [!div class="checklist"]
> * 了解如何載入相關資料
> * 建立 Courses 頁面
> * 建立 Instructors 頁面

若要了解如何更新相關資料，請前往下一篇文章。

> [!div class="nextstepaction"]
> [更新相關資料](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
