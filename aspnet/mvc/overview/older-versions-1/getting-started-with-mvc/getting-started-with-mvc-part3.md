---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
title: 加入視圖 |Microsoft Docs
author: shanselman
description: 這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。 建立可從資料庫讀取和寫入的簡單 web 應用程式。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: e8f1515c-c277-47ff-a23e-224118f13f02
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
msc.type: authoredcontent
ms.openlocfilehash: 462b1210c45da67058899193afcea973f3daf122
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581554"
---
# <a name="adding-a-view"></a>新增檢視

由[Scott Hanselman](https://github.com/shanselman)

> 這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。 您將建立可從資料庫讀取和寫入的簡單 web 應用程式。 請造訪[ASP.NET mvc 學習中心](../../../index.md)，以尋找其他 ASP.NET mvc 教學課程和範例。

在本節中，我們將探討如何讓我們的 HelloWorldController 類別使用視圖範本檔案，將產生的 HTML 回應完全封裝回用戶端。

讓我們從使用具有索引方法的視圖範本開始。 我們的方法稱為 Index，它位於 HelloWorldController 中。 目前，我們的 Index （）方法會傳回字串，內含在控制器類別中硬式編碼的訊息。

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample1.cs)]

現在讓我們將 Index 方法變更為，如下所示：

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample2.cs)]

現在讓我們將一個 View 範本新增至我們的專案，我們可以用來做為 Index （）方法。 若要這麼做，請以滑鼠右鍵按一下索引方法中間的某個位置，然後按一下 [加入視圖]。

![影像](getting-started-with-mvc-part3/_static/image1.png)

這會顯示 [新增視圖] 對話方塊，提供我們一些選項，讓我們瞭解如何建立可供索引方法使用的視圖範本。 目前，請不要變更任何專案，只要按一下 [新增] 按鈕即可。

[![加入視圖 對話方塊](getting-started-with-mvc-part3/_static/image3.png)](getting-started-with-mvc-part3/_static/image2.png)

按一下 [新增] 之後，新的資料夾和新的檔案就會出現在 [方案] 資料夾中，如下所示。 我現在在 Views 底下有一個 [HelloWorld] 資料夾，以及該資料夾內的一個 [Index .aspx] 檔案。

[![solutionexplorerwithindex](getting-started-with-mvc-part3/_static/image5.png)](getting-started-with-mvc-part3/_static/image4.png)

新的索引檔案也已經開啟並可供編輯。 在第一個 &lt;h2 下新增一些文字，&gt;索引&lt;/h2&gt;，例如 "Hello World"。

[!code-html[Main](getting-started-with-mvc-part3/samples/sample3.html)]

執行您的應用程式，並在瀏覽器中再次造訪[`http://localhost:xx/HelloWorld`](http://localhostxx) 。 在此範例中，控制器的索引方法不會執行任何工作，但會呼叫「傳回 View （）」，表示我們想要使用視圖範本檔案將回應轉譯回用戶端。 因為我們並未明確指定要使用的視圖範本檔案的名稱，所以 ASP.NET MVC 會預設為使用 \Views\HelloWorld 資料夾中的 default.aspx view 檔案。 現在我們會在我們的視圖中看到硬式編碼的字串。

[![索引-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image7.png)](getting-started-with-mvc-part3/_static/image6.png)

看起來不錯。 不過，請注意，瀏覽器的標題會顯示「索引」，而頁面上的大標題會顯示「我的 MVC 應用程式」。 讓我們變更這些。

### <a name="changing-views-and-master-pages"></a>變更視圖和主版頁面

首先，讓我們變更「我的 MVC 應用程式」文字。 該文字會共用並顯示在每個頁面上。 它實際上只會出現在我們的程式碼中的一個位置，即使它是在應用程式的每個頁面上也一樣。 移至方案總管中的 [/Views/Shared] 資料夾，然後開啟 [網站] 檔案。 此檔案稱為「主版頁面」，它是所有其他頁面都使用的共用「shell」。

請注意，在此檔案中顯示 ContentPlaceholder "MainContent" 的一些文字。

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample4.aspx)]

該預留位置就是您所建立的所有頁面都會顯示在主版頁面中「包裝」的位置。 請嘗試變更標題，然後執行您的應用程式並流覽多個頁面。 您會發現，您的一項變更會出現在多個頁面上。

[!code-html[Main](getting-started-with-mvc-part3/samples/sample5.html)]

現在每個頁面都會有主要標題，也就是「我的 MVC 電影應用程式」的 H1。 這會處理頂端的白色文字，並在所有頁面上共用。

以下是完整的網站，其中包含已變更的標題：

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample6.aspx)]

現在，讓我們變更 [索引] 頁面的標題。

開啟/HelloWorld/Index.aspx。 有兩個地方可以變更。 首先，出現在瀏覽器標題中的標題，然後是次要標題（也就是 H2）。 我要讓它們彼此略有不同，讓您可以看到哪一段程式碼變更了哪個部分的應用程式。

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample7.aspx)]

執行您的應用程式並造訪/Movies。 請注意，瀏覽器標題、主要標題和次要標題已變更。 您可以輕鬆地在您的應用程式中進行大幅變更，而對您的視圖進行小幅變更。

[![電影清單-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image9.png)](getting-started-with-mvc-part3/_static/image8.png)

有點「資料」（在此案例中為「Hello World！」 訊息）已硬式編碼。 我們有 V （Views），而我們已經有 C （控制器），但沒有 M （模型）。 我們很快就會逐步解說如何建立資料庫，並從中抓取模型資料。

## <a name="passing-a-viewmodel"></a>傳遞 ViewModel

不過，在我們進入資料庫並討論模型之前，先來談談「Viewmodel」。 這些物件代表將 HTML 回應轉譯回用戶端所需的視圖範本。 它們通常是由控制器類別建立並傳遞至視圖範本，而且應該只包含此視圖範本所需的資料，而且不再需要。

先前使用我們的 HelloWorld 範例，我們的歡迎（）動作方法會採用名稱和 Numtimes is 參數，並將它輸出到瀏覽器。 而不是讓控制器直接轉譯此回應，讓我們改為建立小型類別來保存該資料，然後將它傳遞至 View 範本，以使用它來呈現 HTML 回應。 如此一來，控制器就會關心一件事，另一個是「視圖」範本，讓我們能夠在應用程式中維持乾淨的「關注點分離」。

返回 HelloWorldController.cs 檔案並加入新的 "WelcomeViewModel" 類別，並在控制器內變更歡迎使用的方法。 以下是在相同檔案中具有新類別的完整 HelloWorldController.cs。

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample8.cs)]

雖然它是在多行上，但我們的歡迎方法其實只是兩個程式碼語句。 第一個語句會將我們的兩個參數封裝成 ViewModel 物件，而第二個會將產生的物件傳遞到 View。

現在我們需要一個歡迎視圖範本！ 以滑鼠右鍵按一下歡迎方法，然後選取 [加入視圖]。 此時，我們會核取 [建立強型別視圖]，然後從下拉式清單中選取我們的 WelcomeViewModel 類別。 這個新的視圖只會知道 WelcomeViewModels 和其他類型的物件。

> *注意：在新增的 WelcomeViewModel 之後，您必須編譯一次，才會顯示在下拉式清單中。*

您的 [加入視圖] 對話方塊看起來應該會像這樣。 按一下 [加入] 按鈕。 ![新增視圖已圈號](getting-started-with-mvc-part3/_static/image10.png)

將此程式碼新增至新的 [歡迎使用 .aspx] 中的 [&lt;h2]&gt; 之下。 我們會建立迴圈，並在使用者說出「我應該」的時候說「Hello」！

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample9.aspx)]

另外也請注意，因為我們告訴此 WelcomeViewModel （他們已結婚，請記住？），我們會在每次參考模型物件時取得有用的 Intellisense，如下列螢幕擷取畫面所示：

[![NumTime 原始程式碼](getting-started-with-mvc-part3/_static/image12.png)](getting-started-with-mvc-part3/_static/image11.png)

執行您的應用程式，並再次流覽 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`。 現在我們會從 URL 取得資料，並自動將其傳入控制器，我們的控制器會將資料封裝成 ViewModel，並將該物件傳遞至我們的 View。 視圖會將資料以 HTML 形式顯示給使用者。

[![歡迎使用-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image14.png)](getting-started-with-mvc-part3/_static/image13.png)

這就是模型的「M」類型，但不是資料庫種類。 讓我們來看看我們所學到的內容，並建立電影資料庫。

> [!div class="step-by-step"]
> [上一頁](getting-started-with-mvc-part2.md)
> [下一頁](getting-started-with-mvc-part4.md)
