---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: 在 ASP.NET MVC 應用程式中使用 Entity Framework 執行繼承（8/10） |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio ... 來建立 ASP.NET MVC 4 應用程式。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: a5c3feff-5335-4cdd-a97d-f7a8785c2494
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9507cba71b976825257cc9948d54f2651355959d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595312"
---
# <a name="implementing-inheritance-with-the-entity-framework-in-an-aspnet-mvc-application-8-of-10"></a>在 ASP.NET MVC 應用程式中使用 Entity Framework 執行繼承（8之10）

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載已完成的專案](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。 如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 您可以從一開始就開始本教學課程系列，或[下載本章節的入門專案](building-the-ef5-mvc4-chapter-downloads.md)，並從這裡開始。
> 
> > [!NOTE] 
> > 
> > 如果您遇到無法解決的問題，請[下載完整的章節](building-the-ef5-mvc4-chapter-downloads.md)並嘗試重現您的問題。 您通常可以藉由比較您的程式碼與已完成的程式碼，來找出問題的解決方法。 如需瞭解一些常見錯誤以及如何解決問題，請參閱[錯誤和](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)因應措施。

在上一個教學課程中，您已處理並行例外狀況。 本教學課程將示範如何在資料模型中實作繼承。

在物件導向程式設計中，您可以使用繼承來消除多餘的程式碼。 在本教學課程中，您將變更 `Instructor` 和 `Student` 類別，讓它們衍生自 `Person` 基底類別，而此基底類別包含講師和學生通用的屬性，例如 `LastName`。 您不會新增或變更任何網頁，但是您將變更一些程式碼，這些變更將會自動反映在資料庫中。

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a>每個階層的資料表與每個類型的資料表繼承

在物件導向程式設計中，您可以使用繼承，讓您更輕鬆地使用相關的類別。 例如，`School` 資料模型中的 `Instructor` 和 `Student` 類別共用數個屬性，這會導致重複的程式碼：

![Student_and_Instructor_classes](https://asp.net/media/2578113/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_e7a32f99-8bc4-48ce-aeaf-216a18071a8b.png)

假設您想要針對 `Instructor` 和 `Student` 實體所共用的屬性消除多餘的程式碼。 您可以建立只包含這些共用屬性的 `Person` 基類，然後讓 `Instructor` 和 `Student` 實體繼承自該基類，如下圖所示：

![Student_and_Instructor_classes_deriving_from_Person_class](https://asp.net/media/2578119/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_deriving_from_Person_class_671d708c-cbb8-454a-a8f8-c2d99439acd9.png)

有幾種方式可以在資料庫中表示此繼承結構。 您可以有一個 `Person` 的資料表，其中包含單一資料表中的學生和講師的相關資訊。 有些資料行僅適用于講師（`HireDate`），部分僅供學生（`EnrollmentDate`）使用，部分至（`LastName`，`FirstName`）。 一般而言，您會有一個*鑒別*子資料行，以指出每個資料列所代表的類型。 例如，鑑別子資料行的 "Instructor" 代表講師，而 "Student" 代表學生。

![每 hierarchy_example 一個資料表](https://asp.net/media/2578125/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-hierarchy_example_244067cd-b451-4e9b-9595-793b9afca505.png)

從單一資料庫資料表產生實體繼承結構的這種模式稱為「*每個階層的資料表*」（TPH）繼承。

替代方法是讓資料庫看起來更像繼承結構。 例如，您可以只有 `Person` 資料表中的 [名稱] 欄位，而且有不同的 `Instructor` 和 `Student` 資料表與日期欄位。

![每 type_inheritance 一個資料表](https://asp.net/media/2578131/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-type_inheritance.png)

為每個實體類別建立資料庫資料表的這種模式，稱為「*每一類型的資料表*」（TPT）繼承。

在 Entity Framework 中，TPH 繼承模式通常會比 TPT 繼承模式提供更好的效能，因為 TPT 模式可能會導致複雜的聯結查詢。 本教學課程將示範如何實作 TPH 繼承。 您將執行下列步驟來執行此動作：

- 建立 `Person` 類別，並將 `Instructor` 和 `Student` 類別變更為從 `Person`衍生。
- 將模型到資料庫的對應程式碼加入至資料庫內容類別。
- 將整個專案的 `InstructorID` 和 `StudentID` 參考變更為 `PersonID`。

## <a name="creating-the-person-class"></a>建立 Person 類別

 注意：在您更新使用這些類別的控制器之前，您將無法在建立下列類別之後編譯專案。 

在 [*模型*] 資料夾中，建立*Person.cs* ，並將範本程式碼取代為下列程式碼：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

在*Instructor.cs*中，從 `Person` 類別衍生 `Instructor` 類別，並移除 [索引鍵] 和 [名稱] 欄位。 程式碼看起來應該如下列範例所示：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

對*Student.cs*進行類似的變更。 `Student` 類別看起來會如下列範例所示：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="adding-the-person-entity-type-to-the-model"></a>將 Person 實體類型新增至模型

在*SchoolCoNtext.cs*中，加入 `Person` 實體類型的 `DbSet` 屬性：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

這就是 Entity Framework 為了設定單表繼承而必須執行的所有工作。 如您所見，當資料庫重新建立時，它會有一個 `Person` 資料表來取代 `Student` 和 `Instructor` 資料表。

## <a name="changing-instructorid-and-studentid-to-personid"></a>將 InstructorID 和 StudentID 變更為 PersonID

在*SchoolCoNtext.cs*的講師課程對應語句中，將 `MapRightKey("InstructorID")` 變更為 `MapRightKey("PersonID")`：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=4)]

這不是必要的變更;它只會變更多對多聯結資料表中 InstructorID 資料行的名稱。 如果您將名稱保留為 InstructorID，應用程式仍會正常運作。 以下是已完成的*SchoolCoNtext.cs*：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=15,24)]

接下來，您必須將 `InstructorID` 變更為 `PersonID`，並 `StudentID` 至整個專案中的 `PersonID`，***除非***[*遷移*] 資料夾中有時間戳記的遷移檔案。 若要這麼做，您將只會尋找並開啟需要變更的檔案，然後在開啟的檔案上執行全域變更。 在 [*遷移*] 資料夾中，您應該變更的唯一檔案是*Migrations\Configuration.cs.*

1. > [!IMPORTANT]
   > 一開始先關閉 Visual Studio 中所有開啟的檔案。
2. 在 [**編輯**] 功能表中，按一下 [**尋找及取代--尋找所有**檔案]，然後搜尋包含 `InstructorID`之專案中的所有檔案。  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. 在 [**尋找結果**] 視窗中開啟每個檔案，***但***在 [*遷移*] 資料夾中，按兩下每個檔案的一行，&lt;時間戳記&gt; *\_.cs*遷移檔案。  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)
4. 開啟 [檔案**中取代**] 對話方塊，然後變更 [**查看** **所有開啟**的檔]。
5. 使用 [檔案**中取代**] 對話方塊，將所有 `InstructorID` 變更為 `PersonID.`  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)
6. 尋找包含 `StudentID`之專案中的所有檔案。
7. 在 [**尋找結果**] 視窗中開啟每個檔案，***但***&lt;時間戳記&gt;會在 [*遷移*] 資料夾中，按兩下每個檔案的一行，以 *\_\*.cs*遷移檔案。  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
8. 開啟 [檔案**中取代**] 對話方塊，然後變更 [**查看** **所有開啟**的檔]。
9. 使用 [檔案**中取代**] 對話方塊，將所有 `StudentID` 變更為 `PersonID`。   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
10. 建置專案。

（請注意，這會示範用來命名主鍵之 `classnameID` 模式的*缺點*。 如果您已命名「主鍵識別碼」，但未在類別名稱前面加上，則現在*不*需要重新命名。）

## <a name="create-and-update-a-migrations-file"></a>建立和更新遷移檔案

在 [套件管理員主控台] （PMC）中，輸入下列命令：

`Add-Migration Inheritance`

在 PMC 中執行 `Update-Database` 命令。 此時，此命令將會失敗，因為我們有遷移不知道如何處理的現有資料。 您會收到下列錯誤：

*ALTER TABLE 語句與外鍵條件約束 "FK\_dbo 衝突。部門\_dbo。Person\_PersonID」。衝突發生在資料庫 "ContosoUniversity"，資料表 "dbo。Person 「，資料行 ' PersonID '。*

開啟 *[遷移]\&lt; 時間戳記&gt;\_Inheritance.cs* ，並以下列程式碼取代 `Up` 方法：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=25,29-40)]

再次執行 `update-database` 命令。

> [!NOTE]
> 當您遷移資料並進行架構變更時，可能會收到其他錯誤。 如果您收到無法解決的遷移錯誤，可以藉由變更*web.config*檔案中的連接字串或刪除資料庫，繼續進行本教學課程。 最簡單的方法是*在 web.config 檔案*中重新命名資料庫。 例如，將資料庫名稱變更為 CU\_測試，如下列範例所示：
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.xml?highlight=1-2)]
> 
> 使用新的資料庫時，沒有可遷移的資料，而且 `update-database` 命令較可能會在沒有錯誤的情況下完成。 如需有關如何刪除資料庫的指示，請參閱[如何從 Visual Studio 2012 卸載資料庫](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)。 如果您採用此方法來繼續進行本教學課程，請略過本教學課程結尾的部署步驟，因為部署的網站會在自動執行遷移時收到相同的錯誤。 如果您想要針對遷移錯誤進行疑難排解，最佳資源是其中一個 Entity Framework 論壇或 StackOverflow.com。

## <a name="testing"></a>測試

執行網站並嘗試各種頁面。 一切項目的運作與之前一樣。

在**伺服器總管中，** 依序展開 [ **SchoolCoNtext** ] 和 [**資料表]** ，您會看到 [ **Student** ] 和 [**講師**] 資料表已由 [ **Person** ] 資料表取代。 展開 [ **Person** ] 資料表，您就會看到它擁有所有用在**學生**和**講師**資料表中的資料行。

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

以滑鼠右鍵按一下 Person 資料表，然後按一下 [顯示資料表資料] 以查看鑑別子資料行。

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

下圖說明新 School 資料庫的結構：

![School_database_diagram](https://asp.net/media/2578143/Windows-Live-Writer_58f5a93579b2_CC7B_School_database_diagram_6350a801-7199-413f-bbac-4a2009ed19d7.png)

## <a name="summary"></a>總結

現在已針對 `Person`、`Student`和 `Instructor` 類別，執行每個階層的資料表繼承。 如需有關這個和其他繼承結構的詳細資訊，請參閱 Morteza Manavi 的 blog 的[繼承對應策略](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx)。 在下一個教學課程中，您會看到一些執行存放庫和工作單位模式的方式。

您可以在[ASP.NET 資料存取內容對應](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。

> [!div class="step-by-step"]
> [上一頁](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [下一頁](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
