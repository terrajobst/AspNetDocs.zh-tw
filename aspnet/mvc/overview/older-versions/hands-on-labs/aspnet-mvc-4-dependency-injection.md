---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
title: ASP.NET MVC 4 相依性插入 |Microsoft Docs
author: rick-anderson
description: 注意：此實際操作實驗室假設您有 ASP.NET MVC 和 ASP.NET MVC 4 篩選器的基本知識。 如果您之前未使用過 ASP.NET MVC 4 篩選，我們會將 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 84c7baca-1c54-4c44-8f52-4282122d6acb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 15c9d4dcb9e2c6b9f6adf54d65d15737b32cca3b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78560610"
---
# <a name="aspnet-mvc-4-dependency-injection"></a>ASP.NET MVC 4 相依性插入

依[Web Camp 團隊](https://twitter.com/webcamps)

[下載 Web Camp 訓練套件](https://aka.ms/webcamps-training-kit)

這個實際操作實驗室假設您有**ASP.NET mvc**和**ASP.NET mvc 4 篩選器**的基本知識。 如果您之前未使用過**ASP.NET mvc 4 篩選**，建議您前往**ASP.NET Mvc 自訂動作篩選實際操作**實驗室。

> [!NOTE]
> 所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可從[Microsoft web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)取得。 此實驗室的特定專案可在[ASP.NET MVC 4](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection)相依性插入中取得。

在面向**物件程式設計**架構中，物件會在有參與者和取用者的共同作業模型中一起工作。 自然地，此通訊模型會產生物件和元件之間的相依性，因而在複雜度增加時變得很容易管理。

![類別相依性和模型複雜度](aspnet-mvc-4-dependency-injection/_static/image1.png "類別相依性和模型複雜度")

*類別相依性和模型複雜度*

您可能已經聽說過**Factory 模式**，以及介面與使用服務之間的分離，其中用戶端物件通常負責服務位置。

相依性插入模式是控制反轉的特定執行。 **控制反轉（IoC）** 表示物件不會建立其他物件來執行其工作。 相反地，它們會從外部來源取得所需的物件（例如，xml 設定檔案）。

相依性**插入（DI）** 表示這是在沒有物件介入的情況下完成，通常是由傳遞了函式參數和設定屬性的架構元件所組成。

<a id="The_Dependency_Injection_DI_Design_Pattern"></a>
### <a name="the-dependency-injection-di-design-pattern"></a>相依性插入（DI）設計模式

概括而言，相依性插入的目標是用戶端類別（例如*高爾夫的*物件）需要滿足介面的專案（例如*IClub*）。 它並不在意具體的類型（例如*WoodClub、IronClub、WedgeClub*或*PutterClub*），而是要讓其他人處理該型別（例如，不錯的*caddy*）。 ASP.NET MVC 中的相依性解析程式可讓您在其他地方註冊相依性邏輯（例如容器或*俱樂部袋*）。

![相依性插入圖表](aspnet-mvc-4-dependency-injection/_static/image2.png "相依性插入圖")

*相依性插入-高爾夫球比喻*

使用相依性插入模式和反轉控制的優點如下：

- 減少類別結合
- 增加重複使用的程式碼
- 改善程式碼維護性
- 改善應用程式測試

> [!NOTE]
> 相依性插入有時會與抽象 Factory 設計模式進行比較，但這兩種方法之間有些許差異。 DI 具有一個可在後方運作的架構，藉由呼叫 factory 和已註冊的服務來解決相依性。

既然您已瞭解相依性插入模式，您將會在整個實驗室中學習如何在 ASP.NET MVC 4 中加以套用。 您將開始在**控制器**中使用相依性插入，以包含資料庫存取服務。 接下來，您會將相依性插入套用至**Views** ，以取用服務並顯示資訊。 最後，您將擴充 DI 以 ASP.NET MVC 4 篩選，並在方案中插入自訂動作篩選器。

在此實際操作實驗室中，您將瞭解如何：

- 使用 NuGet 套件整合 ASP.NET MVC 4 與 Unity 以進行相依性插入
- 在 ASP.NET MVC 控制器內使用相依性插入
- 在 ASP.NET MVC 視圖內使用相依性插入
- 在 ASP.NET MVC 動作篩選器內使用相依性插入

> [!NOTE]
> 此實驗室會使用 Mvc3 NuGet 套件來進行相依性解析，但是您可以調整任何相依性插入架構，以與 ASP.NET MVC 4 搭配使用。

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

這個實際操作實驗室是由下列練習所組成：

1. [練習1：插入控制器](#Exercise1)
2. [練習2：插入視圖](#Exercise2)
3. [練習3：插入篩選](#Exercise3)

> [!NOTE]
> 每個練習都會伴隨一個**結束**資料夾，其中包含您在完成練習之後應該取得的結果解決方案。 如果您需要額外的協助來進行練習，您可以使用此解決方案做為指南。

完成此實驗室的預估時間： **30 分鐘**。

<a id="Exercise1"></a>

<a id="Exercise_1_Injecting_a_Controller"></a>
### <a name="exercise-1-injecting-a-controller"></a>練習1：插入控制器

在此練習中，您將瞭解如何藉由使用 NuGet 套件整合 Unity，在 ASP.NET MVC 控制器中使用相依性插入。 基於這個理由，您將會在 MvcMusicStore 控制器中包含服務，以將邏輯與資料存取區隔開。 服務會在控制器的函式中建立新的相依性，這會在**Unity**的協助下使用相依性插入來加以解析。

這種方法會示範如何產生較少的結合應用程式，更有彈性且更容易維護和測試。 您也將瞭解如何整合 ASP.NET MVC 與 Unity。

<a id="About_StoreManager_Service"></a>
#### <a name="about-storemanager-service"></a>關於 StoreManager 服務

「開始」解決方案中提供的「MVC 音樂」存放區現在包含一項服務，可管理名為**StoreService**的存放區控制器資料。 您會在下方找到 Store 服務的執行。 請注意，所有方法都會傳回模型實體。

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample1.cs)]

從開始解決方案**StoreController**現在會使用**StoreService**。 所有的資料參考已從**StoreController**移除，現在可以修改目前的資料存取提供者，而不需要變更任何使用**StoreService**的方法。

您會發現， **StoreController**實與類別的函式內的**StoreService**有相依性。

> [!NOTE]
> 本練習中引進的相依性與**控制反轉**（IoC）有關。
> 
> **StoreController**類別的函式會接收**IStoreService**型別參數，這對於從類別內執行服務呼叫而言是不可或缺的。 不過， **StoreController**不會執行任何控制器必須擁有才能使用 ASP.NET MVC 的預設函式（不含任何參數）。
> 
> 若要解決相依性，控制器必須由抽象 factory 建立（傳回指定類型之任何物件的類別）。

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample2.cs)]

> [!NOTE]
> 當類別嘗試建立 StoreController 而不傳送服務物件時，您會收到錯誤，因為沒有宣告無參數的函式。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Running_the_Application"></a>
#### <a name="task-1---running-the-application"></a>工作 1-正在執行應用程式

在這項工作中，您將執行「開始」應用程式，其中會將服務包含在存放區控制器中，以分隔資料存取與應用程式邏輯。

執行應用程式時，您會收到例外狀況，因為控制器服務預設不會當做參數傳遞：

1. 開啟位於**Source\Ex01-Injecting Controller\Begin**的 [**開始**] 解決方案。

   1. 在繼續之前，您必須先下載一些遺漏的 NuGet 套件。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
2. 按**Ctrl + F5**執行應用程式，而不進行偵測。 您將會收到錯誤訊息，&quot;**未針對此物件定義任何無參數的**函式&quot;：

    ![執行 ASP.NET MVC 開始應用程式時發生錯誤](aspnet-mvc-4-dependency-injection/_static/image3.png "執行 ASP.NET MVC 開始應用程式時發生錯誤")

    *執行 ASP.NET MVC 開始應用程式時發生錯誤*
3. 關閉瀏覽器。

在下列步驟中，您將使用「音樂存放」解決方案來插入此控制器所需的相依性。

<a id="Ex1Task2"></a>

<a id="Task_2_-_Including_Unity_into_MvcMusicStore_Solution"></a>
#### <a name="task-2---including-unity-into-mvcmusicstore-solution"></a>工作 2-將 Unity 包含在 MvcMusicStore 方案中

在這項工作中，您將會在解決方案中包含**Mvc3** NuGet 套件。

> [!NOTE]
> Mvc3 封裝是針對 ASP.NET MVC 3 而設計，但它與 ASP.NET MVC 4 完全相容。
> 
> Unity 是輕量、可擴充的相依性插入容器，具有實例和類型攔截的選擇性支援。 這是一般用途的容器，可用於任何類型的 .NET 應用程式。 它提供了相依性插入機制中的所有常見功能，包括：建立物件、在執行時間指定相依性，以及藉由將元件設定延後至容器，以藉由指定相依性來抽象化需求。

1. 在**MvcMusicStore**專案中安裝**Mvc3** NuGet 套件。 若要這樣做，**請從** **其他視窗** | 開啟 [**套件管理員主控台**]。
2. 執行下列命令。

    PMC

    [!code-powershell[Main](aspnet-mvc-4-dependency-injection/samples/sample3.ps1)]

    ![安裝 Unity. Mvc3 NuGet 套件](aspnet-mvc-4-dependency-injection/_static/image4.png "安裝 Unity. Mvc3 NuGet 套件")

    *安裝 Unity. Mvc3 NuGet 套件*
3. 安裝**Mvc3**套件之後，請探索它自動新增的檔案和資料夾，以簡化 Unity 設定。

    ![已安裝 Unity. Mvc3 封裝](aspnet-mvc-4-dependency-injection/_static/image5.png "已安裝 Unity. Mvc3 封裝")

    *已安裝 Unity. Mvc3 封裝*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Registering_Unity_in_Globalasaxcs_Application_Start"></a>
#### <a name="task-3---registering-unity-in-globalasaxcs-application_start"></a>工作 3-在 Global.asax.cs 應用程式中註冊 Unity\_啟動

在這項工作中，您將更新位於**Global.asax.cs**中的**應用程式\_Start**方法來呼叫 Unity 啟動載入器初始化運算式，然後更新啟動載入器檔案，以註冊要用於相依性插入的服務和控制器。

1. 現在，您將連結啟動載入器，這是初始化 Unity 容器和相依性解析程式的檔案。 若要這樣做，請開啟**Global.asax.cs** ，並在應用程式中新增下列反白顯示的**程式碼\_Start**方法。

    （程式碼片段- *ASP.NET 相依性插入實驗室-Ex01-初始化 Unity*）

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample4.cs)]
2. 開啟**Bootstrapper.cs**檔案。
3. 包含下列命名空間： **MvcMusicStore. Services**和**MusicStore**。

    （程式碼片段- *ASP.NET 相依性插入實驗室-Ex01-新增命名空間的啟動載入*器）

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample5.cs)]
4. 將**BuildUnityContainer**方法的內容取代為下列程式碼，以註冊存放區控制器和存放服務。

    （程式碼片段- *ASP.NET 相依性插入實驗室-Ex01-註冊存放區控制器和服務*）

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample6.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>工作 4-正在執行應用程式

在這項工作中，您將執行應用程式，以確認它現在可以在包含 Unity 之後載入。

1. 按**F5**執行應用程式，應用程式現在應該會載入，而不會顯示任何錯誤訊息。

    ![使用相依性插入執行應用程式](aspnet-mvc-4-dependency-injection/_static/image6.png "使用相依性插入執行應用程式")

    *使用相依性插入執行應用程式*
2. 流覽至 **/Store**。 這會叫用**StoreController**，現在是使用**Unity**建立的。

    ![MVC 音樂存放區](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC 音樂存放區")

    *MVC 音樂存放區*
3. 關閉瀏覽器。

在下列練習中，您將瞭解如何擴充相依性插入範圍，以在 ASP.NET MVC Views 和 Action 篩選器內使用。

<a id="Exercise2"></a>

<a id="Exercise_2_Injecting_a_View"></a>
### <a name="exercise-2-injecting-a-view"></a>練習2：插入視圖

在此練習中，您將瞭解如何在視圖中使用相依性插入，以及 ASP.NET MVC 4 for Unity 整合的新功能。 若要這麼做，您將會在 Store 流覽視圖中呼叫自訂服務，這會在下方顯示訊息和影像。

然後，您會將專案與 Unity 整合，並建立自訂相依性解析程式來插入相依性。

<a id="Ex2Task1"></a>

<a id="Task_1_-_Creating_a_View_that_Consumes_a_Service"></a>
#### <a name="task-1---creating-a-view-that-consumes-a-service"></a>工作 1-建立使用服務的視圖

在這項工作中，您將建立一個可執行服務呼叫的視圖，以產生新的相依性。 此服務包含在此解決方案所包含的簡單訊息服務中。

1. 開啟位於**Source\Ex02-Injecting View\Begin**資料夾中的 [**開始**] 解決方案。 否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。

   1. 如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
      > 
      > 如需詳細資訊，請參閱這篇文章： [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。
2. 包含**MessageService.cs**和**IMessageService.cs**類別，其位於 **/Services**的**來源 \Assets**資料夾中。 若要這樣做，請以滑鼠右鍵按一下 [**服務**] 資料夾，然後選取 [**加入現有專案**]。 流覽至檔案的位置，並將其包含在內。

    ![新增訊息服務和服務介面](aspnet-mvc-4-dependency-injection/_static/image8.png "新增訊息服務和服務介面")

    *新增訊息服務和服務介面*

    > [!NOTE]
    > **IMessageService**介面會定義**MessageService**類別所實作為的兩個屬性。 這些屬性-**message**和**ImageUrl**-儲存訊息，以及要顯示之影像的 URL。
3. 在專案的根資料夾中建立 **/Pages**資料夾，然後從**Source\Assets**新增現有的類別**MyBasePage.cs** 。 您會繼承自的基礎頁面具有下列結構。

    ![Pages 資料夾](aspnet-mvc-4-dependency-injection/_static/image9.png "Pages 資料夾")

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample7.cs)]
4. 從 **/Views/Store**資料夾開啟 **[流覽]** ，並使其繼承自**MyBasePage.cs**。

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample8.cshtml)]
5. 在**流覽**視圖中，新增對**MessageService**的呼叫，以顯示由服務所抓取的影像和訊息。
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample9.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Including_a_Custom_Dependency_Resolver_and_a_Custom_View_Page_Activator"></a>
#### <a name="task-2---including-a-custom-dependency-resolver-and-a-custom-view-page-activator"></a>工作 2-包括自訂相依性解析程式和自訂視圖頁啟動項

在上一項工作中，您已在視圖內插入新的相依性，以在其中執行服務呼叫。 現在，您將藉由執行 ASP.NET MVC 相依性插入介面**IViewPageActivator**和**IDependencyResolver**來解決該相依性。 您將會在解決方案中包含**IDependencyResolver**的執行，以使用 Unity 處理服務的抓取。 然後，您將會包含**IViewPageActivator**介面的另一個自訂執行，以解決視圖的建立。

> [!NOTE]
> 由於 ASP.NET MVC 3 的關係，相依性插入的執行已經簡化了註冊服務的介面。 **IDependencyResolver**和**IViewPageActivator**是用於相依性插入的 ASP.NET MVC 3 功能的一部分。
> 
> **-IDependencyResolver**介面會取代先前的 IMvcServiceLocator。 IDependencyResolver 的實施者必須傳回服務或服務集合的實例。
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample10.cs)]
> 
> **-IViewPageActivator**介面可讓您更精細地控制透過相依性插入來具現化視圖頁面的方式。 執行**IViewPageActivator**介面的類別可以使用內容資訊來建立 view 實例。
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample11.cs)]

1. 在專案的**根資料夾中建立/factory**資料夾。
2. 將**CustomViewPageActivator.cs**加入您的方案，從 **/Sources/Assets/** 到**factory 資料夾。** 若要這麼做，請以滑鼠右鍵按一下  **/Factories**  資料夾，然後選取 **新增 |現有專案**，然後選取  **CustomViewPageActivator.cs**。 這個類別會實**IViewPageActivator**介面來保存 Unity 容器。

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample12.cs)]

    > [!NOTE]
    > **CustomViewPageActivator**會負責管理使用 Unity 容器來建立視圖的方式。
3. 將**UnityDependencyResolver.cs**檔案從 **/Sources/Assets**納入 **/Factories**資料夾。 若要這麼做，請以滑鼠右鍵按一下  **/Factories**  資料夾，然後選取 **新增 |現有專案**，然後選取  **UnityDependencyResolver.cs**檔案。

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample13.cs)]

    > [!NOTE]
    > **UnityDependencyResolver**類別是 Unity 的自訂 DependencyResolver。 在 Unity 容器內找不到服務時，會 invocated 基底解析程式。

在下列工作中，這兩個執行將會註冊，讓模型知道服務的位置和 views。

<a id="Ex2Task3"></a>

<a id="Task_3_-_Registering_for_Dependency_Injection_within_Unity_container"></a>
#### <a name="task-3---registering-for-dependency-injection-within-unity-container"></a>工作 3-註冊 Unity 容器內的相依性插入

在這項工作中，您會將所有先前的專案放在一起，以進行相依性插入作業。

目前，您的解決方案具有下列元素：

- 繼承自**MyBaseClass**並使用**MessageService**的**流覽**視圖。
- 中繼類別**MyBaseClass**，其已針對服務介面宣告相依性插入。
- 服務**MessageService**及其介面**IMessageService**。
- 適用于 Unity- **UnityDependencyResolver**的自訂相依性解析程式，負責處理服務的抓取。
- View Page activator- **CustomViewPageActivator** -建立頁面。

若要插入**流覽**視圖，您現在會在 Unity 容器中註冊自訂相依性解析程式。

1. 開啟**Bootstrapper.cs**檔案。
2. 向 Unity 容器註冊**MessageService**的實例，以初始化服務：

    （程式碼片段- *ASP.NET 相依性插入實驗室-Ex02-註冊訊息服務*）

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample14.cs)]
3. 加入**MvcMusicStore**的參考。

    （程式碼片段- *ASP.NET 相依性插入實驗室-Ex02-Factory 命名空間*）

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample15.cs)]
4. 將**CustomViewPageActivator**註冊為 Unity 容器中的 View Page activator：

    （程式碼片段- *ASP.NET 相依性插入實驗室-Ex02-註冊 CustomViewPageActivator*）

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample16.cs)]
5. 以**UnityDependencyResolver**的實例取代 ASP.NET MVC 4 預設相依性解析程式。 若要這麼做，請將**Initialize**方法內容取代為下列程式碼：

    （程式碼片段- *ASP.NET 相依性插入實驗室-Ex02-更新相依性解析程式*）

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample17.cs)]

    > [!NOTE]
    > ASP.NET MVC 提供預設的相依性解析程式類別。 若要使用自訂相依性解析程式做為我們針對 unity 所建立的解決器，必須更換此解決器。

<a id="Ex2Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>工作 4-正在執行應用程式

在這項工作中，您將執行應用程式，以確認存放區瀏覽器會取用服務，並顯示影像和抓取的訊息：

1. 按 **F5** 執行應用程式。
2. 按一下 [內容] 功能表中的 [**搖滾**]，並查看**MessageService**如何插入至視圖中，以及如何載入歡迎訊息和影像。 在此範例中，我們輸入 &quot;**搖滾**&quot;：

    ![MVC 音樂存放區-視圖插入](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC 音樂存放區-視圖插入")

    *MVC 音樂存放區-視圖插入*
3. 關閉瀏覽器。

<a id="Exercise3"></a>

<a id="Exercise_3_Injecting_Action_Filters"></a>
### <a name="exercise-3-injecting-action-filters"></a>練習3：插入動作篩選準則

在先前的實際操作實驗室**自訂動作篩選**條件中，您已使用篩選自訂和插入。 在此練習中，您將瞭解如何使用 Unity 容器，插入具有相依性插入的篩選器。 若要這麼做，您要將追蹤網站活動的自訂動作篩選器新增至 [音樂存放區] 解決方案。

<a id="Ex3Task1"></a>

<a id="Task_1_-_Including_the_Tracking_Filter_in_the_Solution"></a>
#### <a name="task-1---including-the-tracking-filter-in-the-solution"></a>工作 1-在解決方案中包含追蹤篩選

在這項工作中，您會在 [音樂] 存放區中包含追蹤事件的自訂動作篩選準則。 由於自訂動作篩選器概念已在先前的實驗室中處理 &quot;自訂動作篩選&quot;，您只需要在此實驗室的 [資產] 資料夾中包含篩選準則類別，然後建立 Unity 的篩選器提供者：

1. 開啟位於 [ **Source\Ex03-插入動作 Filter\Begin** ] 資料夾中的 [**開始**] 解決方案。 否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。

   1. 如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
      > 
      > 如需詳細資訊，請參閱這篇文章： [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。
2. 將**TraceActionFilter.cs**檔案從 **/Sources/Assets**納入 **/Filters**資料夾。

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample18.cs)]

    > [!NOTE]
    > 此自訂動作篩選準則會執行 ASP.NET 追蹤。 您可以查看 &quot;ASP.NET MVC 4 本機和動態動作篩選&quot; 實驗室以取得更多參考。
3. 將空的類別**FilterProvider.cs**新增至資料夾 **/Filters.** 中的專案
4. 在**FilterProvider.cs**中新增**system.web**和**Unity**命名空間。

    （程式碼片段- *ASP.NET 相依性插入實驗室-Ex03-篩選提供者加入命名空間*）

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample19.cs)]
5. 讓類別繼承自**IFilterProvider**介面。

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample20.cs)]
6. 在**FilterProvider**類別中新增**IUnityContainer**屬性，然後建立類別的函式來指派容器。

    （程式碼片段- *ASP.NET 相依性插入實驗室-Ex03-篩選提供者*函式）

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample21.cs)]

    > [!NOTE]
    > 篩選器提供者類別的函式不會在內建立**新**的物件。 容器會當做參數來傳遞，而相依性則由 Unity 解決。
7. 在**FilterProvider**類別中，執行從**IFilterProvider**介面**GetFilters**的方法。

    （程式碼片段- *ASP.NET 相依性插入實驗室-Ex03-篩選提供者 GetFilters*）

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample22.cs)]

<a id="Ex3Task2"></a>

<a id="Task_2_-_Registering_and_Enabling_the_Filter"></a>
#### <a name="task-2---registering-and-enabling-the-filter"></a>工作 2-註冊並啟用篩選準則

在這項工作中，您將會啟用網站追蹤。 若要這麼做，您會在**Bootstrapper.cs BuildUnityContainer**方法中註冊篩選準則，以開始追蹤：

1. 開啟位於專案根目錄中的**web.config** ，並在 system.web 群組啟用追蹤追蹤。

    [!code-xml[Main](aspnet-mvc-4-dependency-injection/samples/sample23.xml)]
2. 在專案根目錄中開啟**Bootstrapper.cs** 。
3. 加入**MvcMusicStore**命名空間的參考。

    （程式碼片段- *ASP.NET 相依性插入實驗室-Ex03-新增命名空間的啟動載入*器）

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample24.cs)]
4. 選取**BuildUnityContainer**方法，並在 Unity 容器中註冊篩選。 您必須註冊篩選準則提供者以及動作篩選準則。

    （程式碼片段- *ASP.NET 相依性插入實驗室-Ex03-註冊 FilterProvider 和 ActionFilter*）

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample25.cs)]

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>工作 3-正在執行應用程式

在這項工作中，您將執行應用程式，並測試自訂動作篩選器是否正在追蹤活動：

1. 按 **F5** 執行應用程式。
2. 按一下 [內容] 功能表中的 [**搖滾**]。 如果您想要的話，可以流覽至更多內容。

    ![Music 市集](aspnet-mvc-4-dependency-injection/_static/image11.png "Music 市集")

    *Music 市集*
3. 流覽至 **/Trace.axd**以查看 [應用程式追蹤] 頁面，然後按一下 [**查看詳細資料**]。

    ![應用程式追蹤記錄檔](aspnet-mvc-4-dependency-injection/_static/image12.png "應用程式追蹤記錄檔")

    *應用程式追蹤記錄檔*

    ![應用程式追蹤-要求詳細資料](aspnet-mvc-4-dependency-injection/_static/image13.png "應用程式追蹤-要求詳細資料")

    *應用程式追蹤-要求詳細資料*
4. 關閉瀏覽器。

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>總結

藉由完成此實際操作實驗室，您已瞭解如何使用 NuGet 套件整合 Unity，在 ASP.NET MVC 4 中使用相依性插入。 為了達到此目的，您已在控制器、視圖和動作篩選內使用相依性插入。

涵蓋下列概念：

- ASP.NET MVC 4 相依性插入功能
- 使用 Unity 進行 unity 整合 Mvc3 NuGet 套件
- 控制器中的相依性插入
- 在 Views 中插入相依性
- 動作篩選準則的相依性插入

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附錄 A：安裝 Web 的 Visual Studio Express 2012

您可以使用 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** 安裝 Web 或另一個 &quot;Express&quot; 版本**的 Microsoft Visual Studio Express 2012** 。 下列指示會引導您完成使用*Microsoft Web Platform Installer*安裝*Visual studio Express 2012 for Web*所需的步驟。

1. 移至 [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)。 或者，如果您已經安裝 Web Platform Installer，您可以開啟它，然後使用 Windows Azure SDK&quot;來搜尋產品 &quot;<em>Visual Studio Express 2012 For Web</em> 。
2. 按一下 [**立即安裝**]。 如果您沒有**Web Platform Installer**系統會將您重新導向，先下載並安裝。
3. 開啟**Web Platform Installer**之後，請按一下 [**安裝**] 以啟動安裝程式。

    ![安裝 Visual Studio Express](aspnet-mvc-4-dependency-injection/_static/image14.png "安裝 Visual Studio Express")

    *安裝 Visual Studio Express*
4. 閱讀所有產品的授權和條款，然後按一下 [**我接受**] 繼續。

    ![接受授權條款](aspnet-mvc-4-dependency-injection/_static/image15.png)

    *接受授權條款*
5. 等到下載和安裝程式完成為止。

    ![安裝進度](aspnet-mvc-4-dependency-injection/_static/image16.png)

    *安裝進度*
6. 當安裝完成時，按一下 **[完成]** 。

    ![安裝已完成](aspnet-mvc-4-dependency-injection/_static/image17.png)

    *安裝已完成*
7. 按一下 **[** 結束] 以關閉 Web Platform Installer。
8. 若要開啟 Web Visual Studio Express，請移至 [**開始**] 畫面，然後開始撰寫 &quot;**VS Express**&quot;，然後按一下 [ **VS Express for Web** ] 磚。

    ![VS Express for Web 磚](aspnet-mvc-4-dependency-injection/_static/image18.png)

    *VS Express for Web 磚*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>附錄 B：使用程式碼片段

有了程式碼片段，您就可以輕鬆地擁有所需的所有程式碼。 實驗室檔會告訴您可以使用它們的確切時機，如下圖所示。

![使用 Visual Studio 程式碼片段將程式碼插入您的專案](aspnet-mvc-4-dependency-injection/_static/image19.png "使用 Visual Studio 程式碼片段將程式碼插入您的專案")

*使用 Visual Studio 程式碼片段將程式碼插入您的專案*

***若要使用鍵盤新增程式碼片段（C#僅限）***

1. 將游標放在您想要插入程式碼的位置。
2. 開始鍵入程式碼片段名稱（不含空格或連字號）。
3. 監看 IntelliSense 會顯示相符的程式碼片段名稱。
4. 選取正確的程式碼片段（或繼續輸入，直到選取整個程式碼片段的名稱為止）。
5. 按兩次 Tab 鍵，在游標位置插入程式碼片段。

![開始鍵入程式碼片段名稱](aspnet-mvc-4-dependency-injection/_static/image20.png "開始鍵入程式碼片段名稱")

*開始鍵入程式碼片段名稱*

![按 Tab 鍵以選取反白顯示的程式碼片段](aspnet-mvc-4-dependency-injection/_static/image21.png "按 Tab 鍵以選取反白顯示的程式碼片段")

*按 Tab 鍵以選取反白顯示的程式碼片段*

![再按一次 Tab 鍵，將會展開程式碼片段](aspnet-mvc-4-dependency-injection/_static/image22.png "再按一次 Tab 鍵，將會展開程式碼片段")

*再按一次 Tab 鍵，將會展開程式碼片段*

***若要使用滑鼠C#（、Visual Basic 和 XML）加入程式碼片段***sha-1. 以滑鼠右鍵按一下您要插入程式碼片段的位置。

1. 選取 [**插入程式碼片段**]，後面接著 [ **My Code 程式碼片段**]。
2. 按一下清單中的相關程式碼片段，即可加以選取。

![以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]](aspnet-mvc-4-dependency-injection/_static/image23.png "以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]")

*以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]*

![按一下清單中的相關程式碼片段，即可加以選取](aspnet-mvc-4-dependency-injection/_static/image24.png "按一下清單中的相關程式碼片段，即可加以選取")

*按一下清單中的相關程式碼片段，即可加以選取*
