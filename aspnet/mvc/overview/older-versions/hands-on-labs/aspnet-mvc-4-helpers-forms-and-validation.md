---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
title: ASP.NET MVC 4 協助程式、表單和驗證 |Microsoft Docs
author: rick-anderson
description: 在 ASP.NET MVC 4 模型和資料存取實際操作實驗室中，您已從資料庫載入及顯示資料。 在此實際操作實驗室中，您將會新增至 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 187ee9cd-bc70-479b-bfed-f568b8da96eb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
msc.type: authoredcontent
ms.openlocfilehash: 0e2605a4188eaf814f6ab0ebfeaabed4457bcfa3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539575"
---
# <a name="aspnet-mvc-4-helpers-forms-and-validation"></a>ASP.NET MVC 4 協助程式、表單和驗證

依[Web Camp 團隊](https://twitter.com/webcamps)

[下載 Web Camp 訓練套件](https://aka.ms/webcamps-training-kit)

在**ASP.NET MVC 4 模型和資料存取**實際操作實驗室中，您已從資料庫載入及顯示資料。 在這個實際操作的實驗室中，您會將編輯該資料的能力新增至「**音樂存放區**」應用程式。

記住該目標之後，您將會先建立控制器，以支援專輯的建立、讀取、更新和刪除（CRUD）動作。 您將會產生一個索引視圖範本，利用 ASP.NET MVC 的「樣板」功能，在 HTML 資料表中顯示專輯的屬性。 若要增強該視圖，您將加入自訂 HTML helper，將會截斷完整的描述。

之後，您將會新增 [編輯] 和 [建立] 視圖，讓您可以改變資料庫中的專輯，並提供像是下拉式清單等表單元素的協助。

最後，您會讓使用者刪除專輯，同時您也可以藉由驗證其輸入，防止他們輸入錯誤的資料。

這個實際操作實驗室假設您有**ASP.NET MVC**的基本知識。 如果您之前未使用過**ASP.NET mvc** ，建議您移至**ASP.NET mvc 基礎**實際操作實驗室。

本實驗室將針對源資料夾中提供的範例 Web 應用程式套用次要變更，引導您完成先前所述的增強功能和新功能。

> [!NOTE]
> 所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可在[Microsoft web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)取得。 此實驗室的特定專案可在[ASP.NET MVC 4 helper、表單和驗證中](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation)取得。

<a id="Objectives"></a>
### <a name="objectives"></a>目標

在此實際操作實驗室中，您將瞭解如何：

- 建立控制器以支援 CRUD 作業
- 產生索引視圖以顯示 HTML 資料表中的實體屬性
- 新增自訂 HTML helper
- 建立和自訂編輯檢視
- 區分回應 HTTP GET 或 HTTP POST 呼叫的動作方法
- 新增和自訂建立視圖
- 處理實體的刪除
- 驗證使用者輸入

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

如果您不熟悉 Visual Studio Code 程式碼片段，而且想要瞭解如何使用，您可以參閱本檔中的附錄 &quot;[附錄 B：使用程式碼片段](#AppendixB)&quot;。

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>練習

下列練習會組成這個實際操作實驗室：

1. [建立存放管理員控制器及其索引視圖](#Exercise1)
2. [新增 HTML Helper](#Exercise2)
3. [建立編輯檢視](#Exercise3)
4. [新增建立視圖](#Exercise4)
5. [處理刪除](#Exercise5)
6. [新增驗證](#Exercise6)
7. [在用戶端使用不顯眼的 jQuery](#Exercise7)

> [!NOTE]
> 每個練習都會伴隨一個**結束**資料夾，其中包含您在完成練習之後應該取得的結果解決方案。 如果您需要額外的協助來進行練習，您可以使用此解決方案做為指南。

完成此實驗室的預估時間： **60 分鐘**

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_the_Store_Manager_controller_and_its_Index_view"></a>
### <a name="exercise-1-creating-the-store-manager-controller-and-its-index-view"></a>練習1：建立存放管理員控制器及其索引視圖

在此練習中，您將瞭解如何建立新的控制器以支援 CRUD 作業、自訂其索引動作方法，以從資料庫傳回專輯清單，最後再產生利用 ASP.NET MVC 的樣板的索引檢視器範本在 HTML 表格中顯示專輯屬性的功能。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_StoreManagerController"></a>
#### <a name="task-1---creating-the-storemanagercontroller"></a>工作 1-建立 StoreManagerController

在這項工作中，您將建立名為**StoreManagerController**的新控制器，以支援 CRUD 作業。

1. 開啟位於**來源/Ex1-CreatingTheStoreManagerController/開始/** 資料夾的 [**開始**] 解決方案。

   1. 在繼續之前，您必須先下載一些遺漏的 NuGet 套件。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
2. 新增控制器。 若要這麼做，請在方案總管內的 [**控制器**] 資料夾上按一下滑鼠右鍵，然後依序選取 [**新增**] 和 [**控制器**] 命令。 將**控制器** **名稱**變更為**StoreManagerController** ，並確認已選取 [**具有空白讀取/寫入動作的 MVC 控制器**] 選項。 按一下 [新增]。

    ![[新增控制器] 對話方塊](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "[加入控制器] 對話方塊")

    *[新增控制器] 對話方塊*

    會產生新的控制器類別。 由於您指定要為讀取/寫入新增動作，因此會使用已填入的 TODO 批註來建立常見的 CRUD 動作，並提示包含應用程式特定的邏輯。

<a id="Ex1Task2"></a>

<a id="Task_2_-_Customizing_the_StoreManager_Index"></a>
#### <a name="task-2---customizing-the-storemanager-index"></a>工作 2-自訂 StoreManager 索引

在這項工作中，您將自訂 StoreManager 索引動作方法，以傳回具有資料庫專輯清單的視圖。

1. 在 StoreManagerController 類別中，新增下列*using*指示詞。

    （程式碼片段-*使用 MvcMusicStore ASP.NET MVC 4 協助程式和表單和驗證-Ex1*）

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample1.cs)]
2. 將欄位加入至**StoreManagerController** ，以保存 MusicStoreEntities 的實例 **。**

    （程式碼片段- *ASP.NET MVC 4 協助程式和表單和驗證-Ex1 MusicStoreEntities*）

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample2.cs)]
3. 執行 StoreManagerController 索引動作，以使用專輯清單傳回視圖。

    控制器動作邏輯與先前撰寫的 StoreController 索引動作非常類似。 使用 LINQ 取出所有專輯，包括顯示的內容類型和演出者資訊。

    （程式碼片段- *ASP.NET MVC 4 協助程式和表單和驗證-Ex1 StoreManagerController 索引*）

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample3.cs)]

<a id="Ex1Task3"></a>

<a id="strongTask_3_-_Creating_the_Index_Viewstrong"></a>
#### <a name="task-3---creating-the-index-view"></a>工作 3-建立索引視圖

在這項工作中，您將建立索引視圖範本，以顯示**StoreManager**控制器所傳回的專輯清單。

1. 在建立新的視圖範本之前，您應該先建立專案，讓 [**加入視圖] 對話方塊**知道要使用的**專輯**類別。 選取**組建 |組建 MvcMusicStore**以建立專案。
2. 在**索引**動作方法內按一下滑鼠右鍵，然後選取 [**加入視圖**]。 這會顯示 [**加入視圖**] 對話方塊。

    ![加入視圖](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "加入視圖")

    *從 Index 方法內加入視圖*
3. 在 [加入視圖] 對話方塊中，確認視圖名稱為 [**索引**]。 選取 [**建立強型別視圖**] 選項，然後從 [**模型類別**] 下拉式選單選取 [**專輯] （MvcMusicStore）** 。 從 [ **Scaffold 範本**] 下拉式清單中選取 [**清單**]。 將 [ **View engine** ] 保留為**Razor** ，其他欄位則設為預設值，然後按一下 [**新增**]。

    ![加入索引視圖](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "加入索引視圖")

    *加入索引視圖*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Customizing_the_scaffold_of_the_Index_View"></a>
#### <a name="task-4---customizing-the-scaffold-of-the-index-view"></a>工作 4-自訂索引視圖的 scaffold

在這項工作中，您將調整以 ASP.NET MVC 樣板功能建立的簡單視圖範本，讓它顯示您想要的欄位。

> [!NOTE]
> ASP.NET MVC 中的樣板支援會產生一個簡單的視圖範本，其中會列出專輯模型**中的所有**欄位。 [樣板 **] 提供快速**開始使用強型別視圖的方式：您可以快速地產生預設範本，然後修改產生的程式碼，而不需要手動撰寫視圖範本。

1. 檢查所建立的程式碼。 產生的欄位清單將會是下列 HTML**資料表的一部分，而**該架構會用來顯示表格式資料。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample4.cshtml)]
2. 以下列程式碼取代 **&lt;資料表&gt;** 程式**代碼，以顯示 [內容**類型]、[**演出者**]、[**專輯標題**] 和 [**價格**] 欄位。 這會刪除 [ **AlbumId** ] 和 [**專輯封面 URL** ] 資料行。 此外，它也會變更 GenreId 和 ArtistId 資料行，以顯示其**Artist.Name**和**Genre.Name**的連結類別屬性，並移除 [**詳細資料**] 連結。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample5.cshtml)]
3. 變更下列說明。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample6.cshtml)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>工作 5-正在執行應用程式

在這項工作中，您將測試**StoreManager** **索引**視圖範本是否根據先前步驟的設計來顯示專輯清單。

1. 按**F5**執行應用程式。
2. 專案會在首頁中啟動。 將 URL 變更為 [ **/StoreManager** ]，以確認專輯清單已顯示，並顯示其 [**標題**]、[**演出者** **] 和 [** 內容類型]。

    ![流覽專輯清單](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "流覽專輯清單")

    *流覽專輯清單*

<a id="Exercise2"></a>

<a id="Exercise_2_Adding_an_HTML_Helper"></a>
### <a name="exercise-2-adding-an-html-helper"></a>練習2：新增 HTML Helper

StoreManager 的 [索引] 頁面有一個可能的問題： [標題] 和 [演出者名稱] 屬性可以夠長的時間，以擲出資料表格式。 在此練習中，您將學習如何新增自訂 HTML helper 來截斷該文字。

在下圖中，您可以看到當您使用小型瀏覽器大小時，如何修改格式。

![流覽未截斷文字的專輯清單](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "流覽未截斷文字的專輯清單")

*流覽未截斷文字的專輯清單*

<a id="Ex2Task1"></a>

<a id="Task_1_-_Extending_the_HTML_Helper"></a>
#### <a name="task-1---extending-the-html-helper"></a>工作 1-擴充 HTML Helper

在這項工作中，您會將新方法**截斷**至 ASP.NET MVC Views 內公開的**HTML**物件。 若要這麼做，您要將**擴充方法**實作為 ASP.NET Mvc 所提供的內建**system.web. HtmlHelper**類別。

> [!NOTE]
> 如需**擴充方法**的詳細資訊，請造訪這篇 msdn 文章。 [https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx).

1. 開啟位於**來源/Ex2-AddingAnHTMLHelper/開始/** 資料夾的 [**開始**] 解決方案。 否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。

   1. 如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
2. 開啟 StoreManager 的索引視圖。 若要這麼做，請在 方案總管展開  **Views**  資料夾，然後**StoreManager**並開啟  **Index. cshtml**  檔案。
3. 在<strong>@model</strong>指示詞底下新增下列程式碼，以定義<strong>截斷</strong>helper 方法。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample7.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Truncating_Text_in_the_Page"></a>
#### <a name="task-2---truncating-text-in-the-page"></a>工作 2-截斷頁面中的文字

在這項工作中，您將使用**截斷**方法來截斷 View 範本中的文字。

1. 開啟 StoreManager 的索引視圖。 若要這麼做，請在 方案總管展開  **Views**  資料夾，然後**StoreManager**並開啟  **Index. cshtml**  檔案。
2. 取代顯示**演出者名稱**和專輯**標題**的行。 若要這麼做，請取代下列幾行。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample8.cshtml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>工作 3-正在執行應用程式

在這項工作中，您將測試**StoreManager** **索引**視圖範本是否會截斷專輯的標題和演出者名稱。

1. 按**F5**執行應用程式。
2. 專案會在首頁中啟動。 將 URL 變更為 **/StoreManager** ，以確認 [**標題**] 和 [**演出者**] 資料行中的長文字已截斷。

    ![截斷的標題和演出者名稱](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "截斷的標題和演出者名稱")

    *截斷的標題和演出者名稱*

<a id="Exercise3"></a>

<a id="Exercise_3_Creating_the_Edit_View"></a>
### <a name="exercise-3-creating-the-edit-view"></a>練習3：建立編輯檢視

在此練習中，您將瞭解如何建立表單，以允許商店經理編輯專輯。 他們會流覽 **/StoreManager/Edit/id** URL （**id**是要編輯之專輯的唯一識別碼），因此會對伺服器進行 HTTP GET 呼叫。

控制器的 [編輯] 動作方法會從資料庫抓取適當的專輯、建立**StoreManagerViewModel**物件加以封裝（連同演出者和內容的清單），然後將它傳遞至 View 範本，以將 HTML 網頁轉譯回使用者。 此頁面將包含 **&lt;表單&gt;** 元素，以及用來編輯專輯屬性的文字方塊和下拉式清單。

一旦使用者更新專輯表單值，然後按一下 [**儲存**] 按鈕，就會透過 HTTP POST 呼叫將變更提交回 **/StoreManager/Edit/id**。雖然 URL 與最後一個呼叫中的保持相同，但 ASP.NET MVC 會識別這次是 HTTP POST，因此會執行不同的編輯動作方法（一個以 **[HttpPost]** 裝飾的）。

<a id="Ex3Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Edit_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-edit-action-method"></a>工作 1-執行 HTTP-取得編輯動作方法

在這項工作中，您將會執行編輯動作方法的 HTTP GET 版本，以從資料庫中取出適當的專輯，以及所有的內容組和演出者清單。 它會將此資料封裝到最後一個步驟中所定義的**StoreManagerViewModel**物件，然後將其傳遞至視圖範本，以使用呈現回應。

1. 開啟位於**來源/Ex3-CreatingTheEditView/開始/** 資料夾的 [**開始**] 解決方案。 否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。

   1. 如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
2. 開啟**StoreManagerController**類別。 若要這麼做，請展開 [**控制器**] 資料夾，然後按兩下 [ **StoreManagerController.cs**]。
3. 以下列程式碼取代**HTTP-GET 編輯**動作方法，以取出適當的**專輯**以及**內容和** **演出者**清單。

    （程式碼片段- *ASP.NET MVC 4 協助程式和表單和驗證-Ex3 STOREMANAGERCONTROLLER HTTP-取得編輯動作*）

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample9.cs)]

    > [!NOTE]
    > 您使用的是演出者和內容的**System.web** **SelectList** ，而不是**system.object**清單。
    > 
    > **SelectList**是可讓您更清楚的方式來填入 HTML 下拉式清單，以及管理目前選取專案等專案。 在控制器動作中具現化並設定這些 ViewModel 物件，將會使編輯表單案例更整潔。

<a id="Ex3Task2"></a>

<a id="Task_2_-_Creating_the_Edit_View"></a>
#### <a name="task-2---creating-the-edit-view"></a>工作 2-建立編輯檢視

在這項工作中，您將建立編輯檢視範本，稍後會顯示專輯屬性。

1. 建立編輯檢視。 若要這樣做，請以滑鼠右鍵按一下 [**編輯**動作] 方法內部，然後選取 [**新增視圖**]。
2. 在 [加入視圖] 對話方塊中，確認視圖名稱為 [**編輯**]。 核取 [**建立強型別視圖**] 核取方塊，然後從 [**視圖] 資料類別**下拉式方塊中選取 [**專輯（MvcMusicStore）** ]。 從 [ **Scaffold 範本**] 下拉式選單選取 [**編輯**]。 將其他欄位保留為預設值，然後按一下 [**新增**]。

    ![新增編輯檢視](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "新增編輯檢視")

    *新增編輯檢視*

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>工作 3-正在執行應用程式

在這項工作中，您會測試 [ **StoreManager** **編輯**視圖] 頁面是否會針對當做參數傳遞的專輯顯示內容的值。

1. 按**F5**執行應用程式。
2. 專案會在首頁中啟動。 將 URL 變更為 [ **/StoreManager/Edit/1** ]，確認已顯示所傳遞專輯的屬性值。

    ![流覽專輯的編輯檢視](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "流覽專輯的編輯檢視")

    *流覽專輯的編輯檢視*

<a id="Ex3Task4"></a>

<a id="Task_4_-_Implementing_drop-downs_on_the_Album_Editor_Template"></a>
#### <a name="task-4---implementing-drop-downs-on-the-album-editor-template"></a>工作 4-在專輯編輯器範本上執行下拉式清單

在這項工作中，您會將下拉式清單新增至在上一個工作中建立的 View 範本，讓使用者可以從一份演出者和內容類型的清單中進行選取。

1. 以下列內容取代所有**專輯**欄位集程式碼：

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample10.cshtml)]

    > [!NOTE]
    > 已新增**DropDownList** helper 來呈現選擇演出者和內容內容的下拉式清單。 傳遞至**DropDownList**的參數為：
    > 
    > 1. 表單欄位名稱（ **&quot;ArtistId&quot;** ）。
    > 2. 下拉式的值**SelectList** 。

<a id="Ex3Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>工作 5-正在執行應用程式

在這項工作中，您會測試 [ **StoreManager** **編輯**視圖] 頁面是否顯示下拉式清單，而不是 [演出者] 和 [內容類型識別碼] 文字欄位。

1. 按**F5**執行應用程式。
2. 專案會在首頁中啟動。 將 URL 變更為 **/StoreManager/Edit/1** ，以確認它會顯示下拉式清單，而不是 [演出者] 和 [內容類型識別碼] 文字欄位。

    ![使用下拉式清單流覽專輯的編輯檢視](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "使用下拉式清單流覽專輯的編輯檢視")

    *流覽專輯的編輯檢視，這次使用下拉式清單*

<a id="Ex3Task6"></a>

<a id="Task_6_-_Implementing_the_HTTP-POST_Edit_action_method"></a>
#### <a name="task-6---implementing-the-http-post-edit-action-method"></a>工作 6-執行 HTTP POST 編輯動作方法

現在，編輯檢視會如預期般顯示，您必須執行 HTTP POST 編輯動作方法，以儲存對專輯所做的變更。

1. 如有需要，請關閉瀏覽器，以返回 [Visual Studio] 視窗。 從 [**控制器**] 資料夾開啟**StoreManagerController** 。
2. 將**HTTP POST 編輯**動作方法程式碼取代為下列內容（請注意，必須取代的方法是接收兩個參數的多載版本）：

    （程式碼片段- *ASP.NET MVC 4 協助程式和表單和驗證-Ex3 STOREMANAGERCONTROLLER HTTP-POST 編輯動作*）

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample11.cs)]

    > [!NOTE]
    > 當使用者按一下視圖的 [**儲存**] 按鈕，並對伺服器執行表單值的 HTTP POST，將其保存在資料庫中時，就會執行此方法。 裝飾專案 **[HttpPost]** 表示此方法應該用於這些 HTTP POST 案例。 方法會採用**專輯**物件。 ASP.NET MVC 會從張貼的 &lt;表單&gt; 值，自動建立專輯物件。
    > 
    > 方法會執行下列步驟：
    > 
    > 1. 如果模型有效：
    > 
    >     1. 更新內容中的專輯專案，將其標示為已修改的物件。
    >     2. 儲存變更並重新導向至索引視圖。
    > 2. 如果模型無效，它會在 ViewBag 中填入**GenreId**和**ArtistId**，然後它會傳回具有所接收專輯物件的視圖，以允許使用者執行任何必要的更新。

<a id="Ex3Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a>工作 7-執行應用程式

在這項工作中，您會測試 [ **StoreManager 編輯**視圖] 頁面是否會實際將更新的專輯資料儲存在資料庫中。

1. 按**F5**執行應用程式。
2. 專案會在首頁中啟動。 將 URL 變更為 **/StoreManager/Edit/1**。 將 [專輯] 標題變更為 [已**載入**]，然後按一下 [**儲存**]。 確認專輯清單中的專輯標題確實已變更。

    ![更新專輯](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "更新專輯")

    *更新專輯*

<a id="Exercise4"></a>

<a id="Exercise_4_Adding_a_Create_View"></a>
### <a name="exercise-4-adding-a-create-view"></a>練習4：新增建立視圖

既然**StoreManagerController**支援**編輯**功能，在這個練習中，您將學習如何新增建立視圖範本，讓商店經理將新專輯加入應用程式。

就像您對編輯功能所做的一樣，您將使用**StoreManagerController**類別內的兩個不同方法來執行建立案例：

1. 當商店經理第一次造訪 **/StoreManager/Create** URL 時，其中一個動作方法會顯示空白表單。
2. 第二個動作方法會處理案例，其中 store manager 會在表單中按一下 [**儲存**] 按鈕，並將值以 HTTP POST 形式提交回 **/StoreManager/Create** URL。

<a id="Ex4Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Create_action_method"></a>
#### <a name="task-1---implementing-the-http-get-create-action-method"></a>工作 1-執行 HTTP-GET 建立動作方法

在這項工作中，您將會執行 Create action 方法的 HTTP GET 版本來抓取所有內容清單和演出者的清單、將此資料封裝到**StoreManagerViewModel**物件中，然後再傳遞至視圖範本。

1. 開啟位於**來源/Ex4-AddingACreateView/開始/** 資料夾的 [**開始**] 解決方案。 否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。

   1. 如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
2. 開啟**StoreManagerController**類別。 若要這麼做，請展開 [**控制器**] 資料夾，然後按兩下 [ **StoreManagerController.cs**]。
3. 將**Create** action 方法程式碼取代為下列內容：

    （程式碼片段- *ASP.NET MVC 4 協助程式和表單和驗證-Ex4 STOREMANAGERCONTROLLER HTTP-取得建立動作*）

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample12.cs)]

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_the_Create_View"></a>
#### <a name="task-2---adding-the-create-view"></a>工作 2-新增建立視圖

在這項工作中，您將新增建立視圖範本，以顯示新的（空白）專輯表單。

1. 以滑鼠右鍵按一下 [**建立**動作] 方法內部，然後選取 [**新增視圖**]。 這會顯示 [加入視圖] 對話方塊。
2. 在 [加入視圖] 對話方塊中，確認視圖名稱為 [**建立**]。 選取 [**建立強型別視圖**] 選項，然後從 [**模型類別**] 下拉式選單中選取 [**專輯（MvcMusicStore）** ]，然後從 [ **Scaffold 範本**] 下拉式視窗中**建立**。 將其他欄位保留為預設值，然後按一下 [**新增**]。

    ![新增建立視圖](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "adding-a-create-view .png")

    *新增 Create View*
3. 將 [ **GenreId** ] 和 [ **ArtistId** ] 欄位更新為使用下拉式清單，如下所示：

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample13.cshtml)]

<a id="Ex4Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>工作 3-正在執行應用程式

在這項工作中，您會測試 [ **StoreManager** **建立**視圖] 頁面是否顯示空的專輯表單。

1. 按**F5**執行應用程式。
2. 專案會在首頁中啟動。 將 URL 變更為 **/StoreManager/Create**。 確認顯示空白表單以填滿新的專輯屬性。

    ![建立具有空白表單的 View](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "建立具有空白表單的 View")

    *建立具有空白表單的 View*

<a id="Ex4Task4"></a>

<a id="Task_4_-_Implementing_the_HTTP-POST_Create_Action_Method"></a>
#### <a name="task-4---implementing-the-http-post-create-action-method"></a>工作 4-執行 HTTP POST 建立動作方法

在這項工作中，您將會執行建立動作方法的 HTTP POST 版本，當使用者按一下 [**儲存**] 按鈕時將會叫用。 方法應該將新的專輯儲存在資料庫中。

1. 如有需要，請關閉瀏覽器，以返回 [Visual Studio] 視窗。 開啟**StoreManagerController**類別。 若要這麼做，請展開 [**控制器**] 資料夾，然後按兩下 [ **StoreManagerController.cs**]。
2. 將**HTTP POST 建立**動作方法程式碼取代為下列內容：

    （程式碼片段- *ASP.NET MVC 4 協助程式和表單和驗證-Ex4 STOREMANAGERCONTROLLER HTTP-POST 建立動作*）

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample14.cs)]

    > [!NOTE]
    > [建立] 動作與先前的 [編輯動作] 方法非常類似，但它不會將物件設定為已修改，而是加入至內容。

<a id="Ex4Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>工作 5-正在執行應用程式

在這項工作中，您將測試**StoreManager**的 [建立視圖] 頁面可讓您建立新的專輯，然後重新導向至 StoreManager 索引視圖。

1. 按**F5**執行應用程式。
2. 專案會在首頁中啟動。 將 URL 變更為 **/StoreManager/Create**。 以新專輯的資料填滿所有表單欄位，如下圖所示：

    ![建立專輯](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "建立專輯")

    *建立專輯*
3. 確認您已重新導向至 StoreManager 索引視圖，其中包含剛建立的新專輯。

    ![已建立新的專輯](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "已建立新的專輯")

    *已建立新的專輯*

<a id="Exercise5"></a>

<a id="Exercise_5_Handling_Deletion"></a>
### <a name="exercise-5-handling-deletion"></a>練習5：處理刪除

尚未實行刪除專輯的功能。 這就是本練習的相關內容。 就像之前一樣，您將使用**StoreManagerController**類別內的兩個不同方法來執行刪除案例：

1. 一個動作方法會顯示確認表單
2. 第二個動作方法會處理表單提交

<a id="Ex5Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Delete_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-delete-action-method"></a>工作 1-執行 HTTP-GET Delete 動作方法

在這項工作中，您將會執行 Delete 動作方法的 HTTP GET 版本來抓取專輯的資訊。

1. 開啟位於**來源/Ex5-HandlingDeletion/開始/** 資料夾的 [**開始**] 解決方案。 否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。

   1. 如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
2. 開啟**StoreManagerController**類別。 若要這麼做，請展開 [**控制器**] 資料夾，然後按兩下 [ **StoreManagerController.cs**]。
3. 「刪除控制器」動作與先前的「存放區詳細資料控制器」動作完全相同：它會使用 URL 中提供的**識別碼**從資料庫查詢**專輯**物件，並傳回適當的**視圖**。 若要這麼做，請將 HTTP-GET **Delete**動作方法程式碼取代為下列內容：

    （程式碼片段- *ASP.NET MVC 4 協助程式和表單和驗證 Ex5 處理刪除 HTTP-取得刪除動作*）

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample15.cs)]
4. 在**Delete**動作方法內按一下滑鼠右鍵，然後選取 [**加入視圖**]。 這會顯示 [加入視圖] 對話方塊。
5. 在 [加入視圖] 對話方塊中，確認視圖名稱為 [**刪除**]。 選取 [**建立強型別視圖**] 選項，然後從 [**模型類別**] 下拉式選單選取 [**專輯] （MvcMusicStore）** 。 從 [ **Scaffold 範本**] 下拉式選單中選取 [**刪除**]。 將其他欄位保留為預設值，然後按一下 [**新增**]。

    ![加入刪除視圖](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "加入刪除視圖")

    *加入刪除視圖*
6. [刪除] 範本會顯示模型中的所有欄位。 您只會顯示專輯的標題。 若要這麼做，請使用下列程式碼取代此視圖的內容：

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample16.cshtml)]

<a id="Ex05Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>工作 2-正在執行應用程式

在這項工作中，您將測試**StoreManager** **刪除**視圖頁面是否顯示確認刪除表單。

1. 按**F5**執行應用程式。
2. 專案會在首頁中啟動。 將 URL 變更為 **/StoreManager**。 按一下 [**刪除**]，然後確認已上傳新的視圖，以選取要刪除的一個專輯。

    ![刪除專輯](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "刪除專輯")

    *刪除專輯*

<a id="Ex05Task3"></a>

<a id="Task_3-_Implementing_the_HTTP-POST_Delete_Action_Method"></a>
#### <a name="task-3--implementing-the-http-post-delete-action-method"></a>工作 3-執行 HTTP POST 刪除動作方法

在這項工作中，您將會執行刪除動作方法的 HTTP POST 版本，當使用者按一下 [**刪除**] 按鈕時將會叫用。 方法應該刪除資料庫中的專輯。

1. 如有需要，請關閉瀏覽器，以返回 [Visual Studio] 視窗。 開啟**StoreManagerController**類別。 若要這麼做，請展開 [**控制器**] 資料夾，然後按兩下 [ **StoreManagerController.cs**]。
2. 將**HTTP POST 刪除**動作方法程式碼取代為下列內容：

    （程式碼片段- *ASP.NET MVC 4 協助程式和表單和驗證 Ex5 處理刪除 HTTP-POST 刪除動作*）

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample17.cs)]

<a id="Ex5Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>工作 4-正在執行應用程式

在這項工作中，您將測試**StoreManager 刪除**視圖頁面是否可讓您刪除專輯，然後重新導向至 StoreManager 索引視圖。

1. 按**F5**執行應用程式。
2. 專案會在首頁中啟動。 將 URL 變更為 **/StoreManager**。 按一下 [刪除] 來選取要刪除的一個專輯 **。** 按一下 [**刪除**] 按鈕以確認刪除：

    ![刪除專輯](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "刪除專輯")

    *刪除專輯*
3. 確認專輯已刪除，因為它不會出現在 [**索引**] 頁面中。

<a id="Exercise6"></a>

<a id="Exercise_6_Adding_Validation"></a>
### <a name="exercise-6-adding-validation"></a>練習6：加入驗證

目前，您現有的建立和編輯表單不會執行任何類型的驗證。 如果使用者將 [必要] 欄位保留空白，或在 [價格] 欄位中輸入字母，就會從資料庫中取得第一個錯誤。

您可以藉由將資料批註加入至模型類別，將驗證新增至應用程式。 資料批註允許描述您要套用至模型屬性的規則，而 ASP.NET MVC 會負責強制執行並向使用者顯示適當的訊息。

<a id="Ex06Task1"></a>

<a id="Task_1_-_Adding_Data_Annotations"></a>
#### <a name="task-1---adding-data-annotations"></a>工作 1-加入資料批註

在這項工作中，您會將資料批註加入至專輯模型，讓 [建立和編輯] 頁面在適當時顯示驗證訊息。

對於簡單的模型類別而言，加入資料批註只是藉由新增**system.workflow.componentmodel.activity**的**using**語句來處理，然後在適當的屬性上放置 **[Required]** 屬性。 下列範例會將**Name**屬性設為 View 中的必要欄位。

[!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample18.cs)]

這在產生實體資料模型的情況下，這種情況就會變得更複雜。 如果您將資料批註直接加入至模型類別，如果您從資料庫更新模型，就會覆寫它們。 相反地，您可以使用中繼資料部分類別來保存注釋，並使用 **[MetadataType]** 屬性與模型類別產生關聯。

1. 開啟位於**來源/Ex6-AddingValidation/開始/** 資料夾的 [**開始**] 解決方案。 否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。

   1. 如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
2. 從 [**模型**] 資料夾開啟**Album.cs** 。
3. 以反白顯示的程式碼取代**Album.cs**內容，使其看起來如下所示：

    > [!NOTE]
    > **[DisplayFormat （ConvertEmptyStringToNull = false）]** 這一行表示當資料欄位在資料來源中更新時，模型中的空字串將不會轉換成 null。 當 Entity Framework 在資料批註驗證欄位之前，將 null 值指派給模型時，這種設定會避免發生例外狀況。

    （程式碼片段- *ASP.NET MVC 4 協助程式和表單和驗證-Ex6 專輯中繼資料部分類別*）

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample19.cs)]

    > [!NOTE]
    > 此**專輯**部分類別具有**MetadataType**屬性，指向資料批註的**AlbumMetaData**類別。 以下是您用來標注專輯模型的一些資料批註屬性：
    > 
    > - 必要-指出屬性是必要欄位
    > - DisplayName-定義要在表單欄位和驗證訊息上使用的文字
    > - DisplayFormat-指定顯示和格式化資料欄位的方式。
    > - StringLength-定義字串欄位的最大長度
    > - 範圍-提供數值欄位的最大和最小值
    > - ScaffoldColumn-允許隱藏編輯表單中的欄位

<a id="Ex06Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>工作 2-正在執行應用程式

在這項工作中，您將使用上一個工作中所選擇的顯示名稱，測試 [建立] 和 [編輯] 頁面是否會驗證欄位。

1. 按**F5**執行應用程式。
2. 專案會在首頁中啟動。 將 URL 變更為 **/StoreManager/Create**。 確認顯示名稱符合部分類別中的名稱（例如**專輯封面 URL** ，而不是**AlbumArtUrl**）
3. 按一下 [**建立**]，而不填滿表單。 確認您取得對應的驗證訊息。

    ![[建立] 頁面中的已驗證欄位](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "[建立] 頁面中的已驗證欄位")

    *[建立] 頁面中的已驗證欄位*
4. 您可以使用 [**編輯**] 頁面確認相同的情況。 將 URL 變更為 **/StoreManager/Edit/1** ，並確認顯示名稱符合部分類別（例如**專輯封面 URL** ，而不是**AlbumArtUrl**）中的名稱。 清空 [**標題**] 和 [**價格**] 欄位，然後按一下 [**儲存**]。 確認您取得對應的驗證訊息。

    ![[編輯] 頁面中的已驗證欄位](aspnet-mvc-4-helpers-forms-and-validation/_static/image19.png)

    *[編輯] 頁面中的已驗證欄位*

<a id="Exercise7"></a>

<a id="Exercise_7_Using_Unobtrusive_jQuery_at_Client_Side"></a>
### <a name="exercise-7-using-unobtrusive-jquery-at-client-side"></a>練習7：在用戶端使用不顯眼的 jQuery

在此練習中，您將瞭解如何在用戶端啟用 MVC 4 不顯眼的 jQuery 驗證。

> [!NOTE]
> 不顯眼的 jQuery 會使用資料 ajax 前置詞 JavaScript，在伺服器上叫用動作方法，而不是干擾發出內嵌用戶端腳本。

<a id="Ex7Task1"></a>

<a id="Task_1_-_Running_the_Application_before_Enabling_Unobtrusive_jQuery"></a>
#### <a name="task-1---running-the-application-before-enabling-unobtrusive-jquery"></a>工作 1-在啟用不顯眼的 jQuery 之前執行應用程式

在這項工作中，您將在包含 jQuery 之前執行應用程式，以便比較這兩個驗證模型。

1. 開啟位於**來源/Ex7-UnobtrusivejQueryValidation/開始/** 資料夾的 [**開始**] 解決方案。 否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。

   1. 如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
2. 按 **F5** 執行應用程式。
3. 專案會在首頁中啟動。 流覽 **/StoreManager/Create** ，然後按一下 [**建立**] 而不填滿表單，以確認您取得驗證訊息：

    ![已停用用戶端驗證](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "已停用用戶端驗證")

    *已停用用戶端驗證*
4. 在瀏覽器中，開啟 HTML 原始程式碼：

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample20.html)]

<a id="Ex7Task2"></a>

<a id="Task_2_-_Enabling_Unobtrusive_Client_Validation"></a>
#### <a name="task-2---enabling-unobtrusive-client-validation"></a>工作 2-啟用不顯眼的用戶端驗證

在這項工作**中，您將從 web.config**檔案啟用 jQuery 不顯眼的**用戶端驗證**，在所有新的 ASP.NET MVC 4 專案中，預設都會設定為 false。 此外，您還會加入必要的腳本參考，以進行 jQuery 不顯眼的用戶端驗證工作。

1. 在專案根目錄開啟**web.config**檔案，並確定 [ **ClientValidationEnabled** ] 和 [ **UnobtrusiveJavaScriptEnabled**索引鍵] 值已設定為 [ **true**]。

    [!code-xml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample21.xml)]

    > [!NOTE]
    > 您也可以在 Global.asax.cs 的程式碼中啟用用戶端驗證，以取得相同的結果：
    > 
    > **HtmlHelper. ClientValidationEnabled = true;**
    > 
    > 此外，您可以將 ClientValidationEnabled 屬性指派給任何控制器，使其具有自訂行為。
2. 在**Views\StoreManager**開啟**Create. cshtml** 。
3. 請確定已透過 &quot; **~/bundles/jqueryval**&quot; 配套，在 view 中參考下列腳本檔案**jquery.** validate 和**jquery**。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample22.cshtml)]

    > [!NOTE]
    > 所有這些 jQuery 程式庫都包含在 MVC 4 新專案中。 您可以在專案的 **/Scripts**資料夾中找到更多程式庫。
    > 
    > 若要讓此驗證程式庫正常執行，您必須加入 jQuery framework 程式庫的參考。 因為此參考已經加入\_的配置**cshtml**檔案中，所以您不需要將它新增到這個特定的視圖中。

<a id="Ex7Task3"></a>

<a id="Task_3_-_Running_the_Application_Using_Unobtrusive_jQuery_Validation"></a>
#### <a name="task-3---running-the-application-using-unobtrusive-jquery-validation"></a>工作 3-使用不顯眼的 jQuery 驗證執行應用程式

在這項工作中，您將測試**StoreManager** create view 範本會在使用者建立新的專輯時，使用 jQuery 程式庫來執行用戶端驗證。

1. 按 **F5** 執行應用程式。
2. 專案會在首頁中啟動。 流覽 **/StoreManager/Create** ，然後按一下 [**建立**] 而不填滿表單，以確認您取得驗證訊息：

    ![已啟用 jQuery 的用戶端驗證](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "已啟用 jQuery 的用戶端驗證")

    *已啟用 jQuery 的用戶端驗證*
3. 在瀏覽器中，開啟 [建立視圖] 的原始程式碼：

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample23.html)]

   > [!NOTE]
   > 針對每個用戶端驗證規則，不顯眼的 jQuery 會加入具有資料 val-*rulename*=&quot;*訊息*&quot;的屬性。 以下是不顯眼的 jQuery 插入 html 輸入欄位來執行用戶端驗證的標記清單：
   > 
   > - 資料-val
   > - 資料-val-數位
   > - 資料-val-範圍
   > - 資料-val-範圍-分鐘/資料-val-範圍-最大值
   > - 資料-val-必要
   > - 資料-val-長度
   > - 資料-val-長度-最大/資料-val-長度-分鐘
   > 
   > 所有資料值都會填入模型**資料注釋**。 然後，在伺服器端運作的所有邏輯都可以在用戶端執行。 例如，Price 屬性在模型中具有下列資料批註：
   > 
   > [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample24.cs)]
   > 
   > 使用不顯眼的 jQuery 之後，產生的程式碼為：
   > 
   > [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample25.html)]

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>總結

藉由完成此實際操作實驗室，您已瞭解如何讓使用者使用下列各項來變更儲存在資料庫中的資料：

- 控制器動作，例如索引、建立、編輯、刪除
- ASP.NET MVC 在 HTML 資料表中顯示內容的功能
- 自訂 HTML 協助程式以改善使用者體驗
- 回應 HTTP GET 或 HTTP POST 呼叫的動作方法
- 類似視圖範本的共用編輯器範本，例如建立和編輯
- 下拉式清單等表單元素
- 模型驗證的資料批註
- 使用 jQuery 不顯眼程式庫的用戶端驗證

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附錄 A：安裝 Web 的 Visual Studio Express 2012

您可以使用 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** 安裝 Web 或另一個 &quot;Express&quot; 版本**的 Microsoft Visual Studio Express 2012** 。 下列指示會引導您完成使用*Microsoft Web Platform Installer*安裝*Visual studio Express 2012 for Web*所需的步驟。

1. 移至[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。 或者，如果您已經安裝 Web Platform Installer，您可以開啟它，然後使用 Windows Azure SDK&quot;來搜尋產品 &quot;<em>Visual Studio Express 2012 For Web</em> 。
2. 按一下 [**立即安裝**]。 如果您沒有**Web Platform Installer**系統會將您重新導向，先下載並安裝。
3. 開啟**Web Platform Installer**之後，請按一下 [**安裝**] 以啟動安裝程式。

    ![安裝 Visual Studio Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "安裝 Visual Studio Express")

    *安裝 Visual Studio Express*
4. 閱讀所有產品的授權和條款，然後按一下 [**我接受**] 繼續。

    ![接受授權條款](aspnet-mvc-4-helpers-forms-and-validation/_static/image23.png)

    *接受授權條款*
5. 等到下載和安裝程式完成為止。

    ![安裝進度](aspnet-mvc-4-helpers-forms-and-validation/_static/image24.png)

    *安裝進度*
6. 當安裝完成時，按一下 **[完成]** 。

    ![安裝已完成](aspnet-mvc-4-helpers-forms-and-validation/_static/image25.png)

    *安裝已完成*
7. 按一下 **[** 結束] 以關閉 Web Platform Installer。
8. 若要開啟 Web Visual Studio Express，請移至 [**開始**] 畫面，然後開始撰寫 &quot;**VS Express**&quot;，然後按一下 [ **VS Express for Web** ] 磚。

    ![VS Express for Web 磚](aspnet-mvc-4-helpers-forms-and-validation/_static/image26.png)

    *VS Express for Web 磚*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>附錄 B：使用程式碼片段

有了程式碼片段，您就可以輕鬆地擁有所需的所有程式碼。 實驗室檔會告訴您可以使用它們的確切時機，如下圖所示。

![使用 Visual Studio 程式碼片段將程式碼插入您的專案](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "使用 Visual Studio 程式碼片段將程式碼插入您的專案")

*使用 Visual Studio 程式碼片段將程式碼插入您的專案*

***若要使用鍵盤新增程式碼片段（C#僅限）***

1. 將游標放在您想要插入程式碼的位置。
2. 開始鍵入程式碼片段名稱（不含空格或連字號）。
3. 監看 IntelliSense 會顯示相符的程式碼片段名稱。
4. 選取正確的程式碼片段（或繼續輸入，直到選取整個程式碼片段的名稱為止）。
5. 按兩次 Tab 鍵，在游標位置插入程式碼片段。

![開始鍵入程式碼片段名稱](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "開始鍵入程式碼片段名稱")

*開始鍵入程式碼片段名稱*

![按 Tab 鍵以選取反白顯示的程式碼片段](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "按 Tab 鍵以選取反白顯示的程式碼片段")

*按 Tab 鍵以選取反白顯示的程式碼片段*

![再按一次 Tab 鍵，將會展開程式碼片段](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "再按一次 Tab 鍵，將會展開程式碼片段")

*再按一次 Tab 鍵，將會展開程式碼片段*

***若要使用滑鼠C#（、Visual Basic 和 XML）加入程式碼片段***sha-1. 以滑鼠右鍵按一下您要插入程式碼片段的位置。

1. 選取 [**插入程式碼片段**]，後面接著 [ **My Code 程式碼片段**]。
2. 按一下清單中的相關程式碼片段，即可加以選取。

![以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]")

*以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]*

![按一下清單中的相關程式碼片段，即可加以選取](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "按一下清單中的相關程式碼片段，即可加以選取")

*按一下清單中的相關程式碼片段，即可加以選取*
