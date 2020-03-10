---
uid: mvc/overview/views/using-page-inspector-in-aspnet-mvc
title: 在 ASP.NET MVC 中使用 Page Inspector |Microsoft Docs
author: rick-anderson
description: Visual Studio 2012 中的 Page Inspector 是具有整合式瀏覽器的 網頁程式開發工具。 在整合式瀏覽器中選取任何專案，然後 Page Inspector 。
ms.author: riande
ms.date: 08/15/2012
ms.assetid: c7e4e1ab-4932-4614-9f53-aaf7c706d498
msc.legacyurl: /mvc/overview/views/using-page-inspector-in-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 5da3e142c52a770f59222c21d9f9a53cbbdbf498
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78538014"
---
# <a name="using-page-inspector-in-aspnet-mvc"></a>在 ASP.NET MVC 中使用 Page Inspector

依 Tim Ammann

> Visual Studio 2012 中的 Page Inspector 是具有整合式瀏覽器的 網頁程式開發工具。 選取整合式瀏覽器中的任何元素，Page Inspector 立即反白顯示專案的來源和 CSS。 您可以流覽任何 MVC 視圖，快速尋找轉譯標記的來源，並直接在 Visual Studio 環境中使用瀏覽器工具。
> 
> [觀看影片](../../videos/mvc-4/using-page-inspector-in-aspnet-mvc.md)
> 
> 本教學課程示範如何啟用檢查模式，然後在您的 Web 專案中快速找出並編輯標記和 CSS。 本教學課程使用 MVC 專案，但您也可以將 Page Inspector 用於[Web Forms](https://go.microsoft.com/?linkid=9802001)和其他 ASP.NET 應用程式。
> 
> 本教學課程包含下列各節：
> 
> - [必要條件](#_1_prerequisites)
> - [建立 Web 應用程式](#_2_creating_a)
> - [使用 Page Inspector 流覽至視圖](#_3_using_page)
> - [啟用檢查模式](#_4_inspection_mode)
> - [使用 Page Inspector 對標記進行變更](#_5_using_page)
> - [檢查模式和 HTML 視窗](#_6_inspection_mode)
> - [[樣式] 視窗中的預覽 CSS 變更](#_7_previewing_css)
> - [CSS 自動同步處理](#css_auto_sync)
> - [使用 CSS 色彩選擇器](#css_color_picker)
> - [將動態頁面元素對應至 JavaScript](#map_dynamic_elements)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a>Prerequisites

- [適用于 Web 的](https://www.microsoft.com/visualstudio/11/downloads#express-web) [Visual Studio 2012](https://www.microsoft.com/visualstudio/11)或 Visual Studio Express 2012。

> [!NOTE]
> 若要取得最新版本的 Page Inspector，請使用[Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386)安裝適用于 .net 2.0 的 WINDOWS Azure SDK。

Page Inspector 與 Microsoft Web Developer Tools 配套。 最新版本是1.3。 若要檢查您擁有哪個版本，請執行**Visual Studio，然後從 [說明**] 功能表中選取 [**關於 Microsoft Visual Studio** ]。

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a>建立 Web 應用程式

首先，建立您將搭配 Page Inspector 使用的 web 應用程式。 在 Visual Studio 中，**選擇 [** 檔案] &gt; [**新增專案**]。 在左側，展開 [**視覺C#效果**]，選取 [ **Web**]，然後選取 [ **ASP.NET MVC4 Web 應用程式**]。

![新增 ASP.NET MVC 應用程式](using-page-inspector-in-aspnet-mvc/_static/image2.png)

按一下 [確定]。

在 [**新增 ASP.NET MVC 4 專案**] 對話方塊中，選取 [**網際網路應用程式**]。 保留**Razor**做為預設的 view engine。

![新增 ASP.NET MVC 專案-網際網路應用程式](using-page-inspector-in-aspnet-mvc/_static/image4.png)

應用程式會在**原始**檔視圖中開啟。

![來源視圖中的新 ASP.NET MVC 應用程式](using-page-inspector-in-aspnet-mvc/_static/image6.png)

現在您已經有要使用的應用程式，您可以使用 Page Inspector 來檢查及修改它。

<a id="_starting_page_inspector"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-browse-to-a-view"></a>使用 Page Inspector 流覽至視圖

在 Visual Studio 2012 中，您可以用滑鼠右鍵按一下專案中的任何視圖、選取  **Page Inspector 中**的 view，然後 Page Inspector 將會找出路線並顯示該頁面。

在**方案總管**中，依序展開 [ **Views** ] 資料夾和 [ **Home** ] 資料夾。 以滑鼠右鍵按一下索引. cshtml 檔案，然後選擇 [ **View in Page Inspector**]。

![Page Inspector 中的 View Index. cshtml](using-page-inspector-in-aspnet-mvc/_static/image8.png)

根據預設，Page Inspector 會停駐在 Visual Studio 環境左側的視窗中。 如果您想要的話，可以將它停駐在別處，或停用視窗。 請參閱[如何：排列和停駐視窗](https://msdn.microsoft.com/library/z4y0hsax.aspx)。

[Page Inspector] 視窗的上方窗格會在瀏覽器視窗中顯示目前的頁面。 下方窗格會顯示 HTML 標籤中的頁面，以及一些可讓您檢查頁面不同層面的索引標籤。 底部窗格類似 Internet Explorer 中的[F12 開發人員工具](https://msdn.microsoft.com/ie/aa740478)。

![Page Inspector 中的 ASP.NET MVC 應用程式](using-page-inspector-in-aspnet-mvc/_static/image10.png)

在本教學課程中，您將使用 [ **HTML** ] 和 [**樣式**] 索引標籤，快速流覽並對應用程式進行變更。

<a id="_examining_(&quot;decomposing&quot;)_the"></a><a id="_inspection_mode_and"></a><a id="_4_inspection_mode"></a>

## <a name="enableinspection-mode"></a>EnableInspection 模式

若要將 Page Inspector 放入檢查模式，請按一下 [**檢查**] 按鈕。 在檢查模式中，當您將滑鼠指標放在呈現頁面的任何部分上方時，對應的來源標記或程式碼會反白顯示。

![切換檢查模式](using-page-inspector-in-aspnet-mvc/_static/image12.png)

現在將您的滑鼠移到 Page Inspector 內不同的頁面部分。 就像您一樣，滑鼠指標會變更為較大的加號，而下方的元素會反白顯示：

![將滑鼠停留在 div. 內容包裝函式](using-page-inspector-in-aspnet-mvc/_static/image14.png)

當您移動滑鼠指標時，Visual Studio 會反白顯示原始檔案中對應的 Razor 語法。 如果 HTML 元素來自另一個原始檔，Visual Studio 會自動開啟檔案。

在 Page Inspector 中，[ **html** ] 索引標籤會顯示從 Razor 語法產生的 html。 當您移動滑鼠指標時，HTML 元素會反白顯示。 [**樣式**] 索引標籤會顯示元素的 CSS 規則。

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a>使用 Page Inspector 對標記進行變更

Page Inspector 可讓您尋找其位置可能不明顯的標記。 然後您可以修改標記，並查看所產生的變更。

若要查看此功能，請按一下 [**檢查**]，然後在 [Page Inspector] 視窗中的頁面底部流覽。

當您將滑鼠指標移至頁尾區域時，Page Inspector 會開啟 \_配置 cshtml 檔案，並反白顯示您所選取之版面配置頁的區段。 如您所見，頁尾是定義在版面配置檔案中，而不是在 view 本身。

![頁尾](using-page-inspector-in-aspnet-mvc/_static/image16.png)

現在，將滑鼠指標移到具有著作權<a id="a"></a>注意事項的那一行。 在 [\_配置. cshtml] 頁面中，會反白顯示對應的一行。

![已反白顯示頁尾的著作權線](using-page-inspector-in-aspnet-mvc/_static/image18.png)

將一些文字新增至 \_配置. cshtml 檔案中的行尾。

&lt;p&gt;&amp;複製;@DateTime.Now.Year-我的 ASP.NET MVC 應用程式 Rocks！&lt;/p&gt;

現在，按下 Ctrl + Alt + Enter，或按一下更新列以在 [Page Inspector 瀏覽器] 視窗中查看結果。

![我的 ASP.NET 應用程式 Rocks！](using-page-inspector-in-aspnet-mvc/_static/image20.png)

您可能認為頁尾中定義了頁尾，但它是在 \_配置. cshtml 中，而 Page Inspector 為您找到它。

<a id="_inspection_mode_and_1"></a><a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a>檢查模式和 HTML 視窗

接下來，您將快速查看 [HTML] 視窗，以及它如何為您對應元素。

按一下 [**檢查**]，將 Page Inspector 放在檢查模式中。

按一下頁面的上半部，此處會顯示「您的標誌」。 您正以更詳細的方式檢查特定元素，因此當您移動滑鼠指標時，瀏覽器視窗中的顯示不會再變更。

現在，將滑鼠指標移至**HTML**視窗。 當您移動滑鼠指標時，Page Inspector 會在**HTML**視窗中概述元素，並在瀏覽器視窗中反白顯示對應的元素。

![HTML 視窗](using-page-inspector-in-aspnet-mvc/_static/image22.png)

如同之前一樣，Page Inspector 會在暫存索引標籤中開啟 \_的配置. cshtml 檔案。按一下 [\_配置] [暫存] 索引標籤，在 &lt;標頭&gt; 區段中會反白顯示對應的標記：

![反白顯示的標記](using-page-inspector-in-aspnet-mvc/_static/image24.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a>[樣式] 視窗中的預覽 CSS 變更

接下來，您將使用 [Page Inspector**樣式**] 視窗，預覽 CSS 的變更。

按一下 [**檢查**]，將 Page Inspector 放在檢查模式中。

在 [Page Inspector 瀏覽器] 視窗中，將滑鼠指標移到 [首頁] 區段上，直到 [ **div. content-包裝函式**] 標籤出現為止。

![將滑鼠停留在 div. 內容包裝函式](using-page-inspector-in-aspnet-mvc/_static/image26.png)

在 [div] [內容包裝函式] 區段中按一下一次，然後將滑鼠指標移至 [**樣式**] 視窗。 [**樣式**] 視窗會顯示此元素的所有 CSS 規則。 向下滾動以尋找 [精選] [內容包裝函式類別] 選取器。 現在清除 [背景色彩] 屬性的核取方塊。

![清除背景色彩](using-page-inspector-in-aspnet-mvc/_static/image28.png)

請注意，[Page Inspector 瀏覽器] 視窗中的變更預覽會立即進行。

再次選取此核取方塊，然後按兩下屬性值並將它變更為紅色。 變更會立即顯示：

![紅色背景色彩](using-page-inspector-in-aspnet-mvc/_static/image30.png)

[**樣式**] 視窗可讓您在認可樣式表單本身的變更之前，輕鬆地測試和預覽 CSS 變更。

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a>CSS 自動同步處理

> [!NOTE]
> 這項功能需要1.3 版的 Page Inspector。

CSS 自動同步處理功能可讓您直接編輯 CSS 檔案，並在 Page Inspector 瀏覽器中立即查看變更。

按一下 [**檢查**]，將 Page Inspector 放在檢查模式中。

在 Page Inspector 瀏覽器中，將滑鼠指標移到 [首頁] 區段上，直到 [ **div. content-包裝函式**] 標籤出現為止。 按一下 [一次] 以選取此元素。

[**樣式**] 視窗會顯示此元素的所有 CSS 規則。 向下滾動以尋找 [精選] [內容包裝函式類別] 選取器。 按一下 [. 功能內容-包裝函式]。 Page Inspector 會開啟定義此樣式（.css）的 CSS 檔案，並反白顯示對應的 CSS 樣式。

![](using-page-inspector-in-aspnet-mvc/_static/image32.png)

現在將 `background-color` 的值變更為「紅色」。 變更會立即出現在 Page Inspector 瀏覽器中。

![](using-page-inspector-in-aspnet-mvc/_static/image34.png)

<a id="css_color_picker"></a>
## <a name="using-the-css-color-picker"></a>使用 CSS 色彩選擇器

Visual Studio 2012 中的 CSS 編輯器具有色彩選擇器，可讓您輕鬆地選擇和插入色彩。 色彩選擇器包含色彩的標準調色板、支援標準色彩名稱、雜湊碼、RGB、RGBA、HSL 和 HSLA 色彩，並維護您最近在檔中使用的色彩清單。

在上一節中，您已變更 `background-color` 屬性的值。 若要叫用色彩選擇器，請將插入點放在屬性名稱後面，然後輸入 **#** 或**rgb （** ）。

![CSS 色彩選擇器列](using-page-inspector-in-aspnet-mvc/_static/image36.png)

按一下色彩來選取它，或按向下鍵，然後使用向左鍵和向右鍵來流覽色彩。 當您造訪色彩時，會預覽對應的十六進位值：

![預覽的背景色彩屬性值](using-page-inspector-in-aspnet-mvc/_static/image38.png)

如果色軸沒有您想要的色彩，您可以使用色彩選擇器快顯視窗。 若要開啟它，請按一下色軸右端的雙燕號，或在鍵盤上按一次向下箭號或按兩次。

![CSS 色彩選擇器快顯視窗](using-page-inspector-in-aspnet-mvc/_static/image40.png)

按一下右側分隔號的色彩。 這會在主視窗中顯示該色彩的漸層。 按 Enter 鍵直接從分隔號中選擇色彩，或按一下主視窗中的任何點，選擇較高的精確度。

如果您的電腦畫面上有您想要使用的色彩（不一定要在 Visual Studio 使用者介面內），您可以使用右下方的 [滴管] 工具來捕捉其值。

您也可以移動色彩選擇器底部的滑杆來變更色彩的不透明度。 這麼做會將色彩值變更為 RGBA 值，因為 RGBA 格式可以代表不透明度。

選擇色彩之後，請按 Enter 鍵，然後輸入分號來完成*網站 .css*檔案中的背景色彩專案。

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a>Page Inspector 更新列

Page Inspector 會立即偵測到*網站 .css*檔案的變更，並在更新列中顯示警示。

![更新列](using-page-inspector-in-aspnet-mvc/_static/image42.png)

若要儲存所有檔案並重新整理 Page Inspector 的瀏覽器，請按 Ctrl + Alt + Enter，或按一下更新列。 醒目提示色彩中的變更會出現在瀏覽器中。

<a id="map_dynamic_elements"></a>
## <a name="mapping-dynamic-page-elements-to-javascript"></a>將動態頁面元素對應至 JavaScript

在新式 web 應用程式中，頁面中的元素通常是使用 JavaScript 動態產生的。 這表示沒有對應至這些頁面元素的靜態標記（HTML 或 Razor）。

使用1.3 版時，Page Inspector 現在可以將已動態新增至頁面的專案對應回相對應的 JavaScript 程式碼。 為了示範這項功能，我們將使用[單一頁面應用程式（SPA）範本](../../../single-page-application/overview/introduction/knockoutjs-template.md)。

> [!NOTE]
> SPA 範本需要[ASP.NET 和 Web 工具 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650)更新。

在 Visual Studio 中，**選擇 [** 檔案] &gt; [**新增專案**]。 在左側，展開 [**視覺C#效果**]，選取 [ **Web**]，然後選取 [ **ASP.NET MVC4 Web 應用程式**]。 按一下 [確定]。

在 [**新增 ASP.NET MVC 4 專案**] 對話方塊中，選取 [**單一頁面應用程式**]。

在方案總管中，依序展開 [ **Views** ] 資料夾和 [ **Home** ] 資料夾。 以滑鼠右鍵按一下索引. cshtml 檔案，然後選擇 [ **View in Page Inspector**]。

Page Inspector 瀏覽器中顯示的第一件事是登入頁面。 按一下 [註冊]，然後建立使用者名稱和密碼。 註冊之後，應用程式就會將您登入，並使用一些範例專案建立待辦事項清單。

按一下 [**檢查**]，將 Page Inspector 放在檢查模式中。 在 Page Inspector 瀏覽器中，按一下其中一個待辦事項專案。 請注意，不會以藍色反白顯示專案，而是以橙色反白顯示元素，並在專案名稱旁邊加上 "JS"。 這表示已透過腳本動態建立元素。

![](using-page-inspector-in-aspnet-mvc/_static/image44.png)

此外，[**呼叫堆疊**] 索引標籤上會顯示橙色底線。這表示 [**呼叫堆疊**] 窗格具有元素的詳細資訊。

按一下 [**呼叫堆疊**] 索引標籤。[**呼叫堆疊**] 窗格會顯示建立元素之 JavaScript 呼叫的呼叫堆疊。 對外部程式庫（例如 jQuery）的呼叫會折迭，讓您可以輕鬆地查看應用程式腳本的呼叫。

![](using-page-inspector-in-aspnet-mvc/_static/image46.png)

若要查看完整堆疊（包括對外部程式庫的呼叫），您可以展開標示為「外部程式庫」的節點：

![](using-page-inspector-in-aspnet-mvc/_static/image48.png)

如果您按一下呼叫堆疊中的專案，Visual Studio 會開啟程式碼檔案，並反白顯示對應的腳本。

![](using-page-inspector-in-aspnet-mvc/_static/image50.png)

## <a name="see-also"></a>另請參閱

[使用 Visual Studio ASP.NET MVC 4 的簡介](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)（ASP.net 網站）

[Page Inspector 簡介](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/)（Channel 9 影片）

[Page Inspector 錯誤訊息](https://go.microsoft.com/?linkid=9813062)（MSDN）
