---
uid: mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
title: ASP.NET MVC 4 的新功能 |Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 是一種架構，用來建立可調整且以標準為基礎的 web 應用程式，並使用妥善建立的設計模式和 ASP.NET 的強大功能 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 48f7feb3-872f-485d-b96f-e30011ff8c4a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 4235f4fe666cdeb7d0821127a2b349f2ff30cd6e
ms.sourcegitcommit: 295cf898a4c87e264b0c35c7254b0fa4169f2278
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2019
ms.locfileid: "74057035"
---
# <a name="whats-new-in-aspnet-mvc-4"></a>ASP.NET MVC 4 的新功能

依[Web Camp 團隊](https://twitter.com/webcamps)

[下載 Web Camp 訓練套件](https://aka.ms/webcamps-training-kit)

ASP.NET MVC 4 是一種架構，可讓您使用妥善建立的設計模式以及 ASP.NET 和 .NET framework 的強大功能，來建立可擴充且以標準為基礎的 web 應用程式。 這個新的第四個版本的架構著重于讓行動 web 應用程式開發更輕鬆。

一開始，當您建立新的 ASP.NET MVC 4 專案時，現在有一個行動應用程式專案範本，可讓您用來建立專供行動裝置使用的獨立應用程式。 此外，ASP.NET MVC 4 會透過 jQuery NuGet 套件與 jQuery Mobile 整合。 jQuery Mobile 是一種以 HTML5 為基礎的架構，用於開發與所有熱門行動裝置平臺（包括 Windows Phone、iPhone、Android 等等）相容的 web 應用程式。 不過，如果您需要特製化，ASP.NET MVC 4 也可讓您為不同的裝置提供不同的視圖，並提供裝置特定的優化。

在這個實際操作實驗室中，您將從 ASP.NET MVC 4 &quot;Internet Application&quot; 專案範本開始，以建立相片圖庫應用程式。 您將使用 jQuery Mobile 和 ASP.NET MVC 4 的新功能來逐步增強應用程式，使其與不同的行動裝置和桌上型電腦網頁瀏覽器相容。 您也將瞭解程式碼產生的新程式碼配方，以及 ASP.NET MVC 4 如何藉由支援 Task&lt;ActionResult&gt; 傳回型別，讓您更輕鬆地撰寫非同步動作方法。

> [!NOTE]
> 所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可在[Microsoft web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)取得。 此實驗室的特定專案可在[ASP.NET 4.5 中 Web Forms 的新功能](https://github.com/Microsoft-Web/HOL-ASPNETWebForms)中取得。

<a id="Objectives"></a>
### <a name="objectives"></a>目標

在此實際操作實驗室中，您將瞭解如何：

- 利用 ASP.NET MVC 專案範本的增強功能，包括新的行動應用程式專案範本
- 使用 HTML5 視口屬性和 CSS 媒體查詢來改善行動裝置上的顯示
- 使用 jQuery Mobile 進行漸進式增強，以及建立觸控式優化的 web UI
- 建立行動裝置特定的視圖
- 使用視圖切換器元件，在應用程式中的行動和桌面視圖之間切換
- 使用工作支援建立異步控制器

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Prerequisites

您必須具有下列專案，才能完成此實驗室：

- 適用于 Web 或上層的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （如需如何安裝的指示，請參閱[附錄 B](#AppendixB) ）。
- [ASP.NET MVC 4](../../../mvc4.md) （包含在 Microsoft Visual Studio 2012 安裝中）
- Windows Phone 模擬器（隨附于[Windows Phone 7.1.1 SDK](https://www.microsoft.com/download/details.aspx?id=29233)）
- 選擇性- [WebMatrix 2](https://www.microsoft.com/web/webmatrix/)搭配**電動梅紅 iPhone**模擬器延伸模組（僅適用于使用 iPhone 模擬器流覽 Web 應用程式的練習3）

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>安裝程式

在整個實驗室檔中，系統會指示您插入程式碼區塊。 為了方便起見，大部分的程式碼都是以 Visual Studio Code 程式碼片段的形式提供，您可以從 Visual Studio 內使用它來避免手動新增。

若要安裝程式碼片段：

1. 開啟 Windows Explorer 視窗，並流覽至實驗室的 [ **Source\Setup** ] 資料夾。
2. 按兩下此資料夾中的**Setup .cmd**檔案，安裝 Visual Studio 程式碼片段。

如果您不熟悉 Visual Studio Code 程式碼片段，而且想要瞭解如何使用，您可以參閱本檔中的附錄 &quot;[附錄 A：使用程式碼片段](#AppendixA)&quot;。

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>練習

這個實際操作實驗室包含下列練習：

1. [新的 ASP.NET MVC 4 專案範本](#Exercise1)
2. [建立相片圖庫 Web 應用程式](#Exercise2)
3. [新增行動裝置的支援](#Exercise3)
4. [使用非同步控制器](#Exercise4)

> [!NOTE]
> 每個練習都會伴隨一個**結束**資料夾，其中包含您在完成練習之後應該取得的結果解決方案。 如果您需要額外的協助來進行練習，您可以使用此解決方案做為指南。

完成此實驗室的預估時間： **60 分鐘**。

<a id="Exercise1"></a>

<a id="Exercise_1_New_ASPNET_MVC_4_Project_Templates"></a>
### <a name="exercise-1-new-aspnet-mvc-4-project-templates"></a>練習1：新增 ASP.NET MVC 4 專案範本

在此練習中，您將探索 ASP.NET MVC 4 專案範本中的增強功能。 除了網際網路應用程式範本，已存在於 MVC 3 中，此版本現在還包含適用于行動應用程式的個別範本。 首先，您將會看到每個範本的相關功能。 然後，您可以使用正確的方法，在不同的平臺上正確呈現您的頁面。

<a id="Task_1_-_Exploring_the_Internet_Application_Template"></a>
#### <a name="task-1---exploring-the-internet-application-template"></a>工作 1-探索網際網路應用程式範本

1. 開啟**Visual Studio**。
2. 選取檔案 **|新增 |[專案**] 功能表命令。 在 [**新增專案**] 對話方塊中，**選取C#視覺效果 |** 在左窗格樹狀結構上，選擇 [ **ASP.NET MVC 4 Web 應用程式]。** 將專案命名為**PhotoGallery**，選取位置（或保留預設值），然後按一下 **[確定]** 。

    > [!NOTE]
    > 您稍後會自訂您目前建立的 PhotoGallery ASP.NET MVC 4 解決方案。

    ![建立新專案](whats-new-in-aspnet-mvc-4/_static/image1.png "建立新專案")

    *建立新專案*
3. 在 [**新增 ASP.NET MVC 4 專案**] 對話方塊中，選取 [**網際網路應用程式**] 專案範本，然後按一下 **[確定]** 。 請確定您已選取 Razor 做為 view engine。

    ![建立新的 ASP.NET MVC 4 網際網路應用程式](whats-new-in-aspnet-mvc-4/_static/image2.png "建立新的 ASP.NET MVC 4 網際網路應用程式")

    *建立新的 ASP.NET MVC 4 網際網路應用程式*

    > [!NOTE]
    > Razor 語法已在 ASP.NET MVC 3 中引進。 其目標是要將檔案中所需的字元和按鍵數目降至最低，以啟用快速且流暢的程式碼撰寫工作流程。 Razor 利用現有C# /VB （或其他）語言技能，並提供範本標記語法來啟用絕佳的 HTML 結構工作流程。
4. 按**F5**執行方案，並查看已更新的範本。 您可以查看下列功能：

    **現代化樣式範本**

    這些範本已更新，提供更現代化的樣式。

    ![ASP.NET MVC 4 風貌範本](whats-new-in-aspnet-mvc-4/_static/image3.png "MVC 4 風貌範本")

    *ASP.NET MVC 4 風貌範本*

    ![新增連絡人頁面](whats-new-in-aspnet-mvc-4/_static/image4.png "新增連絡人頁面")

    *新增連絡人頁面*

    **適應性呈現**

    查看調整瀏覽器視窗的大小，並注意頁面配置如何動態適應新的視窗大小。 這些範本會使用自動調整轉譯技術，在桌上型電腦和行動平臺中正確轉譯，而不需要任何自訂。

    ![不同瀏覽器大小的 ASP.NET MVC 4 專案範本](whats-new-in-aspnet-mvc-4/_static/image5.png "不同瀏覽器大小的 ASP.NET MVC 4 專案範本")

    *不同瀏覽器大小的 ASP.NET MVC 4 專案範本*

    **使用 JavaScript 的更豐富 UI**

    預設專案範本的另一個增強功能是使用 JavaScript 來提供更互動式的 JavaScript。 在範本中使用的登入和註冊連結範例說明點如何使用 jQuery 驗證來驗證用戶端的輸入欄位。

    ![jQuery 驗證](whats-new-in-aspnet-mvc-4/_static/image6.png)

    *jQuery 驗證*

    > [!NOTE]
    > 請注意兩個登入區段，您可以在第一節中，使用已註冊的帳戶從網站登入，在第二個區段中，您也可以使用其他驗證服務（如 google）登入（預設為停用）。
5. 關閉瀏覽器以停止偵錯工具，並返回 Visual Studio。
6. 開啟位於**應用程式\_[開始**] 資料夾底下的檔案**AuthConfig.cs** 。
7. 從最後一行移除批註，以註冊 Google 用戶端進行*OAuth*驗證。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample1.cs)]

    > [!NOTE]
    > 請注意，您可以輕鬆地使用任何 OpenID 或 OAuth 服務（例如 Facebook、Twitter、Microsoft 等）來啟用驗證。
8. 按**F5**執行方案，並流覽至登入頁面。
9. 選取 [ **Google**服務] 以登入。

    ![選取登入服務](whats-new-in-aspnet-mvc-4/_static/image7.png)

    *選取登入服務*
10. 使用您的 Google 帳戶登入。
11. 允許網站（localhost）從 Google 帳戶取出資訊。
12. 最後，您將必須在網站中註冊，才能建立 Google 帳戶的關聯。

   ![建立 Google 帳戶的關聯](whats-new-in-aspnet-mvc-4/_static/image8.png)

   *建立 Google 帳戶的關聯*
13. 關閉瀏覽器以停止偵錯工具，並返回 Visual Studio。
14. 現在請探索解決方案，以查看專案範本中 ASP.NET MVC 4 所引進的一些新功能。

   ![ASP.NET MVC 4 網際網路應用程式專案範本](whats-new-in-aspnet-mvc-4/_static/image9.png "ASP.NET MVC 4 網際網路應用程式專案範本")

   *ASP.NET MVC 4 網際網路應用程式專案範本*

    - **HTML 5 標記**

       流覽範本視圖以找出新的主題標記。

       ![新範本，使用 Razor 和 HTML5 標記關於 cshtml。](whats-new-in-aspnet-mvc-4/_static/image10.png "新範本，使用 Razor 和 HTML5 標記關於 cshtml。")

       *使用 Razor 和 HTML5 標記的新範本（關於. cshtml）。*
    - **已更新 JavaScript 程式庫**

       ASP.NET MVC 4 預設範本現在包含 KnockoutJS，這是一種 JavaScript MVVM 架構，可讓您使用 JavaScript 和 HTML 建立豐富且回應速度高的 web 應用程式。 如同在 MVC3 中，jQuery 和 jQuery UI 程式庫也包含在 ASP.NET MVC 4 中。

     > [!NOTE]
     > 您可以在此連結中取得 KnockOutJS 程式庫的詳細資訊： [[http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)](http://learn.knockoutjs.com/)。 此外，您可以在[[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/)中瞭解 jQuery 和 jquery UI。

<a id="Task_2_-_Exploring_the_Mobile_Application_Template"></a>
#### <a name="task-2---exploring-the-mobile-application-template"></a>工作 2-探索行動應用程式範本

ASP.NET MVC 4 有助於開發行動和平板電腦瀏覽器的網站。 此範本具有與網際網路應用程式範本相同的應用程式結構（請注意，控制器程式碼幾乎完全相同），但其樣式已修改為在觸控式行動裝置中正確轉譯。

1. 選取檔案 **|新增 |[專案**] 功能表命令。 在 [**新增專案**] 對話方塊中，**選取C#視覺效果 |Web**範本：在左窗格樹狀結構上，選擇 [ **ASP.NET MVC 4 Web 應用程式]。** 將專案命名為**PhotoGallery**，選取位置（或保留預設值），選取 [&quot;新增至方案]&quot; 然後按一下 **[確定]** 。
2. 在 [**新增 ASP.NET MVC 4 專案**] 對話方塊中，選取 [行動**應用程式**] 專案範本，然後按一下 **[確定]** 。 請確定您已選取 Razor 做為 view engine。

    ![建立新的 ASP.NET MVC 4 行動應用程式](whats-new-in-aspnet-mvc-4/_static/image11.png "建立新的 ASP.NET MVC 4 行動應用程式")

    *建立新的 ASP.NET MVC 4 行動應用程式*
3. 現在您可以流覽解決方案，並查看適用于 mobile 的 ASP.NET MVC 4 解決方案範本所引進的一些新功能：

    - **jQuery Mobile 程式庫**

        行動應用程式專案範本包含 jQuery Mobile library，這是行動瀏覽器相容性的開放原始碼程式庫。 jQuery Mobile 會對支援 CSS 和 JavaScript 的行動瀏覽器套用漸進增強功能。 漸進式增強功能可讓所有瀏覽器顯示網頁的基本內容，而只會啟用最強大的瀏覽器來顯示豐富的內容。 包含在 jQuery Mobile 樣式中的 JavaScript 和 CSS 檔案，可協助行動瀏覽器符合畫面中的內容，而不會在頁面標記中進行任何變更。

        ![jQuery-行動庫-內含-範本](whats-new-in-aspnet-mvc-4/_static/image12.png)

        *範本中包含的 jQuery mobile library*
    - **以 HTML5 為基礎的標記**

        ![Mobile-應用程式-範本-使用-HTML5-標記](whats-new-in-aspnet-mvc-4/_static/image13.png)

        *使用 HTML5 標記的行動應用程式範本（Login. cshtml 和 index. cshtml）*
4. 按**F5**執行方案。
5. 開啟**Windows Phone 7 模擬器**。
6. 在手機的 [開始] 畫面中，開啟 Internet Explorer。 查看桌面應用程式啟動的 URL，並從電話流覽至該 URL （例如 `http://localhost:[PortNumber]/`）。
7. 現在您可以進入登入頁面，或查看 [關於] 頁面。 請注意，網站的樣式是以適用於行動裝置的新 Metro 應用程式為基礎。 ASP.NET MVC 4 專案範本會正確地顯示在行動裝置上，確定頁面的所有元素都是可見的，並且已啟用。 請注意，標頭上的連結夠大，可供按一下或點擊。

    ![行動裝置中的專案範本頁面](whats-new-in-aspnet-mvc-4/_static/image14.png "行動裝置中的專案範本頁面")

    *行動裝置中的專案範本頁面*
8. 新範本也會使用「**視口中繼」標記**。 大部分的行動瀏覽器都會定義虛擬瀏覽器視窗或 &quot;區&quot;的寬度，這大於行動裝置的實際寬度。 這可讓行動瀏覽器在虛擬顯示器內部顯示整個網頁。 「**視口中繼標記**」可讓 網頁程式開發人員在行動裝置上設定瀏覽器區域的寬度、高度和規模 **。** 適用于行動應用程式的 ASP.NET MVC 4 範本會將此視口設定為版面配置範本（*Views\Shared\_layout*）中的裝置寬度（&quot;寬度 = 裝置寬度&quot;），讓所有頁面都將其視口設定為裝置螢幕寬度。 請注意，[視口] 中繼標記不會變更預設瀏覽器視圖。
9. 開啟 **\_Layout**，位於**Views |共用**資料夾，並批註「視口」中繼標記。 執行應用程式（如果尚未開啟），並查看差異。

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample2.cshtml)]

![批註區中繼標記之後的網站](whats-new-in-aspnet-mvc-4/_static/image15.png "批註區中繼標記之後的網站")

*批註區中繼標記之後的網站*
10. 在 Visual Studio 中，按**SHIFT** + **F5**停止對應用程式的偵測。
11. 取消批註視口中繼標記。

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample3.cshtml)]

<a id="Task_3_-_Using_Adaptive_Rendering"></a>
#### <a name="task-3---using-adaptive-rendering"></a>工作 3-使用適應性呈現

在這項工作中，您將學習另一種在行動裝置和網頁瀏覽器上正確呈現網頁的方法，而不需要任何自訂。 您已經使用了類似用途的「視口中繼」標記。 現在您會符合另一個強大的*方法：彈性*轉譯。

適應性轉譯是一種技術，使用**CSS3 媒體查詢**來自訂套用至頁面的樣式。 媒體查詢會定義樣式表單內的條件，並在特定條件下將 CSS 樣式分組。 只有當條件為 true 時，樣式才會套用至已宣告的物件。

調適型轉譯技術所提供的彈性可讓您在不同裝置上顯示網站的任何自訂專案。 您可以在單一樣式表單上定義任意數目的樣式，而不需要撰寫邏輯程式碼來選擇樣式。 因此，它是調整頁面樣式的一種非常棒的方式，因為它會減少重複使用的程式碼和邏輯數量。 另一方面，頻寬耗用量會增加，因為 CSS 檔案的大小可能會逐漸成長。

藉由使用調適型呈現技術，不論瀏覽器為何，您的網站都將會**正確顯示。** 不過，您應該考慮頻寬額外負載是否有問題。

> [!NOTE]
> 媒體查詢的基本格式為： @media \[範圍：全部 |掌上 |列印 |投射 |螢幕\] （[屬性：值] 和 。[屬性：值]）

媒體查詢的範例： &gt; **@media 全部和（最大寬度：1000px）和（最小寬度：700px） {}：** 適用于700px 與1000px 之間的所有解析度。

> **@media 螢幕和（最小寬度：400px）和（最大寬度：700px） {...}：** 僅適用于螢幕。 解決方式必須介於400和700px 之間。
> 
> **@media 掌上型和（最小寬度：20em）、螢幕和（最小寬度：20em） {...}：** 適用于掌上型電腦（行動裝置和裝置）和螢幕。 寬度下限必須大於20em。
> 
> 您可以在[W3C 網站](http://www.w3.org/TR/css3-mediaqueries/)上找到更多有關此的資訊。

您現在將探索彈性轉譯的運作方式，改善 ASP.NET MVC 4 預設網站範本的可讀性。

1. 開啟您在工作1建立的 [ **PhotoGallery** ] 方案，然後選取 [ **PhotoGallery** ] 專案。 按**F5**執行方案。
2. 調整瀏覽器寬度的大小，將視窗設定為一半或小於其原始大小的一季。 請注意標頭中的專案會發生什麼情況：部分元素不會出現在標頭的可見區域中。
3. 從位於 [**內容**] 專案資料夾中的 Visual Studio 方案瀏覽器開啟 [**網站 .css**檔案]。 按**CTRL + F**以開啟 Visual Studio 整合式搜尋，然後撰寫 `@media` 以尋找**CSS 媒體查詢**。

    此範本中定義的媒體查詢準則會以這種方式運作：當瀏覽器的視窗大小低於**850 Px**時，所套用的 CSS 規則就是在此媒體區塊內定義的樣式。

    ![尋找媒體查詢](whats-new-in-aspnet-mvc-4/_static/image16.png "尋找媒體查詢")

    *尋找媒體查詢*
4. 將 850 px 中設定的最大寬度屬性值取代為**10px**，以停用自動調整轉譯，然後按**CTRL + S**儲存變更。 返回瀏覽器，然後按下**CTRL + F5** ，使用您所做的變更來重新整理頁面。 在調整視窗的寬度時，請注意這兩個頁面的差異。

    ![在左側，頁面會套用 @media 樣式，在右邊，會省略樣式](whats-new-in-aspnet-mvc-4/_static/image17.png "在左側，頁面會套用 @media 樣式，在右邊，會省略樣式")

    *在左側，頁面會套用 @media 樣式，在右邊，會省略樣式*

    現在，讓我們來看看行動裝置會發生什麼事：

    ![在左側，頁面會套用 @media 樣式，在右邊，會省略樣式](whats-new-in-aspnet-mvc-4/_static/image18.png "在左側，頁面會套用 @media 樣式，在右邊，會省略樣式")

    *在左側，頁面會套用 @media 樣式，在右邊，會省略樣式*

    雖然您會注意到網頁在網頁瀏覽器中呈現時的變更並不重要，但在使用行動裝置時，差異變得更明顯。 在影像的左邊，我們可以看到自訂樣式已改善可讀性。

    彈性轉譯可以在許多案例中使用，讓您更輕鬆地將條件式樣式套用至網站，並使用整齊的方法解決常見的樣式問題。

    「視口」中繼標記和 CSS 媒體查詢不是 ASP.NET MVC 4 特有的，因此您可以在任何 web 應用程式中利用這些功能。
5. 在 Visual Studio 中，按**SHIFT** + **F5**停止對應用程式的偵測。

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_the_Photo_Gallery_Web_Application"></a>
### <a name="exercise-2-creating-the-photo-gallery-web-application"></a>練習2：建立相片圖庫 Web 應用程式

在此練習中，您將使用相片圖庫應用程式來顯示相片。 您將從 ASP.NET MVC 4 專案範本開始，然後新增功能以從服務抓取相片，並將其顯示在首頁中。

在下列練習中，您將更新此解決方案，以增強其在行動裝置上的顯示方式。

<a id="Task_1_-_Creating_a_Mock_Photo_Service"></a>
#### <a name="task-1---creating-a-mock-photo-service"></a>工作 1-建立 Mock 相片服務

在這項工作中，您將建立相片服務的 mock，以抓取將顯示在資源庫中的內容。 若要這麼做，您將加入新的控制器，只會傳回包含每張相片資料的 JSON 檔案。

1. 開啟**Visual Studio** （如果尚未開啟）。
2. 選取檔案 **|新增 |[專案**] 功能表命令。 在 [**新增專案**] 對話方塊中，**選取C#視覺效果 |** 在左窗格樹狀結構上，選擇 [ **ASP.NET MVC 4 Web 應用程式]。** 將專案命名為**PhotoGallery**，選取位置（或保留預設值），然後按一下 **[確定]** 。 或者，您可以繼續使用**練習 1**中現有的 ASP.NET MVC 4**網際網路應用程式**解決方案，並略過下一個步驟。
3. 在 [**新增 ASP.NET MVC 4 專案**] 對話方塊中，選取 [**網際網路應用程式**] 專案範本，然後按一下 **[確定]** 。 請確定您已選取 Razor 做為 View Engine。
4. 在 **方案總管**中，以滑鼠右鍵按一下專案的**應用程式\_Data**  資料夾，然後選取 **新增 |現有的專案**。 流覽至此實驗室的**Source\Assets\App\_Data**資料夾，並新增**相片. json**檔案。
5. 建立名為**PhotoController**的新控制器。 若要這麼做，請在 [**控制器**] 資料夾上按一下滑鼠右鍵，移至 [**新增**]，然後選取 [**控制器]。** 完成 [控制器名稱]，保留**空白的 [MVC 控制器**] 範本，然後按一下 [**新增**]。

    ![新增 PhotoController](whats-new-in-aspnet-mvc-4/_static/image19.png "新增 PhotoController")

    *新增 PhotoController*
6. 以下列元件**庫**動作取代**Index**方法，並從您最近新增至專案的 JSON 檔案傳回內容。

    （程式碼片段- *ASP.NET MVC 4 Lab-Ex02-圖庫動作*）

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample4.cs)]
7. 按**F5**執行解決方案，然後流覽至下列 URL，以測試模擬相片服務： `http://localhost:[port]/photo/gallery` （[埠] 值取決於啟動應用程式的目前埠）。 此 URL 的要求應該會抓取**相片. json**檔案的內容。

    ![測試模擬相片服務](whats-new-in-aspnet-mvc-4/_static/image20.png "測試模擬相片服務")

    *測試模擬相片服務*

在實際的執行中，您可以使用[ASP.NET Web API](../../../../web-api/index.md)來執行相片圖庫服務。 ASP.NET Web API 是一種架構，可讓您輕鬆地建立可觸及各種用戶端（包括瀏覽器和行動裝置）的 HTTP 服務。 ASP.NET Web 應用程式開發介面是在 .NET Framework 上建置 RESTful 應用程式的理想平台。

<a id="Task_2_-_Displaying_the_Photo_Gallery"></a>
#### <a name="task-2---displaying-the-photo-gallery"></a>工作 2-顯示相片圖庫

在這項工作中，您將使用在本練習的第一個工作中建立的模擬服務，更新首頁以顯示相片圖庫。 您將會新增模型檔案，並更新資源庫視圖。

1. 在 Visual Studio 中，按**SHIFT** + **F5**停止對應用程式的偵測。
2. 在 [**模型**] 資料夾中建立**相片**類別。 若要這麼做，請在 [**模型**] 資料夾上按一下滑鼠右鍵，選取 [**新增**]，然後按一下 [**類別**]。 然後，將名稱設定為**Photo.cs** ，然後按一下 [**新增**]。
3. 將下列成員新增至**Photo**類別。

    （程式碼片段- *ASP.NET MVC 4 Lab-Ex02-相片 model*）

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample5.cs)]
4. 從 **Controllers** 資料夾中，開啟 **HomeController.cs** 檔案。
5. 使用陳述式加入下列程式碼。

    （程式碼片段- *ASP.NET MVC 4 Lab-Ex02-HomeController using*）

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample6.cs)]
6. 更新 [**索引**] 動作，以使用**HttpClient**來抓取圖庫資料，然後使用**JavaScriptSerializer**將它還原序列化為視圖模型。

    （程式碼片段- *ASP.NET MVC 4 實驗室-Ex02-索引動作*）

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample7.cs)]
7. 開啟位於**Views\Home**資料夾底下的**Index. cshtml**檔案，並以下列程式碼取代所有內容。

    此程式碼會在所有從服務中取出的相片上執行迴圈，並將其顯示為未排序清單。

    （程式碼片段- *ASP.NET MVC 4 實驗室-Ex02-相片清單*）

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample8.cshtml)]
8. 在 **方案總管**中，以滑鼠右鍵按一下專案的 **內容** 資料夾，然後選取 **新增 |現有的專案**。 流覽至此實驗室的 [ **Source\Assets\Content** ] 資料夾，然後新增 [**網站 .css** ] 檔案。 您將必須確認其取代。 如果您已開啟**網站 .css**檔案，就必須確認是否也要重載檔案。
9. 開啟 [檔案瀏覽器]，然後將位於此實驗室的 [ **Source\Assets** ] 資料夾底下的整個**相片**資料夾，複製到方案總管中專案的根資料夾。
10. 執行應用程式。 您現在應該會在圖庫中看到顯示相片的首頁。

    ![相片圖庫](whats-new-in-aspnet-mvc-4/_static/image21.png "相片圖庫")

    *相片圖庫*
11. 在 Visual Studio 中，按**SHIFT** + **F5**停止對應用程式的偵測。

<a id="Exercise3"></a>

<a id="Exercise_3_Adding_support_for_mobile_devices"></a>
### <a name="exercise-3-adding-support-for-mobile-devices"></a>練習3：新增行動裝置的支援

ASP.NET MVC 4 中的其中一個重要更新是行動裝置開發的支援。 在此練習中，您將藉由擴充您在上一個練習中建立的 PhotoGallery 解決方案，探索行動應用程式的 ASP.NET MVC 4 新功能。

<a id="Task_1_-_Installing_jQuery_Mobile_in_an_ASPNET_MVC_4_Application"></a>
#### <a name="task-1---installing-jquery-mobile-in-an-aspnet-mvc-4-application"></a>工作 1-在 ASP.NET MVC 4 應用程式中安裝 jQuery Mobile

1. 開啟位於**來源/Ex3-MobileSupport/開始/** 資料夾的 [**開始**] 解決方案。 否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。

   1. 如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
2. 按一下 **工具** >  **NuGet 套件管理員** > **套件管理員主控台** 功能表選項，以開啟 **套件管理員主控台**。

    ![開啟 NuGet 套件管理員主控台](whats-new-in-aspnet-mvc-4/_static/image22.png "開啟 NuGet 套件管理員主控台")

    *開啟 NuGet 套件管理員主控台*
3. 在 [套件管理員主控台] 中，執行下列命令以安裝**jQuery.** node.js 封裝。

    jQuery Mobile 是一種開放原始碼程式庫，可用於建立觸控式優化的 web UI。 JQuery NuGet 套件包含協助程式搭配 ASP.NET MVC 4 應用程式使用 jQuery Mobile。

    > [!NOTE]
    > 藉由執行下列命令，您將會從 Nuget 下載 jQuery. MVC 程式庫。

    PM

    [!code-powershell[Main](whats-new-in-aspnet-mvc-4/samples/sample9.ps1)]

    此命令會安裝 jQuery Mobile 和一些 helper 檔案，包括下列各項：

    - **Views/Shared/\_Layout**：是以 jQuery mobile 為基礎的版面配置，針對較小的螢幕進行優化。 當網站從行動瀏覽器收到要求時，會將原始配置（\_Layout）取代為此配置。
    - View-切換器元件：由**Views/Shared/\_ViewSwitcher**部分視圖和**ViewSwitcherController.cs**控制器所組成。 此元件會在行動瀏覽器上顯示連結，讓使用者切換到桌上出版本的頁面。  
        ![具有行動支援的相片圖庫專案](whats-new-in-aspnet-mvc-4/_static/image23.png "Ph具有行動支援的 oto 資源庫專案 "）

        *具有行動支援的相片圖庫專案*
4. 註冊行動套件組合。 若要這麼做，請開啟**Global.asax.cs**檔案，並新增下列這一行。

    （程式碼片段- *ASP.NET MVC 4 Lab-Ex03-註冊*行動套件組合）

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample10.cs)]
5. 使用桌面 web 瀏覽器執行應用程式。
6. 開啟位於 [開始] 功能表中的 [ **Windows Phone 7 模擬器**] **|所有程式 |Windows Phone SDK 7.1 |Windows Phone 模擬器。**
7. 在手機的 [開始] 畫面中，開啟 Internet Explorer。 查看應用程式啟動的 URL，並使用電話瀏覽器流覽至該 URL （例如 `http://localhost:[PortNumber]/`）。

    您會注意到，在 Windows Phone 模擬器中，您的應用程式看起來會不同，因為 jQuery 會在專案中建立新的資產，以顯示針對行動裝置優化的視圖。

    請注意電話頂端的訊息，其中會顯示切換到桌面視圖的連結。 此外，您已安裝之封裝所建立的 **\_配置。** 在應用程式中包含不同的版面配置。

    > [!NOTE]
    > 到目前為止，沒有可回到 mobile view 的連結。 這會包含在較新的版本中。

    ![[相片圖庫] 首頁的 [移動流覽]](whats-new-in-aspnet-mvc-4/_static/image24.png "[相片圖庫] 首頁的 [移動流覽]")

    *[相片圖庫] 首頁的 [移動流覽]*
8. 在 Visual Studio 中，按**SHIFT** + **F5**停止對應用程式的偵測。

<a id="Task_2_-_Creating_Mobile_Views"></a>
#### <a name="task-2---creating-mobile-views"></a>工作 2-建立行動裝置視圖

在這項工作中，您將建立索引視圖的行動版，並將內容調整為可在行動裝置中更佳的外觀。

1. 複製 [ **Views\Home\Index.cshtml** ] 視圖並貼上以建立複本，並將新檔案重新**命名為 [.]** 。
2. 開啟新建立的 [node.js **] 視圖，** 並使用此程式碼取代現有的 &lt;ul&gt; 標記。 如此一來，您將會使用 jQuery Mobile 資料批註來更新 &lt;ul&gt; 標記，以使用 jQuery 中的行動主題。

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample11.html)]

    > [!NOTE] 
    > 
    > 請注意：
    > 
    > - 設定為**listview**的**資料角色**屬性會使用 listview 樣式來轉譯清單。
    > 
    > - **資料-內陷**屬性設為 true 時，會顯示具有圓角框線和邊界的清單。
    > 
    > - 設定為**true**的**資料篩選**屬性會產生搜尋方塊。
    > 
    > 您可以在專案檔案中深入瞭解 jQuery Mobile 慣例： [ [http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)
3. 按**CTRL + S**儲存變更。
4. 切換至**Windows Phone 模擬器**並重新整理網站。 請注意，圖庫清單的新外觀與風格，以及位於頂端的新搜尋方塊。 然後在 [搜尋] 方塊中輸入一個字（例如， **Tulips**），以在相片圖庫中開始搜尋。

    ![使用 listview 樣式搭配篩選的資源庫](whats-new-in-aspnet-mvc-4/_static/image25.png "使用 listview 樣式搭配篩選的資源庫")

    *使用 listview 樣式搭配篩選的資源庫*

    總而言之，您已使用 View Mobilizer 配方，以 &quot;mobile&quot; 尾碼來建立索引視圖的複本。 這個尾碼表示 ASP.NET MVC 4，從行動裝置產生的每個要求都會使用此索引複本。 此外，您已更新索引視圖的行動版，以使用 jQuery Mobile 來增強行動裝置中的網站外觀與風格。
5. 返回 Visual Studio**並開啟位於** **Content**資料夾底下的 node.js。
6. 修正相片標題的位置，使其顯示在影像的右側。 若要這麼做，請將下列程式碼新增至 node.js**檔案。**

    CSS

    [!code-css[Main](whats-new-in-aspnet-mvc-4/samples/sample12.css)]
7. 按**CTRL + S**儲存變更。
8. 切換回**Windows Phone 模擬器**並重新整理網站。 請注意，相片標題現在已正確定位。

    ![標題位於影像右邊](whats-new-in-aspnet-mvc-4/_static/image26.png "標題位於影像右邊")

    *標題位於影像右邊*

<a id="Task_3_-_jQuery_Mobile_Themes"></a>
#### <a name="task-3---jquery-mobile-themes"></a>工作 3-jQuery Mobile 主題

JQuery Mobile 中的每個版面配置和小工具都是針對新的物件導向 CSS 架構所設計，可讓您將完整的統一視覺效果設計主題套用至網站和應用程式。

jQuery Mobile 的預設主題包含5個以字母（a、b、c、d、e）提供的色板，以供快速參考。

在這項工作中，您將更新行動配置，以使用與預設不同的主題。

1. 切換回 Visual Studio。
2. 開啟位於**Views\Shared**的 **\_Layout**檔案。
3. 尋找 資料-角色 設定為 &quot; 頁面上的 div 元素&quot; 並將**資料主題**更新為 &quot;**e**&quot;。

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample13.html)]
4. 按**CTRL + S**儲存變更。
5. 重新整理**Windows Phone 模擬器**中的網站，並注意新的色彩配置。

    ![使用不同色彩配置的行動裝置版面配置](whats-new-in-aspnet-mvc-4/_static/image27.png "使用不同色彩配置的行動裝置版面配置")

    *使用不同色彩配置的行動裝置版面配置*

<a id="Task_4_-_Using_the_View-Switcher_Component_and_the_Browser_Overriding_Features"></a>
#### <a name="task-4---using-the-view-switcher-component-and-the-browser-overriding-features"></a>工作 4-使用視圖切換器元件和瀏覽器覆寫功能

行動優化網頁的慣例是加入一個連結，其文字類似于桌面視圖或完整網站模式，可讓使用者切換至桌上出版本的頁面。 JQuery 封裝包含用於 **\_** 配置中的這個用途的範例**視圖切換**器元件。請參閱。

![切換至桌面視圖的連結](whats-new-in-aspnet-mvc-4/_static/image28.png "切換至桌面視圖的連結")

*切換至桌面視圖的連結*

「視圖切換器」會使用稱為「**瀏覽器覆寫**」的新功能。 這項功能可讓您的應用程式將要求視為來自不同的瀏覽器（使用者代理程式），而不是實際的來源。

在這項工作中，您將探索 jQuery 所新增之視圖切換器的範例執行，以及覆寫 ASP.NET MVC 4 中功能的新瀏覽器。

1. 切換回 Visual Studio。
2. 開啟位於 [ **Views\Shared** ] 資料夾底下的 [ **\_** 配置]，並注意被參考為部分視圖的視圖切換器元件。

    ![使用視圖切換器元件的行動版面配置](whats-new-in-aspnet-mvc-4/_static/image29.png "使用視圖切換器元件的行動版面配置")

    *使用視圖切換器元件的行動版面配置*
3. 開啟 [ **\_ViewSwitcher** ] [部分視圖]。

    部分視圖會使用 ViewCoNtext 的新方法**GetOverriddenBrowser （）** 來判斷 web 要求的來源，並顯示對應的連結以切換到桌面或行動裝置的瀏覽器。

    **GetOverriddenBrowser**方法會傳回**HttpBrowserCapabilitiesBase**實例，其對應至目前針對要求所設定的使用者代理程式（實際或已覆寫）。 您可以使用這個值來取得**IsMobileDevice**之類的屬性。

    ![ViewSwitcher 部分視圖](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher 部分視圖")

    *ViewSwitcher 部分視圖*
4. 開啟位於 [**控制器**] 資料夾中的**ViewSwitcherController.cs**類別。 查看 ViewSwitcher 元件中的連結所呼叫的 SwitchView 動作，並注意新的 HttpCoNtext 方法。

    - **ClearOverriddenBrowser （）** 方法會移除目前要求的任何已覆寫使用者代理程式。
    - **SetOverriddenBrowser （）** 方法會使用指定的使用者代理程式，覆寫要求的實際使用者代理程式值。  
        ![ViewSwitcher 控制器](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher 控制器」）  
*ViewSwitcher 控制器*

        瀏覽器覆寫是 ASP.NET MVC 4 的核心功能，即使您未安裝 jQuery. node.js 封裝也可以使用。 不過，這項功能只會影響視圖、版面配置和部分查看，而且不會影響任何相依于要求的功能。 Browser 物件。

<a id="Task_5_-_Adding_the_View-Switcher_in_the_Desktop_View"></a>
#### <a name="task-5---adding-the-view-switcher-in-the-desktop-view"></a>工作 5-在桌面視圖中新增視圖切換器

在這項工作中，您將更新桌上出版面配置以包含視圖切換器。 這可讓行動使用者在流覽桌面視圖時回到行動視圖。

1. 重新整理**Windows Phone 模擬器**中的網站。
2. 按一下資源庫頂端的 [**桌面視圖**] 連結。 請注意，桌上型電腦視圖中沒有任何視圖切換器可讓您返回行動裝置視圖。
3. 返回 Visual Studio，然後開啟 [ **\_Layout** ] 視圖。
4. 尋找 [登入] 區段，然後插入呼叫，將 **\_ViewSwitcher**部分視圖轉譯 **\_LogOnPartial**部分視圖底下。 然後，按**CTRL + S**儲存變更。

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample14.cshtml)]
5. 按**CTRL + S**儲存變更。
6. 重新整理 Windows Phone 模擬器中的頁面，然後按兩下畫面以放大。 請注意，[首頁] 頁面現在會顯示從 [行動裝置] 切換到 [桌面] 視圖的 [**移動流覽**] 連結。

    ![桌面視圖中呈現的視圖切換器](whats-new-in-aspnet-mvc-4/_static/image32.png "桌面視圖中呈現的視圖切換器")

    *桌面視圖中呈現的視圖切換器*
7. 再次切換到行動裝置視圖，然後流覽至 [**關於**] 頁面（ http://localhost [埠]/Home/About）。 請注意，即使您尚未建立 About. # view 視圖，[About] 頁面還是會使用行動配置（\_Layout）來顯示。

    ![關於頁面](whats-new-in-aspnet-mvc-4/_static/image33.png "About 頁面")

    *關於頁面*
8. 最後，在桌面網頁瀏覽器中開啟網站。 請注意，先前的更新都不會影響到桌面視圖。

    ![PhotoGallery 桌面視圖](whats-new-in-aspnet-mvc-4/_static/image34.png "PhotoGallery 桌面視圖")

    *PhotoGallery 桌面視圖*

<a id="Task_6_-_Creating_New_Display_Modes"></a>
#### <a name="task-6---creating-new-display-modes"></a>工作 6-建立新的顯示模式

新的顯示模式功能可讓應用程式根據產生要求的瀏覽器選取 views。 例如，如果桌面瀏覽器要求首頁，應用程式將會傳回**Views\Home\Index.cshtml**範本。 然後，如果行動瀏覽器要求首頁，應用程式將會傳回**Views\Home\Index.mobile.cshtml**範本。

在這項工作中，您將建立 iPhone 裝置的自訂版面配置，而且您必須模擬 iPhone 裝置的要求。 若要執行這項操作，您可以使用 iPhone 模擬器/模擬器（例如[電動](http://www.electricplum.com/)行動模擬器）或具有修改使用者代理程式之附加元件的瀏覽器。 如需如何在 Safari 瀏覽器中設定使用者代理程式字串以模擬 iPhone 的指示，請參閱[如何讓 safari](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html)在 David Alison 的 blog 中偽裝成 IE。

**請注意，這項工作是選擇性的，您可以在整個實驗室中繼續進行，而不需要執行它。**

1. 在 Visual Studio 中，按**SHIFT** + **F5**停止對應用程式的偵測。
2. 開啟**Global.asax.cs** ，並加入下列 using 語句。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample15.cs)]
3. 將下列反白顯示的程式碼新增至應用程式\_Start 方法。

    （程式碼片段- *ASP.NET MVC 4 Lab-Ex03-IPhone DisplayMode*）

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample16.cs)]

您已在靜態**DisplayModeProvider**中註冊**名為 &quot;iPhone&quot;** 的新 DefaultDisplayMode，其將會針對每個連入要求進行比對。 如果傳入要求包含 iPhone&quot;&quot;的字串，ASP.NET MVC 會尋找其名稱包含 &quot;iPhone&quot; 尾碼的視圖。 0參數表示新模式的特定方式。比方說，此視圖比一般 &quot;更明確。行動&quot; 規則符合來自行動裝置的要求。

在此程式碼執行之後，當 iPhone 瀏覽器產生要求時，您的應用程式將會使用 Views\Shared\\您將在後續步驟中建立的 **_Layout. iPhone. cshtml**配置。

> [!NOTE]
> 這種測試 iPhone 要求的方式已經簡化，以供示範之用，而且可能無法依每個 iPhone 使用者代理程式字串（例如測試區分大小寫）的預期運作。

4. 在**Views\Shared**資料夾中建立 **\_Layout**檔案的複本，並將複本重新命名為 &quot; **\_Layout. cshtml**&quot;。
5. 開啟您在上一個步驟中建立的 **\_Layout. cshtml** 。
6. 尋找 [資料-角色] 屬性設定為 [**頁面**] 的 div 元素，然後將 [**資料主題**] 屬性變更**為 &quot;&quot;** 。

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample17.cshtml)]

您的 ASP.NET MVC 4 應用程式現在有3個版面配置：

1. **\_配置. cshtml**：用於桌面瀏覽器的預設版面配置。
2. **\_layout**：用於行動裝置的預設配置。
3. **\_layout**： iphone 裝置的特定版面配置，使用不同的色彩配置來區別 \_的 layout。
7. 按**F5**以執行應用程式，並在**Windows Phone 模擬器**中流覽網站。
8. 開啟**iPhone**模擬器（如需有關如何安裝和設定 iPhone 模擬器的指示，請參閱[附錄 C](#AppendixC) ），並流覽至網站。 請注意，每個電話都會使用特定的範本。

    ![使用-不同-views-每個 device2](whats-new-in-aspnet-mvc-4/_static/image35.png)

    *針對每個行動裝置使用不同的視圖*

<a id="Exercise4"></a>

<a id="Exercise_4_Using_Asynchronous_Controllers"></a>
### <a name="exercise-4-using-asynchronous-controllers"></a>練習4：使用非同步控制器

Microsoft .NET Framework 4.5 引進和 Visual Basic 中C#的新語言功能，以在 .net 程式設計中提供非同步新基礎。 這個新的基礎使非同步程式設計類似-，而且與同步程式設計一樣簡單。 您現在可以使用**AsyncController**類別，在 ASP.NET MVC 4 中撰寫非同步動作方法。 您可以針對長時間執行的非 CPU 系結要求使用非同步動作方法。 這可避免在處理要求時，阻止 Web 服務器執行工作。 AsyncController 類別通常用於長時間執行的 Web 服務呼叫。

此練習說明 ASP.NET MVC 4 中非同步作業的基本概念。 如果您想要深入瞭解，您可以參閱下列文章： [ [https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)

<a id="Task_1_-_Implementing_an_Asynchronous_Controller"></a>
#### <a name="task-1---implementing-an-asynchronous-controller"></a>工作 1-執行非同步控制器

1. 開啟位於 [**來源/Ex4-非同步/開始/** 資料夾] 的 [**開始**] 解決方案。 否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。

   1. 如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
2. 從 [**控制器**] 資料夾開啟**HomeController.cs**類別。
3. 新增下列 using 語句。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample18.cs)]
4. 更新**HomeController**類別以繼承自**AsyncController**。 衍生自 AsyncController 的控制器可讓 ASP.NET 處理非同步要求，而且仍然可以服務同步動作方法。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample19.cs)]
5. 將**async**關鍵字新增至**Index**方法，使其傳回類型工作 **&lt;ActionResult&gt;** 。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample20.cs)]

    > [!NOTE]
    > **Async**關鍵字是 .NET Framework 4.5 提供的其中一個新關鍵字;它會告知編譯器此方法包含非同步程式碼。 **Task**物件代表可能在未來某個時間點完成的非同步作業。
6. 取代**用戶端。** 使用 await 關鍵字以完整非同步版本呼叫 GetAsync （），如下所示。

    （程式碼片段- *ASP.NET MVC 4 Lab-Ex04-GetAsync*）

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample21.cs)]

    > [!NOTE]
    > 在先前的版本中，您使用**工作物件的** **Result**屬性來封鎖執行緒，直到傳回結果為止（同步處理版本）。
    > 
    > 新增**await**關鍵字會指示編譯器以非同步方式等候方法呼叫所傳回的工作。 這表示程式碼的其餘部分只會在等候的方法完成之後，以回呼的形式執行。 另一個要注意的是，您不需要變更您的 try-catch 區塊來進行這項工作：在背景或前景中所發生的例外狀況仍會被攔截，而不需要使用架構所提供的處理常式進行任何額外的工作。
7. 將程式碼取代為新的程式碼，如下所示，藉以變更程式碼以繼續進行非同步執行

    （程式碼片段- *ASP.NET MVC 4 Lab-Ex04-ReadAsStringAsync*）

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample22.cs)]
8. 執行應用程式。 您會注意到沒有重大變更，但您的程式碼不會封鎖執行緒集區中的執行緒，讓伺服器資源的使用更好，並提升效能。

    > [!NOTE]
    > 您可以深入瞭解實驗室中新的非同步程式設計功能 &quot; **.net 4.5 中的非同步程式設計C# ，以及**Visual Studio 訓練套件中包含的 Visual Basic&quot;。

<a id="Task_2_-_Handling_Time-Outs_with_Cancellation_Tokens"></a>
#### <a name="task-2---handling-time-outs-with-cancellation-tokens"></a>工作 2-使用解除標記處理超時

傳回工作實例的非同步動作方法也可以支援超時。 在這項工作中，您將會更新索引方法程式碼，以使用解除標記來處理超時案例。

1. 返回 Visual Studio，然後按**SHIFT + F5**停止調試。
2. 將下列 using 語句新增至**HomeController.cs**檔案。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample23.cs)]
3. 更新索引動作以接收**CancellationToken**引數。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample24.cs)]
4. 更新**GetAsync**呼叫以傳遞解除標記。

    （程式碼片段- *ASP.NET MVC 4 Lab-Ex04-SendAsync With CancellationToken*）

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample25.cs)]
5. 將**AsyncTimeout**屬性設為500毫秒，並將**HandleError**屬性設定為藉由重新導向至**TimedOut**視圖來處理**TaskCanceledException** ，以裝飾*索引*方法。

    （程式碼片段- *ASP.NET MVC 4 實驗室-Ex04-屬性*）

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample26.cs)]
6. 開啟**PhotoController**類別並更新資源**庫**方法，以順延強制1000毫秒（1秒）來模擬長時間執行的工作。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample27.cs)]
7. 開啟 web.config**檔案**，並藉由新增下列元素來啟用自訂錯誤。

    [!code-xml[Main](whats-new-in-aspnet-mvc-4/samples/sample28.xml)]
8. 在**Views\Shared**中建立名為**TimedOut**的新視圖，並使用預設版面配置。 在 方案總管中，以滑鼠右鍵按一下  **Views\Shared**  資料夾，然後選取 **新增 |View**。

    ![針對每個行動裝置使用不同的視圖](whats-new-in-aspnet-mvc-4/_static/image36.png "針對每個行動裝置使用不同的視圖")

    *針對每個行動裝置使用不同的視圖*
9. 更新**TimedOut** view 內容，如下所示。

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample29.cshtml)]
10. 執行應用程式，並流覽至根 URL。 當您已新增執行緒時，就會出現一段時間1000毫秒的**睡眠**，您將會收到逾時錯誤，由**AsyncTimeout**屬性產生並由**HandleError**屬性攔截。

    ![已處理超時例外狀況](whats-new-in-aspnet-mvc-4/_static/image37.png "已處理超時例外狀況")

    *已處理超時例外狀況*

> [!NOTE]
> 此外，您可以遵循[附錄 D：使用 Web Deploy 發佈 ASP.NET MVC 4 應用程式](#AppendixD)，將此應用程式部署到 Windows Azure 網站。

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>總結

在這個實際操作實驗室中，您已觀察到 ASP.NET MVC 4 中的一些新功能。 已討論過下列概念：

- 利用 ASP.NET MVC 專案範本的增強功能，包括新的行動應用程式專案範本
- 使用 HTML5 視口屬性和 CSS 媒體查詢來改善行動裝置上的顯示
- 使用 jQuery Mobile 進行漸進式增強，以及建立觸控式優化的 web UI
- 建立行動裝置特定的視圖
- 使用視圖切換器元件，在應用程式中的行動和桌面視圖之間切換
- 使用工作支援建立異步控制器

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a>附錄 A：使用程式碼片段

有了程式碼片段，您就可以輕鬆地擁有所需的所有程式碼。 實驗室檔會告訴您可以使用它們的確切時機，如下圖所示。

![使用 Visual Studio 程式碼片段將程式碼插入您的專案](whats-new-in-aspnet-mvc-4/_static/image38.png "使用 Visual Studio 程式碼片段將程式碼插入您的專案")

*使用 Visual Studio 程式碼片段將程式碼插入您的專案*

***若要使用鍵盤新增程式碼片段（C#僅限）***

1. 將游標放在您想要插入程式碼的位置。
2. 開始鍵入程式碼片段名稱（不含空格或連字號）。
3. 監看 IntelliSense 會顯示相符的程式碼片段名稱。
4. 選取正確的程式碼片段（或繼續輸入，直到選取整個程式碼片段的名稱為止）。
5. 按兩次 Tab 鍵，在游標位置插入程式碼片段。

![開始鍵入程式碼片段名稱](whats-new-in-aspnet-mvc-4/_static/image39.png "開始鍵入程式碼片段名稱")

*開始鍵入程式碼片段名稱*

![按 Tab 鍵以選取反白顯示的程式碼片段](whats-new-in-aspnet-mvc-4/_static/image40.png "按 Tab 鍵以選取反白顯示的程式碼片段")

*按 Tab 鍵以選取反白顯示的程式碼片段*

![再按一次 Tab 鍵，將會展開程式碼片段](whats-new-in-aspnet-mvc-4/_static/image41.png "再按一次 Tab 鍵，將會展開程式碼片段")

*再按一次 Tab 鍵，將會展開程式碼片段*

***若要使用滑鼠（C#、VISUAL BASIC 和 XML）加入程式碼片段***

1. 以滑鼠右鍵按一下您要插入程式碼片段的位置。
2. 選取 [**插入程式碼片段**]，後面接著 [ **My Code 程式碼片段**]。
3. 按一下清單中的相關程式碼片段，即可加以選取。

![以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]](whats-new-in-aspnet-mvc-4/_static/image42.png "以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]")

*以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]*

![按一下清單中的相關程式碼片段，即可加以選取](whats-new-in-aspnet-mvc-4/_static/image43.png "按一下清單中的相關程式碼片段，即可加以選取")

*按一下清單中的相關程式碼片段，即可加以選取*

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a>附錄 B：安裝 Web 的 Visual Studio Express 2012

您可以使用 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** 安裝 Web 或另一個 &quot;Express&quot; 版本**的 Microsoft Visual Studio Express 2012** 。 下列指示會引導您完成使用*Microsoft Web Platform Installer*安裝*Visual studio Express 2012 for Web*所需的步驟。

1. 移至[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。 或者，如果您已經安裝 Web Platform Installer，您可以開啟它，然後使用 Windows Azure SDK&quot;來搜尋產品 &quot;*Visual Studio Express 2012 For Web* 。
2. 按一下 [**立即安裝**]。 如果您沒有**Web Platform Installer**系統會將您重新導向，先下載並安裝。
3. 開啟**Web Platform Installer**之後，請按一下 [**安裝**] 以啟動安裝程式。

    ![安裝 Visual Studio Express](whats-new-in-aspnet-mvc-4/_static/image44.png "安裝 Visual Studio Express")

    *安裝 Visual Studio Express*
4. 閱讀所有產品的授權和條款，然後按一下 [**我接受**] 繼續。

    ![接受授權條款](whats-new-in-aspnet-mvc-4/_static/image45.png)

    *接受授權條款*
5. 等到下載和安裝程式完成為止。

    ![安裝進度](whats-new-in-aspnet-mvc-4/_static/image46.png)

    *安裝進度*
6. 當安裝完成時，按一下 **[完成]** 。

    ![安裝已完成](whats-new-in-aspnet-mvc-4/_static/image47.png)

    *安裝已完成*
7. 按一下 **[** 結束] 以關閉 Web Platform Installer。
8. 若要開啟 Web Visual Studio Express，請移至 [**開始**] 畫面，然後開始撰寫 &quot;**VS Express**&quot;，然後按一下 [ **VS Express for Web** ] 磚。

    ![VS Express for Web 磚](whats-new-in-aspnet-mvc-4/_static/image48.png)

    *VS Express for Web 磚*

<a id="AppendixC"></a>

<a id="Appendix_C_Installing_WebMatrix_2_and_iPhone_Simulator"></a>
## <a name="appendix-c-installing-webmatrix-2-and-iphone-simulator"></a>附錄 C：安裝 WebMatrix 2 和 iPhone 模擬器

若要在模擬的 iPhone 裝置中執行您的網站，您可以使用 WebMatrix 擴充功能 &quot;適用于 iPhone&quot;的電子行動模擬器。 此外，您可以設定相同的延伸模組，以從 Visual Studio 2012 執行模擬器。

<a id="ApxCTask1"></a>

<a id="Task_1_-_Installing_WebMatrix_2"></a>
#### <a name="task-1---installing-webmatrix-2"></a>工作 1-安裝 WebMatrix 2

1. 移至[[https://go.microsoft.com/?linkid=9809776](https://go.microsoft.com/?linkid=9809776)](https://go.microsoft.com/?linkid=9810169)。 或者，如果您已經安裝 Web Platform Installer，您可以開啟它，然後搜尋產品 &quot;*WebMatrix 2*&quot;。
2. 按一下 [**立即安裝**]。 如果您沒有**Web Platform Installer**系統會將您重新導向，先下載並安裝。
3. 開啟**Web Platform Installer**之後，請按一下 [**安裝**] 以啟動安裝程式。

    ![安裝 WebMatrix 2](whats-new-in-aspnet-mvc-4/_static/image49.png "安裝 WebMatrix 2")

    *安裝 WebMatrix 2*
4. 閱讀所有產品的授權和條款，然後按一下 [**我接受**] 繼續。

    ![接受授權條款](whats-new-in-aspnet-mvc-4/_static/image50.png "接受授權條款")

    *接受授權條款*
5. 等到下載和安裝程式完成為止。

    ![安裝進度](whats-new-in-aspnet-mvc-4/_static/image51.png "安裝進度")

    *安裝進度*
6. 當安裝完成時，按一下 **[完成]** 。

    ![安裝已完成](whats-new-in-aspnet-mvc-4/_static/image52.png "安裝已完成")

    *安裝已完成*
7. 按一下 **[** 結束] 以關閉 Web Platform Installer。

<a id="ApxCTask2"></a>

<a id="Task_2_-_Installing_the_iPhone_Simulator_Extension"></a>
#### <a name="task-2---installing-the-iphone-simulator-extension"></a>工作 2-安裝 iPhone 模擬器擴充功能

1. 執行**WebMatrix**並開啟任何現有的網站或建立新的網站。
2. 從 [**首頁**] 功能區按一下 [**執行**] 按鈕，然後選取 [**加入新**的]。

    ![正在新增 WebMatrix 擴充功能](whats-new-in-aspnet-mvc-4/_static/image53.png "正在新增 WebMatrix 擴充功能")

    *正在新增 WebMatrix 擴充功能*
3. 選取 [ **iPhone**模擬器]，然後按一下 [**安裝**]。

    ![流覽 WebMatrix 擴充功能](whats-new-in-aspnet-mvc-4/_static/image54.png "流覽 WebMatrix 擴充功能")

    *流覽 WebMatrix 擴充功能*
4. 在套件詳細資料中，按一下 [**安裝**] 以繼續安裝延伸模組。

    ![iPhone 模擬器擴充功能](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone 模擬器擴充功能")

    *iPhone 模擬器擴充功能*
5. 閱讀並接受延伸模組 EULA。

    ![WebMatrix 延伸模組 EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix 延伸模組 EULA")

    *WebMatrix 延伸模組 EULA*
6. 現在，您可以使用 iPhone 模擬器選項，從 WebMatrix 執行您的網站。

    ![使用 iPhone 執行](whats-new-in-aspnet-mvc-4/_static/image57.png "使用 iPhone 執行")

    *使用 iPhone 執行*

<a id="ApxCTask3"></a>

<a id="Task_3_-_Configuring_Visual_Studio_2012_to_run_iPhone_Simulator"></a>
#### <a name="task-3---configuring-visual-studio-2012-to-run-iphone-simulator"></a>工作 3-設定 Visual Studio 2012 來執行 iPhone 模擬器

1. 開啟**Visual Studio 2012**並開啟任何網站，或建立新的專案。
2. 按一下 [執行] 按鈕上的向下箭號，然後選取 **[流覽方式]** 。

    ![流覽方式](whats-new-in-aspnet-mvc-4/_static/image58.png "流覽方式")

    *流覽方式*
3. 在 [&quot;流覽&quot;] 對話方塊中，按一下 [**新增**]。
4. 在 [&quot;新增程式&quot;] 對話方塊中，使用下列值：

   - **程式**： C:\Users\*{CurrentUser} * \AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe *（據以更新路徑）*
   - **引數**： &quot;1&quot;
   - **易記名稱**： iPhone 模擬器

     ![新增程式](whats-new-in-aspnet-mvc-4/_static/image59.png "新增程式")

     *新增要流覽的程式*
5. 按一下 **[確定]** 並關閉對話方塊。
6. 現在您可以從 Visual Studio 2012，在 iPhone 模擬器中執行您的 Web 應用程式。

    ![使用 iPhone 模擬器流覽](whats-new-in-aspnet-mvc-4/_static/image60.png "使用 iPhone 模擬器流覽")

    *使用 iPhone 模擬器流覽*

<a id="AppendixD"></a>

<a id="Appendix_D_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-d-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>附錄 D：使用 Web Deploy 發行 ASP.NET MVC 4 應用程式

本附錄將告訴您如何從 Windows Azure 管理入口網站建立新的網站，以及如何發佈您在實驗室之後取得的應用程式，利用 Windows Azure 提供的 Web Deploy 發行功能。

<a id="ApxDTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>工作 1-從 Windows Azure 入口網站建立新的網站

1. 移至[Windows Azure 管理入口網站](https://manage.windowsazure.com/)並使用與您的訂用帳戶相關聯的 Microsoft 認證登入。

    > [!NOTE]
    > 有了 Windows Azure，您可以免費裝載10個 ASP.NET 網站，然後隨著流量的成長而調整。 您可以在[這裡](https://aka.ms/aspnet-hol-azure)註冊。

    ![登入 Windows Azure 入口網站](whats-new-in-aspnet-mvc-4/_static/image61.png "登入 Windows Azure 入口網站")

    *登入 Windows Azure 管理入口網站*
2. 按一下命令列上的 [**新增**]。

    ![建立新網站](whats-new-in-aspnet-mvc-4/_static/image62.png "建立新網站")

    *建立新網站*
3. 按一下 [**計算** | 的**網站**]。 然後選取 [**快速建立**] 選項。 提供新網站的可用 URL，然後按一下 [**建立網站**]。

    > [!NOTE]
    > Windows Azure 網站是在雲端中執行之 Web 應用程式的主機，您可以控制和管理。 [快速建立] 選項可讓您從入口網站外部，將已完成的 web 應用程式部署至 Windows Azure 網站。 它不包含設定資料庫的步驟。

    ![使用 [快速建立] 建立新的網站](whats-new-in-aspnet-mvc-4/_static/image63.png "使用 [快速建立] 建立新的網站")

    *使用 [快速建立] 建立新的網站*
4. 等到新**網站**建立完畢。
5. 建立網站之後，請按一下 [ **URL** ] 資料行下方的連結。 檢查新網站是否正常運作。

    ![流覽至新網站](whats-new-in-aspnet-mvc-4/_static/image64.png "流覽至新網站")

    *流覽至新網站*

    ![網站正在執行](whats-new-in-aspnet-mvc-4/_static/image65.png "網站正在執行")

    *網站正在執行*
6. 返回入口網站，然後按一下 [**名稱**] 欄底下的網站名稱，以顯示管理頁面。

    ![開啟網站管理頁面](whats-new-in-aspnet-mvc-4/_static/image66.png "開啟網站管理頁面")

    *開啟網站管理頁面*
7. 在 [**儀表板**] 頁面的 [**快速概覽**] 區段下，按一下 [**下載發行設定檔**] 連結。

    > [!NOTE]
    > *發行設定檔*包含將 web 應用程式發佈至 Windows Azure 網站所需的所有資訊，以供每個已啟用的發行方法使用。 發行設定檔包含 Url、使用者認證和資料庫字串，這些都是連接到已啟用發行方法的每個端點並進行驗證所需的。 **Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支援讀取發行設定檔，以將這些程式的設定自動化，以將 Web 應用程式發佈至 Windows Azure 網站。

    ![正在下載網站發行設定檔](whats-new-in-aspnet-mvc-4/_static/image67.png "正在下載網站發行設定檔")

    *正在下載網站發行設定檔*
8. 將發行設定檔下載到已知的位置。 在此練習中，您將瞭解如何使用此檔案，將 web 應用程式從 Visual Studio 發行至 Windows Azure 網站。

    ![儲存發行設定檔](whats-new-in-aspnet-mvc-4/_static/image68.png "正在儲存發行設定檔")

    *儲存發行設定檔*

<a id="ApxDTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>工作 2-設定資料庫伺服器

如果您的應用程式會使用 SQL Server 資料庫，您必須建立 SQL Database 伺服器。 如果您想要部署不使用 SQL Server 的簡單應用程式，您可能會略過這項工作。

1. 您將需要 SQL Database 伺服器來儲存應用程式資料庫。 您可以在 Windows Azure 管理入口網站的  **SQL 資料庫** | **伺服器** | **伺服器的儀表板**上，從您的訂用帳戶中查看 SQL Database 伺服器。 如果您沒有建立伺服器，可以使用命令列上的 [**新增**] 按鈕建立一個。 記下 [**伺服器名稱] 和 [URL]、[系統管理員登入名稱] 和 [密碼**]，因為您將在後續工作中使用它們。 請不要建立資料庫，因為它會在稍後的階段中建立。

    ![SQL Database Server 儀表板](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL Database Server 儀表板")

    *SQL Database Server 儀表板*
2. 在下一項工作中，您將會從 Visual Studio 測試資料庫連線，因此您必須在伺服器的**允許 IP 位址**清單中包含本機 IP 位址。 若要這麼做，請按一下 **設定**，從**目前的用戶端 IP 位址**中選取 IP 位址，並將它貼入 **起始 Ip 位址**] 和 [**結束 ip 位址**] 文字方塊，然後按一下 [![新增-用戶端-IP-位址-確定 按鈕](whats-new-in-aspnet-mvc-4/_static/image70.png) 按鈕。

    ![正在新增用戶端 IP 位址](whats-new-in-aspnet-mvc-4/_static/image71.png)

    *正在新增用戶端 IP 位址*
3. 將**用戶端 Ip 位址**新增至 [允許的 ip 位址] 清單之後，按一下 [**儲存**] 以確認變更。

    ![確認變更](whats-new-in-aspnet-mvc-4/_static/image72.png)

    *確認變更*

<a id="ApxDTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>工作 3-使用 Web Deploy 發行 ASP.NET MVC 4 應用程式

1. 返回 ASP.NET MVC 4 解決方案。 在 **方案總管**中，以滑鼠右鍵按一下 網站 專案，然後選取 **發佈**。

    ![發行應用程式](whats-new-in-aspnet-mvc-4/_static/image73.png "發行應用程式")

    *發行網站*
2. 匯入您在第一個工作中儲存的發行設定檔。

    ![匯入發行設定檔](whats-new-in-aspnet-mvc-4/_static/image74.png "匯入發行設定檔")

    *正在匯入發行設定檔*
3. 按一下 [**驗證連接**]。 驗證完成後，按 **[下一步]** 。

    > [!NOTE]
    > 當您看到 [驗證連線] 按鈕旁出現綠色核取記號時，驗證就會完成。

    ![正在驗證連接](whats-new-in-aspnet-mvc-4/_static/image75.png "正在驗證連接")

    *正在驗證連接*
4. 在 [**設定**] 頁面的 [**資料庫**] 區段底下，按一下資料庫連接的文字方塊旁邊的按鈕（也就是**DefaultConnection**）。

    ![Web deploy 設定](whats-new-in-aspnet-mvc-4/_static/image76.png "Web deploy 設定")

    *Web deploy 設定*
5. 設定資料庫連接，如下所示：

   - 在 [**伺服器名稱**] 中，使用*tcp：* prefix 輸入您的 SQL Database 伺服器 URL。
   - 在 [**使用者名稱**] 中，輸入您的伺服器管理員登入名稱。
   - 在 [**密碼**] 中輸入您的伺服器管理員登入密碼。
   - 輸入新的資料庫名稱，例如： *MVC4SampleDB*。

     ![正在設定目的地連接字串](whats-new-in-aspnet-mvc-4/_static/image77.png "正在設定目的地連接字串")

     *正在設定目的地連接字串*
6. 然後按一下 [確定]。 當系統提示您建立資料庫時，請按一下 **[是]** 。

    ![建立資料庫](whats-new-in-aspnet-mvc-4/_static/image78.png "建立資料庫字串")

    *建立資料庫*
7. 您將用來連接到 Windows Azure 中 SQL Database 的連接字串會顯示在 [預設連接] 文字方塊中。 然後按一下 [下一步]。

    ![指向 SQL Database 的連接字串](whats-new-in-aspnet-mvc-4/_static/image79.png "指向 SQL Database 的連接字串")

    *指向 SQL Database 的連接字串*
8. 在 [**預覽**] 頁面中，按一下 [**發佈**]。

    ![發行 web 應用程式](whats-new-in-aspnet-mvc-4/_static/image80.png "發行 web 應用程式")

    *發行 web 應用程式*
9. 發佈程式完成後，您的預設瀏覽器會開啟已發行的網站。

    ![發行至 Windows Azure 的應用程式](whats-new-in-aspnet-mvc-4/_static/image81.png "發行至 Windows Azure 的應用程式")

    *發行至 Windows Azure 的應用程式*
