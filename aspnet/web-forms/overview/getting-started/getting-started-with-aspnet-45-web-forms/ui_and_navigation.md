---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/ui_and_navigation
title: UI 和流覽 |Microsoft Docs
author: Erikre
description: 本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 為我們建立 ASP.NET Web Forms 應用程式的基本概念 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 5c76891d-e515-4885-b576-76bd2c494efe
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/ui_and_navigation
msc.type: authoredcontent
ms.openlocfilehash: ac1dcaf1ba911fdcaeb3845c6836ec771733d93e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78643553"
---
# <a name="ui-and-navigation"></a>UI 和瀏覽

依[Erik Reitan](https://github.com/Erikre)

[下載 Wingtip 玩具範例專案（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下載電子書（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 建立 ASP.NET Web Forms 應用程式的基本概念。 本教學課程系列隨附有[ C#原始程式碼](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 專案。

在本教學課程中，您將修改預設 Web 應用程式的 UI，以支援 Wingtip 玩具存放區 front 應用程式的功能。 此外，您還會加入簡單和資料系結的導覽。 本教學課程是以先前的教學課程「建立資料存取層」為基礎，而且是 Wingtip 玩具教學課程系列的一部分。

## <a name="what-youll-learn"></a>您將學到什麼：

- 如何變更 UI 以支援 Wingtip 玩具 store front 應用程式的功能。
- 如何設定 HTML5 元素以包含頁面導覽。
- 如何建立資料驅動控制項，以流覽至特定產品資料。
- 如何顯示使用 Entity Framework Code First 建立之資料庫中的資料。

ASP.NET Web Forms 可讓您建立 Web 應用程式的動態內容。 每個 ASP.NET 網頁的建立方式類似于靜態 HTML 網頁（不包括以伺服器為基礎的處理），但是 ASP.NET 網頁包含額外的元素，ASP.NET 會在頁面執行時辨識和處理以產生 HTML。

使用靜態 HTML 網頁（ *.htm*或 *.html*檔案）時，伺服器會藉由讀取檔案並依預設將它傳送至瀏覽器，來滿足 `Web` 的要求。 相反地，當有人要求 ASP.NET 網頁（ *.aspx*檔案）時，網頁會以程式的形式在 web 伺服器上執行。 當網頁正在執行時，它可以執行您的網站所需的任何工作，包括計算值、讀取或寫入資料庫資訊，或呼叫其他程式。 作為輸出，頁面會以動態方式產生標記（例如 HTML 中的專案），並將這個動態輸出傳送至瀏覽器。

## <a name="modifying-the-ui"></a>修改 UI

您將會藉由修改*default.aspx*頁面來繼續本教學課程系列。 您將修改已由用來建立應用程式的預設範本所建立的 UI。 您在建立任何 Web Forms 應用程式時，通常會執行的修改類型。 您會藉由變更標題、取代某些內容，以及移除不必要的預設內容來執行此動作。

1. 開啟或切換至*default.aspx*頁面。
2. 如果頁面出現在**設計**視圖中，請切換至 [**來源**視圖]。
3. 在 [`@Page`] 指示詞的頁面頂端，將 [`Title`] 屬性變更為 [歡迎]，如下所示黃色反白顯示。 

    [!code-aspx[Main](ui_and_navigation/samples/sample1.aspx?highlight=1)]
4. 此外，在*default.aspx*頁面上，取代 [`<asp:Content>`] 標籤中包含的所有預設內容，讓標記看起來如下所示。 

    [!code-aspx[Main](ui_and_navigation/samples/sample2.aspx)]
5. 從 [檔案] 功能表中選取 [**儲存 default.aspx** **]，以**儲存*default.aspx*頁面。

   產生的*default.aspx*頁面會如下所示： 

[!code-aspx[Main](ui_and_navigation/samples/sample3.aspx)]

在此範例中，您已設定 `@Page` 指示詞的 `Title` 屬性。 當 HTML 顯示在瀏覽器中時，伺服器程式碼 `<%: Page.Title %>` 會解析為 `Title` 屬性中包含的內容。

範例頁面包含構成 ASP.NET 網頁的基本元素。 此頁面包含靜態文字，如同您在 HTML 網頁中可能擁有的內容，以及 ASP.NET 特定的專案。 *Default.aspx*頁面中包含的內容將會與主版頁面內容整合，稍後將在本教學課程中說明。

### <a name="page-directive"></a>@Page 指示詞

ASP.NET Web form 通常包含的指示詞可讓您指定頁面的屬性和設定資訊。 ASP.NET 會使用指示詞作為如何處理頁面的指示，但不會轉譯為傳送至瀏覽器之標記的一部分。

最常使用的指示詞是 `@Page` 指示詞，可讓您指定頁面的許多設定選項，包括下列各項：

1. 網頁中程式碼的伺服器程式設計語言，例如C#。
2. 頁面是否是直接在頁面中使用伺服器程式碼的頁面（稱為單一檔案頁面），或其是否為具有程式碼的頁面（稱為程式碼後置頁面）。
3. 頁面是否有相關聯的主版頁面，因此應視為內容頁。
4. 調試和追蹤選項。

如果您未在頁面中包含 `@Page` 指示詞，或指示詞不包含特定的設定，則會從*web.config 設定檔*或*machine.config*設定檔繼承設定。 Machine.config*檔案*會針對在電腦上執行的所有應用程式提供額外的設定。

> [!NOTE] 
> 
> Machine.config*也會*提供所有可能設定的詳細資料。

### <a name="web-server-controls"></a>Web 服務器控制項

在大部分的 ASP.NET Web form 應用程式中，您會加入控制項，讓使用者與頁面互動，例如按鈕、文字方塊、清單等。 這些 Web 服務器控制項類似于 HTML 按鈕和輸入元素。 不過，它們會在伺服器上進行處理，讓您可以使用伺服器程式碼來設定其屬性。 這些控制項也會引發事件，讓您可以在伺服器程式碼中處理。

伺服器控制項使用特殊語法，ASP.NET 會在頁面執行時辨識。 ASP.NET 伺服器控制項的標記名稱是以 `asp:` 前置詞開頭。 這可讓 ASP.NET 辨識及處理這些伺服器控制項。 如果控制項不是 .NET Framework 的一部分，前置詞可能會不同。 除了 `asp:` 前置詞之外，ASP.NET 伺服器控制項還包含 `runat="server"` 屬性，以及您可以用來在伺服器程式碼中參考控制項的 `ID`。

當頁面執行時，ASP.NET 會識別伺服器控制項，並執行與這些控制項相關聯的程式碼。 許多控制項在瀏覽器中顯示時，會將一些 HTML 或其他標記轉譯成頁面。

### <a name="server-code"></a>伺服器程式碼

大部分的 ASP.NET Web Forms 應用程式都包含在處理頁面時，在伺服器上執行的程式碼。 如先前所述，伺服器程式碼可用來執行各種動作，例如將資料新增至 ListView 控制項。 ASP.NET 支援在伺服器上執行的許多語言，包括C#、Visual Basic、j # 和其他語言。

ASP.NET 支援兩種模型來撰寫網頁的伺服器程式碼。 在單一檔案模型中，頁面的程式碼位於腳本元素中，其中開頭標記包含 `runat="server"` 屬性。 或者，您也可以在個別的類別檔案（稱為「程式碼後置模型」）中建立頁面的程式碼。 在此情況下，ASP.NET Web Forms 頁面通常不會包含任何伺服器程式碼。 相反地，`@Page` 指示詞所包含的資訊會連結 *.aspx*頁面及其相關聯的程式碼後置檔案。

`@Page` 指示詞中包含的 `CodeBehind` 屬性會指定個別類別檔案的名稱，而 `Inherits` 屬性會指定程式碼後置檔案中對應至該頁面的類別名稱。

### <a name="updating-the-master-page"></a>更新主版頁面

在 ASP.NET Web Forms 中，主要頁面可用來建立應用程式中頁面的一致性版面配置。 單一主要頁面可為應用程式中的所有頁面 (或頁面群組) 定義您想要的外觀與風格及標準行為。 接著，您可以建立包含您想要顯示之內容的個別內容頁面，如上面所述。 當使用者要求內容頁面時，ASP.NET 會將這些頁面與主要頁面合併，以產生結合主要頁面之配置與內容頁面之內容的輸出。

新網站需要在每個頁面上顯示單一標誌。 若要新增此標誌，您可以在主版頁面上修改 HTML。

1. 在 [方案總管]中，尋找並開啟 **Site.Master** 頁面。
2. 如果頁面在**設計**視圖中，請切換至 [**原始**檔視圖]。
3. **修改或新增**以黃色反白顯示的標記，以更新主版頁面： 

    [!code-aspx[Main](ui_and_navigation/samples/sample4.aspx?highlight=9,49,76-81,87)]

此 HTML 會從 Web 應用程式的 [ *Images* ] 資料夾中顯示名為 [ *.jpg* ] 的影像，您將在稍後新增。 當瀏覽器中顯示使用主版頁面的頁面時，將會顯示標誌。 如果使用者按一下標誌，使用者會流覽回*default.aspx*頁面。 HTML 錨點標記 `<a>` 包裝影像伺服器控制項，並允許在連結中包含影像。 錨點標記的 `href` 屬性會指定網站的根 "`~/`" 做為連結位置。 根據預設，當使用者流覽至網站的根目錄時，會顯示*default.aspx*頁面。 **影像**`<asp:Image>` 伺服器控制項包含在瀏覽器中顯示時，會轉譯為 HTML 的加法屬性（例如 `BorderStyle`）。

### <a name="master-pages"></a>主版頁面

主版頁面是副檔名為 master （例如，*網站*）的 ASP.NET 檔案，其中包含預先定義的版面配置，可包含靜態文字、HTML 專案和伺服器控制項。 主版頁面是由特殊的 `@Master` 指示詞所識別，取代一般 *.aspx*頁面所使用的 `@Page` 指示詞。

除了 `@Master` 指示詞之外，主版頁面也包含頁面的所有最上層 HTML 元素，例如 `html`、`head`和 `form`。 例如，在您先前新增的主版頁面上，您可以使用 HTML `table` 進行版面配置，`img` 元素用於公司標誌、靜態文字和伺服器控制項，以處理網站的一般成員資格。 您可以使用任何 HTML 和任何 ASP.NET 元素做為主版頁面的一部分。

除了會出現在所有頁面上的靜態文字和控制項，主版頁面也包含一個或多個**ContentPlaceHolder**控制項。 這些預留位置控制項會定義可取代內容出現的區域。 接著，使用**內容**伺服器控制項，即可在內容頁面（例如*default.aspx*）中定義可取代的內容。

#### <a name="adding-image-files"></a>新增影像檔案

上述所參考的標誌影像連同所有產品影像，都必須加入至 Web 應用程式，以便在專案顯示在瀏覽器中時看到。

#### <a name="download-from-msdn-samples-site"></a>從 MSDN 範例網站下載：

[使用 ASP.NET 4.5 Web Forms 和 Visual Studio 2013 Wingtip 玩具](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)（C#）的消費者入門

此下載包含 [ *WingtipToys-資產*] 資料夾中用來建立範例應用程式的資源。

1. 如果您尚未這麼做，請從 MSDN 範例網站使用上述連結下載壓縮的範例檔案。
2. 下載之後，請開啟 .zip 檔案，並將內容複寫到您電腦上的本機資料夾。
3. 尋找並開啟 [ *WingtipToys-資產*] 資料夾。
4. 藉由拖放，將*目錄*資料夾從本機資料夾複製到 Web 應用程式專案的根目錄（在 Visual Studio 的**方案總管**中）。 

    ![UI 和流覽-複製檔案](ui_and_navigation/_static/image1.png)
5. 接下來，建立名為*Images*的新資料夾，方法是以滑鼠右鍵**按一下方案總管**中的**WingtipToys**專案，**然後選取 [** 新增 -&gt;**新資料夾**]。
6. 將 [ *WingtipToys-資產*] 資料夾中的 [*標誌 .jpg*檔案 **] 複製到 Web**應用程式專案的 [ *Images* ] 資料夾中 Visual Studio 的**方案總管**。
7. 如果您沒有看到新檔案，請按一下**方案總管**頂端的 [**顯示所有**檔案] 選項來更新檔案清單。  
  
    **方案總管**現在會顯示已更新的專案檔案。 

    ![UI 和導覽-方案總管](ui_and_navigation/_static/image2.png)

### <a name="adding-pages"></a>加入頁面

在將導覽新增至 Web 應用程式之前，您會先加入兩個要流覽的新頁面。 稍後在本教學課程系列中，您將會在這些新的頁面上顯示產品和產品詳細資料。

1. 在**方案總管**中，以滑鼠右鍵按一下 [ **WingtipToys**]，按一下 [**加入**]，然後按一下 [**新增專案**]。   
 隨即顯示 [ 新增項目] 對話方塊。
2. 選取左側的 [ **Visual C#**  -&gt; **Web**範本] 群組。 然後，從中間清單中選取 [**具有主版頁面的 Web Form** ]，並將它命名為*ProductList .aspx*。 

    ![UI 和導覽-加入新專案對話方塊](ui_and_navigation/_static/image3.png)
3. 選取 [**網站**]，將主版頁面附加至新建立的 *.aspx*頁面。 

    ![UI 和流覽-選取主版頁面](ui_and_navigation/_static/image4.png)
4. 遵循這些相同的步驟，新增名為*ProductDetails*的其他頁面。

### <a name="updating-bootstrap"></a>更新啟動程式

Visual Studio 2013 專案範本會使用[啟動](http://getbootstrap.com/)程式，這是 Twitter 所建立的版面配置和主題架構。 啟動程式會使用 CSS3 來提供回應式設計，這表示版面配置可以動態調整成不同的瀏覽器視窗大小。 您也可以使用啟動程式的主題功能，輕鬆地影響應用程式外觀和風格的變更。 根據預設，Visual Studio 2013 中的 ASP.NET Web 應用程式範本包含以 NuGet 封裝的啟動載入器。

在本教學課程中，您將藉由取代啟動載入 CSS 檔案來變更 Wingtip 玩具應用程式的外觀與風格。

1. 在**方案總管**中，開啟 [*內容*] 資料夾。
2. 以滑鼠右鍵按一下*啟動程式 .css*檔案，然後將它重新命名為*bootstrap-original。*
3. 將*bootstrap-original*重新*命名為最小的 .css。*
4. 在**方案總管**中，以滑鼠右鍵按一下 [*內容*] 資料夾，然後選取 [**在檔案瀏覽器中開啟資料夾**]。  
   [檔案瀏覽器] 將會顯示。 您會將已下載的啟動載入 CSS 檔案儲存到這個位置。
5. 在您的瀏覽器中，移至 [ [https://bootswatch.com/3/](https://bootswatch.com/3/)]。
6. 請滾動瀏覽器視窗，直到您看到 Cerulean 主題。 

    ![UI 和流覽 Cerulean 主題](ui_and_navigation/_static/image5.png)
7. 將啟動程式 *.css*檔案和啟動程式.*小 .css*檔案下載至*Content*資料夾。 使用您先前開啟的 [檔案**瀏覽器**] 視窗中所顯示之 [內容] 資料夾的路徑。
8. 在**方案總管**頂端的**Visual Studio**中，選取 [**顯示所有**檔案] 選項，以顯示 [內容] 資料夾中的新檔案。 

    ![UI 和導覽-方案總管](ui_and_navigation/_static/image6.png)

   您會在 [**內容**] 資料夾中看到兩個新的 CSS 檔案，但請注意，每個檔案名旁的圖示都會呈現灰色。這表示檔案尚未新增至專案。
9. 以滑鼠右鍵按一下*啟動程式 .css*檔案，然後*選取 [* **包含在專案中**]。   
   當您稍後在本教學課程中執行 Wingtip 玩具應用程式時，將會顯示新的 UI。

> [!NOTE] 
> 
> ASP.NET Web 應用程式範本會使用專案根目錄的配套 *.config*檔案來儲存啟動程式 CSS 檔案的路徑。

### <a name="modifying-the-default-navigation"></a>修改預設導覽

您可以變更 [*網站*] 頁面中的未排序導覽清單元素，以修改應用程式中每個頁面的預設導覽。

1. 在**方案總管**中，找出並開啟 [*網站*] 頁面。
2. 將以黃色反白顯示的其他導覽連結新增至未排序清單，如下所示：   

    [!code-html[Main](ui_and_navigation/samples/sample5.html?highlight=5)]

如您在上述 HTML 中所見，您已修改每個包含錨點標記的明細專案 `<li>`，`<a>` `href` 屬性的連結。 每個 `href` 都會指向 Web 應用程式中的頁面。 在瀏覽器中，當使用者按一下其中一個連結（例如 [**產品**]）時，他們會流覽至包含在 `href` 中的頁面（例如**ProductList .aspx**）。 您將會在本教學課程結尾處執行應用程式。

> [!NOTE] 
> 
> 波狀符號（`~`）字元是用來指定 `href` 路徑從專案的根目錄開始。

### <a name="adding-a-data-control-to-display-navigation-data"></a>加入資料控制項以顯示導覽資料

接下來，您將加入控制項，以顯示資料庫中的所有類別。 每個類別目錄都會作為*ProductList*的連結。 當使用者在瀏覽器中按一下類別連結時，他們會流覽至 [產品] 頁面，並且只會查看與所選類別相關聯的產品。

您將使用**ListView**控制項來顯示包含在資料庫中的所有類別。 若要將**ListView**控制項加入至主版頁面：

1. 在 [*網站*] 頁面中，將下列反白顯示的 `<div>` 專案新增至包含您稍早新增之 `id="TitleContent"` 的 `<div>` 元素**後面**：  

    [!code-aspx[Main](ui_and_navigation/samples/sample6.aspx?highlight=7-21)]

此程式碼會顯示資料庫中的所有類別。 **ListView**控制項會將每個類別目錄名稱顯示為連結文字，並包含包含該分類之 `ID` 的查詢字串值之*ProductList*的連結。 藉由設定**ListView**控制項中的 [`ItemType`] 屬性，就可以在 [`ItemTemplate`] 節點中使用資料系結運算式 `Item`，而控制項就會成為強型別。 您可以使用 IntelliSense 來選取 `Item` 物件的詳細資料，例如指定 `CategoryName`。 此程式碼包含在標記資料系結運算式的容器 `<%#: %>` 內。 藉由新增（:)在 `<%#` 前置詞的結尾，資料系結運算式的結果會以 HTML 編碼。 當結果是以 HTML 編碼時，您的應用程式會受到較佳的保護，以防止跨網站腳本插入（XSS）和 HTML 插入式攻擊。

> [!NOTE] 
> 
> **秘訣**
> 
> 當您在開發期間輸入來加入程式碼時，您可以確定已找到物件的有效成員，因為強型別資料控制項會根據 IntelliSense 顯示可用的成員。 當您輸入程式碼時，IntelliSense 會提供內容適當的程式碼選擇，例如屬性、方法和物件。

在下一個步驟中，您將會執行 `GetCategories` 方法來取出資料。

### <a name="linking-the-data-control-to-the-database"></a>將資料控制項連結至資料庫

您必須先將資料控制項連結到資料庫，才可以在資料控制中顯示資料。 若要建立連結，您可以修改*Site.Master.cs*檔案的程式碼後置。

1. 在**方案總管**中，以滑鼠右鍵按一下 [*網站*] 頁面，然後按一下 [**查看程式碼**]。 *Site.Master.cs*檔案會在編輯器中開啟。
2. 在*Site.Master.cs*檔案的開頭附近，加入兩個額外的命名空間，讓所有包含的命名空間顯示如下：  

    [!code-csharp[Main](ui_and_navigation/samples/sample7.cs?highlight=8-9)]
3. 將反白顯示的 `GetCategories` 方法加入 `Page_Load` 事件處理常式之後，如下所示：  

    [!code-csharp[Main](ui_and_navigation/samples/sample8.cs?highlight=6-11)]

在瀏覽器中載入使用主版頁面的任何頁面時，會執行上述程式碼。 您稍早在本教學課程中新增的 `ListView` 控制項（名為 "categoryList"）會使用模型系結來選取資料。 在 `ListView` 控制項的標記中，您可以將控制項的 `SelectMethod` 屬性設定為 `GetCategories` 方法，如上所示。 `ListView` 控制項會在頁面生命週期的適當時間呼叫 `GetCategories` 方法，並自動系結傳回的資料。 在下一個教學課程中，您將深入瞭解如何系結資料。

### <a name="running-the-application-and-creating-the-database"></a>執行應用程式並建立資料庫

稍早在本教學課程系列中，您已建立初始化運算式類別（名為 "ProductDatabaseInitializer"），並在*global.asax.cs*檔案中指定此類別。 當第一次執行應用程式時，Entity Framework 將會產生資料庫，因為*global.asax.cs*檔案中包含的 `Application_Start` 方法將會呼叫初始化運算式類別。 初始化運算式類別會使用您稍早在本教學課程系列中新增的模型類別（`Category` 和 `Product`）來建立資料庫。

1. 在**方案總管**中，以滑鼠右鍵按一下*default.aspx*頁面，然後選取 [**設定為起始頁**]。
2. 在 Visual Studio 按**F5**。   
 在第一次執行期間設定所有專案需要一些時間。   
    ![UI 和導覽瀏覽器視窗](ui_and_navigation/_static/image7.png)  
 當您執行應用程式時，將會編譯應用程式，而且會在*應用程式\_Data*資料夾中建立名為*wingtiptoys*的資料庫。 在瀏覽器中，您會看到 [類別] 導覽功能表。 此功能表是藉由從資料庫中抓取類別來產生。 在下一個教學課程中，您將會執行導覽。
3. 關閉瀏覽器以停止執行中的應用程式。

### <a name="reviewing-the-database"></a>檢查資料庫

開啟 web.config*檔案*，並查看 [連接字串] 區段。 您可以看到，連接字串中的 `AttachDbFilename` 值指向 Web 應用程式專案的 `DataDirectory`。 `|DataDirectory|` 的值是保留的值，表示專案中的*應用程式\_的 Data*資料夾。 此資料夾是從您的實體類別建立的資料庫所在位置。

[!code-xml[Main](ui_and_navigation/samples/sample9.xml)]

> [!NOTE] 
> 
> 如果看不到 [*應用程式\_* ] 資料夾，或資料夾是空的，請**選取 [重新整理] 圖示，** 然後在 [**方案總管**] 視窗頂端的 [**顯示所有**檔案] 圖示。 可能需要擴充**方案總管**視窗的寬度，才能顯示所有可用的圖示。

現在您可以使用 [**伺服器總管**] 視窗，檢查*wingtiptoys*所包含的資料。

1. 展開*應用程式\_[Data* ] 資料夾。 如果看不到*應用程式\_的資料*資料夾，請參閱上面的注意事項。
2. 如果看不到*wingtiptoys .mdf*資料庫檔案，請**選取 [重新整理] 圖示，** 然後選取 [**方案總管**] 視窗頂端的 [**顯示所有**檔案] 圖示。
3. 以滑鼠右鍵按一下*wingtiptoys .mdf*資料庫檔案，然後選取 [**開啟**]。  
    隨即顯示 [**伺服器總管**]。 

    ![UI 和導覽-伺服器總管](ui_and_navigation/_static/image8.png)
4. 展開 *[資料表]* 資料夾。
5. 以滑鼠右鍵按一下 [ **Products**] 資料表，然後選取 [**顯示資料表資料**]。  
 [ **Products** ] 資料表隨即顯示。 

    ![UI 和流覽產品資料表](ui_and_navigation/_static/image9.png)
6. 此視圖可讓您以手動方式查看及修改**Products**資料表中的資料。
7. 關閉 [**產品**] 資料表視窗。
8. 在 **伺服器總管**中，再次以滑鼠右鍵按一下**Products**資料表，然後選取 **開啟資料表定義**。  
 [ **Products** ] 資料表的資料設計隨即顯示。 

    ![UI 和流覽-產品設計](ui_and_navigation/_static/image10.png)
9. 在 [ **t-sql** ] 索引標籤中，您會看到用來建立資料表的 SQL DDL 語句。 您也可以使用 [**設計**] 索引標籤中的 UI 來修改架構。
10. 在**伺服器總管**中，以滑鼠右鍵按一下 [ **WingtipToys**資料庫]，然後選取 [**關閉連接**]。   
 藉由卸離資料庫與 Visual Studio，稍後在本教學課程系列中將能夠修改資料庫架構。
11. 選取 [**伺服器總管**] 視窗底部的 [**方案總管**] 索引標籤，以返回**方案總管**。

## <a name="summary"></a>總結

在此系列的本教學課程中，您已新增一些基本 UI、圖形、頁面和導覽。 此外，您已執行 Web 應用程式，這會從您在上一個教學課程中新增的資料類別建立資料庫。 您也可以直接流覽資料庫，以查看資料庫的*Products*資料表內容。 在下一個教學課程中，您將會顯示資料庫中的資料項目和詳細資料。

## <a name="additional-resources"></a>其他資源

程式[設計 ASP.NET Web Pages  簡介](https://msdn.microsoft.com/library/ms178125.aspx)  
[ASP.NET Web 服務器控制項總覽](https://msdn.microsoft.com/library/zsyt68f1.aspx)   
[CSS 教學課程](http://www.w3schools.com/css/default.asp)

> [!div class="step-by-step"]
> [上一頁](create_the_data_access_layer.md)
> [下一頁](display_data_items_and_details.md)
