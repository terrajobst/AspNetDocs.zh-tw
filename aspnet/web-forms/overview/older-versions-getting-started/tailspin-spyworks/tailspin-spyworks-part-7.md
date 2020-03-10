---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
title: 第7部分：新增功能 |Microsoft Docs
author: JoeStagner
description: 本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。 第7部分新增額外的功能，例如 account revie 。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 50223ee9-11b9-4cf3-bca2-e2f10bf471f3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
msc.type: authoredcontent
ms.openlocfilehash: ffd2b862c727db9572c272b7b21bcc33c822fffa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641992"
---
# <a name="part-7-adding-features"></a>第7部分：新增功能

依[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks 示範為 .NET 平臺建立功能強大、可擴充的應用程式有多麼簡單。 它會說明如何使用 ASP.NET 4 中的絕佳新功能來建立線上商店，包括購物、結帳和管理。
> 
> 本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。 第7部分新增額外的功能，例如帳戶審查、產品評論和「常用專案」，以及「也購買」的使用者控制項。

## <a id="_Toc260221673"></a>新增功能

雖然使用者可以流覽我們的目錄、將專案放在其購物車中，以及完成結帳程式，但我們將會包含一些支援功能來改善我們的網站。

1. 帳戶審查（列出訂單及查看詳細資料）。
2. 將一些內容特定內容新增至 front 頁面。
3. 新增功能，讓使用者能夠查看目錄中的產品。
4. 建立使用者控制項來顯示熱門專案，並將該控制項放在 front 頁面上。
5. 建立「也已購買」使用者控制項，並將它新增至產品詳細資料頁面。
6. 新增連絡人頁面。
7. 新增 [關於] 頁面。
8. 全域錯誤

## <a id="_Toc260221674"></a>帳戶審查

在 [帳戶] 資料夾中，建立名為 OrderList 的兩個 .aspx 頁面，另一個名為 OrderDetails .aspx

OrderList 會利用 GridView 和 EntityDataSource 控制項，就像我們之前的一樣。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample1.aspx)]

EntityDataSource 會根據使用者登入時，在會話變數中設定的 [Orders] 資料表中，選取已篩選的記錄（請參閱 WhereParameter）。

另請注意 GridView HyperlinkField 中的這些參數：

[!code-xml[Main](tailspin-spyworks-part-7/samples/sample2.xml)]

這些會針對每個產品指定 [訂單詳細資料] 視圖的連結，並將 [訂單] 欄位指定為 OrderDetails 的 QueryString 參數。

## <a id="_Toc260221675"></a>OrderDetails .aspx

我們將使用 EntityDataSource 控制項來存取訂單和 FormView，以顯示訂單資料和另一個具有 GridView 的 EntityDataSource，以顯示所有訂單的明細專案。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample3.aspx)]

在程式碼後置檔案（OrderDetails.aspx.cs）中，我們有兩個小部分的維護。

首先，我們必須確定 OrderDetails 一律會取得「訂單」。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample4.cs)]

我們也需要計算並顯示明細專案的訂單總計。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample5.cs)]

## <a id="_Toc260221676"></a>首頁

讓我們將一些靜態內容新增至 default.aspx 頁面。

首先我要建立一個 [Content （內容）] 資料夾，並在其中包含 [Images （首頁）] 資料夾。

在 default.aspx 頁面的底部預留位置中，新增下列標記。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample6.aspx)]

## <a id="_Toc260221677"></a>產品評論

首先，我們會新增一個按鈕，其中包含可供我們用來輸入產品評論的表單連結。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample7.aspx)]

![](tailspin-spyworks-part-7/_static/image1.jpg)

請注意，我們會在查詢字串中傳遞 ProductID

接下來，我們將新增名為 ReviewAdd 的頁面

此頁面會使用 ASP.NET AJAX 控制項工具組。 如果您還沒有這麼做，可以從[DevExpress](http://devexpress.com/act)下載，而且有關于設定工具組以用於此處[https://www.asp.net/learn/ajax-videos/video-76.aspx](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md)之 Visual Studio 的指導方針。

在設計模式中，從 [工具箱] 拖曳控制項和驗證器，並建立如下所示的表單。

![](tailspin-spyworks-part-7/_static/image2.jpg)

標記看起來會像這樣。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample8.aspx)]

現在我們可以輸入評論，讓我們在 [產品] 頁面上顯示這些評論。

將此標記新增至 [ProductDetails] 頁面。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample9.aspx)]

立即執行我們的應用程式，並流覽至產品，其中會顯示產品資訊，包括客戶評論。

![](tailspin-spyworks-part-7/_static/image3.jpg)

## <a id="_Toc260221678"></a>熱門專案控制項（建立使用者控制項）

為了增加網站的銷售額，我們會將幾項功能新增至「暗示銷售」熱門或相關的產品。

這些功能的第一項是產品目錄中更熱門的產品清單。

我們會建立「使用者控制項」，以在應用程式的首頁上顯示最前面的銷售專案。 因為這會是控制項，所以我們可以在任何頁面上使用它，只要在 Visual Studio 的設計工具中，將控制項拖放到想要的任何頁面上即可。

在 Visual Studio 的方案 explorer 中，以滑鼠右鍵按一下方案名稱，然後建立名為 "Controls" 的新目錄。 雖然不需要這麼做，但我們會在「控制項」目錄中建立所有的使用者控制項，以協助保護專案的組織。

以滑鼠右鍵按一下 [控制項] 資料夾，然後選擇 [新增專案]：

![](tailspin-spyworks-part-7/_static/image4.jpg)

為我們的 "PopularItems" 控制項指定名稱。 請注意，使用者控制項的副檔名為 .ascx，而不是 .aspx。

我們的熱門專案使用者控制項將定義如下。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample10.aspx)]

在這裡，我們將使用我們尚未在此應用程式中使用的方法。 我們使用的是中繼器控制項，而不是使用資料來源控制項，我們會將 Repeater 控制項系結至 LINQ to Entities 查詢的結果。

在控制項背後的程式碼中，我們會執行此動作，如下所示。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample11.cs)]

請注意，我們在控制項標記的頂端也會看到這一行重要的程式碼。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample12.aspx)]

由於最受歡迎的專案不會每分鐘變更一次，因此我們可以新增 aching 指示詞來改善應用程式的效能。 這個指示詞只會在控制項的快取輸出過期時，才執行控制項程式碼。 否則，將會使用控制項輸出的快取版本。

我們只需要在 default.aspx 頁面中加入新的控制項即可。

使用拖放功能，將控制項的實例放在預設表單的 [開啟] 資料行中。

![](tailspin-spyworks-part-7/_static/image5.jpg)

現在當我們執行應用程式時，首頁會顯示最受歡迎的專案。

![](tailspin-spyworks-part-7/_static/image6.jpg)

## <a id="_Toc260221679"></a>「也購買」控制項（具有參數的使用者控制項）

我們所建立的第二個使用者控制項，會藉由新增內容的明確性，讓您有更好的銷售。

計算前「也已購買」專案的邏輯並不簡單。

我們的「也已購買」控制項將會針對目前選取的 ProductID 選取 OrderDetails 記錄（先前購買的），並針對每個找到的唯一訂單取得 Orderid。

然後，我們會選取所有訂單中的產品，並加總購買的數量。 我們會依該數量總和排序產品，並顯示前五個專案。

基於此邏輯的複雜度，我們會將此演算法實作為預存程式。

預存程式的 T-sql 如下所示。

[!code-sql[Main](tailspin-spyworks-part-7/samples/sample13.sql)]

請注意，當我們在應用程式中包含此預存程式（SelectPurchasedWithProducts）時，資料庫中會有此預存程式，而當我們所指定的實體資料模型，除了我們所需的資料表和 Views 以外，實體資料模型應該包含此預存程式。

若要從實體資料模型存取預存程式，我們必須匯入函數。

按兩下 [方案瀏覽器] 中的 [實體資料模型]，在設計工具中開啟它並開啟 [模型瀏覽器]，然後在設計工具中按一下滑鼠右鍵，然後選取 [加入函式匯入]。

![](tailspin-spyworks-part-7/_static/image1.png)

這麼做會開啟此對話方塊。

![](tailspin-spyworks-part-7/_static/image2.png)

如下所示填寫欄位，並選取 "SelectPurchasedWithProducts"，並使用程式名稱作為匯入函式的名稱。

按一下 [確定]。

完成這項作業之後，就可以像在模型中的其他專案一樣，對預存程式進行程式設計。

因此，在我們的 "Controls" 資料夾中，建立名為 AlsoPurchased 的新使用者控制項。

這個控制項的標記看起來很熟悉 PopularItems 控制項。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample14.aspx)]

值得注意的差異在於，因為要轉譯的專案會依產品而有所不同，所以不會快取輸出。

ProductId 會是控制項的「屬性」。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample15.cs)]

在控制項的可呈現事件處理常式中，我們 eed 執行三項工作。

1. 請確定已設定 ProductID。
2. 查看是否有任何已使用目前產品購買的產品。
3. 輸出 #2 中判斷的某些專案。

請注意，透過模型呼叫預存程式有多麼簡單。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample16.cs)]

判斷「也已購買」之後，我們可以直接將中繼器系結至查詢所傳回的結果。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample17.cs)]

如果沒有任何「也購買」的專案，我們只會顯示類別目錄中的其他熱門專案。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample18.cs)]

若要查看「也購買」的專案，請開啟 [ProductDetails] 頁面，並從 [方案瀏覽器] 拖曳 AlsoPurchased 控制項，使其出現在標記中的這個位置。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample19.aspx)]

這麼做會在 [ProductDetails] 頁面頂端建立控制項的參考。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample20.aspx)]

因為 AlsoPurchased 使用者控制項需要 ProductId 編號，所以我們會針對頁面的目前資料模型專案使用 Eval 語句，以設定控制項的 ProductID 屬性。

![](tailspin-spyworks-part-7/_static/image3.png)

當我們建立並立即執行並流覽至產品時，我們會看到「也購買」的專案。

![](tailspin-spyworks-part-7/_static/image7.jpg)

> [!div class="step-by-step"]
> [上一頁](tailspin-spyworks-part-6.md)
> [下一頁](tailspin-spyworks-part-8.md)
