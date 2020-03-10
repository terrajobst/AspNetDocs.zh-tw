---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
title: 第4部分：列出產品 |Microsoft Docs
author: JoeStagner
description: 本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。 第4部分涵蓋以 GridView contr 列出產品 。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 4fab47d5-a6ec-4fdc-91f0-651a093a24b9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
msc.type: authoredcontent
ms.openlocfilehash: 7af1b8afa2ecc8df9846f2edd2091b26b93a811c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78566980"
---
# <a name="part-4-listing-products"></a>第4部分：列出產品

依[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks 示範為 .NET 平臺建立功能強大、可擴充的應用程式有多麼簡單。 它會說明如何使用 ASP.NET 4 中的絕佳新功能來建立線上商店，包括購物、結帳和管理。
> 
> 本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。 第4部分涵蓋了使用 GridView 控制項列出產品的內容。

## <a id="_Toc260221670"></a>使用 GridView 控制項列出產品

讓我們先在解決方案上按一下滑鼠右鍵，然後選取 [新增] 和 [新專案]，開始執行 ProductsList .aspx 頁面。

![](tailspin-spyworks-part-4/_static/image1.jpg)

選擇 [使用主版頁面的 Web 表單]，然後輸入 ProductsList 的頁面名稱。

按一下 [新增]。

![](tailspin-spyworks-part-4/_static/image2.jpg)

接下來，選擇我們放置 [網站] 頁面的 [樣式] 資料夾，然後從 [資料夾內容] 視窗中選取它。

![](tailspin-spyworks-part-4/_static/image3.jpg)

按一下 [確定] 以建立頁面。

我們的資料庫會填入產品資料，如下所示。

![](tailspin-spyworks-part-4/_static/image4.jpg)

建立頁面之後，我們會再次使用實體資料來源來存取該產品資料，但在此情況下，我們需要選取產品實體，而且我們需要限制只傳回所選類別的專案。

為了達到此目的，我們會告訴 EntityDataSource 自動產生 WHERE 子句，而我們將指定 WhereParameter。

您會回想一下，當我們在 [產品類別目錄] 功能表中建立功能表項目時，我們會將類別目錄新增至每個連結的 QueryString，以動態建立連結。 我們會告訴實體資料來源從該 QueryString 參數衍生 WHERE 參數。

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample1.aspx)]

接下來，我們將設定 ListView 控制項以顯示產品清單。 為了建立最佳的購物體驗，我們會將數個精簡的功能壓縮成 ListVew 中顯示的每個個別產品。

- 產品名稱將是產品詳細資料檢視的連結。
- 將會顯示產品的價格。
- 將會顯示產品的影像，而我們會在應用程式中以動態方式從 [目錄映射] 目錄選取影像。
- 我們會包含一個連結，以立即將特定產品新增至購物車。

以下是 ListView 控制項實例的標記。

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample2.aspx)]

我們會以動態方式為每個顯示的產品建立數個連結。

此外，在測試自己的新頁面之前，我們必須先建立產品目錄映射的目錄結構，如下所示。

![](tailspin-spyworks-part-4/_static/image1.png)

當我們的產品映射可供存取之後，我們就可以測試產品清單頁面。

![](tailspin-spyworks-part-4/_static/image5.jpg)

從網站的 [首頁] 中，按一下其中一個 [類別目錄清單] 連結。

![](tailspin-spyworks-part-4/_static/image6.jpg)

現在我們需要執行 ProductDetails .aspx 頁面和 AddToCart 功能。

使用 [檔案-&gt;新增]，依照先前的方式使用網站主版頁面建立 ProductDetails 的頁面名稱。

我們會再次使用 EntityDataSource 控制項來存取資料庫中的特定產品記錄，我們將使用 ASP.NET FormView 控制項來顯示產品資料，如下所示。

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample3.aspx)]

如果格式化看起來有點有趣，別擔心。 上述標記會針對我們稍後將會執行的幾項功能，將空間留在顯示版面配置中。

購物車會代表我們的應用程式中更複雜的邏輯。 若要開始，請使用 [檔案-&gt;新增] 來建立名為 MyShoppingCart 的頁面。

請注意，我們不會選擇名稱 ShoppingCart。

我們的資料庫包含名為 "ShoppingCart" 的資料表。 當我們產生實體資料模型類別是針對資料庫中的每個資料表所建立。 因此，實體資料模型產生一個名為 "ShoppingCart" 的實體類別。 我們可以編輯模型，讓我們可以將該名稱用於我們的購物車實施，或針對我們的需求進行擴充，但我們將改為選擇可避免衝突的名稱。

另外值得一提的是，我們將建立簡單的購物車，並使用購物車顯示來內嵌購物車邏輯。 我們也可以選擇在完全獨立的商務層中執行我們的購物車。

> [!div class="step-by-step"]
> [上一頁](tailspin-spyworks-part-3.md)
> [下一頁](tailspin-spyworks-part-5.md)
