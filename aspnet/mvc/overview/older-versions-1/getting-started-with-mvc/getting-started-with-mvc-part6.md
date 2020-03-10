---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
title: 新增 Create 方法和 Create View |Microsoft Docs
author: shanselman
description: 這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。 建立可從資料庫讀取和寫入的簡單 web 應用程式。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: a3a90963-0286-4fa0-9b3d-c230cc18b0a3
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
msc.type: authoredcontent
ms.openlocfilehash: 05a281720f76b107fe8d902ef60d5d2e72af3ef5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543656"
---
# <a name="adding-a-create-method-and-create-view"></a>新增 Create 方法和 Create 檢視

由[Scott Hanselman](https://github.com/shanselman)

> 這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。 您將建立可從資料庫讀取和寫入的簡單 web 應用程式。 請造訪[ASP.NET mvc 學習中心](../../../index.md)，以尋找其他 ASP.NET mvc 教學課程和範例。

在本節中，我們將會執行必要的支援，讓使用者能夠在資料庫中建立新電影。 我們會藉由執行/Movies/Create URL 動作來完成這項工作。

/Movies/Create URL 的執行過程分為兩個步驟。 當使用者第一次造訪/Movies/Create URL 時，我們想要顯示 HTML 表單，他們可以填寫以輸入新電影。 然後，當使用者提交表單並將資料張貼回伺服器時，我們會想要抓取張貼的內容，並將它儲存到資料庫中。

我們會在 Moviescontroller.cs 類別內的兩個 Create （）方法內，執行這兩個步驟。 其中一種方法會顯示 &lt;表單&gt;，使用者應在此填寫以建立新的電影。 第二種方法會在使用者將 &lt;表單&gt; 回伺服器時，處理張貼的資料處理，並在資料庫中儲存新的電影。

以下是我們要新增至 Moviescontroller.cs 類別的程式碼，以執行此動作：

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample1.cs)]

上述程式碼包含我們在控制器內所需的所有程式碼。

現在，讓我們來執行建立視圖範本，用來向使用者顯示表單。 我們要在第一個 Create 方法中按一下滑鼠右鍵，然後選取 [新增視圖] 來建立電影表單的視圖範本。

我們會選擇將「電影」做為 view 資料類別來傳遞，並指出我們想要「scaffold」「建立」範本。

[![加入視圖](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)

按一下 [新增] 按鈕之後，就會為您建立 \Movies\Create.aspx View 範本。 因為我們已從 [查看內容] 下拉式清單中選取 [建立]，所以 [加入視圖] 對話方塊會自動為我們「scaffold」一些預設內容。 此樣板建立了一個 HTML &lt;表單&gt;、一個位置用於驗證錯誤訊息，而且由於架構會知道電影，因此它會為類別的每個屬性建立標籤和欄位。

[!code-aspx[Main](getting-started-with-mvc-part6/samples/sample2.aspx)]

由於我們的資料庫會自動為電影提供識別碼，因此讓我們移除參考模型的欄位。來自我們建立視圖的識別碼。 &lt;圖例&gt;欄位之後，請移除7行，&lt;/legend&gt; 顯示我們不想要的 ID 欄位。

現在讓我們建立新的電影，並將它加入至資料庫。 我們將再次執行應用程式並流覽 "/Movies" URL，然後按一下 [建立] 連結以新增電影。

[![建立-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)

當我們按一下 [建立] 按鈕時，我們會將此表單上的資料張貼到我們剛才建立的/Movies/Create 方法中（透過 HTTP POST）。 就像系統會自動從 URL 取得 "Numtimes is" 和 "name" 參數，並將它們對應至先前方法上的參數，系統會自動從文章中取出表單欄位，並將其對應至物件。 在此情況下，HTML 欄位中的值（例如 "ReleaseDate" 和 "Title"）會自動放入電影新實例的正確屬性中。

讓我們再次查看 Moviescontroller.cs 的第二個 Create 方法。 請注意，它會採用「電影」物件做為引數：

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample3.cs)]

此 Movie 物件接著會傳遞至建立動作方法的 [HttpPost] 版本，並將它儲存在資料庫中，然後將使用者重新導向回到 Index （）動作方法，這會在電影清單中顯示儲存的結果：

[![電影清單-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)

不過，我們不會檢查電影是否正確，而且資料庫不允許我們儲存沒有標題的電影。 如果我們可以告訴使用者，在資料庫擲回錯誤之前，會有很大的好處。 我們接下來會在應用程式中新增驗證支援。

> [!div class="step-by-step"]
> [上一頁](getting-started-with-mvc-part5.md)
> [下一頁](getting-started-with-mvc-part7.md)
