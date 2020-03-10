---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
title: 第10部分：流覽和網站設計的最後更新，結論 |Microsoft Docs
author: jongalloway
description: 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第10部分涵蓋了最後的流覽和更新 。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 0c6e4c2f-fcdb-4978-9656-1990c6f15727
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
msc.type: authoredcontent
ms.openlocfilehash: f701d1fbabc3e1a97c3750d00e96bf8dba1105cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539365"
---
# <a name="part-10-final-updates-to-navigation-and-site-design-conclusion"></a>第10部分：流覽和網站設計的最後更新，結論

依[Jon Galloway](https://github.com/jongalloway)

> MVC 音樂存放區是教學課程應用程式，其仲介紹如何使用 ASP.NET MVC 和 Visual Studio 進行 web 程式開發的逐步解說。  
>   
> MVC 音樂存放區是輕量的範例商店執行，可在線上銷售音樂專輯，並實行基本的網站管理、使用者登入和購物車功能。  
>   
> 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第10部分涵蓋流覽和網站設計的最後更新，結論。

我們已完成網站的所有主要功能，但仍有一些功能可新增至網站導覽、首頁和存放區流覽頁面。

## <a name="creating-the-shopping-cart-summary-partial-view"></a>建立購物車摘要部分視圖

我們想要在整個網站上公開使用者購物車中的專案數。

![](mvc-music-store-part-10/_static/image1.png)

我們可以藉由建立已新增至我們網站的部分視圖，輕鬆地執行這項工作。

如先前所示，ShoppingCart 控制器包含會傳回部分視圖的 CartSummary 動作方法：

[!code-csharp[Main](mvc-music-store-part-10/samples/sample1.cs)]

若要建立 CartSummary 部分視圖，請在 Views/ShoppingCart 資料夾上按一下滑鼠右鍵，然後選取 [加入視圖]。 為 view CartSummary 命名，並核取 [建立部分視圖] 核取方塊，如下所示。

![](mvc-music-store-part-10/_static/image2.png)

CartSummary 部分視圖其實很簡單，只是 ShoppingCart 索引視圖的連結，它會顯示購物車中的專案數。 CartSummary 的完整程式碼如下所示：

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample2.cshtml)]

我們可以使用 RenderAction 方法，在網站的任何頁面中包含部分視圖，包括網站主機。 RenderAction 需要我們指定動作名稱（"CartSummary"）和控制器名稱（"ShoppingCart"），如下所示。

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample3.cshtml)]

在將此內容新增至網站配置之前，我們也會建立 [內容類型] 功能表，讓我們可以將所有網站更新一次。

## <a name="creating-the-genre-menu-partial-view"></a>建立 [內容類型] 功能表部分視圖

我們可以藉由新增 [內容類型] 功能表（其中列出我們的存放區中所有可用的內容類型），讓使用者更輕鬆地流覽 store。

![](mvc-music-store-part-10/_static/image3.png)

我們會遵循相同的步驟，也會建立 GenreMenu 部分視圖，然後我們可以將它們同時新增至網站主機。 首先，將下列 GenreMenu 控制器動作新增至 StoreController：

[!code-csharp[Main](mvc-music-store-part-10/samples/sample4.cs)]

此動作會傳回內容清單，這些內容會由部分視圖顯示，我們將在下一步建立。

*注意：我們已將 [ChildActionOnly] 屬性新增至此控制器動作，這表示我們只想要從部分視圖使用此動作。這個屬性會藉由流覽至/Store/GenreMenu. 來防止執行控制器動作部分視圖並不需要這樣做，但這是很好的作法，因為我們想要確定我們的控制器動作會如我們預期的方式使用。我們也會傳回 PartialView 而不是 View，這讓視圖引擎知道它不應該使用此視圖的版面配置，因為它包含在其他視圖中。*

以滑鼠右鍵按一下 [GenreMenu 控制器] 動作，並建立名為 GenreMenu 的部分視圖，這是使用內容類型 view 資料類別的強型別，如下所示。

![](mvc-music-store-part-10/_static/image4.png)

更新 GenreMenu 部分視圖的視圖程式碼，以使用未排序的清單來顯示專案，如下所示。

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample5.cshtml)]

## <a name="updating-site-layout-to-display-our-partial-views"></a>正在更新網站版面配置以顯示我們的部分視圖

我們可以藉由呼叫 RenderAction （），將我們的部分觀點新增至網站配置（/Views/Shared/\_Layout）。 我們會在中新增這兩個專案，以及用來顯示它們的一些額外標記，如下所示：

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample6.cshtml)]

現在當我們執行應用程式時，我們會在左側導覽區域中看到內容類型，並在頂端看到購物車摘要。

## <a name="update-to-the-store-browse-page"></a>更新存放區流覽頁面

[存放區流覽] 頁面可正常運作，但外觀不佳。 我們可以藉由更新視圖程式碼（在/Views/Store/Browse.cshtml 中找到）來更新頁面，以更佳的版面配置顯示專輯，如下所示：

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample7.cshtml)]

我們使用的是 Url，而不是 Html.actionlink，讓我們可以將特殊的格式套用至連結以包含專輯作品。

*注意：我們會顯示這些專輯的一般專輯封面。這項資訊會儲存在資料庫中，而且可透過存放區管理員來編輯。歡迎您加入自己的作品。*

現在當我們流覽至內容類型時，我們會在方格中看到以專輯圖案顯示的專輯。

![](mvc-music-store-part-10/_static/image5.png)

## <a name="updating-the-home-page-to-show-top-selling-albums"></a>更新首頁以顯示熱門銷售專輯

我們想要在首頁上為我們的頂尖銷售專輯提供功能，以增加銷售。 我們會對我們的 HomeController 進行一些更新，以處理這種情況，並同時新增一些其他圖形。

首先，我們會將導覽屬性新增至我們的專輯類別，讓 EntityFramework 知道它們是相關聯的。 **專輯**類別的最後幾行現在看起來應該像這樣：

[!code-csharp[Main](mvc-music-store-part-10/samples/sample8.cs)]

*注意：這將需要加入 using 語句來帶入 System.web 命名空間。*

首先，我們會使用語句來新增 storeDB 欄位和 MvcMusicStore，如同在我們的其他控制器中一樣。 接下來，我們會將下列方法新增至 HomeController，以查詢我們的資料庫，根據 OrderDetails 尋找最熱門的銷售專輯。

[!code-csharp[Main](mvc-music-store-part-10/samples/sample9.cs)]

這是私用方法，因為我們不想讓它當做控制器動作來使用。 為了簡單起見，我們在 HomeController 中包含它，但建議您視需要將商務邏輯移至不同的服務類別。

備妥之後，我們可以更新 [索引控制器] 動作來查詢前5名銷售專輯，並將其傳回給視圖。

[!code-csharp[Main](mvc-music-store-part-10/samples/sample10.cs)]

已更新之 HomeController 的完整程式碼如下所示。

[!code-csharp[Main](mvc-music-store-part-10/samples/sample11.cs)]

最後，我們需要更新 [主目錄] 視圖，使其可以藉由更新模型類型並將 [專輯清單] 新增至底部來顯示專輯清單。 我們也會利用這個機會，將標題和升級區段新增至頁面。

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample12.cshtml)]

現在當我們執行應用程式時，我們會看到我們已更新的首頁，其中包含最高的銷售專輯和我們的促銷訊息。

![](mvc-music-store-part-10/_static/image1.jpg)

## <a name="conclusion"></a>結論

我們已瞭解 ASP.NET MVC 可讓您輕鬆地建立具有資料庫存取權、成員資格、AJAX 等的精密網站。 非常快速。 希望本教學課程提供您開始建立自己的 ASP.NET MVC 應用程式所需的工具！

> [!div class="step-by-step"]
> [上一篇](mvc-music-store-part-9.md)
