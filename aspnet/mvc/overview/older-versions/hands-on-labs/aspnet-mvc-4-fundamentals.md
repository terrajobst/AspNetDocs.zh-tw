---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
title: ASP.NET MVC 4 基本概念 |Microsoft Docs
author: rick-anderson
description: 這個實際操作實驗室是以 MVC （模型視圖控制器）音樂商店為基礎，這是一項教學課程應用程式，其仲介紹了如何使用 ASP.NET MV 的逐步解說 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: b7dba543-73c3-4534-a9a0-ba70fa2c6a8a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
msc.type: authoredcontent
ms.openlocfilehash: 95e9b9f55b2080c0ed01dc34e3a32f9f1c905644
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598816"
---
# <a name="aspnet-mvc-4-fundamentals"></a>ASP.NET MVC 4 基本概念

依[Web Camp 團隊](https://twitter.com/webcamps)

[下載 Web Camp 訓練套件](https://aka.ms/webcamps-training-kit)

這個實際操作實驗室是以 MVC （模型視圖控制器）音樂商店為基礎，這是一種教學課程應用程式，介紹如何使用 ASP.NET MVC 和 Visual Studio 的逐步解說。 在整個實驗室中，您將學習簡單的功能，但同時使用這些技術。 您將從簡單的應用程式開始，並將其建立，直到您擁有功能完整的 ASP.NET MVC 4 Web 應用程式。

這個實驗室適用于 ASP.NET MVC 4。

如果您想要探索教學課程應用程式的 ASP.NET MVC 3 版本，您可以在[MVC-音樂存放區](https://github.com/evilDave/MVC-Music-Store)中找到它。

這個實際操作實驗室假設開發人員有經驗的 Web 開發技術，例如 HTML 和 JavaScript。

> [!NOTE]
> 所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可在[Microsoft web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)取得。 此實驗室的特定專案可在[ASP.NET MVC 4 基本](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals)概念中取得。

<a id="The_Music_Store_application"></a>
### <a name="the-music-store-application"></a>音樂存放區應用程式

將在此實驗室中建立的音樂存放區 web 應用程式包含三個主要部分：購物、結帳和管理。 訪客可以依內容類型流覽專輯、將專輯加入購物車、檢查其選擇，最後繼續簽出以登入並完成訂單。 此外，存放區系統管理員將能夠管理可用的專輯以及其主要屬性。

![音樂存放畫面](aspnet-mvc-4-fundamentals/_static/image1.png "音樂存放畫面")

*音樂存放畫面*

<a id="ASPNET_MVC_4_Essentials"></a>
### <a name="aspnet-mvc-4-essentials"></a>ASP.NET MVC 4 Essentials

音樂存放區應用程式將使用**Model View Controller （MVC）** 建立，這是將應用程式分成三個主要元件的架構模式：

- **模型**：模型物件是應用程式中用來執行領域邏輯的元件。 通常，模型物件也會在資料庫中捕獲和儲存模型狀態。
- **Views：** Views 是顯示應用程式的使用者介面（UI）的元件。 通常此 UI 是從模型資料建立。 例如，專輯的編輯檢視會根據專輯物件的目前狀態顯示文字方塊和下拉式清單。
- **控制器：** 控制器是處理使用者互動、操作模型，最後選取要呈現 UI 之視圖的元件。 在 MVC 應用程式中，檢視只會顯示資訊，而控制器則會處理及回應使用者輸入和互動。

MVC 模式可協助您建立應用程式，以區隔應用程式的不同層面（輸入邏輯、商務邏輯和 UI 邏輯），同時提供這些元素之間的鬆散結合。 這種區隔可協助您在建立應用程式時管理複雜性，因為它可讓您一次專注于一層面的執行。 此外，MVC 模式可讓您輕鬆地測試應用程式，同時也鼓勵使用以測試為導向的開發（TDD）來建立應用程式。

**ASP.NET MVC**架構提供 ASP.NET Web form 模式的替代方案，可用於建立以 MVC 為基礎的 ASP.NET web 應用程式。 **ASP.NET MVC**架構是輕量、高度可測試的呈現架構，（如同 Web 表單架構應用程式）已與現有的 ASP.NET 功能整合，例如主版頁面和以成員資格為基礎的驗證，因此您可以取得核心 .net framework 的所有威力。 如果您已經熟悉 ASP.NET Web form，這會很有用，因為您已經使用的所有程式庫也都可在 ASP.NET MVC 4 中取得。

此外，MVC 應用程式的三個主要元件之間的鬆散耦合也會提升平行開發。 比方說，有一位開發人員可以使用此視圖，第二位開發人員可以處理控制器邏輯，而第三位開發人員則可以專注于模型中的商務邏輯。

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>目標

在此實際操作實驗室中，您將瞭解如何：

- 根據音樂存放區應用程式教學課程從頭開始建立 ASP.NET MVC 應用程式
- 新增控制器以處理網站首頁的 Url，並流覽其主要功能
- 新增視圖以自訂顯示的內容及其樣式
- 新增模型類別以包含及管理資料和網域邏輯
- 使用視圖模型模式將控制器動作的資訊傳遞至視圖範本
- 探索適用于網際網路應用程式的 ASP.NET MVC 4 新範本

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Prerequisites

您必須具有下列專案，才能完成此實驗室：

- 適用于[Web 的 Visual Studio 2012 Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （如需如何安裝的指示，請參閱[附錄 A](#AppendixA) ）

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>安裝程式

**安裝程式碼片段**

為了方便起見，您將在此實驗室中管理的大部分程式碼都是以 Visual Studio 程式碼片段的形式提供。 若要安裝程式碼片段，請執行 **.\Source\Setup\CodeSnippets.vsi**檔案。

如果您不熟悉 Visual Studio Code 程式碼片段，而且想要瞭解如何使用，您可以參閱本檔中的附錄 &quot;[附錄 C：使用程式碼片段](#AppendixC)&quot;。

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>練習

這個實際操作實驗室是由下列練習所組成：

1. [練習1：建立 MusicStore ASP.NET MVC Web 應用程式專案](#Exercise1)
2. [練習2：建立控制器](#Exercise2)
3. [練習3：將參數傳遞至控制器](#Exercise3)
4. [練習4：建立視圖](#Exercise4)
5. [練習5：建立視圖模型](#Exercise5)
6. [練習6：使用 View 中的參數](#Exercise6)
7. [練習7：膝上圍繞 ASP.NET MVC 4 新範本](#Exercise7)

> [!NOTE]
> 每個練習都會伴隨一個**結束**資料夾，其中包含您在完成練習之後應該取得的結果解決方案。 如果您需要額外的協助來進行練習，您可以使用此解決方案做為指南。

完成此實驗室的預估時間： **60 分鐘**。

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_MusicStore_ASPNET_MVC_Web_Application_Project"></a>
### <a name="exercise-1-creating-musicstore-aspnet-mvc-web-application-project"></a>練習1：建立 MusicStore ASP.NET MVC Web 應用程式專案

在此練習中，您將瞭解如何在 Visual Studio 2012 Express for Web 以及其主要資料夾組織中建立 ASP.NET MVC 應用程式。 此外，您將學習如何加入新的控制器，並讓它在應用程式的首頁中顯示簡單的字串。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_ASPNET_MVC_Web_Application_Project"></a>
#### <a name="task-1---creating-the-aspnet-mvc-web-application-project"></a>工作 1-建立 ASP.NET MVC Web 應用程式專案

1. 在這項工作中，您將使用 MVC Visual Studio 範本來建立空白的 ASP.NET MVC 應用程式專案。 啟動**VS Express for Web**。
2. 按一下 [檔案] 功能表上的 [新增專案]。
3. 在 [**新增專案**] 對話方塊中，選取 [ **ASP.NET MVC 4 web 應用程式**] 專案類型，位於 [**視覺效果C#，** **web**範本清單] 底下。
4. 將**名稱**變更為*MvcMusicStore*。
5. 將解決方案的位置設定在此練習的源資料夾中新的 **開始**] 資料夾內，例如 **[您的 \Source\Ex01-CreatingMusicStoreProject\Begin**。 按一下 [確定]。

    ![[建立新專案] 對話方塊](aspnet-mvc-4-fundamentals/_static/image2.png "[建立新專案] 對話方塊")

    *[建立新專案] 對話方塊*
6. 在 [**新增 ASP.NET MVC 4 專案**] 對話方塊中，選取 [**基本**] 範本，並確定選取的 [**視圖引擎**] 為 [ **Razor**]。 按一下 [確定]。

    ![[新增 ASP.NET MVC 4 專案] 對話方塊](aspnet-mvc-4-fundamentals/_static/image3.png "[新增 ASP.NET MVC 4 專案] 對話方塊")

    *[新增 ASP.NET MVC 4 專案] 對話方塊*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Exploring_the_Solution_Structure"></a>
#### <a name="task-2---exploring-the-solution-structure"></a>工作 2-探索方案結構

ASP.NET MVC 架構包含一個 Visual Studio 專案範本，可協助您建立支援 MVC 模式的 Web 應用程式。 此範本會建立具有必要資料夾、專案範本和設定檔案專案的新 ASP.NET MVC Web 應用程式。

在這項工作中，您將檢查解決方案結構，以瞭解所牽涉的元素及其關聯性。 下列資料夾會包含在所有 ASP.NET MVC 應用程式中，因為 ASP.NET MVC 架構預設會使用 &quot;慣例，而不是透過設定&quot; 方法，並根據資料夾命名慣例做出一些預設假設。

1. 建立專案之後，請檢查在右側的方案總管中建立的資料夾結構：

    ![方案總管中的 ASP.NET MVC 資料夾結構](aspnet-mvc-4-fundamentals/_static/image4.png "方案總管中的 ASP.NET MVC 資料夾結構")

    *方案總管中的 ASP.NET MVC 資料夾結構*

   1. **控制器**。 此資料夾將包含控制器類別。 在 MVC 架構的應用程式中，控制器會負責處理使用者互動、操作模型，最後選擇要呈現 UI 的視圖。

       > [!NOTE]
       > MVC framework 需要所有控制器的名稱以 &quot;控制器&quot;結尾，例如 HomeController、LoginController 或 ProductController。
   2. **模型**。 此資料夾是針對代表 MVC Web 應用程式之應用程式模型的類別所提供。 這通常包括定義物件的程式碼，以及與資料存放區互動的邏輯。 通常實際的模型物件會位於不同的類別庫中。 不過，當您建立新的應用程式時，您可能會包含類別，然後在開發週期的稍後將它們移至不同的類別庫。
   3. **Views**。 此資料夾是瀏覽器的建議位置，這是負責顯示應用程式使用者介面的元件。 Views 會使用 .aspx、.ascx、cshtml 和 .master 檔案，以及任何與轉譯視圖相關的其他檔案。 Views 資料夾包含每個控制器的資料夾;此資料夾會以控制器名稱前置詞命名。 例如，如果您有一個名為**HomeController**的控制器，Views 資料夾將會包含一個名為 Home 的資料夾。 根據預設，當 ASP.NET MVC 架構載入視圖時，它會在 Views\controllerName 資料夾（**views [controllerName] [action] .aspx**）或 Razor 視圖的（**views [ControllerName] [action]. cshtml**）中尋找要求的視圖名稱的 .aspx 檔案。

      > [!NOTE]
      > 除了先前所列的資料夾，MVC Web 應用程式會使用**global.asax**檔案來設定全域 URL 路由預設值，並**使用 web.config 檔案**來設定應用程式。

<a id="Ex1Task3"></a>

<a id="Task_3_-_Adding_a_HomeController"></a>
#### <a name="task-3---adding-a-homecontroller"></a>工作 3-新增 HomeController

在不使用 MVC 架構的 ASP.NET 應用程式中，使用者互動會組織在頁面周圍，以及引發和處理來自這些頁面的事件。 相反地，使用者與 ASP.NET MVC 應用程式的互動會組織在控制器及其動作方法的周圍。

另一方面，ASP.NET MVC framework 會將 Url 對應至稱為「控制器」的類別。 控制器會處理連入要求、處理使用者輸入和互動、執行適當的應用程式邏輯，以及判斷要傳回給用戶端的回應（顯示 HTML、下載檔案、重新導向至不同的 URL 等等）。 在顯示 HTML 的情況下，控制器類別通常會呼叫個別的 view 元件，以產生要求的 HTML 標籤。 在 MVC 應用程式中，檢視只會顯示資訊，而控制器則會處理及回應使用者輸入和互動。

在這項工作中，您將會新增控制器類別，以處理音樂存放區網站首頁的 Url。

1. 以滑鼠右鍵按一下方案總管中的 [**控制器**] 資料夾，然後依序選取 [**新增**] 和 [**控制器**命令]：

    ![新增控制器命令](aspnet-mvc-4-fundamentals/_static/image5.png "新增控制器命令")

    *新增控制器命令*
2. [**新增控制器**] 對話方塊隨即出現。 將控制器命名為*HomeController* ，然後按 [**新增**]。

    ![[新增控制器] 對話方塊](aspnet-mvc-4-fundamentals/_static/image6.png "[新增控制器] 對話方塊")

    *[新增控制器] 對話方塊*
3. 檔案**HomeController.cs**會建立在 [**控制器**] 資料夾中。 為了讓**HomeController**在其索引動作上傳回字串，請以下列程式碼取代**Index**方法：

    （程式碼片段- *ASP.NET MVC 4 基本概念-Ex1 HomeController 索引*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample1.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>工作 4-正在執行應用程式

在這項工作中，您將在網頁瀏覽器中試用應用程式。

1. 按**F5**執行應用程式。 會編譯專案，並啟動本機 IIS Web 服務器。 本機 IIS Web 服務器會自動開啟網頁瀏覽器，指向網頁伺服器的 URL。

    ![在網頁瀏覽器中執行的應用程式](aspnet-mvc-4-fundamentals/_static/image7.png "在網頁瀏覽器中執行的應用程式")

    *在網頁瀏覽器中執行的應用程式*

    > [!NOTE]
    > 本機 IIS Web 服務器會以隨機的免費埠號碼來執行網站。 在上圖中，網站是在 `http://localhost:50103/`執行，因此正在使用埠50103。 您的埠號碼可能會有所不同。
2. 關閉瀏覽器。

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Controller"></a>
### <a name="exercise-2-creating-a-controller"></a>練習2：建立控制器

在此練習中，您將瞭解如何更新控制器，以執行音樂存放應用程式的簡單功能。 該控制器將會定義動作方法，以處理下列每個特定的要求：

- 音樂存放區中音樂內容的清單頁面
- 一種流覽頁面，其中列出特定內容類型的所有音樂專輯
- 顯示特定音樂專輯相關資訊的詳細資料頁面

針對此練習的範圍，這些動作只會立即傳回字串。

<a id="Ex2Task1"></a>

<a id="Task_1_-_Adding_a_New_StoreController_Class"></a>
#### <a name="task-1---adding-a-new-storecontroller-class"></a>工作 1-加入新的 StoreController 類別

在這項工作中，您將加入新的控制器。

1. 如果尚未開啟，請啟動**VS Express for Web 2012**。
2. 在 [檔案 **] 功能表中，選擇 [** **開啟專案**]。 在 [開啟專案] 對話方塊中，流覽至**Source\Ex02-CreatingAController\Begin**，選取 [**開始**]，然後按一下 [**開啟**]。 或者，您可以繼續進行上一個練習完成後取得的解決方案。

   1. 如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
3. 新增控制器。 若要這麼做，請在方案總管內的 [**控制器**] 資料夾上按一下滑鼠右鍵，然後依序選取 [**新增**] 和 [**控制器**] 命令。 將**控制器名稱**變更為*StoreController*，然後按一下 [**新增**]。

    ![[新增控制器] 對話方塊](aspnet-mvc-4-fundamentals/_static/image8.png "[新增控制器] 對話方塊")

    *[新增控制器] 對話方塊*

<a id="Ex2Task2"></a>

<a id="Task_2_-_Modifying_the_StoreControllers_Actions"></a>
#### <a name="task-2---modifying-the-storecontrollers-actions"></a>工作 2-修改 StoreController 的動作

在這項工作中，您將修改稱為「**動作**」的控制器方法。 動作會負責處理 URL 要求，以及判斷應該傳回給已叫用 URL 之瀏覽器或使用者的內容。

1. **StoreController**類別已經有**索引**方法。 您稍後會在此實驗室中使用它來執行列出音樂存放區所有內容類型的頁面。 目前，只要將**Index**方法取代為下列程式碼，即可從 Store. Index （）&quot;傳回字串 &quot;Hello：

    （程式碼片段- *ASP.NET MVC 4 基本概念-Ex2 StoreController 索引*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample2.cs)]
2. 新增**流覽**和**詳細資料**方法。 若要這麼做，請將下列程式碼新增至**StoreController**：

    （程式碼片段- *ASP.NET MVC 4 基本概念-Ex2 StoreController BrowseAndDetails*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample3.cs)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>工作 3-正在執行應用程式

在這項工作中，您將在網頁瀏覽器中試用應用程式。

1. 按**F5**執行應用程式。
2. 專案會在**首頁**中啟動。 變更 URL，以確認每個動作的執行。

    1. **/Store**。 您會看到 **&quot;Hello 從 Store. Index （）&quot;** 。
    2. **/Store/Browse**。 您會看到**來自 Store. Browse （）&quot;&quot;Hello** 。
    3. **/Store/Details**。 您會看到 **&quot;Hello From Store. Details （）&quot;** 。

        ![流覽 StoreBrowse](aspnet-mvc-4-fundamentals/_static/image9.png "流覽 StoreBrowse")

        *流覽/Store/Browse*
3. 關閉瀏覽器。

<a id="Exercise3"></a>

<a id="Exercise_3_Passing_parameters_to_a_Controller"></a>
### <a name="exercise-3-passing-parameters-to-a-controller"></a>練習3：將參數傳遞至控制器

到目前為止，您已從控制器傳回常數位串。 在此練習中，您將學習如何使用 URL 和 querystring 將參數傳遞至控制器，然後讓方法動作以文字回應瀏覽器。

<a id="Ex3Task1"></a>

<a id="Task_1_-_Adding_Genre_Parameter_to_StoreController"></a>
#### <a name="task-1---adding-genre-parameter-to-storecontroller"></a>工作 1-將內容類型參數新增至 StoreController

在這項工作中，您將使用**querystring**將參數傳送至**StoreController**中的**流覽**動作方法。

1. 如果尚未開啟，請啟動**VS Express for Web**。
2. 在 [檔案 **] 功能表中，選擇 [** **開啟專案**]。 在 [開啟專案] 對話方塊中，流覽至**Source\Ex03-PassingParametersToAController\Begin**，選取 [**開始**]，然後按一下 [**開啟**]。 或者，您可以繼續進行上一個練習完成後取得的解決方案。

   1. 如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
3. 開啟**StoreController**類別。 若要這麼做，請在 **方案總管**中展開 **控制器** 資料夾，然後按兩下  **StoreController.cs**。
4. 變更**流覽**方法，並新增字串參數來要求特定類型的類型。 ASP.NET MVC 會在叫用時，自動將名為內容**類型的任何**querystring 或表單 post 參數傳遞至此動作方法。 若要這麼做，請使用下列程式碼取代**流覽**方法：

    （程式碼片段- *ASP.NET MVC 4 基本概念-Ex3 StoreController BrowseMethod*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample4.cs)]

> [!NOTE]
> 您使用的是**HTTPutility.htmlencode. HtmlEncode**公用程式方法，以防止使用者使用/Store/Browse 之類的連結將 JAVAscript 插入此視圖 **？內容類型 =&lt;腳本&gt;視窗。位置 = '[http://hackersite.com](http://hackersite.com)'&lt;/script&gt;** 。
> 
> 如需進一步說明，請造訪[這篇 msdn 文章](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx)。

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>工作 2-正在執行應用程式

在這項工作中，您將在網頁瀏覽器中試用應用程式，並使用內容**類型參數。**

1. 按**F5**執行應用程式。
2. 專案會在**首頁**中啟動。 將 URL 變更為 */Store/Browse？內容類型 = Disco* ，用來驗證動作是否會接收內容類型參數。

    ![流覽 StoreBrowseGenre = Disco](aspnet-mvc-4-fundamentals/_static/image10.png "流覽 StoreBrowseGenre = Disco")

    *流覽/Store/Browse？內容類型 = Disco*
3. 關閉瀏覽器。

<a id="Ex3Task3"></a>

<a id="Task_3_-_Adding_an_Id_Parameter_Embedded_in_the_URL"></a>
#### <a name="task-3---adding-an-id-parameter-embedded-in-the-url"></a>工作 3-新增內嵌在 URL 中的 Id 參數

在這項工作中，您將使用**URL**將**Id**參數傳遞至**StoreController**的**Details**動作方法。 ASP.NET MVC 的預設路由慣例是在動作方法名稱之後，將 URL 的區段視為名為**Id**的參數。如果您的動作方法具有名為 Id 的參數，則 ASP.NET MVC 會自動將 URL 區段當做參數傳遞給您。 在 URL**存放區/詳細資料/5**中，**識別碼**會解讀為**5**。

1. 變更**StoreController**的**Details**方法，並新增名為**id**的**int**參數。若要這麼做，請以下列程式碼取代**Details**方法：

    （程式碼片段- *ASP.NET MVC 4 基本概念-Ex3 StoreController DetailsMethod*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample5.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>工作 4-正在執行應用程式

在這項工作中，您將在網頁瀏覽器中試用應用程式，並使用**Id**參數。

1. 按**F5**執行應用程式。
2. 專案會在**首頁**中啟動。 將 URL 變更為 */Store/Details/5* ，以確認動作會收到 id 參數。

    ![流覽 StoreDetails5](aspnet-mvc-4-fundamentals/_static/image11.png "流覽 StoreDetails5")

    *流覽/Store/Details/5*

<a id="Exercise4"></a>

<a id="Exercise_4_Creating_a_View"></a>
### <a name="exercise-4-creating-a-view"></a>練習4：建立視圖

到目前為止，您已從控制器動作傳回字串。 雖然這是瞭解控制器如何使用的實用方式，但並不是您實際 Web 應用程式的建立方式。 Views 是元件，可提供更好的方法，讓您使用範本檔案，將 HTML 產生回瀏覽器。

在此練習中，您將學習如何新增版面配置主版頁面，以設定常用 HTML 內容的範本，這是一個可增強網站外觀與風格的樣式表單，最後是一個可讓 HomeController 傳回 HTML 的視圖範本。

<a id="Ex4Task1"></a>

<a id="Task_1_-_Modifying_the_file__layoutcshtml"></a>
#### <a name="task-1---modifying-the-file-_layoutcshtml"></a>工作 1-修改檔案 \_配置. cshtml

檔案 **~/Views/Shared/\_layout**可讓您設定通用 HTML 的範本，以在整個網站上使用。 在這項工作中，您將新增具有通用標題的版面配置主版頁面，其中包含首頁和商店區域的連結。

1. 如果尚未開啟，請啟動**VS Express for Web**。
2. 在 [檔案 **] 功能表中，選擇 [** **開啟專案**]。 在 [開啟專案] 對話方塊中，流覽至**Source\Ex04-CreatingAView\Begin**，選取 [**開始**]，然後按一下 [**開啟**]。 或者，您可以繼續進行上一個練習完成後取得的解決方案。

   1. 如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
3. 檔案<strong>\_layout</strong>包含網站上所有頁面的 HTML 容器版面配置。 其中包含 HTML 回應的<strong>&lt;html&gt;</strong>元素，以及<strong>&lt;head&gt;</strong>和<strong>&lt;body&gt;</strong>元素。 HTML 主體中的<strong>@RenderBody（）</strong>會識別視圖範本能夠填入動態內容的區域。
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample6.cshtml)]
4. 新增通用標題，其中包含首頁的連結，以及網站中所有頁面上的存放區。 若要這麼做，請將下列程式碼加入 &lt;body&gt; 語句。
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample7.cshtml)]
5. 包含一個 div 來轉譯每個頁面的內文區段。 將<strong>@RenderBody（）</strong>取代為下列反白顯示的C#程式碼：（）

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample8.cshtml)]

    > [!NOTE]
    > 您知道嗎？ Visual Studio 2012 具有程式碼片段，可讓您輕鬆地在 HTML、程式碼檔案和更多功能中加入常用的程式碼！ 輸入 **&lt;div&gt;** 並按兩次**tab**鍵，以插入完整的**div**標記來試試看。

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_CSS_Stylesheet"></a>
#### <a name="task-2---adding-css-stylesheet"></a>工作 2-新增 CSS 樣式表單

空白專案範本包含非常簡單的 CSS 檔案，其中只包含用來顯示基本表單和驗證訊息的樣式。 您將使用其他 CSS 和影像（設計工具可能會提供），以增強網站的外觀與風格。

在這項工作中，您將新增 CSS 樣式表單以定義網站的樣式。

1. CSS 檔案和影像會包含在此實驗室的**Source\Assets\Content**資料夾中。 若要將它們新增至應用程式，請將其內容從**Windows Explorer**視窗拖曳至 Visual Studio Express for Web 中的**方案總管**，如下所示：

    ![拖曳樣式內容](aspnet-mvc-4-fundamentals/_static/image12.png "拖曳樣式內容")

    *拖曳樣式內容*
2. 隨即會出現警告對話方塊，要求確認取代**網站 .css**檔案和部分現有的影像。 勾選 [套用**至所有專案**]，然後按一下 **[是]** 。

<a id="Ex4Task3"></a>

<a id="Task_3_-_Adding_a_View_Template"></a>
#### <a name="task-3---adding-a-view-template"></a>工作 3-加入視圖範本

在這項工作中，您將加入一個 View 範本來產生 HTML 回應，以使用此練習中新增的版面配置主版頁面和 CSS。

1. 若要在流覽網站的首頁時使用視圖範本，您必須先指示，不要傳回字串， **HomeController Index**方法會傳回**View**。 開啟**HomeController**類別，並將其**Index**方法變更為傳回**ActionResult**，並讓它返回**View （）** 。

    （程式碼片段- *ASP.NET MVC 4 基本概念-Ex4 HomeController 索引*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample9.cs)]
2. 現在，您需要新增適當的視圖範本。 若要這麼做，請在**索引**動作方法內**按一下滑鼠右鍵**，然後選取 [**加入視圖**]。 這會顯示 [**加入視圖**] 對話方塊。

    ![從 Index 方法內加入視圖](aspnet-mvc-4-fundamentals/_static/image13.png "從 Index 方法內加入視圖")

    *從 Index 方法內加入視圖*
3. [**加入視圖**] 對話方塊隨即出現，以產生視圖範本檔案。 根據預設，這個對話方塊會預先填入視圖範本的名稱，使其符合將使用它的動作方法。 因為您在 HomeController 內的**索引**動作方法中使用了 [**加入視圖**] 內容功能表，所以 [**加入視圖**] 對話方塊的 [索引] 會是預設的 view name。 按一下 [新增]。

    ![[加入視圖] 對話方塊](aspnet-mvc-4-fundamentals/_static/image14.png "[加入視圖] 對話方塊")

    *[加入視圖] 對話方塊*
4. Visual Studio 會在**Views\Home**資料夾內產生一個. **cshtml**視圖範本，然後再開啟它。

    ![已建立主索引視圖](aspnet-mvc-4-fundamentals/_static/image15.png "已建立主索引視圖")

    *已建立主索引視圖*

    > [!NOTE]
    > **Index. cshtml**檔案的名稱和位置是相關的，並且遵循預設的 ASP.NET MVC 命名慣例。
    > 
    > 資料夾 \Views\**Home** 符合控制器名稱（**Home** controller）。 視圖範本名稱（**索引**）符合將顯示此視圖的控制器動作方法。
    > 
    > 如此一來，當使用此命名慣例來傳回視圖時，ASP.NET MVC 會避免必須明確指定視圖範本的名稱或位置。
5. 產生的視圖範本是以稍早定義的 **\_layout. cshtml**範本為基礎。 將 [ViewBag] 屬性更新為 [**首頁**]，並將主要內容變更為 **[首頁**]，如下列程式碼所示：

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample10.cshtml)]
6. 在方案總管中選取 [ **MvcMusicStore**專案]，然後按**F5**執行應用程式。

<a id="Ex4Task4"></a>

<a id="Task_4_Verification"></a>
#### <a name="task-4-verification"></a>工作4：驗證

若要確認您已正確執行前一個練習中的所有步驟，請依照以下方式進行：

當應用程式在瀏覽器中開啟時，您應該注意：

1. HomeController 的索引動作方法會找到並顯示 **\Views\Home\Index.cshtml** View 範本，即使程式碼稱為**return view （）** ，因為視圖範本會遵循標準命名慣例。
2. [首頁] 頁面會顯示在 **\Views\Home\Index.cshtml** view 範本中定義的歡迎訊息。
3. 首頁使用的是 **\_layout**樣板，因此歡迎訊息包含在標準網站 HTML 版面配置中。

    ![使用定義的 LayoutPage 和樣式的主索引視圖](aspnet-mvc-4-fundamentals/_static/image16.png "使用定義的 LayoutPage 和樣式的主索引視圖")

    *使用定義的 LayoutPage 和樣式的主索引視圖*

<a id="Exercise5"></a>

<a id="Exercise_5_Creating_a_View_Model"></a>
### <a name="exercise-5-creating-a-view-model"></a>練習5：建立視圖模型

到目前為止，您已將您的視圖顯示成硬式編碼 HTML，但為了建立動態 web 應用程式，視圖範本應該接收來自控制器的資訊。 要用於該用途的常見技巧之一是**ViewModel**模式，可讓控制器封裝產生適當 HTML 回應所需的所有資訊。

在此練習中，您將瞭解如何建立 ViewModel 類別，並新增必要的屬性：存放區中的內容類型，以及這些類型的清單。 您也會更新 StoreController 以使用建立的 ViewModel，最後，您將建立新的 View 範本，以在頁面中顯示提到的屬性。

<a id="Ex5Task1"></a>

<a id="Task_1_-_Creating_a_ViewModel_Class"></a>
#### <a name="task-1---creating-a-viewmodel-class"></a>工作 1-建立 ViewModel 類別

在這項工作中，您將建立一個 ViewModel 類別，它會實作為「商店內容類型」清單案例。

1. 如果尚未開啟，請啟動**VS Express for Web**。
2. 在 [檔案 **] 功能表中，選擇 [** **開啟專案**]。 在 [開啟專案] 對話方塊中，流覽至**Source\Ex05-CreatingAViewModel\Begin**，選取 [**開始**]，然後按一下 [**開啟**]。 或者，您可以繼續進行上一個練習完成後取得的解決方案。

   1. 如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
3. 建立**viewmodel**資料夾來保存 ViewModel。 若要這樣做，請以滑鼠右鍵按一下頂層**MvcMusicStore**專案 **，然後依序選取 [** 新增] 和 [**新增資料夾**]。

    ![加入新的資料夾](aspnet-mvc-4-fundamentals/_static/image17.png "加入新的資料夾")

    *加入新的資料夾*
4. 將資料夾命名為*viewmodel*。

    ![方案總管中的 Viewmodel 資料夾](aspnet-mvc-4-fundamentals/_static/image18.png "方案總管中的 Viewmodel 資料夾")

    *方案總管中的 Viewmodel 資料夾*
5. 建立**ViewModel**類別。 若要這麼做，請以滑鼠右鍵按一下最近建立的**viewmodel**資料夾 **，然後依序選取 [** 新增] 和 [**新增專案**]。 在 [程式**代碼**] 底下選擇**類別**專案，並將檔案命名為*StoreIndexViewModel.cs*，然後按一下 [**新增**]。

    ![加入新的類別](aspnet-mvc-4-fundamentals/_static/image19.png "加入新的類別")

    *加入新的類別*

    ![建立 StoreIndexViewModel 類別](aspnet-mvc-4-fundamentals/_static/image20.png "建立 StoreIndexViewModel 類別")

    *建立 StoreIndexViewModel 類別*

<a id="Ex5Task2"></a>

<a id="Task_2_-_Adding_Properties_to_the_ViewModel_class"></a>
#### <a name="task-2---adding-properties-to-the-viewmodel-class"></a>工作 2-將屬性新增至 ViewModel 類別

有兩個參數可從 StoreController 傳遞至 View 範本，以產生預期的 HTML 回應：存放區中的內容組數，以及這些內容的清單。

在這項工作中，您會將這**兩個屬性**新增至**StoreIndexViewModel**類別： **NumberOfGenres** （整數）和內容類型（字串清單）。

1. 將**NumberOfGenres**和**內容**類型屬性新增至**StoreIndexViewModel**類別。 若要這麼做，請將下列2行新增至類別定義：

    （程式碼片段- *ASP.NET MVC 4 基本概念-Ex5 StoreIndexViewModel 屬性*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample11.cs)]

> [!NOTE]
> **{Get; set;}** 標記法會使用C#的自動執行屬性功能。 它提供屬性的優點，而不需要我們宣告支援欄位。

<a id="Ex5Task3"></a>

<a id="Task_3_-_Updating_StoreController_to_use_the_StoreIndexViewModel"></a>
#### <a name="task-3---updating-storecontroller-to-use-the-storeindexviewmodel"></a>工作 3-更新 StoreController 以使用 StoreIndexViewModel

**StoreIndexViewModel**類別會封裝從**StoreController**的**Index**方法傳遞到 View 範本所需的資訊，以便產生回應。

在這項工作中，您將更新**StoreController**以使用**StoreIndexViewModel**。

1. 開啟**StoreController**類別。

    ![開啟 StoreController 類別](aspnet-mvc-4-fundamentals/_static/image21.png "開啟 StoreController 類別")

    *開啟 StoreController 類別*
2. 若要使用**StoreController**中的**StoreIndexViewModel**類別，請在**StoreController**程式碼的頂端新增下列命名空間：

    （程式碼片段- *ASP.NET MVC 4 基本概念-使用 viewmodel 的 Ex5 StoreIndexViewModel*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample12.cs)]
3. 變更**StoreController**的**索引**動作方法，讓它建立並填入**StoreIndexViewModel**物件，然後將它傳遞至 View 範本，以產生 HTML 回應。

    > [!NOTE]
    > 在實驗室 &quot;ASP.NET MVC 模型和資料存取&quot; 您會撰寫程式碼，以從資料庫中抓取商店內容清單。 在下列程式碼中，您將建立會填入**StoreIndexViewModel**的虛擬資料類型**清單**。
    > 
    > 建立並設定**StoreIndexViewModel**物件之後，它會當做引數傳遞給**View**方法。 這表示此視圖範本會使用該物件來產生 HTML 回應。
4. 以下列程式碼取代**Index**方法：

    （程式碼片段- *ASP.NET MVC 4 基本概念-Ex5 StoreController Index 方法*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample13.cs)]

> [!NOTE]
> 如果您不熟悉C#，可以假設使用**var**表示**viewModel**變數是晚期繫結。 這不正確， C#編譯器會根據您指派給變數的內容來使用型別推斷，以判斷**viewModel**的型別是**StoreIndexViewModel**。 此外，藉由將本機**viewModel**變數編譯為**StoreIndexViewModel**類型，您會取得編譯時期檢查，並 Visual Studio 程式碼編輯器支援。

<a id="Ex5Task4"></a>

<a id="Task_4_-_Creating_a_View_Template_that_Uses_StoreIndexViewModel"></a>
#### <a name="task-4---creating-a-view-template-that-uses-storeindexviewmodel"></a>工作 4-建立使用 StoreIndexViewModel 的視圖範本

在這項工作中，您將會建立一個視圖範本，以使用從控制器傳遞的 StoreIndexViewModel 物件來顯示內容清單。

1. 在建立新的視圖範本之前，讓我們先建立專案，使 [**加入視圖] 對話方塊**知道**StoreIndexViewModel**類別。 建立專案，方法是選取 [**建立**] 功能表項目，然後選取 [**建立 MvcMusicStore**]。

    ![建立專案](aspnet-mvc-4-fundamentals/_static/image22.png "建立專案")

    *建立專案*
2. 建立新的視圖範本。 若要這麼做，請在**索引**方法內部按一下滑鼠右鍵，然後選取 [**加入視圖**]。

    ![新增檢視](aspnet-mvc-4-fundamentals/_static/image23.png "新增檢視")

    *新增檢視*
3. 因為 [**加入視圖] 對話方塊**是從**StoreController**叫用的，所以預設會在 **\Views\Store\Index.cshtml**檔案中加入視圖範本。 勾選 [**建立強型別-view** ] 核取方塊，然後選取 [ **StoreIndexViewModel** ] 做為**模型類別**。 此外，請確定選取的 View engine 是**Razor**。 按一下 [新增]。

    ![[加入視圖] 對話方塊](aspnet-mvc-4-fundamentals/_static/image24.png "[加入視圖] 對話方塊")

    *[加入視圖] 對話方塊*

    隨即建立並開啟 **\Views\Store\Index.cshtml** View 範本檔案。 根據在最後一個步驟中提供給 [**加入視圖**] 對話方塊的資訊，View 範本會預期**StoreIndexViewModel**實例會當做用來產生 HTML 回應的資料。 您會注意到範本會繼承中C#的 `ViewPage<musicstore.viewmodels.storeindexviewmodel>`。

<a id="Ex5Task5"></a>

<a id="Task_5_-_Updating_the_View_Template"></a>
#### <a name="task-5---updating-the-view-template"></a>工作 5-更新視圖範本

在這項工作中，您將更新在上一個工作中建立的視圖範本，以抓取頁面中的內容和名稱的數目。

> [!NOTE]
> 您將使用 @ 語法（通常稱為 &quot;程式碼區塊&quot;）來執行 View 範本中的程式碼。

1. 在 [**存放區**] 資料夾中的**索引. cshtml**檔案中，將其程式碼取代為下列內容：

[!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample14.cshtml)]

    > [!NOTE]
    > As soon as you finish typing the period after the word **Model**, Visual Studio's Intellisense will show a list of possible properties and methods to choose from.
    > 
    > ![](aspnet-mvc-4-fundamentals/_static/image25.png)
    > 
    > *Getting Model properties and methods with Visual Studio's IntelliSense*
    > 
    > The **Model** property references the **StoreIndexViewModel** object that the Controller passed to the View template. This means that you can access all of the data passed from the Controller to the View template via the **Model** property, and format it into an appropriate HTML response within the View template.
    > 
    > You can just select the **NumberOfGenres** property from the Intellisense list rather than typing it in and then it will auto-complete it by pressing the **tab key**.
2. 在**StoreIndexViewModel**中的內容類型清單上迴圈，並使用**FOREACH**迴圈建立 HTML **&lt;ul&gt;** 清單。
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample15.cshtml)]
3. 按**F5**執行應用程式並流覽 **/Store**。 您會在**StoreIndexViewModel**物件中看到從**StoreController**傳遞至 View 範本的內容清單。

    ![顯示內容清單的視圖](aspnet-mvc-4-fundamentals/_static/image26.png "顯示內容清單的視圖")

    *顯示內容清單的視圖*
4. 關閉瀏覽器。

<a id="Exercise6"></a>

<a id="Exercise_6_Using_Parameters_in_View"></a>
### <a name="exercise-6-using-parameters-in-view"></a>練習6：使用 View 中的參數

在練習3中，您已瞭解如何將參數傳遞至控制器。 在此練習中，您將瞭解如何在 View 範本中使用這些參數。 基於這個目的，您將會先引進模型類別，協助您管理資料和領域邏輯。 此外，您將學習如何在 ASP.NET MVC 應用程式內建立頁面的連結，而不需要擔心 URL 路徑編碼之類的事情。

<a id="Ex6Task1"></a>

<a id="Task_1_-_Adding_Model_Classes"></a>
#### <a name="task-1---adding-model-classes"></a>工作 1-加入模型類別

不同于 Viewmodel，只是為了將資訊從控制器傳遞至視圖，而建立模型類別是為了包含及管理資料和網域邏輯。 在這項工作中，您將新增兩個模型類別來表示這些**概念：內容**類型和**專輯**。

1. 如果尚未開啟，請啟動**VS Express for Web**
2. 在 [檔案 **] 功能表中，選擇 [** **開啟專案**]。 在 [開啟專案] 對話方塊中，流覽至**Source\Ex06-UsingParametersInView\Begin**，選取 [**開始**]，然後按一下 [**開啟**]。 或者，您可以繼續進行上一個練習完成後取得的解決方案。

   1. 如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
3. 加入內容**類型模型類別**。 若要這麼做，請以滑鼠右鍵按一下**方案總管**中的 [**模型**] 資料夾，然後依序選取 [**加入**] 和 [**新增專案**] 選項。 在 [程式**代碼**] 底下選擇**類別**專案，並將檔案命名為*Genre.cs*，然後按一下 [**新增**]。

    ![新增類別](aspnet-mvc-4-fundamentals/_static/image27.png "新增類別")

    *加入新專案*

    ![加入內容類型模型類別](aspnet-mvc-4-fundamentals/_static/image28.png "加入內容類型模型類別")

    *加入內容類型模型類別*
4. 將 [**名稱**] 屬性加入至 [內容類型] 類別。 若要這麼做，請新增下列程式碼：

    （程式碼片段- *ASP.NET MVC 4 基本概念-Ex6*內容類型）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample16.cs)]
5. 遵循與先前相同的程式，加入**專輯**類別。 若要這麼做，請以滑鼠右鍵按一下**方案總管**中的 [**模型**] 資料夾，然後依序選取 [**加入**] 和 [**新增專案**] 選項。 在 [程式**代碼**] 底下選擇**類別**專案，並將檔案命名為*Album.cs*，然後按一下 [**新增**]。
6. 將兩個屬性新增至專輯類別 **：內容**類型和**標題**。 若要這麼做，請新增下列程式碼：

    （程式碼片段- *ASP.NET MVC 4 基本概念-Ex6 專輯*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample17.cs)]

<a id="Ex6Task2"></a>

<a id="Task_2_-_Adding_a_StoreBrowseViewModel"></a>
#### <a name="task-2---adding-a-storebrowseviewmodel"></a>工作 2-新增 StoreBrowseViewModel

此工作中將會使用**StoreBrowseViewModel**來顯示符合所選類型的專輯。 在這項工作中，您將建立此類別，然後新增兩個屬性來處理內容**類型和其** **專輯**清單。

1. 新增**StoreBrowseViewModel**類別。 若要這麼做，請以滑鼠右鍵按一下**方案總管**中的 [ **viewmodel** ] 資料夾 **，然後依序選取 [** 新增] 和 [**新專案**] 選項。 在 [程式**代碼**] 底下選擇**類別**專案，並將檔案命名為*StoreBrowseViewModel.cs*，然後按一下 [**新增**]。
2. 在**StoreBrowseViewModel**類別中加入模型的參考。 若要這麼做，請使用命名空間新增下列內容：

    （程式碼片段- *ASP.NET MVC 4 基本概念-Ex6 UsingModel*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample18.cs)]
3. 將兩個屬性新增至 StoreBrowseViewModel**類別：內容**類型和**專輯**。 若要這麼做，請新增下列程式碼：

    （程式碼片段- *ASP.NET MVC 4 基本概念-Ex6 ModelProperties*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample19.cs)]

> [!NOTE]
> 什麼是 **&lt;專輯&gt;清單**？：此定義使用**清單&lt;t&gt;** 類型，其中**t**會限制此**清單**元素所屬的類型，在此案例中為**專輯**（或其子系）。
> 
> 設計類別和方法以延遲一或多個類型的規格，直到用戶端程式代碼宣告並具現化類別或方法，這項功能就是C#稱為**泛型**的語言之一。
> 
> **清單&lt;t&gt;** 是**ArrayList**類型的泛型對應項，而且可以在**system.string 命名空間中使用。** 使用**泛型**的優點之一，是因為指定了型別，所以您不需要處理型別檢查作業，像是使用**ArrayList**來將元素轉換成**專輯**一樣。

<a id="Ex6Task3"></a>

<a id="Task_3_-_Using_the_New_ViewModel_in_the_StoreController"></a>
#### <a name="task-3---using-the-new-viewmodel-in-the-storecontroller"></a>工作 3-在 StoreController 中使用新的 ViewModel

在這項工作中，您將修改**StoreController**的 **[流覽] 和 [** **詳細資料**] 動作方法，以使用新的**StoreBrowseViewModel**。

1. 將參考新增至**StoreController**類別中的 [模型] 資料夾。 若要這麼做，請展開 **方案總管**中的 **控制器** 資料夾，然後開啟**StoreController**類別。 然後新增下列程式碼：

    （程式碼片段- *ASP.NET MVC 4 基本概念-Ex6 UsingModelInController*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample20.cs)]
2. 取代**流覽**動作方法以使用**StoreViewBrowseController**類別。 您將建立具有虛擬資料的內容類型和兩個新的專輯物件（在下一個實際操作實驗室中，您將會取用資料庫中的實際資料）。 若要這麼做，請使用下列程式碼取代**流覽**方法：

    （程式碼片段- *ASP.NET MVC 4 基本概念-Ex6 BrowseMethod*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample21.cs)]
3. 取代**Details**動作方法以使用**StoreViewBrowseController**類別。 您將建立新的**專輯**物件，以傳回給**視圖**。 若要這麼做，請以下列程式碼取代**Details**方法：

    （程式碼片段- *ASP.NET MVC 4 基本概念-Ex6 DetailsMethod*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample22.cs)]

<a id="Ex6Task4"></a>

<a id="Task_4_-_Adding_a_Browse_View_Template"></a>
#### <a name="task-4---adding-a-browse-view-template"></a>工作 4-加入流覽視圖範本

在這項工作中，您將新增 **[流覽]** 視圖，以顯示找到特定類型的專輯。

1. 在建立新的視圖範本之前，您應該先建立專案，讓 [**加入視圖**] 對話方塊知道要使用的**ViewModel**類別。 建立專案，方法是選取 [**建立**] 功能表項目，然後選取 [**建立 MvcMusicStore**]。
2. 新增 **[流覽]** 視圖。 若要這麼做，請在**StoreController**的 [**流覽動作]** 方法中按一下滑鼠右鍵，然後按一下 [**加入視圖**]。
3. 在 [**加入視圖**] 對話方塊中，確認視圖名稱為 **[流覽]** 。 勾選 [**建立強型別視圖**] 核取方塊，然後從 [**模型類別**] 下拉式清單中選取 [ **StoreBrowseViewModel** ]。 將其他欄位保留為預設值。 然後按一下 [加入]。

    ![加入流覽視圖](aspnet-mvc-4-fundamentals/_static/image29.png "加入流覽視圖")

    *加入流覽視圖*
4. 修改**Browse**以顯示內容類型的資訊，並存取傳遞至視圖範本的**StoreBrowseViewModel**物件。 若要這麼做，請將內容取代為下列各C#項：（）

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample23.cshtml)]

<a id="Ex6Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>工作 5-正在執行應用程式

在這項工作中，您將測試**流覽**方法從**流覽**方法動作中抓取專輯。

1. 按**F5**執行應用程式。
2. 專案會在首頁中啟動。 將 URL 變更為 **/Store/Browse？內容類型 = Disco** ，用以確認動作會傳回兩個專輯。

    ![流覽存放區 Disco 專輯](aspnet-mvc-4-fundamentals/_static/image30.png "流覽存放區 Disco 專輯")

    *流覽存放區 Disco 專輯*

<a id="Ex6Task6"></a>

<a id="Task_6_-_Displaying_information_About_a_Specific_Album"></a>
#### <a name="task-6---displaying-information-about-a-specific-album"></a>工作 6-顯示特定專輯的相關資訊

在這項工作中，您將會執行 [ **Store/Details** ] 視圖，以顯示特定專輯的相關資訊。 在這個實際操作的實驗室中，您將會看到有關專輯的所有內容，都已經包含在**View**範本中。 因此，您不需要建立**StoreDetailsViewModel**類別，而是使用目前的**StoreBrowseViewModel**範本將專輯傳遞給它。

1. 如有需要，請關閉瀏覽器，以返回 [Visual Studio] 視窗。 為**StoreController**的**詳細資料**動作方法新增新的**詳細資料**視圖。 若要這樣做，請以滑鼠右鍵按一下 [ **StoreController** ] 類別中的**詳細資料**方法，然後按一下 [**新增視圖**]。
2. 在 [**加入視圖**] 對話方塊中，確認**視圖名稱**為 [**詳細資料**]。 勾選 [**建立強型別視圖**] 核取方塊，然後從 [**模型類別**] 下拉式方塊中選取 [**專輯**]。 將其他欄位保留為預設值。 然後按一下 [加入]。 這會建立並開啟 **\Views\Store\Details.cshtml**檔案。

    ![新增詳細資料檢視](aspnet-mvc-4-fundamentals/_static/image31.png "新增詳細資料檢視")

    *新增詳細資料檢視*
3. 修改**Details**檔案以顯示專輯資訊，存取傳遞至 view 範本的**專輯**物件。 若要這麼做，請將內容取代為下列各C#項：（）

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample24.cshtml)]

<a id="Ex6Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a>工作 7-執行應用程式

在這項工作中，您將測試**詳細資料**視圖是否從**details 動作**方法中抓取專輯資訊。

1. 按**F5**執行應用程式。
2. 專案會在**首頁**中啟動。 將 URL 變更為 **/Store/Details/5** ，以驗證專輯的資訊。

    ![流覽專輯詳細資料](aspnet-mvc-4-fundamentals/_static/image32.png "流覽專輯詳細資料")

    *流覽專輯的詳細資料*

<a id="Ex6Task8"></a>

<a id="Task_8_-_Adding_Links_Between_Pages"></a>
#### <a name="task-8---adding-links-between-pages"></a>工作 8-在頁面之間新增連結

在這項工作中，您會在 [存放區] 視圖中新增連結，讓每個內容類型名稱中的連結都具有適當的 **/Store/Browse** URL。 如此一來，當您按一下內容類型（例如**Disco**）時，它會流覽至 **/Store/Browse？內容類型 = Disco** URL。

1. 如有需要，請關閉瀏覽器，以返回 [Visual Studio] 視窗。 更新 [**索引**] 頁面，將連結新增至**流覽**頁面。 若要這麼做，請在**方案總管**展開 [ **Views** ] 資料夾，然後按一下 [ **Store** ] 資料夾，再按兩下 [ **Index. cshtml** ] 頁面。
2. 新增 [流覽] 視圖的連結，指出已選取的內容類型。 若要這麼做，請將下列反白顯示的程式碼取代為 **&lt;li&gt;** 標記：（C#）

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample25.cshtml)]

   > [!NOTE]
   > 另一種方法是直接連結到頁面，其程式碼如下所示：
   > 
   > &lt;href =&quot;/Store/Browse？內容類型 =@genreName&quot;&gt;@genreName&lt;/a&gt;
   > 
   > 雖然這種方法可行，但它相依于硬式編碼的字串。 如果您稍後重新命名控制器，就必須手動變更此指令。 更好的替代方式是使用**HTML Helper**方法。 ASP.NET MVC 包含適用于這類工作的 HTML Helper 方法。 **.Html （）** helper 方法可讓您輕鬆地建立 html **&lt;&gt;** 連結，確保 url 路徑的 url 編碼正確。
   > 
   > Html.actionlink 有數個多載。 在此練習中，您將使用接受三個參數的其中一個：
   > 
   > 1. 連結文字，會顯示內容類型名稱
   > 2. 控制器動作名稱（**流覽**）
   > 3. 路由參數值，同時指定**名稱（內容**類型）和值（內容類型**名稱**）

<a id="Ex6Task9"></a>

<a id="Task_9_-_Running_the_Application"></a>
#### <a name="task-9---running-the-application"></a>工作 9-正在執行應用程式

在這項工作中，您將測試每個內容類型是否顯示，並附有適當 **/Store/Browse** URL 的連結。

1. 按**F5**執行應用程式。
2. 專案會在首頁中啟動。 將 URL 變更為 **/Store** ，以確認每個內容類型都連結到適當的 **/Store/Browse** URL。

    ![流覽具有流覽頁面連結的內容內容](aspnet-mvc-4-fundamentals/_static/image33.png "流覽具有流覽頁面連結的內容內容")

    *流覽具有流覽頁面連結的內容內容*

<a id="Ex6Task10"></a>

<a id="Task_10_-_Using_Dynamic_ViewModel_Collection_to_Pass_Values"></a>
#### <a name="task-10---using-dynamic-viewmodel-collection-to-pass-values"></a>工作 10-使用動態 ViewModel 集合來傳遞值

在這項工作中，您將學習簡單且功能強大的方法，以便在控制器和視圖之間傳遞值，而不需要在模型中進行任何變更。 ASP.NET MVC 4 提供集合 &quot;ViewModel&quot;，可以指派給任何動態值，並在控制器和 views 內進行存取。

您現在將使用 ViewBag 動態集合，將從控制器&quot; 的 &quot;**加星號**內容清單傳遞給視圖。 [存放區索引] 視圖將會存取**ViewModel**並顯示資訊。

1. 如有需要，請關閉瀏覽器，以返回 [Visual Studio] 視窗。 開啟**StoreController.cs**並修改**Index**方法，以在 ViewModel 集合中建立加星號的內容清單：

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample26.cs)]

    > [!NOTE]
    > 您也可以使用語法**ViewBag [&quot;加星號&quot;]** 來存取屬性。
2. 此實驗室的**Source\Assets\Images**資料夾中包含 **&quot;&quot;加星號**的星星圖示。 若要將其新增至應用程式，請將其內容從**Windows Explorer**視窗拖曳至 Visual Web Developer Express 中的**方案總管**，如下所示：

    ![將星形影像新增至解決方案](aspnet-mvc-4-fundamentals/_static/image34.png "將星形影像新增至解決方案")

    *將星形影像新增至解決方案*
3. 開啟 view **Store/Index. cshtml**並修改內容。 您將讀取**ViewBag**集合中的 &quot;加星號&quot; 屬性，並詢問目前的內容類型名稱是否在清單中。 在此情況下，您會向 [內容類型] 連結顯示星形圖示。
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample27.cshtml)]

<a id="Ex6Task11"></a>

<a id="Task_11_-_Running_the_Application"></a>
#### <a name="task-11---running-the-application"></a>工作 11-正在執行應用程式

在這項工作中，您將測試加星號的內容內容是否顯示星形圖示。

1. 按**F5**執行應用程式。
2. 專案會在**首頁**中啟動。 將 URL 變更為 **/Store** ，以確認每個精選的內容類型都具有 [遵循] 標籤：

    ![使用加星號專案流覽內容流派](aspnet-mvc-4-fundamentals/_static/image35.png "使用加星號專案流覽內容流派")

    *使用加星號專案流覽內容流派*

<a id="Exercise7"></a>

<a id="Exercise_7_A_lap_around_ASPNET_MVC_4_new_template"></a>
### <a name="exercise-7-a-lap-around-aspnet-mvc-4-new-template"></a>練習7：膝上圍繞 ASP.NET MVC 4 新範本

在此練習中，您將探索 ASP.NET MVC 4 專案範本中的增強功能，並查看新範本最相關的功能。

<a id="Ex7Task1"></a>

<a id="Task_1_Exploring_the_ASPNET_MVC_4_Internet_Application_Template"></a>
#### <a name="task-1-exploring-the-aspnet-mvc-4-internet-application-template"></a>工作1：探索 ASP.NET MVC 4 網際網路應用程式範本

1. 如果尚未開啟，請啟動**VS Express for Web**
2. 選取檔案 **|新增 |[專案**] 功能表命令。 在 [**新增專案**] 對話方塊中，**選取C#視覺效果 |Web**範本：在左窗格樹狀結構上，選擇 [ **ASP.NET MVC 4 Web 應用程式**]。 將專案**命名**為*MusicStore* ，並將**方案名稱**更新為 [*開始*]，然後選取位置（或保留預設值），然後按一下 **[確定]** 。

    ![建立新的 ASP.NET MVC 4 專案](aspnet-mvc-4-fundamentals/_static/image36.png "建立新的 ASP.NET MVC 4 專案")

    *建立新的 ASP.NET MVC 4 專案*
3. 在 [**新增 ASP.NET MVC 4 專案**] 對話方塊中，選取 [**網際網路應用程式**] 專案範本，然後按一下 **[確定]** 。 請注意，您可以選取 Razor 或 ASPX 做為 view engine。

    ![建立新的 ASP.NET MVC 4 網際網路應用程式](aspnet-mvc-4-fundamentals/_static/image37.png "建立新的 ASP.NET MVC 4 網際網路應用程式")

    *建立新的 ASP.NET MVC 4 網際網路應用程式*

    > [!NOTE]
    > Razor 語法已在 ASP.NET MVC 3 中引進。 其目標是要將檔案中所需的字元和按鍵數目降至最低，以啟用快速且流暢的程式碼撰寫工作流程。 Razor 利用現有C#的/VB （或其他）語言技能，並提供範本標記語法來啟用絕佳的 HTML 結構工作流程。
4. 按**F5**執行方案，並查看已更新的範本。 您可以查看下列功能：

    1. **現代化樣式範本**

        這些範本已更新，提供更現代化的樣式。

        ![ASP.NET MVC 4 風貌範本](aspnet-mvc-4-fundamentals/_static/image38.png "ASP.NET MVC 4 風貌範本")

        *ASP.NET MVC 4 風貌範本*
    2. **適應性呈現**

        查看調整瀏覽器視窗的大小，並注意頁面配置如何動態適應新的視窗大小。 這些範本會使用自動調整轉譯技術，在桌上型電腦和行動平臺中正確轉譯，而不需要任何自訂。

        ![不同瀏覽器大小的 ASP.NET MVC 4 專案範本](aspnet-mvc-4-fundamentals/_static/image39.png "不同瀏覽器大小的 ASP.NET MVC 4 專案範本")

        *不同瀏覽器大小的 ASP.NET MVC 4 專案範本*
5. 關閉瀏覽器以停止偵錯工具，並返回 Visual Studio。
6. 現在您可以流覽解決方案，並查看 ASP.NET MVC 4 在專案範本中引進的一些新功能。

    ![ASP.NET MVC4-網際網路-應用程式-專案範本](aspnet-mvc-4-fundamentals/_static/image40.png "ASP.NET MVC 4 網際網路應用程式專案範本")

    *ASP.NET MVC 4 網際網路應用程式專案範本*

   1. **HTML5 標記**

       流覽範本視圖以找出新的主題標記，例如，在**主**資料夾內開啟**About. cshtml** view。

       ![使用 Razor 和 HTML5 標記的新範本](aspnet-mvc-4-fundamentals/_static/image41.png "使用 Razor 和 HTML5 標記的新範本")

       *使用 Razor 和 HTML5 標記的新範本*
   2. **包含的 JavaScript 程式庫**

      1. **jquery**： jquery 簡化了 HTML 檔案的遍歷、事件處理、動畫，以及 Ajax 互動。
      2. **JQUERY UI**：此程式庫提供建立于 jQuery JavaScript 程式庫之上的低層級互動和動畫、advanced 效果和 themeable widget 的抽象概念。

         > [!NOTE]
         > 您可以在[[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/)中瞭解 jQuery 和 jquery UI。
      3. **KnockoutJS**： ASP.NET MVC 4 預設範本現在包含**KnockoutJS**，這是一種 javascript MVVM 架構，可讓您使用 javascript 和 HTML 建立豐富且回應速度高的 web 應用程式。 如同在 ASP.NET MVC 3 中，jQuery 和 jQuery UI 程式庫也包含在 ASP.NET MVC 4 中。

          > [!NOTE]
          > 您可以在此連結中取得 KnockOutJS 程式庫的詳細資訊： [http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)。
      4. **Modernizr**：此程式庫會自動執行，讓您的網站在使用 HTML5 和 CSS3 技術時與舊版瀏覽器相容。

          > [!NOTE]
          > 您可以在此連結中取得 Modernizr 程式庫的詳細資訊： [http://www.modernizr.com/](http://www.modernizr.com/)。
   3. **解決方案中包含的 SimpleMembership**

       SimpleMembership 已設計為取代先前的 ASP.NET 角色和成員資格提供者系統。 它有許多新功能，可讓開發人員更輕鬆地以更有彈性的方式保護網頁。

       網際網路範本已設定一些專案來整合 SimpleMembership，例如，AccountController 已準備好使用 OAuthWebSecurity （適用于 OAuth 帳戶註冊、登入、管理等）和 Web 安全性。

       ![解決方案中包含的 SimpleMembership](aspnet-mvc-4-fundamentals/_static/image42.png "解決方案中包含的 SimpleMembership")

       *解決方案中包含的 SimpleMembership*

       > [!NOTE]
       > 在 MSDN 中尋找有關[OAuthWebSecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx)的詳細資訊。

> [!NOTE]
> 此外，您可以遵循[附錄 B：使用 Web Deploy 發佈 ASP.NET MVC 4 應用程式](#AppendixB)，將此應用程式部署到 Windows Azure 網站。

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>總結

藉由完成此實際操作實驗室，您已瞭解 ASP.NET MVC 的基本概念：

- MVC 應用程式的核心元素及其互動方式
- 如何建立 ASP.NET MVC 應用程式
- 如何新增和設定控制器來處理透過 URL 和 querystring 傳遞的參數
- 如何新增版面配置主版頁面來設定常用 HTML 內容的範本、增強外觀與風格的樣式表單，以及顯示 HTML 內容的視圖範本
- 如何使用 ViewModel 模式將屬性傳遞至 View 範本以顯示動態資訊
- 如何使用傳遞至 View 範本中之控制器的參數
- 如何將連結新增至 ASP.NET MVC 應用程式內的頁面
- 如何在視圖中新增和使用動態屬性
- ASP.NET MVC 4 專案範本中的增強功能

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附錄 A：安裝 Web 的 Visual Studio Express 2012

您可以使用 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** 安裝 Web 或另一個 &quot;Express&quot; 版本**的 Microsoft Visual Studio Express 2012** 。 下列指示會引導您完成使用*Microsoft Web Platform Installer*安裝*Visual studio Express 2012 for Web*所需的步驟。

1. 移至[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。 或者，如果您已經安裝 Web Platform Installer，您可以開啟它，然後使用 Windows Azure SDK&quot;來搜尋產品 &quot;<em>Visual Studio Express 2012 For Web</em> 。
2. 按一下 [**立即安裝**]。 如果您沒有**Web Platform Installer**系統會將您重新導向，先下載並安裝。
3. 開啟**Web Platform Installer**之後，請按一下 [**安裝**] 以啟動安裝程式。

    ![安裝 Visual Studio Express](aspnet-mvc-4-fundamentals/_static/image43.png "安裝 Visual Studio Express")

    *安裝 Visual Studio Express*
4. 閱讀所有產品的授權和條款，然後按一下 [**我接受**] 繼續。

    ![接受授權條款](aspnet-mvc-4-fundamentals/_static/image44.png)

    *接受授權條款*
5. 等到下載和安裝程式完成為止。

    ![安裝進度](aspnet-mvc-4-fundamentals/_static/image45.png)

    *安裝進度*
6. 當安裝完成時，按一下 **[完成]** 。

    ![安裝已完成](aspnet-mvc-4-fundamentals/_static/image46.png)

    *安裝已完成*
7. 按一下 **[** 結束] 以關閉 Web Platform Installer。
8. 若要開啟 Web Visual Studio Express，請移至 [**開始**] 畫面，然後開始撰寫 &quot;**VS Express**&quot;，然後按一下 [ **VS Express for Web** ] 磚。

    ![VS Express for Web 磚](aspnet-mvc-4-fundamentals/_static/image47.png)

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

    ![登入 Windows Azure 入口網站](aspnet-mvc-4-fundamentals/_static/image48.png "登入 Windows Azure 入口網站")

    *登入 Windows Azure 管理入口網站*
2. 按一下命令列上的 [**新增**]。

    ![建立新網站](aspnet-mvc-4-fundamentals/_static/image49.png "建立新網站")

    *建立新網站*
3. 按一下 [**計算** | 的**網站**]。 然後選取 [**快速建立**] 選項。 提供新網站的可用 URL，然後按一下 [**建立網站**]。

    > [!NOTE]
    > Windows Azure 網站是在雲端中執行之 Web 應用程式的主機，您可以控制和管理。 [快速建立] 選項可讓您從入口網站外部，將已完成的 web 應用程式部署至 Windows Azure 網站。 它不包含設定資料庫的步驟。

    ![使用 [快速建立] 建立新的網站](aspnet-mvc-4-fundamentals/_static/image50.png "使用 [快速建立] 建立新的網站")

    *使用 [快速建立] 建立新的網站*
4. 等到新**網站**建立完畢。
5. 建立網站之後，請按一下 [ **URL** ] 資料行下方的連結。 檢查新網站是否正常運作。

    ![流覽至新網站](aspnet-mvc-4-fundamentals/_static/image51.png "流覽至新網站")

    *流覽至新網站*

    ![網站正在執行](aspnet-mvc-4-fundamentals/_static/image52.png "網站正在執行")

    *網站正在執行*
6. 返回入口網站，然後按一下 [**名稱**] 欄底下的網站名稱，以顯示管理頁面。

    ![開啟網站管理頁面](aspnet-mvc-4-fundamentals/_static/image53.png "開啟網站管理頁面")

    *開啟網站管理頁面*
7. 在 [**儀表板**] 頁面的 [**快速概覽**] 區段下，按一下 [**下載發行設定檔**] 連結。

    > [!NOTE]
    > *發行設定檔*包含將 web 應用程式發佈至 Windows Azure 網站所需的所有資訊，以供每個已啟用的發行方法使用。 發行設定檔包含 URL、使用者認證和資料庫字串，這些都是用來連接到已啟用發行方法的每個端點並進行驗證的必要資訊。 **Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支援讀取發行設定檔，以將這些程式的設定自動化，以將 Web 應用程式發佈至 Windows Azure 網站。

    ![正在下載網站發行設定檔](aspnet-mvc-4-fundamentals/_static/image54.png "正在下載網站發行設定檔")

    *正在下載網站發行設定檔*
8. 將發行設定檔下載到已知的位置。 在此練習中，您將瞭解如何使用此檔案，將 web 應用程式從 Visual Studio 發行至 Windows Azure 網站。

    ![儲存發行設定檔](aspnet-mvc-4-fundamentals/_static/image55.png "正在儲存發行設定檔")

    *儲存發行設定檔*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>工作 2-設定資料庫伺服器

如果您的應用程式會使用 SQL Server 資料庫，您必須建立 SQL Database 伺服器。 如果您想要部署不使用 SQL Server 的簡單應用程式，您可能會略過這項工作。

1. 您將需要 SQL Database 伺服器來儲存應用程式資料庫。 您可以在 Windows Azure 管理入口網站的  **SQL 資料庫** | **伺服器** | **伺服器的儀表板**上，從您的訂用帳戶中查看 SQL Database 伺服器。 如果您沒有建立伺服器，可以使用命令列上的 [**新增**] 按鈕建立一個。 記下 [**伺服器名稱] 和 [URL]、[系統管理員登入名稱] 和 [密碼**]，因為您將在後續工作中使用它們。 請不要建立資料庫，因為它會在稍後的階段中建立。

    ![SQL Database Server 儀表板](aspnet-mvc-4-fundamentals/_static/image56.png "SQL Database Server 儀表板")

    *SQL Database Server 儀表板*
2. 在下一項工作中，您將會從 Visual Studio 測試資料庫連線，因此您必須在伺服器的**允許 IP 位址**清單中包含本機 IP 位址。 若要這麼做，請按一下 **設定**，從**目前的用戶端 IP 位址**中選取 IP 位址，並將它貼入 [**起始 Ip 位址**] 和 [**結束 ip 位址**] 文字方塊，然後按一下 ![新增-用戶端-IP-位址-確定 按鈕](aspnet-mvc-4-fundamentals/_static/image57.png) 按鈕。

    ![正在新增用戶端 IP 位址](aspnet-mvc-4-fundamentals/_static/image58.png)

    *正在新增用戶端 IP 位址*
3. 將**用戶端 Ip 位址**新增至 [允許的 ip 位址] 清單之後，按一下 [**儲存**] 以確認變更。

    ![確認變更](aspnet-mvc-4-fundamentals/_static/image59.png)

    *確認變更*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>工作 3-使用 Web Deploy 發行 ASP.NET MVC 4 應用程式

1. 返回 ASP.NET MVC 4 解決方案。 在 **方案總管**中，以滑鼠右鍵按一下 網站 專案，然後選取 **發佈**。

    ![發行應用程式](aspnet-mvc-4-fundamentals/_static/image60.png "發行應用程式")

    *發行網站*
2. 匯入您在第一個工作中儲存的發行設定檔。

    ![匯入發行設定檔](aspnet-mvc-4-fundamentals/_static/image61.png "匯入發行設定檔")

    *正在匯入發行設定檔*
3. 按一下 [**驗證連接**]。 驗證完成後，按 **[下一步]** 。

    > [!NOTE]
    > 當您看到 [驗證連線] 按鈕旁出現綠色核取記號時，驗證就會完成。

    ![正在驗證連接](aspnet-mvc-4-fundamentals/_static/image62.png "正在驗證連接")

    *正在驗證連接*
4. 在 [**設定**] 頁面的 [**資料庫**] 區段底下，按一下資料庫連接的文字方塊旁邊的按鈕（也就是**DefaultConnection**）。

    ![Web deploy 設定](aspnet-mvc-4-fundamentals/_static/image63.png "Web deploy 設定")

    *Web deploy 設定*
5. 設定資料庫連接，如下所示：

   - 在 [**伺服器名稱**] 中，使用*tcp：* prefix 輸入您的 SQL Database 伺服器 URL。
   - 在 [**使用者名稱**] 中，輸入您的伺服器管理員登入名稱。
   - 在 [**密碼**] 中輸入您的伺服器管理員登入密碼。
   - 輸入新的資料庫名稱，例如： *MVC4SampleDB*。

     ![正在設定目的地連接字串](aspnet-mvc-4-fundamentals/_static/image64.png "正在設定目的地連接字串")

     *正在設定目的地連接字串*
6. 然後按一下 [確定]。 當系統提示您建立資料庫時，請按一下 **[是]** 。

    ![建立資料庫](aspnet-mvc-4-fundamentals/_static/image65.png "建立資料庫字串")

    *建立資料庫*
7. 您將用來連接到 Windows Azure 中 SQL Database 的連接字串會顯示在 [預設連接] 文字方塊中。 然後按一下 [下一步]。

    ![指向 SQL Database 的連接字串](aspnet-mvc-4-fundamentals/_static/image66.png "指向 SQL Database 的連接字串")

    *指向 SQL Database 的連接字串*
8. 在 [**預覽**] 頁面中，按一下 [**發佈**]。

    ![發行 web 應用程式](aspnet-mvc-4-fundamentals/_static/image67.png "發行 web 應用程式")

    *發行 web 應用程式*
9. 發佈程式完成後，您的預設瀏覽器會開啟已發行的網站。

    ![發行至 Windows Azure 的應用程式](aspnet-mvc-4-fundamentals/_static/image68.png "發行至 Windows Azure 的應用程式")

    *發行至 Windows Azure 的應用程式*

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>附錄 C：使用程式碼片段

有了程式碼片段，您就可以輕鬆地擁有所需的所有程式碼。 實驗室檔會告訴您可以使用它們的確切時機，如下圖所示。

![使用 Visual Studio 程式碼片段將程式碼插入您的專案](aspnet-mvc-4-fundamentals/_static/image69.png "使用 Visual Studio 程式碼片段將程式碼插入您的專案")

*使用 Visual Studio 程式碼片段將程式碼插入您的專案*

***若要使用鍵盤新增程式碼片段（C#僅限）***

1. 將游標放在您想要插入程式碼的位置。
2. 開始鍵入程式碼片段名稱（不含空格或連字號）。
3. 監看 IntelliSense 會顯示相符的程式碼片段名稱。
4. 選取正確的程式碼片段（或繼續輸入，直到選取整個程式碼片段的名稱為止）。
5. 按兩次 Tab 鍵，在游標位置插入程式碼片段。

![開始鍵入程式碼片段名稱](aspnet-mvc-4-fundamentals/_static/image70.png "開始鍵入程式碼片段名稱")

*開始鍵入程式碼片段名稱*

![按 Tab 鍵以選取反白顯示的程式碼片段](aspnet-mvc-4-fundamentals/_static/image71.png "按 Tab 鍵以選取反白顯示的程式碼片段")

*按 Tab 鍵以選取反白顯示的程式碼片段*

![再按一次 Tab 鍵，將會展開程式碼片段](aspnet-mvc-4-fundamentals/_static/image72.png "再按一次 Tab 鍵，將會展開程式碼片段")

*再按一次 Tab 鍵，將會展開程式碼片段*

***若要使用滑鼠C#（、Visual Basic 和 XML）加入程式碼片段***sha-1. 以滑鼠右鍵按一下您要插入程式碼片段的位置。

1. 選取 [**插入程式碼片段**]，後面接著 [ **My Code 程式碼片段**]。
2. 按一下清單中的相關程式碼片段，即可加以選取。

![以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]](aspnet-mvc-4-fundamentals/_static/image73.png "以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]")

*以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]*

![按一下清單中的相關程式碼片段，即可加以選取](aspnet-mvc-4-fundamentals/_static/image74.png "按一下清單中的相關程式碼片段，即可加以選取")

*按一下清單中的相關程式碼片段，即可加以選取*
