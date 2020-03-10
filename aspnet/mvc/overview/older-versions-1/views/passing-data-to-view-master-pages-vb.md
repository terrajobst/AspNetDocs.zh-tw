---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
title: 將資料傳遞給 View 主版頁面（VB） |Microsoft Docs
author: microsoft
description: 本教學課程的目的是要說明如何將資料從控制器傳遞至視圖主版頁面。 我們會檢查兩個將資料傳送到 view m 的策略 。
ms.author: riande
ms.date: 10/16/2008
ms.assetid: 37a1ebae-8773-408f-8645-d21da7ff9ae1
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 9f768f47557adedc43cebfa2c092014bba5842de
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600104"
---
# <a name="passing-data-to-view-master-pages-vb"></a>將資料傳遞至檢視主版頁面 (VB)

由[Microsoft](https://github.com/microsoft)

[下載 PDF](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_VB.pdf)

> 本教學課程的目的是要說明如何將資料從控制器傳遞至視圖主版頁面。 我們會檢查兩個將資料傳送至視圖主版頁面的策略。 首先，我們會討論一個簡單的解決方案，會導致應用程式變得很難維護。 接下來，我們會檢查更好的解決方案，需要更多的初始工作，但會產生更容易維護的應用程式。

## <a name="passing-data-to-view-master-pages"></a>傳遞資料以觀看主版頁面

本教學課程的目的是要說明如何將資料從控制器傳遞至視圖主版頁面。 我們會檢查兩個將資料傳送至視圖主版頁面的策略。 首先，我們會討論一個簡單的解決方案，會導致應用程式變得很難維護。 接下來，我們會檢查更好的解決方案，需要更多的初始工作，但會產生更容易維護的應用程式。

### <a name="the-problem"></a>問題

假設您正在建立電影資料庫應用程式，而且想要在應用程式的每一頁上顯示電影類別清單（請參閱 [圖 1]）。 另外，想像一下電影類別目錄的清單是儲存在資料庫資料表中。 在這種情況下，從資料庫中取出類別目錄，並在視圖主版頁面中轉譯電影類別目錄是有意義的。

[![在視圖主版頁面中顯示電影類別](passing-data-to-view-master-pages-vb/_static/image2.png)](passing-data-to-view-master-pages-vb/_static/image1.png)

**圖 01**：在視圖主版頁面中顯示電影類別（[按一下以觀看完整大小的影像](passing-data-to-view-master-pages-vb/_static/image3.png)）

這是問題所在。 如何在主版頁面中取出電影類別目錄清單？ 直接在主版頁面中呼叫模型類別的方法相當吸引人。 換句話說，在主版頁面中包含用來從資料庫中抓取資料的程式碼很有吸引力。 不過，略過您的 MVC 控制器來存取資料庫，會違反建立 MVC 應用程式的主要優點之一，這是完全分離的問題。

在 MVC 應用程式中，您想要讓 mvc 視圖和 MVC 模型之間的所有互動都由 MVC 控制器處理。 這項顧慮的分離會導致更容易維護、可調整且可測試的應用程式。

在 MVC 應用程式中，傳遞至視圖的所有資料（包括視圖主版頁面）都應該透過控制器動作傳遞至視圖。 此外，您應該利用視圖資料來傳遞資料。 在本教學課程的其餘部分，我將探討兩種將 view 資料傳遞至視圖主版頁面的方法。

### <a name="the-simple-solution"></a>簡單的解決方案

讓我們從一個最簡單的解決方案開始，將視圖資料從控制器傳遞至視圖主版頁面。 最簡單的解決方法是在每個控制器動作中傳遞主版頁面的視圖資料。

請考慮 [清單 1] 中的控制器。 它會公開名為 `Index()` 和 `Details()`的兩個動作。 `Index()` 動作方法會傳回電影資料庫資料表中的每一部電影。 `Details()` 動作方法會傳回特定電影類別中的每一部電影。

**清單1– `Controllers\HomeController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample1.vb)]

請注意，`Index()` 和 `Details()` 動作都會加入兩個專案來查看資料。 `Index()` 動作會新增兩個索引鍵：分類和電影。 [類別目錄] 索引鍵代表視圖主版頁面所顯示的電影類別目錄清單。 電影金鑰代表索引視圖頁面所顯示的電影清單。

[`Details()`] 動作也會新增兩個名為 [類別和電影] 的機碼。 [類別目錄] 索引鍵同樣地代表 [視圖主版] 頁面所顯示的電影類別目錄清單。 電影金鑰代表詳細資料檢視頁面所顯示之特定類別中的電影清單（請參閱 [圖 2]）。

[![詳細資料檢視](passing-data-to-view-master-pages-vb/_static/image5.png)](passing-data-to-view-master-pages-vb/_static/image4.png)

**圖 02**：詳細資料檢視（[按一下以查看完整大小的影像](passing-data-to-view-master-pages-vb/_static/image6.png)）

索引視圖包含在 [清單 2] 中。 它只會逐一查看 [觀看資料] 中 [電影] 專案所代表的電影清單。

**清單2– `Views\Home\Index.aspx`**

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample2.aspx)]

[視圖主版] 頁面包含在 [清單 3] 中。 [視圖主版] 頁面會逐一查看並轉譯 [視圖資料] 中類別專案所代表的所有電影類別目錄。

**清單3– `Views\Shared\Site.master`**

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample3.aspx)]

所有資料都會透過視圖資料傳遞至視圖和視圖主版頁面。 這是將資料傳遞至主版頁面的正確方式。

那麼，這個解決方案有什麼問題呢？ 問題在於，此解決方案違反了試（不重複原則）原則。 每個控制器動作都必須新增相同的電影類別清單來查看資料。 在您的應用程式中擁有重複的程式碼，可讓您的應用程式更難以維護、調整和修改。

### <a name="the-good-solution"></a>良好的解決方案

在本節中，我們會探討將資料從控制器動作傳遞至視圖主版頁面的替代方案和更好的解決方案。 我們不會在每個控制器動作中新增主版頁面的電影類別，而是只將電影類別新增至 view 資料一次。 視圖主版頁面所使用的所有視圖資料都會加入應用程式控制器中。

ApplicationController 類別包含在 [清單 4] 中。

ApplicationController 類別包含在 [清單 4] 中。

**清單4– `Controllers\ApplicationController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample4.vb)]

在 [清單 4] 中，您應該會看到關於應用程式控制器的三件事。 首先，請注意，類別繼承自基底 System.web. Mvc 類別。 應用程式控制器是控制器類別。

第二，請注意，應用程式控制器類別是 MustInherit 類別。 MustInherit 類別是一個類別，必須由實體類別來執行。 因為應用程式控制器是 MustInherit 類別，所以您無法直接叫用在類別中定義的任何方法。 如果您嘗試直接叫用應用程式類別，則會出現「找不到資源」的錯誤訊息。

第三，請注意，應用程式控制器包含一個可新增電影類別清單以查看資料的函式。 繼承自應用程式控制器的每個控制器類別都會自動呼叫應用程式控制器的函式。 每當您在任何繼承自應用程式控制器的控制器上呼叫任何動作時，電影類別目錄就會自動包含在視圖資料中。

[清單 5] 中的 [電影控制器] 繼承自應用程式控制器。

**清單5– `Controllers\MoviesController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample5.vb)]

電影控制器就像上一節所討論的主控制器一樣，會公開名為 `Index()` 和 `Details()`的兩個動作方法。 請注意，視圖主版頁面所顯示的電影類別目錄清單並不會加入至 `Index()` 或 `Details()` 方法中的資料。 由於電影控制器會繼承自應用程式控制器，因此會自動新增電影類別清單來查看資料。

請注意，此方案會加入視圖主版頁面的視圖資料，並不會違反試（不重複原則）準則。 用來將電影類別目錄清單新增至視圖資料的程式碼只包含在一個位置：應用程式控制器的函式。

### <a name="summary"></a>總結

在本教學課程中，我們討論了兩種將視圖資料從控制器傳遞至視圖主版頁面的方法。 首先，我們檢查了簡單但很難維護的方法。 在第一節中，我們討論了如何在應用程式的每個控制器動作中，加入視圖主版頁面的視圖資料。 我們結論是，這是不好的方法，因為它違反了試（不重複原則）原則。

接下來，我們檢查了更好的策略來加入視圖主版頁面所需的資料，以查看資料。 我們不會在每個控制器動作中新增 view 資料，而是只在應用程式控制器內新增一次 view 資料。 如此一來，您可以在 ASP.NET MVC 應用程式中將資料傳遞至視圖主版頁面時，避免重複的程式碼。

> [!div class="step-by-step"]
> [上一篇](creating-page-layouts-with-view-master-pages-vb.md)
