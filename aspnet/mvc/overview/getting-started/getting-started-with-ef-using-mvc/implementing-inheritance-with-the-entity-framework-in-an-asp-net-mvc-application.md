---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教學課程：在 ASP.NET MVC 5 應用程式中使用 EF 執行繼承
description: 本教學課程將示範如何在資料模型中實作繼承。
author: tdykstra
ms.author: riande
ms.date: 01/21/2019
ms.topic: tutorial
ms.assetid: 08834147-77ec-454a-bb7a-d931d2a40dab
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 73a01ed47b0935a1a9734c197377470defb1fe36
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519384"
---
# <a name="tutorial-implement-inheritance-with-ef-in-an-aspnet-mvc-5-app"></a>教學課程：在 ASP.NET MVC 5 應用程式中使用 EF 執行繼承

在上一個教學課程中，您已處理並行例外狀況。 本教學課程將示範如何在資料模型中實作繼承。

在物件導向程式設計中，您可以使用[繼承](http://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming))來加速程式[代碼重複使用](http://en.wikipedia.org/wiki/Code_reuse)。 在本教學課程中，您將變更 `Instructor` 和 `Student` 類別，讓它們衍生自 `Person` 基底類別，而此基底類別包含講師和學生通用的屬性，例如 `LastName`。 您不會新增或變更任何網頁，但是您將變更一些程式碼，這些變更將會自動反映在資料庫中。

在本教學課程中，您將：

> [!div class="checklist"]
> * 瞭解如何將繼承對應至資料庫
> * 建立 Person 類別
> * 更新 Instructor 和 Student
> * 將 Person 新增至模型
> * 建立和更新遷移
> * 測試實作
> * 部署到 Azure

## <a name="prerequisites"></a>必要條件：

* [處理並行](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="map-inheritance-to-database"></a>將繼承對應至資料庫

`School` 資料模型中的 `Instructor` 和 `Student` 類別有數個相同的屬性：

![Student_and_Instructor_classes](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

假設您想要針對 `Instructor` 和 `Student` 實體所共用的屬性消除多餘的程式碼。 或者，您想要撰寫服務，以便用來格式化名稱，而無需在意名稱是來自講師還是學生。 您可以建立只包含這些共用屬性的 `Person` 基類，然後讓 `Instructor` 和 `Student` 實體繼承自該基類，如下圖所示：

![Student_and_Instructor_classes_deriving_from_Person_class](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

有幾種方式可以在資料庫中表示此繼承結構。 您可以有一個 `Person` 的資料表，其中包含單一資料表中的學生和講師的相關資訊。 有些資料行僅適用于講師（`HireDate`），部分僅供學生（`EnrollmentDate`）使用，部分至（`LastName`，`FirstName`）。 一般而言，您會有一個*鑒別*子資料行，以指出每個資料列所代表的類型。 例如，鑑別子資料行的 "Instructor" 代表講師，而 "Student" 代表學生。

![每 hierarchy_example 一個資料表](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

從單一資料庫資料表產生實體繼承結構的這種模式稱為「*每個階層的資料表*」（TPH）繼承。

替代方法是讓資料庫看起來更像繼承結構。 例如，您可以只有 `Person` 資料表中的 [名稱] 欄位，而且有不同的 `Instructor` 和 `Student` 資料表與日期欄位。

![每 type_inheritance 一個資料表](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

為每個實體類別建立資料庫資料表的這種模式，稱為「*每一類型的資料表*」（TPT）繼承。

還有另一個選項是將所有的非抽象類型對應至個別資料表。 類別的所有屬性 (包括繼承的屬性) 都會對應至對應資料表的資料行。 這個模式稱為一實體類一表 (TPC) 繼承。 如果您已如先前所示，對 `Person`、`Student`和 `Instructor` 類別執行 TPC 繼承，`Student` 和 `Instructor` 資料表在執行繼承之後看起來不會與之前相同。

TPC 和 TPH 繼承模式通常會在 Entity Framework 中提供比 TPT 繼承模式更好的效能，因為 TPT 模式可能會導致複雜的聯結查詢。

本教學課程將示範如何實作 TPH 繼承。 TPH 是 Entity Framework 中的預設繼承模式，因此您只需要建立 `Person` 類別，將 `Instructor` 和 `Student` 類別變更為衍生自 `Person`，將新類別新增至 `DbContext`，並建立遷移。 （如需如何執行其他繼承模式的相關資訊，請參閱 MSDN Entity Framework 檔中的[對應每一類型的資料表（TPT）繼承](https://msdn.microsoft.com/data/jj591617#2.5)和[對應每個具體的資料表類別（TPC）繼承](https://msdn.microsoft.com/data/jj591617#2.6)。

## <a name="create-the-person-class"></a>建立 Person 類別

在 [*模型*] 資料夾中，建立*Person.cs* ，並將範本程式碼取代為下列程式碼：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="update-instructor-and-student"></a>更新 Instructor 和 Student

現在更新*Instructor.cs*和*Student.cs* ，以繼承*Person.sc*的值。

在*Instructor.cs*中，從 `Person` 類別衍生 `Instructor` 類別，並移除 [索引鍵] 和 [名稱] 欄位。 程式碼看起來應該如下列範例所示：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

對*Student.cs*進行類似的變更。 `Student` 類別看起來會如下列範例所示：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="add-person-to-the-model"></a>將 Person 新增至模型

在*SchoolCoNtext.cs*中，加入 `Person` 實體類型的 `DbSet` 屬性：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

這就是 Entity Framework 為了設定單表繼承而必須執行的所有工作。 如您所見，當資料庫更新時，它會有一個 `Person` 資料表來取代 `Student` 和 `Instructor` 資料表。

## <a name="create-and-update-migrations"></a>建立和更新遷移

在 [套件管理員主控台] （PMC）中，輸入下列命令：

`Add-Migration Inheritance`

在 PMC 中執行 `Update-Database` 命令。 此時，此命令將會失敗，因為我們有遷移不知道如何處理的現有資料。 您會收到類似下列的錯誤訊息：

> *無法捨棄物件 ' dbo。講師 '，因為它是由 FOREIGN KEY 條件約束所參考。*

開啟 *[遷移]\&lt; 時間戳記&gt;\_Inheritance.cs* ，並以下列程式碼取代 `Up` 方法：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

此程式碼負責下列資料庫更新工作：

- 移除指向 Student 資料表的外部索引鍵條件約束和索引。
- 將 Instructor 資料表重新命名為 Person，並對其進行所需的變更來儲存 Student 資料：

    - 針對學生新增可為 null 的 EnrollmentDate。
    - 新增 Discriminator 資料行，以指出資料列適用於學生或講師。
    - 使 HireDate 成為可為 Null，因為學生資料列不會有雇用日期。
    - 新增暫存欄位，它將用來更新指向學生的外部索引鍵。 當您將學生複製到 Person 資料表時，他們會取得新的主要金鑰值。
- 將 Student 資料表中的資料複製到 Person 資料表。 這會導致學生獲指派新的主索引鍵值。
- 修正指向學生的外部索引鍵值。
- 重新建立外部索引鍵條件約束和索引，現在將它們指向 Person 資料表。

(如果您使用 GUID 而不是整數作為主索引鍵類型，學生的主索引鍵值將無需變更，而且可能已省略其中幾個步驟。)

再次執行 `update-database` 命令。

（在生產系統中，您會對 Down 方法進行相對應的變更，以防您必須使用它來返回先前的資料庫版本。 在本教學課程中，您將不會使用向下方法）。

> [!NOTE]
> 當您遷移資料並進行架構變更時，可能會收到其他錯誤。 如果您收到無法解決的遷移錯誤，可以藉由變更*web.config*檔案中的連接字串或刪除資料庫來繼續進行本教學課程。 最簡單的方法是*在 web.config 檔案*中重新命名資料庫。 例如，將資料庫名稱變更為 ContosoUniversity2，如下列範例所示：
>
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.xml?highlight=2)]
>
> 使用新的資料庫時，沒有可遷移的資料，而且 `update-database` 命令較可能會在沒有錯誤的情況下完成。 如需有關如何刪除資料庫的指示，請參閱[如何從 Visual Studio 2012 卸載資料庫](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)。 如果您採用此方法來繼續進行本教學課程，請略過本教學課程結尾的部署步驟，或部署到新的網站和資料庫。 如果您將更新部署至已部署至的相同網站，則 EF 會在執行自動遷移時收到相同的錯誤。 如果您想要針對遷移錯誤進行疑難排解，最佳資源是其中一個 Entity Framework 論壇或 StackOverflow.com。

## <a name="test-the-implementation"></a>測試實作

執行網站並嘗試各種頁面。 一切項目的運作與之前一樣。

在**伺服器總管中，** 依序展開 [**資料 Connections\SchoolCoNtext** ] 和 [**資料表]** ，您會看到 [ **Student** ] 和 [**講師**] 資料表已由 [ **Person** ] 資料表取代。 展開 [ **Person** ] 資料表，您就會看到它擁有所有用在**學生**和**講師**資料表中的資料行。

以滑鼠右鍵按一下 Person 資料表，然後按一下 [顯示資料表資料] 以查看鑑別子資料行。

下圖說明新 School 資料庫的結構：

![School_database_diagram](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

## <a name="deploy-to-azure"></a>部署到 Azure

本節要求您已完成本教學課程系列的[第3部分、排序、篩選和分頁](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)中的選擇性將**應用程式部署至 Azure**一節。 如果您藉由刪除本機專案中的資料庫來解決了遷移錯誤，請略過此步驟;或者，建立新的網站和資料庫，並部署到新的環境。

1. 在 Visual Studio 的 [方案總管] 中以滑鼠右鍵按一下專案，再選取內容功能表中的 [發佈]。

2. 按一下 [發行]。

    Web 應用程式會在您的預設瀏覽器中開啟。

3. 測試應用程式以確認其運作正常。

    當您第一次執行存取資料庫的頁面時，Entity Framework 會執行所有需要的遷移 `Up` 方法，使資料庫與目前的資料模型保持在最新狀態。

## <a name="get-the-code"></a>取得程式碼

[下載已完成的專案](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>其他資源

您可以在[ASP.NET 資料存取-建議的資源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。

如需有關這個和其他繼承結構的詳細資訊，請參閱 MSDN 上的[TPT 繼承模式](https://msdn.microsoft.com/data/jj618293)和[TPH 繼承模式](https://msdn.microsoft.com/data/jj618292)。 在下一個教學課程中，您將了解如何處理各種相對進階的 Entity Framework 案例。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您將：

> [!div class="checklist"]
> * 瞭解如何將繼承對應至資料庫
> * 建立 Person 類別
> * 更新 Instructor 和 Student
> * 已將人員新增至模型
> * 建立和更新遷移
> * 測試實作
> * 已部署至 Azure

前往下一篇文章，以瞭解當您超越開發使用 Entity Framework Code First 的 ASP.NET web 應用程式的基本概念時，可以注意的主題。
> [!div class="nextstepaction"]
> [進階 Entity Framework 案例](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
