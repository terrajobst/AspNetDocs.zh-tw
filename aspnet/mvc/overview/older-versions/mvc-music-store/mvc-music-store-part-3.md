---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
title: 第3部分： Views 和 Viewmodel |Microsoft Docs
author: jongalloway
description: 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第3部分涵蓋 Views 和 Viewmodel。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 94297aa0-1f2d-4d72-bbcb-63f64653e0c0
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
msc.type: authoredcontent
ms.openlocfilehash: 3fcfc816cde22c697a78bab2c9ea7ace1bf68501
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559805"
---
# <a name="part-3-views-and-viewmodels"></a>第3部分： Views 和 Viewmodel

依[Jon Galloway](https://github.com/jongalloway)

> MVC 音樂存放區是教學課程應用程式，其仲介紹如何使用 ASP.NET MVC 和 Visual Studio 進行 web 程式開發的逐步解說。  
>   
> MVC 音樂存放區是輕量的範例商店執行，可在線上銷售音樂專輯，並實行基本的網站管理、使用者登入和購物車功能。  
>   
> 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第3部分涵蓋 Views 和 Viewmodel。

到目前為止，我們只是從控制器動作傳回字串。 這是一種很好的方法，讓您瞭解控制器的工作方式，但不是您想要建立實際 web 應用程式的方式。 我們想要有更好的方法，讓您將 HTML 傳回到流覽網站的瀏覽器，我們可以使用範本檔案更輕鬆地自訂 HTML 內容送回。 這正是 Views 的功能。

## <a name="adding-a-view-template"></a>加入視圖範本

若要使用視圖範本，我們會將 HomeController Index 方法變更為傳回 ActionResult，並讓它返回 View （），如下所示：

[!code-csharp[Main](mvc-music-store-part-3/samples/sample1.cs)]

上述變更指出，而不是傳回字串，而是改為使用「View」來產生結果。

我們現在會將適當的視圖範本加入至專案。 若要這麼做，我們要將文字游標放在索引動作方法內，然後以滑鼠右鍵按一下並選取 [加入視圖]。 這會顯示 [新增視圖] 對話方塊：

![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)

[加入視圖] 對話方塊可讓我們快速且輕鬆地產生視圖範本檔案。 根據預設，[加入視圖] 對話方塊會預先填入要建立之視圖範本的名稱，使其符合將使用它的動作方法。 因為我們在 HomeController 的 Index （）動作方法中使用 [新增視圖] 操作功能表，所以上面的 [加入視圖] 對話方塊會有「索引」做為預設預先填入的視圖名稱。 我們不需要變更此對話方塊上的任何選項，因此，請按一下 [新增] 按鈕。

當我們按一下 [加入] 按鈕時，Visual Web Developer 會在 \Views\Home 目錄中為我們建立新的 [索引] 視圖範本，如果尚未存在，則建立資料夾。

![](mvc-music-store-part-3/_static/image2.png)

"Index. #" 檔案的名稱和資料夾位置很重要，並遵循預設的 ASP.NET MVC 命名慣例。 目錄名稱 \Views\Home 會符合名為 HomeController 的控制器。 [視圖] 範本名稱 [索引] 符合將顯示此視圖的控制器動作方法。

當我們使用此命名慣例來傳回視圖時，ASP.NET MVC 可讓我們避免必須明確指定視圖範本的名稱或位置。 當我們在 HomeController 中撰寫如下所示的程式碼時，它會預設呈現 \Views\Home\Index.cshtml view 範本：

[!code-csharp[Main](mvc-music-store-part-3/samples/sample2.cs)]

在我們按一下 [加入視圖] 對話方塊中的 [新增] 按鈕之後，Visual Web Developer 已建立並開啟 "Index. cshtml" 視圖範本。 如下列所示，會顯示索引. cshtml 的內容。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample3.cshtml)]

此視圖會使用 Razor 語法，這比 ASP.NET Web form 和舊版 ASP.NET MVC 中使用的 Web form view engine 更簡潔。 Web form view 引擎仍然可以在 ASP.NET MVC 3 中使用，但許多開發人員發現 Razor view 引擎很適合 ASP.NET MVC 開發。

前三行使用 ViewBag 來設定頁面標題。 我們很快就會介紹這項功能的運作方式，但首先讓我們更新文字標題文字並查看頁面。 將 &lt;h2&gt; 標記更新為 [這是首頁]，如下所示。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample4.cshtml)]

執行應用程式時，會顯示在首頁上可以看到我們的新文字。

![](mvc-music-store-part-3/_static/image3.png)

## <a name="using-a-layout-for-common-site-elements"></a>使用通用網站元素的版面配置

大部分網站都有許多頁面之間共用的內容：導覽、頁尾、標誌影像、樣式表單參考等等。Razor view 引擎可讓您輕鬆地使用稱為 \_Layout 的頁面來進行管理，並在/Views/Shared 資料夾內自動為我們建立。

![](mvc-music-store-part-3/_static/image4.png)

按兩下此資料夾以查看內容，如下所示。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample5.cshtml)]

來自個別視圖的內容將會由 @RenderBody（）命令顯示，而我們想要出現在外的任何一般內容，都可以加入 \_Layout 標記中。 我們會想要讓 MVC 音樂存放區有一個通用標題，其中包含首頁的連結，以及網站中所有頁面的存放區，因此我們會將其新增至範本中的 @RenderBody（）語句正上方。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample6.cshtml)]

## <a name="updating-the-stylesheet"></a>更新樣式表單

空白專案範本包含非常簡單的 CSS 檔案，其中只包含用來顯示驗證訊息的樣式。 我們的設計工具提供了一些額外的 CSS 和影像，可定義網站的外觀與風格，因此我們將在現在新增這些功能。

已更新的 CSS 檔案和影像會包含在 MvcMusicStore-Assets 的內容目錄中，可在 [ [MVC-音樂] 存放區](https://github.com/evilDave/MVC-Music-Store)取得。 我們會在 Windows Explorer 中選取這兩個專案，並將其放入 Visual Web Developer 中解決方案的 Content 資料夾，如下所示：

![](mvc-music-store-part-3/_static/image5.png)

系統會要求您確認是否要覆寫現有的網站 .css 檔案。 按一下 [是]。

![](mvc-music-store-part-3/_static/image6.png)

應用程式的 Content 資料夾現在會如下所示：

![](mvc-music-store-part-3/_static/image7.png)

現在讓我們來執行應用程式，並在首頁上查看變更的外觀。

![](mvc-music-store-part-3/_static/image8.png)

- 讓我們來複習一下變更的內容： HomeController 的索引動作方法已找到並顯示 \Views\Home\Index.cshtmlView 範本，雖然我們的程式碼稱為 "return View （）"，因為我們的視圖範本遵循標準命名慣例。
- 首頁會顯示在 \Views\Home\Index.cshtml view 範本內定義的簡單歡迎訊息。
- 首頁是使用我們的 \_Layout 範本，因此歡迎訊息包含在標準網站 HTML 版面配置中。

## <a name="using-a-model-to-pass-information-to-our-view"></a>使用模型將資訊傳遞至我們的視圖

只顯示硬式編碼 HTML 的視圖範本不會產生非常有趣的網站。 為了建立動態網站，我們會改為將控制器動作的資訊傳遞至我們的視圖範本。

在模型視圖控制器模式中，「模型」一詞指的是代表應用程式中資料的物件。 通常，模型物件會對應至資料庫中的資料表，但不一定要這麼做。

傳回 ActionResult 的控制器動作方法可以將模型物件傳遞給視圖。 這可讓控制器完全封裝產生回應所需的所有資訊，然後將此資訊傳送到 View 範本，用來產生適當的 HTML 回應。 藉由查看其運作方式最容易瞭解，讓我們開始吧。

首先，我們將建立一些模型類別，以代表我們存放區內的內容類型和專輯。 讓我們從建立內容類型類別開始。 以滑鼠右鍵按一下專案中的 [模型] 資料夾，選擇 [新增類別] 選項，並將檔案命名為 "Genre.cs"。

![](mvc-music-store-part-3/_static/image2.jpg)

![](mvc-music-store-part-3/_static/image9.png)

然後將 [公用字串名稱] 屬性加入至已建立的類別：

[!code-csharp[Main](mvc-music-store-part-3/samples/sample7.cs)]

*注意：如果您想要的話，{get; set;} 標記法會使用C#的自動執行屬性功能。這讓我們有屬性的優點，而不需要我們宣告支援欄位。*

接下來，請遵循相同的步驟來建立具有 [標題] 和 [內容類型] 屬性的專輯類別（名為 Album.cs）：

[!code-csharp[Main](mvc-music-store-part-3/samples/sample8.cs)]

現在我們可以修改 StoreController，以使用可顯示模型中動態資訊的 Views。 如果現在是-基於示範目的，我們根據要求識別碼來命名專輯，我們可以如下圖所示顯示該資訊。

![](mvc-music-store-part-3/_static/image10.png)

我們會先變更 [Store Details] 動作，讓它顯示單一專輯的資訊。 在**StoreControllers**類別的頂端新增 "using" 語句以包含 MvcMusicStore 命名空間，因此我們不需要在每次想要使用專輯類別時輸入 MvcMusicStore。 該類別的 "using" 區段現在應該會顯示如下。

[!code-csharp[Main](mvc-music-store-part-3/samples/sample9.cs)]

接下來，我們會更新詳細資料控制器動作，讓它傳回 ActionResult，而不是字串，就像我們使用 HomeController 的 Index 方法所做的一樣。

[!code-csharp[Main](mvc-music-store-part-3/samples/sample10.cs)]

現在我們可以修改邏輯，將專輯物件傳回給視圖。 稍後在本教學課程中，我們將從資料庫中抓取資料，但現在我們會使用「虛擬資料」來開始。

[!code-csharp[Main](mvc-music-store-part-3/samples/sample11.cs)]

*注意：如果您不熟悉C#，您可能會假設使用 var 表示我們的專輯變數是晚期繫結。這不正確， C#編譯器會根據我們指派給變數的內容來使用型別推斷，以判斷專輯是專輯類型，並將本機專輯變數編譯為專輯類型，因此我們會取得編譯時期檢查，並 Visual Studio 程式碼編輯器支援。*

現在讓我們建立一個使用專輯的視圖範本來產生 HTML 回應。 在這麼做之前，我們必須先建立專案，讓 [加入視圖] 對話方塊知道我們新建立的專輯類別。 您可以藉由選取 [Debug ⇨ Build MvcMusicStore] 功能表項目來建立專案（如需額外的點數，您可以使用 Ctrl + Shift-B 快捷方式來建立專案）。

![](mvc-music-store-part-3/_static/image11.png)

既然我們已設定支援的類別，我們就可以開始建立我們的 View 範本。 以滑鼠右鍵按一下詳細資料方法，然後選取 [加入視圖 ...]從內容功能表。

![](mvc-music-store-part-3/_static/image12.png)

我們會建立新的視圖範本，就像我們之前使用 HomeController 一樣。 因為我們是從 StoreController 建立它，所以預設會在 \Views\Store\Index.cshtml 檔案中產生。

與之前不同的是，我們要核取 [建立強型別] 核取方塊。 接著，我們要在「View data class」（downlist）中選取「專輯」類別。 這會導致 [加入視圖] 對話方塊建立一個需要將專輯物件傳遞給它使用的視圖範本。

![](mvc-music-store-part-3/_static/image13.png)

當我們按一下 [新增] 按鈕時，將會建立 \Views\Store\Details.cshtml View 範本，其中包含下列程式碼。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample12.cshtml)]

請注意第一行，這表示此視圖已針對我們的專輯類別進行強型別。 Razor view 引擎瞭解它已通過專輯物件，因此我們可以輕鬆地存取模型屬性，甚至能夠在 Visual Web Developer editor 中取得 IntelliSense 的優點。

更新 &lt;h2&gt; 標記，讓它藉由修改該行以顯示專輯的 Title 屬性，如下所示。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample13.cshtml)]

請注意，當您在 @Model 關鍵字之後輸入句點時，會觸發 IntelliSense，其中顯示專輯類別支援的屬性和方法。

現在讓我們重新執行專案，並造訪/Store/Details/5 URL。 我們會看到專輯的詳細資料，如下所示。

![](mvc-music-store-part-3/_static/image14.png)

現在，我們將針對 Store 流覽動作方法進行類似的更新。 更新方法，使其傳回 ActionResult，並修改方法邏輯，讓它建立新的類型物件，並將它傳回給視圖。

[!code-csharp[Main](mvc-music-store-part-3/samples/sample14.cs)]

在流覽方法上按一下滑鼠右鍵，然後選取 [新增 View ...]從操作功能表中，新增強型別的視圖，將強型別加入至內容類型類別。

![](mvc-music-store-part-3/_static/image15.png)

更新 view 程式碼中的 &lt;h2&gt; 元素（在/Views/Store/Browse.cshtml 中），以顯示內容類型資訊。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample15.cshtml)]

現在讓我們重新執行專案，並流覽至/Store/Browse？內容類型 = Disco URL。 我們會看到如下所示的流覽頁面。

![](mvc-music-store-part-3/_static/image16.png)

最後，讓我們對**存放區索引**動作方法和 view 進行稍微比較複雜的更新，以顯示我們存放區中所有內容的清單。 我們會使用內容清單做為模型物件，而不只是單一內容類型來執行此動作。

[!code-csharp[Main](mvc-music-store-part-3/samples/sample16.cs)]

以滑鼠右鍵按一下 [存放區索引動作] 方法，然後依序選取 [加入視圖]，選取 [內容類型] 做為模型類別，然後按 [加入] 按鈕。

![](mvc-music-store-part-3/_static/image17.png)

首先，我們將變更 @model 宣告，以指出此視圖會預期有數個內容類型物件，而不是只有一個。 將/Store/Index.cshtml 的第一行變更為 [讀取]，如下所示：

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample17.cshtml)]

這會告訴 Razor view 引擎，它將使用可以保存數個內容類型物件的模型物件。 我們使用 IEnumerable&lt;內容類型&gt;，而不是清單&gt;&lt;類型類型，因為它較通用，可讓我們將模型類型稍後變更為支援 IEnumerable 介面的任何物件類型。

接下來，我們會迴圈處理模型中的內容類型物件，如下列已完成的視圖程式碼所示。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample18.cshtml)]

請注意，當我們輸入這段程式碼時，我們有完整的 IntelliSense 支援，因此當我們鍵入「@Model」時。 我們會看到型別類型的 IEnumerable 所支援的所有方法和屬性。

![](mvc-music-store-part-3/_static/image18.png)

在我們的 "foreach" 迴圈內，Visual Web Developer 知道每個專案都屬於類型類型，因此我們會看到每個類型的 IntelliSense。

![](mvc-music-store-part-3/_static/image19.png)

接下來，[樣板] 功能會檢查內容類型物件，並判斷每個都有一個 Name 屬性，因此它會迴圈執行並將其寫出。它也會產生每個個別專案的編輯、詳細資料和刪除連結。 我們稍後將在我們的存放區管理員中利用這項功能，但現在我們想要改為使用簡單的清單。

當我們執行應用程式並流覽至/Store 時，我們會看到顯示的是 [計數] 和 [清單]。

![](mvc-music-store-part-3/_static/image20.png)

## <a name="adding-links-between-pages"></a>在頁面之間新增連結

列出內容類型的/Store URL 目前只會將內容類型名稱列出為純文字。 讓我們變更此專案，讓我們改為將內容類型名稱連結至適當的/Store/Browse URL，讓按一下音樂類型（如「Disco」）會流覽至/Store/Browse？內容類型 = Disco URL。 我們可以使用如下的程式碼來更新 \Views\Store\Index.cshtml View 範本，以輸出這些連結 **（不要在此輸入-我們將在此進行改善）** ：

[!code-html[Main](mvc-music-store-part-3/samples/sample19.html)]

這是可行的，但之後可能會導致問題，因為它依賴硬式編碼的字串。 比方說，如果我們想要重新命名控制器，我們需要搜尋程式碼，尋找需要更新的連結。

我們可以使用的替代方法是利用 HTML Helper 方法。 ASP.NET MVC 包含 HTML Helper 方法，可從我們的 View 範本程式碼取得，以執行像這樣的各種常見工作。 .Html （） helper 方法特別有用，可讓您輕鬆地建立 HTML &lt;&gt; 連結，並處理討厭的詳細資料，例如確定 URL 路徑的 URL 編碼正確。

.Html （）有數個不同的多載，可讓您盡可能指定連結所需的資訊。 在最簡單的情況下，只要按一下用戶端上的超連結，您就只會提供連結文字和動作方法來移至。 例如，我們可以使用下列呼叫，連結至存放區詳細資料頁面上的 "/Store/" Index （）方法，並將連結文字「移至存放區索引」：

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample20.cshtml)]

*注意：在此情況下，我們不需要指定控制器名稱，因為我們只會連結至呈現目前視圖的相同控制器內的另一個動作。*

我們的流覽頁面連結必須傳遞參數，因此我們將會使用採用三個參數的 .Html 方法的另一個多載：

- 1. 連結文字，會顯示內容類型名稱
- 2. 控制器動作名稱（流覽）
- 3. 路由參數值，同時指定名稱（內容類型）和值（內容類型名稱）

總之，以下是我們將這些連結寫到商店索引視圖的方式：

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample21.cshtml)]

現在當我們再次執行專案並存取/Store/URL 時，我們會看到一份內容清單。 每個內容類型都是超連結–按一下時，會將我們帶到我們的/Store/Browse？內容類型 = [內容類型 *]* URL。

![](mvc-music-store-part-3/_static/image3.jpg)

內容類型清單的 HTML 看起來像這樣：

[!code-html[Main](mvc-music-store-part-3/samples/sample22.html)]

> [!div class="step-by-step"]
> [上一頁](mvc-music-store-part-2.md)
> [下一頁](mvc-music-store-part-4.md)
