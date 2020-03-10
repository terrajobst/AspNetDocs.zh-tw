---
uid: visual-studio/overview/2013/visual-studio-2013-web-tools
title: 實習實驗室： Visual Studio 2013 Web 工具 |Microsoft Docs
author: rick-anderson
description: Visual Studio 是適用于的絕佳開發環境。以網路為基礎的 Windows 和 Web 專案。 其中包含強大的文字編輯器，可輕鬆地用於 。
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 09e82351-816b-402d-acd1-0f9ac6901d16
msc.legacyurl: /visual-studio/overview/2013/visual-studio-2013-web-tools
msc.type: authoredcontent
ms.openlocfilehash: 2fb987dd9b26ad9f0e8a88fd881bde4505ec4148
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622672"
---
# <a name="hands-on-lab-visual-studio-2013-web-tools"></a>實習實驗室： Visual Studio 2013 Web 工具

依[Web Camp 團隊](https://twitter.com/webcamps)

[下載 Web Camp 訓練套件](https://aka.ms/webcamps-training-kit)

> Visual Studio 是適用于的絕佳開發環境。以網路為基礎的 Windows 和 Web 專案。 其中包含強大的文字編輯器，可輕鬆地在不使用專案的情況下編輯獨立檔案。
> 
> 當您編輯每個檔案時，Visual Studio 會維護功能完整的剖析樹狀目錄。 這可讓 Visual Studio 提供無與倫比的自動完成和以檔為基礎的動作，同時讓開發體驗變得更快且更愉快。 這些功能在 HTML 和 CSS 檔中特別有用。
> 
> 這項功能也適用于延伸模組，可讓您輕鬆擴充具有強大新功能的編輯器，以符合您的需求。 Web Essentials 是（大部分）與 web 相關的 Visual Studio 增強功能的集合。 其中包含許多新的 IntelliSense 完成（特別是針對 CSS）、新的瀏覽器連結功能、JavaScript 檔案的自動 JSHint、HTML 和 CSS 的新警告，以及許多對新式 網頁程式開發不可或缺的其他功能。
> 
> 所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可在[https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)取得。

<a id="Overview"></a>
## <a name="overview"></a>概觀

<a id="Objectives"></a>
### <a name="objectives"></a>目標

在此實際操作實驗室中，您將瞭解如何：

- 使用 Web Essentials 中包含的新 HTML 編輯器功能，例如豐富的 HTML5 程式碼片段和 Zen 編碼
- 使用 Web Essentials 中包含的新 CSS 編輯器功能，例如色彩選擇器和瀏覽器矩陣工具提示
- 使用 Web Essentials 中包含的新 JavaScript 編輯器功能，例如 [解壓縮至檔案] 和 [IntelliSense]，適用于所有 HTML 元素
- 使用瀏覽器連結在瀏覽器與 Visual Studio 之間交換資料

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Prerequisites

若要完成此實際操作實驗室，需要下列各項：

- [Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/)或更高版本
- [Web Essentials 2013](http://vswebessentials.com/)
- [Google Chrome](https://www.google.com/chrome/)

<a id="Setup"></a>
### <a name="setup"></a>安裝程式

為了在此實際操作實驗室中執行練習，您必須先設定您的環境。

1. 開啟 Windows Explorer 視窗，並流覽至實驗室的 [**源**] 資料夾。
2. 以滑鼠右鍵按一下 [ **Setup** ]，然後選取 [以**系統管理員身分執行**] 來啟動安裝程式，以設定您的環境並安裝此實驗室的 Visual Studio 程式碼片段。
3. 如果顯示 [使用者帳戶控制] 對話方塊，請確認動作以繼續。

> [!NOTE]
> 執行安裝程式之前，請確定您已檢查過此實驗室的所有相依性。

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>使用程式碼片段

在整個實驗室檔中，系統會指示您插入程式碼區塊。 為了方便起見，大部分的程式碼都是以 Visual Studio Code 程式碼片段的形式提供，您可以從 Visual Studio 2013 內進行存取，以避免必須以手動方式新增。

> [!NOTE]
> 每個練習都附有一個起始解決方案，此方案位於練習的 [**開始**] 資料夾中，可讓您獨立于其他練習之外進行追蹤。 請注意，在練習期間新增的程式碼片段缺少這些起始的解決方案，而且在您完成練習之前可能無法正常執行。 在練習的原始程式碼中，您也會找到一個包含 Visual Studio 解決方案的**結束**資料夾，其中含有完成對應練習中步驟所產生的程式碼。 如果您在進行此實際操作實驗室時需要其他協助，您可以使用這些解決方案做為指導方針。

---

<a id="Exercises"></a>
## <a name="exercises"></a>練習

這個實際操作實驗室包含下列練習：

1. [使用瀏覽器連結和 Web Essentials](#Exercise1)
2. [利用程式碼片段和 IntelliSense](#Exercise2)

> [!NOTE]
> 當您第一次啟動 Visual Studio 時，您必須選取其中一個預先定義的設定集合。 每個預先定義的集合都是設計來符合特定的開發風格，並決定視窗配置、編輯器行為、IntelliSense 程式碼片段和對話方塊選項。 本實驗室中的程式說明在使用 [**一般開發設定**] 集合時，在 Visual Studio 中完成指定工作所需的動作。 如果您針對開發環境選擇不同的 [設定] 集合，您應該考慮的步驟可能會有所差異。

<a id="Exercise1"></a>
### <a name="exercise-1-working-with-browser-link-and-web-essentials"></a>練習1：使用瀏覽器連結和 Web Essentials

**Web Essentials**是一個 Visual Studio 延伸模組，可為新式 Web 開發新增各種有用的功能，其主要著重于讓 網頁程式開發體驗更快、更愉快。 您可以從 Visual Studio 的擴充功能庫安裝 Web Essentials。

**瀏覽器連結**是包含在 Visual Studio 2013 中的新功能，可在 Visual Studio IDE 和任何開啟的瀏覽器之間提供通道，以便在您的 web 應用程式和 Visual Studio 之間交換資料。 Web Essentials 使用工具擴充瀏覽器連結，直接從瀏覽器操作您網頁的 DOM 物件模型和 CSS 樣式。

在此練習中，您將探索**Web Essentials**和**瀏覽器**所支援的一些功能，以增強簡單的測驗頁面。

<a id="Ex1Task1"></a>
#### <a name="task-1---running-the-project-in-multiple-browsers"></a>工作 1-在多個瀏覽器中執行專案

在這項工作中，您會將 web 應用程式設定為同時在多個瀏覽器中執行，這對於跨瀏覽器測試很有用。

1. 開啟**Microsoft Visual Studio**。
2. **在 [檔案**] 功能表中，選取 [開啟] **|專案/方案 ...** 然後流覽至實驗室的**源**資料夾中的**Ex1-WorkingwithBrowserLinkandWebEssentials\Begin** （C:\WebCampsTK\HOL\VSWebTooling\Source）。 選取 [**開始**]，然後按一下 [**開啟**]。
3. 在 [Visual Studio] 工具列中，展開 [瀏覽器] 功能表，然後選取 **[流覽方式 ...]** 。

    ![流覽功能表選項](visual-studio-2013-web-tools/_static/image1.png "流覽方式 。在瀏覽器功能表中")

    *流覽功能表選項*
4. 在 [**流覽方式**] 對話方塊中，按住**CTRL**鍵並按一下 [**設定為預設值**]，以選取**Google Chrome**和**Internet Explorer** 。

    ![[流覽方式] 對話方塊](visual-studio-2013-web-tools/_static/image2.png "[流覽方式] 對話方塊")

    *選取多個預設瀏覽器*
5. Google Chrome 和 Internet Explorer 現在應該會顯示為預設瀏覽器。 按一下 [**取消**] 關閉對話方塊。

    ![Google Chrome 和 Internet Explorer 做為預設瀏覽器](visual-studio-2013-web-tools/_static/image3.png "Google Chrome 和 Internet Explorer 預設瀏覽器")

    *Google Chrome 和 Internet Explorer 做為預設瀏覽器*

    > [!NOTE]
    > 設定預設瀏覽器之後，瀏覽器功能表中會選取 [**多個流覽**器] 選項。
    > 
    > ![多個瀏覽器](visual-studio-2013-web-tools/_static/image4.png "多個瀏覽器")
6. 按**CTRL** + **F5**以執行應用程式，而不進行偵測。
7. 當這兩個瀏覽器視窗都開啟時，將其中一項放在另一個上方，以便同時查看兩個瀏覽器的更新。 瀏覽器應該會顯示含有淺藍色矩形的網頁。

    ![將一個瀏覽器放在另一個上方](visual-studio-2013-web-tools/_static/image5.png "將一個瀏覽器放在另一個上方")

    *將一個瀏覽器放在另一個上方*
8. 請勿關閉瀏覽器。 您將在下一項工作中使用它們。

<a id="Ex1Task2"></a>
#### <a name="task-2---using-zen-coding-to-create-html-elements"></a>工作 2-使用 Zen 編碼來建立 HTML 元素

**Zen 編碼**是一個編輯器外掛程式，適用于高速 HTML、XML、XSL （或任何其他結構化程式碼格式）編碼和編輯。 此外掛程式的核心是功能強大的縮寫引擎，可讓您將運算式（類似于 CSS 選取器）展開為 HTML 程式碼。 Zen 編碼是使用 CSS 樣式選擇器語法來撰寫 HTML 的快速方式。

在此練習中，您將使用 Web Essentials 提供的 Zen 編碼功能來產生代表問題選項的 HTML 按鈕。

1. 切換回 Visual Studio。
2. 開啟位於**Views** | **Home**資料夾中的**Index. cshtml**檔案。
3. 取代 **&lt;!--TODO：在此加入選項--&gt;** 批註加上下列程式碼，然後按**tab**鍵。

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample1.css)]
4. 程式碼應該展開為 HTML。

    ![擴充的 HTML](visual-studio-2013-web-tools/_static/image6.png "擴充的 HTML")

    *擴充的 HTML*

    > [!NOTE]
    > 若要深入瞭解 Zen 編碼語法，請參閱下列[文章](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/)。
5. 按一下 [重新整理**連結的瀏覽器**] 按鈕，以更新這兩個瀏覽器。

    ![重新整理連結的瀏覽器](visual-studio-2013-web-tools/_static/image7.png "重新整理連結的瀏覽器")

    *重新整理連結的瀏覽器*

    ![Internet Explorer-頁面已更新四個按鈕](visual-studio-2013-web-tools/_static/image8.png "Internet Explorer-頁面已更新四個按鈕")

    *Internet Explorer-頁面已更新四個按鈕*

    ![Google Chrome-頁面已更新四個按鈕](visual-studio-2013-web-tools/_static/image9.png "Google Chrome-頁面已更新四個按鈕")

    *Google Chrome-頁面已更新四個按鈕*
6. 切換回 Visual Studio。
7. 您已將按鈕新增至頁面，但您仍然需要新增範本問題。 若要這麼做，您將使用 Web Essentials 中名為**Lorem Ipsum**產生器的新功能。 找出具有**class**屬性**front**的**div**元素。
8. 新增下列程式碼做為**div**的第一個子專案，然後按**tab**鍵。

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample2.css)]
9. 程式碼應該展開為 HTML。

    ![自動產生的 Lorem Ipsum](visual-studio-2013-web-tools/_static/image10.png "自動產生的 Lorem Ipsum")

    *自動產生的 Lorem Ipsum*

    > [!NOTE]
    > 在 Zen 程式碼撰寫過程中，您現在可以直接在 HTML 編輯器中產生 Lorem Ipsum 程式碼。 只要輸入**lorem**並按**TAB 鍵**，就會插入30個單字 lorem Ipsum 文字。 例如， *lorem10*會插入10個 Lorem Ipsum 文字。
10. 您會使用 Web Essentials 中的另一項新功能（稱為**Lorem 圖元**產生器），在問題頂端新增標誌。 新增下列程式碼做為**div**元素的第一個子專案，並將**container**當做**類別**值，然後按**tab**鍵。

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample3.css)]
11. 程式碼應展開為 HTML。

    ![自動產生的 Lorem 圖元](visual-studio-2013-web-tools/_static/image11.png "自動產生的 Lorem 圖元")

    *自動產生的 Lorem 圖元*

    > [!NOTE]
    > 在 Zen 程式碼撰寫過程中，您也可以直接在 HTML 編輯器中產生 Lorem 圖元的程式碼。 只要輸入**pix-200x200-動物**並按**TAB 鍵**，就會插入含有動物200x200 影像的**img**標記。 如需詳細資訊，請參閱[Lorem 圖元](http://www.lorempixel.com)。
12. 按一下 [重新整理**連結的瀏覽器**] 按鈕，以更新這兩個瀏覽器。

    ![Internet Explorer-自動產生的影像和文字](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer-自動產生的影像和文字")

    *Internet Explorer-自動產生的影像和文字*

    ![Google Chrome-自動產生的影像和文字](visual-studio-2013-web-tools/_static/image13.png "Google Chrome-自動產生的影像和文字")

    *Google Chrome-自動產生的影像和文字*

    > [!NOTE]
    > 由於新增程式碼片段時，會隨機選取影像，因此瀏覽器中顯示的影像可能會不同。
13. 請勿關閉瀏覽器。 您將在下一項工作中使用它們。

<a id="Ex1Task3"></a>
#### <a name="task-3---updating-a-style-property"></a>工作 3-更新樣式屬性

在這項工作中，您將使用瀏覽器連結的 [**檢查模式]** 功能來偵測產生特定 DOM 元素的確切位置，然後使用 Web Essentials 所提供的色彩選擇器來更新該專案的 color 屬性。

1. 在 Internet Explorer 瀏覽器中，按**CTRL** + **ALT** + **I**以啟用 [檢查] 模式。
2. 將指標移到淺藍色框線上，然後按一下。

    ![將指標移到淺藍色框線上](visual-studio-2013-web-tools/_static/image14.png "將指標移到淺藍色框線上")

    *將指標移到淺藍色框線上*
3. 切換回 Visual Studio。 請注意，在 [Visual Studio HTML 編輯器] 中，也會選取您在瀏覽器中選取的 HTML 元素。

    ![在 Visual Studio HTML 編輯器中選取 HTML 元素](visual-studio-2013-web-tools/_static/image15.png "在 Visual Studio HTML 編輯器中選取 HTML 元素")

    *在 Visual Studio HTML 編輯器中選取 HTML 元素*
4. 您現在將更新**front** CSS 類別，以便變更所選項目的樣式。 若要這麼做，請按**CTRL** +  **，** 開啟 [**流覽至**搜尋] 方塊。 輸入**網站 .css** ，然後按**enter**鍵以開啟檔案。

    ![正在開啟檔案網站 .css](visual-studio-2013-web-tools/_static/image16.png "正在開啟檔案網站 .css")

    *正在開啟檔案網站 .css*
5. 按**CTRL** + **F**並輸入**flip-CONTAINER. front**以尋找 CSS 選取器。
6. 按一下類別之 [框線] 屬性中的淺藍色方塊，以開啟色彩選擇器。

    ![開啟色彩選擇器](visual-studio-2013-web-tools/_static/image17.png "開啟色彩選擇器")

    *開啟色彩選擇器*
7. 按一下箭號按鈕以展開色彩選擇器，然後選取新的色彩。

    ![展開色彩選擇器](visual-studio-2013-web-tools/_static/image18.png "展開色彩選擇器")

    *展開色彩選擇器*
8. 按**CTRL** + **ALT** + **enter**以重新整理連結的瀏覽器。
9. 切換到 Internet Explorer，並注意框線的色彩如何變更。

    ![Internet Explorer-框線色彩已更新](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer-框線色彩已更新")

    *Internet Explorer-框線色彩已更新*
10. 切換至 Google Chrome，並注意框線的色彩如何變更。

    ![Google Chrome-框線色彩已更新](visual-studio-2013-web-tools/_static/image20.png "Google Chrome-框線色彩已更新")

    *Google Chrome-框線色彩已更新*
11. 切換回 Visual Studio。
12. 移至**網站 .css**檔案的結尾，然後按**CTRL** + **F**以尋找**btn**選取器。
13. 請注意， **-webkit-border-radius**屬性會加上綠色的底線。

    ![-webkit-btn 選取器的邊界半徑屬性](visual-studio-2013-web-tools/_static/image21.png "-webkit-btn 選取器的邊界半徑屬性")

    *-webkit-btn 選取器的邊界半徑屬性*
14. 將插入號放在 **-webkit-border-radius**屬性中。 屬性之第一個單字的第一個字母底下應會出現藍線。 這是**智慧標籤**。
15. 按**CTRL** +  **。** 開啟 [建議] 功能表，然後按一下 [**新增遺漏的標準屬性（框線-半徑）** ]。

    ![新增遺漏的標準屬性建議](visual-studio-2013-web-tools/_static/image22.png "新增遺漏的標準屬性建議")

    *新增遺漏的標準屬性建議*
16. [**框線-半徑**] 屬性會自動新增至 [CSS 規則]。

    ![遺漏新增的標準屬性](visual-studio-2013-web-tools/_static/image23.png "遺漏新增的標準屬性")

    *遺漏新增的標準屬性*
17. 將指標移到 [**框線半徑**] 屬性上方，以顯示**瀏覽器矩陣工具提示**。 **瀏覽器矩陣工具提示**會顯示每個瀏覽器中屬性的可用性。

    ![瀏覽器矩陣工具提示](visual-studio-2013-web-tools/_static/image24.png "瀏覽器矩陣工具提示")

    *瀏覽器矩陣工具提示*
18. 請注意，[**框線-半徑**] 屬性的值仍會加上底線。 將指標移到值上方，以查看警告訊息。

    ![框線-radius 屬性值警告](visual-studio-2013-web-tools/_static/image25.png "框線-radius 屬性值警告")

    *框線-radius 屬性值警告*
19. 移除工具提示所建議的**框線-radius**屬性值單位。
20. As **border-半徑**是定義圓角框線角落的標準屬性，您可以從 CSS 規則中移除 **-webkit-border-radius**屬性和值。
21. 將插入號放在**自動換行**屬性中，並注意智慧標籤也會出現在下方。
22. 開啟功能表，然後按一下 [**新增遺漏的廠商詳細資訊**]。

    ![新增缺少的廠商詳細資訊建議](visual-studio-2013-web-tools/_static/image26.png "新增缺少的廠商詳細資訊建議")

    *新增缺少的廠商詳細資訊建議*
23. **-Ms-單字 wrap**屬性會自動新增至 CSS 規則。

    ![新增的廠商特定屬性](visual-studio-2013-web-tools/_static/image27.png "新增的廠商特定屬性")

    *新增的廠商特定屬性*

<a id="Ex1Task4"></a>
#### <a name="task-4---updating-the-html-code-from-the-browser"></a>工作 4-從瀏覽器更新 HTML 程式碼

在這項工作中，您將使用瀏覽器連結的 [**設計模式]** 功能，從瀏覽器編輯 DOM 物件，並將變更傳送至 Visual Studio 中的 HTML 原始程式檔。

1. 在 Google Chrome 中，按**CTRL** + **ALT** + **D**以啟用設計模式。
2. 將指標移到**Lorem Ipsum dolor sit amet**標籤上，然後按一下。

    ![編輯問題](visual-studio-2013-web-tools/_static/image28.png "編輯問題")

    *編輯問題*
3. 游標應該會出現。 *當我撰寫較長的問題時*，將原始文字取代為它看起來的樣子，然後按**ESC**鍵結束設計模式。

    ![已編輯問題](visual-studio-2013-web-tools/_static/image29.png "已編輯問題")

    *已編輯問題*
4. 切換回 Visual Studio 並開啟 [ **Index**] （如果尚未開啟）。 請注意，已更新 **&lt;p&gt;** 元素的內部文字。

    ![HTML 網頁中的已更新問題](visual-studio-2013-web-tools/_static/image30.png "HTML 網頁中的已更新問題")

    *HTML 網頁中的已更新問題*

<a id="Ex1Task5"></a>
#### <a name="task-5---reviewing-seo-related-warnings"></a>工作 5-查看 SEO 相關警告

**搜尋引擎優化**（SEO）是在搜尋引擎的結果清單上讓網站排名更高的流程。 網站排名越高，列出的也越一致，網站就會從該搜尋引擎取得更多的訪客。 Web Essentials 包含可檢查 HTML 的分析工具、報告找到的問題，並提供修正的協助。

1. 移至 [ **View** ] 功能表，然後按一下 [**錯誤清單**] 以開啟 [**錯誤清單**] 視窗。

    ![在 [視圖] 功能表中錯誤清單](visual-studio-2013-web-tools/_static/image31.png "在 [視圖] 功能表中錯誤清單")

    *在 [視圖] 功能表中錯誤清單*
2. 請注意，有一個 SEO 警告，會通知頁面描述缺少 **&lt;的中繼&gt;** 標記。 按兩下 [SEO 警告] 專案加以修正。

    ![錯誤清單視窗](visual-studio-2013-web-tools/_static/image32.png "錯誤清單視窗")

    *錯誤清單視窗*
3. 在 [ **Web Essentials** ] 對話方塊中，按一下 **[是]** ，將描述插入 &lt;meta&gt; 標記。

    ![Web 基本知識對話方塊](visual-studio-2013-web-tools/_static/image33.png "Web 基本知識對話方塊")

    *Web 基本知識對話方塊*
4. **\_Layout**的編輯器隨即開啟，而且 **&lt;meta&gt;** 標記會自動加入至 HTML 檔案的**標頭**區段。

    ![_Layout 頁面中自動新增的中繼標記](visual-studio-2013-web-tools/_static/image34.png "_Layout 頁面中自動新增的中繼標記")

    *中繼標記自動新增至 \_版面配置頁*
5. 將**content**屬性的值變更為*GeekQuiz* ，並儲存檔案。

<a id="Exercise2"></a>
### <a name="exercise-2-taking-advantage-of-code-snippets-and-intellisense"></a>練習2：利用程式碼片段和 IntelliSense

使用 Web Essentials，HTML 編輯器已透過額外的功能擴充。 在此練習中，您會看到一些有助於開發 web 應用程式的新功能。

<a id="Ex2Task1"></a>
#### <a name="task-1---using-intellisense-in-html-documents"></a>工作 1-在 HTML 檔案中使用 IntelliSense

您會在這項工作中看到的第一項新功能，稱為**動態 IntelliSense**。 動態 IntelliSense 會讀取其他標記和屬性，以推斷您將使用的可能識別碼。

在這項工作中，您將建立新的 HTML 表單元素，其中包含標籤和輸入欄位。 接著，您會將**for**屬性新增至標籤，以將它系結至輸入，而且您會看到根據範圍內輸入之識別碼的 IntelliSense 建議。

1. 開啟**Web 的 Visual Studio Express 2013** ，以及位於**Source/Ex2-TakingAdvantageofCodeSnippetsandIntelliSense/Begin**資料夾中的**Begin .sln**解決方案。 或者，您可以繼續使用您在上一個練習中取得的解決方案。
2. 在**方案總管**中，開啟位於**Views** | **Home**資料夾中的**Index. cshtml**檔案。
3. 將下列表單加入&gt;元素的 **&lt;區段**內。

    （程式碼片段- *VisualStudio2013WebTooling* - *Ex2* - *格式*）

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample4.html)]
4. 輸入標記前面必須加上具有欄位描述的標籤。 在輸入標記之前新增下列標籤。

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample5.html)]
5. **&lt;標籤**的**for**屬性&gt;會指定標籤所系結的表單元素。 屬性的值應該等於相關元素的識別碼。 將**for**屬性新增至 **&lt;標籤&gt;** 元素。 如下圖所示，[IntelliSense] 方塊中會顯示 &quot;名稱&quot; 值，這取決於相同範圍內專案的識別碼（封閉的 **&lt;表單&gt;** ）。

    ![在 IntelliSense 中顯示識別碼](visual-studio-2013-web-tools/_static/image35.png "在 IntelliSense 中顯示識別碼")

    *在 IntelliSense 中顯示識別碼*
6. 刪除最近新增的 **&lt;表單&gt;** 元素和其內容。

<a id="Ex2Task2"></a>
#### <a name="task-2---using-html-code-snippets"></a>工作 2-使用 HTML 程式碼片段

HTML5 引進了超過25個新的語義標記。 Visual Studio 已經具有這些標記的 IntelliSense 支援，但 Visual Studio 2013 藉由新增程式碼片段，讓您更快速且更輕鬆地撰寫標記。 雖然這些標記並不複雜，但有幾個小微妙差異，例如新增*音訊*標記的正確編解碼器。 在這項工作中，您會看到音訊標記的 HTML 程式碼片段。

1. 在**Index. cshtml**檔案中，于 **&lt;區段&gt;** 元素內輸入 **&lt;aud** ，如下圖所示。

    ![插入音訊元素](visual-studio-2013-web-tools/_static/image36.png "插入音訊元素")

    *插入音訊元素*
2. 按兩次**tab**鍵，並注意如何在頁面上加入下列程式碼，並將游標放在第一個來源的**src**屬性上。

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample6.html)]

    > [!NOTE]
    > 按**tab**鍵兩次，即會插入程式碼片段。 [音訊] 程式碼片段會顯示*音訊*標記的標準使用方式，並提供兩個原始程式檔來改善支援。
3. 刪除第二行，並使用下列 WebCampsTV Katana show 的連結更新第一行的來源： [http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3)。 產生的程式碼如下所示。

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample7.html)]

    > [!NOTE]
    > 原始程式檔*KatanaProject*是用來作為範例。 如果您想要的話，可以使用另一個來源。
4. 按**CTRL** + **S**以儲存檔案。
5. 按**CTRL** + **F5**啟動應用程式。
6. 請注意，音訊播放機已新增至應用程式。

    ![Internet Explorer 中的音訊播放機](visual-studio-2013-web-tools/_static/image37.png "Internet Explorer 中的音訊播放機")

    *Internet Explorer 中的音訊播放機*

    ![Google Chrome 中的音訊播放機](visual-studio-2013-web-tools/_static/image38.png "Google Chrome 中的音訊播放機")

    *Google Chrome 中的音訊播放機*
7. 請勿關閉瀏覽器。 您將在下一項工作中使用它們。

<a id="Ex2Task3"></a>
#### <a name="task-3---using-intellisense-in-javascript-documents"></a>工作 3-在 JavaScript 檔中使用 IntelliSense

使用 Web Essentials 2013，樣式表單和 HTML 網頁會產生識別碼和類別名稱的清單。 在這項工作中，您將瞭解這些清單如何改善 Web Essentials 2013 中的 JavaScript IntelliSense 支援。

1. 在 [ **Index. cshtml** ] 檔案中，加入下列程式碼以定義 JavaScript 程式碼的**腳本**標記。

    [!code-cshtml[Main](visual-studio-2013-web-tools/samples/sample8.cshtml)]
2. 在**腳本**標記內加入下列程式碼，以定義就緒的回呼函數。

    （程式碼片段- *VisualStudio2013WebTooling* - *Ex2* - *ReadyFunction*）

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample9.js)]
3. 將插入號放在**腳本**標記中，然後按**CTRL** +  **。** 以開啟 [建議] 功能表。
4. 按一下 [**解壓縮至**檔案]。

    ![JavaScript 解壓縮至檔案建議](visual-studio-2013-web-tools/_static/image39.png "JavaScript 解壓縮至檔案建議")

    *JavaScript 解壓縮至檔案建議*
5. 在 [**另存**新檔] 視窗中，選取 [**腳本**] 資料夾，將檔案命名為**Init** ，然後按一下 [**儲存**]。

    ![另存新檔視窗](visual-studio-2013-web-tools/_static/image40.png "另存新檔視窗")

    *另存新檔視窗*

    > [!NOTE]
    > 隨即建立**init .js**檔案，並將腳本的內容移至檔案。
    > 
    > ![以包含的內容建立的 Init .js 檔案](visual-studio-2013-web-tools/_static/image41.png "以包含的內容建立的 Init .js 檔案")
    > 
    > *以包含的內容建立的 Init .js 檔案*
6. 開啟**Index. cshtml**檔案，並檢查腳本標記是否已取代為**init .js**檔案的參考。

    ![Init .js html 參考](visual-studio-2013-web-tools/_static/image42.png "Init .js html 參考")

    *Init .js html 參考*
7. 請移至**方案總管**，並注意**init .js**檔案已自動包含在方案中。

    ![方案中包含的 Init .js 檔案](visual-studio-2013-web-tools/_static/image43.png "方案中包含的 Init .js 檔案")

    *方案中包含的 Init .js 檔案*
8. 切換回**init .js**檔案，以更新**就緒**函式回呼。
9. 在傳遞至*ready*的函式回呼定義內，新增下列程式碼以取得特定類別屬性的所有專案。

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample10.js)]
10. 在**getElementsByClassName**函式呼叫內的引號之間，按**CTRL** + **空格鍵**。

    ![顯示 getElementsByClassName 函式的 IntelliSense](visual-studio-2013-web-tools/_static/image44.png "顯示 getElementsByClassName 函式的 IntelliSense")

    *顯示 getElementsByClassName 函式的 IntelliSense*

    > [!NOTE]
    > 請注意，IntelliSense 會顯示專案樣式表單中定義的類別。
11. 以下列程式碼取代您所建立的行。

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample11.js)]
12. 將游標放在**getElementsByTagName**函式中引號內的**au**後面，然後按**CTRL** + **空格鍵**。

    ![顯示 getElementByTagName 方法的 IntelliSense](visual-studio-2013-web-tools/_static/image45.png "顯示 getElementByTagName 方法的 IntelliSense")

    *顯示 getElementsByTagName 方法的 IntelliSense*
13. 從清單中選取 **&quot;音訊&quot;** ，然後按**enter**鍵。 其結果如下圖所示。

    ![正在抓取音訊元素](visual-studio-2013-web-tools/_static/image46.png "正在抓取音訊元素")

    *正在抓取音訊元素*
14. 在**方案總管**中，以滑鼠右鍵按一下 [**腳本**] 資料夾中的 [ **init** ] 檔案，然後從 [ **Web Essentials** ] 功能表中選取 [**縮小 JavaScript**檔案]。

    ![縮小 JavaScript 檔案](visual-studio-2013-web-tools/_static/image47.png "縮小 JavaScript 檔案")

    *縮小 JavaScript 檔案*
15. 當來源檔案變更時，系統提示您啟用自動縮制時，請按一下 **[是]** 。

    ![啟用自動縮制警告](visual-studio-2013-web-tools/_static/image48.png "啟用自動縮制警告")

    *啟用自動縮制警告*

    > [!NOTE]
    > 隨即建立**init. min .js** ，並加入作為**init**檔案的相依性。
    > 
    > ![已建立 Init. min .js 檔案](visual-studio-2013-web-tools/_static/image49.png "已建立 Init. min .js 檔案")
    > 
    > *已建立 Init. min .js 檔案*
16. 開啟**init. min .js**檔案，並注意檔案是縮減。

    ![Init. min .js 檔案內容](visual-studio-2013-web-tools/_static/image50.png "Init. min .js 檔案內容")

    *Init. min .js 檔案內容*
17. 在**init .js**檔案中，將下列程式碼新增至**getElementsByTagName**函式呼叫下方，以播放所有的音訊元素。

    （程式碼片段- *VisualStudio2013WebTooling* - *Ex2* - *PlayAudioElements*）

    [!code-csharp[Main](visual-studio-2013-web-tools/samples/sample12.cs)]
18. 按一下**CTRL** + **S**以儲存檔案。 由於縮減檔案已開啟，您會看到一個對話方塊，指出檔案已在原始檔編輯器之外修改過。 按一下 [ **是**]。

    ![Microsoft Visual Studio 警告](visual-studio-2013-web-tools/_static/image51.png "Microsoft Visual Studio 警告")

    *Microsoft Visual Studio 警告*
19. 切換回**init. min .js**檔案，確認已使用新的程式碼更新檔案。

    ![已更新 Init. 最小 .js 檔案](visual-studio-2013-web-tools/_static/image52.png "已更新 Init. 最小 .js 檔案")

    *已更新 Init. 最小 .js 檔案*
20. 按一下 [**瀏覽器連結**重新整理] 按鈕。
21. 這兩個瀏覽器都重新整理後，您在上一項工作中看到的音訊播放機將會自動開始播放。

    ![包含在 view 中的音訊播放機](visual-studio-2013-web-tools/_static/image53.png "包含在 view 中的音訊播放機")

    *包含在 view 中的音訊播放機*

---

<a id="Summary"></a>
## <a name="summary"></a>總結

藉由完成此實際操作實驗室，您已瞭解如何：

- 使用 Web Essentials 中包含的新 HTML 編輯器功能，例如豐富的 HTML5 程式碼片段和 Zen 編碼
- 使用 Web Essentials 中包含的新 CSS 編輯器功能，例如色彩選擇器和瀏覽器矩陣工具提示
- 使用 Web Essentials 中包含的新 JavaScript 編輯器功能，例如 [解壓縮至檔案] 和 [IntelliSense]，適用于所有 HTML 元素
- 使用瀏覽器連結在瀏覽器與 Visual Studio 之間交換資料
