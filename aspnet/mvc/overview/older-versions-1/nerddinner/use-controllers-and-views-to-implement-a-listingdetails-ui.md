---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: 使用控制器和 Views 來執行清單/詳細資料 UI |Microsoft Docs
author: microsoft
description: 步驟4顯示如何將控制器新增至應用程式，利用我們的模型為使用者提供資料清單/詳細導覽體驗 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 74319fe5ea4c79b50140834349e2fdf86420cfbb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600741"
---
# <a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a>使用控制器和檢視來實作清單/詳細資料 UI

由[Microsoft](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md)課程的步驟4，逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的 web 應用程式。
> 
> 步驟4顯示如何將控制器新增至應用程式，以利用我們的模型在我們的 NerdDinner 網站上為使用者提供 dinners 的資料列/詳細導覽體驗。
> 
> 如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。

## <a name="nerddinner-step-4-controllers-and-views"></a>NerdDinner 步驟4：控制器和 Views

使用傳統的 web 架構（傳統 ASP、PHP、ASP.NET Web form 等等）時，連入 Url 通常會對應到磁片上的檔案。 例如： "/Products.aspx" 或 "/Products.php" 等 URL 的要求可能會由 "Products" 或 "Products. php" 檔案處理。

以 Web 為基礎的 MVC 架構會以稍有不同的方式將 Url 對應至伺服器程式碼。 與其將傳入 Url 對應至檔案，它們會改為將 Url 對應至類別上的方法。 這些類別稱為「控制器」，負責處理傳入 HTTP 要求、處理使用者輸入、抓取和儲存資料，以及判斷要傳回給用戶端的回應（顯示 HTML、下載檔案、重新導向至不同的URL 等）。

既然我們已為 NerdDinner 應用程式建立基本模型，下一步就是將控制器新增至應用程式，利用它來為使用者提供 Dinners 在我們網站上的資料列/詳細導覽體驗。

### <a name="adding-a-dinnerscontroller-controller"></a>新增 DinnersController 控制器

首先，以滑鼠右鍵按一下 Web 專案中的 [控制器] 資料夾，然後選取 [**新增&gt;控制器**] 功能表命令（您也可以輸入 Ctrl-M、ctrl-c 來執行此命令）：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

這會顯示 [新增控制器] 對話方塊：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

我們會將新的控制器命名為 "DinnersController"，然後按一下 [新增] 按鈕。 Visual Studio 接著會在 \Controllers 目錄下新增 DinnersController.cs 檔案：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

它也會在程式碼編輯器中開啟新的 DinnersController 類別。

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a>將 Index （）和 Details （）動作方法加入至 DinnersController 類別

我們想要讓訪客使用我們的應用程式流覽即將推出的 dinners 清單，並允許他們按一下清單中的任何晚餐，以查看其相關特定的詳細資料。 我們將從我們的應用程式發佈下列 Url 來完成這項操作：

| **URL** | **目的** |
| --- | --- |
| */Dinners/* | 顯示即將推出的 dinners HTML 清單 |
| */Dinners/Details/[識別碼]* | 顯示在 URL 中內嵌的「識別碼」參數所指示之特定晚餐的詳細資料–這會符合資料庫中晚餐的 DinnerID。 例如：/Dinners/Details/2 會顯示 HTML 頁面，其中包含其 DinnerID 值為2之晚餐的詳細資料。 |

我們會將兩個公用的「動作方法」新增至我們的 DinnersController 類別，以發佈這些 Url 的初始執行，如下所示：

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

接著，我們會執行 NerdDinner 應用程式，並使用我們的瀏覽器來叫用它們。 在 *"/Dinners/"* URL 中輸入會導致我們的*Index （）* 方法執行，並傳回下列回應：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

輸入 *"/Dinners/Details/2"* URL 會導致我們的*Details （）* 方法執行，並傳回下列回應：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

您可能會想： ASP.NET MVC 如何知道如何建立 DinnersController 類別並叫用這些方法？ 若要瞭解這一點，讓我們快速查看路由的運作方式。

### <a name="understanding-aspnet-mvc-routing"></a>瞭解 ASP.NET MVC 路由

ASP.NET MVC 包含強大的 URL 路由引擎，可提供很大的彈性來控制 Url 對應至控制器類別的方式。 它可讓我們完全自訂 ASP.NET MVC 如何選擇要建立的控制器類別、要在其上叫用的方法，以及設定變數可以從 URL/Querystring 自動剖析並當做參數引數傳遞至方法的不同方式。 它提供彈性來完全優化 SEO 的網站（搜尋引擎優化），並從應用程式發佈所需的任何 URL 結構。

根據預設，新的 ASP.NET MVC 專案會隨附一組預先設定的 URL 路由規則已註冊。 這可讓我們輕鬆地開始使用應用程式，而不需要明確地設定任何專案。 您可以在專案的 [應用程式] 類別中找到預設的路由規則註冊，我們可以按兩下專案根目錄中的 "global.asax" 檔案來開啟它：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

預設 ASP.NET MVC 路由規則會在此類別的 "RegisterRoutes" 方法中註冊：

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

「路由」。上述的 Maproute.html （） "方法呼叫會註冊預設路由規則，其會使用 URL 格式將傳入 Url 對應至控制器類別："/{controller}/{action}/{id} "–其中" controller "是要具現化的控制器類別名稱，" action "是要在其上叫用之公用方法的名稱，而" id "是內嵌在 URL 內的選擇性參數，可當做引數傳遞給方法。 傳遞至 "Maproute.html （）" 方法呼叫的第三個參數是一組預設值，如果它們不存在於 URL 中（控制器 = "Home"，Action = "Index"，Id = ""），就會在控制器/動作/識別碼的值中使用。

以下表格示範如何使用預設的 "<em>/{controllers}/{action}/{id}"</em>路由規則來對應各種 url：

| **URL** | **控制器類別** | **動作方法** | **傳遞的參數** |
| --- | --- | --- | --- |
| */Dinners/Details/2* | DinnersController | 詳細資料（識別碼） | 識別碼 = 2 |
| */Dinners/Edit/5* | DinnersController | 編輯（id） | 識別碼 = 5 |
| */Dinners/Create* | DinnersController | Create() | N/A |
| */Dinners* | DinnersController | Index （） | N/A |
| */Home* | HomeController | Index （） | N/A |
| */* | HomeController | Index （） | N/A |

最後三個數據列會顯示使用的預設值（控制器 = Home，Action = Index，Id = ""）。 因為 "Index" 方法已註冊為預設動作名稱（如果未指定），所以 "/Dinners" 和 "/Home" Url 會使 Index （）動作方法在其控制器類別上叫用。 因為 "Home" 控制器已註冊為預設控制器（如果未指定），所以 "/" URL 會導致建立 HomeController，並在其上叫用 Index （）動作方法。

如果您不喜歡這些預設的 URL 路由規則，好消息是可以輕鬆地進行變更，只要在上面的 RegisterRoutes 方法中編輯它們即可。 不過，針對我們的 NerdDinner 應用程式，我們不會變更任何預設的 URL 路由規則，而是改為直接使用它們。

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a>從我們的 DinnersController 使用 DinnerRepository

現在讓我們將 DinnersController 的 Index （）和 Details （）動作方法的目前執行，取代為使用我們模型的程式。

我們將使用稍早建立的 DinnerRepository 類別來執行此行為。 首先，我們會新增一個參考 "NerdDinner" 命名空間的 "using" 語句，然後在 DinnerController 類別上宣告 DinnerRepository 的實例作為欄位。

我們將在本章稍後介紹「相依性插入」的概念，並顯示另一種方式，讓我們的控制器取得對 DinnerRepository 的參考，以進行更好的單元測試，但現在我們只會建立 DinnerRepository 的實例。內嵌，如下所示。

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

現在，我們已準備好使用我們抓取的資料模型物件來產生 HTML 回應。

### <a name="using-views-with-our-controller"></a>搭配我們的控制器使用 Views

雖然您可以在動作方法中撰寫程式碼來組合 HTML，然後使用*Response （）* helper 方法將它傳回給用戶端，但該方法會變得相當難以處理。 更好的方法是讓我們只在 DinnersController 動作方法內執行應用程式和資料邏輯，然後將呈現 HTML 回應所需的資料傳遞至個別的「view」範本，以負責輸出 HTML 標記法其中的。 如我們稍後所見，「view」範本是一個文字檔，通常包含 HTML 標籤和內嵌呈現程式碼的組合。

將我們的控制器邏輯與我們的視圖轉譯分開，可提供數個大優勢。 特別是，這有助於在應用程式代碼和 UI 格式設定/轉譯程式碼之間，強制執行明確的「關注點分離」。 這可讓您更輕鬆地對應用程式邏輯進行單元測試，而不受 UI 轉譯邏輯的隔離。 這可讓您更輕鬆地修改 UI 轉譯範本，而不需要變更應用程式程式碼。 而且它可以讓開發人員和設計人員更輕鬆地在專案上共同作業。

我們可以更新 DinnersController 類別，以指出我們想要使用視圖範本來傳回 HTML UI 回應，方法是變更兩個動作方法的方法簽章，使其傳回型別為 "void"，而改用 "ActionResult" 的傳回型別。 然後，我們可以在控制器基類上呼叫*View （）* helper 方法，傳回 "ViewResult" 物件，如下所示：

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

我們在上面使用的*View （）* helper 方法的簽章如下所示：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

*View （）* helper 方法的第一個參數是我們想要用來呈現 HTML 回應的視圖範本檔案名。 第二個參數是模型物件，其中包含視圖範本所需的資料，以便呈現 HTML 回應。

在我們的 Index （）動作方法中，我們會呼叫*View （）* helper 方法，並指出我們想要使用「索引」視圖範本來呈現 DINNERS 的 HTML 清單。 我們會傳遞一個晚餐物件序列給此視圖範本，以產生下列清單：

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

在我們的 Details （）動作方法中，我們嘗試使用 URL 中提供的識別碼來抓取晚餐物件。 如果找到有效的晚餐，我們會呼叫*View （）* 協助程式方法，表示我們想要使用「詳細資料」視圖範本來呈現抓取的晚餐物件。 如果要求的晚餐無效，我們會轉譯一個有用的錯誤訊息，指出晚餐不是使用 "NotFound" view 範本（和只接受範本名稱的*view （）* helper 方法的多載版本）：

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

現在讓我們來執行「NotFound」、「Details」和「Index」視圖範本。

### <a name="implementing-the-notfound-view-template"></a>執行 "NotFound" View 範本

我們一開始會先執行「NotFound」視圖範本，這會顯示一個易記的錯誤訊息，指出找不到所要求的晚餐。

我們會建立新的 view 範本，方法是將文字游標放在控制器動作方法中，然後以滑鼠右鍵按一下並選擇 [新增視圖] 功能表命令（我們也可以輸入 Ctrl-M、Ctrl-c 來執行此命令）：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

這會顯示 [新增視圖] 對話方塊，如下所示。 根據預設，對話方塊會預先填入要建立的視圖名稱，以符合在啟動對話時游標所在的動作方法名稱（在此案例中為「詳細資料」）。 因為我們想要先執行「NotFound」範本，所以我們將覆寫此視圖名稱，並將它設定為「NotFound」：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

當我們按一下 [新增] 按鈕時，Visual Studio 會在 "\Views\Dinners" 目錄中為我們建立新的 "NotFound" 視圖範本（如果目錄不存在，也會建立）：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

它也會在程式碼編輯器中開啟新的「NotFound .aspx」視圖範本：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

根據預設，視圖範本有兩個「內容區域」，我們可以在其中新增內容和程式碼。 第一個可讓我們自訂送回之 HTML 網頁的「標題」。 第二個可讓我們自訂送回之 HTML 網頁的「主要內容」。

若要執行我們的「NotFound」視圖範本，我們將新增一些基本內容：

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

然後，我們可以在瀏覽器內試用它。 若要這麼做，讓我們要求 *"/Dinners/Details/9999"* URL。 這會參考目前不存在於資料庫中的晚餐，並會導致我們的 DinnersController （）動作方法呈現我們的 "NotFound" 視圖範本：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

您在上面的螢幕擷取畫面中會注意到的一件事，就是我們的「基本觀點」範本繼承了一堆圍繞螢幕上主要內容的 HTML。 這是因為我們的視圖範本使用「主版頁面」範本，可讓我們在網站上的所有視圖中套用一致的版面配置。 我們將在本教學課程稍後的部分討論主版頁面的工作方式。

### <a name="implementing-the-details-view-template"></a>執行「詳細資料」視圖範本

現在，讓我們來執行「詳細資料」視圖範本，這會針對單一晚餐模型產生 HTML。

若要這麼做，請將文字游標放在詳細資料動作方法中，然後以滑鼠右鍵按一下並選擇 [加入視圖] 功能表命令（或按下 Ctrl-M、Ctrl + V）：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

這會顯示 [新增視圖] 對話方塊。 我們會保留預設的視圖名稱（「詳細資料」）。 我們也會選取對話方塊中的 [建立強型別視圖] 核取方塊，然後選取（使用 combobox 下拉式清單）我們從控制器傳遞至視圖的模型類型名稱。 在此視圖中，我們會傳遞晚餐物件（此類型的完整名稱為： "NerdDinner"）：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

不同于先前的範本，我們選擇建立「空的視圖」，這次我們會選擇使用「詳細資料」範本自動「scaffold」此視圖。 我們可以藉由變更上述對話方塊中的 [視圖內容] 下拉式功能表來指出這一點。

「架構」會根據我們要傳遞給它的晚餐物件，產生詳細資料檢視範本的初始執行。 這可讓我們快速地開始使用我們的視圖範本。

當我們按一下 [新增] 按鈕時，Visual Studio 會在 "\Views\Dinners" 目錄中為我們建立新的 "default.aspx" view 範本檔案：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

它也會在程式碼編輯器中開啟新的「詳細資料 .aspx」視圖範本。 它將包含以晚餐模型為基礎之詳細資料檢視的初始 scaffold 執行。 此樣板引擎會使用 .NET 反映來查看傳遞給它的類別所公開的公用屬性，並根據它找到的每個類型來新增適當的內容：

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

我們可以要求 *"/Dinners/Details/1"* URL，以查看此「詳細資料」 scaffold 在瀏覽器中的執行外觀。 使用此 URL 時，將會顯示我們在第一次建立資料庫時，手動新增至資料庫的其中一個 dinners：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

這會讓我們快速啟動並執行，並為我們提供詳細資料 .aspx 視圖的初始程式。 然後我們可以調整它，以自訂 UI 以符合我們的滿意度。

當我們更仔細查看 default.aspx 範本時，我們會發現它包含靜態 HTML 和內嵌的轉譯程式碼。 &lt;%%&gt; 程式碼區塊會在視圖範本呈現時執行程式碼，而 &lt;% =%&gt; 程式碼區塊執行其中包含的程式碼，然後將結果轉譯為範本的輸出資料流程。

我們可以在我們的觀點中撰寫程式碼，以存取使用強型別「模型」屬性從我們的控制器傳遞的「晚餐」模型物件。 Visual Studio 在編輯器中存取此 "Model" 屬性時，會提供完整的程式碼 intellisense：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

讓我們進行一些調整，讓最終詳細資料檢視範本的來源看起來如下：

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

當我們再次存取 *"/Dinners/Details/1"* URL 時，它現在會呈現如下：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a>執行「索引」視圖範本

現在讓我們來執行「Index」 view 範本，這會產生即將推出的 Dinners 清單。 為此，我們會將文字游標放在索引動作方法內，然後以滑鼠右鍵按一下並選擇 [加入視圖] 功能表命令（或按 Ctrl-M、Ctrl + V）。

在 [加入視圖] 對話方塊中，我們會保留名為 "Index" 的視圖範本，然後選取 [建立強型別的視圖] 核取方塊。 這次我們會選擇自動產生「清單」視圖範本，並選取「NerdDinner」作為模型類型傳遞至「視圖」（因為我們指出我們要建立「清單」 scaffold 會使 [加入視圖] 對話方塊假設我們是將一系列的晚餐物件從我們的控制器傳遞至視圖）：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

當我們按一下 [新增] 按鈕時，Visual Studio 會在 "\Views\Dinners" 目錄中為我們建立新的 "Index .aspx" view 範本檔案。 它會「scaffold」它在其中的初始執行，它會提供一個 HTML 資料表，列出我們傳遞給視圖的 Dinners。

當我們執行應用程式並存取 *"/Dinners/"* URL 時，它會轉譯我們的 Dinners 清單，如下所示：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

上述資料表解決方案提供我們晚餐資料的類似方格版面配置，這不是我們想要取用者面向晚餐的清單。 我們可以更新 default.aspx view 範本並加以修改，以列出較少的資料行，並使用 &lt;的 ul&gt; 元素來轉譯它們，而不是使用下列程式碼來呈現資料表：

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

我們使用上述 foreach 語句內的 "var" 關鍵字，因為我們會在我們的模型中迴圈處理每個晚餐。 不熟悉C# 3.0 的人可能會認為使用「var」表示晚餐物件是晚期繫結。 相反地，編譯器會針對強型別 "Model" 屬性（其型別為 "IEnumerable&lt;晚餐&gt;"）使用類型推斷，並將當地的「晚餐」變數編譯為晚餐類型，這表示我們會在程式碼區塊內取得完整的 intellisense 和編譯時間檢查：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

當我們在瀏覽器中按下 */Dinners* URL 的重新整理時，我們的更新視圖現在如下所示：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

這看起來更好，但尚未完成。 最後一個步驟是讓使用者按一下清單中的個別 Dinners，並查看其相關詳細資料。 我們會藉由呈現連結至 DinnersController 上 Details 動作方法的 HTML 超連結元素，來執行這項操作。

我們可以透過兩種方式的其中一種，在索引視圖內產生這些超連結。 第一個是手動建立 HTML &lt;如下所示的&gt; 元素，我們會在 &lt;HTML 專案中內嵌 &lt;%%&gt; 區塊：&gt;

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

我們可以使用的替代方法，是利用 ASP.NET MVC 中的內建 "Html.actionlink （）" helper 方法，以程式設計方式建立 HTML &lt;&gt; 元素，該專案會連結至控制器上的另一個動作方法：

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

Html 的第一個參數。 Html.actionlink （） helper 方法是要顯示的連結文字（在此案例中為晚餐的標題），第二個參數是我們想要產生連結的控制器動作名稱（在此案例中為 Details 方法），而第三個參數是要傳送至動作的一組參數（實作為具有屬性名稱/值的匿名型別）。 在此情況下，我們會指定我們想要連結的晚餐的「識別碼」參數，而且因為 ASP.NET MVC 中的預設 URL 路由規則是 "{Controller}/{Action}/{id}"，所以 .Html （） helper 方法會產生下列輸出：

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

針對我們的 Index .aspx view，我們將使用 Html.actionlink （） helper 方法方法，並將清單中的每個晚餐連結至適當的詳細資料 URL：

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

現在當我們達到 */Dinners* URL 時，我們的晚餐清單如下所示：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

當我們按一下清單中的任何 Dinners 時，我們會流覽以查看其詳細資料：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a>以慣例為基礎的命名和 \Views 目錄結構

在解析視圖範本時，預設會 ASP.NET MVC 應用程式使用以慣例為基礎的目錄命名結構。 這可讓開發人員在參考控制器類別內的視圖時，避免必須完整限定位置路徑。 根據預設，ASP.NET MVC 會在應用程式底下的 * \Views\[ControllerName]\* 目錄中尋找視圖範本檔案。

例如，我們一直在處理 DinnersController 類別，它會明確參考三個視圖範本：「索引」、「詳細資料」和「NotFound」。 ASP.NET MVC 預設會在應用程式根目錄底下的 *\Views\Dinners*目錄中尋找這些 views：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

請注意，專案中目前有三個控制器類別（DinnersController、HomeController 和 AccountController –在建立專案時，預設會新增最後兩個），而且有三個子目錄（每個目錄各有一個）控制器），在 \Views 目錄中。

從 Home 和 Accounts 控制器參考的視圖，會自動從個別的 *\Views\Home*和 *\Views\Account*目錄解析其視圖範本。 *\Views\Shared*子目錄提供了一種方式，可以儲存跨應用程式內多個控制器重複使用的視圖範本。 當 ASP.NET MVC 嘗試解析視圖範本時，它會先在 *\Views\[Controller]* 特定目錄內進行檢查，如果找不到 view 範本，它會在 *\Views\Shared*目錄中尋找。

在命名個別的視圖範本時，建議的指引是讓視圖範本共用與造成它呈現的動作方法相同的名稱。 例如，上面的「索引」動作方法會使用「索引」視圖來轉譯視圖結果，而「詳細資料」動作方法會使用「詳細資料」視圖來呈現其結果。 這可讓您輕鬆地快速查看與每個動作相關聯的範本。

當視圖範本的名稱與在控制器上叫用的動作方法相同時，開發人員不需要明確指定視圖範本名稱。 我們可以改為只將模型物件傳遞給 "View （）" 協助程式方法（不指定視圖名稱），而 ASP.NET MVC 會自動推斷要使用磁片上的 *\Views\[ControllerName]\[ActionName]* View 範本來呈現它。

這可讓我們稍微清理我們的控制器程式碼，並避免在我們的程式碼中重複此名稱兩次：

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

上述程式碼就是為網站實現絕佳晚餐清單/詳細資料體驗所需的一切。

#### <a name="next-step"></a>後續步驟

我們現在已建立好的晚餐流覽體驗。

現在讓我們啟用 CRUD （建立、讀取、更新、刪除）資料表單編輯支援。

> [!div class="step-by-step"]
> [上一頁](build-a-model-with-business-rule-validations.md)
> [下一頁](provide-crud-create-read-update-delete-data-form-entry-support.md)
