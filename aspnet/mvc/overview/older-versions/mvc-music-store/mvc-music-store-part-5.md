---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
title: 第5部分：編輯表單和範本化 |Microsoft Docs
author: jongalloway
description: 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第5部分涵蓋編輯表單和範本化。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 6b09413a-6d6a-425a-87c9-629f91b91b28
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
msc.type: authoredcontent
ms.openlocfilehash: 20b99cbe57b5dfa623205838a5929733a6c2d70d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559546"
---
# <a name="part-5-edit-forms-and-templating"></a>第5部分：編輯表單和範本化

依[Jon Galloway](https://github.com/jongalloway)

> MVC 音樂存放區是教學課程應用程式，其仲介紹如何使用 ASP.NET MVC 和 Visual Studio 進行 web 程式開發的逐步解說。  
>   
> MVC 音樂存放區是輕量的範例商店執行，可在線上銷售音樂專輯，並實行基本的網站管理、使用者登入和購物車功能。
> 
> 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第5部分涵蓋編輯表單和範本化。

在過去的章節中，我們會從資料庫載入資料並加以顯示。 在本章中，我們也會啟用資料的編輯。

## <a name="creating-the-storemanagercontroller"></a>建立 StoreManagerController

首先，我們會建立名為**StoreManagerController**的新控制器。 在此控制器中，我們將會利用 ASP.NET MVC 3 工具更新中提供的基本架構功能。 設定 [新增控制器] 對話方塊的選項，如下所示。

![](mvc-music-store-part-5/_static/image1.png)

當您按一下 [新增] 按鈕時，您會看到 ASP.NET MVC 3 [樣板] 機制會為您執行良好的工作量：

- 它會建立具有本機 Entity Framework 變數的新 StoreManagerController
- 它會將 [StoreManager] 資料夾新增至專案的 [Views] 資料夾
- 它會加入建立的. cshtml、Delete. cshtml、Details、. cshtml 和 Index. cshtml 視圖，強型別到專輯類別

![](mvc-music-store-part-5/_static/image2.png)

新的 StoreManager 控制器類別包含 CRUD （建立、讀取、更新、刪除）控制器動作，其可瞭解如何使用專輯模型類別，並使用我們的 Entity Framework 內容來存取資料庫。

## <a name="modifying-a-scaffolded-view"></a>修改 Scaffold 視圖

請務必記住，雖然這段程式碼是為我們產生的，但它是標準的 ASP.NET MVC 程式碼，就像我們在本教學課程中所撰寫的一樣。 它的目的是要讓您省下花在撰寫重複使用的控制器程式碼，以及手動建立強型別視圖的時間，但這不是您前面所見過的程式碼目錄，您可能會在不得變更錯誤碼. 這是您的程式碼，您應該要加以變更。

因此，讓我們從快速編輯 StoreManager 索引視圖（/Views/StoreManager/Index.cshtml）開始。 此視圖會顯示一個表格，其中列出存放區中的專輯，其中包含編輯/詳細資料/刪除連結，並包含專輯的公用屬性。 我們將移除 [AlbumArtUrl] 欄位，因為它在此顯示中並沒有太大説明。 在 view 程式碼 &lt;table&gt; 區段中，移除 &lt;的&gt;，並 &lt;括住 AlbumArtUrl 參考的 td&gt; 元素，如下列反白顯示的幾行所示：

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample1.cshtml)]

修改過的視圖程式碼將會如下所示：

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample2.cshtml)]

## <a name="a-first-look-at-the-store-manager"></a>第一次查看商店經理

現在執行應用程式，並流覽至/StoreManager/。 這會顯示剛才修改的存放區經理索引，並顯示商店中的專輯清單，其中包含編輯、詳細資料和刪除的連結。

![](mvc-music-store-part-5/_static/image3.png)

按一下 [編輯] 連結會顯示含有專輯欄位的編輯表單，包括內容類型和演出者的下拉式清單。

![](mvc-music-store-part-5/_static/image4.png)

按一下底部的 [返回清單] 連結，然後按一下專輯的 [詳細資料] 連結。 這會顯示個別專輯的詳細資訊。

![](mvc-music-store-part-5/_static/image5.png)

再次按一下 [回到清單] 連結，然後按一下 [刪除] 連結。 這會顯示確認對話方塊，其中會顯示專輯詳細資料，並詢問我們是否確定要將它刪除。

![](mvc-music-store-part-5/_static/image6.png)

按一下底部的 [刪除] 按鈕將會刪除專輯，並返回 [索引] 頁面，其中會顯示已刪除的專輯。

我們不是使用 Store Manager 完成，但我們有工作控制器和程式碼可供 CRUD 作業開始。

## <a name="looking-at-the-store-manager-controller-code"></a>查看 Store Manager 控制器程式碼

存放區管理員控制器包含適當的程式碼數量。 讓我們從上到下逐一查看。 控制器包含一些 MVC 控制器的標準命名空間，以及我們的模型命名空間的參考。 控制器具有 MusicStoreEntities 的私用實例，用於每個控制器動作以進行資料存取。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample3.cs)]

### <a name="store-manager-index-and-details-actions"></a>存放管理員索引和詳細資料動作

[索引] 視圖會抓取專輯清單，包括每個專輯參考的內容類型和演出者資訊，如同我們在使用 Store Browse 方法時所看到的一樣。 索引視圖會遵循連結化物件的參考，讓它可以顯示每個專輯的內容類型名稱和演出者名稱，讓控制器有效率地在原始要求中查詢這項資訊。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample4.cs)]

StoreManager 控制器的詳細資料控制器動作的運作方式與我們先前撰寫的 Store Controller Details 動作完全相同-它會使用 Find （）方法來依識別碼查詢專輯，然後將它傳回給視圖。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample5.cs)]

### <a name="the-create-action-methods"></a>建立動作方法

建立動作方法與我們目前看到的不同，因為它們會處理表單輸入。 使用者第一次造訪/StoreManager/Create/時，將會顯示空白表單。 這個 HTML 網頁會包含一個 &lt;表單&gt; 元素，其中包含下拉式清單和 textbox input 元素，可在其中輸入專輯的詳細資料。

使用者填滿專輯表單值後，可以按 [儲存] 按鈕，將這些變更提交回我們的應用程式，以儲存在資料庫中。 當使用者按下 [儲存] 按鈕時，&lt;表單&gt; 會對/StoreManager/Create/URL 執行 HTTP POST，並提交 &lt;表單&gt; 值做為 HTTP POST 的一部分。

ASP.NET MVC 可讓我們輕鬆地分割這兩個 URL 調用案例的邏輯，方法是讓我們在我們的 StoreManagerController 類別內執行兩個不同的「建立」動作方法–一個用來處理初始 HTTP-GET 流覽至/StoreManager/Create/URL，另一個用來處理已提交變更的 HTTP POST。

### <a name="passing-information-to-a-view-using-viewbag"></a>使用 ViewBag 將資訊傳遞至視圖

我們稍早在本教學課程中使用過此 ViewBag，但尚未討論過。 ViewBag 可讓我們在不使用強型別模型物件的情況下，將資訊傳遞給視圖。 在此情況下，我們的編輯 HTTP-取得控制器動作必須將內容類型和演出者清單傳遞至表單以填入下拉式清單，而最簡單的方法是將它們當做 ViewBag 專案傳回。

ViewBag 是動態物件，這表示您可以輸入 ViewBag 或 ViewBag，而不需要撰寫程式碼來定義這些屬性。 在此情況下，控制器程式碼會使用 ViewBag. GenreId 和 ViewBag ArtistId，讓以表單提交的下拉式值將會是 GenreId 和 ArtistId，也就是他們將設定的專輯屬性。

這些下拉式值會使用 SelectList 物件（專為該目的而建立）傳回給表單。 這會使用類似如下的程式碼來完成：

[!code-csharp[Main](mvc-music-store-part-5/samples/sample6.cs)]

如您在動作方法程式碼中所見，有三個參數是用來建立這個物件：

- 下拉式清單將顯示的專案清單。 請注意，這不只是字串，而是要傳遞內容清單。
- 要傳遞至 SelectList 的下一個參數是選取的值。 SelectList 如何知道如何預先選取清單中的專案。 當我們查看 [編輯] 表單時，這會比較容易瞭解，這非常類似。
- 最後一個參數是要顯示的屬性。 在此情況下，這表示 Genre.Name 屬性就是將向使用者顯示的內容。

記住這一點之後，HTTP GET Create 動作非常簡單-這兩個 SelectLists 會加入至 ViewBag，而且不會有任何模型物件傳遞至表單（因為尚未建立）。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample7.cs)]

### <a name="html-helpers-to-display-the-drop-downs-in-the-create-view"></a>HTML 協助程式，以顯示 [建立] 視圖中的下拉式清單

既然我們已經討論過如何將下拉式值傳遞至視圖，讓我們快速查看一下視圖，以查看這些值的顯示方式。 在 view code （/Views/StoreManager/Create.cshtml）中，您會看到下列呼叫來顯示 [內容類型] 下拉式按鈕。

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample8.cshtml)]

這就是所謂的 HTML Helper，這是一個可執行一般 view 工作的公用程式方法。 HTML helper 非常適合讓我們的視圖程式碼變得簡潔易懂。 DropDownList helper 是由 ASP.NET MVC 提供，但我們稍後會看到，我們可以建立自己的協助程式，以在我們的應用程式中重複使用。

DropDownList 呼叫只需要告訴兩件事，就可以在何處取得要顯示的清單，以及應該預先選取的值（如果有的話）。 第一個參數 GenreId 會告知 DropDownList 在模型或 ViewBag 中尋找名為 GenreId 的值。 第二個參數是用來指出要顯示為下拉式清單中一開始所選取的值。 因為此表單是建立表單，所以沒有預先選取的值和 String。會傳遞空的。

### <a name="handling-the-posted-form-values"></a>處理已張貼的表單值

如先前所討論，每個表單有兩個相關聯的動作方法。 第一個會處理 HTTP GET 要求，並顯示表單。 第二個處理 HTTP POST 要求，其中包含已提交的表單值。 請注意，控制器動作有一個 [HttpPost] 屬性，它會告知 ASP.NET MVC 它應該只回應 HTTP POST 要求。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample9.cs)]

此動作有四個責任：

- 1. 讀取表單值
- 2. 檢查表單值是否通過任何驗證規則
- 3. 如果表單提交有效，請儲存資料並顯示更新的清單
- 4. 如果表單提交無效，請重新顯示含有驗證錯誤的表單

#### <a name="reading-form-values-with-model-binding"></a>使用模型系結讀取表單值

控制器動作會處理表單提交，其中包含 GenreId 和 ArtistId （從下拉式清單）的值，以及 Title、Price 和 AlbumArtUrl 的 textbox 值。 雖然可以直接存取表單值，但更好的方法是使用內建于 ASP.NET MVC 中的模型系結功能。 當控制器動作接受模型類型做為參數時，ASP.NET MVC 會使用表單輸入（以及路由和 querystring 值）嘗試填入該類型的物件。 其執行方式是尋找名稱符合模型物件屬性的值，例如，設定新專輯物件的 GenreId 值時，它會尋找名稱為 GenreId 的輸入。 當您使用 ASP.NET MVC 中的標準方法來建立視圖時，表單一律會使用屬性名稱做為輸入功能變數名稱來呈現，因此此功能變數名稱將會完全相符。

#### <a name="validating-the-model"></a>驗證模型

此模型會使用 ModelState 的簡單呼叫來進行驗證。 我們尚未將任何驗證規則新增至我們的專輯類別-我們將在稍後執行此動作，但現在這項檢查並不會有太多的功能。 重要的是，此 ModelStat 檢查會根據我們放在模型上的驗證規則來調整，因此未來對驗證規則所做的變更不需要對控制器動作程式碼進行任何更新。

#### <a name="saving-the-submitted-values"></a>儲存已提交的值

如果表單提交通過驗證，就可以將值儲存至資料庫。 使用 Entity Framework，只需要將模型加入專輯集合，然後呼叫 SaveChanges。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample10.cs)]

Entity Framework 會產生適當的 SQL 命令來保存值。 儲存資料之後，我們會重新導向回到專輯清單，讓我們可以看到我們的更新。 這是藉由傳回 RedirectToAction，並以我們想要顯示的控制器動作名稱來完成。 在此情況下，這是索引方法。

#### <a name="displaying-invalid-form-submissions-with-validation-errors"></a>顯示驗證錯誤的無效表單提交

在不正確表單輸入案例中，下拉式清單值會加入至 ViewBag （如同在 HTTP GET 案例中），而系結的模型值則會傳回給 view 以供顯示。 驗證錯誤會使用 @Html.ValidationMessageFor HTML Helper 自動顯示。

#### <a name="testing-the-create-form"></a>測試建立表單

若要測試這項作業，請執行應用程式並流覽至/StoreManager/Create/-這會顯示 StoreController Create HTTP GET 方法所傳回的空白表單。

填入一些值，然後按一下 [建立] 按鈕以提交表單。

![](mvc-music-store-part-5/_static/image7.png)

![](mvc-music-store-part-5/_static/image8.png)

### <a name="handling-edits"></a>處理編輯

[編輯動作組] （HTTP-GET 和 HTTP POST）與我們剛才查看的建立動作方法非常類似。 因為編輯案例牽涉到使用現有的專輯，所以 Edit HTTP GET 方法會根據「識別碼」參數載入專輯，並透過路由傳入。 這段程式碼可供 AlbumId 用來抓取專輯，如同我們先前在詳細資料控制器動作中所探討的一樣。 如同 Create/HTTP-GET 方法，下拉式值會透過 ViewBag 傳回。 這可讓我們將專輯當做我們的模型物件傳回給視圖（這是對專輯類別的強型別），同時透過 ViewBag 傳遞其他資料（例如內容類型的清單）。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample11.cs)]

編輯 HTTP POST 動作與建立 HTTP POST 動作非常類似。 唯一的差別在於，它不會將新的專輯新增至資料庫。專輯集合，我們正在使用 db 尋找專輯的目前實例。專案（專輯），並將其狀態設定為 [已修改]。 這會告訴 Entity Framework 我們修改現有的專輯，而不是建立新的專輯。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample12.cs)]

我們可以藉由執行應用程式並流覽至/StoreManger/，然後按一下專輯的 [編輯] 連結，來進行測試。

![](mvc-music-store-part-5/_static/image9.png)

這會顯示編輯 HTTP GET 方法所顯示的編輯表單。 填入一些值，然後按一下 [儲存] 按鈕。

![](mvc-music-store-part-5/_static/image10.png)

這會張貼表單、儲存值，並將我們傳給專輯清單，顯示值已更新。

![](mvc-music-store-part-5/_static/image11.png)

### <a name="handling-deletion"></a>處理刪除

刪除作業會遵循與 [編輯] 和 [建立] 相同的模式，使用一個控制器動作來顯示確認表單，以及另一個控制器動作來處理表單提交。

「HTTP-取得刪除控制器」動作與先前的「存放區管理員詳細資料控制器」動作完全相同。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample13.cs)]

我們使用 [刪除視圖內容] 範本，顯示強型別為專輯類型的表單。

![](mvc-music-store-part-5/_static/image12.png)

[刪除] 範本會顯示模型的所有欄位，但我們可以稍微簡化。 將/Views/StoreManager/Delete.cshtml 中的 view 程式碼變更為下列。

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample14.cshtml)]

這會顯示簡化的刪除確認。

![](mvc-music-store-part-5/_static/image13.png)

按一下 [刪除] 按鈕會導致表單回傳至伺服器，這會執行 DeleteConfirmed 動作。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample15.cs)]

我們的 HTTP POST 刪除控制器動作會採取下列動作：

- 1. 依識別碼載入專輯
- 2. 刪除專輯並儲存變更
- 3. 重新導向至索引，顯示已從清單中移除專輯

若要進行測試，請執行應用程式，並流覽至/StoreManager。 從清單中選取專輯，然後按一下 [刪除] 連結。

![](mvc-music-store-part-5/_static/image14.png)

這會顯示我們的刪除確認畫面。

![](mvc-music-store-part-5/_static/image15.png)

按一下 [刪除] 按鈕會移除專輯，並將我們返回 [Store Manager 索引] 頁面，其中顯示已刪除專輯。

![](mvc-music-store-part-5/_static/image16.png)

### <a name="using-a-custom-html-helper-to-truncate-text"></a>使用自訂 HTML Helper 來截斷文字

我們的商店經理的 [索引] 頁面有一個可能的問題。 我們的專輯 [標題] 和 [演出者名稱] 屬性可以夠長，而可能會擲出我們的資料表格式。 我們將建立自訂的 HTML 協助程式，讓我們能夠輕鬆地截斷我們的視圖中的這些和其他屬性。

![](mvc-music-store-part-5/_static/image17.png)

Razor 的 @helper 語法讓您建立自己的 helper 函式，以便在您的視圖中使用是相當容易的。 開啟 [/Views/StoreManager/Index.cshtml] 視圖，並將下列程式碼直接加在 @model 行之後。

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample16.cshtml)]

此 helper 方法會接受字串和最大長度以允許。 如果提供的文字比指定的長度短，協助專家就會依自己的方式輸出它。 如果較長，則會截斷文字並呈現 "..."餘數。

現在我們可以使用截斷協助程式，確保專輯標題和演出者名稱屬性都少於25個字元。 使用新的截斷協助程式的完整 view 程式碼如下所示。

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample17.cshtml)]

現在當我們流覽/StoreManager/URL 時，專輯和標題會保留在我們的最大長度之下。

![](mvc-music-store-part-5/_static/image18.png)

注意：這會顯示在單一視圖中建立和使用 helper 的簡單案例。 若要深入瞭解如何建立可在整個網站中使用的協助程式，請參閱我的 blog 文章： [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)

> [!div class="step-by-step"]
> [上一頁](mvc-music-store-part-4.md)
> [下一頁](mvc-music-store-part-6.md)
