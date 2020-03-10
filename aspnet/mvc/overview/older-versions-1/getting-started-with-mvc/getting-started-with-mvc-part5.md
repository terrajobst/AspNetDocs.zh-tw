---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
title: 從控制器存取模型的資料 |Microsoft Docs
author: shanselman
description: 這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。 建立可從資料庫讀取和寫入的簡單 web 應用程式。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 004703cd-e0e9-4ba7-9974-1b0475c71222
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
msc.type: authoredcontent
ms.openlocfilehash: 207ed880977d794d81efdc1ea458d17a68d501d8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543747"
---
# <a name="accessing-your-models-data-from-a-controller"></a>從控制器存取模型資料

由[Scott Hanselman](https://github.com/shanselman)

> 這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。 您將建立可從資料庫讀取和寫入的簡單 web 應用程式。 請造訪[ASP.NET mvc 學習中心](../../../index.md)，以尋找其他 ASP.NET mvc 教學課程和範例。

在本節中，我們將建立一個新的 Moviescontroller.cs 類別，並撰寫一些程式碼來抓取電影資料，並使用視圖範本將其顯示回瀏覽器。

以滑鼠右鍵按一下 [控制器] 資料夾，並建立新的 Moviescontroller.cs。

[![新增控制器](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)

這會在專案內的 \Controllers 資料夾下方建立新的 "MoviesController.cs" 檔案。 讓我們更新 MovieController，以從我們新填入的資料庫中取出電影清單。

[!code-csharp[Main](getting-started-with-mvc-part5/samples/sample1.cs)]

我們正在執行 LINQ 查詢，因此我們只會取出1984年夏季之後所發行的電影。 我們需要一個 View 範本來轉譯這份電影清單，因此，請在方法中按一下滑鼠右鍵，然後選取 [新增視圖] 加以建立。

在 [新增視圖] 對話方塊中，我們會指出我們將清單&lt;電影&gt; 到我們的視圖範本。 與先前使用 [加入視圖] 對話方塊並選擇建立「空白」範本的時間不同，這次我們會指出我們想要 Visual Studio 為我們自動「scaffold」具有一些預設內容的視圖範本。 我們將在 [View content] 下拉式功能表中選取 [清單] 專案來執行此動作。

請記住，當您建立新的類別時，您必須編譯應用程式，它才會顯示在 [加入視圖] 對話方塊中。

![加入視圖](getting-started-with-mvc-part5/_static/image3.png)

按一下 [新增]，系統就會自動為我們產生顯示電影清單的視圖程式碼。 這是將 &lt;h2&gt; 標題變更為「我的電影清單」的好時機，如同我們先前使用 Hello World view 所做的一樣。

[![電影-Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)

執行您的應用程式，並流覽網址列中的/Movies。 現在，我們已使用控制器內的基本查詢從資料庫中取出資料，並將資料傳回給瞭解電影的視圖。 該視圖接著會旋轉電影清單，並為我們建立資料的資料表。

[![電影清單-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)

我們不會使用此應用程式來執行編輯、詳細資料和刪除功能，因此我們不需要 scaffold 範本為我們建立的預設連結。 開啟/Movies/Index.aspx 檔案，並將其移除。

以下是我們進行這些變更之後，更新後的視圖範本應該看起來的原始程式碼：

[!code-aspx[Main](getting-started-with-mvc-part5/samples/sample2.aspx)]

它會建立我們不需要的連結，因此我們會在此範例中將其刪除。 我們會保留 [建立新的] 連結，如下所示！ 以下是我們的應用程式在移除該資料行時的外觀。

[![電影清單-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)

我們現在有簡單的電影資料清單。 不過，如果我們按一下 [建立新的] 連結，就會收到錯誤，因為它並未連接！ 讓我們來執行建立動作方法，並讓使用者在資料庫中輸入新電影。

> [!div class="step-by-step"]
> [上一頁](getting-started-with-mvc-part4.md)
> [下一頁](getting-started-with-mvc-part6.md)
