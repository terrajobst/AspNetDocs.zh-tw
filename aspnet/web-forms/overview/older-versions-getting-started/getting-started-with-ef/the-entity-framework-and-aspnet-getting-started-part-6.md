---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-6
title: Entity Framework 4.0 Database First 和 ASP.NET 4 Web form 的消費者入門-第6部分 |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 來建立 ASP.NET Web Forms 應用程式。 範例應用程式為 。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 994a5496-c648-4830-b03c-55bb43f325d2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-6
msc.type: authoredcontent
ms.openlocfilehash: 8bfbe74f90eb03ea9aab7610842ef2578e80d113
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78564222"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-6"></a>Entity Framework 4.0 Database First 和 ASP.NET 4 Web form 的消費者入門-第6部分

由[Tom 作者: dykstra](https://github.com/tdykstra)

> Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 4.0 和 Visual Studio 2010 來建立 ASP.NET Web Forms 應用程式。 如需教學課程系列的資訊，請參閱本[系列的第一個教學](the-entity-framework-and-aspnet-getting-started-part-1.md)課程

## <a name="implementing-table-per-hierarchy-inheritance"></a>實作每個階層的資料表繼承

在上一個教學課程中，您會藉由新增和刪除關聯性，以及加入具有現有實體關聯性的新實體來處理相關資料。 本教學課程將示範如何在資料模型中實作繼承。

在物件導向程式設計中，您可以使用繼承，讓您更輕鬆地使用相關的類別。 例如，您可以建立 `Instructor`，並 `Student` 衍生自 `Person` 基類的類別。 您可以在 Entity Framework 中的實體之間建立相同類型的繼承結構。

在本教學課程的這個部分中，您不會建立任何新的網頁。 相反地，您會將衍生的實體加入至資料模型，並修改現有的頁面以使用新的實體。

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a>每個階層的資料表與每個類型的資料表繼承

資料庫可以將相關物件的資訊儲存在一個資料表或多個資料表中。 例如，在 `School` 資料庫中，`Person` 資料表會在單一資料表中包含學生和講師的相關資訊。 有些資料行僅適用于講師（`HireDate`），部分只有學生（`EnrollmentDate`），而有些則是（`LastName`，`FirstName`）。

[![image11](the-entity-framework-and-aspnet-getting-started-part-6/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image1.png)

您可以設定 Entity Framework 來建立 `Instructor` 和 `Student` 繼承自 `Person` 實體的實體。 從單一資料庫資料表產生實體繼承結構的這種模式稱為「*每個階層的資料表*」（TPH）繼承。

針對課程，`School` 資料庫會使用不同的模式。 線上課程和現場課程會儲存在不同的資料表中，每個都有一個指向 `Course` 資料表的外鍵。 這兩種課程類型通用的資訊只會儲存在 `Course` 資料表中。

[![image12](the-entity-framework-and-aspnet-getting-started-part-6/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image3.png)

您可以設定 Entity Framework 資料模型，讓 `OnlineCourse` 和 `OnsiteCourse` 實體繼承自 `Course` 實體。 這種模式會從每個類型的個別資料表產生實體繼承結構，而每個不同的資料表會參照回一個資料表來儲存所有類型的通用資料，稱為「*資料表/類型*」（TPT）繼承。

在 Entity Framework 中，TPH 繼承模式通常會比 TPT 繼承模式提供更好的效能，因為 TPT 模式可能會導致複雜的聯結查詢。 本逐步解說示範如何執行 TPH 繼承。 您將執行下列步驟來執行此動作：

- 建立衍生自 `Person`的 `Instructor` 和 `Student` 實體類型。
- 將與衍生實體相關的屬性從 `Person` 實體移至衍生的實體。
- 設定衍生類型中屬性的條件約束。
- 將 `Person` 實體設為抽象實體。
- 將每個衍生實體對應至 `Person` 資料表，並指定如何判斷 `Person` 資料列是否代表該衍生類型的條件。

## <a name="adding-instructor-and-student-entities"></a>新增講師和學生實體

開啟 [ <em>SchoolModel</em> ] 檔案，以滑鼠右鍵按一下設計工具中未佔用的區域，選取 [<strong>新增</strong>]，然後選取 [<strong>實體</strong>]<em>。</em>

[![image01](the-entity-framework-and-aspnet-getting-started-part-6/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image5.png)

在 [**加入實體**] 對話方塊中，將實體命名為 `Instructor`，並將其 [**基底類型**] 選項設定為 [`Person`]。

[![image02](the-entity-framework-and-aspnet-getting-started-part-6/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image7.png)

按一下 [確定]。 設計工具會建立衍生自 `Person` 實體的 `Instructor` 實體。 新實體還沒有任何屬性。

[![image03](the-entity-framework-and-aspnet-getting-started-part-6/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image9.png)

重複此程式，建立也衍生自 `Person`的 `Student` 實體。

只有講師擁有雇用日期，因此您必須將該屬性從 `Person` 實體移至 `Instructor` 實體。 在 [`Person`] 實體中，以滑鼠右鍵按一下 `HireDate` 屬性，然後按一下 [**剪**下]。 然後以滑鼠右鍵按一下 `Instructor` 實體中的 [**屬性**]，然後按一下 [**貼**上]。

[![image04](the-entity-framework-and-aspnet-getting-started-part-6/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image11.png)

`Instructor` 實體的雇用日期不可以是 null。 以滑鼠右鍵按一下 [`HireDate`] 屬性，然後按一下 [**屬性**]，然後在 [**屬性**] 視窗中，將 `Nullable` 變更為 [`False`]。

[![image05](the-entity-framework-and-aspnet-getting-started-part-6/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image13.png)

重複此程式，將 `EnrollmentDate` 屬性從 `Person` 實體移至 `Student` 實體。 請確定您也將 [`Nullable`] 設定為 [`EnrollmentDate`] 屬性的 [`False`]。

現在，`Person` 實體只有 `Instructor` 和 `Student` 實體通用的屬性（除了不會移動的導覽屬性以外），實體只能用來做為繼承結構中的基底實體。 因此，您必須確保它永遠不會被視為獨立的實體。 以滑鼠右鍵按一下 [`Person`] 實體，選取 [**屬性**]，然後在 [**屬性**] 視窗中，將 [ **Abstract** ] 屬性的值變更為 [ **True**]。

[![image06](the-entity-framework-and-aspnet-getting-started-part-6/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image15.png)

## <a name="mapping-instructor-and-student-entities-to-the-person-table"></a>將講師和 Student 實體對應至 Person 資料表

現在您需要告訴 Entity Framework 如何區分資料庫中的 `Instructor` 和 `Student` 實體。

以滑鼠右鍵按一下 [`Instructor`] 實體，然後選取 [**資料表對應**]。 在 [**對應詳細資料**] 視窗中，按一下 [**加入資料表或視圖**]，然後選取 [**人員**]。

[![image07](the-entity-framework-and-aspnet-getting-started-part-6/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image17.png)

按一下 [**新增條件**]，然後選取 [**雇用**日期]。

[![image09](the-entity-framework-and-aspnet-getting-started-part-6/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image19.png)

將 [ **Operator** ] 變更為 [ **Is** ]，將 [**值/屬性**] 改為**Not Null**

[![image10](the-entity-framework-and-aspnet-getting-started-part-6/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image21.png)

針對 `Students` 實體重複此程式，指定當 `EnrollmentDate` 的資料行不是 null 時，這個實體會對應到 `Person` 資料表。 然後儲存並關閉資料模型。

建立專案，以建立新的實體做為類別，並在設計工具中提供它們。

## <a name="using-the-instructor-and-student-entities"></a>使用講師和學生實體

當您建立使用學生和講師資料的網頁時，您會將它們系結至 `Person` 實體集，並根據 `HireDate` 或 `EnrollmentDate` 屬性進行篩選，以將傳回的資料限制為學生或講師。 不過，現在當您將每個資料來源控制項系結至 `Person` 實體集時，您可以指定只選取 `Student` 或 `Instructor` 的實體類型。 因為 Entity Framework 知道如何區分 `Person` 實體集中的學生和講師，所以您可以移除手動輸入的 `Where` 屬性設定來執行此動作。

在 Visual Studio 設計工具中，您可以在 [`Configure Data Source` wizard] 的 [ **EntityTypeFilter** ] 下拉式方塊中指定 `EntityDataSource` 控制項應選取的實體類型，如下列範例所示。

[![image13](the-entity-framework-and-aspnet-getting-started-part-6/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image23.png)

在 [**屬性**] 視窗中，您可以移除不再需要的 `Where` 子句值，如下列範例所示。

[![image14](the-entity-framework-and-aspnet-getting-started-part-6/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image25.png)

不過，因為您已將 `EntityDataSource` 控制項的標記變更為使用 `ContextTypeName` 屬性，所以無法在已建立的 `EntityDataSource` 控制項上執行 [**設定資料來源**]。 因此，您將改為變更標記來進行所需的變更。

開啟 [ *student] 頁面。* 在 `StudentsEntityDataSource` 控制項中，移除 `Where` 屬性，並加入 `EntityTypeFilter="Student"` 屬性。 標記現在會類似下列範例：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample1.aspx)]

設定 `EntityTypeFilter` 屬性可確保 `EntityDataSource` 控制項只會選取指定的實體類型。 如果您想要同時取得 `Student` 和 `Instructor` 實體類型，則不會設定這個屬性。 （只有當您使用控制項進行唯讀資料存取時，才可以選擇使用一個 `EntityDataSource` 控制項來抓取多個實體類型。 如果您使用 `EntityDataSource` 控制項來插入、更新或刪除實體，而且它所系結的實體集可以包含多個類型，您只能使用一個實體類型，而您必須設定此屬性。）

針對 `SearchEntityDataSource` 控制項重複此程式，但只移除 `Where` 屬性的部分，其中只會選取 `Student` 實體，而不是完全移除屬性。 控制項的開頭標記現在會如下列範例所示：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample2.aspx)]

執行頁面，確認它的運作方式與之前相同。

[![image15](the-entity-framework-and-aspnet-getting-started-part-6/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image27.png)

更新您在先前的教學課程中建立的下列頁面，使其使用新的 `Student` 並 `Instructor` 實體，而不是 `Person` 實體，然後執行它們以確認其運作方式與之前相同：

- 在*StudentsAdd*中，將 `EntityTypeFilter="Student"` 新增至 `StudentsEntityDataSource` 控制項。 標記現在會類似下列範例： 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample3.aspx)]

    [![image16](the-entity-framework-and-aspnet-getting-started-part-6/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image29.png)
- 在 [*關於 .aspx*] 中，將 `EntityTypeFilter="Student"` 新增至 `StudentStatisticsEntityDataSource` 控制項，並移除 `Where="it.EnrollmentDate is not null"`。 標記現在會類似下列範例： 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample4.aspx)]

    [![image17](the-entity-framework-and-aspnet-getting-started-part-6/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image31.png)
- 在 [ *.aspx* ] 和 [ *InstructorsCourses*] 中，將 `EntityTypeFilter="Instructor"` 新增至 `InstructorsEntityDataSource` 控制項，並移除 `Where="it.HireDate is not null"`。 在*講師*中的標記現在與下列範例類似： 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample5.aspx)]

    [![image18](the-entity-framework-and-aspnet-getting-started-part-6/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image33.png)

    *InstructorsCourses*中的標記現在會如下列範例所示：

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample6.aspx)]

    [![image19](the-entity-framework-and-aspnet-getting-started-part-6/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image35.png)

由於這些變更，您已改善 Contoso 大學應用程式的可維護性，方法有好幾種。 您已將選取和驗證邏輯移出 UI 層（ *.aspx*標記），並使它成為資料存取層的不可或缺部分。 這有助於將您的應用程式程式碼與您未來可能會對資料庫架構或資料模型進行的變更隔離。 例如，您可以決定將學生視為老師的輔助人員，因而取得雇用日期。 然後，您可以加入新的屬性來區分學生與講師，並更新資料模型。 Web 應用程式中的任何程式碼都不需要變更，除非您想要顯示學生的雇用日期。 新增 `Instructor` 和 `Student` 實體的另一個優點是，您的程式碼比參考實際學生或講師的 `Person` 物件更容易理解。

您現在已經看過在 Entity Framework 中執行繼承模式的一種方式。 在下列教學課程中，您將瞭解如何使用預存程式，以便更充分掌控 Entity Framework 如何存取資料庫。

> [!div class="step-by-step"]
> [上一頁](the-entity-framework-and-aspnet-getting-started-part-5.md)
> [下一頁](the-entity-framework-and-aspnet-getting-started-part-7.md)
