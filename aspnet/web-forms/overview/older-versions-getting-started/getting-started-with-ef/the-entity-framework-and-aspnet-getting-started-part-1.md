---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1
title: Entity Framework 4.0 Database First 和 ASP.NET 4 Web Forms 的消費者入門 |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 4.0 和 Visual Studio 2010 來建立 ASP.NET Web Forms 應用程式 。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 5cb00916-8f46-491f-be25-4739a615d619
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1
msc.type: authoredcontent
ms.openlocfilehash: fd88b32ad2a65e5b4c7ead15f0d6dc5dc6e97e75
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78630456"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms"></a>Entity Framework 4.0 Database First 和 ASP.NET 4 Web form 的消費者入門

由[Tom 作者: dykstra](https://github.com/tdykstra)

> Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 4.0 和 Visual Studio 2010 來建立 ASP.NET Web Forms 應用程式。 範例應用程式是虛構 Contoso 大學的網站。 其中包括的功能有學生入學許可、課程建立、教師指派。
> 
> 本教學課程會顯示C#中的範例。 [可下載的範例](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)包含C#和 Visual Basic 中的程式碼。
> 
> ## <a name="database-first"></a>Database First
> 
> 有三種方式可以使用 Entity Framework 中的資料： *Database First*、 *Model First*和*Code First*。 本教學課程適用于 Database First。 如需這些工作流程之間的差異，以及如何為您的案例選擇最適合的指引的詳細資訊，請參閱[Entity Framework 開發工作流程](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)。
> 
> ## <a name="web-forms"></a>Web Form
> 
> 本教學課程系列使用 ASP.NET Web form 模型，並假設您知道如何在 Visual Studio 中使用 ASP.NET Web Forms。 如果您沒有，請參閱[使用 ASP.NET 4.5 Web Forms 消費者入門](../../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)。 如果您想要使用 ASP.NET MVC 架構，請參閱[使用 ASP.NET MVC 的 Entity Framework 消費者入門](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。
> 
> ## <a name="software-versions"></a>軟體版本
> 
> | **教學課程中所示** | **也適用于** |
> | --- | --- |
> | Windows 7 | Windows 8 |
> | Visual Studio 2010 | 適用于 Web 的 Visual Studio 2010 Express。 本教學課程尚未使用較新版本的 Visual Studio 進行測試。 功能表選項、對話方塊和範本有許多差異。 |
> | .NET 4 | .NET 4.5 與 .NET 4 回溯相容，但本教學課程尚未使用 .NET 4.5 進行測試。 |
> | Entity Framework 4 | 本教學課程尚未使用較新版本的 Entity Framework 進行測試。 從 Entity Framework 5 開始，EF 預設會使用 EF 4.1 引進的 `DbContext API`。 EntityDataSource 控制項的設計目的是要使用 `ObjectContext` API。 如需如何搭配 `DbContext` API 使用 EntityDataSource 控制項的相關資訊，請參閱[這篇 blog 文章](https://blogs.msdn.com/b/webdev/archive/2012/09/13/how-to-use-the-entitydatasource-control-with-entity-framework-code-first.aspx)。 |
> 
> ## <a name="questions"></a>問題
> 
> 如果您有與本教學課程不直接相關的問題，您可以將其張貼到[ASP.NET Entity Framework 論壇](https://forums.asp.net/1227.aspx)、 [Entity Framework 和 LINQ to Entities 論壇](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/)，或[StackOverflow.com](http://stackoverflow.com/)。

## <a name="overview"></a>概觀

您將在這些教學課程中建立的應用程式是一個簡單的大學網站。

[![Image03](the-entity-framework-and-aspnet-getting-started-part-1/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image1.png)

使用者可以檢視和更新學生、課程和教師資訊。 您將會建立幾個畫面，如下所示。

[![Image30](the-entity-framework-and-aspnet-getting-started-part-1/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image3.png)

[![Image37](the-entity-framework-and-aspnet-getting-started-part-1/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image5.png)

[![Image31](the-entity-framework-and-aspnet-getting-started-part-1/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image7.png)

[![Image32](the-entity-framework-and-aspnet-getting-started-part-1/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image9.png)

## <a name="creating-the-web-application"></a>建立 Web 應用程式

若要開始本教學課程，請開啟 Visual Studio，然後使用**ASP.NET Web 應用程式**範本建立新的 ASP.NET Web 應用程式專案：

[![Image01](the-entity-framework-and-aspnet-getting-started-part-1/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image11.png)

此範本會建立一個已包含樣式表單和主版頁面的 web 應用程式專案：

[![Image02](the-entity-framework-and-aspnet-getting-started-part-1/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image13.png)

開啟*網站*檔案，然後將「我的 ASP.NET 應用程式」變更為「Contoso 大學」。

[!code-html[Main](the-entity-framework-and-aspnet-getting-started-part-1/samples/sample1.html)]

尋找名為 `NavigationMenu` 的*功能表*控制項，並以下列標記取代它，這會為您要建立的頁面新增功能表項目。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-1/samples/sample2.aspx)]

開啟 default.aspx 頁面，並將名為 `BodyContent` 的 `Content` 控制項變更為此*值*：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-1/samples/sample3.aspx)]

您現在有一個簡單的首頁，其中包含您將建立之各種頁面的連結：

[![Image03](the-entity-framework-and-aspnet-getting-started-part-1/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image15.png)

## <a name="creating-the-database"></a>建立資料庫

在這些教學課程中，您將使用 Entity Framework 資料模型設計師，根據現有的資料庫（通常稱為「*資料庫優先*」方法）來自動建立資料模型。 本教學課程系列未涵蓋的替代方案是手動建立資料模型，然後讓設計工具產生腳本來建立資料庫（*模型優先*方法）。

針對本教學課程中使用的資料庫優先方法，下一步就是將資料庫新增至網站。 最簡單的方式是先下載本教學課程所提供的專案。 然後以滑鼠右鍵按一下*應用程式\_[資料*] 資料夾，選取 [**加入現有專案**]，然後從已下載的專案中選取*School*資料庫檔案。

另一個替代方式是依照[建立 School 範例資料庫](https://msdn.microsoft.com/library/bb399731.aspx)中的指示進行。 無論您是下載或建立資料庫，請將下列資料夾中的*School .mdf*檔案複製到應用程式 *\_* 資料夾：

`%PROGRAMFILES%\Microsoft SQL Server\MSSQL10.SQLEXPRESS\MSSQL\DATA`

（ *.Mdf*檔案的這個位置會假設您使用的是 SQL Server 2008 Express）。

如果您從腳本建立資料庫，請執行下列步驟來建立資料庫關係圖：

1. 在**伺服器總管**中，依序展開 [**資料連線**]、[ *School .Mdf*]、[**資料庫關係圖**]，然後選取 [**加入新的圖表**]。

    [![Image35](the-entity-framework-and-aspnet-getting-started-part-1/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image17.png)
2. 選取所有資料表，然後按一下 [**新增**]。

    [![Image36](the-entity-framework-and-aspnet-getting-started-part-1/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image19.png)

    SQL Server 會建立一個資料庫關係圖，其中顯示資料表、資料表中的資料行，以及資料表之間的關聯性。 您可以隨意移動資料表來組織它們。
3. 將圖表儲存為 "SchoolDiagram"，並將它關閉。

如果您下載本教學課程所採用的*School .mdf*檔案，可以在**伺服器總管**的 [**資料庫關係圖**] 底下，按兩下 [ **SchoolDiagram** ] 來查看資料庫關係圖。

[![Image38](the-entity-framework-and-aspnet-getting-started-part-1/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image21.png)

圖表看起來像這樣（資料表可能位於這裡所示的不同位置）：

[![Image04](the-entity-framework-and-aspnet-getting-started-part-1/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image23.png)

## <a name="creating-the-entity-framework-data-model"></a>建立 Entity Framework 資料模型

現在您可以從這個資料庫建立 Entity Framework 資料模型。 您可以在應用程式的根資料夾中建立資料模型，但在本教學課程中，您會將它放在名為*DAL*的資料夾中（適用于資料存取層）。

在**方案總管**中，新增名為*DAL*的專案資料夾（請確定它是在專案底下，而不是在方案底下）。

在*DAL*資料夾上按一下滑鼠右鍵，然後選取 [**加入**] 和 [**新增專案**]。 在 [**已安裝的範本**] 底下選取 [**資料**]，選取 [ **ADO.NET 實體資料模型**] 範本，將它命名為*SchoolModel*，然後按一下 [**新增**]。

[![Image05](the-entity-framework-and-aspnet-getting-started-part-1/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image25.png)

這會啟動實體資料模型 Wizard。 在第一個 wizard 步驟中，預設會選取 [**從資料庫產生**] 選項。 按 [下一步]。

[![Image06](the-entity-framework-and-aspnet-getting-started-part-1/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image27.png)

在 [**選擇您的資料連線**] 步驟中，保留預設值，然後按 **[下一步]** 。 預設會選取 School 資料庫，而且連線設定會以**SchoolEntities**的形式儲存*在 web.config 檔案*中。

[![Image07](the-entity-framework-and-aspnet-getting-started-part-1/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image29.png)

在 [**選擇您的資料庫物件**] wizard 步驟中，選取除了 `sysdiagrams` （為您稍早產生的圖表所建立）以外的所有資料表，然後按一下 **[完成]** 。

[![Image08](the-entity-framework-and-aspnet-getting-started-part-1/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image31.png)

完成模型建立之後，Visual Studio 會顯示對應至資料庫資料表之 Entity Framework 物件（實體）的圖形表示。 （如同資料庫關係圖，個別元素的位置可能會與您在下圖中看到的不同。 您可以視需要拖曳專案，以符合圖例。）

[![Image09](the-entity-framework-and-aspnet-getting-started-part-1/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image33.png)

## <a name="exploring-the-entity-framework-data-model"></a>探索 Entity Framework 資料模型

您可以看到，實體圖表看起來非常類似資料庫關係圖，但有幾項差異。 其中一個差異是在每個關聯的結尾加上符號，以指出關聯的類型（資料表關聯性在資料模型中稱為「實體關聯」）：

- 一對零或一關聯是以 "1" 和 "0 .1" 表示。

    [![Image39](the-entity-framework-and-aspnet-getting-started-part-1/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image35.png)

    在此情況下，`Person` 實體不一定會與 `OfficeAssignment` 實體相關聯。 `OfficeAssignment` 的實體必須與 `Person` 實體相關聯。 換句話說，講師不一定會指派給辦公室，而且任何辦公室都只能指派給一個講師。
- 一對多關聯是以 "1" 和 "\*" 表示。

    [![Image40](the-entity-framework-and-aspnet-getting-started-part-1/_static/image38.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image37.png)

    在此情況下，`Person` 實體不一定會有相關聯的 `StudentGrade` 實體。 `StudentGrade` 的實體必須與一個 `Person` 實體相關聯。 `StudentGrade` 實體代表這個資料庫中已註冊的課程;如果學生在課程中註冊，而且尚未進行任何評分，則 `Grade` 屬性為 null。 換句話說，學生可能尚未在任何課程中註冊，可能是在一個課程中註冊，也可能在多個課程中註冊。 註冊課程中的每個成績僅適用于一名學生。
- 「多對多關聯」是以「\*」和「\*」來表示。

    [![Image41](the-entity-framework-and-aspnet-getting-started-part-1/_static/image40.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image39.png)

    在此情況下，`Person` 實體不一定會有相關聯的 `Course` 實體，而相反的情況也是如此： `Course` 實體不一定有相關聯的 `Person` 實體。 換句話說，講師可以教授多個課程，而課程可能會由多個講師教授。 （在此資料庫中，此關聯性僅適用于講師，而不會將學生連結到課程。 學生會透過 StudentGrades 資料表連結到課程）。

資料庫關係圖和資料模型之間的另一個差異是每個實體的其他**導覽屬性**區段。 實體的導覽屬性會參考相關的實體。 例如，`Person` 實體中的 `Courses` 屬性包含與該 `Person` 實體相關之所有 `Course` 實體的集合。

[![Image12](the-entity-framework-and-aspnet-getting-started-part-1/_static/image42.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image41.png)

但是，資料庫和資料模型之間的另一個差異是，沒有資料庫中所使用的 `CourseInstructor` 關聯資料表來連結 `Person`，並 `Course` 多對多關聯性中的資料表。 導覽屬性可讓您從 `Course` 實體的 `Person` 實體和相關的 `Person` 實體取得相關的 `Course` 實體，因此不需要在資料模型中代表關聯資料表。

[![Image11](the-entity-framework-and-aspnet-getting-started-part-1/_static/image44.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image43.png)

基於本教學課程的目的，假設 `Person` 資料表的 `FirstName` 資料行，實際上同時包含一個人的名字和中間名。 您想要變更欄位的名稱以反映這種情況，但資料庫管理員（DBA）可能不會想要變更資料庫。 您可以變更資料模型中 `FirstName` 屬性的名稱，同時讓它的資料庫對等項保持不變。

在設計工具中，以滑鼠右鍵按一下 [`Person`] 實體中的 [ **FirstName** ]，然後選取 [**重新命名**]。

[![Image13](the-entity-framework-and-aspnet-getting-started-part-1/_static/image46.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image45.png)

輸入新名稱 "Firstmidname 變更"。 這會變更您在程式碼中參考資料行的方式，而不需要變更資料庫。

[![Image29](the-entity-framework-and-aspnet-getting-started-part-1/_static/image48.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image47.png)

[模型瀏覽器] 提供另一種方式來查看資料庫結構、資料模型結構和兩者之間的對應。 若要查看此專案，請以滑鼠右鍵按一下實體設計工具中的空白區域，然後按一下 [**模型瀏覽器**]。

[![Image18](the-entity-framework-and-aspnet-getting-started-part-1/_static/image50.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image49.png)

[**模型瀏覽器**] 窗格會顯示樹狀檢視。 （[**模型瀏覽器**] 窗格可能會停駐于 [**方案總管**] 窗格）。[ **SchoolModel** ] 節點代表資料模型結構，而 [ **SchoolModel** ] 節點代表資料庫結構。

[![Image26](the-entity-framework-and-aspnet-getting-started-part-1/_static/image52.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image51.png)

展開 [ **SchoolModel** ] 以查看資料表，並展開 [**資料表/視圖**] 以查看資料表，然後展開 [**課程**] 以查看資料表中的資料行。

[![Image19](the-entity-framework-and-aspnet-getting-started-part-1/_static/image54.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image53.png)

依序展開 [ **SchoolModel**]、[**實體類型**]，然後展開 [**課程**] 節點以查看實體中的實體和屬性。

[![Image20](the-entity-framework-and-aspnet-getting-started-part-1/_static/image56.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image55.png)

在 [設計師] 或 [**模型瀏覽器**] 窗格中，您可以看到 Entity Framework 如何關聯這兩個模型的物件。 以滑鼠右鍵按一下 [`Person`] 實體，然後選取 [**資料表對應**]。

[![Image21](the-entity-framework-and-aspnet-getting-started-part-1/_static/image58.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image57.png)

這會開啟 [**對應詳細資料**] 視窗。 請注意，此視窗可讓您看到 `FirstName` 的資料庫資料行對應至 `FirstMidName`，這就是您在資料模型中將它重新命名的內容。

[![Image22](the-entity-framework-and-aspnet-getting-started-part-1/_static/image60.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image59.png)

Entity Framework 使用 XML 來儲存資料庫的相關資訊、資料模型，以及它們之間的對應。 *SchoolModel .edmx*檔案實際上是包含此資訊的 XML 檔案。 設計工具會以圖形格式呈現資訊，但您也可以用滑鼠右鍵按一下**方案總管**中的 *.edmx*檔案，按一下 [**開啟方式**]，然後選取 **[xml （文字）編輯器**]，將檔案當做 XML 來查看。 （資料模型設計工具和 XML 編輯器只是開啟和使用相同檔案的兩種不同方式，因此您無法開啟設計工具，並在 XML 編輯器中開啟檔案）。

您現在已建立網站、資料庫和資料模型。 在下一個逐步解說中，您將開始使用資料模型和 ASP.NET `EntityDataSource` 控制項來處理資料。

> [!div class="step-by-step"]
> [下一個](the-entity-framework-and-aspnet-getting-started-part-2.md)
