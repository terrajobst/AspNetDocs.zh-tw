---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
title: 將驗證加入至模型 |Microsoft Docs
author: shanselman
description: 這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。 建立可從資料庫讀取和寫入的簡單 web 應用程式。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: aa7b3e8e-e23d-49f1-b160-f99a7f2982bd
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
msc.type: authoredcontent
ms.openlocfilehash: 9403be574324c34edf93bef1e0e4fd7ba68a3a9d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543642"
---
# <a name="adding-validation-to-the-model"></a>將驗證新增至模型

由[Scott Hanselman](https://github.com/shanselman)

> 這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。 您將建立可從資料庫讀取和寫入的簡單 web 應用程式。 請造訪[ASP.NET mvc 學習中心](../../../index.md)，以尋找其他 ASP.NET mvc 教學課程和範例。

在本節中，我們將會執行在應用程式內啟用輸入驗證所需的支援。 我們會確保資料庫內容一律是正確的，並在使用者嘗試輸入不正確電影資料時，為他們提供有用的錯誤訊息。 首先，我們會將少量驗證邏輯新增至 Movie 類別。

以滑鼠右鍵按一下 [模型] 資料夾，然後選取 [新增類別]。 將您的類別命名為 Movie。

當我們稍早建立電影實體模型時，IDE 會建立 Movie 類別。 事實上，Movie 類別的一部分可以放在一個檔案中，而另一個檔案則部分。 這稱為部分類別。 我們要從另一個檔案延伸 Movie 類別。

我們將建立一個指向 "好友 class" 的部分 movie 類別，其中包含一些屬性，可將驗證提示提供給系統。 我們會視需要標示 [標題] 和 [價格]，並堅持該價格在特定範圍內。 以滑鼠右鍵按一下 [模型] 資料夾，然後選取 [新增類別]。 將您的類別命名為 Movie，然後按一下 [確定] 按鈕。 我們的部分 Movie 類別看起來像這樣。

[!code-csharp[Main](getting-started-with-mvc-part7/samples/sample1.cs)]

重新執行您的應用程式，並嘗試輸入價格超過100的電影。 提交表單之後，您會收到錯誤。 此錯誤會在伺服器端攔截，並在表單公佈之後發生。 請注意，ASP.NET MVC 的內建 HTML 協助程式如何聰明地顯示錯誤訊息，並在 textbox 元素內維護我們的值：

[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)

這項功能很好用，但是如果我們可以立即在用戶端上告知使用者，就很好用。

讓我們啟用一些使用 JavaScript 的用戶端驗證。

## <a name="adding-client-side-validation"></a>加入用戶端驗證

由於電影類別已經有一些驗證屬性，因此我們只需要將一些 JavaScript 檔案新增至 [建立 .aspx 視圖] 範本，然後新增一行程式碼，就可以進行用戶端驗證。

從 VWD 中，移至 [Views/Movie] 資料夾，然後開啟 [建立 .aspx]。

開啟 方案總管中的 腳本 資料夾，然後將下列三個腳本拖曳至 &lt;標頭&gt; 標記內。

- Microsoftajax.debug.js .js
- Microsoftmvcvalidation.js .js

您想要這些腳本檔案以這種順序出現。

[!code-html[Main](getting-started-with-mvc-part7/samples/sample2.html)]

此外，在 Html.beginform 的上方新增此一行：

[!code-aspx[Main](getting-started-with-mvc-part7/samples/sample3.aspx)]

以下是 IDE 中顯示的程式碼。

[![電影-Microsoft Visual Web Developer 2010 Express （10）](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)

執行您的應用程式並再次流覽/Movies/Create，然後按一下 [建立] 而不輸入任何資料。 錯誤訊息會立即顯示，而不會有與將資料一起傳送回伺服器相關聯的 page flash。 這是因為 ASP.NET MVC 現在會驗證用戶端（使用 JavaScript）和伺服器上的輸入。

[![建立-Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)

這看起來不錯！ 現在讓我們在資料庫中加入一個額外的資料行。

> [!div class="step-by-step"]
> [上一頁](getting-started-with-mvc-part6.md)
> [下一頁](getting-started-with-mvc-part8.md)
