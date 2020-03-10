---
uid: web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
title: 使用 Visual Studio 2012 中的 Page Inspector |Microsoft Docs
author: rick-anderson
description: 在這個實際操作的實驗室中，您將探索新工具，以尋找並修正 Visual Studio 中的網頁問題-Page Inspector。 Page Inspector 是一種新工具，其為 b。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 73232292-a5fe-4720-82a1-8f6553effd1f
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: f42b1be2697ba7d1145b3e334fe8f4ebf019cd12
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586251"
---
# <a name="using-page-inspector-in-visual-studio-2012"></a>在 Visual Studio 2012 中使用 Page Inspector

依[Web Camp 團隊](https://twitter.com/webcamps)

> 在這個實際操作的實驗室中，您將探索新工具，以尋找並修正 Visual Studio 中的網頁問題-Page Inspector。
> 
> Page Inspector 是新工具，可將瀏覽器診斷工具帶入 Visual Studio，並在瀏覽器、ASP.NET 和原始程式碼之間提供整合的體驗。 它會直接在 Visual Studio IDE 內呈現網頁（HTML、Web form、ASP.NET MVC 或網頁），並讓您檢查原始程式碼和所產生的輸出。 Page Inspector 可讓您輕鬆地分解網站、快速從頭開始建立頁面，並快速診斷問題。
> 
> 現今我們有一些 Web 架構，可即時建立彈性且可調整的網站，例如 ASP.NET MVC 和 WebForms。 另一方面，因為 IDE 不支援以範本為基礎的頁面和動態內容中的設計工具，所以在頁面上找出問題會比較困難。 因此，這些網站必須在瀏覽器中開啟，才能查看他們對使用者的外觀。
> 
> Web 開發人員使用外部工具來尋找在瀏覽器中定期執行的問題。 然後，它們會回到 IDE 並開始修正。 在 IDE 之間來回活動的瀏覽器和程式碼剖析工具可能沒有效率，而且有時候每次您想要重現問題時，都需要全新的部署和快取清理。
> 
> Page Inspector 在用戶端（瀏覽器工具）與伺服器（ASP.NET 和原始程式碼）之間建立 Web 開發的橋樑，方法是使用結合的一組功能結合兩個世界的優勢。
> 
> 使用 Page Inspector，您可以查看原始程式檔（包括伺服器端程式碼）中的哪些元素產生要在瀏覽器中轉譯的 HTML 標籤。 Page Inspector 也可讓您修改 CSS 屬性和 DOM 元素屬性，以查看立即反映在瀏覽器中的變更。
> 
> 這個實際操作實驗室將逐步引導您完成 Page Inspector 的功能，並示範如何使用它們來修正 Web 應用程式中的問題。 **此實驗室包含兩個使用類似流程但以不同技術為目標的練習。如果您是 ASP.NET MVC 開發人員，請遵循練習一，如果您是 WebForms 開發人員，請遵循練習二**。
> 
> 本實驗室將針對源資料夾中提供的範例 Web 應用程式套用次要變更，引導您完成先前所述的增強功能和新功能。
> 
> 所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可在[https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)取得。

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>目標

在此實際操作實驗室中，您將瞭解如何：

- 使用 Page Inspector 分解網站
- 使用 Page Inspector 檢查和預覽 CSS 樣式變更
- 使用 Page Inspector 偵測並修正網頁中的問題

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Prerequisites

您必須具有下列專案，才能完成此實驗室：

- 適用于 Web 或上層的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （如需有關如何安裝的指示，請參閱[附錄 A](#AppendixA) ）。
- Internet Explorer 9 或更新版本

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>練習

這個實際操作實驗室包含下列練習：

1. [練習1：在 ASP.NET MVC 專案中使用 Page Inspector](#Exercise1)
2. [練習2：在 WebForms 專案中使用 Page Inspector](#Exercise2)

> [!NOTE]
> 每個練習都附有一個起始解決方案，此方案位於練習的 [開始] 資料夾中，可讓您個別追蹤每個練習。 在練習的原始程式碼中，您也會找到一個包含 Visual Studio 解決方案的結束資料夾，其中含有完成對應練習中步驟所產生的程式碼。 如果您在進行此實際操作實驗室時需要其他協助，您可以使用這些解決方案做為指導方針。

完成此實驗室的預估時間： **30 分鐘**。

<a id="Exercise1"></a>

<a id="Exercise_1_Using_Page_Inspector_in_ASPNET_MVC_Projects"></a>
### <a name="exercise-1-using-page-inspector-in-aspnet-mvc-projects"></a>練習1：在 ASP.NET MVC 專案中使用 Page Inspector

在此練習中，您將瞭解如何使用**Page Inspector**來預覽和 DEBUG **ASP.NET MVC 4**解決方案。 首先，您將會在工具周圍執行簡短的膝上，以瞭解有助於 Web 偵錯工具的功能。 然後，您將會在包含樣式問題的網頁中工作。 您將瞭解如何使用 Page Inspector 來尋找產生問題的原始程式碼並加以修正。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a>工作 1-探索 Page Inspector

在這項工作中，您將瞭解如何在顯示相片圖庫的 ASP.NET MVC 4 專案內容中使用 Page Inspector。

1. 開啟位於**來源/Ex1-MVC4/開始/** 資料夾的 [**開始**] 解決方案。

   1. 在繼續之前，您必須先下載一些遺漏的 NuGet 套件。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
2. 在 方案總管中，尋找 **/Views/Home**專案資料夾底下的  **Index. cshtml** ，以滑鼠右鍵按一下它，然後**在 Page Inspector 中**選取 view。

    ![在 Page Inspector 中選取要預覽的檔案](using-page-inspector-in-visual-studio-2012/_static/image1.png "在 Page Inspector 中選取要預覽的檔案")

    *在 Page Inspector 中選取要預覽的檔案*
3. [Page Inspector] 視窗會顯示對應至您所選取之來源視圖的 */Home/Index* URL。

    ![第一個使用 PageInspector 的連絡人](using-page-inspector-in-visual-studio-2012/_static/image2.png)

    *第一個與 Page Inspector 的連絡人*

    Page Inspector 工具已整合到您的 Visual Studio 環境中。 偵測器包含一個內嵌的瀏覽器，以及強大的 HTML profiler。 請注意，您不需要執行解決方案來查看頁面的外觀。

    > [!NOTE]
    > 當 Page Inspector 瀏覽器的寬度小於已開啟頁面的寬度時，您將不會正確地看到此頁面。 如果發生這種情況，請調整 Page Inspector 的寬度。
4. 按一下 Page Inspector**中的 [** 檔案] 索引標籤。

    您會看到組成索引頁的所有原始程式檔。 這項功能有助於一眼地識別所有元素，特別是當您使用部分視圖和範本時。 請注意，如果您按一下連結，也可以開啟每個檔案。

    ![-Files-索引標籤](using-page-inspector-in-visual-studio-2012/_static/image3.png)

    *[檔案] 索引標籤*
5. 按一下位於索引標籤左側的**切換檢查模式** 按鈕。

    這項工具可讓您選取頁面的任何元素，並查看其 HTML 和 Razor 程式碼。

    ![切換-檢查模式-按鈕](using-page-inspector-in-visual-studio-2012/_static/image4.png)

    *切換檢查模式按鈕*
6. 在 Page Inspector 瀏覽器中，將滑鼠指標移到頁面元素上方。 當您將滑鼠指標移到所呈現頁面的任何部分上方時，會顯示專案類型，並在 [Visual Studio 編輯器] 中反白顯示對應的來源標記或程式碼。

    ![作用中的檢查模式](using-page-inspector-in-visual-studio-2012/_static/image5.png)

    *作用中的檢查模式*

    > [!NOTE]
    > 請勿將 [Page Inspector] 視窗最大化，否則您將無法看到顯示原始程式碼的 [預覽] 索引標籤。 如果您在 Page Inspector 中按一下最大化的專案，將會出現選取範圍的原始程式碼，但會隱藏 [Page Inspector] 視窗。

    如果您注意到**Index. cshtml**檔案，就會注意到產生所選項目的原始程式碼部分會反白顯示。 這項功能可協助編輯較長的原始程式檔，以提供直接且快速的方式來存取程式碼。

    ![檢查元素](using-page-inspector-in-visual-studio-2012/_static/image6.png)

    *檢查元素*
7. 按一下 [**切換檢查模式**] 按鈕（![選取 [html] 索引標籤，以顯示在 Page Inspector 瀏覽器中轉譯的 html 程式碼。](using-page-inspector-in-visual-studio-2012/_static/image7.png "選取 [HTML] 索引標籤，以顯示在 Page Inspector 瀏覽器中轉譯的 HTML 程式碼。") ）以停用游標。
8. 選取 [ **html** ] 索引標籤，以顯示在 Page Inspector 瀏覽器中轉譯的 html 程式碼。
9. 在 HTML 標籤中，找出具有 Koala 連結的清單專案，並加以選取。

    請注意，當您選取程式碼時，會在瀏覽器中自動反白顯示對應的輸出。 這項功能非常適合用來查看 HTML 區塊在頁面上的呈現方式。

    ![選取頁面中的 HTML 元素](using-page-inspector-in-visual-studio-2012/_static/image8.png "選取頁面中的 HTML 元素")

    *選取頁面中的 HTML 元素*
10. 按一下 [**切換檢查模式**] 按鈕以啟用*檢查模式*，然後按一下巡覽列。 在 HTML 程式碼右邊的 [樣式] 窗格中，您會看到一份清單，其中包含套用至所選元素的 CSS 樣式。

    > [!NOTE]
    > 由於標頭是網站配置的一部分，因此 Page Inspector 也會開啟 \_配置的 cshtml 檔案，並反白顯示受影響的程式碼區段。

    ![探索樣式](using-page-inspector-in-visual-studio-2012/_static/image9.png)

    *探索所選元素的樣式和原始檔*
11. 啟用切換檢查指標後，將滑鼠指標移到藍色的功能列下方，然後按一下半圓。

    ![選取元素](using-page-inspector-in-visual-studio-2012/_static/image10.png "選取元素")

    *選取元素*
12. 在 [樣式] 窗格中，找出 [**主要-內容**] 群組底下的 [**背景影像**] 專案。 **取消** **核取背景影像**，並查看發生什麼事。 您會注意到，瀏覽器會立即反映變更，並隱藏圓形。

    > [!NOTE]
    > 您在 [Page Inspector 樣式] 索引標籤上套用的變更不會影響原始樣式表單。 您可以視需要取消核取樣式或變更其值，但它們會在重新整理頁面之後還原。

    ![啟用和停用 CSS 樣式](using-page-inspector-in-visual-studio-2012/_static/image11.png "啟用和停用 CSS 樣式")

    *啟用和停用 CSS 樣式*
13. 現在，使用 [檢查] 模式按一下標頭上的 [**這裡的標誌**] 文字。
14. 在 [**樣式**] 索引標籤中，找出 [**網站-標題**] 群組底下的 [**字型大小**] CSS 屬性。 按兩下屬性值，並以**3 個 em**取代 2.3 em 值，然後按**enter**鍵。 請注意，標題看起來更大。

    ![變更 Page Inspector 中的 CSS 值](using-page-inspector-in-visual-studio-2012/_static/image12.png "變更 Page Inspector 中的 CSS 值")

    *變更 Page Inspector 中的 CSS 值*
15. 按一下位於 Page Inspector 右窗格中的 [**追蹤樣式**] 索引標籤。 這是一種替代方式，可查看套用至選取專案的所有樣式（依屬性名稱排序）。

    ![CSS 樣式追蹤](using-page-inspector-in-visual-studio-2012/_static/image13.png)

    *追蹤所選元素的 CSS 樣式*
16. Page Inspector 的另一項功能是 [版面配置] 窗格。 使用 [檢查] 模式，選取巡覽列，然後按一下右窗格中**的 [配置**] 索引標籤。 您會看到所選元素的確切大小，以及其位移、邊界、填補和框線大小。 請注意，您也可以從這個視圖中修改值。

    ![Page Inspector 中的元素版面配置](using-page-inspector-in-visual-studio-2012/_static/image14.png "Page Inspector 中的元素版面配置")

    *Page Inspector 中的元素版面配置*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a>工作 2-在相片圖庫中尋找和修正樣式問題

您要如何診斷舊版 Visual Studio 的網頁問題？ 您很可能熟悉在 Visual Studio IDE 外部執行的 web 偵錯工具，例如 Internet Explorer 開發人員工具或 Firebug。 瀏覽器只會瞭解 HTML、腳本和樣式，而基礎架構則會產生要轉譯的 HTML。 基於這個理由，您通常需要部署整個網站，以查看網頁的外觀。

當您想要在網站中偵測並修正問題時，您可能會遵循下列步驟：

1. 從 Visual Studio 執行解決方案，或在 web 伺服器上部署頁面。
2. 在瀏覽器中，開啟您使用的開發人員工具，或直接開啟原始程式碼和樣式，並嘗試符合問題。 若要尋找相關的檔案，您可以使用 [&quot;搜尋]&quot; 或 &quot;在 [檔案]&quot; [功能] 中，以樣式類別的名稱進行搜尋。
3. 一旦偵測到錯誤，請停止網頁瀏覽器和伺服器。
4. 清除瀏覽器快取。
5. 回到 Visual Studio 以套用修正程式。 重複所有要測試的步驟。

由於 ASP.NET MVC 4 中沒有實際的 WYSIWYG，因此在執行或部署 web 應用程式之後，大部分的樣式問題都會在稍後的階段中偵測到。 現在，有了 Page Inspector，就可以預覽任何頁面，而不需要執行解決方案。

在這項工作中，您將使用 Page inspector 並修正相片圖庫應用程式的某些問題。

1. 使用 Page Inspector，找出標頭左邊的**註冊**和**登入**連結。

    請注意，連結不會顯示在右邊的預期位置，而且會顯示為項目符號清單。 您現在會將連結向右對齊，並據以調整其樣式。

    ![尋找註冊和登入連結](using-page-inspector-in-visual-studio-2012/_static/image15.png "尋找註冊和登入連結")

    *尋找註冊和登入連結*
2. 選取 [切換檢查模式] 時，按一下 [註冊] 連結以開啟其程式碼，然後按一下 [關閉]，但不是 [開啟]。

    請注意，連結的原始程式碼位於 **\_loginpartial.html. cshtml**檔案中，而不是 \_的 Layout，也就是您可能會在第一次尋找的位置。 您已直接放在正確的來源檔案中。
3. 在 **樣式** 索引標籤中，找出並按一下  **\< 區段 > #login**專案，這是這些連結的 HTML 容器。

    請注意，在您按一下之後， **#login**樣式會自動置於 [**網站地圖**] 中。 此外，現在會反白顯示程式碼。

    ![選取 CSS 樣式](using-page-inspector-in-visual-studio-2012/_static/image16.png "選取 CSS 樣式")

    *選取 CSS 樣式*
4. 藉由移除開頭和結尾字元並儲存**網站 .css**檔案，取消反白顯示的程式碼中的**文字對齊**屬性。

    Page Inspector 知道組成目前頁面的所有不同檔案，而且它可以偵測到這些檔案中的任何變更。 當瀏覽器中目前的頁面未與來源檔案同步時，它就會對您發出警示。
5. 在 Page Inspector 瀏覽器中，按一下位於網址列下方的列以重載頁面。

    ![重載頁面](using-page-inspector-in-visual-studio-2012/_static/image17.png)

    *重載頁面*

    連結現在位於右方，但它們仍看起來像是項目符號清單。 現在，您將移除專案符號，並水準對齊連結。

    ![已更新頁面](using-page-inspector-in-visual-studio-2012/_static/image18.png)

    *已更新頁面*
6. 使用 檢查 模式，選取包含 &quot;暫存器&quot; 的任何 **&lt;li&gt;** 專案，然後 &quot;連結。&quot; 然後，按一下  **&lt; 區段&gt; #login**專案 來存取**樣式 .css**程式碼。

    ![尋找樣式](using-page-inspector-in-visual-studio-2012/_static/image19.png "尋找樣式")

    *尋找樣式*
7. 在**Style .css**中，將 **#login li**專案的程式碼取消批註。 您要新增的樣式將會隱藏專案符號，並以水準方式顯示專案。

    ![Restyling 登入連結](using-page-inspector-in-visual-studio-2012/_static/image20.png "Restyling 登入連結")

    *Restyling 登入連結*
8. 儲存**樣式 .css**檔案，然後在位址下方的列上按一下 [一次]，以重載頁面。 請注意，連結會正確顯示。

    ![對應至右側的連結](using-page-inspector-in-visual-studio-2012/_static/image21.png "對應至右側的連結")

    *對應至右側的連結*
9. 最後，您將變更標題標題。 使用 [檢查] 模式，在**這裡按一下您的標誌**，並取得產生此文字的原始程式碼。
10. 現在您已 **\_Layout**，請使用「**相片圖庫**」取代「**此處的標誌**」文字。 儲存並更新 Page Inspector 的瀏覽器。

    ![指派新的標題](using-page-inspector-in-visual-studio-2012/_static/image22.png "指派新的標題")

    *指派新的標題*

    ![[相片圖庫] 頁面](using-page-inspector-in-visual-studio-2012/_static/image23.png)

    *已更新相片圖庫頁面*
11. 最後，選取 [ **PhotoGallery** ] 專案，然後按**F5**以執行應用程式。 查看所有變更如預期般運作。

---

<a id="Exercise2"></a>

<a id="Exercise_2_Using_Page_Inspector_in_WebForms_Projects"></a>
### <a name="exercise-2-using-page-inspector-in-webforms-projects"></a>練習2：在 WebForms 專案中使用 Page Inspector

在此練習中，您將瞭解如何使用 Page Inspector 來預覽和偵測 WebForms 解決方案。 您會先執行工具的簡短膝上，以瞭解有助於 Web 偵錯工具的 Page Inspector 功能。 然後，您將會在包含樣式問題的網頁中工作。 您將瞭解如何使用 Page Inspector 來尋找產生問題的原始程式碼並加以修正。

<a id="Ex2Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a>工作 1-探索 Page Inspector

在這項工作中，您將學習如何在顯示相片圖庫的 WebForms 專案內容中，使用 Page Inspector 功能。

1. 開啟位於**來源/Ex2-WebForms/開始/** 資料夾的 [**開始**] 解決方案。

   1. 在繼續之前，您必須先下載一些遺漏的 NuGet 套件。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
2. 在 方案總管中，找出**default.aspx**頁面，以滑鼠右鍵按一下它，然後選取 **在 Page Inspector 中查看**。

    ![使用 Page Inspector 開啟 default.aspx](using-page-inspector-in-visual-studio-2012/_static/image24.png "使用 Page Inspector 開啟 default.aspx")

    *使用 Page Inspector 開啟 default.aspx*
3. [Page Inspector] 視窗會顯示 default.aspx。

    ![在 Page Inspector 中查看 default.aspx](using-page-inspector-in-visual-studio-2012/_static/image25.png "在 Page Inspector 中查看 default.aspx")

    *在 Page Inspector 中查看 default.aspx*

    Page Inspector 工具已整合到您的 Visual Studio 環境中。 偵測器包含內嵌的瀏覽器，以及會顯示所選程式碼的強大 HTML profiler。 請注意，您不需要執行解決方案來查看頁面的外觀。

    > [!NOTE]
    > 當 Page Inspector 瀏覽器的寬度小於已開啟頁面的寬度時，您將不會正確地看到此頁面。 如果發生這種情況，請調整 Page Inspector 的寬度。
4. 按一下 Page Inspector**中的 [** 檔案] 索引標籤。

    您會看到所有撰寫呈現之預設頁面的原始程式檔。 這是一種很有用的功能，可以一目了然地識別所有的元素，特別是當您使用使用者控制項和主版頁面時。 請注意，您也可以流覽至每個檔案。

    ![[檔案] 索引標籤](using-page-inspector-in-visual-studio-2012/_static/image26.png "[檔案] 索引標籤")

    *[檔案] 索引標籤*
5. 按一下位於索引標籤左側的**切換檢查模式** 按鈕。

    這項工具可讓您選取頁面的任何元素，並查看其 HTML 程式碼和 .aspx 來源。

    ![切換檢查模式按鈕](using-page-inspector-in-visual-studio-2012/_static/image27.png "切換檢查模式按鈕")

    *切換檢查模式按鈕*
6. 在 Page Inspector 瀏覽器中，將滑鼠指標移到頁面元素上方。 當您將滑鼠指標移到所呈現頁面的任何部分上方時，會顯示專案類型，並在 [Visual Studio 編輯器] 中反白顯示對應的來源標記或程式碼。

    ![作用中的檢查模式](using-page-inspector-in-visual-studio-2012/_static/image28.png "作用中的檢查模式")

    *作用中的檢查模式*

    > [!NOTE]
    > 請勿將 [Page Inspector] 視窗最大化，否則您將無法看到顯示原始程式碼的 [預覽] 索引標籤。 如果您在 Page Inspector 中按一下最大化的專案，將會出現選取範圍的原始程式碼，但會隱藏 [Page Inspector] 視窗。

    如果您注意到**default.aspx**檔案，就會注意到產生所選項目的原始程式碼部分會反白顯示。 這項功能可協助較長的來源檔案版本，並提供直接且快速的方式來存取程式碼。

    ![檢查元素](using-page-inspector-in-visual-studio-2012/_static/image29.png "檢查元素")

    *檢查元素*
7. 按一下 [**切換檢查模式**] 按鈕（![選取-html](using-page-inspector-in-visual-studio-2012/_static/image30.png "選取-HTML---------------------------------------") --------------------------------------- ），位於 Page Inspector 索引標籤中，以停用游標。
8. 選取 [ **html** ] 索引標籤，以顯示在 Page Inspector 瀏覽器中轉譯的 html 程式碼。
9. 在 HTML 程式碼中，找出具有 Koala 連結的清單專案，並加以選取。

    請注意，當您選取程式碼時，對應的輸出會自動反白顯示在瀏覽器中。 這項功能非常適合用來查看 HTML 區塊在頁面上的呈現方式。

    ![選取頁面中的 HTML 元素](using-page-inspector-in-visual-studio-2012/_static/image31.png "選取頁面中的 HTML 元素")

    *選取頁面中的 HTML 元素*
10. 按一下 [**切換檢查模式**] 按鈕以啟用*檢查模式*，然後按一下巡覽列。 在 HTML 程式碼右邊的 [樣式] 窗格中，您會看到一份清單，其中包含套用至所選元素的 CSS 樣式。

    > [!NOTE]
    > 由於標頭是網站配置的一部分，因此 Page Inspector 也會開啟網站檔案，並反白顯示受影響的程式碼區段。

    ![探索樣式 WebForms](using-page-inspector-in-visual-studio-2012/_static/image32.png "探索所選元素的樣式和原始檔")

    *探索所選元素的樣式和原始檔*
11. 啟用切換檢查指標後，將滑鼠指標移至功能表列下方，然後按一下空白的半圓。

    ![選取元素](using-page-inspector-in-visual-studio-2012/_static/image33.png "選取元素")

    *選取元素*
12. 在 [樣式] 窗格中，找出 [**主要-內容**] 群組底下的 [**背景影像**] 專案。 **取消** **核取背景影像**，並查看發生什麼事。 您會注意到，瀏覽器會立即反映變更，並隱藏圓形。

    > [!NOTE]
    > 您在 [Page Inspector 樣式] 索引標籤上套用的變更不會影響原始樣式表單。 您可以視需要取消核取樣式或變更其值，但它們會在重新整理頁面之後還原。

    ![啟用和停用 CSS styles2](using-page-inspector-in-visual-studio-2012/_static/image34.png "啟用和停用 CSS 樣式")

    *啟用和停用 CSS 樣式*
13. 現在，使用 [檢查] 模式按一下標頭上的 [這裡**的** **標誌**] 文字。
14. 在 [**樣式**] 索引標籤中，找出 [**網站-標題**] 群組底下的 [**字型大小**] CSS 屬性。 按兩下屬性一次以編輯其值。 以**3em**取代 2.3 em 值，然後按 enter。 請注意，標題看起來更大。

    ![變更頁面 Inspector2 中的 CSS 值](using-page-inspector-in-visual-studio-2012/_static/image35.png "變更 Page Inspector 中的 CSS 值")

    *變更 Page Inspector 中的 CSS 值*
15. 按一下位於 Page Inspector 右窗格中的 [**追蹤樣式**] 索引標籤。 這是一種替代方式，可查看套用至選取專案的所有樣式（依屬性名稱排序）。

    ![追蹤所選元素的 CSS 樣式](using-page-inspector-in-visual-studio-2012/_static/image36.png "追蹤所選元素的 CSS 樣式")

    *追蹤所選元素的 CSS 樣式*
16. Page Inspector 的另一項功能是 [版面配置] 窗格。 使用 [檢查] 模式，選取巡覽列，然後按一下右窗格中**的 [配置**] 索引標籤。 您會看到所選元素的確切大小，以及其位移、邊界、填補和框線大小。 請注意，您也可以從這個視圖中修改值。

    ![Page Inspector 中的元素版面配置](using-page-inspector-in-visual-studio-2012/_static/image37.png "Page Inspector 中的元素版面配置")

    *Page Inspector 中的元素版面配置*

<a id="Ex2Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a>工作 2-在相片圖庫中尋找和修正樣式問題

您要如何診斷舊版 Visual Studio 的網頁問題？ 您很可能熟悉在 Visual Studio IDE 外部執行的 web 偵錯工具，例如 Internet Explorer 開發人員工具或 Firebug。 瀏覽器只會瞭解 HTML、腳本和樣式，而基礎架構則會產生要轉譯的 HTML。 基於這個理由，您通常需要部署整個網站，以查看網頁的外觀。

當您想要在網站中偵測並修正問題時，您可能會遵循下列步驟：

1. 從 Visual Studio 執行解決方案，或在 web 伺服器上部署頁面。
2. 在瀏覽器中，開啟您使用的開發人員工具，或直接開啟原始程式碼和樣式，並嘗試符合問題。 若要尋找相關的檔案，您可以使用 [&quot;搜尋]&quot; 或 &quot;在 [檔案]&quot; [功能] 中搜尋樣式類別的名稱。
3. 一旦偵測到錯誤，請停止網頁瀏覽器和伺服器。
4. 清除瀏覽器快取。
5. 回到 Visual Studio 以套用修正程式。 重複所有要測試的步驟。

由於 ASP.NET WebForms 中沒有實際的 WYSIWYG，因此在執行或部署之後，會在後續階段偵測到某些樣式問題。 現在，有了 Page Inspector，就可以預覽任何頁面，而不需要執行解決方案。

在這項工作中，您將使用 Page inspector 來修正相片圖庫應用程式的某些問題。 在下列步驟中，您將在標頭中偵測並快速修正一些簡單的樣式問題。

1. 使用頁面檢查，找出標頭左邊的**註冊**和**登入**連結。

    請注意，此連結不會顯示在右邊的預期位置。 您現在會將連結對齊右邊，並據以調整其樣式。

    ![位於左側的 [登入] 連結](using-page-inspector-in-visual-studio-2012/_static/image38.png "位於左側的 [登入] 連結")

    *位於左側的 [登入] 連結*
2. 選取 [切換檢查模式] 後，選取 [登入] 連結以開啟其程式碼。

    請注意，連結原始程式碼位於**網站**檔案中，而不是預設的 .aspx 頁面中，這是您可能會看到的位置;您已直接放在正確的來源檔案中。
3. 在 **樣式** 索引標籤中，找出並按一下  **&lt; 區段&gt; #login**專案，這是這些連結的 HTML 容器。

    請注意，在您按一下之後， **#login**樣式會自動置於 [**網站地圖**] 中。 此外，現在會反白顯示程式碼。

    ![選取 CSS 樣式](using-page-inspector-in-visual-studio-2012/_static/image39.png "選取 CSS 樣式")

    *選取 CSS 樣式*
4. 藉由移除開頭和結尾字元並儲存**網站 .css**檔案，取消反白顯示的程式碼中的**文字對齊**屬性。

    Page Inspector 知道組成目前頁面的所有不同檔案，而且它可以偵測到這些檔案中的任何變更。 當瀏覽器中目前的頁面未與來源檔案同步時，它就會對您發出警示。
5. 在 Page Inspector 瀏覽器中，按一下位於網址列下方的列，以儲存變更並重載頁面。

    ![重載頁面](using-page-inspector-in-visual-studio-2012/_static/image40.png)

    *重載頁面*

    連結現在位於右方，但它們仍看起來像是項目符號清單。 現在，您將移除專案符號，並水準對齊連結。

    ![已更新頁面](using-page-inspector-in-visual-studio-2012/_static/image41.png)

    *已更新頁面*
6. 使用 檢查 模式，選取包含 &quot;暫存器&quot; 的任何 **&lt;li&gt;** 專案，然後 &quot;連結。&quot; 然後，按一下  **&lt; 區段&gt; #login**專案 來存取**樣式 .css**程式碼。

    ![尋找樣式](using-page-inspector-in-visual-studio-2012/_static/image42.png "尋找樣式")

    *尋找樣式*
7. 在**Style .css**中，將 **#login li**專案的程式碼取消批註。 您要新增的樣式將會隱藏專案符號，並以水準方式顯示專案。

    ![Restyling 登入連結](using-page-inspector-in-visual-studio-2012/_static/image43.png "Restyling 登入連結")

    *Restyling 登入連結*
8. 儲存**樣式 .css**檔案，然後在位址下方的列上按一下 [一次]，以重載頁面。 請注意，連結會正確顯示。

    ![對應至右側的連結](using-page-inspector-in-visual-studio-2012/_static/image44.png "對應至右側的連結")

    *對應至右側的連結*
9. 最後，您將變更標題標題。 不是在所有檔案中搜尋「**此處的標誌**」文字，而是使用 [檢查] 模式來按一下文字，然後取得產生它的原始碼。

    ![尋找網站標題](using-page-inspector-in-visual-studio-2012/_static/image45.png "尋找網站標題")

    *尋找網站標題*
10. 現在您已在**網站**中，使用 [**相片圖庫**] 取代 [**您的標誌這裡**] 文字。 儲存並更新 Page Inspector 的瀏覽器。

    ![已更新相片圖庫頁面](using-page-inspector-in-visual-studio-2012/_static/image46.png "已更新相片圖庫頁面")

    *已更新相片圖庫頁面*
11. 最後按**F5**鍵執行應用程式，查看所有變更如預期般運作。

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>總結

藉由完成這個實際操作實驗室，您就可以學會如何使用 Page Inspector 來預覽您的 Web 應用程式，而不需要在瀏覽器中重建和執行網站。 此外，您還學會如何藉由從轉譯的輸出直接存取原始程式碼，快速尋找並修正 bug。

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附錄 A：安裝 Web 的 Visual Studio Express 2012

您可以使用 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** 安裝 Web 或另一個 &quot;Express&quot; 版本**的 Microsoft Visual Studio Express 2012** 。 下列指示會引導您完成使用*Microsoft Web Platform Installer*安裝*Visual studio Express 2012 for Web*所需的步驟。

1. 移至[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。 或者，如果您已經安裝 Web Platform Installer，您可以開啟它，然後使用 Windows Azure SDK&quot;來搜尋產品 &quot;<em>Visual Studio Express 2012 For Web</em> 。
2. 按一下 [**立即安裝**]。 如果您沒有**Web Platform Installer**系統會將您重新導向，先下載並安裝。
3. 開啟**Web Platform Installer**之後，請按一下 [**安裝**] 以啟動安裝程式。

    ![安裝 Visual Studio Express](using-page-inspector-in-visual-studio-2012/_static/image47.png "安裝 Visual Studio Express")

    *安裝 Visual Studio Express*
4. 閱讀所有產品的授權和條款，然後按一下 [**我接受**] 繼續。

    ![接受授權條款](using-page-inspector-in-visual-studio-2012/_static/image48.png)

    *接受授權條款*
5. 等到下載和安裝程式完成為止。

    ![安裝進度](using-page-inspector-in-visual-studio-2012/_static/image49.png)

    *安裝進度*
6. 當安裝完成時，按一下 **[完成]** 。

    ![安裝已完成](using-page-inspector-in-visual-studio-2012/_static/image50.png)

    *安裝已完成*
7. 按一下 **[** 結束] 以關閉 Web Platform Installer。
8. 若要開啟 Web Visual Studio Express，請移至 [**開始**] 畫面，然後開始撰寫 &quot;**VS Express**&quot;，然後按一下 [ **VS Express for Web** ] 磚。

    ![VS Express for Web 磚](using-page-inspector-in-visual-studio-2012/_static/image51.png)

    *VS Express for Web 磚*
