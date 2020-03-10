---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
title: Entity Framework 4.0 的新功能 |Microsoft Docs
author: tdykstra
description: 本教學課程系列是以 Entity Framework 4.0 教學課程系列的消費者入門所建立的 Contoso 大學 web 應用程式為基礎。 I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 393df4a8-b1db-44c4-9db7-2b533ca887d0
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
msc.type: authoredcontent
ms.openlocfilehash: 29d2bd61e8361b130e7b9415dad4fe1d5b847945
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78642671"
---
# <a name="whats-new-in-the-entity-framework-40"></a>Entity Framework 4.0 的新功能

由[Tom 作者: dykstra](https://github.com/tdykstra)

> 本教學課程系列是[以 Entity Framework](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)教學課程系列的消費者入門所建立的 Contoso 大學 web 應用程式為基礎。 如果您未完成先前的教學課程，做為本教學課程的起點，您可以下載您所建立[的應用程式](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)。 您也可以下載完整的教學課程系列所建立[的應用程式](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)。 如果您有關于教學課程的問題，可以將其張貼到[ASP.NET Entity Framework 論壇](https://forums.asp.net/1227.aspx)。

在上一個教學課程中，您已看到一些方法，可讓使用 Entity Framework 之 web 應用程式的效能最大化。 本教學課程會回顧 Entity Framework 第4版中最重要的新功能，並連結至可提供所有新功能之完整簡介的資源。 本教學課程中反白顯示的功能包括下列各項：

- 外鍵關聯。
- 執行使用者定義的 SQL 命令。
- 模型優先開發。
- POCO 支援。

此外，本教學課程將會簡短介紹程式*代碼優先開發*，這項功能會在下一版的 Entity Framework 推出。

若要開始本教學課程，請啟動 Visual Studio，並開啟您在上一個教學課程中使用的 Contoso 大學 web 應用程式。

## <a name="foreign-key-associations"></a>外鍵關聯

3\.5 版的 Entity Framework 包含導覽屬性，但它不包含資料模型中的外鍵屬性。 例如，`StudentGrade` 實體會省略 `StudentGrade` 資料表的 `CourseID` 和 `StudentID` 資料行。

[![Image01](what-s-new-in-the-entity-framework-4/_static/image2.png)](what-s-new-in-the-entity-framework-4/_static/image1.png)

這種方法的原因是，嚴格來說，外鍵是實體的執行詳細資料，而不屬於概念資料模型。 不過，在實際情況下，當您有外鍵的直接存取權時，使用程式碼中的實體通常會比較容易。

如需資料模型中的外鍵如何簡化您的程式碼的範例，請考慮您在不使用*DepartmentsAdd*的情況下，必須如何編碼該頁面。 在 `Department` 實體中，`Administrator` 屬性是對應至 `Person` 實體中 `PersonID` 的外鍵。 若要建立新部門和其系統管理員之間的關聯，您只需要在資料系結控制項的 `ItemInserting` 事件處理常式中設定 [`Administrator`] 屬性的值即可：

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample1.cs)]

在資料模型中沒有外鍵時，您會處理資料來源控制項的 `Inserting` 事件，而不是資料系結控制項的 `ItemInserting` 事件，以便在實體加入至實體集之前，先取得實體本身的參考。 當您擁有該參考時，您可以使用類似下列範例中的程式碼來建立關聯：

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample2.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample3.cs)]

如您在 Entity Framework 小組在[外鍵關聯上的 blog 文章](https://blogs.msdn.com/b/efdesign/archive/2009/03/16/foreign-keys-in-the-entity-framework.aspx)中所見，在程式碼複雜度上有很大差異的其他情況。 為了因應較簡單的程式碼，而想要以概念資料模型中的執行細節為依據的需求，現在 Entity Framework 可讓您選擇在資料模型中包含外鍵。

在 Entity Framework 的術語中，如果您在資料模型中包含外鍵關聯，則會使用*外鍵關聯*，而且如果排除外鍵，則會使用*獨立關聯*。

## <a name="executing-user-defined-sql-commands"></a>執行使用者定義的 SQL 命令

在舊版的 Entity Framework 中，沒有簡單的方法可以立即建立您自己的 SQL 命令並加以執行。 Entity Framework 為您動態產生的 SQL 命令，或者您必須建立預存程式並將它匯入為函數。 第4版會將 `ExecuteStoreQuery` 和 `ExecuteStoreCommand` 方法加入 `ObjectContext` 類別，讓您更輕鬆地將任何查詢直接傳遞至資料庫。

假設 Contoso 大學系統管理員想要能夠在資料庫中執行大量變更，而不需要經過建立預存程式並將它匯入資料模型的程式。 其第一個要求是針對頁面，讓他們變更資料庫中所有課程的信用額度數目。 在網頁上，他們想要能夠輸入一個數位，用來將每個 `Course` 資料列的 `Credits` 資料行的值相乘。

建立使用 [*網站*主要] 頁面的新頁面，並將其命名為*UpdateCredits .aspx*。 然後將下列標記新增至名為 `Content2`的 `Content` 控制項：

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample4.aspx)]

此標記會建立一個 `TextBox` 控制項，使用者可以在其中輸入乘數值、要按一下的 `Button` 控制項來執行命令，以及 `Label` 控制項來指出受影響的資料列數目。

開啟*UpdateCredits.aspx.cs*，然後為按鈕的 `Click` 事件新增下列 `using` 語句和處理常式：

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample5.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample6.cs)]

這段程式碼會使用文字方塊中的值來執行 SQL `Update` 命令，並使用標籤來顯示受影響的資料列數目。 執行此頁面之前，請執行 [*課程 .aspx* ] 頁面，以取得某些資料的「之前」圖片。

[![Image02](what-s-new-in-the-entity-framework-4/_static/image4.png)](what-s-new-in-the-entity-framework-4/_static/image3.png)

執行*UpdateCredits*，輸入 "10" 做為乘數，然後按一下 [**執行**]。

[![Image03](what-s-new-in-the-entity-framework-4/_static/image6.png)](what-s-new-in-the-entity-framework-4/_static/image5.png)

再次執行 [*課程 .aspx* ] 頁面，以查看變更的資料。

[![Image04](what-s-new-in-the-entity-framework-4/_static/image8.png)](what-s-new-in-the-entity-framework-4/_static/image7.png)

（如果您想要將點數的數目設回其原始值，請在 [ *UpdateCredits.aspx.cs* ] [變更 `Credits * {0}`] 中 `Credits / {0}` 並重新執行頁面，輸入10做為除數）。

如需有關執行您在程式碼中定義之查詢的詳細資訊，請參閱[如何：直接針對資料來源執行命令](https://msdn.microsoft.com/library/ee358769.aspx)。

## <a name="model-first-development"></a>模型優先開發

在這些逐步解說中，您會先建立資料庫，然後根據資料庫結構產生資料模型。 在 Entity Framework 4 中，您可以改為從資料模型開始，並根據資料模型結構產生資料庫。 如果您要建立的應用程式已不存在資料庫，則模型優先方法可讓您建立對應用程式進行概念上合理的實體和關聯性，而不需擔心實體的執行細節. （不過，這只會透過開發的初始階段才會如此。 最後，將會建立資料庫，並在其中包含生產資料，然後從模型重新建立它將不再可行。此時您會回到資料庫優先的方法）。

在本教學課程的這一節中，您將建立簡單的資料模型，並從它產生資料庫。

在**方案總管**中，以滑鼠右鍵按一下*DAL*資料夾，然後選取 [**新增專案**]。 在 [**新增專案**] 對話方塊的 [**已安裝的範本**] 底下，選取 [**資料**]，然後選取 [ **ADO.NET 實體資料模型**] 範本。 將新檔案命名為*AlumniAssociationModel* ，**然後按一下 [新增]** 。

[![Image06](what-s-new-in-the-entity-framework-4/_static/image10.png)](what-s-new-in-the-entity-framework-4/_static/image9.png)

這會啟動實體資料模型 Wizard。 在 [**選擇模型內容**] 步驟中，選取 [**空的模型**]，然後按一下 **[完成]** 。

[![Image07](what-s-new-in-the-entity-framework-4/_static/image12.png)](what-s-new-in-the-entity-framework-4/_static/image11.png)

**實體資料模型設計**工具隨即開啟，並顯示空白的設計介面。 將**實體**專案從 [**工具箱**] 拖曳至設計介面。

[![Image08](what-s-new-in-the-entity-framework-4/_static/image14.png)](what-s-new-in-the-entity-framework-4/_static/image13.png)

將 機構名稱 從 `Entity1` 變更為 `Alumnus`，將 `Id` 屬性名稱變更為 `AlumnusId`，然後新增名為 `Name` 的新純量屬性。 若要加入新的屬性，您可以在變更 `Id` 資料行的名稱之後按下 Enter，或以滑鼠右鍵按一下實體，然後選取 [加入純量**屬性**]。 新屬性的預設類型是 `String`，這適用于這種簡單的示範，但您也可以在 [**屬性**] 視窗中變更資料類型之類的專案。

以相同的方式建立另一個實體，並將其命名為 `Donation`。 將 [`Id`] 屬性變更為 [`DonationId`]，然後新增名為 `DateAndAmount`的純量屬性。

[![Image09](what-s-new-in-the-entity-framework-4/_static/image16.png)](what-s-new-in-the-entity-framework-4/_static/image15.png)

若要新增這兩個實體之間的關聯，請以滑鼠右鍵按一下 [`Alumnus`] 實體，選取 [**新增**]，然後選取 [**關聯**]。

[![Image10](what-s-new-in-the-entity-framework-4/_static/image18.png)](what-s-new-in-the-entity-framework-4/_static/image17.png)

[**加入關聯**] 對話方塊中的預設值是您想要的（一對多、包含導覽屬性、包含外鍵），因此只要按一下 **[確定]** 即可。

[![Image11](what-s-new-in-the-entity-framework-4/_static/image20.png)](what-s-new-in-the-entity-framework-4/_static/image19.png)

設計工具會加入關聯線和外鍵屬性。

[![Image12](what-s-new-in-the-entity-framework-4/_static/image22.png)](what-s-new-in-the-entity-framework-4/_static/image21.png)

現在您已經準備好建立資料庫。 以滑鼠右鍵按一下設計介面，然後選取 [**從模型產生資料庫**]。

[![Image13](what-s-new-in-the-entity-framework-4/_static/image24.png)](what-s-new-in-the-entity-framework-4/_static/image23.png)

這會啟動 [產生資料庫] Wizard。 （如果您看到指出實體未對應的警告，您可以忽略它們的時間）。

在 [**選擇您的資料連線**] 步驟中，按一下 [**新增連接**]。

[![Image14](what-s-new-in-the-entity-framework-4/_static/image26.png)](what-s-new-in-the-entity-framework-4/_static/image25.png)

在 [**連接屬性**] 對話方塊中，選取本機 SQL Server Express 實例，並將資料庫命名為 `AlumniAssociation`。

[![Image15](what-s-new-in-the-entity-framework-4/_static/image28.png)](what-s-new-in-the-entity-framework-4/_static/image27.png)

當系統詢問您是否要建立資料庫時，請按一下 **[是]** 。 再次顯示 [**選擇您的資料連線**] 步驟時，請按 **[下一步]** 。

在 [**摘要和設定**] 步驟中，按一下 **[完成]** 。

[![Image18](what-s-new-in-the-entity-framework-4/_static/image30.png)](what-s-new-in-the-entity-framework-4/_static/image29.png)

已建立具有資料定義語言（DDL）命令的 *.sql*檔案，但尚未執行命令。

[![Image20](what-s-new-in-the-entity-framework-4/_static/image32.png)](what-s-new-in-the-entity-framework-4/_static/image31.png)

使用像是**SQL Server Management Studio**之類的工具來執行腳本並建立資料表，就像您在[消費者入門教學課程系列中的第一個教學](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)課程建立 `School` 資料庫時所做的一樣。 （除非您已下載資料庫）。

您現在可以在網頁中使用 `AlumniAssociation` 資料模型，就像使用 `School` 模型一樣。 若要試試看，請將一些資料加入至資料表，並建立顯示資料的網頁。

使用**伺服器總管**，將下列資料列新增至 [`Alumnus`] 和 [`Donation`] 資料表。

[![Image21](what-s-new-in-the-entity-framework-4/_static/image34.png)](what-s-new-in-the-entity-framework-4/_static/image33.png)

建立名為*前輩人脈*的新網頁，此網頁會使用*網站*的主版頁面。 將下列標記新增至名為 `Content2`的 `Content` 控制項：

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample7.aspx)]

此標記會建立嵌套 `GridView` 控制項，外部則是用來顯示前輩人脈名稱，而內部則是用來顯示捐贈日期和金額。

開啟*Alumni.aspx.cs*。 為數據存取層加入 `using` 語句，並為外部 `GridView` 控制項的 `RowDataBound` 事件新增處理常式：

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample8.cs)]

這段程式碼會使用目前資料列之 `Alumnus` 實體的 `Donations` 導覽屬性，來將內部 `GridView` 控制項。

執行頁面。

[![Image22](what-s-new-in-the-entity-framework-4/_static/image36.png)](what-s-new-in-the-entity-framework-4/_static/image35.png)

（注意：此頁面包含在可下載的專案中，但若要讓它正常執行，您必須在本機 SQL Server Express 實例中建立資料庫; 資料庫不會在*應用程式\_* 資料夾中包含為 *.mdf*檔案）。

如需使用 Entity Framework 之模型優先功能的詳細資訊，請參閱[Entity Framework 4 中的模型優先](https://msdn.microsoft.com/data/ff830362.aspx)。

## <a name="poco-support"></a>POCO 支援

當您使用網域驅動的設計方法時，您會設計資料類別，以代表與商務領域相關的資料和行為。 這些類別應該與用來儲存（保存）資料的任何特定技術無關;換句話說，它們應該是持續性*未知*的。 持續性無知也可以讓類別更容易進行單元測試，因為單元測試專案可以使用任何最方便進行測試的持續性技術。 舊版的 Entity Framework 針對持續性無知提供有限的支援，因為實體類別必須繼承自 `EntityObject` 類別，因此包含大量 Entity Framework 特有的功能。

Entity Framework 4 引進了使用不會繼承自 `EntityObject` 類別之實體類別的功能，因而導致非持續性的情況。 在 Entity Framework 的內容中，像這樣的類別通常稱為「*純舊 CLR 物件*」（POCO 或 poco）。 您可以手動撰寫 POCO 類別，也可以使用 Entity Framework 所提供的文字模板轉換工具組（T4）範本，根據現有的資料模型自動產生。

如需在 Entity Framework 中使用 Poco 的詳細資訊，請參閱下列資源：

- [使用 POCO 實體](https://msdn.microsoft.com/library/dd456853.aspx)。 這是一份 MSDN 檔，其中包含 Poco 的總覽，並連結至其他具有更詳細資訊的檔。
- [逐步解說： Entity Framework 的 POCO 範本](https://blogs.msdn.com/b/adonet/archive/2010/01/25/walkthrough-poco-template-for-the-entity-framework.aspx)這是來自 Entity Framework 開發小組的 blog 文章，其中包含 Poco 的其他 blog 文章連結。

## <a name="code-first-development"></a>程式碼優先開發

Entity Framework 4 中的 POCO 支援仍然需要您建立資料模型，並將實體類別連結至資料模型。 下一版的 Entity Framework 將包含名為「*程式碼優先開發*」的功能。 這項功能可讓您將 Entity Framework 與自己的 POCO 類別搭配使用，而不需要使用資料模型設計工具或資料模型 XML 檔案。 （因此，這個選項也稱為「*僅限程式碼*」;*程式碼優先*和*僅限程式碼*都參考相同的 Entity Framework 功能）。

如需使用程式碼優先方法進行開發的詳細資訊，請參閱下列資源：

- [第一次使用 Entity Framework 4 進行程式碼開發](https://weblogs.asp.net/scottgu/archive/2010/07/16/code-first-development-with-entity-framework-4.aspx)。 這是 Scott Guthrie 引進程式碼優先開發的 blog 文章。
- [Entity Framework 開發小組的 Blog-貼文標記 CodeOnly](https://blogs.msdn.com/b/efdesign/archive/tags/codeonly/)
- [Entity Framework 開發小組的網路日誌-已標記的文章 Code First](https://blogs.msdn.com/b/efdesign/archive/tags/code+first/)
- [MVC 音樂存放教學課程-第4部分：模型和資料存取](../../../../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4.md)
- [MVC 3 的消費者入門-第4部： Entity Framework 程式碼優先開發](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model.md)

此外，建立類似 Contoso 大學應用程式之應用程式的新 MVC 程式碼優先教學課程，預計會在2011的春季發佈， [https://asp.net/entity-framework/tutorials](../../../../entity-framework.md)

## <a name="more-information"></a>詳細資訊

這會完成 Entity Framework 的新功能，並繼續進行 Entity Framework 教學課程系列。 如需此處未涵蓋之 Entity Framework 4 新功能的詳細資訊，請參閱下列資源：

- [ADO.NET 的新功能](https://msdn.microsoft.com/library/ex6y04yf.aspx)Entity Framework 第4版中新功能的 MSDN 主題。
- [宣佈發行 Entity Framework 4](https://blogs.msdn.com/b/efdesign/archive/2010/04/12/announcing-the-release-of-entity-framework-4.aspx)Entity Framework 開發小組的第4版新功能的 blog 文章。

> [!div class="step-by-step"]
> [上一篇](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)
