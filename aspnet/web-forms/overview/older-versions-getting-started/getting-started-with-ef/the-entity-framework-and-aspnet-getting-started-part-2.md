---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2
title: 具有 Entity Framework 4.0 Database First 和 ASP.NET 4 Web form 的消費者入門-第2部分 |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 來建立 ASP.NET Web Forms 應用程式。 範例應用程式為 。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: fb63a326-a4ae-4b0c-a4f5-412327197216
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2
msc.type: authoredcontent
ms.openlocfilehash: bd6a2e29e6f0df04e39be29160e2e08cc99c4706
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78566007"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-2"></a>Entity Framework 4.0 Database First 和 ASP.NET 4 Web form 的消費者入門-第2部分

由[Tom 作者: dykstra](https://github.com/tdykstra)

> Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 4.0 和 Visual Studio 2010 來建立 ASP.NET Web Forms 應用程式。 如需教學課程系列的資訊，請參閱本[系列的第一個教學](the-entity-framework-and-aspnet-getting-started-part-1.md)課程

## <a name="the-entitydatasource-control"></a>EntityDataSource 控制項

在上一個教學課程中，您建立了網站、資料庫和資料模型。 在本教學課程中，您會使用 ASP.NET 所提供的 `EntityDataSource` 控制項，以便輕鬆地使用 Entity Framework 資料模型。 您將建立一個 `GridView` 控制項，用於顯示和編輯學生資料、用來新增學生的 `DetailsView` 控制項，以及用於選取部門的 `DropDownList` 控制項（您稍後會用來顯示相關課程）。

[![Image20](the-entity-framework-and-aspnet-getting-started-part-2/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image1.png)

[![Image09](the-entity-framework-and-aspnet-getting-started-part-2/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image3.png)

[![Image18](the-entity-framework-and-aspnet-getting-started-part-2/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image5.png)

請注意，在此應用程式中，您不會在更新資料庫的頁面上加入輸入驗證，而且某些錯誤處理將不會像實際執行應用程式中所需的一樣健全。 這會讓教學課程專注于 Entity Framework，並讓它不會太久。 如需如何將這些功能新增至應用程式的詳細資訊，請參閱在[ASP.NET 網頁和應用程式](https://msdn.microsoft.com/library/w16865z6.aspx)中[驗證使用者輸入 ASP.NET Web Pages](https://msdn.microsoft.com/library/7kh55542.aspx)和錯誤處理。

## <a name="adding-and-configuring-the-entitydatasource-control"></a>加入和設定 EntityDataSource 控制項

首先，設定 `EntityDataSource` 控制項，從 `People` 實體集讀取 `Person` 的實體。

請確定您已開啟 Visual Studio，而且您正在使用第1部分中所建立的專案。 如果您在建立資料模型之後，或自從上次變更後尚未建立專案，請立即建立專案。 在建立專案之前，不會將資料模型的變更提供給設計工具。

使用**使用主版頁面範本的 Web 表單**建立新的網頁，並將其命名為*default.aspx*。

[![Image23](the-entity-framework-and-aspnet-getting-started-part-2/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image7.png)

指定 [*網站*] 作為主版頁面。 您為這些教學課程建立的所有頁面都會使用此主版頁面。

[![Image24](the-entity-framework-and-aspnet-getting-started-part-2/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image9.png)

在 [**來源**視圖] 中，將 `h2` 標題新增至名為 `Content2`的 `Content` 控制項，如下列範例所示：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample1.aspx)]

從 [**工具箱**] 的 [**資料**] 索引標籤中，將 [`EntityDataSource`] 控制項拖曳至頁面，並將其放在標題下方，然後將識別碼變更為 `StudentsEntityDataSource`：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample2.aspx)]

切換至 [**設計**視圖]，按一下資料來源控制項的智慧標籤，然後按一下 [**設定資料來源**] 以啟動 [**設定資料來源**]。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-2/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image11.png)

在 [**設定 ObjectCoNtext** wizard] 步驟中，選取 [ **SchoolEntities** ] 作為 [**已命名的連接**] 的值，然後選取 [ **SchoolEntities** ] 做為**DefaultContainerName**值。 然後按一下 [下一步]。

[![Image02](the-entity-framework-and-aspnet-getting-started-part-2/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image13.png)

注意：如果此時會出現下列對話方塊，您必須先建立專案，然後再繼續進行。

[![Image25](the-entity-framework-and-aspnet-getting-started-part-2/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image15.png)

在 [**設定資料選擇**] 步驟中，選取 [**人員**] 做為**EntitySetName**的值。 在 [**選取**] 下，確定已選取 [**選取**ll] 核取方塊。 然後選取選項以啟用 [更新] 和 [刪除]。 當您完成時，請按一下 **[完成]** 。

[![Image03](the-entity-framework-and-aspnet-getting-started-part-2/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image17.png)

## <a name="configuring-database-rules-to-allow-deletion"></a>設定資料庫規則以允許刪除

您將會建立一個頁面，讓使用者從 `Person` 資料表中刪除學生，這與其他資料表有三個關聯性（`Course`、`StudentGrade`和 `OfficeAssignment`）。 根據預設，如果其中一個其他資料表中有相關資料列，資料庫將會防止您刪除 `Person` 中的資料列。 您可以先手動刪除相關資料列，或將資料庫設定為在您刪除 `Person` 的資料列時，自動將它們刪除。 對於本教學課程中的學生記錄，您會將資料庫設定為自動刪除相關資料。 因為學生只能在 `StudentGrade` 資料表中擁有相關的資料列，所以您只需要設定這三個關聯性的其中一個。

如果您使用的是從本教學課程中的專案下載的*School*檔案，則可以略過本節，因為這些設定變更已經完成。 如果您藉由執行腳本來建立資料庫，請執行下列程式來設定資料庫。

在**伺服器總管**中，開啟您在第1部分建立的資料庫關係圖。 以滑鼠右鍵按一下 `Person` 和 `StudentGrade` 之間的關聯性（資料表之間的線條），然後選取 [**屬性**]。

[![Image04](the-entity-framework-and-aspnet-getting-started-part-2/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image19.png)

在 [**屬性**] 視窗中，展開 [**插入和更新規格**]，並將 [ **DeleteRule** ] 屬性設定為 [ **Cascade**]。

[![Image05](the-entity-framework-and-aspnet-getting-started-part-2/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image21.png)

儲存並關閉圖表。 如果系統詢問您是否要更新資料庫，請按一下 **[是]** 。

若要確保模型會將記憶體中的實體與資料庫所執行的作業保持同步，您必須在資料模型中設定對應的規則。 開啟*SchoolModel*，以滑鼠右鍵按一下 `Person` 和 `StudentGrade`之間的關聯線，然後選取 [**屬性**]。

[![Image21](the-entity-framework-and-aspnet-getting-started-part-2/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image23.png)

在 [**屬性**] 視窗中，將 [ **End1 OnDelete** ] 設定為 [ **Cascade**]。

[![Image22](the-entity-framework-and-aspnet-getting-started-part-2/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image25.png)

儲存並關閉*SchoolModel .edmx*檔案，然後重建專案。

一般而言，當資料庫變更時，您會有數個選項可讓您瞭解如何同步處理模型：

- 針對特定種類的變更（例如，加入或重新整理資料表、views 或預存程式），在設計工具中按一下滑鼠右鍵，然後選取 [**從資料庫更新模型**]，讓設計工具自動進行變更。
- 重新產生資料模型。
- 進行手動更新，例如這一項。

在此情況下，您可能已重新產生模型，或重新整理受到關聯性變更影響的資料表，但是您必須再次變更功能變數名稱（從 `FirstName` 到 `FirstMidName`）。

## <a name="using-a-gridview-control-to-read-and-update-entities"></a>使用 GridView 控制項來讀取和更新實體

在本節中，您將使用 `GridView` 控制項來顯示、更新或刪除學生。

開啟或切換至 [student] *，並切換至 [* **設計**視圖]。 從 [**工具箱**] 的 [**資料**] 索引標籤中，將 [`GridView`] 控制項拖曳至 [`EntityDataSource`] 控制項的右邊，將它命名為 `StudentsGridView`，按一下智慧標籤，然後選取 [ **StudentsEntityDataSource** ] 做為資料來源。

[![Image06](the-entity-framework-and-aspnet-getting-started-part-2/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image27.png)

按一下 [重新整理**架構**] （如果系統提示您確認，請按一下 **[是]** ），然後按一下 [**啟用分頁**]、**啟用排序**、**啟用編輯**，以及**啟用刪除**。

按一下 [**編輯資料行**]。

[![Image10](the-entity-framework-and-aspnet-getting-started-part-2/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image29.png)

在 [**選取的欄位**] 方塊中，刪除**PersonID**、 **LastName**和**雇用**項。 您通常不會向使用者顯示記錄金鑰，雇用日期與學生無關，而且您會將這兩個部分的名稱放在一個欄位中，因此您只需要其中一個 [名稱] 欄位）。

[![Image11](the-entity-framework-and-aspnet-getting-started-part-2/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image31.png)

選取 [ **firstmidname 變更**] 欄位，然後按一下 [**將此欄位轉換成 TemplateField**]。

對**EnrollmentDate**執行相同的動作。

[![Image13](the-entity-framework-and-aspnet-getting-started-part-2/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image33.png)

按一下 **[確定]** ，然後切換至 [**來源**視圖]。 其餘的變更將更容易直接在標記中執行。 `GridView` 控制項標記現在看起來如下列範例所示。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample3.aspx)]

命令欄位之後的第一個資料行是目前顯示名字的範本欄位。 變更此範本欄位的標記，看起來如下列範例所示：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample4.aspx)]

在顯示模式中，兩個 `Label` 控制項會顯示第一個和最後一個名稱。 在編輯模式中，會提供兩個文字方塊，讓您可以變更第一個和最後一個名稱。 如同 [顯示模式] 中的 `Label` 控制項，您可以使用 `Bind` 和 `Eval` 運算式，與直接連接到資料庫的 ASP.NET 資料來源控制項相同。 唯一的差別在於您是指定實體屬性，而不是資料庫資料行。

最後一個資料行是顯示註冊日期的範本欄位。 變更此欄位的標記，看起來如下列範例所示：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample5.aspx)]

在顯示和編輯模式中，格式字串 "{0，d}" 會使日期以「簡短日期」格式顯示。 （您的電腦可能會設定為以不同于本教學課程中所顯示的螢幕影像來顯示此格式）。

請注意，在這些範本欄位中，設計工具預設會使用 `Bind` 運算式，但您已將其變更為 `ItemTemplate` 元素中的 `Eval` 運算式。 `Bind` 運算式會在您需要存取程式碼中的資料時，將資料提供給 `GridView` 控制項屬性。 在此頁面中，您不需要在程式碼中存取這項資料，因此您可以使用 `Eval`，這會更有效率。 如需詳細資訊，請參閱[從資料控制處取得資料](https://weblogs.asp.net/davidfowler/archive/2008/12/12/getting-your-data-out-of-the-data-controls.aspx)。

## <a name="revising-entitydatasource-control-markup-to-improve-performance"></a>修訂 EntityDataSource 控制項標記以改善效能

在 `EntityDataSource` 控制項的標記中，移除 `ConnectionString` 和 `DefaultContainerName` 屬性，並以 `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"` 屬性加以取代。 這是您每次建立 `EntityDataSource` 控制項時應該進行的變更，除非您需要使用與在物件內容類別中硬式編碼的連線不同的連接。 使用 `ContextTypeName` 屬性可提供下列優點：

- 效能較佳。 當 `EntityDataSource` 控制項使用 `ConnectionString` 和 `DefaultContainerName` 屬性來初始化資料模型時，它會執行額外的工作，以在每個要求上載入中繼資料。 如果您指定 `ContextTypeName` 屬性，就不需要這麼做。
- 在 Entity Framework 4.0 中，產生的物件內容類別別（如本教學課程中的 `SchoolEntities`）預設會開啟消極式載入。 這表示當您需要時，導覽屬性會自動載入相關的資料。 稍後會在本教學課程中詳細說明消極式載入。
- 您已套用至物件內容類別的任何自訂（在此案例中為 `SchoolEntities` 類別）都會提供給使用 `EntityDataSource` 控制項的控制項。 自訂物件內容類別是本教學課程系列中未涵蓋的一個「高級」主題。 如需詳細資訊，請參閱[擴充 Entity Framework 產生的類型](https://msdn.microsoft.com/library/dd456844.aspx)。

標記現在會類似下列範例（屬性的順序可能會不同）：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample6.aspx)]

`EnableFlattening` 屬性指的是舊版 Entity Framework 所需的功能，因為外鍵資料行並未公開為實體屬性。 目前的版本可讓您使用*外鍵關聯*，這表示會針對所有但多對多關聯公開外鍵屬性。 如果您的實體具有外鍵屬性，而且沒有[複雜類型](https://msdn.microsoft.com/library/bb738472.aspx)，您可以將此屬性設定為 `False`。 請勿移除標記中的屬性，因為預設值為 `True`。 如需詳細資訊，請參閱簡維[物件（EntityDataSource）](https://msdn.microsoft.com/library/ee404746.aspx)。

執行頁面，您會看到一份學生和員工清單（在下一個教學課程中，您只會針對學生進行篩選）。 [名字] 和 [姓氏] 會一起顯示。

[![Image07](the-entity-framework-and-aspnet-getting-started-part-2/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image35.png)

若要排序顯示，請按一下 [資料行名稱]。

按一下任何資料列中的 [**編輯**]。 文字方塊隨即顯示，您可以在其中變更第一個和最後一個名稱。

[![Image08](the-entity-framework-and-aspnet-getting-started-part-2/_static/image38.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image37.png)

[**刪除**] 按鈕也可以運作。 針對具有註冊日期的資料列，按一下 [刪除]，然後資料列就會消失。 （沒有註冊日期的資料列代表講師，而您可能會收到參考完整性錯誤。 在下一個教學課程中，您將篩選這份清單，只包含學生。）

## <a name="displaying-data-from-a-navigation-property"></a>顯示導覽屬性中的資料

現在假設您想要知道每個學生註冊的課程數。 Entity Framework 會在 `Person` 實體的 `StudentGrades` 導覽屬性中提供該資訊。 因為資料庫設計不允許學生在沒有指派等級的課程中註冊，所以在本教學課程中，您可以假設 `StudentGrade` 資料表資料列中有一個與課程相關聯的資料列與在課程中註冊的相同。 （`Courses` 導覽屬性僅適用于講師）。

當您使用 `EntityDataSource` 控制項的 `ContextTypeName` 屬性時，Entity Framework 會在您存取該屬性時，自動捕獲導覽屬性的資訊。 這稱為「*延遲載入*」。 不過，這可能會造成效率不佳，因為它會在每次需要額外的資訊時，個別呼叫資料庫。 如果您需要 `EntityDataSource` 控制項所傳回之每個實體的導覽屬性中的資料，在資料庫的單一呼叫中，將相關資料和實體本身一併抓取會更有效率。 這稱為「*積極式載入*」，您可以藉由設定 `EntityDataSource` 控制項的 [`Include`] 屬性，指定導覽屬性的積極式載入。

在 [student]*中，您*想要顯示每個學生的課程數，因此積極式載入是最佳選擇。 如果您是顯示所有學生，但只顯示其中幾個課程的課程數（除了標記以外，需要撰寫一些程式碼），則消極式載入可能是較佳的選擇。

開啟或切換至 [student *]，切換至 [* **設計**視圖]，選取 [`StudentsEntityDataSource`]，然後在 [**屬性**] 視窗中，將 [**包含**] 屬性設定為 [ **StudentGrades**]。 （如果您想要取得多個導覽屬性，您可以指定以逗號分隔的名稱，例如**StudentGrades、課程**）。

[![Image19](the-entity-framework-and-aspnet-getting-started-part-2/_static/image40.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image39.png)

切換至**來源**視圖。 在 [`StudentsGridView`] 控制項中，于最後一個 `asp:TemplateField` 元素之後，新增下列 [新範本] 欄位：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample7.aspx)]

在 `Eval` 運算式中，您可以參考 `StudentGrades`的導覽屬性。 因為這個屬性包含一個集合，所以它有一個 `Count` 屬性，可讓您用來顯示學生註冊的課程數目。 在稍後的教學課程中，您將瞭解如何從包含單一實體而不是集合的導覽屬性顯示資料。 （請注意，您無法使用 `BoundField` 元素來顯示導覽屬性中的資料）。

執行頁面，您現在會看到每個學生註冊的課程數。

[![Image20](the-entity-framework-and-aspnet-getting-started-part-2/_static/image42.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image41.png)

## <a name="using-a-detailsview-control-to-insert-entities"></a>使用 DetailsView 控制項插入實體

下一步是建立一個頁面，其中具有 `DetailsView` 控制項，可讓您新增學生。 關閉瀏覽器，然後使用 [*網站*] 主版頁面建立新的網頁。 將頁面命名為*StudentsAdd*，然後切換至 [**來源**視圖]。

新增下列標記，以取代名為 `Content2`之 `Content` 控制項的現有標記：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample8.aspx)]

此標記會建立一個與您在 student 中建立的 `EntityDataSource` 控制項類似 *，但*它會啟用插入。 就像 `GridView` 控制項一樣，`DetailsView` 控制項的系結欄位的編碼方式，與直接連接到資料庫的資料控制項相同，不同之處在于它們會參考實體屬性。 在此情況下，`DetailsView` 控制項只會用於插入資料列，因此您必須將預設模式設定為 [`Insert`]。

執行頁面並加入新的學生。

[![Image09](the-entity-framework-and-aspnet-getting-started-part-2/_static/image44.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image43.png)

當您插入新的學生之後，就不會發生任何事，但如果您現在執行了 student *.aspx*，就會看到新的學生資訊。

## <a name="displaying-data-in-a-drop-down-list"></a>在下拉式清單中顯示資料

在下列步驟中，您會使用 `EntityDataSource` 控制項，將 `DropDownList` 控制項進行程式化至實體集。 在本教學課程的這個部分中，您不會對此清單執行太多動作。 不過，在後續的部分中，您將使用清單讓使用者選取一個部門，以顯示與該部門相關聯的課程。

建立名為「*課程 .aspx*」的新網頁。 在 [**來源**視圖] 中，將標題新增至名為 `Content2`的 `Content` 控制項：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample9.aspx)]

在**設計**視圖中，如同之前一樣將 `EntityDataSource` 控制項加入至頁面，但這段時間名稱 `DepartmentsEntityDataSource`。 選取 [**部門**] 做為**EntitySetName**值，然後只選取 [ **DepartmentID** ] 和 [ **Name** ] 屬性。

[![Image15](the-entity-framework-and-aspnet-getting-started-part-2/_static/image46.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image45.png)

從 [**工具箱**] 的 [**標準**] 索引標籤中，將 [`DropDownList`] 控制項拖曳至頁面，將其命名為 `DepartmentsDropDownList`，按一下智慧標籤，然後選取 **[選擇資料來源**] 以啟動 [ **DataSource 設定向導]** 。

[![Image16](the-entity-framework-and-aspnet-getting-started-part-2/_static/image48.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image47.png)

在 [**選擇資料來源**] 步驟中，選取 [ **DepartmentsEntityDataSource** ] 做為資料來源，按一下 [重新整理**架構**]，然後選取 [**名稱**] 做為要顯示的資料欄位，並**DepartmentID**為 [數值資料] 欄位。 按一下 [確定]。

[![Image17](the-entity-framework-and-aspnet-getting-started-part-2/_static/image50.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image49.png)

您用來利用 Entity Framework 來資料繫結控制項的方法，與其他 ASP.NET 資料來源控制項相同，但您指定的是實體和實體屬性。

切換至 [**來源**視圖]，並在 `DropDownList` 控制項之前新增 [選取部門：]。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample10.aspx)]

提醒您，您可以使用 `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"` 屬性來取代 `ConnectionString` 和 `DefaultContainerName` 屬性，以變更 `EntityDataSource` 控制項的標記。 在您變更 `EntityDataSource` 控制項標記之前，最好等到建立連結至資料來源控制項的資料繫結控制項，因為在進行變更之後，設計工具不會在資料繫結控制項中提供 [重新整理**架構**] 選項。

執行頁面，您可以從下拉式清單中選取部門。

[![Image18](the-entity-framework-and-aspnet-getting-started-part-2/_static/image52.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image51.png)

這會完成使用 `EntityDataSource` 控制項的簡介。 使用此控制項通常與使用其他 ASP.NET 資料來源控制項不同，但您參考的是實體和屬性，而不是資料表和資料行。 唯一的例外是當您想要存取導覽屬性時。 在下一個教學課程中，您會發現，當您篩選、分組和排序資料時，與 `EntityDataSource` 控制項搭配使用的語法可能也會與其他資料來源控制項不同。

> [!div class="step-by-step"]
> [上一頁](the-entity-framework-and-aspnet-getting-started-part-1.md)
> [下一頁](the-entity-framework-and-aspnet-getting-started-part-3.md)
