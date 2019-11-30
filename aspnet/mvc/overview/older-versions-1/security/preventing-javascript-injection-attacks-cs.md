---
uid: mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-cs
title: 防止 JavaScript 插入式攻擊C#（） |Microsoft Docs
author: StephenWalther
description: 避免發生 JavaScript 插入式攻擊和跨網站腳本攻擊。 在本教學課程中，Stephen Walther 將說明您可以如何輕鬆地取消 。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: d0136da6-81a4-4815-b002-baa84744c09e
msc.legacyurl: /mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-cs
msc.type: authoredcontent
ms.openlocfilehash: fb00ee8a7e3d678e824052060eb5d9fd5d4b6a42
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74594890"
---
# <a name="preventing-javascript-injection-attacks-c"></a>防止 JavaScript 插入式攻擊 (C#)

依[Stephen Walther](https://github.com/StephenWalther)

[下載 PDF](https://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_06_CS.pdf)

> 避免發生 JavaScript 插入式攻擊和跨網站腳本攻擊。 在本教學課程中，Stephen Walther 將說明如何透過 HTML 編碼您的內容，輕鬆地對抗這些類型的攻擊。

本教學課程的目的是要說明如何防止 ASP.NET MVC 應用程式中的 JavaScript 插入式攻擊。 本教學課程將討論兩種保護您的網站免于遭受 JavaScript 插入式攻擊的方法。 您將瞭解如何藉由編碼所顯示的資料，來防止 JavaScript 插入式攻擊。 您也將瞭解如何藉由編碼您接受的資料，來防止 JavaScript 插入式攻擊。

## <a name="what-is-a-javascript-injection-attack"></a>什麼是 JavaScript 插入式攻擊？

每當您接受使用者輸入並重新顯示使用者輸入時，您就會開啟您的網站以進行 JavaScript 插入式攻擊。 讓我們來檢查對 JavaScript 插入式攻擊開放的實體應用程式。

假設您已建立客戶意見反應網站（請參閱 [圖 1]）。 客戶可以造訪網站，並輸入您的產品使用經驗的意見反應。 當客戶提交意見反應時，意見反應會顯示在 [意見反應] 頁面上。

[![客戶意見反應網站](preventing-javascript-injection-attacks-cs/_static/image2.png)](preventing-javascript-injection-attacks-cs/_static/image1.png)

**圖 01**：客戶意見反應網站（[按一下以觀看完整大小的影像](preventing-javascript-injection-attacks-cs/_static/image3.png)）

客戶意見反應網站使用 [清單 1] 中的 `controller`。 此 `controller` 包含兩個名為 `Index()` 和 `Create()`的動作。

**清單1– `HomeController.cs`**

[!code-csharp[Main](preventing-javascript-injection-attacks-cs/samples/sample1.cs)]

`Index()` 方法會顯示 `Index` view。 這個方法會藉由從資料庫中抓取意見反應（使用 LINQ to SQL 查詢），將所有先前的客戶意見反應傳遞至 `Index` view。

`Create()` 方法會建立新的意見反應專案，並將其新增至資料庫。 客戶在表單中輸入的訊息會傳遞至 message 參數中的 `Create()` 方法。 隨即建立意見專案，並將訊息指派給意見專案的 [`Message`] 屬性。 意見專案會以 `DataContext.SubmitChanges()` 方法呼叫提交至資料庫。 最後，訪客會重新導向回到 [`Index`] 視圖，其中顯示所有的意見反應。

[`Index`] 視圖包含在 [清單 2] 中。

**清單2– `Index.aspx`**

[!code-aspx[Main](preventing-javascript-injection-attacks-cs/samples/sample2.aspx)]

[`Index`] 視圖有兩個區段。 頂端區段包含實際的客戶意見反應表單。 底部區段包含適用于. 的。每個迴圈會逐一查看所有先前的客戶意見反應專案，並顯示每個意見專案的 EntryDate 和訊息屬性。

客戶意見反應網站是一個簡單的網站。 可惜的是，此網站已開放給 JavaScript 插入式攻擊。

假設您在 [客戶意見反應] 表單中輸入下列文字：

[!code-html[Main](preventing-javascript-injection-attacks-cs/samples/sample3.html)]

此文字代表會顯示警示訊息方塊的 JavaScript 腳本。 有人將此腳本提交到意見反應表單之後，訊息<em>Boo！</em>每當有人造訪客戶意見反應網站時，就會出現（請參閱 [圖 2]）。

[![JavaScript 插入](preventing-javascript-injection-attacks-cs/_static/image5.png)](preventing-javascript-injection-attacks-cs/_static/image4.png)

**圖 02**： JavaScript 插入（[按一下以查看完整大小的影像](preventing-javascript-injection-attacks-cs/_static/image6.png)）

現在，您對 JavaScript 插入式攻擊的初始回應可能會動力。 您可能認為 JavaScript 插入式攻擊只是一*種攻擊的*類型。 您可能會認為沒有人可以藉由認可 JavaScript 插入式攻擊來執行任何真正的麻煩。

可惜的是，駭客可以藉由將 JavaScript 插入網站中，來執行一些真正的惡意專案。 您可以使用 JavaScript 插入式攻擊來執行跨網站腳本（XSS）攻擊。 在跨網站腳本攻擊中，您會竊取機密的使用者資訊，並將資訊傳送至另一個網站。

例如，駭客可以使用 JavaScript 插入式攻擊，竊取其他使用者的瀏覽器 cookie 值。 如果機密資訊（例如密碼、信用卡號碼或社會保險號碼）儲存在瀏覽器 cookie 中，則駭客可以使用 JavaScript 插入式攻擊來竊取這項資訊。 或者，如果使用者在含有 JavaScript 攻擊的頁面中所包含的表單欄位中輸入敏感性資訊，則駭客可以使用插入的 JavaScript 來抓取表單資料，並將它傳送至另一個網站。

*請害怕*。 認真採取 JavaScript 插入式攻擊，並保護您的使用者機密資訊。 在接下來的兩節中，我們將討論您可以用來保護 ASP.NET MVC 應用程式免于 JavaScript 插入式攻擊的兩項技術。

## <a name="approach-1-html-encode-in-the-view"></a>方法 #1：在視圖中進行 HTML 編碼

防止 JavaScript 插入式攻擊的一種簡單方法，就是在您重新顯示視圖中的資料時，以 HTML 編碼網站使用者所輸入的任何資料。 [清單 3] 中已更新的 `Index` 視圖會遵循此方法。

**清單3– `Index.aspx` （HTML 編碼）**

[!code-aspx[Main](preventing-javascript-injection-attacks-cs/samples/sample4.aspx)]

請注意，在以下列程式碼顯示值之前，`feedback.Message` 的值是 HTML 編碼的：

[!code-aspx[Main](preventing-javascript-injection-attacks-cs/samples/sample5.aspx)]

HTML 編碼字串的意義為何？ 當您以 HTML 編碼字串時，`<` 和 `>` 等危險字元會由 HTML 實體參考（例如 `&lt;` 和 `&gt;`）取代。 因此，當字串 `<script>alert("Boo!")</script>` 以 HTML 編碼時，它會轉換成 `&lt;script&gt;alert(&quot;Boo!&quot;)&lt;/script&gt;`。 已編碼的字串在瀏覽器轉譯時，不再以 JavaScript 腳本的形式執行。 相反地，您會在 [圖 3] 中看到無害的頁面。

[![失效的 JavaScript 攻擊](preventing-javascript-injection-attacks-cs/_static/image8.png)](preventing-javascript-injection-attacks-cs/_static/image7.png)

**圖 03**：通過 JavaScript 攻擊（[按一下以觀看完整大小的影像](preventing-javascript-injection-attacks-cs/_static/image9.png)）

請注意，在 [清單 3] 的 [`Index`] 視圖中，只會編碼 `feedback.Message` 的值。 `feedback.EntryDate` 的值未編碼。 您只需要對使用者輸入的資料進行編碼。 因為 EntryDate 的值是在控制器中產生的，所以您不需要對此值進行 HTML 編碼。

## <a name="approach-2-html-encode-in-the-controller"></a>方法 #2：在控制器中進行 HTML 編碼

您可以在將資料提交至資料庫之前，將資料進行 HTML 編碼，而不是 HTML 編碼資料。 第二種方法是在 [清單 4] 的 `controller` 的情況下採取。

**清單4– `HomeController.cs` （HTML 編碼）**

[!code-csharp[Main](preventing-javascript-injection-attacks-cs/samples/sample6.cs)]

請注意，在 `Create()` 動作內將值提交至資料庫之前，Message 的值是 HTML 編碼的。 當訊息在視圖中重新顯示時，訊息會以 HTML 編碼，而且不會執行任何插入訊息中的 JavaScript。

一般而言，您應該優先于本教學課程中討論的第一種方法，而不是第二種方法。 第二種方法的問題是，您的資料庫中會有 HTML 編碼的資料。 換句話說，您的資料庫資料會以有趣的字元變動。

為什麼這不好？ 如果您需要在網頁以外的地方顯示資料庫資料，就會發生問題。 例如，您無法再輕鬆地在 Windows Forms 應用程式中顯示資料。

## <a name="summary"></a>總結

本教學課程的目的是要怪嚇人您有關 JavaScript 插入式攻擊的潛在客戶。 本教學課程討論了兩種保護 ASP.NET MVC 應用程式免于 JavaScript 插入式攻擊的方法：您可以在視圖中對使用者提交的資料進行 HTML 編碼，或您可以在控制器中對使用者提交的資料進行 HTML 編碼。

> [!div class="step-by-step"]
> [上一頁](authenticating-users-with-windows-authentication-cs.md)
> [下一頁](authenticating-users-with-forms-authentication-vb.md)
