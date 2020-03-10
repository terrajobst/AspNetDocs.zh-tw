---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
title: 第4部分：模型和資料存取 |Microsoft Docs
author: jongalloway
description: 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第4部分涵蓋模型和資料存取。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: ab55ca81-ab9b-44a0-8700-dc6da2599335
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
msc.type: authoredcontent
ms.openlocfilehash: 402be340f1ea3344675e7b859cea8c5130cfc8ee
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559672"
---
# <a name="part-4-models-and-data-access"></a>第4部分：模型和資料存取

依[Jon Galloway](https://github.com/jongalloway)

> MVC 音樂存放區是教學課程應用程式，其仲介紹如何使用 ASP.NET MVC 和 Visual Studio 進行 web 程式開發的逐步解說。  
>   
> MVC 音樂存放區是輕量的範例商店執行，可在線上銷售音樂專輯，並實行基本的網站管理、使用者登入和購物車功能。
> 
> 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第4部分涵蓋模型和資料存取。

到目前為止，我們只是從我們的控制器將「虛擬資料」傳遞給我們的「視圖」範本。 現在我們已經準備好連接實際的資料庫了。 在本教學課程中，我們將討論如何使用 SQL Server Compact Edition （通常稱為 SQL CE）做為資料庫引擎。 SQL CE 是一種免費的內嵌檔案型資料庫，不需要任何安裝或設定，這讓您在本機開發上十分方便。

## <a name="database-access-with-entity-framework-code-first"></a>Entity Framework 程式碼的資料庫存取權優先

我們將使用 ASP.NET MVC 3 專案中所包含的 Entity Framework （EF）支援來查詢和更新資料庫。 EF 是彈性的物件關聯式對應（ORM）資料 API，可讓開發人員以物件導向的方式查詢和更新儲存在資料庫中的資料。

Entity Framework 第4版支援稱為「程式碼優先」的開發範例。 Code first 可讓您藉由撰寫簡單的類別（也稱為來自「單純的」 CLR 物件的 POCO）來建立模型物件，甚至可以從類別即時建立資料庫。

### <a name="changes-to-our-model-classes"></a>模型類別的變更

在本教學課程中，我們將利用 Entity Framework 中的資料庫建立功能。 不過在這麼做之前，讓我們先對模型類別進行一些次要變更，以加入稍後將使用的一些專案。

#### <a name="adding-the-artist-model-classes"></a>加入演出者模型類別

我們的專輯會與演出者相關聯，因此我們會新增一個簡單的模型類別來描述演出者。 使用如下所示的程式碼，將新類別新增至名為 Artist.cs 的 [模型] 資料夾。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample1.cs)]

#### <a name="updating-our-model-classes"></a>更新我們的模型類別

更新專輯類別，如下所示。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample2.cs)]

接下來，對內容類型類別進行下列更新。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample3.cs)]

### <a name="adding-the-app_data-folder"></a>將應用程式新增\_Data 資料夾

我們會將應用程式\_資料目錄新增至專案，以保存我們的 SQL Server Express 資料庫檔案。 應用程式\_資料是 ASP.NET 中的特殊目錄，其中已經具有資料庫存取的正確安全性存取權限。 從 [專案] 功能表中，依序選取 [新增 ASP.NET 資料夾] 和 [應用程式\_資料]。

![](mvc-music-store-part-4/_static/image1.png)

### <a name="creating-a-connection-string-in-the-webconfig-file"></a>在 web.config 檔案中建立連接字串

我們會在網站的設定檔中新增幾行，讓 Entity Framework 知道如何連接到我們的資料庫。 按兩下位於專案根目錄中的 web.config 檔案。

![](mvc-music-store-part-4/_static/image2.png)

請前往此檔案的底部，並在最後一行的正上方加入 &lt;connectionStrings&gt; 區段，如下所示。

[!code-xml[Main](mvc-music-store-part-4/samples/sample4.xml)]

### <a name="adding-a-context-class"></a>加入內容類別

以滑鼠右鍵按一下 [模型] 資料夾，然後加入名為 MusicStoreEntities.cs 的新類別。

![](mvc-music-store-part-4/_static/image3.png)

這個類別將代表 Entity Framework 資料庫內容，並會為我們處理我們的建立、讀取、更新和刪除作業。 此類別的程式碼如下所示。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample5.cs)]

這就是-沒有其他設定、特殊介面等等。藉由擴充 DbCoNtext 基類，我們的 MusicStoreEntities 類別能夠為我們處理我們的資料庫作業。 既然我們已連結，現在讓我們在我們的模型類別中加入幾個屬性，以利用資料庫中的一些額外資訊。

### <a name="adding-our-store-catalog-data"></a>新增我們的商店目錄資料

我們將利用 Entity Framework 中的功能，將「種子」資料新增至新建立的資料庫。 這會預先填入我們的商店目錄，其中包含內容清單、演出者和專輯。 MvcMusicStore-Assets .zip 下載-其中包含我們稍早在本教學課程中使用的網站設計檔案-具有具有此種子資料的類別檔案，該檔案位於名為 Code 的資料夾中。

在 [程式碼/模型] 資料夾內，找出 SampleData.cs 檔案，並將它放入專案的 [模型] 資料夾中，如下所示。

![](mvc-music-store-part-4/_static/image4.png)

現在，我們需要新增一行程式碼，告訴 Entity Framework 該 SampleData 類別的相關資訊。 按兩下專案根目錄中的 global.asax 檔案加以開啟，然後將下列一行新增至應用程式\_Start 方法的頂端。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample6.cs)]

到目前為止，我們已完成為專案設定 Entity Framework 所需的工作。

## <a name="querying-the-database"></a>查詢資料庫

現在讓我們更新我們的 StoreController，如此一來，您就可以改為使用「虛擬資料」來呼叫我們的資料庫，以查詢其所有資訊。 首先，我們會在**StoreController**上宣告一個欄位，以保存 MusicStoreEntities 類別的實例，名為 storeDB：

[!code-csharp[Main](mvc-music-store-part-4/samples/sample7.cs)]

### <a name="updating-the-store-index-to-query-the-database"></a>更新存放區索引以查詢資料庫

MusicStoreEntities 類別是由 Entity Framework 維護，並公開資料庫中每個資料表的集合屬性。 讓我們更新我們的 StoreController 索引動作，以取得資料庫中的所有內容。 我們先前是以硬式編碼字串資料的方式來執行這項操作。 現在，我們可以改為使用 Entity Framework 內容 Generes 集合：

[!code-csharp[Main](mvc-music-store-part-4/samples/sample8.cs)]

我們不需要對我們的 View 範本進行任何變更，因為我們仍然會傳回我們先前傳回的相同 StoreIndexViewModel-我們現在只會從資料庫傳回即時資料。

當我們再次執行專案並流覽 "/Store" URL 時，我們現在會在資料庫中看到所有內容清單：

![](mvc-music-store-part-4/_static/image1.jpg)

### <a name="updating-store-browse-and-details-to-use-live-data"></a>更新存放區流覽和詳細資料以使用即時資料

我們使用/Store/Browse？內容類型 = *[部分類型]* 動作方法，依名稱搜尋內容類型。 我們只會預期一個結果，因為在相同的內容類型名稱中不應該有兩個專案，因此我們可以使用。LINQ 中的單一（）延伸模組，可查詢適當的類型物件，如下所示（尚不輸入此項）：

[!code-csharp[Main](mvc-music-store-part-4/samples/sample9.cs)]

單一方法會採用 Lambda 運算式做為參數，這會指定我們想要單一內容類型物件，使其名稱符合我們定義的值。 在上述案例中，我們會載入單一類型物件，其名稱值符合 Disco。

我們將利用 Entity Framework 功能，讓我們在取得內容類型物件時，指出我們想要載入的其他相關實體。 這項功能稱為「查詢結果塑造」，可讓我們減少存取資料庫所需的次數，以取得我們所需的所有資訊。 我們想要預先提取專輯以取得我們所取得的內容類型，因此我們將更新查詢以包含在內容類型中。包含（「專輯」）表示我們也想要相關的專輯。 這會更有效率，因為它會在單一資料庫要求中同時取得內容類型和專輯資料。

有了這方面的說明，以下是我們更新的「流覽控制器」動作的樣子：

[!code-csharp[Main](mvc-music-store-part-4/samples/sample10.cs)]

我們現在可以更新 [Store] 流覽視圖，以顯示每個內容類型中可用的專輯。 開啟 [view] 範本（可在/Views/Store/Browse.cshtml 中找到），然後新增項目符號清單，如下所示。

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample11.cshtml)]

執行我們的應用程式，並流覽至/Store/Browse？內容類型 = 爵士樂會顯示我們現在已從資料庫提取結果，並顯示所選類型中的所有專輯。

![](mvc-music-store-part-4/_static/image2.jpg)

我們會對/Store/Details/[id] URL 進行相同的變更，並將我們的虛擬資料取代成一個資料庫查詢，其會載入識別碼符合參數值的專輯。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample12.cs)]

執行我們的應用程式並流覽至/Store/Details/1，會顯示我們的結果現在已從資料庫提取。

![](mvc-music-store-part-4/_static/image5.png)

現在，我們的商店詳細資料頁面已設定為依專輯識別碼顯示專輯，讓我們更新 [**流覽]** 視圖以連結至詳細資料檢視。 我們會使用 Html.actionlink，與我們在上一節結尾處的「存放區索引」連結和「儲存」流覽方式完全相同。 流覽視圖的完整來源如下所示。

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample13.cshtml)]

我們現在可以從我們的 [商店] 頁面流覽至 [內容類型] 頁面，其中會列出可用的專輯，而按一下專輯後，我們就可以查看該專輯的詳細資料。

![](mvc-music-store-part-4/_static/image6.png)

> [!div class="step-by-step"]
> [上一頁](mvc-music-store-part-3.md)
> [下一頁](mvc-music-store-part-5.md)
