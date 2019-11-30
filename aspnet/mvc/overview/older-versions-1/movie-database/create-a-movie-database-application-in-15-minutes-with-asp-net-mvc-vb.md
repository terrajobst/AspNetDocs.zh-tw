---
uid: mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb
title: 使用 ASP.NET MVC 在15分鐘內建立電影資料庫應用程式（VB） |Microsoft Docs
author: StephenWalther
description: Stephen Walther 會從一開始到完成，建立整個資料庫驅動的 ASP.NET MVC 應用程式。 本教學課程是新使用者的最佳簡介 。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: e4ba9786-734c-4eb3-91bb-089793325d0d
msc.legacyurl: /mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb
msc.type: authoredcontent
ms.openlocfilehash: 0ce8161d29a8ab4005e2b20462b08c9e10ee815a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595500"
---
# <a name="create-a-movie-database-application-in-15-minutes-with-aspnet-mvc-vb"></a>使用 ASP.NET MVC 在 15 分鐘內建立影片資料庫應用程式 (VB)

依[Stephen Walther](https://github.com/StephenWalther)

[下載程式代碼](https://download.microsoft.com/download/7/2/8/728F8794-E59A-4D18-9A56-7AD2DB05BD9D/MovieApp_VB.zip)

> Stephen Walther 會從一開始到完成，建立整個資料庫驅動的 ASP.NET MVC 應用程式。 本教學課程是 ASP.NET MVC 架構的新手，以及想要瞭解如何建立 ASP.NET MVC 應用程式之人員的絕佳簡介。

本教學課程的目的是要讓您瞭解「這是什麼」來建立 ASP.NET MVC 應用程式。 在本教學課程中，我會從一開始到完成建立整個 ASP.NET 的 MVC 應用程式。 我會向您示範如何建立一個簡單的資料庫導向應用程式，以說明如何列出、建立和編輯資料庫記錄。

為了簡化應用程式的建立過程，我們將利用 Visual Studio 2008 的「樣板」功能。 我們會讓 Visual Studio 產生我們的控制器、模型和視圖的初始程式碼和內容。

如果您已經使用過 Active Server Pages 或 ASP.NET，則應該會發現 ASP.NET MVC 非常熟悉。 ASP.NET MVC views 非常類似 Active Server Pages 應用程式中的頁面。 而且，如同傳統的 ASP.NET Web form 應用程式，ASP.NET MVC 可讓您完整存取 .NET framework 所提供的一組豐富的語言和類別。

我希望這個教學課程可讓您瞭解建立 ASP.NET MVC 應用程式的體驗，與建立 Active Server Pages 或 ASP.NET Web Forms 應用程式的體驗有何不同。

## <a name="overview-of-the-movie-database-application"></a>電影資料庫應用程式的總覽

因為我們的目標是要簡化事情，所以我們將建立一個非常簡單的電影資料庫應用程式。 我們的簡單電影資料庫應用程式可讓我們執行三項工作：

1. 列出一組電影資料庫記錄
2. 建立新的電影資料庫記錄
3. 編輯現有的電影資料庫記錄

同樣地，因為我們想要簡單起見，所以我們將利用建立應用程式所需之 ASP.NET MVC 架構的最小功能。 例如，我們不會利用以測試為導向的開發。

為了建立我們的應用程式，我們需要完成下列每個步驟：

1. 建立 ASP.NET MVC Web 應用程式專案
2. 建立資料庫
3. 建立資料庫模型
4. 建立 ASP.NET MVC 控制器
5. 建立 ASP.NET MVC views

## <a name="preliminaries"></a>準備工作

您需要 Visual Studio 2008 或 Visual Web Developer 2008 Express，才能建立 ASP.NET MVC 應用程式。 您也需要下載 ASP.NET MVC 架構。

如果您未擁有 Visual Studio 2008，則可以從這個網站下載 Visual Studio 2008 的90天試用版：

[https://msdn.microsoft.com/vs2008/products/cc268305.aspx](https://msdn.microsoft.com/vs2008/products/cc268305.aspx)

或者，您也可以使用 Visual Web Developer Express 2008 建立 ASP.NET MVC 應用程式。 如果您決定使用 Visual Web Developer Express，則必須安裝 Service Pack 1。 您可以從這個網站下載 Visual Web Developer 2008 Express （含 Service Pack 1）：

[https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;d isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en)

安裝 Visual Studio 2008 或 Visual Web Developer 2008 之後，您必須安裝 ASP.NET MVC 架構。 您可以從下列網站下載 ASP.NET MVC 架構：

[https://www.asp.net/mvc/](../../../index.md)

> [!NOTE] 
> 
> 您可以利用 Web Platform Installer，而不是個別下載 ASP.NET framework 和 ASP.NET MVC 架構。 Web Platform Installer 是一種應用程式，可讓您輕鬆地管理已安裝的應用程式是您的電腦：
> 
> [https://www.microsoft.com/web/gallery/Install.aspx](https://www.microsoft.com/web/gallery/Install.aspx)

## <a name="creating-an-aspnet-mvc-web-application-project"></a>建立 ASP.NET MVC Web 應用程式專案

讓我們從在 Visual Studio 2008 中建立新的 ASP.NET MVC Web 應用程式專案開始。 選取功能表選項 [檔案] **、[新增專案**]，您會看到 [圖 1] 中的 [新增專案] 對話方塊。 選取 [Visual Basic] 做為程式設計語言，然後選取 [ASP.NET MVC Web 應用程式] 專案範本。 提供專案名稱 MovieApp，然後按一下 [確定] 按鈕。

[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.png)

**圖 01**： [新增專案] 對話方塊（[按一下以查看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.png)）

請確定您從 [新增專案] 對話方塊頂端的下拉式清單中選取 [.NET Framework 3.5]，否則不會出現 [ASP.NET MVC Web 應用程式] 專案範本。

每當您建立新的 MVC Web 應用程式專案時，Visual Studio 會提示您建立個別的單元測試專案。 [圖 2] 中的對話方塊隨即出現。 由於時間限制，我們不會在本教學課程中建立測試（沒錯，我們應該會覺得有點犯）選取 [**否**] 選項，然後按一下 [**確定]** 按鈕。

> [!NOTE] 
> 
> Visual Web Developer 不支援測試專案。

[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.png)

**圖 02**： [建立單元測試專案] 對話方塊（[按一下以查看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.png)）

ASP.NET MVC 應用程式具有一組標準的資料夾： [模型]、[Views] 和 [控制器] 資料夾。 您可以在 [方案總管] 視窗中看到這組標準資料夾。 我們必須將檔案新增至每個 [模型]、[Views] 和 [控制器] 資料夾，才能建立電影資料庫應用程式。

當您使用 Visual Studio 建立新的 MVC 應用程式時，您會取得範例應用程式。 因為我們想要從頭開始，所以我們需要刪除此範例應用程式的內容。 您必須刪除下列檔案和下列資料夾：

- Controllers\HomeController.vb
- Views\Home

## <a name="creating-the-database"></a>建立資料庫

我們需要建立一個資料庫來保存電影資料庫記錄。 幸運的是，Visual Studio 包含一個名為 SQL Server Express 的免費資料庫。 請遵循下列步驟來建立資料庫：

1. 在 [方案總管] 視窗中，以滑鼠右鍵按一下應用程式\_[Data] 資料夾，然後選取 [**新增]、[新增專案**] 功能表選項。
2. 選取 [**資料**] 類別，然後選取 [ **SQL Server 資料庫**] 範本（請參閱 [圖 3]）。
3. 將新的資料庫命名為*MoviesDB* ，然後按一下 [**新增**] 按鈕。

建立資料庫之後，您可以按兩下位於應用程式\_Data 資料夾中的 MoviesDB .mdf 檔案來連接到資料庫。 按兩下 [MoviesDB] 檔案，即可開啟 [伺服器總管] 視窗。

> [!NOTE] 
> 
> 在 Visual Web Developer 的案例中，[伺服器總管] 視窗會命名為 [資料庫總管] 視窗。

[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.png)

**圖 03**：建立 Microsoft SQL Server 資料庫（[按一下以查看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.png)）

接下來，我們需要建立新的資料庫資料表。 在 [伺服器 Explorer] 視窗中，以滑鼠右鍵按一下 [資料表] 資料夾，然後選取 [**加入新的資料表**] 功能表選項。 選取此功能表選項會開啟 [資料庫資料表設計工具]。 建立下列資料庫資料行：

<a id="0.2_table01"></a>

| **資料行名稱** | **資料類型** | **允許 Null** |
| --- | --- | --- |
| ID | Int | False |
| 標題 | NVarchar （100） | False |
| Director | NVarchar （100） | False |
| DateReleased | DateTime | False |

第一個資料行（Id 資料行）有兩個特殊的屬性。 首先，您必須將識別碼資料行標記為主鍵資料行。 選取 [Id] 資料行之後，請按一下 [**設定主要金鑰**] 按鈕（它是看起來像是索引鍵的圖示）。 第二，您必須將 Id 資料行標示為識別欄位。 在屬性視窗的資料行中，向下流覽至 [識別規格] 區段，並將它展開。 將 [ **Is Identity** ] 屬性變更為 [**是]** 值。 當您完成時，資料表看起來應該如 [圖 4] 所示。

[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.png)

**圖 04**：電影資料庫資料表（[按一下以查看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.png)）

最後一個步驟是儲存新的資料表。 按一下 [儲存] 按鈕（軟碟的圖示），並為新的資料表命名 [電影]。

建立完資料表之後，請將一些電影記錄新增至資料表。 以滑鼠右鍵按一下 [伺服器總管] 視窗中的 [電影] 資料表，然後選取 [**顯示資料表資料**] 功能表選項。 輸入您最愛的電影清單（請參閱 [圖 5]）。

[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.png)

**圖 05**：輸入電影記錄（[按一下以觀看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.png)）

## <a name="creating-the-model"></a>建立模型

接下來，我們需要建立一組類別來代表我們的資料庫。 我們需要建立資料庫模型。 我們將利用 Microsoft Entity Framework，自動為資料庫模型產生類別。

> [!NOTE] 
> 
> ASP.NET MVC 架構並未系結至 Microsoft Entity Framework。 您可以利用各種物件關聯式對應（或/M）工具（包括 LINQ to SQL、Subsonic 和 NHibernate）來建立資料庫模型類別。

請遵循下列步驟來啟動實體資料模型 Wizard：

1. 以滑鼠右鍵按一下 [方案總管] 視窗中的 [模型] 資料夾，然後選取 [**加入]、[新增專案**] 功能表選項。
2. 選取 [**資料**] 類別，然後選取 [ **ADO.NET 實體資料模型**] 範本。
3. 提供您的資料模型名稱*MoviesDBModel* ，然後按一下 [**新增**] 按鈕。

按一下 [新增] 按鈕之後，[實體資料模型 Wizard] 隨即出現（請參閱 [圖 6]）。 請遵循下列步驟來完成嚮導：

1. 在 [**選擇模型內容**] 步驟中，選取 [**從資料庫產生**] 選項。
2. 在 [**選擇您的資料**連線] 步驟中，使用 [ *MoviesDB* ] 資料連線和 [連線設定] 的名稱*MoviesDBEntities* 。 按 [**下一步]** 按鈕。
3. 在 [**選擇您的資料庫物件**] 步驟中，展開 [資料表] 節點，選取 [電影] 資料表。 輸入命名空間*MovieApp* ，然後按一下 [**完成]** 按鈕。

[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.png)

**圖 06**：使用實體資料模型 Wizard 產生資料庫模型（[按一下以查看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.png)）

當您完成實體資料模型 Wizard 之後，實體資料模型設計工具隨即開啟。 設計工具應該會顯示電影資料庫資料表（請參閱 [圖 7]）。

[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.png)

**圖 07**：實體資料模型設計工具（[按一下以查看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.png)）

我們需要先進行一項變更，才能繼續進行。 「實體資料」 Wizard 會產生名為「電影」的模型類別，代表電影資料庫資料表。 因為我們將使用 Movie 類別來代表特定電影，所以我們需要將類別的名稱修改成*電影*，而不是*電影*（單數而非複數）。

按兩下設計工具介面上的類別名稱，並將類別的名稱從電影變更為 Movie。 進行這項變更之後，請按一下 [**儲存**] 按鈕（磁片磁碟機的圖示）以產生 Movie 類別。

## <a name="creating-the-aspnet-mvc-controller"></a>建立 ASP.NET MVC 控制器

下一個步驟是建立 ASP.NET MVC 控制器。 控制器負責控制使用者與 ASP.NET MVC 應用程式互動的方式。

請依照下列步驟：

1. 在 [方案總管] 視窗中，以滑鼠右鍵按一下 [控制器] 資料夾，然後選取 [**新增]、[控制器**] 功能表選項。
2. 在 [新增控制器] 對話方塊中，輸入名稱*HomeController* ，並核取標示**為 [新增]、[更新] 和 [詳細資料案例] 的動作方法**（請參閱 [圖 8]）。
3. 按一下 [**新增**] 按鈕，將新的控制器新增至您的專案。

完成這些步驟之後，即會建立 [清單 1] 中的控制器。 請注意，它包含名為 Index、Details、Create 和 Edit 的方法。 在下列各節中，我們將新增必要的程式碼，以讓這些方法正常執行。

[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image15.png)

**圖 08**：加入新的 ASP.NET MVC 控制器（[按一下以觀看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image16.png)）

**清單1– Controllers\HomeController.vb**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample1.vb)]

## <a name="listing-database-records"></a>列出資料庫記錄

Home 控制器的 Index （）方法是 ASP.NET MVC 應用程式的預設方法。 當您執行 ASP.NET MVC 應用程式時，Index （）方法是第一個呼叫的控制器方法。

我們將使用 Index （）方法來顯示電影資料庫資料表中的記錄清單。 我們將利用稍早建立的資料庫模型類別，以使用 Index （）方法來抓取電影資料庫記錄。

我已修改 [清單 2] 中的 HomeController 類別，使其包含名為 \_db 的新私用欄位。 MoviesDBEntities 類別代表我們的資料庫模型，我們將使用此類別來與我們的資料庫通訊。

我也修改了 [清單 2] 中的 Index （）方法。 Index （）方法會使用 MoviesDBEntities 類別來抓取電影資料庫資料表中的所有電影記錄。 運算式 *\_db。MovieSet. ToList （）* 會傳回電影資料庫資料表中所有電影記錄的清單。

電影清單會傳遞至 view。 傳遞至 view （）方法的任何專案都會以視圖資料的形式傳遞至 view。

**清單2–控制器/HomeController （已修改的索引方法）**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample2.vb)]

Index （）方法會傳回名為 Index 的 view。 我們必須建立此視圖，以顯示電影資料庫記錄的清單。 請依照下列步驟：

在開啟 [**加入視圖**] 對話方塊之前，您應該建立專案（選取 [**組建]、[組建方案**] 功能表選項），否則 [**視圖資料類別**] 下拉式清單中不會顯示任何類別。

1. 以滑鼠右鍵按一下程式碼編輯器中的 Index （）方法，然後選取 [**新增視圖**] 功能表選項（請參閱 [圖 9]）。
2. 在 [加入視圖] 對話方塊中，確認已核取標示為 [**建立強型別視圖**] 的核取方塊。
3. 從 [**視圖內容**] 下拉式清單中，選取 [值]*清單*。
4. 從 [ **View data class** ] 下拉式清單中，選取 [ *MovieApp*] 值。
5. 按一下 [新增] 按鈕以建立新的視圖（請參閱 [圖 10]）。

完成這些步驟之後，名為 Views\Home 的新視圖會新增至 [] 資料夾。 索引視圖的內容包含在 [清單 3] 中。

[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image17.png)

**圖 09**：從控制器動作加入視圖（[按一下以觀看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image18.png)）

[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image19.png)

**圖 10**：使用 [加入視圖] 對話方塊來建立新的視圖（[按一下以查看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image20.png)）

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample3.aspx)]

[索引] 視圖會顯示 HTML 資料表中電影資料庫資料表的所有電影記錄。 此視圖包含 For Each 迴圈，可逐一查看 ViewData 所代表的每個電影。 如果您按 F5 鍵來執行應用程式，則會看到 [圖 11] 中的網頁。

[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image21.png)

**圖 11**：索引視圖（[按一下以查看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image22.png)）

## <a name="creating-new-database-records"></a>建立新的資料庫記錄

我們在上一節中建立的索引視圖包含用來建立新資料庫記錄的連結。 讓我們繼續執行邏輯，並建立建立新電影資料庫記錄所需的視圖。

Home 控制器包含兩個名為 Create （）的方法。 第一個 Create （）方法沒有參數。 Create （）方法的這個多載會用來顯示用來建立新電影資料庫記錄的 HTML 表單。

第二個 Create （）方法具有 FormCollection 參數。 當建立新電影的 HTML 表單張貼至伺服器時，會呼叫 Create （）方法的這個多載。 請注意，第二個 Create （）方法有一個 AcceptVerbs 屬性，可防止呼叫方法，除非執行 HTTP Post 作業。

第二個 Create （）方法已在清單4中已更新的 HomeController 類別中修改。 新版本的 Create （）方法會接受 Movie 參數，並包含將新電影插入電影資料庫資料表的邏輯。

> [!NOTE] 
> 
> 請注意 Bind 屬性。 因為我們不想要從 HTML 表單更新 Movie Id 屬性，所以我們需要明確排除這個屬性。

**清單4– Controllers\HomeController.vb （已修改的 Create 方法）**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample4.vb)]

Visual Studio 可讓您輕鬆建立建立新電影資料庫記錄的表單（請參閱 [圖 12]）。 請依照下列步驟：

1. 以滑鼠右鍵按一下程式碼編輯器中的 Create （）方法，然後選取功能表選項 [**加入視圖**]。
2. 確認已核取標示為 [**建立強型別視圖**] 的核取方塊。
3. 從 [**視圖內容**] 下拉式清單中，選取 [*建立*] 值。
4. 從 [ **View data class** ] 下拉式清單中，選取 [ *MovieApp*] 值。
5. 按一下 [**新增**] 按鈕以建立新的視圖。

[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image23.png)

**圖 12**：新增 Create View （[按一下以觀看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image24.png)）

Visual Studio 會自動產生清單5中的視圖。 此視圖包含 HTML 表單，其中包含的欄位會對應至 Movie 類別的每個屬性。

**清單5– Views\Home\Create.aspx**

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample5.aspx)]

> [!NOTE] 
> 
> [加入視圖] 對話方塊所產生的 HTML 表單會產生識別碼表單欄位。 因為 Id 資料行是識別欄位，所以我們不需要此表單欄位，因此您可以放心地將它移除。

新增 [建立] 視圖之後，您可以將新的電影記錄新增至資料庫。 按 F5 鍵執行您的應用程式，然後按一下 [建立新的] 連結以查看 [圖 13] 中的表單。 如果您完成並提交表單，則會建立新的電影資料庫記錄。

請注意，您會自動取得表單驗證。 如果您不想輸入電影的發行日期，或輸入了不正確發行日期，則會重新顯示表單，並醒目提示 [發行日期] 欄位。

[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image25.png)

**圖 13**：建立新的電影資料庫記錄（[按一下以觀看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image26.png)）

## <a name="editing-existing-database-records"></a>編輯現有的資料庫記錄

在先前的章節中，我們討論了如何列出和建立新的資料庫記錄。 在最後一節中，我們會討論如何編輯現有的資料庫記錄。

首先，我們需要產生編輯表單。 這個步驟很簡單，因為 Visual Studio 會自動為我們產生編輯表單。 在 Visual Studio 程式碼編輯器中開啟 HomeController，並遵循下列步驟：

1. 以滑鼠右鍵按一下程式碼編輯器中的 Edit （）方法，然後選取 [**新增視圖**] 功能表選項（請參閱 [圖 14]）。
2. 核取標示為 [**建立強型別的視圖**] 的核取方塊。
3. 從 [**視圖內容**] 下拉式清單中，選取 [*編輯*] 值。
4. 從 [ **View data class** ] 下拉式清單中，選取 [ *MovieApp*] 值。
5. 按一下 [**新增**] 按鈕以建立新的視圖。

完成這些步驟之後，會將名為 Edit 的新視圖加入至 Views\Home 資料夾。 此視圖包含用於編輯電影記錄的 HTML 表單。

[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image27.png)

**圖 14**：新增編輯檢視（[按一下以觀看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image28.png)）

> [!NOTE] 
> 
> 編輯檢視包含一個對應于 Movie Id 屬性的 HTML 表單欄位。 因為您不想讓人員編輯 Id 屬性的值，所以您應該移除此表單欄位。

最後，我們需要修改「主控制器」，讓它支援編輯資料庫記錄。 已更新的 HomeController 類別包含在 [清單 6] 中。

**清單6– Controllers\HomeController.vb （編輯方法）**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample6.vb)]

在 [清單 6] 中，我已將其他邏輯新增至 Edit （）方法的兩個多載。 第一個 Edit （）方法會傳回電影資料庫記錄，其對應至傳遞給方法的 Id 參數。 第二個多載會執行資料庫中電影記錄的更新。

請注意，您必須取出原始電影，然後呼叫 ApplyPropertyChanges （），以更新資料庫中的現有電影。

## <a name="summary"></a>總結

本教學課程的目的是要讓您瞭解建立 ASP.NET MVC 應用程式的體驗。 我希望您發現建立 ASP.NET MVC web 應用程式非常類似于建立 Active Server Pages 或 ASP.NET 應用程式的體驗。

在本教學課程中，我們只會檢查 ASP.NET MVC 架構的最基本功能。 在未來的教學課程中，我們將深入探討控制器、控制器動作、視圖、視圖資料和 HTML 協助程式等主題。

> [!div class="step-by-step"]
> [上一篇](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs.md)
