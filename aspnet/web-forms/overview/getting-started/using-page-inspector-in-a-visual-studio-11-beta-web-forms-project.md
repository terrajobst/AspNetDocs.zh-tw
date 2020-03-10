---
uid: web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
title: 在 ASP.NET Web Forms 中使用適用于 Visual Studio 2012 的 Page Inspector |Microsoft Docs
author: rick-anderson
description: Visual Studio 2012 的 Page Inspector 是具有整合式瀏覽器的 網頁程式開發工具。 選取整合式瀏覽器中的任何元素，然後 Page Inspector 。
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 2ece0bf4-aae5-4ff4-8f62-28e0819d4f86
msc.legacyurl: /web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: c165bbea505b4cb8eae1312cdd587f4ed36541a0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78575919"
---
# <a name="using-page-inspector-for-visual-studio-2012-in-aspnet-web-forms"></a>在 ASP.NET Web Forms 中使用 Page Inspector for Visual Studio 2012

依 Tim Ammann

> Visual Studio 2012 的 Page Inspector 是具有整合式瀏覽器的 網頁程式開發工具。 選取整合式瀏覽器中的任何元素，Page Inspector 立即反白顯示專案的來源和 CSS。 您可以流覽應用程式中的任何頁面，快速尋找轉譯標記的來源，並直接在 Visual Studio 環境中使用瀏覽器工具。
> 
> 本教學課程示範如何啟用檢查模式，然後在您的 Web 專案中快速找出並編輯 CSS 規則和文字。 本教學課程使用 Web Forms 應用程式專案，但您也可以使用網站專案和[MVC](https://go.microsoft.com/?linkid=9802002)應用程式的 Page Inspector。
> 
> 本教學課程包含下列各節：
> 
> [必要條件](#_1_prerequisites)
> 
> [建立 Web 應用程式](#_2_creating_a)
> 
> [使用 Page Inspector 來查看應用程式](#_3_using_page)
> 
> [啟用檢查模式](#_4_inspection_mode)
> 
> [使用 Page Inspector 對標記進行變更](#_5_using_page)
> 
> [檢查模式和 HTML 視窗](#_6_inspection_mode)
> 
> [[樣式] 視窗中的預覽 CSS 變更](#_7_previewing_css)
> 
> [CSS 自動同步處理](#css_auto_sync)
> 
> [使用 CSS 色彩選擇器](#css_color_picker)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a>Prerequisites

- [適用于 Web 的](https://www.microsoft.com/visualstudio/11/downloads#express-web) [Visual Studio 2012](https://www.microsoft.com/visualstudio/11)或 Visual Studio Express 2012。

> [!NOTE]
> 若要取得最新版本的 Page Inspector，請使用[Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386)來安裝 Azure SDK for .net 2.0。

Page Inspector 與 Microsoft Web Developer Tools 配套。 最新版本是1.3。 若要檢查您擁有哪個版本，請執行**Visual Studio，然後從 [說明**] 功能表中選取 [**關於 Microsoft Visual Studio** ]。

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a>建立 Web 應用程式

首先，您將建立要搭配 Page Inspector 使用的 web 應用程式。 在 Visual Studio 中，**選擇 [** 檔案] &gt; [**新增專案**]。 在左側，展開 [**視覺C#效果**]，選取 [ **Web**]，然後選取 [ **ASP.NET Web Forms 應用程式**]。

![新的 Web Forms 應用程式](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image1.png)

按一下 [確定]。

應用程式會在**原始**檔視圖中開啟。

![來源視圖中的新 Web Forms 應用程式](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image2.png)

現在您已經有要使用的應用程式，您可以使用 Page Inspector 來檢查及修改它。

<a id="_starting_page_inspector"></a><a id="_3_starting_page"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-view-the-application"></a>使用 Page Inspector 來查看應用程式

接下來，您將使用 Page Inspector 來觀看應用程式。 在**方案總管**中，以滑鼠右鍵按一下專案，然後選擇 [**在 Page Inspector 中顯示**]。

![在 Page Inspector 中檢視](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image3.png)

根據預設，當 Page Inspector 第一次啟動時，它會停駐在 Visual Studio 環境左側的縮小視窗。 將它停駐在左側，並將它設為您慣用的寬度，或將它固定在頂端、底部或右邊的其中一個工具區域中：

![Page Inspector 銜接位置](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image4.png)

如果您停用 [Page Inspector] 視窗，則可以將它放在 Visual Studio 之外，甚至是在第二個監視器上（如果有的話）。 不過，若要在 Page Inspector 視窗停駐時，Page Inspector 和 Visual Studio 之間進行 ALT + TAB，請移至 **工具**&gt;**選項** &gt;**環境**&gt; 索引標籤**和 視窗**，然後在 索引標籤 底下，清除名為 **浮動工具視窗** 的核取方塊： 一律保留

![清除 [浮動工具視窗] 核取方塊，以在 Visual Studio 和停駐的 Page Inspector 視窗之間進行 ALT + TAB](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image5.png)

[Page Inspector] 視窗的上方窗格會在瀏覽器視窗中顯示目前的頁面。 底部窗格會在左側顯示 HTML 標籤中的頁面，以及右邊的一些索引標籤，可讓您檢查頁面的不同層面。 底部窗格類似 Internet Explorer 中的[F12 開發人員工具](https://msdn.microsoft.com/ie/aa740478)。 （不過，與開發人員工具不同的是，您可以直接在 Visual Studio 中使用 Page Inspector）。

![Page Inspector](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image6.png)

在本教學課程中，您將使用 [Page Inspector 瀏覽器] 窗格，以及 [ **HTML** ] 和 [**樣式**] 索引標籤，協助您快速流覽並變更應用程式。

<a id="_4_inspection_mode"></a>
## <a name="enable-inspection-mode"></a>啟用檢查模式

接下來，您會看到 Page Inspector 的檢查模式運作方式。 在 [Page Inspector] 視窗中，按一下 [**檢查**] 按鈕。

![檢查元素](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image7.png)

若要查看作用中的檢查模式，請將滑鼠移至 [Page Inspector 瀏覽器] 視窗中頁面的不同部分。 就像您一樣，滑鼠指標會變更為較大的加號，而下方的元素會反白顯示：

![將滑鼠停留在 div. 內容包裝函式](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image8.png)

當您移動滑鼠指標時，請注意

- **來源**視圖中的內容會變更，以顯示與頁面上所選項目對應的標記。 相關的標記會反白顯示。 如果來源位於另一個檔案中，則會在原始檔中開啟該檔案，並反白顯示相關的標記。

- 在 Page Inspector 的 [ **HTML** ] 索引標籤中顯示的標記也會變更，以對應至頁面上所選取的元素。 在 [ **HTML** ] 索引標籤中，會列出相關的標記。

- [**樣式**] 索引標籤會顯示與目前選取專案相關的 CSS 規則。

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a>使用 Page Inspector 對標記進行變更

現在您將瞭解如何使用 Page Inspector 來尋找和變更位置可能不會立即明顯的標記或文字。

將 Page Inspector 放在檢查模式中，然後在首頁的底部進行滾動。

一旦您輸入頁尾區域，Page Inspector 會在 [**來源**視圖] 中，于 [其他] 索引標籤右邊的暫時索引標籤中開啟 [*網站*] 設定檔案，並反白顯示您所選取之主版頁面的區段。 這會向您示範 Page Inspector 如何在頁面上尋找和顯示內容，而這可能實際上來自于您原本開啟的檔案。

![檢查模式中的頁尾醒目提示](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image9.png)

在 [Page Inspector 瀏覽器] 視窗中，將滑鼠指標移到具有著作權<a id="a"></a>注意事項的那一行。

在 [*網站*] 頁面中，會反白顯示對應的一行。

![已反白顯示頁尾的著作權線](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image10.png)

將一些文字加入至*網站*結尾檔案中的行尾。

&lt;p&gt;&amp;複製;&lt;%： DateTime。現在. 年%&gt;-我的 ASP.NET 應用程式 Rocks！&lt;/p&gt;

現在，按下 Ctrl + Alt + Enter，或按一下更新列以在 [Page Inspector 瀏覽器] 視窗中查看結果。

![我的 ASP.NET 應用程式 Rocks！](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image11.png)

您可能已經認為頁尾是在*default.aspx*頁面上，但是它已經放在主要版面配置頁面中，Page Inspector 找到它。

<a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a>檢查模式和 HTML 視窗

接下來，您將快速查看 [HTML] 視窗，以及它如何為您對應元素。

將 Page Inspector 放在檢查模式中。

![檢查元素](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image12.png)

按一下頁面的上半部，此處會顯示「您的標誌」。 您正以更詳細的方式檢查特定元素，因此當您移動滑鼠指標時，瀏覽器視窗中的顯示不會再變更。

現在，將滑鼠指標移至**HTML**視窗。 當您移動滑鼠指標時，Page Inspector 會在**HTML**視窗中概述元素，並在瀏覽器視窗中反白顯示對應的元素。

![HTML 視窗](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image13.png)

如同之前一樣，Page Inspector 會在暫存索引標籤中開啟*網站*檔案。按一下 [網站] 索引標籤，即可在 [&lt;標題]&gt; 區段中反白顯示對應的標記：

![反白顯示的標記](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image14.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a>[樣式] 視窗中的預覽 CSS 變更

接下來，您將瞭解如何使用 [Page Inspector**樣式**] 視窗，預覽 CSS 的變更。

按一下 [**檢查**] 按鈕，將 Page Inspector 放在檢查模式中。

在 [Page Inspector 瀏覽器] 視窗中，將滑鼠指標移到 [首頁] 區段上，直到 [ **div. content-包裝函式**] 標籤出現為止。

![將滑鼠停留在元素上](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image15.png)

在 [div] [內容包裝函式] 區段中按一下一次，然後將滑鼠指標移至 [**樣式**] 視窗。 在 [專題-包裝函式類別] 選取器底下，清除並選取 [背景色彩] 屬性的核取方塊。

![清除背景色彩](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image16.png)

請注意，[Page Inspector 瀏覽器] 視窗中的變更預覽會立即進行。

再次選取此核取方塊，然後按兩下屬性值並將它變更為 `red`。 變更會立即顯示：

![紅色背景色彩](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image17.png)

[**樣式**] 視窗可讓您在認可樣式表單本身的變更之前，輕鬆地測試和預覽 CSS 變更。

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a>CSS 自動同步處理

> [!NOTE]
> 這項功能需要1.3 版的 Page Inspector。

CSS 自動同步處理功能可讓您直接編輯 CSS 檔案，並在 Page Inspector 瀏覽器中立即查看變更。

按一下 [**檢查**]，將 Page Inspector 放在檢查模式中。

在 Page Inspector 瀏覽器中，將滑鼠指標移到 [首頁] 區段上，直到 [ **div. content-包裝函式**] 標籤出現為止。 按一下 [一次] 以選取此元素。

[**樣式**] 視窗會顯示此元素的所有 CSS 規則。 向下滾動以尋找 [精選] [內容包裝函式類別] 選取器。 按一下 [. 功能內容-包裝函式]。 Page Inspector 會開啟定義此樣式（.css）的 CSS 檔案，並反白顯示對應的 CSS 樣式。

![CSS 檔案](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image18.png)

現在將 `background-color` 的值變更為「紅色」。 變更會立即出現在 Page Inspector 瀏覽器中。

![Page Inspector 瀏覽器](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image19.png)

<a id="css_color_picker"></a>

## <a name="using-the-css-color-picker"></a>使用 CSS 色彩選擇器

接下來，您將瞭解如何使用 Page Inspector 來快速尋找並變更預設應用程式中反白顯示文字的 CSS。 在此範例中，您已決定不喜歡藍色反白顯示，而且想要將它變更為另一個色彩。

按一下 [**檢查**] 按鈕。

![檢查元素](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image20.png)

在 [Page Inspector 瀏覽器] 視窗中，將滑鼠指標移至反白顯示的 [影片、教學課程和範例] 文字上方，以顯示 CSS "mark" 標籤。

![將滑鼠停留在 mark 元素上方](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image21.png)

按一下以選取文字。 對應的 CSS 標記選取器會出現在 [**樣式**] 視窗的底部。

![[樣式] 視窗中的標記選取器](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image22.png)

按一下標記選取器。 這會開啟 web 應用程式的*網站 .css*檔案。 按一下 [網站 .css] 索引標籤，就會反白顯示選取器的對應 CSS：

![在樣式表單中標記選取器](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image23.png)

選取並移除具有背景色彩屬性的行。

您現在將使用新的 Visual Studio 2012 CSS 色彩選擇器，為 [**標記**背景色彩] 屬性選擇新的色彩。

<a id="_using_the_visual"></a>

### <a name="using-the-visual-studio-2012-css-color-picker"></a>使用 Visual Studio 2012 CSS 色彩選擇器

Visual Studio 2012 中的 CSS 編輯器具有色彩選擇器，可讓您輕鬆地選擇和插入色彩。 它有一個簡單的色軸和一個可提供更細微控制的「快顯」選擇器。

色彩選擇器包含色彩的標準調色板、支援標準色彩名稱、雜湊碼、RGB、RGBA、HSL 和 HSLA 色彩，並維護您最近在檔中使用的色彩清單。

在背景色彩屬性所在的行上輸入 "bc"，然後按向下鍵一次。

當您輸入以連字號分隔的屬性（例如「背景色彩」）中每個單字的第一個字元時，IntelliSense 會篩選清單，讓您只顯示符合的屬性：

![Intellisense 篩選值](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image24.png)

現在輸入冒號。 當您這麼做時，就會插入完整的背景色彩屬性名稱。 輸入 **#** 或**rgb （** ，並顯示色彩選擇器列：

![CSS 色彩選擇器列](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image25.png)

若要查看色彩選擇器列的運作方式，請按一下滑鼠指標的色彩，或按向下鍵，然後使用向左鍵和向右鍵來流覽色彩。 當您造訪色彩時，會預覽背景色彩屬性的對應值：

![預覽的背景色彩屬性值](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image26.png)

此時，您可以按 Enter 鍵來選取值，然後按分號（;)以完成 CSS 專案。 現在請移至下一節，讓您可以看到色彩選擇器快顯的運作方式。

#### <a name="using-the-color-picker-pop-down"></a>使用色彩選擇器快顯視窗

當色軸沒有您要尋找的確切色彩時，您可以使用 [色彩選擇器] 快顯視窗。

若要開啟它，請按一下色軸右端的雙燕號，或在鍵盤上按一次向下箭號或按兩次。

![CSS 色彩選擇器快顯視窗](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image27.png)

按一下右側分隔號的色彩。 這會在主視窗中顯示該色彩的漸層。 按 Enter 鍵直接從分隔號中選擇色彩，或按一下主視窗中的任何點，選擇較高的精確度。

如果您的電腦畫面上有您想要使用的色彩（不一定要在 Visual Studio 使用者介面內），您可以使用右下方的 [滴管] 工具來捕捉其值。

您也可以移動色彩選擇器底部的滑杆來變更色彩的不透明度。 這麼做會將色彩值變更為 RGBA 值，因為 RGBA 格式可以代表不透明度。

選擇色彩之後，請按 Enter 鍵，然後輸入分號來完成*網站 .css*檔案中的背景色彩專案。

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a>Page Inspector 更新列

Page Inspector 會立即偵測到*網站 .css*檔案的變更（或應用程式中的任何檔案），並在更新列中顯示警示。

![更新列](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image28.png)

若要儲存所有檔案並重新整理 Page Inspector 的瀏覽器，請按 Ctrl + Alt + Enter，或按一下更新列。 醒目提示色彩中的變更會出現在瀏覽器中：

![反白顯示色彩已變更](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image29.png)

<a id="_using_page_inspector_1"></a>請注意，您可以直接從 Visual Studio 環境中，輕鬆地重新整理 Page Inspector 瀏覽器。 使用 Page Inspector 而非外部瀏覽器，可讓您在開發 web 應用程式時保持在編輯器中。

## <a name="see-also"></a>另請參閱

[Page Inspector 簡介](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector)（Channel 9 影片）

[Page Inspector 錯誤訊息](https://go.microsoft.com/?linkid=9813062)（MSDN）
