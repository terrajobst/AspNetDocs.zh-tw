---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
title: 第5部分：商務邏輯 |Microsoft Docs
author: JoeStagner
description: 本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。 第5部分會加入一些商務邏輯。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: eaef475a-ca91-47ea-a4a7-d074005ed80c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
msc.type: authoredcontent
ms.openlocfilehash: c60eece9223c47304786d7b0d0ca4b11ac0572e9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78630302"
---
# <a name="part-5-business-logic"></a>第5部分：商務邏輯

依[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks 示範為 .NET 平臺建立功能強大、可擴充的應用程式有多麼簡單。 它會說明如何使用 ASP.NET 4 中的絕佳新功能來建立線上商店，包括購物、結帳和管理。
> 
> 本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。 第5部分會加入一些商務邏輯。

## <a id="_Toc260221671"></a>新增一些商務邏輯

我們希望每次有人造訪我們的網站時，都能使用我們的購物體驗。 即使他們未註冊或登入，訪客也能夠流覽並將專案新增至購物車。 當他們準備好簽出時，系統會提供驗證選項，如果他們還不是成員，他們就能夠建立帳戶。

這表示我們必須執行邏輯，將購物車從匿名狀態轉換為「已註冊的使用者」狀態。

讓我們建立一個名為「類別」的目錄，然後以滑鼠右鍵按一下該資料夾，並建立名為 MyShoppingCart.cs 的新「類別」檔案。

![](tailspin-spyworks-part-5/_static/image1.jpg)

![](tailspin-spyworks-part-5/_static/image1.png)

如先前所述，我們將擴充可執行 MyShoppingCart 的類別，我們將使用來進行此動作。NET 強大的「部分類別」結構。

針對我們的 MyShoppingCart.aspx.cf 檔案產生的呼叫看起來像這樣。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample1.cs)]

請注意 "partial" 關鍵字的用法。

我們剛才產生的類別檔案看起來像這樣。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample2.cs)]

我們也會將部分關鍵字新增至這個檔案，以合併我們的程式。

我們的新類別檔案現在看起來像這樣。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample3.cs)]

我們將在類別中新增的第一個方法是「AddItem」方法。 這是當使用者按一下 [產品清單] 和 [產品詳細資料] 頁面上的 [新增至美工] 連結時，最後會呼叫的方法。

將下列附加至頁面頂端的 using 語句。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample4.cs)]

並將此方法新增至 MyShoppingCart 類別。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample5.cs)]

我們會使用 LINQ to Entities 來查看該專案是否已存在於購物車中。 若是如此，我們會更新專案的訂單數量，否則我們會為選取的專案建立新的專案

為了呼叫這個方法，我們將會執行一個 AddToCart 的 .aspx 頁面，這個網頁不僅會將此方法類別，還會在新增專案之後顯示目前的購物 a = 購物車。

以滑鼠右鍵按一下 [方案瀏覽器] 中的方案名稱，然後新增名為 AddToCart 的新頁面，如同我們先前所做的一樣。

雖然我們可以使用此頁面來顯示暫時結果（例如，低股票問題），但在我們的實中，頁面實際上不會轉譯，而是呼叫「新增」邏輯和重新導向。

為了達成此目的，我們會將下列程式碼新增至頁面\_載入事件。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample6.cs)]

請注意，我們正在從 QueryString 參數中抓取要加入購物車的產品，並呼叫我們類別的 AddItem 方法。

假設未發生任何錯誤，控制權會傳遞至 SHoppingCart，我們將會在下一步中完整地執行此頁面。 如果應該發生錯誤，我們會擲回例外狀況。

目前我們尚未執行全域錯誤處理常式，因此我們的應用程式無法處理此例外狀況，但我們很快就會解決此問題。

另請注意語句 Debug. Fail （）的用法（可透過 `using System.Diagnostics;)`

應用程式是否在偵錯工具內執行，這個方法會顯示詳細的對話方塊，其中包含應用程式狀態的相關資訊，以及我們指定的錯誤訊息。

在生產環境中執行時，會忽略 Debug. Fail （）語句。

在上述程式碼中，您會注意到我們的購物車類別名稱 "GetShoppingCartId" 中的方法呼叫。

新增程式碼來執行方法，如下所示。

請注意，我們也新增了 [更新] 和 [簽出] 按鈕，以及可顯示購物車「總計」的標籤。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample7.cs)]

我們現在可以將專案新增至購物車，但我們尚未實行在新增產品後顯示購物車的邏輯。

因此，在 MyShoppingCart .aspx 頁面中，我們將新增 EntityDataSource 控制項和 GridVire 控制項，如下所示。

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample8.aspx)]

在設計工具中呼叫表單，讓您可以按兩下 [更新購物車] 按鈕，並產生在標記的宣告中指定的 click 事件處理常式。

我們稍後會執行詳細資料，但這麼做可讓我們建立和執行我們的應用程式，而不會發生錯誤。

當您執行應用程式並將專案新增至購物車時，您會看到這個。

![](tailspin-spyworks-part-5/_static/image2.jpg)

請注意，我們已藉由執行三個自訂資料行，從 [預設] 方格顯示中偏離。

第一個是適用于數量的可編輯「系結」欄位：

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample9.aspx)]

下一個是 [計算] 資料行，可顯示明細專案總計（專案成本乘以要排序的數量）：

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample10.aspx)]

最後，我們有一個包含 CheckBox 控制項的自訂資料行，使用者會用它來指出應該從購物圖表中移除該專案。

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample11.aspx)]

![](tailspin-spyworks-part-5/_static/image3.jpg)

如您所見，訂單合計列是空的，因此讓我們新增一些邏輯來計算訂單總計。

我們會先對我們的 MyShoppingCart 類別執行 "GetTotal" 方法。

在 MyShoppingCart.cs 檔案中，新增下列程式碼。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample12.cs)]

然後在頁面\_載入事件處理常式 中，我們可以呼叫 GetTotal 方法。 同時我們也會新增測試，以查看購物車是否為空白，並據此調整顯示。

現在，如果購物車是空的，我們會取得：

![](tailspin-spyworks-part-5/_static/image4.jpg)

如果不是，我們會看到總計。

![](tailspin-spyworks-part-5/_static/image5.jpg)

不過，此頁面尚未完成。

我們需要額外的邏輯來重新計算購物車，方法是移除標示為移除的專案，以及判斷新的數量詞，因為使用者可能已在方格中變更某些數值。

讓我們將 "RemoveItem" 方法新增至 MyShoppingCart.cs 中的購物車類別，以處理使用者標示要移除之專案的情況。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample13.cs)]

現在讓我們在使用者直接變更要在 GridView 中排序的品質時，使用一種方法來處理這種情況。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample14.cs)]

有了基本的 [移除] 和 [更新] 功能之後，我們就可以在資料庫中執行實際更新購物車的邏輯。 （在 MyShoppingCart.cs 中）

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample15.cs)]

您會注意到這個方法需要兩個參數。 其中一個是購物車識別碼，另一個則是使用者定義類型的物件陣列。

為了儘量減少我們的邏輯對使用者介面細節的相依性，我們定義了一個資料結構，我們可以用來將購物車專案傳遞給程式碼，而不需要直接存取 GridView 控制項的方法。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample16.cs)]

在我們的 MyShoppingCart.aspx.cs 檔案中，我們可以在 [更新] 按鈕的 Click 事件處理常式中使用此結構，如下所示。 請注意，除了更新購物車，我們也會更新購物車總計。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample17.cs)]

請注意，這行程式碼特別有趣：

[!code-javascript[Main](tailspin-spyworks-part-5/samples/sample18.js)]

GetValues （）是我們將在 MyShoppingCart.aspx.cs 中執行的特殊 helper 函式，如下所示。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample19.cs)]

這可讓您以全新的方式存取 GridView 控制項中繫結項目的值。 因為我們的「移除專案」核取方塊控制項並未系結，所以我們會透過 FindControl （）方法來存取它。

在您專案開發的這個階段，我們準備好開始執行結帳程式。

在這麼做之前，讓我們使用 Visual Studio 來產生成員資格資料庫，並將使用者新增至成員資格存放庫。

> [!div class="step-by-step"]
> [上一頁](tailspin-spyworks-part-4.md)
> [下一頁](tailspin-spyworks-part-6.md)
