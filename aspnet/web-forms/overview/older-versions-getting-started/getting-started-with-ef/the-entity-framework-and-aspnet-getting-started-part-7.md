---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
title: Entity Framework 4.0 Database First 和 ASP.NET 4 Web form 的消費者入門-第7部分 |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 來建立 ASP.NET Web Forms 應用程式。 範例應用程式為 。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: f8afb245-b705-419c-8790-0b295e90d5e2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
msc.type: authoredcontent
ms.openlocfilehash: 18d4b44c5e23fd6942c3adf48a33a5602e6df6d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78603429"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-7"></a>Entity Framework 4.0 Database First 和 ASP.NET 4 Web form 的消費者入門-第7部分

由[Tom 作者: dykstra](https://github.com/tdykstra)

> Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 4.0 和 Visual Studio 2010 來建立 ASP.NET Web Forms 應用程式。 如需教學課程系列的資訊，請參閱本[系列的第一個教學](the-entity-framework-and-aspnet-getting-started-part-1.md)課程

## <a name="using-stored-procedures"></a>使用預存程序

在上一個教學課程中，您已執行每個階層的資料表繼承模式。 本教學課程將示範如何使用預存程式，對資料庫存取進行更多的控制。

Entity Framework 可讓您指定它應該使用預存程式來存取資料庫。 針對任何實體類型，您可以指定用來建立、更新或刪除該類型實體的預存程式。 然後在資料模型中，您可以加入預存程式的參考，以便用來執行工作，例如，抓取實體集。

使用預存程式是資料庫存取的常見需求。 在某些情況下，資料庫管理員可能會要求所有的資料庫存取都必須經過預存程式，以確保安全性。 在其他情況下，您可能會想要將商務邏輯建立到 Entity Framework 在更新資料庫時所使用的部分程式。 例如，每當刪除實體時，您可能會想要將它複製到封存資料庫。 或者，每次更新資料列時，您可能會想要將資料列寫入記錄資料表中，以記錄進行變更的人員。 您可以在每次 Entity Framework 刪除實體或更新實體時所呼叫的預存程式中執行這類工作。

如同在上一個教學課程中，您不會建立任何新的頁面。 相反地，您會變更 Entity Framework 針對您已建立的某些頁面存取資料庫的方式。

在本教學課程中，您將在資料庫中建立預存程式，以插入 `Student` 和 `Instructor` 實體。 您會將它們加入至資料模型，並指定 Entity Framework 應該使用它們來將 `Student` 和 `Instructor` 實體加入至資料庫。 您也會建立可用來抓取 `Course` 實體的預存程式。

## <a name="creating-stored-procedures-in-the-database"></a>在資料庫中建立預存程式

（如果您使用此教學課程可供下載之專案中的*School .mdf*檔案，則可以略過本節，因為預存程式已經存在）。

在**伺服器總管**中，展開 [ *School*]，以滑鼠右鍵按一下 [**預存程式**]，然後選取 [**加入新的預存**程式]。

[![image15](the-entity-framework-and-aspnet-getting-started-part-7/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image1.png)

複製下列 SQL 語句，並將其貼入 [預存程式] 視窗中，並取代基本架構預存程式。

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample1.sql)]

[![image14](the-entity-framework-and-aspnet-getting-started-part-7/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image3.png)

`Student` 實體具有四個屬性： `PersonID`、`LastName`、`FirstName`和 `EnrollmentDate`。 資料庫會自動產生識別碼值，而預存程式會接受其他三個參數。 預存程式會傳回新資料列記錄索引鍵的值，讓 Entity Framework 可以追蹤它保留在記憶體中的實體版本。

儲存並關閉 [預存程式] 視窗。

使用下列 SQL 語句，以相同的方式建立 `InsertInstructor` 預存程式：

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample2.sql)]

同時為 `Student` 和 `Instructor` 實體建立 `Update` 預存程式。 （資料庫已經有 `DeletePerson` 預存程式，可同時適用于 `Instructor` 和 `Student` 實體）。

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample3.sql)]

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample4.sql)]

在本教學課程中，您將會對應每個實體類型的所有三個函式--insert、update 和 delete。 Entity Framework 版本4可讓您只將其中一個或兩個函式對應至預存程式，而不需要對應其他函式，但有一個例外：如果您對應 update 函式，而不是 delete 函式，則 Entity Framework 會在您嘗試刪除實體。 在 Entity Framework 版本3.5 中，您在對應預存程式中沒有這麼大的彈性：如果您對應了一個函式，則必須對應這三個函數。

若要建立可讀取而不是更新資料的預存程式，請使用下列 SQL 語句建立一個選取所有 `Course` 實體的儲存程式：

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample5.sql)]

## <a name="adding-the-stored-procedures-to-the-data-model"></a>將預存程式加入至資料模型

預存程式現在已在資料庫中定義，但必須加入至資料模型，才能供 Entity Framework 使用。 開啟*SchoolModel*，以滑鼠右鍵按一下設計介面，然後選取 [**從資料庫更新模型**]。 在 [**選擇您的資料庫物件**] 對話方塊的 [**加入**] 索引標籤中，展開 [**預存程式**]，選取新建立的預存程式和 `DeletePerson` 預存程式，然後按一下 **[完成**]。

[![image20](the-entity-framework-and-aspnet-getting-started-part-7/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image5.png)

## <a name="mapping-the-stored-procedures"></a>對應預存程式

在 [資料模型設計師] 中，以滑鼠右鍵按一下 [`Student`] 實體，然後選取 [**預存程式對應**]。

[![image21](the-entity-framework-and-aspnet-getting-started-part-7/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image7.png)

[**對應詳細資料**] 視窗隨即出現，您可以在其中指定 Entity Framework 應用來插入、更新和刪除此類型之實體的預存程式。

[![image22](the-entity-framework-and-aspnet-getting-started-part-7/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image9.png)

將**Insert**函數設定為**InsertStudent**。 此視窗會顯示預存程式參數的清單，每一個都必須對應至一個實體屬性。 其中兩個會自動對應，因為名稱是相同的。 沒有名為 `FirstName`的實體屬性，因此您必須手動從顯示可用實體屬性的下拉式清單中選取 [`FirstMidName`]。 （這是因為您在第一個教學課程中，將 `FirstName` 屬性的名稱變更為 `FirstMidName`。）

[![image23](the-entity-framework-and-aspnet-getting-started-part-7/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image11.png)

在相同的 [**對應詳細資料**] 視窗中，將 `Update` 函式對應至 `UpdateStudent` 預存程式（請務必指定 `FirstMidName` 做為 `FirstName`的參數值，如同您在 `Insert` 預存程式中所做的）和 `Delete` 函數到 `DeletePerson` 預存程式。

[![image01](the-entity-framework-and-aspnet-getting-started-part-7/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image13.png)

遵循相同的程式，將講師的插入、更新和刪除預存程式對應至 `Instructor` 實體。

[![image02](the-entity-framework-and-aspnet-getting-started-part-7/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image15.png)

對於讀取而不是更新資料的預存程式，您可以使用 [**模型瀏覽器**] 視窗，將預存程式對應至它所傳回的實體類型。 在 [資料模型設計師] 中，以滑鼠右鍵按一下設計介面，然後選取 [**模型瀏覽器**]。 開啟 [ **SchoolModel** ] 節點，然後開啟 [**預存程式**] 節點。 然後以滑鼠右鍵按一下 `GetCourses` 預存程式，然後選取 [**新增函數匯入**]。

[![image24](the-entity-framework-and-aspnet-getting-started-part-7/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image17.png)

在 [**加入**函式匯入] 對話方塊中，于 [傳回選取**實體** **的集合**] 底下，選取 [`Course`] 做為傳回的實體類型。 完成後，按一下 [ **確定**]。 儲存並關閉 *.edmx*檔案。

[![image25](the-entity-framework-and-aspnet-getting-started-part-7/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image19.png)

## <a name="using-insert-update-and-delete-stored-procedures"></a>使用 Insert、Update 和 Delete 預存程式

插入、更新和刪除資料的預存程式會在您將其新增至資料模型並將它們對應至適當的實體之後，自動由 Entity Framework 使用。 您現在可以執行*StudentsAdd* ，而且每次建立新的學生時，Entity Framework 都會使用 `InsertStudent` 預存程式，將新的資料列加入 `Student` 資料表。

[![image03](the-entity-framework-and-aspnet-getting-started-part-7/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image21.png)

執行 [student *] 頁面，* 新的學生會出現在清單中。

[![image04](the-entity-framework-and-aspnet-getting-started-part-7/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image23.png)

變更名稱以確認更新函式可正常運作，然後刪除學生以確認 delete 函式可以運作。

[![image05](the-entity-framework-and-aspnet-getting-started-part-7/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image25.png)

## <a name="using-select-stored-procedures"></a>使用 Select 預存程式

Entity Framework 不會自動執行 `GetCourses`的預存程式，而且您無法將它們與 `EntityDataSource` 控制項搭配使用。 若要使用它們，您可以從程式碼呼叫它們。

開啟*InstructorsCourses.aspx.cs*檔案。 `PopulateDropDownLists` 方法會使用 LINQ to entities 查詢來抓取所有課程實體，讓它可以在清單中執行迴圈，並判斷講師指派給哪一個或哪些未指派：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample6.cs)]

將此取代為下列程式碼：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample7.cs)]

此頁面現在會使用 `GetCourses` 預存程式來取出所有課程的清單。 執行頁面，確認它的運作方式與之前相同。

（根據 `ObjectContext` 預設設定，預存程式所抓取之實體的導覽屬性可能不會自動填入與這些實體相關的資料。 如需詳細資訊，請參閱 MSDN Library 中的[載入相關物件](https://msdn.microsoft.com/library/bb896272.aspx)。）

在下一個教學課程中，您將瞭解如何使用動態資料功能，讓您更輕鬆地設計和測試資料格式和驗證規則。 您可以在資料模型中繼資料中指定這類規則，而不是在每個網頁規則上指定，而不是在每個頁面上都自動套用。

> [!div class="step-by-step"]
> [上一頁](the-entity-framework-and-aspnet-getting-started-part-6.md)
> [下一頁](the-entity-framework-and-aspnet-getting-started-part-8.md)
