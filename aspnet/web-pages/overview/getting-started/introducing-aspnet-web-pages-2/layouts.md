---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
title: ASP.NET Web Pages 簡介-建立一致的版面配置 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程示範如何使用版面配置，在使用 ASP.NET Web Pages 的網站上建立頁面的一致外觀。 它假設您已完成 。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: c85ec591-f8d7-4882-b763-de6ab9f3df7a
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
msc.type: authoredcontent
ms.openlocfilehash: 678eb7089e95e3d221d6b2d82034a62aefa75757
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78526688"
---
# <a name="introducing-aspnet-web-pages---creating-a-consistent-layout"></a>ASP.NET Web Pages 簡介-建立一致的版面配置

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本教學課程示範如何使用*版面*配置，在使用 ASP.NET Web Pages 的網站上建立頁面的一致外觀。 它假設您已透過[刪除 ASP.NET Web Pages 中的資料庫資料](https://go.microsoft.com/fwlink/?LinkId=251584)來完成數列。
> 
> 您將學到什麼：
> 
> - 什麼是版面配置頁。
> - 如何結合版面配置頁與動態內容。
> - 如何將值傳遞至版面配置頁。

## <a name="about-layouts"></a>關於版面配置

您目前所建立的頁面已全部完成，也就是獨立頁面。 它們全都屬於相同的網站，但沒有任何通用元素或標準外觀。

大部分的網站都具有一致的外觀和版面配置。 例如，如果您移至[Microsoft.com/web](https://www.microsoft.com/web/)網站並尋找，您會看到所有頁面都遵守整體版面配置和視覺主題：

![顯示標題、導覽區域、內容區域和頁尾版面配置的 Microsoft.com/web 網站頁面](layouts/_static/image1.png)

建立這種版面配置的*效率*不佳，就是在每個頁面上分別定義頁首、導覽列和頁尾。 您每次都會複製相同的標記。 如果您想要變更某個專案（例如，更新頁尾），您必須分別變更每個頁面。

這就是*版面配置頁面*的所在位置。 在 ASP.NET Web Pages 中，您可以定義在網站上提供頁面整體容器的版面配置頁。 例如，版面配置頁可以包含頁首、導覽區域和頁尾。 版面配置頁包含主要內容的預留位置。

接著，您可以定義個別的內容頁面，其中只包含該頁面的標記和程式碼。 內容頁不需要是完整的 HTML 網頁;他們甚至不需要有 `<body>` 元素。 它們也有一行程式碼，告訴 ASP.NET 您要顯示內容的版面配置頁。 以下是大致說明此關聯性運作方式的圖片：

![顯示兩個內容頁和版面配置頁的概念圖表](layouts/_static/image2.png)

當您看到此互動運作時，可以輕鬆地瞭解。 在本教學課程中，您會將電影頁面變更為使用版面配置。

## <a name="adding-a-layout-page"></a>新增版面配置頁

首先，您要建立一個版面配置頁面，其中定義了標題為頁尾的一般頁面配置，以及主要內容的區域。 在 WebPagesMovies 網站中，新增名為 *\_Layout*的 CSHTML 頁面。

前置底線（`_`）字元很重要。 如果頁面名稱的開頭是底線，ASP.NET 就不會直接將該頁面傳送至瀏覽器。 此慣例可讓您定義網站所需的頁面，但使用者應該不能直接要求。

將頁面中的內容取代為下列內容：

[!code-html[Main](layouts/samples/sample1.html)]

如您所見，此標記只是 HTML，它會使用 `<div>` 元素來定義頁面中的三個區段，再加上一個 `<div>` 元素來保存這三個區段。 頁尾包含一些 Razor 程式碼： `@DateTime.Now.Year`，這會在頁面中的該位置呈現目前的年份。

請注意，有一個名為 [*電影 .css*] 的樣式表單連結。 樣式表單是要定義元素實體配置詳細資料的位置。 您很快就會建立這項功能。

此 *\_Layout*  頁面中唯一不尋常的功能是 `@Render.Body()` 行。 這就是當此配置與另一個頁面合併時，內容將會前往的預留位置。

## <a name="adding-a-css-file"></a>新增 .css 檔案

若要定義頁面上元素的實際相片順序（也就是外觀），慣用的方法是使用級聯樣式表（CSS）規則。 因此，您將建立一個 *.css*檔案，其中包含您新版面配置的規則。

在 WebMatrix 中，選取您網站的根目錄。 然後在功能區的 [檔案] 索引標籤中，按一下 [**新增**] 按鈕**底下的箭**號，然後按一下 [**新增資料夾**]。

![功能區中 [新增] 底下的 [新增資料夾] 選項。](layouts/_static/image3.png)

將新的資料夾命名為*樣式*。

![將新資料夾命名為「樣式」](layouts/_static/image4.png)

在 [新*樣式*] 資料夾內，建立名為 [*電影 .css*] 的檔案。

![建立新的電影 .css 檔案](layouts/_static/image5.png)

將新 *.css*檔案的內容取代為下列內容：

[!code-css[Main](layouts/samples/sample2.css)]

除了注意兩件事以外，我們不會對這些 CSS 規則有太大的看法。 其中一種是除了設定字型和大小之外，規則也會使用絕對位置來建立頁首、頁尾和主要內容區域的位置。 如果您不熟悉 CSS 中的定位，可以閱讀 W3Schools 網站上的[Css 定位](http://www.w3schools.com/css/css_positioning.asp)教學課程。

另一個要注意的是，我們在底部複製了原本在*電影. cshtml*檔案中個別定義的樣式規則。 這些規則是在使用 ASP.NET Web Pages 教學課程來[顯示資料的簡介](https://go.microsoft.com/fwlink/?LinkId=251580)中使用，以便讓 `WebGrid` 協助程式轉譯標記將條紋新增至資料表。 （如果您要使用樣式定義的 *.css*檔案，可能也會將整個網站的樣式規則放在其中）。

## <a name="updating-the-movies-file-to-use-the-layout"></a>更新電影檔案以使用版面配置

現在您可以更新網站中的現有檔案，以使用新的版面配置。 開啟 [*電影*] 檔案。 在頂端，作為第一行程式碼，新增下列內容：

[!code-csharp[Main](layouts/samples/sample3.cs)]

網頁現在以這種方式啟動：

[!code-cshtml[Main](layouts/samples/sample4.cshtml?highlight=2)]

這一行程式碼會告訴 ASP.NET，當 [*電影*] 頁面執行時，應該與\_的配置*cshtml*檔案合併。

由於*電影的 cshtml*檔案現在使用版面配置頁面，因此您可以從 *\_配置 cshtml*檔案所處理的 [ *cshtml* ] 頁面中移除標記。 取出 `<!DOCTYPE>`、`<html>`，並 `<body>` 開頭和結束記號。 取出整個 `<head>` 專案及其內容，其中包括方格的樣式規則，因為您現在已經在 *.css*檔案中取得這些規則。 當您在此時，請將現有的 `<h1>` 專案變更為 `<h2>` 元素;您在版面配置頁中已經有 `<h1>` 元素。 將 `<h2>` 文字變更為「列出電影」。

通常您不需要在 [內容] 頁面中進行這類變更。 當您使用版面配置頁面來啟動網站時，您會建立內容頁面，而不需要所有這些元素。 不過，在此情況下，您要將獨立頁面轉換成使用版面配置的網頁，所以有一些清除。

當您完成時，[*影片*] 的 [cshtml] 頁面看起來會像下面這樣：

[!code-cshtml[Main](layouts/samples/sample5.cshtml)]

### <a name="testing-the-layout"></a>測試版面配置

現在您可以看到版面配置的外觀。 在 WebMatrix 中，以滑鼠右鍵按一下 [*影片. cshtml* ] 頁面，然後選取 [**在瀏覽器中啟動**]。 當瀏覽器顯示頁面時，它看起來會像這個頁面：

![使用版面配置呈現的電影頁面](layouts/_static/image6.png)

ASP.NET 已將 電影 頁面的內容合併到 `RenderBody` 方法所在的 *\_Layout*  頁面中。 當然， *\_Layout*  頁面會參考定義頁面外觀的 *.css*檔案。

## <a name="updating-the-addmovie-page-to-use-the-layout"></a>更新 AddMovie 頁面以使用版面配置

版面配置的實際優點是您可以將其用於網站中的所有頁面。 開啟 [ *AddMovie* ] 頁面。

您可能會忘了， *AddMovie*一頁原本有一些 CSS 規則，可以定義驗證錯誤訊息的外觀。 因為您現在有網站的 *.css*檔案，所以您可以將這些規則移到 *.css*檔案。 將它們從*AddMovie*檔案中移除，並將它們新增至*電影 .css*檔案的底部。 您要移動下列規則：

[!code-css[Main](layouts/samples/sample6.css)]

現在在*AddMovie*中，對您的電影進行相同的變更。 *cshtml* —新增 `Layout="~/_Layout.cshtml;`，並移除現在無關的 HTML 標籤。 將 `<h1>` 元素變更為 `<h2>`。 當您完成時，頁面看起來會像下列範例：

[!code-cshtml[Main](layouts/samples/sample7.cshtml)]

執行頁面。 現在看起來如下圖所示：

![使用版面配置呈現的 [新增電影] 頁面](layouts/_static/image7.png)

您想要對網站中的頁面進行類似的變更，也就是*EditMovie*和*DeleteMovie*。 不過，在這麼做之前，您可以對配置進行另一個變更，讓它更具彈性。

## <a name="passing-title-information-to-the-layout-page"></a>將標題資訊傳遞至版面配置頁

您所建立的 *\_配置. cshtml*  頁面具有設定為「我的電影網站」的 `<title>` 元素。 大部分的瀏覽器都會將此元素的內容顯示為索引標籤上的文字：

![在瀏覽器索引標籤中顯示的頁面 &lt;標題&gt; 元素](layouts/_static/image8.png)

此標題資訊是泛型的。 假設您希望標題文字更特定于目前頁面。 （搜尋引擎也會使用標題文字來判斷您的頁面為何）。您可以將內容頁面中的資訊（例如，像是*電影*或*AddMovie* ）傳遞至版面配置頁，然後使用該資訊來自訂版面配置頁的呈現方式。

再次開啟 [*電影. cshtml* ] 頁面。 在頂端的程式碼中，新增下面這一行：

[!code-csharp[Main](layouts/samples/sample8.cs)]

`Page` 物件可在所有的*cshtml*頁面上使用，基於此目的，也就是在頁面與其配置之間共用資訊。

開啟 *\_Layout*  頁面。 變更 `<title>` 元素，使其看起來像此標記：

[!code-html[Main](layouts/samples/sample9.html)]

此程式碼會在頁面中的該位置直接呈現在 [`Page.Title`] 屬性中的任何內容。

執行 [*電影. cshtml* ] 頁面。 此時，[瀏覽器] 索引標籤會顯示您傳遞做為 `Page.Title`值的內容：

![顯示動態建立之標題的瀏覽器索引標籤](layouts/_static/image9.png)

如果您想要的話，請在瀏覽器中查看頁面來源。 您可以看到 `<title>` 元素會轉譯為 `<title>List Movies</title>`。

> [!TIP] 
> 
> **Page 物件**
> 
> `Page` 的一個有用功能是動態物件，`Title` 屬性不是固定或保留名稱。 您可以使用*任何*名稱作為 `Page` 物件的值。 例如，您可以使用名為 `Page.CurrentName` 或 `Page.MyPage`的屬性，輕鬆地傳遞標題。 唯一的限制是名稱必須遵循一般規則，才能命名哪些屬性。 （例如，名稱不能包含空格）。
> 
> 您可以使用 `Page` 物件來傳遞任意數目的值。 如果您想要將電影資訊傳遞至版面配置頁面，您可以使用類似 `Page.MovieTitle` 和 `Page.Genre` 和 `Page.MovieYear`來傳遞值。 （或您為了儲存資訊所需的任何其他名稱）。唯一的要求（可能是顯而易見的）是您必須在 [內容] 頁面和 [版面配置] 頁面中使用相同的名稱。
> 
> 您使用 `Page` 物件傳遞的資訊，並不限於只在版面配置頁上顯示的文字。 您可以將值傳遞至版面配置頁，然後在版面配置頁中的程式碼可以使用值來決定要顯示頁面的區段、要使用的 *.css*檔案等等。 您在 `Page` 物件中傳遞的值，就像您在程式碼中使用的任何其他值。 這只是值源自于 [內容] 頁面，而且會傳遞至版面配置頁。

開啟 [ *AddMovie* ] 頁面，並在程式碼頂端新增一行，以提供 [ *AddMovie* ] 頁面的標題：

[!code-csharp[Main](layouts/samples/sample10.cs)]

執行 [ *AddMovie* ] 頁面。 您會在該處看到新的標題：

![顯示動態建立的 [新增電影] 標題的瀏覽器索引標籤](layouts/_static/image10.png)

## <a name="updating-the-remaining-pages-to-use-the-layout"></a>更新其餘頁面以使用版面配置

現在您可以完成網站中的其餘頁面，使其使用新的版面配置。 依次開啟*EditMovie*和*DeleteMovie* ，並在每個中進行相同的變更。

加入連結至版面配置頁的程式程式碼：

[!code-csharp[Main](layouts/samples/sample11.cs)]

新增行以設定頁面的標題：

[!code-csharp[Main](layouts/samples/sample12.cs)]

或：

[!code-csharp[Main](layouts/samples/sample13.cs)]

移除所有無關的 HTML 標籤-基本上，只保留 `<body>` 專案內的位（再加上頂端的程式碼區塊）。

將 `<h1>` 元素變更為 `<h2>` 元素。

當您進行這些變更時，請進行測試，並確定其顯示正確且標題正確。

## <a name="parting-thoughts-about-layout-pages"></a>關於版面配置頁的資訊

在本教學課程中，您建立了 *\_Layout*  頁面，並使用 `RenderBody` 方法來合併另一頁的內容。 這是在網頁中使用版面配置的基本模式。

版面配置頁有其他不在此討論的功能。 例如，您可以嵌套版面配置頁，一個版面配置頁可以輪流參考另一個。 如果您要使用需要不同版面配置的網站子區段，則可以使用嵌套的版面配置。 您也可以使用其他方法（例如 `RenderSection`），在版面配置頁面中設定已命名的區段。

版面配置頁和 *.css*檔案的組合功能強大。 如您在下一個教學課程系列中所見，您可以在 WebMatrix 中建立以*範本*為基礎的網站，這會提供您在其中預先建立功能的網站。 這些範本可充分利用版面配置頁和 CSS，建立外觀良好且具有功能表等功能的網站。 以下是以範本為基礎之網站首頁的螢幕擷取畫面，其中顯示使用版面配置頁和 CSS 的功能：

![由 WebMatrix 網站範本所建立的版面配置，顯示標頭、流覽區域、內容區域、選擇性區段和登入連結](layouts/_static/image11.png)

## <a name="complete-listing-for-movie-page-updated-to-use-a-layout-page"></a>電影頁面的完整清單（更新為使用版面配置頁面）

[!code-cshtml[Main](layouts/samples/sample14.cshtml)]

## <a name="complete-page-listing-for-add-movie-page-updated-for-layout"></a>[新增電影] 頁面的完成頁面清單（針對版面配置更新）

[!code-cshtml[Main](layouts/samples/sample15.cshtml)]

## <a name="complete-page-listing-for-delete-movie-page-updated-for-layout"></a>[刪除電影] 頁面的完成頁面清單（已針對版面配置更新）

[!code-cshtml[Main](layouts/samples/sample16.cshtml)]

## <a name="complete-page-listing-for-edit-movie-page-updated-for-layout"></a>編輯電影頁面的完成頁面清單（已針對版面配置更新）

[!code-cshtml[Main](layouts/samples/sample17.cshtml)]

## <a name="coming-up-next"></a>下一步

在下一個教學課程中，您將瞭解如何將您的網站發佈至網際網路，讓每個人都能看到它。

## <a name="additional-resources"></a>其他資源

- [建立一致的外觀](https://go.microsoft.com/fwlink/?LinkID=202891)：一篇文章，提供更多有關使用版面配置的詳細資料。 它也會說明如何將值傳遞至版面配置頁，以顯示或隱藏部分內容。
- [含有 Razor 的嵌套版面配置頁](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor)— Mike Brind 的 blog，是如何將版面配置頁的範例。 （包含頁面的下載）。

> [!div class="step-by-step"]
> [上一頁](deleting-data.md)
> [下一頁](publishing.md)
