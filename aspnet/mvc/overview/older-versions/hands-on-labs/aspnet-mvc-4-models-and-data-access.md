---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
title: ASP.NET MVC 4 模型和資料存取 |Microsoft Docs
author: rick-anderson
description: 注意：此實際操作實驗室假設您有 ASP.NET MVC 的基本知識。 如果您之前未使用過 ASP.NET MVC，建議您移至 ASP.NET MVC 4 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 634ea84b-f904-4afe-b71b-49cccef4d9cc
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
msc.type: authoredcontent
ms.openlocfilehash: 90635b617930d0a9c126795f4c8790d542e33dc9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78560197"
---
# <a name="aspnet-mvc-4-models-and-data-access"></a>ASP.NET MVC 4 模型和資料存取

依[Web Camp 團隊](https://twitter.com/webcamps)

[下載 Web Camp 訓練套件](https://aka.ms/webcamps-training-kit)

這個實際操作實驗室假設您有**ASP.NET MVC**的基本知識。 如果您之前未使用過**ASP.NET mvc** ，建議您移至**ASP.NET mvc 4 基礎**實際操作實驗室。

本實驗室將針對源資料夾中提供的範例 Web 應用程式套用次要變更，引導您完成先前所述的增強功能和新功能。

> [!NOTE]
> 所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可在[Microsoft web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)取得。 此實驗室的特定專案可在[ASP.NET MVC 4 模型和資料存取](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess)中取得。

在**ASP.NET MVC 基礎**實際操作實驗室中，您已將硬式編碼的資料從控制器傳遞至 View 範本。 但是，為了建立真實的 Web 應用程式，您可能會想要使用實際的資料庫。

這個實際操作實驗室將示範如何使用資料庫引擎，以儲存和抓取音樂存放區應用程式所需的資料。 為達到此目的，您將從現有的資料庫開始，並從中建立實體資料模型。 在此實驗室中，您將符合**Database First**的方法，以及**Code First**的方法。

不過，您也可以使用**Model First**方法，使用工具建立相同的模型，然後從它產生資料庫。

![Database First 與 Model First](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First 與 Model First")

*Database First 與 Model First*

產生模型之後，您將在 StoreController 中進行適當的調整，以提供存放區視圖與從資料庫取得的資料，而不是使用硬式編碼的資料。 您不需要對視圖範本進行任何變更，因為此 StoreController 將會傳回相同的 Viewmodel 給視圖範本，不過這次資料會來自資料庫。

**Code First 方法**

Code First 的方法可讓我們從程式碼定義模型，而不會產生通常與架構結合的類別。

在 code first 中，模型物件是使用 Poco 來定義，&quot;純舊 CLR 物件&quot;。 Poco 是簡單的純類別，沒有繼承且不會執行介面。 我們可以自動產生資料庫，也可以使用現有的資料庫，並從程式碼產生類別對應。

使用這種方法的優點是，模型與持續性架構（在此案例中為 Entity Framework）保持獨立，因為 Poco 類別不會與對應架構結合。

> [!NOTE]
> 這個實驗室是以 ASP.NET MVC 4 和自訂和最小化的音樂存放範例應用程式版本為基礎，只符合此實際操作實驗室中顯示的功能。
> 
> 如果您想要流覽整個**音樂存放**教學課程應用程式，您可以在[MVC-音樂存放區](https://github.com/evilDave/MVC-Music-Store)中找到它。

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Prerequisites

您必須具有下列專案，才能完成此實驗室：

- 適用于 Web 或上層的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （如需有關如何安裝的指示，請參閱[附錄 A](#AppendixA) ）。

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>安裝程式

**安裝程式碼片段**

為了方便起見，您將在此實驗室中管理的大部分程式碼都是以 Visual Studio 程式碼片段的形式提供。 若要安裝程式碼片段，請執行 **.\Source\Setup\CodeSnippets.vsi**檔案。

如果您不熟悉 Visual Studio Code 程式碼片段，而且想要瞭解如何使用，您可以參閱本檔中的附錄 &quot;[附錄 C：使用程式碼片段](#AppendixC)&quot;。

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>練習

這個實際操作實驗室是由下列練習所組成：

1. [練習1：加入資料庫](#Exercise1)
2. [練習2：使用 Code First 建立資料庫](#Exercise2)
3. [練習3：使用參數查詢資料庫](#Exercise3)

> [!NOTE]
> 每個練習都會伴隨一個**結束**資料夾，其中包含您在完成練習之後應該取得的結果解決方案。 如果您需要額外的協助來進行練習，您可以使用此解決方案做為指南。

完成此實驗室的預估時間： **35 分鐘**。

<a id="Exercise1"></a>

<a id="Exercise_1_Adding_a_Database"></a>
### <a name="exercise-1-adding-a-database"></a>練習1：加入資料庫

在此練習中，您將瞭解如何將具有 MusicStore 應用程式資料表的資料庫新增至方案，以便取用其資料。 一旦使用模型產生資料庫，並將其加入至方案，您就會修改 StoreController 類別，以提供具有從資料庫取得之資料的視圖範本，而不是使用硬式編碼的值。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Adding_a_Database"></a>
#### <a name="task-1---adding-a-database"></a>工作 1-加入資料庫

在這項工作中，您會將已建立的資料庫（其中包含 MusicStore 應用程式的主資料表）新增至方案。

1. 開啟位於**來源/Ex1-AddingADatabaseDBFirst/開始/** 資料夾的 [**開始**] 解決方案。

   1. 在繼續之前，您必須先下載一些遺漏的 NuGet 套件。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
2. 新增**MvcMusicStore**資料庫檔案。 在這個實際操作的實驗室中，您將使用已建立的資料庫，稱為**MvcMusicStore**。 若要這麼做，請以滑鼠右鍵按一下 [**應用程式\_資料**資料夾]，指向 [**加入**]，然後按一下 [**現有專案**]。 流覽至 **\Source\Assets** ，然後選取 [ **MvcMusicStore** ] 檔案。

    ![加入現有的專案](aspnet-mvc-4-models-and-data-access/_static/image2.png "加入現有的專案")

    *加入現有的專案*

    ![MvcMusicStore .mdf 資料庫檔案](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore .mdf 資料庫檔案")

    *MvcMusicStore .mdf 資料庫檔案*

    資料庫已加入至專案。 即使資料庫位於方案內部，您仍可以查詢並更新它裝載于不同的資料庫伺服器。

    ![方案總管中的 MvcMusicStore 資料庫](aspnet-mvc-4-models-and-data-access/_static/image4.png "方案總管中的 MvcMusicStore 資料庫")

    *方案總管中的 MvcMusicStore 資料庫*
3. 驗證與資料庫的連接。 若要這麼做，請按兩下 [ **MvcMusicStore** ] 以建立連接。

    ![連接到 MvcMusicStore .mdf](aspnet-mvc-4-models-and-data-access/_static/image5.png "連接到 MvcMusicStore .mdf")

    *連接到 MvcMusicStore .mdf*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_a_Data_Model"></a>
#### <a name="task-2---creating-a-data-model"></a>工作 2-建立資料模型

在這項工作中，您將建立資料模型，以與上一個工作中新增的資料庫互動。

1. 建立將代表資料庫的資料模型。 若要這麼做，請在方案總管以滑鼠右鍵按一下 [**模型**] 資料夾，指向 [**加入**]，然後按一下 [**新增專案**]。 在 **加入新專案** 對話方塊中，選取 **資料** 範本，然後**ADO.NET 實體資料模型**專案。 將資料模型名稱變更為**StoreDB** ，然後按一下 [**新增**]。

    ![新增 StoreDB ADO.NET 實體資料模型](aspnet-mvc-4-models-and-data-access/_static/image6.png "新增 StoreDB ADO.NET 實體資料模型")

    *新增 StoreDB ADO.NET 實體資料模型*
2. [**實體資料模型 Wizard]** 隨即出現。 此 wizard 會引導您建立模型層。 因為模型應該根據最近新增的現有資料庫來建立，所以請選取 [**從資料庫產生**]，然後按 **[下一步]** 。

    ![選擇模型內容](aspnet-mvc-4-models-and-data-access/_static/image7.png "選擇模型內容")

    *選擇模型內容*
3. 由於您是從資料庫產生模型，因此您必須指定要使用的連接。 按一下 [**新增連接**]。
4. 選取 [ **Microsoft SQL Server 資料庫**檔案]，然後按一下 [**繼續**]。

    ![選擇資料來源](aspnet-mvc-4-models-and-data-access/_static/image8.png "選擇資料來源")

    *[選擇資料來源] 對話方塊*
5. 按一下 **[流覽]** 並選取位於**應用程式\_Data**資料夾中的資料庫**MvcMusicStore** ，然後按一下 **[確定]** 。

    ![連接屬性](aspnet-mvc-4-models-and-data-access/_static/image9.png "連線內容")

    *連接屬性*
6. 產生的類別應該與實體連接字串具有相同的名稱，因此請將其名稱變更為**MusicStoreEntities** ，然後按 **[下一步]** 。

    ![選擇資料連線](aspnet-mvc-4-models-and-data-access/_static/image10.png "選擇資料連線")

    *選擇資料連線*
7. 選擇要使用的資料庫物件。 當實體模型只會使用資料庫的資料表時，請選取 [**資料表]** 選項，並確定也已選取 [在**模型中包含外鍵資料行**] 和 [將複數化] 或 [單數化] [**產生的物件名稱**] 選項。 將 [模型命名空間] 變更為**MvcMusicStore** ，然後按一下 **[完成]** 。

    ![選擇資料庫物件](aspnet-mvc-4-models-and-data-access/_static/image11.png "選擇資料庫物件")

    *選擇資料庫物件*

    > [!NOTE]
    > 如果顯示 [安全性警告] 對話方塊，請按一下 **[確定]** 以執行範本，並產生模型實體的類別。
8. 資料庫的實體圖表將會出現，而會建立對應每個資料表到資料庫的個別類別。 例如，**專輯**資料表會以**專輯**類別表示，而資料表中的每個資料行都會對應至類別屬性。 這可讓您查詢和使用代表資料庫中資料列的物件。

    ![實體圖表](aspnet-mvc-4-models-and-data-access/_static/image12.png "實體圖表")

    *實體圖表*

    > [!NOTE]
    > T4 範本（tt）會執行程式碼來產生實體類別，並會覆寫具有相同名稱的現有類別。 在此範例中，&quot;專輯&quot;的類別、&quot;內容類型&quot; 和 &quot;演出者&quot; 會被產生的程式碼覆寫。

<a id="Ex1Task3"></a>

<a id="Task_3_-_Building_the_Application"></a>
#### <a name="task-3---building-the-application"></a>工作 3-建立應用程式

在這項工作中，您將會檢查，雖然模型產生已移除**專輯**、內容**類型和** **演出者**模型類別，但已使用新的資料模型類別成功建立專案。

1. 建立專案，方法是選取 [**建立**] 功能表項目，然後選取 [**建立 MvcMusicStore**]。

    ![建立專案](aspnet-mvc-4-models-and-data-access/_static/image13.png "建立專案")

    *建立專案*
2. 已成功建立專案。 為什麼它仍然有效？ 其運作方式是因為資料庫資料表具有欄位，其中包含您在已移除的類別**專輯** **和內容**類型中使用的屬性。

    ![組建成功](aspnet-mvc-4-models-and-data-access/_static/image14.png "組建成功")

    *組建成功*
3. 雖然設計工具會以圖表格式顯示實體，但它們實際上C#是類別。 在方案總管中展開 [ **StoreDB** ] 節點，然後在**StoreDB.tt**中，您會看到新產生的實體。

    ![產生的檔案](aspnet-mvc-4-models-and-data-access/_static/image15.png "產生的檔案")

    *產生的檔案*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a>工作 4-查詢資料庫

在這項工作中，您將更新 StoreController 類別，如此一來，它就會查詢資料庫以取得資訊，而不是使用硬式編碼的資料。

1. 開啟**Controllers\StoreController.cs** ，並將下欄欄位新增至類別，以保存**MusicStoreEntities**類別的實例，名為**storeDB**：

    （程式碼片段-*模型和資料存取-Ex1 storeDB*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample1.cs)]
2. **MusicStoreEntities**類別會針對資料庫中的每個資料表公開集合屬性。 更新**流覽**動作方法，以取得所有**專輯**的內容類型。

    （程式碼片段-*模型和資料存取-Ex1 存放區流覽*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample2.cs)]

    > [!NOTE]
    > 您會使用稱為**LINQ** （語言整合式查詢）的 .net 功能，針對這些集合撰寫強型別查詢運算式-這將會針對資料庫執行程式碼，並傳回您可以對其進行程式設計的物件。
    > 
    > 如需 LINQ 的詳細資訊，請造訪[msdn 網站](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx)。
3. 更新**索引**動作方法，以取得所有內容內容。

    （程式碼片段-*模型和資料存取-Ex1 存放區索引*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample3.cs)]
4. 更新**索引**動作方法以抓取所有內容，並將集合轉換為清單。

    （程式碼片段-*模型和資料存取-Ex1 Store GenreMenu*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample4.cs)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>工作 5-正在執行應用程式

在這項工作中，您將檢查 [存放區索引] 頁面現在會顯示儲存在資料庫中的內容，而不是硬式編碼的內容。 不需要變更 View 範本，因為**StoreController**會傳回與之前相同的實體，不過這次資料會來自資料庫。

1. 重建方案，然後按**F5**執行應用程式。
2. 專案會在首頁中啟動。 確認 [內容類型] 功能表**不再是 [** 硬式編碼] 清單，而且資料是從資料庫中直接抓取。

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image16.png)

    *從資料庫流覽內容內容*
3. 現在，流覽至任何內容類型，並確認專輯已從資料庫中填入。

    ![從資料庫流覽專輯](aspnet-mvc-4-models-and-data-access/_static/image17.png "從資料庫流覽專輯")

    *從資料庫流覽專輯*

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Database_Using_Code_First"></a>
### <a name="exercise-2-creating-a-database-using-code-first"></a>練習2：使用 Code First 建立資料庫

在此練習中，您將瞭解如何使用 Code First 的方法，以 MusicStore 應用程式的資料表來建立資料庫，以及如何存取其資料。

產生模型之後，您將修改 StoreController，以提供具有從資料庫取得之資料的視圖範本，而不是使用硬式編碼的值。

> [!NOTE]
> 如果您已完成練習1，而且已經使用 Database First 的方法，您現在將瞭解如何使用不同的程式來取得相同的結果。 在練習1中共通的工作已標示為可讓您更輕鬆閱讀。 如果您尚未完成練習1，但想要學習 Code First 的方法，您可以從這個練習著手，取得主題的完整涵蓋範圍。

<a id="Ex2Task1"></a>

<a id="Task_1_-_Populating_Sample_Data"></a>
#### <a name="task-1---populating-sample-data"></a>工作 1-填入範例資料

在這項工作中，您會在資料庫最初使用程式碼優先建立時，將範例資料填入其中。

1. 開啟位於**來源/Ex2-CreatingADatabaseCodeFirst/開始/** 資料夾的 [**開始**] 解決方案。 否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。

   1. 如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
2. 將**SampleData.cs**檔案新增至 [**模型**] 資料夾。 若要這麼做，請以滑鼠右鍵按一下 [**模型**] 資料夾，指向 [**加入**]，然後按一下 [**現有專案**]。 流覽至 **\Source\Assets** ，然後選取**SampleData.cs**檔案。

    ![範例資料填入程式碼](aspnet-mvc-4-models-and-data-access/_static/image18.png "範例資料填入程式碼")

    *範例資料填入程式碼*
3. 開啟**Global.asax.cs**檔案，並新增下列*using*語句。

    （程式碼片段-*模型和資料存取-Ex2 Global Global.asax using*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample5.cs)]
4. 在**應用程式\_Start （）** 方法中，加入下列這一行來設定資料庫初始化運算式。

    （程式碼片段-*模型和資料存取-Ex2 Global Global.asax SetInitializer*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample6.cs)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Configuring_the_connection_to_the_Database"></a>
#### <a name="task-2---configuring-the-connection-to-the-database"></a>工作 2-設定與資料庫的連接

既然您已經將資料庫加入至專案，您就會**在 web.config 檔案**中寫入連接字串。

1. 在 web.config 新增連接字串 **。** 若要這麼做，請在專案根目錄開啟**web.config** ，並在 **&lt;connectionStrings&gt;** 區段中，將名為 DefaultConnection 的連接字串取代為這一行：

    ![Web.config 檔案位置](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config 檔案位置")

    *Web.config 檔案位置*

    [!code-xml[Main](aspnet-mvc-4-models-and-data-access/samples/sample7.xml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Working_with_the_Model"></a>
#### <a name="task-3---working-with-the-model"></a>工作 3-使用模型

既然您已經設定資料庫的連接，就會將此模型與資料庫資料表連結。 在這項工作中，您將建立一個類別，它會使用 Code First 連結到資料庫。 請記住，有一個應該修改的 POCO 模型類別存在。

> [!NOTE]
> 如果您已完成練習1，您會注意到這個步驟是由嚮導執行。 藉由執行 Code First，您將以手動方式建立將連結至資料實體的類別。

1. 從**模型**專案資料夾開啟 POCO 模型類別內容類型，並包含識別碼。 使用名稱為**GenreId**的 int 屬性。

    （程式碼片段-*模型和資料存取-Ex2 Code First*內容類型）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample8.cs)]

    > [!NOTE]
    > 若要使用 Code First 慣例，類別內容類型必須具有將會自動偵測的 primary key 屬性。
    > 
    > 您可以在這[篇 msdn 文章](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx)中閱讀更多有關 Code First 慣例的資訊。
2. 現在，從 [**模型**] 專案資料夾開啟 POCO 模型類別**專輯**，並包含外鍵，並建立名稱為**GenreId**和**ArtistId**的屬性。 此類別已有主要金鑰的**GenreId** 。

    （程式碼片段-*模型和資料存取-Ex2 Code First 專輯*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample9.cs)]
3. 開啟 POCO 模型類別**演出者**，並包含**ArtistId**屬性。

    （程式碼片段-*模型和資料存取-Ex2 Code First 演出者*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample10.cs)]
4. 以滑鼠右鍵按一下**模型**專案資料夾，然後選取 [**新增] |類別**。 將檔案命名為**MusicStoreEntities.cs**。 然後，按一下 [**新增]。**

    ![新增類別](aspnet-mvc-4-models-and-data-access/_static/image20.png "新增類別")

    *加入新專案*

    ![新增 class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "新增 class2")

    *新增類別*
5. 開啟您剛才建立的類別（ **MusicStoreEntities.cs**），並包含命名空間**system.object**和**entity。**

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample11.cs)]
6. 取代類別宣告以擴充**DbCoNtext**類別：宣告公用**DBSet**和覆寫**OnModelCreating**方法。 在此步驟之後，您會取得網域類別，將您的模型與 Entity Framework 連結。 若要這麼做，請將類別程式碼取代為下列內容：

    （程式碼片段-*模型和資料存取-Ex2 Code First MusicStoreEntities*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample12.cs)]

> [!NOTE]
> 有了 Entity Framework **DbCoNtext**和**DBSet** ，您就能夠查詢 POCO 類別的內容類型。 藉由擴充**OnModelCreating**方法，您就可以在程式**代碼**中指定內容類型如何對應至資料庫資料表。 您可以在這篇 msdn 文章中找到有關 DBCoNtext 和 DBSet 的詳細資訊：[連結](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)

<a id="Ex2Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a>工作 4-查詢資料庫

在這項工作中，您將更新 StoreController 類別，如此一來，它就會從資料庫中取出資料，而不是使用硬式編碼的資料。

> [!NOTE]
> 這項工作在練習1中很常見。
> 
> 如果您已完成練習1，您會注意到這兩種方法中的步驟都相同（Database first 或 Code first）。 資料與模型的連結方式不同，但對資料實體的存取也不會受到控制器的透明度。

1. 開啟**Controllers\StoreController.cs** ，並將下欄欄位新增至類別，以保存**MusicStoreEntities**類別的實例，名為**storeDB**：

    （程式碼片段-*模型和資料存取-Ex1 storeDB*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample13.cs)]
2. **MusicStoreEntities**類別會針對資料庫中的每個資料表公開集合屬性。 更新**流覽**動作方法，以取得所有**專輯**的內容類型。

    （程式碼片段-*模型和資料存取-Ex2 存放區流覽*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample14.cs)]

    > [!NOTE]
    > 您會使用稱為**LINQ** （語言整合式查詢）的 .net 功能，針對這些集合撰寫強型別查詢運算式-這將會針對資料庫執行程式碼，並傳回您可以對其進行程式設計的物件。
    > 
    > 如需 LINQ 的詳細資訊，請造訪[msdn 網站](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx)。
3. 更新**索引**動作方法，以取得所有內容內容。

    （程式碼片段-*模型和資料存取-Ex2 存放區索引*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample15.cs)]
4. 更新**索引**動作方法以抓取所有內容，並將集合轉換為清單。

    （程式碼片段-*模型和資料存取-Ex2 Store GenreMenu*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample16.cs)]

<a id="Ex2Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>工作 5-正在執行應用程式

在這項工作中，您將檢查 [存放區索引] 頁面現在會顯示儲存在資料庫中的內容，而不是硬式編碼的內容。 不需要變更視圖範本，因為**StoreController**會傳回與之前相同的**StoreIndexViewModel** ，但是這次資料會來自資料庫。

1. 重建方案，然後按**F5**執行應用程式。
2. 專案會在首頁中啟動。 確認 [內容類型] 功能表**不再是 [** 硬式編碼] 清單，而且資料是從資料庫中直接抓取。

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image22.png)

    *從資料庫流覽內容內容*
3. 現在，流覽至任何內容類型，並確認專輯已從資料庫中填入。

    ![從資料庫流覽專輯](aspnet-mvc-4-models-and-data-access/_static/image23.png "從資料庫流覽專輯")

    *從資料庫流覽專輯*

<a id="Exercise3"></a>

<a id="Exercise_3_Querying_the_Database_with_Parameters"></a>
### <a name="exercise-3-querying-the-database-with-parameters"></a>練習3：使用參數查詢資料庫

在此練習中，您將學習如何使用參數來查詢資料庫，以及如何使用查詢結果成形，這項功能可減少資料庫存取以更有效率的方式抓取資料的次數。

> [!NOTE]
> 如需查詢結果成形的進一步資訊，請造訪下列[msdn 文章](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx)。

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_StoreController_to_Retrieve_Albums_from_Database"></a>
#### <a name="task-1---modifying-storecontroller-to-retrieve-albums-from-database"></a>工作 1-修改 StoreController 以從資料庫中取出專輯

在這項工作中，您將變更**StoreController**類別來存取資料庫，以從特定的內容類型中取出專輯。

1. 如果您想要使用「資料庫優先」方法 **，請開啟**位於**Source\Ex3-QueryingTheDatabaseWithParametersCodeFirst\Begin**資料夾的「**開始**」方案。 否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。

   1. 如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
2. 開啟**StoreController**類別以變更**流覽**動作方法。 若要這麼做，請在 **方案總管**中展開 **控制器** 資料夾，然後按兩下  **StoreController.cs**。
3. 變更 [**流覽動作]** 方法，以取得特定內容類型的專輯。 若要這麼做，請取代下列程式碼：

    （程式碼片段-*模型和資料存取-Ex3 StoreController BrowseMethod*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample17.cs)]

> [!NOTE]
> 若要填入實體的集合，您必須使用**Include**方法來指定您也想要取得專輯。 您可以使用。LINQ 中的**單一（）** 延伸模組，因為在此情況下，專輯僅應有一個內容類型。 **Single （）** 方法會採用 Lambda 運算式做為參數，在此情況下，它會指定單一類型物件，使其名稱符合所定義的值。
> 
> 您將會利用一項功能，讓您在抓取內容類型物件時，指出您想要載入的其他相關實體。 這項功能稱為「**查詢結果塑造**」，可讓您減少存取資料庫以取得資訊所需的次數。 在此案例中，您會想要為您所取得的內容類型預先提取專輯。
> 
> 此查詢包含內容類型 **。包含（&quot;專輯&quot;）** ，表示您也想要相關的專輯。 這會導致更有效率的應用程式，因為它會在單一資料庫要求中同時取得內容類型和專輯資料。

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>工作 2-正在執行應用程式

在這項工作中，您將執行應用程式，並從資料庫中取出特定類型的專輯。

1. 按**F5**執行應用程式。
2. 專案會在首頁中啟動。 將 URL 變更為 **/Store/Browse？內容類型 = Pop** ，以確認結果是從資料庫中取得。

    ![依內容類型流覽](aspnet-mvc-4-models-and-data-access/_static/image24.png "依內容類型流覽")

    *流覽/Store/Browse？內容類型 = Pop*

<a id="Ex3Task3"></a>

<a id="Task_3_-_Accessing_Albums_by_Id"></a>
#### <a name="task-3---accessing-albums-by-id"></a>工作 3-依識別碼存取專輯

在這項工作中，您將重複先前的程式，依其識別碼取得專輯。

1. 如有需要，請關閉瀏覽器，以返回 Visual Studio。 開啟**StoreController**類別來變更**Details**動作方法。 若要這麼做，請在 **方案總管**中展開 **控制器** 資料夾，然後按兩下  **StoreController.cs**。
2. 變更 [**詳細資料**動作] 方法，以根據其**識別碼**抓取專輯詳細資料。若要這麼做，請取代下列程式碼：

    （程式碼片段-*模型和資料存取-Ex3 StoreController DetailsMethod*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample18.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>工作 4-正在執行應用程式

在這項工作中，您將會在網頁瀏覽器中執行應用程式，並依其識別碼取得專輯詳細資料。

1. 按**F5**執行應用程式。
2. 專案會在首頁中啟動。 將 URL 變更為 **/Store/Details/51**或流覽內容類型，然後選取專輯以確認結果是從資料庫中取得。

    ![流覽詳細資料](aspnet-mvc-4-models-and-data-access/_static/image25.png "流覽詳細資料")

    *流覽/Store/Details/51*

> [!NOTE]
> 此外，您可以遵循[附錄 B：使用 Web Deploy 發佈 ASP.NET MVC 4 應用程式](#AppendixB)，將此應用程式部署到 Windows Azure 網站。

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>總結

藉由完成此實際操作實驗室，您已瞭解 ASP.NET MVC 模型和資料存取的基本概念，並使用**Database First**方法以及**Code First**方法：

- 如何將資料庫新增至方案，以便取用其資料
- 如何更新控制器以提供視圖範本，其中包含從資料庫取得的資料，而不是硬式編碼
- 如何使用參數查詢資料庫
- 如何使用查詢結果成形，這項功能可減少資料庫存取次數，以更有效率的方式來抓取資料
- 如何使用 Microsoft Entity Framework 中的 Database First 和 Code First 方法，將資料庫與模型連結

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附錄 A：安裝 Web 的 Visual Studio Express 2012

您可以使用 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** 安裝 Web 或另一個 &quot;Express&quot; 版本**的 Microsoft Visual Studio Express 2012** 。 下列指示會引導您完成使用*Microsoft Web Platform Installer*安裝*Visual studio Express 2012 for Web*所需的步驟。

1. 移至[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。 或者，如果您已經安裝 Web Platform Installer，您可以開啟它，然後使用 Windows Azure SDK&quot;來搜尋產品 &quot;<em>Visual Studio Express 2012 For Web</em> 。
2. 按一下 [**立即安裝**]。 如果您沒有**Web Platform Installer**系統會將您重新導向，先下載並安裝。
3. 開啟**Web Platform Installer**之後，請按一下 [**安裝**] 以啟動安裝程式。

    ![安裝 Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "安裝 Visual Studio Express")

    *安裝 Visual Studio Express*
4. 閱讀所有產品的授權和條款，然後按一下 [**我接受**] 繼續。

    ![接受授權條款](aspnet-mvc-4-models-and-data-access/_static/image27.png)

    *接受授權條款*
5. 等到下載和安裝程式完成為止。

    ![安裝進度](aspnet-mvc-4-models-and-data-access/_static/image28.png)

    *安裝進度*
6. 當安裝完成時，按一下 **[完成]** 。

    ![安裝已完成](aspnet-mvc-4-models-and-data-access/_static/image29.png)

    *安裝已完成*
7. 按一下 **[** 結束] 以關閉 Web Platform Installer。
8. 若要開啟 Web Visual Studio Express，請移至 [**開始**] 畫面，然後開始撰寫 &quot;**VS Express**&quot;，然後按一下 [ **VS Express for Web** ] 磚。

    ![VS Express for Web 磚](aspnet-mvc-4-models-and-data-access/_static/image30.png)

    *VS Express for Web 磚*

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>附錄 B：使用 Web Deploy 發行 ASP.NET MVC 4 應用程式

本附錄將告訴您如何從 Windows Azure 管理入口網站建立新的網站，以及如何發佈您在實驗室之後取得的應用程式，利用 Windows Azure 提供的 Web Deploy 發行功能。

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>工作 1-從 Windows Azure 入口網站建立新的網站

1. 移至[Windows Azure 管理入口網站](https://manage.windowsazure.com/)並使用與您的訂用帳戶相關聯的 Microsoft 認證登入。

    > [!NOTE]
    > 有了 Windows Azure，您可以免費裝載10個 ASP.NET 網站，然後隨著流量的成長而調整。 您可以在[這裡](https://aka.ms/aspnet-hol-azure)註冊。

    ![登入 Windows Azure 入口網站](aspnet-mvc-4-models-and-data-access/_static/image31.png "登入 Windows Azure 入口網站")

    *登入 Windows Azure 管理入口網站*
2. 按一下命令列上的 [**新增**]。

    ![建立新網站](aspnet-mvc-4-models-and-data-access/_static/image32.png "建立新網站")

    *建立新網站*
3. 按一下 [**計算** | 的**網站**]。 然後選取 [**快速建立**] 選項。 提供新網站的可用 URL，然後按一下 [**建立網站**]。

    > [!NOTE]
    > Windows Azure 網站是在雲端中執行之 Web 應用程式的主機，您可以控制和管理。 [快速建立] 選項可讓您從入口網站外部，將已完成的 web 應用程式部署至 Windows Azure 網站。 它不包含設定資料庫的步驟。

    ![使用 [快速建立] 建立新的網站](aspnet-mvc-4-models-and-data-access/_static/image33.png "使用 [快速建立] 建立新的網站")

    *使用 [快速建立] 建立新的網站*
4. 等到新**網站**建立完畢。
5. 建立網站之後，請按一下 [ **URL** ] 資料行下方的連結。 檢查新網站是否正常運作。

    ![流覽至新網站](aspnet-mvc-4-models-and-data-access/_static/image34.png "流覽至新網站")

    *流覽至新網站*

    ![網站正在執行](aspnet-mvc-4-models-and-data-access/_static/image35.png "網站正在執行")

    *網站正在執行*
6. 返回入口網站，然後按一下 [**名稱**] 欄底下的網站名稱，以顯示管理頁面。

    ![開啟網站管理頁面](aspnet-mvc-4-models-and-data-access/_static/image36.png "開啟網站管理頁面")

    *開啟網站管理頁面*
7. 在 [**儀表板**] 頁面的 [**快速概覽**] 區段下，按一下 [**下載發行設定檔**] 連結。

    > [!NOTE]
    > *發行設定檔*包含將 web 應用程式發佈至 Windows Azure 網站所需的所有資訊，以供每個已啟用的發行方法使用。 發行設定檔包含 URL、使用者認證和資料庫字串，這些都是用來連接到已啟用發行方法的每個端點並進行驗證的必要資訊。 **Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支援讀取發行設定檔，以將這些程式的設定自動化，以將 Web 應用程式發佈至 Windows Azure 網站。

    ![正在下載網站發行設定檔](aspnet-mvc-4-models-and-data-access/_static/image37.png "正在下載網站發行設定檔")

    *正在下載網站發行設定檔*
8. 將發行設定檔下載到已知的位置。 在此練習中，您將瞭解如何使用此檔案，將 web 應用程式從 Visual Studio 發行至 Windows Azure 網站。

    ![儲存發行設定檔](aspnet-mvc-4-models-and-data-access/_static/image38.png "正在儲存發行設定檔")

    *儲存發行設定檔*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>工作 2-設定資料庫伺服器

如果您的應用程式會使用 SQL Server 資料庫，您必須建立 SQL Database 伺服器。 如果您想要部署不使用 SQL Server 的簡單應用程式，您可能會略過這項工作。

1. 您將需要 SQL Database 伺服器來儲存應用程式資料庫。 您可以在 Windows Azure 管理入口網站的  **SQL 資料庫** | **伺服器** | **伺服器的儀表板**上，從您的訂用帳戶中查看 SQL Database 伺服器。 如果您沒有建立伺服器，可以使用命令列上的 [**新增**] 按鈕建立一個。 記下 [**伺服器名稱] 和 [URL]、[系統管理員登入名稱] 和 [密碼**]，因為您將在後續工作中使用它們。 請不要建立資料庫，因為它會在稍後的階段中建立。

    ![SQL Database Server 儀表板](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL Database Server 儀表板")

    *SQL Database Server 儀表板*
2. 在下一項工作中，您將會從 Visual Studio 測試資料庫連線，因此您必須在伺服器的**允許 IP 位址**清單中包含本機 IP 位址。 若要這麼做，請按一下 **設定**，從**目前的用戶端 IP 位址**中選取 IP 位址，並將它貼入 [**起始 Ip 位址**] 和 [**結束 ip 位址**] 文字方塊，然後按一下 ![新增-用戶端-IP-位址-確定 按鈕](aspnet-mvc-4-models-and-data-access/_static/image40.png) 按鈕。

    ![正在新增用戶端 IP 位址](aspnet-mvc-4-models-and-data-access/_static/image41.png)

    *正在新增用戶端 IP 位址*
3. 將**用戶端 Ip 位址**新增至 [允許的 ip 位址] 清單之後，按一下 [**儲存**] 以確認變更。

    ![確認變更](aspnet-mvc-4-models-and-data-access/_static/image42.png)

    *確認變更*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>工作 3-使用 Web Deploy 發行 ASP.NET MVC 4 應用程式

1. 返回 ASP.NET MVC 4 解決方案。 在 **方案總管**中，以滑鼠右鍵按一下 網站 專案，然後選取 **發佈**。

    ![發行應用程式](aspnet-mvc-4-models-and-data-access/_static/image43.png "發行應用程式")

    *發行網站*
2. 匯入您在第一個工作中儲存的發行設定檔。

    ![匯入發行設定檔](aspnet-mvc-4-models-and-data-access/_static/image44.png "匯入發行設定檔")

    *正在匯入發行設定檔*
3. 按一下 [**驗證連接**]。 驗證完成後，按 **[下一步]** 。

    > [!NOTE]
    > 當您看到 [驗證連線] 按鈕旁出現綠色核取記號時，驗證就會完成。

    ![正在驗證連接](aspnet-mvc-4-models-and-data-access/_static/image45.png "正在驗證連接")

    *正在驗證連接*
4. 在 [**設定**] 頁面的 [**資料庫**] 區段底下，按一下資料庫連接的文字方塊旁邊的按鈕（也就是**DefaultConnection**）。

    ![Web deploy 設定](aspnet-mvc-4-models-and-data-access/_static/image46.png "Web deploy 設定")

    *Web deploy 設定*
5. 設定資料庫連接，如下所示：

   - 在 [**伺服器名稱**] 中，使用*tcp：* prefix 輸入您的 SQL Database 伺服器 URL。
   - 在 [**使用者名稱**] 中，輸入您的伺服器管理員登入名稱。
   - 在 [**密碼**] 中輸入您的伺服器管理員登入密碼。
   - 輸入新的資料庫名稱。

     ![正在設定目的地連接字串](aspnet-mvc-4-models-and-data-access/_static/image47.png "正在設定目的地連接字串")

     *正在設定目的地連接字串*
6. 然後按一下 [確定]。 當系統提示您建立資料庫時，請按一下 **[是]** 。

    ![建立資料庫](aspnet-mvc-4-models-and-data-access/_static/image48.png "建立資料庫字串")

    *建立資料庫*
7. 您將用來連接到 Windows Azure 中 SQL Database 的連接字串會顯示在 [預設連接] 文字方塊中。 然後按一下 [下一步]。

    ![指向 SQL Database 的連接字串](aspnet-mvc-4-models-and-data-access/_static/image49.png "指向 SQL Database 的連接字串")

    *指向 SQL Database 的連接字串*
8. 在 [**預覽**] 頁面中，按一下 [**發佈**]。

    ![發行 web 應用程式](aspnet-mvc-4-models-and-data-access/_static/image50.png "發行 web 應用程式")

    *發行 web 應用程式*
9. 發佈程式完成後，您的預設瀏覽器會開啟已發行的網站。

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>附錄 C：使用程式碼片段

有了程式碼片段，您就可以輕鬆地擁有所需的所有程式碼。 實驗室檔會告訴您可以使用它們的確切時機，如下圖所示。

![使用 Visual Studio 程式碼片段將程式碼插入您的專案](aspnet-mvc-4-models-and-data-access/_static/image51.png "使用 Visual Studio 程式碼片段將程式碼插入您的專案")

*使用 Visual Studio 程式碼片段將程式碼插入您的專案*

***若要使用鍵盤新增程式碼片段（C#僅限）***

1. 將游標放在您想要插入程式碼的位置。
2. 開始鍵入程式碼片段名稱（不含空格或連字號）。
3. 監看 IntelliSense 會顯示相符的程式碼片段名稱。
4. 選取正確的程式碼片段（或繼續輸入，直到選取整個程式碼片段的名稱為止）。
5. 按兩次 Tab 鍵，在游標位置插入程式碼片段。

![開始鍵入程式碼片段名稱](aspnet-mvc-4-models-and-data-access/_static/image52.png "開始鍵入程式碼片段名稱")

*開始鍵入程式碼片段名稱*

![按 Tab 鍵以選取反白顯示的程式碼片段](aspnet-mvc-4-models-and-data-access/_static/image53.png "按 Tab 鍵以選取反白顯示的程式碼片段")

*按 Tab 鍵以選取反白顯示的程式碼片段*

![再按一次 Tab 鍵，將會展開程式碼片段](aspnet-mvc-4-models-and-data-access/_static/image54.png "再按一次 Tab 鍵，將會展開程式碼片段")

*再按一次 Tab 鍵，將會展開程式碼片段*

***若要使用滑鼠C#（、Visual Basic 和 XML）加入程式碼片段***sha-1. 以滑鼠右鍵按一下您要插入程式碼片段的位置。

1. 選取 [**插入程式碼片段**]，後面接著 [ **My Code 程式碼片段**]。
2. 按一下清單中的相關程式碼片段，即可加以選取。

![以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]](aspnet-mvc-4-models-and-data-access/_static/image55.png "以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]")

*以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]*

![按一下清單中的相關程式碼片段，即可加以選取](aspnet-mvc-4-models-and-data-access/_static/image56.png "按一下清單中的相關程式碼片段，即可加以選取")

*按一下清單中的相關程式碼片段，即可加以選取*
