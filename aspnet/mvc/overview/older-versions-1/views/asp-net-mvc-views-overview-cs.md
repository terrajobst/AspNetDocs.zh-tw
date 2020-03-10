---
uid: mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-cs
title: ASP.NET MVC Views 總覽（C#） |Microsoft Docs
author: StephenWalther
description: 什麼是 ASP.NET MVC 視圖，其與 HTML 網頁有何不同？ 在本教學課程中，Stephen Walther 會向您介紹 Views，並示範如何進行 。
ms.author: riande
ms.date: 02/16/2008
ms.assetid: 152ab1e5-aec2-4ea7-b8cc-27a24dd9acb8
msc.legacyurl: /mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-cs
msc.type: authoredcontent
ms.openlocfilehash: b3f44aa9654a2a718381eaf9c856ca3e15ed1e27
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600314"
---
# <a name="aspnet-mvc-views-overview-c"></a>ASP.NET MVC 檢視概觀 (C#)

依[Stephen Walther](https://github.com/StephenWalther)

> 什麼是 ASP.NET MVC 視圖，其與 HTML 網頁有何不同？ 在本教學課程中，Stephen Walther 會向您介紹 Views，並示範如何在視圖中利用視圖資料和 HTML 協助程式。

本教學課程的目的是為您提供 ASP.NET MVC views、view data 和 HTML helper 的簡介。 本教學課程結束時，您應該瞭解如何建立新的視圖、將資料從控制器傳遞至視圖，以及使用 HTML 協助程式來產生視圖中的內容。

## <a name="understanding-views"></a>了解檢視

若為 ASP.NET 或 Active Server Pages，ASP.NET MVC 不會包含直接對應至頁面的任何專案。 在 ASP.NET MVC 應用程式中，磁片上沒有對應至您在瀏覽器網址列中輸入的路徑的頁面。 ASP.NET MVC 應用程式中最接近的頁面，就是所謂的*觀點*。

在 ASP.NET MVC 應用程式中，傳入瀏覽器要求會對應至控制器動作。 控制器動作可能會傳回一個視圖。 不過，控制器動作可能會執行一些其他類型的動作，例如將您重新導向至另一個控制器動作。

[清單 1] 包含名為 HomeController 的簡單控制器。 HomeController 會公開名為 Index （）和 Details （）的兩個控制器動作。

**清單 1-HomeController.cs**

[!code-csharp[Main](asp-net-mvc-views-overview-cs/samples/sample1.cs)]

您可以在瀏覽器網址列中輸入下列 URL，以叫用第一個動作，也就是 Index （）動作：

/Home/Index

您可以藉由在瀏覽器中輸入下列位址，叫用第二個動作，也就是詳細資料（）動作：

/Home/Details

Index （）動作會傳回 view。 您所建立的大部分動作都會傳回 views。 不過，動作可能會傳回其他類型的動作結果。 例如，Details （）動作會傳回將傳入要求重新導向至 Index （）動作的 RedirectToActionResult。

Index （）動作包含下列一行程式碼：

View （）;

這行程式碼會傳回必須位於 web 伺服器上下列路徑的視圖：

\Views\Home\Index.aspx

視圖的路徑是從控制器的名稱和控制器動作的名稱推斷而來。

如果您想要的話，可以明確瞭解此視圖。 下面這行程式碼會傳回名為 Fred 的視圖：

View （Fred）;

執行這行程式碼時，會從下列路徑傳回 view：

\Views\Home\Fred.aspx

> [!NOTE] 
> 
> 如果您打算為 ASP.NET MVC 應用程式建立單元測試，則最好明確瞭解視圖名稱。 如此一來，您就可以建立單元測試，以確認控制器動作是否傳回預期的視圖。

## <a name="adding-content-to-a-view"></a>將內容加入至視圖

「視圖」是一種可包含腳本的標準（X） HTML 檔案。 您可以使用腳本將動態內容新增至視圖。

例如，[清單 2] 中的視圖會顯示目前的日期和時間。

**清單 2-\Views\Home\Index.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample2.aspx)]

請注意，[清單 2] 中的 HTML 頁面主體包含下列腳本：

&lt;% Response。 Write （DateTime. Now）;%&gt;

您可以使用腳本分隔符號 &lt;% 和%&gt; 來標記腳本的開頭和結尾。 此腳本是以C#撰寫。 它會藉由呼叫回應. Write （）方法來顯示目前的日期和時間，以將內容轉譯至瀏覽器。 &lt;% 和%&gt; 的腳本分隔符號可以用來執行一個或多個語句。

因為您呼叫回應，所以請經常寫入（），Microsoft 會提供一個快捷方式來呼叫回應. Write （）方法。 [清單 3] 中的視圖使用分隔符號 &lt;% = 和%&gt; 做為呼叫 Response 的快捷方式。 Write （）。

**清單 3-Views\Home\Index2.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample3.aspx)]

您可以使用任何 .NET 語言，在視圖中產生動態內容。 一般來說，您會使用 Visual Basic .NET 或C#來撰寫您的控制器和 views。

## <a name="using-html-helpers-to-generate-view-content"></a>使用 HTML helper 產生視圖內容

為了讓您更輕鬆地將內容新增至視圖，您可以利用名為*HTML Helper*的東西。 HTML Helper 通常是產生字串的方法。 您可以使用 HTML helper 來產生標準 HTML 元素，例如文字方塊、連結、下拉式清單和清單方塊。

例如，[清單 4] 中的視圖會利用三個 HTML 協助程式，也就是 Html.beginform （）、TextBox （）和 Password （） helper--以產生登入表單（請參閱 [圖 1]）。

**清單 4--\Views\Home\Login.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample4.aspx)]

[![[新增專案] 對話方塊](asp-net-mvc-views-overview-cs/_static/image1.jpg)](asp-net-mvc-views-overview-cs/_static/image1.png)

**圖 01**：標準登入表單（[按一下以查看完整大小的影像](asp-net-mvc-views-overview-cs/_static/image2.png)）

所有 HTML helper 方法都是在 view 的 Html 屬性上呼叫。 例如，您可以藉由呼叫 Html. TextBox （）方法來呈現 TextBox。

請注意，當您同時呼叫 Html. TextBox （）和 .Html （） helper 時，會使用腳本分隔符號 &lt;% = 和%&gt;。 這些協助程式只會傳回字串。 您必須呼叫 Response. Write （），才能將字串轉譯為瀏覽器。

使用 HTML Helper 方法是選擇性的。 藉由減少您需要撰寫的 HTML 和腳本量，讓您的生活更輕鬆。 [清單 5] 中的視圖會在不使用 HTML 協助程式的情況下，呈現與清單4中的視圖完全相同的表單。

**清單 5--\Views\Home\Login.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample5.aspx)]

您也可以選擇建立自己的 HTML 協助程式。 例如，您可以建立 GridView （） helper 方法，自動在 HTML 資料表中顯示一組資料庫記錄。 我們會在**建立自訂 HTML**協助程式教學課程中探索此主題。

## <a name="using-view-data-to-pass-data-to-a-view"></a>使用視圖資料將資料傳遞至視圖

您可以使用 [視圖資料]，將控制器的資料傳遞給視圖。 請將 view 資料視為您透過郵件傳送的套件。 從控制器傳遞到視圖的所有資料都必須使用此封裝來傳送。 例如，[清單 6] 中的控制器會新增訊息來查看資料。

**清單 6-ProductController.cs**

[!code-csharp[Main](asp-net-mvc-views-overview-cs/samples/sample6.cs)]

控制器 ViewData 屬性代表名稱和值配對的集合。 在 [清單 6] 中，Index （）方法會將專案新增至名為 message 的 view 資料集合，其值 Hello World！。 當 Index （）方法傳回 view 時，會自動將視圖資料傳遞給視圖。

[清單 7] 中的視圖會從 view 資料中抓取訊息，並將訊息轉譯至瀏覽器。

**清單 7--\Views\Product\Index.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample7.aspx)]

請注意，在轉譯訊息時，此視圖會利用 Html 的編碼方式（） HTML Helper 方法。 Html. 編碼（） HTML Helper 會將特殊字元（例如 &lt; 和 &gt;）編碼成可在網頁中顯示的安全字元。 每當您呈現使用者提交至網站的內容時，您應該將內容編碼以防止 JavaScript 插入式攻擊。

（因為我們會在 ProductController 中自行建立訊息，所以我們不需要對訊息進行編碼。 不過，在視圖中顯示從 view 資料抓取的內容時，一律會呼叫 Html. 編碼（）方法是很好的習慣。）

在 [清單 7] 中，我們利用了視圖資料，將簡單的字串訊息從控制器傳遞至視圖。 您也可以使用 [視圖資料]，將其他類型的資料（例如資料庫記錄的集合）從控制器傳遞至視圖。 例如，如果您想要在視圖中顯示 Products 資料庫資料表的內容，則您會將資料庫記錄的集合傳遞至 view data。

您也可以選擇將強型別視圖資料從控制器傳遞到 view。 我們會在瞭解強型別**視圖資料和 Views**教學課程中探索此主題。

## <a name="summary"></a>總結

本教學課程提供 ASP.NET MVC 視圖、視圖資料和 HTML 協助程式的簡介。 在第一節中，您已瞭解如何將新的視圖加入至您的專案。 您已瞭解，您必須將 view 新增至正確的資料夾，才能從特定的控制器呼叫它。 接下來，我們討論過 HTML 協助程式的主題。 您已瞭解 HTML 協助程式如何讓您輕鬆地產生標準 HTML 內容。 最後，您已瞭解如何利用視圖資料，將控制器中的資料傳遞給視圖。

> [!div class="step-by-step"]
> [下一個](creating-custom-html-helpers-cs.md)
