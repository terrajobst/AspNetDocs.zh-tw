---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
title: Visual Studio 2012 中 ASP.NET 和 Web 程式開發的新功能 |Microsoft Docs
author: rick-anderson
description: 新版本的 Visual Studio 引進了一些增強功能，著重于改善使用 Web 技術時的體驗和效能 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 6d40d276-1642-4a77-b6c9-02ac914f6805
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 80c77ec65ed86b06e417d3f6ba608e404c46768b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525932"
---
# <a name="whats-new-in-aspnet-and-web-development-in-visual-studio-2012"></a>Visual Studio 2012 中的 ASP.NET 和網頁程式開發的新功能

依[Web Camp 團隊](https://twitter.com/webcamps)

> 新版本的 Visual Studio 引進了許多增強功能，著重于改善使用 Web 技術時的體驗和效能。 CSS 的 Visual Studio 編輯器、JavaScript 和 HTML 已完全改頭換面，以包含許多最隨選的程式碼輔助，例如 IntelliSense 和自動縮排。 關於效能、組合和縮制現在已整合為內建功能，可輕鬆地減少頁面載入時間。
> 
> Visual Studio 可讓您使用最新的網站技術。 您可以使用跨瀏覽器 CSS3 程式碼片段，確保您的網站無論用戶端平臺如何運作，同時也會利用新的 HTML5 元素和功能。
> 
> 使用此 Visual Studio 版本，撰寫和分析 JavaScript 程式碼應該更容易。 IntelliSense 清單、整合式 XML 檔和導覽功能現在可供 JavaScript 程式碼使用。 您現在可以輕鬆地擁有 JavaScript 目錄。 此外，您可以檢查 ECMAScript5 是否符合您的腳本，並在早期階段偵測語法錯誤。
> 
> 最後，這個 Visual Studio 版本會執行內建的組合和縮制。 您的腳本檔案和樣式表單將會進行封裝和壓縮，讓網站執行的速度更快。
> 
> 本實驗室將針對源資料夾中提供的範例 Web 應用程式套用次要變更，引導您完成先前所述的增強功能和新功能。
> 
> 所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可在[https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)取得。

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>目標

在此實習實驗室中，您將瞭解如何：

- 使用 CSS 編輯器中的新功能和改進
- 使用 HTML 編輯器中的新功能和改進
- 使用 JavaScript 編輯器的新功能和改進
- 設定及使用配套和縮制

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Prerequisites

- 適用于 Web 或上層的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （如需有關如何安裝的指示，請參閱[附錄 A](#AppendixA) ）。
- [Windows PowerShell](https://support.microsoft.com/kb/968930/) （適用于安裝腳本-已安裝在 windows 8 和 windows Server 2008 R2 上）
- [Internet Explorer 10](https://windows.microsoft.com/internet-explorer/products/ie/home)或符合 HTML5 的瀏覽器

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>練習

這堂實習實驗室包含下列練習：

1. [練習1： CSS 編輯器的新功能](#Exercise1)
2. [練習2： HTML 編輯器的新功能](#Exercise2)
3. [練習3： JavaScript 編輯器的新功能](#Exercise3)
4. [練習4：捆綁和縮制](#Exercise4)

完成此實驗室的預估時間： **60 分鐘**。

<a id="Exercise1"></a>

<a id="Exercise_1_Whats_New_in_the_CSS_Editor"></a>
### <a name="exercise-1-whats-new-in-the-css-editor"></a>練習1： CSS 編輯器的新功能

Web 開發人員應該很熟悉與 CSS 編輯相關的許多困難之處。 CSS 樣式的最大問題之一，就是跨瀏覽器的相容性。 通常會發生這種情況，在將樣式套用至您的網站之後，您會注意到，如果您在另一個瀏覽器或裝置中開啟，它看起來會不同。 因此，您可能會花相當長的時間來修正這些視覺問題，以瞭解當您最後讓它在一個瀏覽器中工作時，它會在其他人中中斷。

Visual Studio 現在包含可協助開發人員有效率地存取、工作及組織 CSS 樣式表單的功能。 在此練習中，您將會符合有效組織和版本的新功能，以及跨瀏覽器相容性的 CSS3 程式碼片段。

<a id="Ex1Task1"></a>

<a id="Task_1_-_New_Editor_Features"></a>
#### <a name="task-1---new-editor-features"></a>工作 1-新編輯器功能

在這項工作中，您將探索 CSS 編輯器的新功能。 這個新的編輯器將利用新的智慧型縮排、改良的程式碼批註和增強的 IntelliSense 清單，協助您提高生產力。

1. 啟動**Visual Studio** ，然後開啟位於此實驗室的**Source\WhatsNewASPNET**資料夾中的 [ **WhatsNewASPNET** ] 方案。
2. 在方案總管中，開啟位於 [**樣式**] 資料夾底下的 [ **.css** ] 檔案。 請確定 [**文字編輯器**] 工具顯示在工具列上。 若要這麼做，請選取 [ **View** | **工具列**] 功能表選項，然後勾選 [**文字編輯器**] 選項。 您會注意到，自這個新版本起，[**批註**] 按鈕（![的 [批註] 按鈕](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image1.png)）和 [**取消**批註] 按鈕（![[取消批註] 按鈕](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image2.png)）也會針對 CSS 編輯器啟用。

    ![啟用編輯器和 CSS 工具](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image3.png "啟用編輯器和 CSS 工具")

    *啟用編輯器和 CSS 工具*
3. 請滾動程式碼，然後選取任何 CSS 類別定義。 按一下 **批註** \ （![批註按鈕](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image4.png)） 按鈕，以批註選取的行。 然後，按一下 **取消**批註 （![取消批註 按鈕](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image5.png)）按鈕來復原變更。
4. 按一下折**迭（![** 折迭](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image6.png)），然後**展開**（![展開 [](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image7.png)]）按鈕，其位於文字的左邊界。 請注意，您現在可以隱藏不會使用的樣式以讓您擁有更整潔的觀點。

    ![折迭 CSS 類別](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image8.png "折迭 CSS 類別")

    *折迭 CSS 類別*
5. 請確定已啟用 [智慧型縮排] 功能。 選取 **工具** | **選項** 功能表選項，然後在畫面的左窗格中選取 **文字編輯器** |  **CSS** | **格式** 頁面。 選取 [**階層式縮排**] 選項。

    ![啟用階層式縮排](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image9.png "啟用階層式縮排")

    *啟用階層式縮排*
6. 找出主要類別定義（main），並將樣式附加至 div 元素。 您會發現程式碼會自動對齊，協助使用者一目了然地尋找父類別。

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample1.css)]

    ![CSS 中的階層對齊](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image10.png "CSS 中的階層對齊")

    *CSS 中的階層對齊*
7. 在 [**主要 div** ] 類別內，找出框線結尾處的游標 **： 0px;** 然後按**enter**以顯示 IntelliSense 清單。 開始輸入**top** ，並注意清單在您輸入時的篩選方式。 此清單會顯示在單字的任何部分包含**頂端**的元素（在舊版的 Visual Studio 中，清單會依*以詞彙開頭*的專案進行篩選）。

    ![CSS 中的 IntelliSense 增強功能](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image11.png "CSS 中的 IntelliSense 增強功能")

    *CSS 中的 IntelliSense 增強功能*

<a id="Ex1Task2"></a>

<a id="Task_2_-_The_Color_Picker"></a>
#### <a name="task-2---the-color-picker"></a>工作 2-色彩選擇器

在這項工作中，您會發現整合到 Visual Studio IntelliSense 的新 CSS 色彩選擇器。

1. 在 .css 中 **，** 找出標頭類別定義（. header），並將游標放在 **背景色彩**屬性 旁，在 &quot;：&quot; 和 &quot;#&quot; 該程式程式碼的字元之間 **。**

    ![尋找游標](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image12.png "尋找游標")

    *尋找游標*
2. 刪除**冒號**（:)然後再寫一次，以顯示色彩選擇器。 請注意，您會看到的第一種色彩是最常用的網站色彩。 如果您按一下白色色彩，其 HTML 色彩代碼（#fff）將會取代樣式表單中目前的色彩代碼。

    ![色彩選擇器](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image13.png "色彩選擇器")

    *色彩選擇器*
3. 按下色彩選擇器上的 [**展開**（![com](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image14.png)）] 按鈕，以顯示色彩漸層，然後拖曳漸層游標來選取不同的色彩。 之後，請按一下 [**滴管**] 按鈕，然後從螢幕中選取任何色彩。 請注意，當您移動游標時，背景色彩值會動態變更。

    ![色彩選擇器漸層](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image15.png "色彩選擇器漸層")

    *色彩選擇器漸層*
4. 在 [**不透明度**] 滑杆中，將選取器移至橫條的中央，以減少不透明度。 請注意，[背景色彩] 值現在會將其縮放比例變更為 RGBA。

    ![色彩選擇器不透明度](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image16.png "色彩選擇器不透明度")

    *色彩選擇器不透明度*

    > [!NOTE]
    > CSS3 中的 RGBA （紅色、綠色、藍色、Alpha）色彩定義，可讓您定義單一專案的色彩不透明度值。 不同于**不透明度-** 類似的 CSS 屬性 **-** RGBA 色彩也會與最新的瀏覽器相容。

<a id="Ex1Task3"></a>

<a id="Task_3_-_CSS_Compatible_Code_Snippets"></a>
#### <a name="task-3---css-compatible-code-snippets"></a>工作 3-CSS 相容程式碼片段

在這項工作中，您將瞭解如何使用跨瀏覽器相容的 CSS3 程式碼片段，以在您的網站中執行一些功能。

1. 在 [ **.css** ] 檔案中，找出**標頭**css 類別定義（. header），並將游標放在 [ **/\*框線半徑\*/** 預留位置] 下方，以加入新的程式碼片段。 按**enter**以顯示 IntelliSense 清單並輸入**radius**以篩選清單。 選取清單中的 [**框線-半徑**] 選項，並按兩下，然後按下**tab**鍵以插入程式碼片段。 然後，輸入以圖元為單位的 radius 大小，然後按**enter**鍵。 例如，輸入**15px**。

    程式碼片段所新增的 CSS3 屬性會在大部分的 HTML5 合規性瀏覽器中轉譯圓角框線，包括 Mozilla 和 WebKit 為基礎的瀏覽器。

    ![使用框線-radius 程式碼片段](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image17.png "使用框線-radius 程式碼片段")

    *使用框線-radius 程式碼片段*
2. 將相同的**框線**程式碼片段套用到頁面樣式（. page）。

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample2.css)]
3. 按 **F5** 執行方案。 請注意，每個頁面現在都有圓角框線。

    ![圓角](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image18.png "圓角")

    *圓角*
4. 關閉瀏覽器並返回 Visual Studio。
5. 開啟位於 [**樣式**] 資料夾底下的**自訂 .css**檔案，並將游標放在 [div] 中 **。**
6. 按 enter 以顯示 [IntelliSense] 清單、輸入**box-陰影**，然後按兩次**tab**鍵，將預設的陰影程式碼片段插入類別定義內。 將陰影值設定為**10px 10px 5px #888**。 然後，輸入**框線半徑**，並插入程式碼片段。 輸入**15px**以設定 radius 大小，然後按**enter**。

    ![具有陰影的圓角](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image19.png "具有陰影的圓角")

    *具有陰影的圓角*

    > [!NOTE]
    > 此時，陰影屬性會以對應的前置詞（moz-appearance、webkit、o）插入，以支援 Mozilla 和 Webkit （Chrome、Safari、Konkeror）瀏覽器。
7. 建立新的類別**div。影像 ul li img：將滑鼠停留**在**div. images u l i m g**類別定義底下，並將游標放在方括弧內 **。**

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample3.css)]
8. 輸入**轉換**，並按兩次**tab**鍵以插入轉換程式碼片段。 然後，輸入**旋轉（-15deg）** ，以在影像暫留時變更旋轉角度值。

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample4.css)]
9. 按**F5**執行方案，並流覽至 [CSS3] 頁面。 請注意，影像具有圓角和方塊陰影。 將滑鼠停留在影像上，並觀賞它們旋轉。

    ![旋轉影像的轉換程式碼片段](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image20.png "旋轉影像的轉換程式碼片段")

    *旋轉影像的轉換程式碼片段*

    > [!NOTE]
    > 如果您使用的是 Internet Explorer 10，而且看不到陰影，請確定 [檔案模式] 設定為 [IE10 標準]。 按**F12**開啟 Internet Explorer 開發人員工具，然後按一下 [**檔案模式]** 變更為 IE10 標準。

    ![關於-us](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image21.png)

<a id="Exercise2"></a>

<a id="Exercise_2_Whats_New_in_the_HTML_Editor"></a>
### <a name="exercise-2-whats-new-in-the-html-editor"></a>練習2： HTML 編輯器的新功能

Visual Studio 具有改良的 HTML 編輯器。 此版本中包含的一些增強功能包括 HTML 檔案中的智慧型縮排、HTML5 程式碼片段、HTML 開始和結束標記比對，以及 HTML 驗證。 在此練習中，您將會在網站標記中工作時，看到這些變更如何改善您的順暢。

如同 CSS 編輯器，HTML 編輯器也已經過改善。 這些改良功能大多是讓 Web 開發人員的生活變得更簡單的小部分。 針對 HTML 檔案 DOCTYPE 進行編輯和驗證時，像是 HTML5、智慧型縮排、比對開始和結束標記等更多程式碼片段的專案，就是其中一些改良功能。

<a id="Ex2Task1"></a>

<a id="Task_1_-_Improved_DOCTYPE_Validation"></a>
#### <a name="task-1---improved-doctype-validation"></a>工作 1-改良的 DOCTYPE 驗證

HTML 編輯器現在可以檢查頁面的 DOCTYPE，即使定義可能在主版頁面中也一樣。 根據頁面的 DOCTYPE，HTML 編輯器會使用正確的規則集進行驗證，並會篩選 IntelliSense 清單並考慮 DOCTYPE 元素。

在這項工作中，您將變更頁面的 DOCTYPE，以查看 HTML 編輯器的行為如何隨之變更。

1. 如果尚未開啟，請啟動**Visual Studio** ，然後開啟位於此實驗室的**Source\WhatsNewASPNET**資料夾中的**WhatsNewASPNET。**
2. 開啟 [**網站**] 頁面。
3. 請注意 [驗證] 工具列的 [目標架構]。 HTML 編輯器的運作方式（驗證、IntelliSense 等等）會適當地變更，以符合所選的 Doctype。

    ![在 HTML 原始檔編輯工具列中使用 Doctype](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image22.png "在 HTML 原始檔編輯工具列中使用 Doctype")

    *在 HTML 原始檔編輯工具列中使用 Doctype*
4. 將目標架構變更為 HTML 4.01。

    ![在 HTML 原始檔編輯工具列中變更 Doctype](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image23.png "在 HTML 原始檔編輯工具列中變更 Doctype")

    *在 HTML 原始檔編輯工具列中變更 Doctype*
5. 將游標放在**body**元素底下，然後開始輸入 HTML5 元素的名稱（例如**影片**）。 請注意，[IntelliSense] 清單中不提供此元素。

    ![未列出 HTML5 元素](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image24.png "未列出 HTML5 元素")

    *未列出 HTML5 元素*
6. 復原 [驗證] 工具列之 [目標架構] 的變更，並從下拉式清單中挑選 [DOCTYPE： XHTML5]。

    ![在 HTML 原始檔編輯工具列中使用 Doctype](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image25.png "在 HTML 原始檔編輯工具列中使用 Doctype")

    *在 HTML 原始檔編輯工具列中重設 Doctype*
7. 將游標放在**body**元素底下，然後再次開始輸入 HTML5 元素（例如，像是**影片**）。 請注意，HTML5 元素現在可以在 IntelliSense 清單中取得。

    ![列出的 HTML5 元素](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image26.png "列出的 HTML5 元素")

    *列出的 HTML5 元素*

<a id="Ex2Task2"></a>

<a id="Task_2_-_StartEnd_Tags_Automatic_Update"></a>
#### <a name="task-2---startend-tags-automatic-update"></a>工作 2-開始/結束標記自動更新

Visual Studio 現在會更新您正在編輯之專案的 HTML 開頭或結束記號，使兩者彼此相符。 這項新功能可改善您編輯 HTML 標籤時的生產力。

1. 在**default.aspx**頁面上，新增包含標題的**H3**元素（例如，Visual Studio 2012 Rocks！）。

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample5.aspx)]
2. 變更**H3**標記並輸入**H2**或**H1。**

    請注意，結束標記會自動更新。 您也可以修改結束標記，以查看啟動標記也會一併更新。

    ![結束標記的自動更新](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image27.png "結束標記的自動更新")

    *結束標記的自動更新*

<a id="Ex2Task3"></a>

<a id="Task_3_-_New_HTML5_Code_Snippets"></a>
#### <a name="task-3---new-html5-code-snippets"></a>工作 3-新的 HTML5 程式碼片段

Visual Studio 現在包含數個 HTML5 程式碼片段。 在這項工作中，您將使用其中一些程式碼片段。

1. 將名為 [**音訊**] 的新資料夾新增至網站資料夾的根目錄。 開啟 [Windows Explorer]，並將任何音訊檔案複製到 [ **WhatsNewASPNET** ] 方案的 [**音訊**] 資料夾中。
2. 在**default.aspx**頁面中，找出 Web11 Rocks！！底下的游標 標頭。 輸入**音訊**，然後按下 tab 鍵。

    新的 HTML 編輯器包含 HTML5 內容的程式碼片段。 請記得使用適當的 DOCTYPE 定義來啟用 HTML5 程式碼片段。

    ![插入 HTML5 程式碼片段](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image28.png "插入 HTML5 程式碼片段")

    *插入 HTML5 程式碼片段*
3. 更新音訊來源以指向現有的音訊檔案。

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample6.aspx)]

    > [!NOTE]
    > 您必須將音訊檔案新增至方案。
4. 按**F5**鍵執行網站並播放音訊。

    ![執行音訊控制項](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image29.png "執行音訊控制項")

    *執行音訊控制項*

    > [!NOTE]
    > 您也可以嘗試 Visual Studio 中包含的程式碼片段，例如影片、圖等等。
5. 現在，請嘗試在頁面的某個部分插入控制項。 例如，請嘗試插入**GridView**控制項，但不要輸入 **&lt;Gri，** 而是開始輸入 **&lt;GV**。 請注意，[IntelliSense] 清單會顯示**asp： GridView**控制項。

    HTML 編輯器中的 IntelliSense 現在提供標題大小寫搜尋，以及部分比對（抓取包含詞彙的所有元素）。

    ![使用 IntelliSense 清單插入 GridView](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image30.png "使用 IntelliSense 清單插入 GridView")

    *使用 IntelliSense 清單插入 GridView*

    如果您輸入 **&lt;方格**，則會取得符合該詞彙的所有專案，但 Visual Studio 會建議**gridview**控制項：

    ![使用 IntelliSense 清單和部分比對插入 GridView](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image31.png "使用 IntelliSense 清單和部分比對插入 GridView")

    *使用 IntelliSense 清單和部分比對插入 GridView*

<a id="Ex2Task4"></a>

<a id="Task_4_-_HTML_Editor_Smart_Tags"></a>
#### <a name="task-4---html-editor-smart-tags"></a>工作 4-HTML 編輯器智慧標籤

HTML 編輯器中的另一項改進是智慧標籤功能。 智慧標籤可讓您以每個控制項為基礎，輕鬆地執行一般或重複性的開發工作。 這項功能已在 HTML 設計工具中提供，但無法在 HTML 編輯器中使用。

1. 開啟 [ **Master** ]，然後找出 [ **asp： Menu** ] 元素。 將游標放在開始標記上，並注意在專案底部顯示的小型字元-按一下以開啟 [智慧型工作] 功能表。 請注意，您可以快速存取與功能表控制項相關的某些工作。

    ![Menu 控制項的智慧型工作](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image32.png "Menu 控制項的智慧型工作")

    *Menu 控制項的智慧型工作*

<a id="Ex2Task5"></a>

<a id="Task_5_-_Smart_Indentation"></a>
#### <a name="task-5---smart-indentation"></a>工作 5-智慧型縮排

HTML 中的其中一個最佳做法是縮排嵌套的元素，讓程式碼可讀取。 在 Visual Studio 2012 中，您會注意到，當您撰寫程式碼時，編輯器會自動縮排元素。

> [!NOTE]
> 在舊版的 Visual Studio 中，智慧型縮排可以在 XML 編輯器中使用，但在 HTML 編輯器中則不提供。

1. 請確定 [HTML 編輯器] 上的 [縮排設定] 已設為 [智慧型縮排]。 若要這麼做，請選取 [**工具] |[選項**] 功能表選項，然後選取 [**文字編輯器] |HTML |[索引**標籤] 頁面，位於畫面的左窗格中。 選取 [智慧型縮排] 選項。

    ![HTML 編輯器設定](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image33.png "HTML 編輯器設定")

    *HTML 編輯器設定*
2. 在**default.aspx**頁面上，移除 [音訊] 元素下的所有內容。
3. 將游標放在開頭**音訊**元素的結尾，然後按**ENTER 鍵**。

    請注意，資料指標的新位置有額外的縮排層級。

    ![HTML 編輯器中的智慧型縮排](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image34.png "HTML 編輯器中的智慧型縮排")

    *HTML 編輯器中的智慧型縮排*
4. 使用已移除的內容還原音訊標記，或關閉**default.aspx**而不儲存變更。

<a id="Ex2Task6"></a>

<a id="Task_6_-_Extract_to_User_Control"></a>
#### <a name="task-6---extract-to-user-control"></a>工作 6-解壓縮至使用者控制項

包含在 Visual Studio 中的重構工具（例如，將部分程式碼解壓縮至函式）是很棒的功能，可協助改善和重構現有的程式碼。 ASP.NET 網頁的對應項就是將 HTML 程式碼解壓縮至使用者控制項。 手動執行作業牽涉到幾個步驟，例如建立新的使用者控制項、將程式碼區段移至使用者控制項、註冊使用者控制項的標記前置詞，最後再將頁面上的使用者控制項具現化。 現在，新的 [*解壓縮至使用者控制*] 工具會自動為您執行所有這些步驟。

在這項工作中，您將使用新的 [解壓縮至使用者控制項] 內容作業，從選取的程式碼產生新的使用者控制項。

1. 在 [ **default.aspx** ] 頁面上，選取 [ **H2** ] 和 [**音訊**] 元素。
2. 按一下滑鼠右鍵，然後選取 [**解壓縮至使用者控制項**]。

    ![[解壓縮至使用者控制項] 功能表選項](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image35.png "[解壓縮至使用者控制項] 功能表選項")

    *[解壓縮至使用者控制項] 功能表選項*
3. 輸入新使用者控制項的名稱。 例如，[ **Jukebox**]，然後按一下 **[確定]** 。

    ![儲存已解壓縮的使用者控制項](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image36.png "儲存已解壓縮的使用者控制項")

    *儲存已解壓縮的使用者控制項*
4. 請注意，選取的程式碼已解壓縮至使用者控制項，而所選取程式碼的原始位置已取代為新使用者控制項的實例。

    ![頁面會自動更新以使用新的使用者控制項](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image37.png "頁面會自動更新以使用新的使用者控制項")

    *頁面會自動更新以使用新的使用者控制項*
5. 按**F5**執行頁面，並確認控制項可以運作。

<a id="Exercise3"></a>

<a id="Exercise_3_Whats_New_in_the_JavaScript_Editor"></a>
### <a name="exercise-3-whats-new-in-the-javascript-editor"></a>練習3： JavaScript 編輯器的新功能

撰寫或編輯 JavaScript 程式碼不是簡單的工作，特別是當您的應用程式開始變大時，您會發現自己處理的是長檔案和數以百計的功能。 腳本開發人員通常必須執行一些額外的工作，以維護程式碼的可讀性，並跨檔案進行流覽。 隨著 jQuery 這類 JavaScript 程式庫的包含，腳本導覽也會因為程式碼長度而變得很困難。

Visual Studio 已更新 JavaScript 編輯器，使其具備可供存取和組織程式碼模式的承諾。 已經存在C#或 VB 編輯器中的許多 Visual Studio 功能現在都是在 JavaScript 編輯器中執行： [移至定義]、[自動縮排]、[檔集] 和 [驗證] （當您撰寫時）。 在更新的 IntelliSense 清單中，您可以輕鬆地擁有 JavaScript 函數目錄。

在此練習中，您將瞭解 JavaScript 編輯器的一些新功能和改進。 您將流覽範例檔案，並探索每個新特性，讓您的 JavaScript 程式設計在 Visual Studio 2012 內更有效率。

<a id="Ex3Task1"></a>

<a id="Task_1_-_JavaScript_Editor_New_Features"></a>
#### <a name="task-1---javascript-editor-new-features"></a>工作 1-JavaScript 編輯器的新功能

這項工作會向您介紹一些新的 JavaScript 編輯器功能，其中著重于組織您的程式碼，並提供更好的使用者體驗。

1. 如果尚未開啟，請啟動**Visual Studio** ，然後開啟位於此實驗室的**Source\WhatsNewASPNET**資料夾中的**WhatsNewASPNET。**
2. 按**F5**執行應用程式，然後按一下巡覽列中的 [JavaScript] 連結。 重新整理頁面數次，並檢查計數器的遞增方式。

    ![頁面計數器](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image38.png "頁面計數器")

    *頁面計數器*
3. 關閉瀏覽器，然後返回 Visual Studio。
4. 開啟 [ **JavaScript .aspx** ] 頁面，並找出 **&lt;腳本&gt;** 區塊（如下所示）。

    下列程式碼會使用 HTML5 本機儲存區來儲存*pageLoadCount*變數，以儲存目前使用者已造訪過頁面的次數。 本機儲存體是以 HTML5 標準引進的用戶端索引鍵/值資料庫。 資料會儲存在本機電腦上的使用者瀏覽器中。

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample7.html)]

    > [!NOTE]
    > 請先確定 DOCTYPE 已設定為 XHTML5，再繼續進行後續步驟。
5. 編輯程式碼，並注意適用于 JavaScript 的 IntelliSense 包含 HTML5 功能，例如本機儲存體和其內部方法。

    ![JavaScript 中的 HTML5 JavaScript 功能](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image39.png "JavaScript 中的 HTML5 JavaScript 功能")

    *JavaScript 中的 HTML5 JavaScript 功能*
6. 按一下腳本程式碼中的任何左括弧（ **{** ），並注意括弧會反白顯示。

    ![括弧會反白顯示](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image40.png "括弧會反白顯示")

    *括弧會反白顯示*
7. 取消批註函數**testAutoAlign （）** （選取三行，您可以使用**CTRL** + **K**;**CTRL** + **U**），並找出函式程式碼內的游標。 按 enter 鍵以附加第二行。 請注意，程式碼現在已**對齊**並**自動縮排**。

    ![JavaScript 程式碼已自動對齊](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image41.png "JavaScript 程式碼已自動對齊")

    *JavaScript 程式碼已自動對齊*

<a id="Ex3Task2"></a>

<a id="Task_2_-_Validating_JavaScript"></a>
#### <a name="task-2---validating-javascript"></a>工作 2-驗證 JavaScript

在這項工作中，您將探索 ECMAScript5 standard 的新 JavaScript 驗證。 這項功能可協助您撰寫相容的 JavaScript 程式碼，同時在網站部署之前防止腳本問題。

> [!NOTE]
> Visual Studio 2010 實行 ECMAStript3 合規性，而 Visual Studio 2012 則提供 ECMAScript5 合規性。

1. 開啟位於**Scripts\custom**專案資料夾底下的**ECMA5script5** 。 您現在會測試 ECMAScript5 standard 的驗證。

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample8.html)]

    您可以在檔案的第一行中查看 &quot;**使用嚴格**的 &quot; 方向，這會啟用 ECMAScript5 **strict 模式**。 這個模式是由語言的子集所組成，其中包含過去版本的多義性，並加入一些新功能，例如 getter 和 setter、JSON 的程式庫支援，以及更完整的物件屬性反映。
2. 開啟 [**錯誤清單**] （如果尚未開啟）（[**視圖**] 功能表 |**錯誤清單**）。 請注意，**函數**聲明會加上底線。 這是因為在 ECMA5 標準函式中，不能嵌套于語言結構內部。 在下面的 [錯誤清單] 中，您會看到警告詳細資料。

    ![JavaScript 驗證錯誤訊息](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image42.png "JavaScript 驗證錯誤訊息")

    *JavaScript 驗證錯誤訊息*
3. 批註外 **&quot;使用嚴格的&quot;** 方向，並注意錯誤會消失，但仍會出現警告。
4. 在檔案的最後一行中，寫入任何字串（例如 **&quot;測試&quot;** （包含引號來表示它是字串）。 在字串旁邊撰寫一個句點以顯示 IntelliSense 清單，然後選取 [**修剪**] 選項。

    在 ECMAScript5 standard 中，字串值和變數也會定義字串方法，例如 trim、大寫、搜尋和取代。

    ![JavaScript 中的 IntelliSense 清單](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image43.png "JavaScript 中的 IntelliSense 清單")

    *JavaScript 中的 IntelliSense 清單*

<a id="Ex3Task3"></a>

<a id="Task_3_-_XML_Documentation_for_JavaScript"></a>
#### <a name="task-3---xml-documentation-for-javascript"></a>工作 3-JavaScript 的 XML 檔

在這項工作中，您將探索 JavaScript 中的 XML 檔 Visual Studio 功能。 您會看到 JavaScript IntelliSense 清單現在會顯示每個函式的 XML 檔。 此外，您將探索 JavaScript 中的導覽功能。

1. 開啟位於**腳本/自訂**專案資料夾中的**XMLDoc。** 此檔案包含每個 JavaScript 函數的 XML 檔。

    ![整合至 IntelliSense 的 JavaScript XML 檔](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image44.png "整合至 IntelliSense 的 JavaScript XML 檔")

    *整合至 IntelliSense 的 JavaScript XML 檔*
2. 在**XMLDoc**的 **[新增函式] 底下，** 建立名為**test**的新函數。
3. 在**測試**函式中，呼叫接收兩個參數的**乘法**函數。 請注意，[工具提示] 方塊會顯示 [**乘法**函數] 檔。

    [!code-javascript[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample9.js)]

    ![JavaScript 函式的 XML 檔](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image45.png "JavaScript 函式的 XML 檔")

    *JavaScript 函式的 XML 檔*
4. 完成函式呼叫語句，並輸入一個*點*來開啟所傳回值的 IntelliSense 清單。 請注意，Visual Studio 會偵測檔中的**傳回值，** 並將該值視為數位。

    ![傳回類型的 XML 檔](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image46.png "傳回類型的 XML 檔")

    *傳回類型的 XML 檔*
5. 現在，插入呼叫以加入函數。 請注意，JavaScript 編輯器現在支援函數多載。 當您撰寫函式名稱時，您將能夠選取在檔中指定的任何可用的多載。

    ![多載的 XML 檔](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image47.png "多載的 XML 檔")

    *多載的 XML 檔*
6. 開啟**GotoDefinition** ，並找出 **$ （） .html （）** 函式呼叫。 在**html**上尋找游標。
7. 按**F12**並流覽至定義。 請注意，您現在可以存取和流覽 JavaScript 程式碼，而不需要使用 [**尋找**] 工具。
8. 在程式碼檔案底部的簽章區塊之前，于 jQuery 指令上尋找游標。 按**F12**。 您將流覽至 jQuery 程式庫檔案。 請注意，您也可以使用**F12**跨 jQuery 檔案進行流覽。

    ![導覽至 jQuery 定義](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image48.png "導覽至 jQuery 定義")

    *導覽至 jQuery 定義*

> [!NOTE]
> 在儲存檔案之前，請確定 GotoDefinition 沒有任何語法錯誤。

<a id="Exercise4"></a>

<a id="Exercise_4_Bundling_and_Minification"></a>
### <a name="exercise-4-bundling-and-minification"></a>練習4：捆綁和縮制

您的網站有多少次包含一個以上的 JavaScript 或 CSS 檔案？ 這是一個很常見的案例，其中的組合和縮制有助於減少檔案大小，並讓網站執行速度更快。 ASP.NET 4.5 中的新配套功能會將一組 JS 或 CSS 檔案封裝成單一專案，並藉由縮小內容來減少其大小（也就是移除不必要的空格、移除批註、減少識別碼）。

ASP.NET 4.5 中的組合和縮制是在執行時間執行，因此，進程可以識別使用者代理程式（例如 IE、Mozilla 等等），並藉由鎖定使用者瀏覽器（例如，移除 Mozilla 特定的內容）來改善壓縮。當要求來自 IE 時）。

在此練習中，您將瞭解如何在 ASP.NET 4.5 中啟用和使用不同類型的組合和縮制。

<a id="Ex4Task1"></a>

<a id="Task_1_-_Installing_the_Bundling_and_Minification_Package_from_NuGet"></a>
#### <a name="task-1---installing-the-bundling-and-minification-package-from-nuget"></a>工作 1-從 NuGet 安裝封裝和縮制套件

1. 如果尚未開啟，請啟動**Visual Studio** ，然後開啟位於此實驗室的**Source\WhatsNewASPNET**資料夾中的**WhatsNewASPNET。**
2. 開啟 NuGet 套件管理員主控台。 若要這麼做，請使用功能表**視圖** | **其他 Windows** | **套件管理員主控台**。

    ![開啟封裝管理員 file:///C:/Users/User/AppData/Local/Temp/Marker3744//media/44462/Multiple-Stylesheets-and-JavaScript-files-in-the-application.pngconsole](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image49.png "開啟套件管理員主控台")

    *開啟套件管理員主控台*
3. 在 [**套件管理員主控台**] 中，輸入**Install-Package** Web.config，然後按**enter**。

<a id="Ex4Task2"></a>

<a id="Task_2_-_Default_Bundles"></a>
#### <a name="task-2---default-bundles"></a>工作 2-預設組合

使用配套和縮制最簡單的方式，就是啟用預設組合。 這個方法會使用慣例，讓您參考資料夾中 JS 和 CSS 檔案的配套和縮減版本。

在這項工作中，您將學習如何啟用和參考配套的和縮減 JS 和 CSS 檔案，並查看產生的輸出。

1. 如果尚未開啟，請啟動**Visual Studio** ，然後開啟位於此實驗室的**Source\WhatsNewASPNET**資料夾中的**WhatsNewASPNET。**
2. 在 **方案總管**中，展開 **樣式**、 **Scripts\custom**  和  **Scripts\bundle**  資料夾。

    請注意，應用程式會使用一個以上的 CSS 和 JS 檔案。

    ![應用程式中的多個樣式表單和 JavaScript 檔案](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image50.png "應用程式中的多個樣式表單和 JavaScript 檔案")

    *應用程式中的多個樣式表單和 JavaScript 檔案*
3. 開啟**Global.asax.cs**檔案。

    請注意，新的**Microsoft. Web. 優化**命名空間在檔案開頭會加上批註。 取消批註 using 指示詞，以包含捆綁和縮制功能。

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample10.cs)]
4. 找出**應用程式\_Start**方法。

    在此方法中，取消批註 EnableDefaultBundles 呼叫，如下列程式碼片段所示。 這可讓我們使用資料夾的路徑，以及 &quot;CSS&quot; 或 &quot;JS&quot; 尾碼，來參考資料夾中的 CSS 檔案配套集合。

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample11.cs)]
5. 開啟 [**優化 .aspx**檔案]，並找出**HeadContent**的內容控制項。

    請注意，CSS 檔案和 JS 檔案有一個參考的標記。

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample12.aspx)]

    > [!NOTE]
    > 這段程式碼是為了示範之用。 在理想的情況下，您將會參考網站中的套件組合。 在此範例程式碼中，您會發現一些配套的檔案也被網站主控檔案參照，因此最後一個參考是多餘的。
6. 請注意，連結會使用**href**屬性中的組合慣例，分別從 [樣式] 和 [Scripts\custom] 資料夾取得所有 CSS 或 JS 檔案。

    您可以使用如下所示的路徑**腳本/自訂/JS** ，在**腳本/自訂**資料夾內組合及縮小所有 JS 檔案。 這是預設的組合的預設行為。

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample13.aspx)]
7. 開啟**Styles\Site.css**檔案。

    請注意，原始的 CSS 檔案包含縮排的程式碼、空白空格和用來放大檔案的批註。 （此外，JavaScript 檔案也包含空格和批註）。

    ![[腳本] 資料夾中的其中一個原始 CSS 檔案](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image51.png "[腳本] 資料夾中的其中一個原始 CSS 檔案")

    *[腳本] 資料夾中的其中一個原始 CSS 檔案*
8. 按**F5**執行應用程式，並流覽至 [**優化**] 頁面。
9. 按一下 [ **CSS**配套] 連結，以下載並開啟檔案。

    查看縮減配套的檔案。 您會發現所有的空格、批註和縮排字元都已移除，產生較小的檔案。

    ![配套的 CSS 檔案](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image52.png "配套的 CSS 檔案")

    *配套的 CSS 檔案*
10. 現在，按一下 [ **JS**套件組合] 連結，以開啟 JavaScript 配套的檔案。 您可以放心地忽略 explorer 警告。 請注意，**自訂**資料夾下的 JavaScript 檔案也已配套並縮減。

    ![配套的 JavaScript 檔案](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image53.png "配套的 JavaScript 檔案")

    *配套的 JavaScript 檔案*

    在先前的 ASP.NET 版本中，啟用 CSS 或 JS 檔案的壓縮更為複雜。 現在，如您所見，您只需要在*global.asax*檔案中加入一行來啟用組合，然後從您的網站參考配套的檔案。

<a id="Ex4Task3"></a>

<a id="Task_3_-_Static_Bundles"></a>
#### <a name="task-3---static-bundles"></a>工作 3-靜態組合

靜態組合方法可讓您自訂要組合的一組檔案、參考和將使用的縮制方法。

在這項工作中，您將設定靜態組合，以定義要配套和縮小的一組特定檔案。

1. 關閉瀏覽器。
2. 開啟**Global.asax.cs**檔案，並找出**應用程式\_Start**方法。
3. 取消批註靜態組合程式碼，如下列程式碼所示。

    您正在定義將使用 &quot; **~/StaticBundle**&quot; 虛擬路徑來參考的靜態組合，並使用**JsMinify**來縮制所有具有**AddFile**方法的指定檔案。 最後，您會將靜態組合新增至**當**並加以啟用。

    請注意，檔案不是位於相同的位置;這是預設的配套的另一個優點。

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample14.cs)]
4. 開啟 [**優化 .aspx**檔案]。

    請注意，當您在 Global.asax.cs 檔案中設定靜態組合時，**靜態 JS**套件組合的連結會使用您所宣告的路徑： **/StaticBundle**。

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample15.aspx)]
5. 按**F5**執行應用程式，然後流覽至 [**優化**] 頁面。
6. 按一下 [**靜態 JS**組合] 連結以開啟檔案。

    請注意，縮減配套的 JavaScript 檔案是在靜態套件組合檔案中設定的所有 JavaScript 檔案的輸出，該檔案位於&quot;的路徑 &quot;的/StaticBundle。

    ![靜態 JavaScript 檔案配套](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image54.png "靜態 JavaScript 檔案配套")

    *靜態 JavaScript 檔案配套*
7. 關閉瀏覽器並返回 Visual Studio。

<a id="Ex4Task4"></a>

<a id="Task_4_-_Dynamic_Folder_Bundles"></a>
#### <a name="task-4---dynamic-folder-bundles"></a>工作 4-動態資料夾組合

在這項工作中，您將瞭解如何設定動態資料夾組合。 動態組合的威力在於，您可以在編譯成 JavaScript 的語言中包含靜態 JavaScript 和其他檔案，因此在執行組合之前，需要進行一些處理。

在此範例中，您將瞭解如何使用**DynamicFolderBundle**類別，為以 CofeeScript 撰寫的檔案建立動態組合。 CofeeScript 是一種程式設計語言，它會編譯成 JavaScript，並提供更簡單的語法來撰寫 JavaScript 程式碼，強化 JavaScript 的簡潔性和可讀性。

1. 開啟**Global.asax.cs**檔案，並找出**應用程式\_Start**方法。
2. 取消批註動態套件組合程式碼，如下列程式碼所示。

    您所定義的動態資料夾配套會使用**CoffeeMinify**自訂縮制處理器，此套件只會套用至具有 &quot;**咖啡**&quot; 延伸模組（CoffeeScript 檔案）的檔案。 請注意，您可以使用搜尋模式來選取要在資料夾內組合的檔案，例如 '\*咖啡 '。

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample16.cs)]
3. 開啟 NuGet 套件管理員主控台。 若要這麼做，請使用功能表**視圖** | **其他 Windows** | **套件管理員主控台**。
4. 在 [**套件管理員主控台**] 中，輸入**Install-Package CoffeeSharp** ，然後按**enter**。
5. 按一下 [**方案總管**] 視窗中的 [**顯示所有**檔案] 按鈕

    ![顯示所有檔案](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image55.png "顯示所有檔案")

    *顯示所有檔案*
6. 以滑鼠右鍵按一下**方案總管**中的**CoffeeMinify.cs**檔案，然後選取 [**包含在專案中**]

    ![將 CoffeeMinify.cs 檔案包含在專案中](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image56.png "將 CoffeeMinify.cs 檔案包含在專案中")

    *將 CoffeeMinify.cs 檔案包含在專案中*
7. 開啟**CoffeeMinify.cs**檔案。

    這個類別繼承自 JsMinify，以縮小 CoffeeScript 程式碼編譯所產生的 JavaScript 輸出。 它會呼叫 CoffeeScript 編譯器先產生 JavaScript 程式碼，然後將它傳送至 JsMinify 方法，以縮小產生的程式碼。

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample17.cs)]
8. 從 [**腳本/** 組合] 資料夾開啟**Script1 咖啡**和**Script2 咖啡**檔案。

    這些檔案會包含在使用 CoffeeMinify 類別執行組合時所要編譯的 CoffeScript 程式碼。

    為了簡單起見，所提供的 CoffeeScript 檔案只包含 CoffeeScript 範例程式碼。 批註會由 JsMinify 流程排除。

    ![CoffeeScript 檔案](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image57.png "CoffeeScript 檔案")

    *CoffeeScript 檔案*

    > [!NOTE]
    > [CofeeScript](https://github.com/jashkenas/coffeescript/)提供更簡單的語法來撰寫 javascript 程式碼、增強 javascript 的簡潔性和可讀性，以及加入其他功能，例如陣列理解和模式比對。
9. 開啟 [**優化 .aspx**檔案]，並找出 [組合] 連結。

    請注意，**動態 JS**配套的連結會使用您為動態資料夾配套所設定的 **/Coffee**尾碼來參考**腳本/** 組合資料夾。

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample18.aspx)]
10. 按**F5**執行應用程式，然後流覽至 [**優化**] 頁面。
11. 按一下 [**動態 JS**套件組合] 連結，以開啟產生的檔案。

    請注意，此配套中包含的內容只包含**咖啡**檔案。 您也可以看到 CoffeeScript 程式碼已編譯成 JavaScript，而且已移除批註的行。

    ![動態 JS 檔案配套](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image58.png "動態 JS 檔案配套")

    *動態 JS 檔案配套*

> [!NOTE]
> 此外，您可以遵循[附錄 B：使用 Web Deploy 發佈 ASP.NET MVC 4 應用程式](#AppendixB)，將此應用程式部署到 Windows Azure 網站。

<a id="Summary"></a>
## <a name="summary"></a>總結

此實驗室可協助您瞭解 Visual Studio 2012 中 ASP.NET 和 Web 開發的新功能，以及如何利用 Visual Studio 2012 中的各種增強功能。

藉由完成此實際操作實驗室，您就可以學會如何使用適用于 CSS、JavaScript 和 HTML 的 Visual Studio 2012 編輯器中的新功能和改善。 此外，您還學會了 Visual Studio 2012 如何實行內建的組合和縮制。

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附錄 A：安裝 Web 的 Visual Studio Express 2012

您可以使用 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** 安裝 Web 或另一個 &quot;Express&quot; 版本**的 Microsoft Visual Studio Express 2012** 。 下列指示會引導您完成使用*Microsoft Web Platform Installer*安裝*Visual studio Express 2012 for Web*所需的步驟。

1. 移至[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。 或者，如果您已經安裝 Web Platform Installer，您可以開啟它，然後使用 Windows Azure SDK&quot;來搜尋產品 &quot;<em>Visual Studio Express 2012 For Web</em> 。
2. 按一下 [**立即安裝**]。 如果您沒有**Web Platform Installer**系統會將您重新導向，先下載並安裝。
3. 開啟**Web Platform Installer**之後，請按一下 [**安裝**] 以啟動安裝程式。

    ![安裝 Visual Studio Express](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image59.png "安裝 Visual Studio Express")

    *安裝 Visual Studio Express*
4. 閱讀所有產品的授權和條款，然後按一下 [**我接受**] 繼續。

    ![接受授權條款](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image60.png)

    *接受授權條款*
5. 等到下載和安裝程式完成為止。

    ![安裝進度](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image61.png)

    *安裝進度*
6. 當安裝完成時，按一下 **[完成]** 。

    ![安裝已完成](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image62.png)

    *安裝已完成*
7. 按一下 **[** 結束] 以關閉 Web Platform Installer。
8. 若要開啟 Web Visual Studio Express，請移至 [**開始**] 畫面，然後開始撰寫 &quot;**VS Express**&quot;，然後按一下 [ **VS Express for Web** ] 磚。

    ![VS Express for Web 磚](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image63.png)

    *VS Express for Web 磚*

---

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>附錄 B：使用 Web Deploy 發行 ASP.NET MVC 4 應用程式

本附錄將告訴您如何從 Windows Azure 管理入口網站建立新的網站，以及如何發佈您在實驗室之後取得的應用程式，利用 Windows Azure 提供的 Web Deploy 發行功能。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>工作 1-從 Windows Azure 入口網站建立新的網站

1. 移至[Windows Azure 管理入口網站](https://manage.windowsazure.com/)並使用與您的訂用帳戶相關聯的 Microsoft 認證登入。

    > [!NOTE]
    > 有了 Windows Azure，您可以免費裝載10個 ASP.NET 網站，然後隨著流量的成長而調整。 您可以在[這裡](https://aka.ms/aspnet-hol-azure)註冊。

    ![登入 Windows Azure 入口網站](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image64.png "登入 Windows Azure 入口網站")

    *登入 Windows Azure 管理入口網站*
2. 按一下命令列上的 [**新增**]。

    ![建立新網站](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image65.png "建立新網站")

    *建立新網站*
3. 按一下 [**計算** | 的**網站**]。 然後選取 [**快速建立**] 選項。 提供新網站的可用 URL，然後按一下 [**建立網站**]。

    > [!NOTE]
    > Windows Azure 網站是在雲端中執行之 Web 應用程式的主機，您可以控制和管理。 [快速建立] 選項可讓您從入口網站外部，將已完成的 web 應用程式部署至 Windows Azure 網站。 它不包含設定資料庫的步驟。

    ![使用 [快速建立] 建立新的網站](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image66.png "使用 [快速建立] 建立新的網站")

    *使用 [快速建立] 建立新的網站*
4. 等到新**網站**建立完畢。
5. 建立網站之後，請按一下 [ **URL** ] 資料行下方的連結。 檢查新網站是否正常運作。

    ![流覽至新網站](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image67.png "流覽至新網站")

    *流覽至新網站*

    ![網站正在執行](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image68.png "網站正在執行")

    *網站正在執行*
6. 返回入口網站，然後按一下 [**名稱**] 欄底下的網站名稱，以顯示管理頁面。

    ![開啟網站管理頁面](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image69.png "開啟網站管理頁面")

    *開啟網站管理頁面*
7. 在 [**儀表板**] 頁面的 [**快速概覽**] 區段下，按一下 [**下載發行設定檔**] 連結。

    > [!NOTE]
    > *發行設定檔*包含將 web 應用程式發佈至 Windows Azure 網站所需的所有資訊，以供每個已啟用的發行方法使用。 發行設定檔包含 URL、使用者認證和資料庫字串，這些都是用來連接到已啟用發行方法的每個端點並進行驗證的必要資訊。 **Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支援讀取發行設定檔，以將這些程式的設定自動化，以將 Web 應用程式發佈至 Windows Azure 網站。

    ![正在下載網站發行設定檔](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image70.png "正在下載網站發行設定檔")

    *正在下載網站發行設定檔*
8. 將發行設定檔下載到已知的位置。 在此練習中，您將瞭解如何使用此檔案，將 web 應用程式從 Visual Studio 發行至 Windows Azure 網站。

    ![儲存發行設定檔](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image71.png "正在儲存發行設定檔")

    *儲存發行設定檔*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>工作 2-設定資料庫伺服器

如果您的應用程式會使用 SQL Server 資料庫，您必須建立 SQL Database 伺服器。 如果您想要部署不使用 SQL Server 的簡單應用程式，您可能會略過這項工作。

1. 您將需要 SQL Database 伺服器來儲存應用程式資料庫。 您可以在 Windows Azure 管理入口網站的  **SQL 資料庫** | **伺服器** | **伺服器的儀表板**上，從您的訂用帳戶中查看 SQL Database 伺服器。 如果您沒有建立伺服器，可以使用命令列上的 [**新增**] 按鈕建立一個。 記下 [**伺服器名稱] 和 [URL]、[系統管理員登入名稱] 和 [密碼**]，因為您將在後續工作中使用它們。 請不要建立資料庫，因為它會在稍後的階段中建立。

    ![SQL Database Server 儀表板](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image72.png "SQL Database Server 儀表板")

    *SQL Database Server 儀表板*
2. 在下一項工作中，您將會從 Visual Studio 測試資料庫連線，因此您必須在伺服器的**允許 IP 位址**清單中包含本機 IP 位址。 若要這麼做，請按一下 [**設定**]，選取**目前用戶端 IP 位址**的 ip 位址，並將它貼在 [**起始 Ip 位址**] 和 [**結束 ip 位址**] 文字方塊上。 輸入規則的名稱，然後按一下 ![新增-用戶端-ip-位址-確定 按鈕](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image73.png) 按鈕。

    ![正在新增用戶端 IP 位址](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image74.png)

    *正在新增用戶端 IP 位址*
3. 將**用戶端 Ip 位址**新增至 [允許的 ip 位址] 清單之後，按一下 [**儲存**] 以確認變更。

    ![確認變更](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image75.png)

    *確認變更*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>工作 3-使用 Web Deploy 發行 ASP.NET MVC 4 應用程式

1. 返回 ASP.NET MVC 4 解決方案。 在 **方案總管**中，以滑鼠右鍵按一下 網站 專案，然後選取 **發佈**。

    ![發行應用程式](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image76.png "發行應用程式")

    *發行網站*
2. 匯入您在第一個工作中儲存的發行設定檔。

    ![匯入發行設定檔](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image77.png "匯入發行設定檔")

    *正在匯入發行設定檔*
3. 按一下 [**驗證連接**]。 驗證完成後，按 **[下一步]** 。

    > [!NOTE]
    > 當您看到 [驗證連線] 按鈕旁出現綠色核取記號時，驗證就會完成。

    ![正在驗證連接](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image78.png "正在驗證連接")

    *正在驗證連接*
4. 在 [**設定**] 頁面的 [**資料庫**] 區段底下，按一下資料庫連接的文字方塊旁邊的按鈕（也就是**DefaultConnection**）。

    ![Web deploy 設定](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image79.png "Web deploy 設定")

    *Web deploy 設定*
5. 設定資料庫連接，如下所示：

   - 在 [**伺服器名稱**] 中，使用*tcp：* prefix 輸入您的 SQL Database 伺服器 URL。
   - 在 [**使用者名稱**] 中，輸入您的伺服器管理員登入名稱。
   - 在 [**密碼**] 中輸入您的伺服器管理員登入密碼。
   - 輸入新的資料庫名稱，例如： *MVC4SampleDB*。

     ![正在設定目的地連接字串](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image80.png "正在設定目的地連接字串")

     *正在設定目的地連接字串*
6. 然後按一下 [確定]。 當系統提示您建立資料庫時，請按一下 **[是]** 。

    ![建立資料庫](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image81.png "建立資料庫字串")

    *建立資料庫*
7. 您將用來連接到 Windows Azure 中 SQL Database 的連接字串會顯示在 [預設連接] 文字方塊中。 然後按一下 [下一步]。

    ![指向 SQL Database 的連接字串](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image82.png "指向 SQL Database 的連接字串")

    *指向 SQL Database 的連接字串*
8. 在 [**預覽**] 頁面中，按一下 [**發佈**]。

    ![發行 web 應用程式](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image83.png "發行 web 應用程式")

    *發行 web 應用程式*
9. 發佈程式完成後，您的預設瀏覽器會開啟已發行的網站。

    ![發行至 Windows Azure 的應用程式](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image84.png "發行至 Windows Azure 的應用程式")

    *發行至 Windows Azure 的應用程式*
