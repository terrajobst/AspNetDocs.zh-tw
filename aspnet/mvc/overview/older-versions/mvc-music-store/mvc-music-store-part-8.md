---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
title: 第8部分：使用 Ajax 更新的購物車 |Microsoft Docs
author: jongalloway
description: 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第8部分涵蓋使用 Ajax 更新的購物車。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 26b2f55e-ed42-4277-89b0-c941eb754145
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
msc.type: authoredcontent
ms.openlocfilehash: 89897ad41b217764cbd17317d4bf5d6a5c5d488f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539253"
---
# <a name="part-8-shopping-cart-with-ajax-updates"></a>第8部分：使用 Ajax 更新的購物車

依[Jon Galloway](https://github.com/jongalloway)

> MVC 音樂存放區是教學課程應用程式，其仲介紹如何使用 ASP.NET MVC 和 Visual Studio 進行 web 程式開發的逐步解說。  
>   
> MVC 音樂存放區是輕量的範例商店執行，可在線上銷售音樂專輯，並實行基本的網站管理、使用者登入和購物車功能。  
>   
> 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第8部分涵蓋使用 Ajax 更新的購物車。

我們可讓使用者將專輯放在自己的購物車中，而不需註冊，但他們必須註冊為來賓才能完成結帳。 購物和結帳程式會分成兩個控制器：一個 ShoppingCart 控制器，可讓您以匿名方式將專案新增至購物車，並使用簽出控制器來處理結帳程式。 我們會從本節的「購物車」開始，然後在下一節中建立結帳程式。

## <a name="adding-the-cart-order-and-orderdetail-model-classes"></a>加入購物車、順序和 OrderDetail 模型類別

我們的購物車和結帳程式會使用一些新的類別。 以滑鼠右鍵按一下 [模型] 資料夾，然後使用下列程式碼加入購物車類別（Cart.cs）。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample1.cs)]

這個類別非常類似于目前為止使用的其他專案，但 RecordId 屬性的 [Key] 屬性除外。 我們的購物車專案會有一個名為 CartID 的字串識別碼，以允許匿名購物，但資料表包含名為 RecordId 的整數主要金鑰。 依照慣例，Entity Framework 程式碼優先預期名為購物車之資料表的主鍵會是 CartId 或 ID，但我們可以視需要透過注釋或程式碼輕鬆地覆寫該金鑰。 這是一個範例，示範如何在 Entity Framework 程式碼中使用簡單的慣例（如果它們符合我們的條件），但不會在它們不受到限制。

接下來，使用下列程式碼新增 Order 類別（Order.cs）。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample2.cs)]

這個類別會追蹤訂單的摘要和傳遞資訊。 **它還不會編譯**，因為它有一個 OrderDetails 的導覽屬性，其相依于尚未建立的類別。 讓我們透過新增名為 OrderDetail.cs 的類別，新增下列程式碼來修正此問題。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample3.cs)]

我們會對我們的 MusicStoreEntities 類別進行最後一次更新，以包含會公開這些新模型類別的 DbSets，其中也包括 DbSet&lt;的演出者&gt;。 更新後的 MusicStoreEntities 類別會如下所示。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample4.cs)]

## <a name="managing-the-shopping-cart-business-logic"></a>管理購物車商務邏輯

接下來，我們會在 [模型] 資料夾中建立 ShoppingCart 類別。 ShoppingCart 模型會處理對購物車資料表的資料存取。 此外，它也會處理從購物車新增和移除專案的商務邏輯。

因為我們不想要求使用者註冊帳戶，只是要將專案新增至購物車，所以我們會在存取購物車時，為使用者指派一個暫時的唯一識別碼（使用 GUID 或全域唯一識別碼）。 我們會使用 ASP.NET 會話類別來儲存此識別碼。

*注意： ASP.NET 會話是一個方便的位置，用來儲存使用者特定資訊，這會在離開網站後過期。雖然誤用會話狀態可能會對較大的網站造成效能的影響，但我們的輕量使用也適用于示範用途。*

ShoppingCart 類別會公開下列方法：

**AddToCart**會採用專輯做為參數，並將它新增至使用者的購物車。 由於 [購物車] 資料表會追蹤每個專輯的數量，因此它會包含邏輯以視需要建立新的資料列，或只在使用者已訂購一份專輯副本時，才增加數量。

**RemoveFromCart**會採用專輯識別碼，並將它從使用者的購物車中移除。 如果使用者的購物車中只有一個專輯複本，則會移除該資料列。

**EmptyCart**會從使用者的購物車移除所有專案。

**GetCartItems**會抓取用於顯示或處理的 CartItems 清單。

**GetCount**會抓取使用者在其購物車中的專輯總數。

**GetTotal**會計算購物車中所有專案的總成本。

**CreateOrder**會在結帳階段期間將購物車轉換成訂單。

**GetCart**是一種靜態方法，可讓我們的控制器取得購物車物件。 它會使用**GetCartId**方法來處理從使用者的會話讀取 CartId。 GetCartId 方法需要 HttpCoNtextBase，讓它可以從使用者的會話讀取使用者的 CartId。

以下是完整的**ShoppingCart 類別**：

[!code-csharp[Main](mvc-music-store-part-8/samples/sample5.cs)]

## <a name="viewmodels"></a>ViewModels

我們的購物車控制器必須將一些複雜的資訊傳達給其觀點，而無法完全對應到我們的模型物件。 我們不想要修改我們的模型，以符合我們的觀點;模型類別應該代表我們的網域，而不是使用者介面。 其中一個解決方法是使用 ViewBag 類別將資訊傳遞給我們的視圖，如同我們對存放區管理員的下拉式清單資訊所做的，但透過 ViewBag 傳遞大量資訊很難管理。

解決方法是使用*ViewModel*模式。 使用此模式時，我們會建立針對我們的特定視圖案例優化的強型別類別，並針對我們的視圖範本所需的動態值/內容公開屬性。 接著，我們的控制器類別可以填入這些視圖優化的類別，並將其傳遞給我們的 view 範本來使用。 這可讓您在 [視圖] 範本內進行型別安全、編譯時間檢查和編輯器 IntelliSense。

我們會建立兩個用於購物車控制器的視圖模型： ShoppingCartViewModel 會保存使用者購物車的內容，而 ShoppingCartRemoveViewModel 則會在使用者移除某個專案時用來顯示確認資訊從他們的購物車。

讓我們在專案的根目錄中建立新的 Viewmodel 資料夾，以保持組織的內容。 以滑鼠右鍵按一下專案，然後選取 [加入]/[新增資料夾]。

![](mvc-music-store-part-8/_static/image1.jpg)

將資料夾命名為 Viewmodel。

![](mvc-music-store-part-8/_static/image1.png)

接下來，在 Viewmodel 資料夾中新增 ShoppingCartViewModel 類別。 它有兩個屬性：購物車專案清單，以及用來保存購物車中所有專案之總價的十進位值。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample6.cs)]

現在，將 ShoppingCartRemoveViewModel 新增至 Viewmodel 資料夾，並具有下列四個屬性。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample7.cs)]

## <a name="the-shopping-cart-controller"></a>購物車控制器

購物車控制器有三個主要用途：將專案新增至購物車、移除購物車中的專案，以及查看購物車中的專案。 它會使用我們剛才建立的三個類別： ShoppingCartViewModel、ShoppingCartRemoveViewModel 和 ShoppingCart。 如同在 StoreController 和 StoreManagerController 中，我們會新增欄位來保存 MusicStoreEntities 的實例。

使用空白控制器範本，將新的購物車控制器新增至專案。

![](mvc-music-store-part-8/_static/image2.png)

以下是完整的 ShoppingCart 控制器。 「索引」和「新增控制器」動作看起來應該很熟悉。 [移除] 和 [CartSummary 控制器] 動作會處理兩個特殊案例，我們將在下一節中討論。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample8.cs)]

## <a name="ajax-updates-with-jquery"></a>使用 jQuery 的 Ajax 更新

接下來，我們將建立一個強型別為 ShoppingCartViewModel 的購物車索引頁面，並使用與先前相同的方法來使用清單視圖範本。

![](mvc-music-store-part-8/_static/image3.png)

不過，我們不會使用 Html.actionlink 來移除購物車中的專案，而是使用 jQuery 以「連接」此視圖中所有連結的 click 事件，其中具有 HTML 類別 RemoveLink。 此 click 事件處理常式不會張貼表單，而只會對我們的 RemoveFromCart 控制器動作進行 AJAX 回呼。 RemoveFromCart 會傳回 JSON 序列化結果，而我們的 jQuery 回呼接著會使用 jQuery 剖析並執行四個快速更新頁面：

- 1. 從清單中移除已刪除的專輯
- 2. 更新標頭中的購物車計數
- 3. 向使用者顯示更新訊息
- 4. 更新購物車的總價

由於「移除」案例正由「索引」視圖內的 Ajax 回呼處理，因此我們不需要額外的 RemoveFromCart 動作視圖。 以下是/ShoppingCart/Index view 的完整程式碼：

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample9.cshtml)]

為了測試這一點，我們必須能夠將專案新增至我們的購物車。 我們會更新**存放區詳細資料**視圖，以包含 [新增至購物車] 按鈕。 當我們在此時，我們可以包含我們在上次更新此視圖之後新增的一些專輯其他資訊：內容類型、演出者、價格和專輯封面。 更新的商店詳細資料檢視程式碼隨即出現，如下所示。

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample10.cshtml)]

現在，我們可以按一下 [存放區]，並在我們的購物車中進行新增和移除專輯的測試。 執行應用程式，並流覽至存放區索引。

![](mvc-music-store-part-8/_static/image4.png)

接下來，按一下內容類型來查看專輯清單。

![](mvc-music-store-part-8/_static/image5.png)

按一下專輯標題現在會顯示更新的專輯詳細資料檢視，包括 [新增至購物車] 按鈕。

![](mvc-music-store-part-8/_static/image6.png)

按一下 [新增至購物車] 按鈕，即可使用 [購物車摘要] 清單顯示我們的購物車索引視圖。

![](mvc-music-store-part-8/_static/image7.png)

載入購物車之後，您可以按一下 [從購物車移除] 連結，以查看您的購物車的 Ajax 更新。

![](mvc-music-store-part-8/_static/image8.png)

我們建立了一個可運作的購物車，讓未註冊的使用者可以將專案新增至購物車。 在下一節中，我們將允許他們註冊並完成結帳程式。

> [!div class="step-by-step"]
> [上一頁](mvc-music-store-part-7.md)
> [下一頁](mvc-music-store-part-9.md)
