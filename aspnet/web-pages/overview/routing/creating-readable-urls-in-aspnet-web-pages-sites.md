---
uid: web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
title: 在 ASP.NET Web Pages （Razor）網站中建立可讀取的 Url |Microsoft Docs
author: Rick-Anderson
description: 本文說明 ASP.NET Web Pages （Razor）網站中的路由，以及如何讓您使用更容易閱讀且更適合 SEO 的 Url。 您將 。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: a8aac1ac-89de-4415-afe0-97a41c6423d2
msc.legacyurl: /web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: 832db8e144cab730f16c78f67c12feb9b7c92c7c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628391"
---
# <a name="creating-readable-urls-in-aspnet-web-pages-razor-sites"></a>在 ASP.NET Web Pages （Razor）網站中建立可讀取的 Url

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本文說明 ASP.NET Web Pages （Razor）網站中的路由，以及如何讓您使用更容易閱讀且更適合 SEO 的 Url。
> 
> 您將學到什麼：
> 
> - ASP.NET 如何使用路由，讓您使用更容易閱讀和可搜尋的 Url。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - ASP.NET Web Pages （Razor）3
>   
> 
> 本教學課程也適用于 ASP.NET Web Pages 2。

## <a name="about-routing"></a>關於路由

網站中頁面的 Url 可能會影響網站運作的程度。 &quot;易記&quot; 的 URL 可讓使用者更輕鬆地使用網站。 它也可以協助網站的搜尋引擎優化（SEO）。 ASP.NET 網站包含自動使用易記 Url 的功能。

ASP.NET 可讓您建立有意義的 Url 來描述使用者動作，而不是只指向伺服器上的檔案。 針對虛構的 blog，請考慮下列 Url：

- `http://www.contoso.com/Blog/blog.cshtml?categories=hardware`
- `http://www.contoso.com//Blog/blog.cshtml?startdate=2009-11-01&enddate=2009-11-30`

比較這些 Url 與下列各項：

- `http://www.contoso.com/Blog/categories/hardware/`
- `http://www.contoso.com/Blog/2009/November`

在第一組中，使用者必須知道使用 [ *blog* ] 頁面來顯示該 blog，然後必須建立查詢字串，以取得正確的類別或日期範圍。 第二組範例較容易理解和建立。

第一個範例的 Url 也會直接指向特定檔案（*blog. cshtml*）。 如果基於某些原因而將 blog 移至伺服器上的另一個資料夾，或者如果重新撰寫的是使用不同的頁面，則連結會錯誤。 第二組 Url 並不會指向特定的頁面，因此即使 blog 的執行或位置變更，Url 仍然有效。

在 ASP.NET Web Pages 中，您可以建立更易懂的 Url，如同上述範例中的一樣，因為 ASP.NET 會使用*路由*。 路由會從可滿足要求的頁面（或頁面）的 URL 建立邏輯對應。 因為對應是邏輯的（非實體、特定的檔案），所以路由在定義網站 Url 的方式上提供了極大的彈性。

## <a name="how-routing-works"></a>路由的運作方式

當 ASP.NET 處理要求時，它會讀取 URL 以決定如何路由傳送。 ASP.NET 會嘗試比對 URL 的個別區段與磁片上的檔案（從左至右）。 如果有相符專案，則 URL 中剩餘的任何內容都會以*路徑資訊*的形式傳遞至頁面。

假設有人使用此 URL 提出要求：

`http://www.contoso.com/a/b/c`

搜尋如下所示：

1. 是否有檔案的路徑和名稱為 */a/b/c.cshtml*？ 若是如此，請執行該頁面，並不傳遞任何資訊。 否則...
2. 是否有檔案的路徑和名稱為 */a/b.cshtml*？ 若是如此，請執行該頁面，並將值 `c` 傳遞給它。 否則 。
3. 是否有檔案的路徑和名稱為 */a.cshtml*？ 若是如此，請執行該頁面，並將值 `b/c` 傳遞給它。

如果搜尋在其指定的資料夾中找不到與*cshtml*檔案完全相符的專案，ASP.NET 會繼續依序尋找這些檔案：

1. */a/b/c/default.cshtml* （沒有路徑資訊）。
2. */a/b/c/index.cshtml* （沒有路徑資訊）。

> [!NOTE]
> 更明確地說，特定頁面的要求（也就是包含 .rc 副檔名*的要求*）的運作方式就如同您所預期。 `http://www.contoso.com/a/b.cshtml` 之類的要求將會執行頁面*b. cshtml* 。

在頁面中，您可以透過頁面的 `UrlData` 屬性（也就是字典）取得路徑資訊。 假設您有一個名為*ViewCustomers*的檔案，而您的網站取得此要求：

`http://mysite.com/myWebSite/ViewCustomers/1000`

如上述規則所述，要求將會移至您的頁面。 在頁面中，您可以使用類似下列的程式碼來取得和顯示路徑資訊（在此案例中，值 &quot;1000&quot;）：

[!code-html[Main](creating-readable-urls-in-aspnet-web-pages-sites/samples/sample1.html)]

> [!NOTE]
> 由於路由不會包含完整的檔案名，因此如果您有相同名稱但副檔名不同的頁面（例如， *mypage.aspx*和*mypage.aspx*），則可能會造成混淆。 為了避免路由的問題，最好確保您的網站中沒有其名稱只會與延伸模組不同的頁面。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他資源

[WebMatrix-SEO 的 url、urldata.base 和路由](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO)。 Mike Brind 的此 blog 專案提供了有關路由在 ASP.NET Web Pages 中的運作方式的其他詳細資料。
