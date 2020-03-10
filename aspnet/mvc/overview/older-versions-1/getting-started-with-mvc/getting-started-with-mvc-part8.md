---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
title: 將資料行加入至模型 |Microsoft Docs
author: shanselman
description: 這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。 建立可從資料庫讀取和寫入的簡單 web 應用程式。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 7ae696b9-348f-4993-8ebb-a838acbe0c28
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
msc.type: authoredcontent
ms.openlocfilehash: 1cf092c3db3959d6f47006f1be2ba82833c5dc06
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543579"
---
# <a name="adding-a-column-to-the-model"></a>將資料行新增至模型

由[Scott Hanselman](https://github.com/shanselman)

> 這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。 您將建立可從資料庫讀取和寫入的簡單 web 應用程式。 請造訪[ASP.NET mvc 學習中心](../../../index.md)，以尋找其他 ASP.NET mvc 教學課程和範例。

在本節中，我們將逐步解說如何對資料庫架構進行變更，並處理應用程式內的變更。

讓我們在電影資料表中新增「評等」資料行。 回到 IDE，然後按一下 [資料庫總管]。 以滑鼠右鍵按一下電影資料表，然後選取 [開啟資料表定義]。

新增「評等」資料行，如下所示。 因為我們目前沒有任何評等，所以資料行可以允許 null。 按一下 [儲存]。

[![編輯電影資料表](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)

接下來，返回方案總管並開啟 [電影 .edmx] 檔案（位於 \Models 資料夾）。 以滑鼠右鍵按一下設計介面（白色區域），然後選取 [從資料庫更新模型]。

[![電影-Microsoft Visual Web Developer 2010 Express （11）](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)

這會啟動「更新嚮導」。 按一下其中的 [重新整理] 索引標籤，然後按一下 [完成]。 我們的電影模型類別會以新的資料行更新。

![更新嚮導（2）](getting-started-with-mvc-part8/_static/image5.png)

按一下 [完成] 之後，您就可以看到新的評等資料行已新增至模型中的 Movie 實體。

[![Movie 實體](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)

我們已在資料庫模型中新增資料行，但 Views 並不知道它的相關資訊。

## <a name="update-views-with-model-changes"></a>更新具有模型變更的視圖

有幾種方式可以更新我們的視圖範本，以反映新的評等資料行。 因為我們透過 [加入視圖] 對話方塊產生這些視圖，所以我們可以刪除它們，然後重新建立它們。 不過，使用者通常已經從初始 scaffold 產生修改其 View 範本，而且想要手動新增或刪除欄位，就如同我們在建立時的 [識別碼] 欄位一樣。

開啟 [\Views\Movies\Index.aspx] 範本，然後將 &lt;的&gt;評等&lt;/th&gt; 新增至電影資料表的標題。 我在內容類型後面加入了。 然後，在相同的資料行位置，但向下縮小，以輸出新的評等。

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample1.aspx)]

我們最後的 Index .aspx 範本看起來會像這樣：

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample2.aspx)]

讓我們開啟 \Views\Movies\Create.aspx 範本，並為新的評等屬性新增標籤和文字方塊：

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample3.aspx)]

最後的 [建立 .aspx] 範本看起來像這樣，然後讓我們將瀏覽器的標題和次要 &lt;h2&gt; 標題變更為「建立電影」，而不是在這裡！

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample4.aspx)]

執行您的應用程式，現在您已將資料庫中的新欄位新增至 [建立] 頁面。 新增電影-這次有評等，然後按一下 [建立]。

[![建立電影-Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)

按一下 [建立] 之後，系統會將您傳送至 [索引] 頁面，其中會以資料庫中的新 [評等] 欄列出新電影

[![電影清單-Windows Internet Explorer （12）](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)

這個基本教學課程讓您開始建立控制器、將它們與 Views 產生關聯，以及傳遞硬式編碼的資料。 然後我們建立並設計資料庫，並在其中放入一些資料。 我們已從資料庫中取出資料，並將它顯示在 HTML 資料表中。 然後，我們加入了建立表單，讓使用者可以從 Web 應用程式中將資料加入資料庫本身。 我們已新增驗證，然後進行驗證，並在用戶端上使用 JavaScript。 最後，我們將資料庫變更為包含新的資料行，然後更新兩個頁面，以建立及顯示這項新資料。

我現在建議您移至我們的中繼層級教學課程「[MVC 音樂存放區](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)」，以及[https://asp.net/mvc](https://asp.net/mvc)的許多影片和資源，以深入瞭解 ASP.NET MVC！

敬祝您使用愉快！

- Scott Hanselman-在 Twitter 上[http://hanselman.com](http://hanselman.com)和[@shanselman](http://twitter.com/shanselman) 。

> [!div class="step-by-step"]
> [上一篇](getting-started-with-mvc-part7.md)
