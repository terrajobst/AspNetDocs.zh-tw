---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
title: ASP.NET MVC 4 自訂動作篩選 |Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 會提供動作篩選準則，以便在呼叫動作方法之前或之後執行篩選邏輯。 動作篩選器是自訂屬性 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 969ab824-1b98-4552-81fe-b60ef5fc6887
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
msc.type: authoredcontent
ms.openlocfilehash: eaeb32180f79fabf557cbc38ff067eb26b47fea7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579692"
---
# <a name="aspnet-mvc-4-custom-action-filters"></a>ASP.NET MVC 4 自訂動作篩選

依[Web Camp 團隊](https://twitter.com/webcamps)

[下載 Web Camp 訓練套件](https://aka.ms/webcamps-training-kit)

ASP.NET MVC 會提供動作篩選準則，以便在呼叫動作方法之前或之後執行篩選邏輯。 動作篩選器是自訂屬性，可提供宣告式方式，將動作前和動作後的行為新增至控制器的動作方法。

在這個實際操作的實驗室中，您將會在 MvcMusicStore 解決方案中建立自訂動作篩選屬性來攔截控制器的要求，並將網站的活動記錄到資料庫資料表中。 您可以藉由插入任何控制器或動作，將您的記錄篩選器新增至其中。 最後，您會看到記錄檔視圖，顯示訪客清單。

這個實際操作實驗室假設您有**ASP.NET MVC**的基本知識。 如果您之前未使用過**ASP.NET mvc** ，建議您移至**ASP.NET mvc 4 基礎**實際操作實驗室。

> [!NOTE]
> 所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可從[Microsoft web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)取得。 此實驗室的特定專案可在[ASP.NET MVC 4 自訂動作篩選](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters)中取得。

<a id="Objectives"></a>
### <a name="objectives"></a>目標

在此實際操作實驗室中，您將瞭解如何：

- 建立自訂動作篩選準則屬性以擴充篩選功能
- 藉由將自訂篩選屬性插入特定層級來套用
- 全域註冊自訂動作篩選準則

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

1. [練習1：記錄動作](#Exercise1)
2. [練習2：管理多個動作篩選準則](#Exercise2)

完成此實驗室的預估時間： **30 分鐘**。

> [!NOTE]
> 每個練習都會伴隨一個**結束**資料夾，其中包含您在完成練習之後應該取得的結果解決方案。 如果您需要額外的協助來進行練習，您可以使用此解決方案做為指南。

<a id="Exercise1"></a>

<a id="Exercise_1_Logging_Actions"></a>
### <a name="exercise-1-logging-actions"></a>練習1：記錄動作

在此練習中，您將瞭解如何使用 ASP.NET MVC 4 篩選器提供者來建立自訂動作記錄篩選器。 基於這個目的，您會將記錄篩選套用至 MusicStore 網站，以記錄所選控制器中的所有活動。

篩選會擴充**ActionFilterAttributeClass**並覆寫**OnActionExecuting**方法，以攔截每個要求，然後執行記錄動作。 ASP.NET MVC **ActionExecutingCoNtext**類別會提供有關 HTTP 要求、執行方法、結果和參數的內容資訊 **。**

> [!NOTE]
> ASP.NET MVC 4 也有預設的篩選器提供者，您可以使用，而不需要建立自訂篩選器。 ASP.NET MVC 4 提供下列類型的篩選準則：
> 
> - **授權**篩選準則，它會針對是否執行動作方法進行安全性決策，例如執行驗證或驗證要求的屬性。
> - **動作**篩選準則，會包裝動作方法的執行。 此篩選可以執行額外的處理，例如將額外的資料提供給動作方法、檢查傳回值，或取消執行動作方法。
> - **結果**篩選準則，會包裝 ActionResult 物件的執行。 此篩選可以執行其他的結果處理，例如修改 HTTP 回應。
> - **例外**狀況篩選準則，它會在動作方法中的某處擲回未處理的例外狀況時執行，從授權篩選準則開始，並以結果執行結束。 例外狀況篩選條件可以用於記錄或顯示錯誤頁面這類工作。
> 
> 如需篩選器提供者的詳細資訊，請造訪此 MSDN 連結：（[https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)）。

<a id="AboutLoggingFeature"></a>

<a id="About_MVC_Music_Store_Application_logging_feature"></a>
#### <a name="about-mvc-music-store-application-logging-feature"></a>關於 MVC 音樂儲存應用程式記錄功能

此音樂存放區解決方案有一個新的資料模型資料表可供網站記錄**ActionLog**使用，其欄位如下：接收要求的控制器名稱，稱為「動作」、「用戶端 IP」和「時間戳記」。

![資料模型。ActionLog 資料表。](aspnet-mvc-4-custom-action-filters/_static/image1.png "資料模型。ActionLog 資料表。")

*資料模型-ActionLog 資料表*

解決方案會為動作記錄檔提供 ASP.NET 的 MVC 視圖，可在**MvcMusicStores/Views/ActionLog**找到：

![動作記錄檔視圖](aspnet-mvc-4-custom-action-filters/_static/image2.png "動作記錄檔視圖")

*動作記錄檔視圖*

使用此指定的結構，所有工作都將著重于中斷控制器的要求，並使用自訂篩選來執行記錄。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_Custom_Filter_to_Catch_a_Controllers_Request"></a>
#### <a name="task-1---creating-a-custom-filter-to-catch-a-controllers-request"></a>工作 1-建立自訂篩選來攔截控制器的要求

在這項工作中，您將建立自訂篩選屬性類別，其中將包含記錄邏輯。 基於這個目的，您將擴充 ASP.NET MVC **actionfilterattribut**類別，並執行介面**IActionFilter**。

> [!NOTE]
> **Actionfilterattribut**是所有屬性篩選準則的基類。 它提供下列方法，以在執行控制器動作的前後執行特定邏輯：
> 
> - **OnActionExecuting**（ActionExecutingCoNtext filterCoNtext）：在呼叫動作方法之前。
> - **OnActionExecuted**（ActionExecutedCoNtext filterCoNtext）：在呼叫動作方法之後，以及執行結果之前（view render 之前）。
> - **OnResultExecuting**（ResultExecutingCoNtext filterCoNtext）：緊接在執行結果之前（view render 之前）。
> - **OnResultExecuted**（ResultExecutedCoNtext filterCoNtext）：執行結果之後（呈現視圖之後）。
> 
> 藉由將這些方法中的任何一項覆寫成衍生類別，您就可以執行自己的篩選程式代碼。

1. 開啟位於 **\Source\Ex01-LoggingActions\Begin**資料夾的 [**開始**] 解決方案。

   1. 在繼續之前，您必須先下載一些遺漏的 NuGet 套件。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
      > 
      > 如需詳細資訊，請參閱這篇文章： [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。
2. 將新類別C#新增至 [**篩選**] 資料夾，並將其命名為*CustomActionFilter.cs*。 這個資料夾會儲存所有的自訂篩選器。
3. 開啟**CustomActionFilter.cs** ，並加入**system.web**和**MvcMusicStore**命名空間的參考：

    （程式碼片段- *ASP.NET MVC 4 自訂動作篩選-Ex1-CustomActionFilterNamespaces*）

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample1.cs)]
4. 從**actionfilterattribut**繼承**CustomActionFilter**類別，然後將**CustomActionFilter**類別實作為**IActionFilter**介面。

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample2.cs)]
5. 使**CustomActionFilter**類別覆寫方法**OnActionExecuting** ，並新增必要的邏輯以記錄篩選器的執行。 若要這樣做，請在**CustomActionFilter**類別內新增下列反白顯示的程式碼。

    （程式碼片段- *ASP.NET MVC 4 自訂動作篩選-Ex1-LoggingActions*）

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample3.cs#Highlight)]

    > [!NOTE]
    > **OnActionExecuting**方法使用**Entity Framework**新增新的 ActionLog 暫存器。 它會使用來自**filterCoNtext**的內容資訊，建立並填滿新的實體實例。
    > 
    > 您可以在[msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx)閱讀更多關於**ControllerCoNtext**類別的資訊。

<a id="Ex1Task2"></a>

<a id="Task_2_-_Injecting_a_Code_Interceptor_into_the_Store_Controller_Class"></a>
#### <a name="task-2---injecting-a-code-interceptor-into-the-store-controller-class"></a>工作 2-將程式碼攔截器插入存放控制器類別

在這項工作中，您會將自訂篩選器插入所有要記錄的控制器類別和控制器動作。 基於此練習的目的，存放區控制器類別會有一個記錄檔。

從**ActionLogFilterAttribute**自訂篩選準則**OnActionExecuting**的方法會在呼叫插入的元素時執行。

也可以攔截特定的控制器方法。

1. 在**MvcMusicStore\Controllers**開啟**StoreController** ，並將參考新增至**篩選器**命名空間：

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample4.cs)]
2. 藉由在類別宣告之前加入 **[CustomActionFilter]** 屬性，將自訂篩選**CustomActionFilter**插入**StoreController**類別中。

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample5.cs)]

   > [!NOTE]
   > 當篩選器插入控制器類別時，其所有動作也會一併插入。 如果您只想要對一組動作套用篩選，就必須將 **[CustomActionFilter]** 插入其中每個動作：
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample6.cs)]

<a id="Ex1Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>工作 3-正在執行應用程式

在這項工作中，您將測試記錄篩選是否正常運作。 您將會啟動應用程式並造訪存放區，然後您會檢查已記錄的活動。

1. 按 **F5** 執行應用程式。
2. 流覽至 **/ActionLog**以查看記錄檔視圖的初始狀態：

    ![頁面活動前的記錄追蹤程式狀態](aspnet-mvc-4-custom-action-filters/_static/image3.png "頁面活動前的記錄追蹤程式狀態")

    *頁面活動前的記錄追蹤程式狀態*

   > [!NOTE]
   > 根據預設，它一律會顯示在抓取功能表的現有內容類型時所產生的一個專案。
   > 
   > 為了簡單起見，我們會在每次應用程式執行時清除**ActionLog**資料表，因此它只會顯示每個特定工作的驗證記錄。
   > 
   > 您可能需要從會話中移除下列程式碼 **\_Start**方法（在**global.asax**類別中），以便儲存在存放區控制器內執行之所有動作的歷程記錄。
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample7.cs)]
3. 按一下功能表中的其中一個內容，**然後在其中**執行一些動作，例如流覽可用的專輯。
4. 流覽至 **/ActionLog** ，如果記錄檔是空的，請按**F5**重新整理頁面。 檢查是否已追蹤您的造訪：

    ![已記錄活動的動作記錄](aspnet-mvc-4-custom-action-filters/_static/image4.png "已記錄活動的動作記錄")

    *已記錄活動的動作記錄*

<a id="Exercise2"></a>

<a id="Exercise_2_Managing_Multiple_Action_Filters"></a>
### <a name="exercise-2-managing-multiple-action-filters"></a>練習2：管理多個動作篩選準則

在此練習中，您會將第二個自訂動作篩選準則新增至 StoreController 類別，並定義執行這兩個篩選準則的特定順序。 接著，您將更新程式碼以全域註冊篩選。

定義篩選準則的執行順序時，有不同的選項要納入考慮。 例如，Order 屬性和篩選準則的範圍：

您可以定義每個篩選準則的**範圍**，例如，您可以將所有動作篩選準則的範圍設為在**控制器範圍**內執行，並將所有授權篩選準則設為在**全域範圍**中執行。 範圍具有已定義的執行順序。

此外，每個動作篩選準則都有一個 Order 屬性，用來判斷篩選準則範圍中的執行順序。

如需自訂動作篩選執行順序的詳細資訊，請造訪這篇 MSDN 文章：（[https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx)）。

<a id="Ex2Task1"></a>

<a id="Task_1_Creating_a_new_Custom_Action_Filter"></a>
#### <a name="task-1-creating-a-new-custom-action-filter"></a>工作1：建立新的自訂動作篩選準則

在這項工作中，您將建立新的自訂動作篩選器以插入 StoreController 類別，學習如何管理篩選的執行順序。

1. 開啟位於 **\Source\Ex02-ManagingMultipleActionFilters\Begin**資料夾的 [**開始**] 解決方案。 否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。

    1. 如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
    2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
    3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

        > [!NOTE]
        > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
        > 
        > 如需詳細資訊，請參閱這篇文章： [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。
2. 將新類別C#新增至**篩選器**資料夾，並將其命名為*MyNewCustomActionFilter.cs*
3. 開啟**MyNewCustomActionFilter.cs** ，並加入**system.web**和**MvcMusicStore**命名空間的參考：

    （程式碼片段- *ASP.NET MVC 4 自訂動作篩選-Ex2-MyNewCustomActionFilterNamespaces*）

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample8.cs)]
4. 將預設類別宣告取代為下列程式碼。

    （程式碼片段- *ASP.NET MVC 4 自訂動作篩選-Ex2-MyNewCustomActionFilterClass*）

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample9.cs)]

    > [!NOTE]
    > 此自訂動作篩選與您在上一個練習中建立的篩選幾乎相同。 主要差異在於它具有 *&quot;記錄的&quot;* 屬性已使用這個新類別的名稱更新，以識別哪一個篩選註冊了記錄檔。

<a id="Ex2Task2"></a>

<a id="Task_2_Injecting_a_new_Code_Interceptor_into_the_StoreController_Class"></a>
#### <a name="task-2-injecting-a-new-code-interceptor-into-the-storecontroller-class"></a>工作2：將新的程式碼攔截器插入 StoreController 類別

在這項工作中，您會將新的自訂篩選器新增至 StoreController 類別，並執行解決方案來確認兩個篩選準則如何搭配運作。

1. 開啟位於**MvcMusicStore\Controllers**的**StoreController**類別，並將新的自訂篩選**MyNewCustomActionFilter**插入**StoreController**類別，如下列程式碼所示。

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample10.cs)]
2. 現在，請執行應用程式，以查看這兩個自訂動作篩選準則的運作方式。 若要這麼做，請按**F5**並等候應用程式啟動。
3. 流覽至 **/ActionLog**以查看記錄檔視圖的初始狀態。

    ![頁面活動前的記錄追蹤程式狀態](aspnet-mvc-4-custom-action-filters/_static/image5.png "頁面活動前的記錄追蹤程式狀態")

    *頁面活動前的記錄追蹤程式狀態*
4. 按一下功能表中的其中一個內容，**然後在其中**執行一些動作，例如流覽可用的專輯。
5. 請檢查這次。您的造訪已追蹤兩次：一次針對您在**StorageController**類別中新增的每個自訂動作篩選準則。

    ![已記錄活動的動作記錄](aspnet-mvc-4-custom-action-filters/_static/image6.png "已記錄活動的動作記錄")

    *已記錄活動的動作記錄*
6. 關閉瀏覽器。

<a id="Ex2Task3"></a>

<a id="Task_3_Managing_Filter_Ordering"></a>
#### <a name="task-3-managing-filter-ordering"></a>工作3：管理篩選順序

在這項工作中，您將瞭解如何使用 Order 屬性來管理篩選準則的執行順序。

1. 開啟位於**MvcMusicStore\Controllers**的**StoreController**類別，並在這兩個篩選準則中指定**Order**屬性，如下所示。

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample11.cs)]
2. 現在，請根據訂單屬性的值，確認篩選準則的執行方式。 您會發現具有最小順序值（**CustomActionFilter**）的篩選是第一個執行的。 按**F5** ，並等候應用程式啟動。
3. 流覽至 **/ActionLog**以查看記錄檔視圖的初始狀態。

    ![頁面活動前的記錄追蹤程式狀態](aspnet-mvc-4-custom-action-filters/_static/image7.png "頁面活動前的記錄追蹤程式狀態")

    *頁面活動前的記錄追蹤程式狀態*
4. 按一下功能表中的其中一個內容，**然後在其中**執行一些動作，例如流覽可用的專輯。
5. 請檢查這次，您的造訪已依照篩選準則「順序值： **CustomActionFilter**記錄」進行追蹤。

    ![已記錄活動的動作記錄](aspnet-mvc-4-custom-action-filters/_static/image8.png "已記錄活動的動作記錄")

    *已記錄活動的動作記錄*
6. 現在，您將更新篩選準則的順序值，並確認記錄順序的變更方式。 在**StoreController**類別中，更新篩選準則的順序值，如下所示。

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample12.cs)]
7. 按**F5**再次執行應用程式。
8. 按一下功能表中的其中一個內容，**然後在其中**執行一些動作，例如流覽可用的專輯。
9. 檢查這次， **MyNewCustomActionFilter**篩選器所建立的記錄會先出現。

    ![已記錄活動的動作記錄](aspnet-mvc-4-custom-action-filters/_static/image9.png "已記錄活動的動作記錄")

    *已記錄活動的動作記錄*

<a id="Ex2Task4"></a>

<a id="Task_4_Registering_Filters_Globally"></a>
#### <a name="task-4-registering-filters-globally"></a>工作4：全域註冊篩選

在這項工作中，您將更新解決方案，將新的篩選器（**MyNewCustomActionFilter**）註冊為全域篩選器。 如此一來，就會由應用程式中執行的所有動作觸發，而不只是在上一個工作中的 StoreController。

1. 在**StoreController**類別中，從 **[CustomActionFilter]** 移除 **[MyNewCustomActionFilter]** 屬性和 order 屬性。 它應該如下所示：

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample13.cs)]
2. 開啟**global.asax**檔案，並找出**應用程式\_Start**方法。 請注意，應用程式每次啟動時，都會藉由呼叫**filterconfig.math**類別內的**RegisterGlobalFilters**方法，來註冊全域篩選器。

    ![在 global.asax 中註冊全域篩選器](aspnet-mvc-4-custom-action-filters/_static/image10.png "在 global.asax 中註冊全域篩選器")

    *在 global.asax 中註冊全域篩選器*
3. 在**App\_開始** 資料夾中開啟**FilterConfig.cs**檔案。
4. 使用 System.object 新增的參考。使用 MvcMusicStore;命名空間.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample14.cs)]
5. 更新**RegisterGlobalFilters**方法新增您的自訂篩選。 若要這麼做，請新增反白顯示的程式碼：

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample15.cs)]
6. 按 **F5** 鍵執行應用程式。
7. 按一下功能表中的其中一個內容，**然後在其中**執行一些動作，例如流覽可用的專輯。
8. 請檢查 **[MyNewCustomActionFilter]** 現在是否已插入 HomeController 和 ActionLogController。

    ![已記錄活動的動作記錄](aspnet-mvc-4-custom-action-filters/_static/image11.png "已記錄活動的動作記錄")

    *已記錄全域活動的動作記錄*

> [!NOTE]
> 此外，您可以遵循[附錄 B：使用 Web Deploy 發佈 ASP.NET MVC 4 應用程式](#AppendixB)，將此應用程式部署到 Windows Azure 網站。

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>總結

藉由完成此實際操作實驗室，您已瞭解如何擴充動作篩選準則來執行自訂動作。 您也已瞭解如何將任何篩選器插入頁面控制器。 使用的概念如下：

- 如何使用 ASP.NET MVC Actionfilterattribut 類別建立自訂動作篩選準則
- 如何將篩選器插入 ASP.NET MVC 控制器
- 如何使用 Order 屬性管理篩選順序
- 如何全域註冊篩選

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附錄 A：安裝 Web 的 Visual Studio Express 2012

您可以使用 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** 安裝 Web 或另一個 &quot;Express&quot; 版本**的 Microsoft Visual Studio Express 2012** 。 下列指示會引導您完成使用*Microsoft Web Platform Installer*安裝*Visual studio Express 2012 for Web*所需的步驟。

1. 移至 [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)。 或者，如果您已經安裝 Web Platform Installer，您可以開啟它，然後使用 Windows Azure SDK&quot;來搜尋產品 &quot;<em>Visual Studio Express 2012 For Web</em> 。
2. 按一下 [**立即安裝**]。 如果您沒有**Web Platform Installer**系統會將您重新導向，先下載並安裝。
3. 開啟**Web Platform Installer**之後，請按一下 [**安裝**] 以啟動安裝程式。

    ![安裝 Visual Studio Express](aspnet-mvc-4-custom-action-filters/_static/image12.png "安裝 Visual Studio Express")

    *安裝 Visual Studio Express*
4. 閱讀所有產品的授權和條款，然後按一下 [**我接受**] 繼續。

    ![接受授權條款](aspnet-mvc-4-custom-action-filters/_static/image13.png)

    *接受授權條款*
5. 等到下載和安裝程式完成為止。

    ![安裝進度](aspnet-mvc-4-custom-action-filters/_static/image14.png)

    *安裝進度*
6. 當安裝完成時，按一下 **[完成]** 。

    ![安裝已完成](aspnet-mvc-4-custom-action-filters/_static/image15.png)

    *安裝已完成*
7. 按一下 **[** 結束] 以關閉 Web Platform Installer。
8. 若要開啟 Web Visual Studio Express，請移至 [**開始**] 畫面，然後開始撰寫 &quot;**VS Express**&quot;，然後按一下 [ **VS Express for Web** ] 磚。

    ![VS Express for Web 磚](aspnet-mvc-4-custom-action-filters/_static/image16.png)

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

    ![登入 Windows Azure 入口網站](aspnet-mvc-4-custom-action-filters/_static/image17.png "登入 Windows Azure 入口網站")

    *登入 Windows Azure 管理入口網站*
2. 按一下命令列上的 [**新增**]。

    ![建立新網站](aspnet-mvc-4-custom-action-filters/_static/image18.png "建立新網站")

    *建立新網站*
3. 按一下 [**計算** | 的**網站**]。 然後選取 [**快速建立**] 選項。 提供新網站的可用 URL，然後按一下 [**建立網站**]。

    > [!NOTE]
    > Windows Azure 網站是在雲端中執行之 Web 應用程式的主機，您可以控制和管理。 [快速建立] 選項可讓您從入口網站外部，將已完成的 web 應用程式部署至 Windows Azure 網站。 它不包含設定資料庫的步驟。

    ![使用 [快速建立] 建立新的網站](aspnet-mvc-4-custom-action-filters/_static/image19.png "使用 [快速建立] 建立新的網站")

    *使用 [快速建立] 建立新的網站*
4. 等到新**網站**建立完畢。
5. 建立網站之後，請按一下 [ **URL** ] 資料行下方的連結。 檢查新網站是否正常運作。

    ![流覽至新網站](aspnet-mvc-4-custom-action-filters/_static/image20.png "流覽至新網站")

    *流覽至新網站*

    ![網站正在執行](aspnet-mvc-4-custom-action-filters/_static/image21.png "網站正在執行")

    *網站正在執行*
6. 返回入口網站，然後按一下 [**名稱**] 欄底下的網站名稱，以顯示管理頁面。

    ![開啟網站管理頁面](aspnet-mvc-4-custom-action-filters/_static/image22.png "開啟網站管理頁面")

    *開啟網站管理頁面*
7. 在 [**儀表板**] 頁面的 [**快速概覽**] 區段下，按一下 [**下載發行設定檔**] 連結。

    > [!NOTE]
    > *發行設定檔*包含將 web 應用程式發佈至 Windows Azure 網站所需的所有資訊，以供每個已啟用的發行方法使用。 發行設定檔包含 URL、使用者認證和資料庫字串，這些都是用來連接到已啟用發行方法的每個端點並進行驗證的必要資訊。 **Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支援讀取發行設定檔，以將這些程式的設定自動化，以將 Web 應用程式發佈至 Windows Azure 網站。

    ![正在下載網站發行設定檔](aspnet-mvc-4-custom-action-filters/_static/image23.png "正在下載網站發行設定檔")

    *正在下載網站發行設定檔*
8. 將發行設定檔下載到已知的位置。 在此練習中，您將瞭解如何使用此檔案，將 web 應用程式從 Visual Studio 發行至 Windows Azure 網站。

    ![儲存發行設定檔](aspnet-mvc-4-custom-action-filters/_static/image24.png "正在儲存發行設定檔")

    *儲存發行設定檔*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>工作 2-設定資料庫伺服器

如果您的應用程式會使用 SQL Server 資料庫，您必須建立 SQL Database 伺服器。 如果您想要部署不使用 SQL Server 的簡單應用程式，您可能會略過這項工作。

1. 您將需要 SQL Database 伺服器來儲存應用程式資料庫。 您可以在 Windows Azure 管理入口網站的  **SQL 資料庫** | **伺服器** | **伺服器的儀表板**上，從您的訂用帳戶中查看 SQL Database 伺服器。 如果您沒有建立伺服器，可以使用命令列上的 [**新增**] 按鈕建立一個。 記下 [**伺服器名稱] 和 [URL]、[系統管理員登入名稱] 和 [密碼**]，因為您將在後續工作中使用它們。 請不要建立資料庫，因為它會在稍後的階段中建立。

    ![SQL Database Server 儀表板](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL Database Server 儀表板")

    *SQL Database Server 儀表板*
2. 在下一項工作中，您將會從 Visual Studio 測試資料庫連線，因此您必須在伺服器的**允許 IP 位址**清單中包含本機 IP 位址。 若要這麼做，請按一下 **設定**，從**目前的用戶端 IP 位址**中選取 IP 位址，並將它貼入 [**起始 Ip 位址**] 和 [**結束 ip 位址**] 文字方塊，然後按一下 ![新增-用戶端-IP-位址-確定 按鈕](aspnet-mvc-4-custom-action-filters/_static/image26.png) 按鈕。

    ![正在新增用戶端 IP 位址](aspnet-mvc-4-custom-action-filters/_static/image27.png)

    *正在新增用戶端 IP 位址*
3. 將**用戶端 Ip 位址**新增至 [允許的 ip 位址] 清單之後，按一下 [**儲存**] 以確認變更。

    ![確認變更](aspnet-mvc-4-custom-action-filters/_static/image28.png)

    *確認變更*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>工作 3-使用 Web Deploy 發行 ASP.NET MVC 4 應用程式

1. 返回 ASP.NET MVC 4 解決方案。 在 **方案總管**中，以滑鼠右鍵按一下 網站 專案，然後選取 **發佈**。

    ![發行應用程式](aspnet-mvc-4-custom-action-filters/_static/image29.png "發行應用程式")

    *發行網站*
2. 匯入您在第一個工作中儲存的發行設定檔。

    ![匯入發行設定檔](aspnet-mvc-4-custom-action-filters/_static/image30.png "匯入發行設定檔")

    *正在匯入發行設定檔*
3. 按一下 [**驗證連接**]。 驗證完成後，按 **[下一步]** 。

    > [!NOTE]
    > 當您看到 [驗證連線] 按鈕旁出現綠色核取記號時，驗證就會完成。

    ![正在驗證連接](aspnet-mvc-4-custom-action-filters/_static/image31.png "正在驗證連接")

    *正在驗證連接*
4. 在 [**設定**] 頁面的 [**資料庫**] 區段底下，按一下資料庫連接的文字方塊旁邊的按鈕（也就是**DefaultConnection**）。

    ![Web deploy 設定](aspnet-mvc-4-custom-action-filters/_static/image32.png "Web deploy 設定")

    *Web deploy 設定*
5. 設定資料庫連接，如下所示：

   - 在 [**伺服器名稱**] 中，使用*tcp：* prefix 輸入您的 SQL Database 伺服器 URL。
   - 在 [**使用者名稱**] 中，輸入您的伺服器管理員登入名稱。
   - 在 [**密碼**] 中輸入您的伺服器管理員登入密碼。
   - 輸入新的資料庫名稱。

     ![正在設定目的地連接字串](aspnet-mvc-4-custom-action-filters/_static/image33.png "正在設定目的地連接字串")

     *正在設定目的地連接字串*
6. 然後按一下 [確定]。 當系統提示您建立資料庫時，請按一下 **[是]** 。

    ![建立資料庫](aspnet-mvc-4-custom-action-filters/_static/image34.png "建立資料庫字串")

    *建立資料庫*
7. 您將用來連接到 Windows Azure 中 SQL Database 的連接字串會顯示在 [預設連接] 文字方塊中。 然後按一下 [下一步]。

    ![指向 SQL Database 的連接字串](aspnet-mvc-4-custom-action-filters/_static/image35.png "指向 SQL Database 的連接字串")

    *指向 SQL Database 的連接字串*
8. 在 [**預覽**] 頁面中，按一下 [**發佈**]。

    ![發行 web 應用程式](aspnet-mvc-4-custom-action-filters/_static/image36.png "發行 web 應用程式")

    *發行 web 應用程式*
9. 發佈程式完成後，您的預設瀏覽器會開啟已發行的網站。

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>附錄 C：使用程式碼片段

有了程式碼片段，您就可以輕鬆地擁有所需的所有程式碼。 實驗室檔會告訴您可以使用它們的確切時機，如下圖所示。

![使用 Visual Studio 程式碼片段將程式碼插入您的專案](aspnet-mvc-4-custom-action-filters/_static/image37.png "使用 Visual Studio 程式碼片段將程式碼插入您的專案")

*使用 Visual Studio 程式碼片段將程式碼插入您的專案*

***若要使用鍵盤新增程式碼片段（C#僅限）***

1. 將游標放在您想要插入程式碼的位置。
2. 開始鍵入程式碼片段名稱（不含空格或連字號）。
3. 監看 IntelliSense 會顯示相符的程式碼片段名稱。
4. 選取正確的程式碼片段（或繼續輸入，直到選取整個程式碼片段的名稱為止）。
5. 按兩次 Tab 鍵，在游標位置插入程式碼片段。

![開始鍵入程式碼片段名稱](aspnet-mvc-4-custom-action-filters/_static/image38.png "開始鍵入程式碼片段名稱")

*開始鍵入程式碼片段名稱*

![按 Tab 鍵以選取反白顯示的程式碼片段](aspnet-mvc-4-custom-action-filters/_static/image39.png "按 Tab 鍵以選取反白顯示的程式碼片段")

*按 Tab 鍵以選取反白顯示的程式碼片段*

![再按一次 Tab 鍵，將會展開程式碼片段](aspnet-mvc-4-custom-action-filters/_static/image40.png "再按一次 Tab 鍵，將會展開程式碼片段")

*再按一次 Tab 鍵，將會展開程式碼片段*

***若要使用滑鼠C#（、Visual Basic 和 XML）加入程式碼片段***sha-1. 以滑鼠右鍵按一下您要插入程式碼片段的位置。

1. 選取 [**插入程式碼片段**]，後面接著 [ **My Code 程式碼片段**]。
2. 按一下清單中的相關程式碼片段，即可加以選取。

![以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]](aspnet-mvc-4-custom-action-filters/_static/image41.png "以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]")

*以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]*

![按一下清單中的相關程式碼片段，即可加以選取](aspnet-mvc-4-custom-action-filters/_static/image42.png "按一下清單中的相關程式碼片段，即可加以選取")

*按一下清單中的相關程式碼片段，即可加以選取*
