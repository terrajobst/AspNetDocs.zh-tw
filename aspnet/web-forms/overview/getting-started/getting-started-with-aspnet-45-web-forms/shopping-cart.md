---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/shopping-cart
title: 購物車 |Microsoft Docs
author: Erikre
description: 本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 為我們建立 ASP.NET Web Forms 應用程式的基本概念 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 6898c601-6c31-432f-8388-e6843f8a17cb
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/shopping-cart
msc.type: authoredcontent
ms.openlocfilehash: d3b619ebd9448d30857ffbaf17fd245b1d54a662
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519293"
---
# <a name="shopping-cart"></a>購物車

依[Erik Reitan](https://github.com/Erikre)

[下載 Wingtip 玩具範例專案（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下載電子書（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 建立 ASP.NET Web Forms 應用程式的基本概念。 本教學課程系列隨附有[ C#原始程式碼](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 專案。

本教學課程說明將購物車新增至 Wingtip 玩具範例 ASP.NET Web Forms 應用程式所需的商務邏輯。 本教學課程是根據上一個教學課程「顯示資料項目和詳細資料」來建立，屬於 Wingtip 玩具商店教學課程系列。 當您完成本教學課程時，您的範例應用程式使用者將能夠在其購物車中新增、移除及修改產品。

## <a name="what-youll-learn"></a>您將學到什麼：

1. 如何建立 web 應用程式的購物車。
2. 如何讓使用者將專案新增至購物車。
3. 如何新增[GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview(v=vs.110).aspx#introduction)控制項以顯示購物車詳細資料。
4. 如何計算和顯示訂單總計。
5. 如何移除和更新購物車中的專案。
6. 如何包含購物車計數器。

## <a name="code-features-in-this-tutorial"></a>本教學課程中的程式碼功能：

1. Entity Framework Code First
2. 資料註釋
3. 強型別資料控制
4. 模型繫結

## <a name="creating-a-shopping-cart"></a>建立購物車

稍早在本教學課程系列中，您已新增頁面和程式碼，以從資料庫中查看產品資料。 在本教學課程中，您將建立購物車來管理使用者有興趣購買的產品。 使用者即使未註冊或登入，也可以流覽並將專案新增至購物車。 若要管理購物車存取權，當使用者第一次存取購物車時，您會使用全域唯一識別碼（GUID）將唯一的 `ID` 指派給使用者。 您會使用 ASP.NET 會話狀態來儲存此 `ID`。

> [!NOTE] 
> 
> ASP.NET 會話狀態是儲存使用者特定資訊的方便位置，這會在使用者離開網站後過期。 雖然誤用會話狀態可能會對較大的網站造成效能的影響，但會話狀態的輕量使用很適合用於示範。 Wingtip 玩具範例專案顯示如何使用沒有外部提供者的會話狀態，其中會話狀態會在裝載網站的 web 伺服器上以同進程方式儲存。 對於提供多個應用程式實例的大型網站，或針對在不同伺服器上執行多個應用程式實例的網站，請考慮使用**Windows Azure**快取服務。 此快取服務會提供網站外部的分散式快取服務，並解決使用同進程會話狀態的問題。 如需詳細資訊，請參閱[如何搭配 Windows Azure 網站使用 ASP.NET 會話狀態](https://docs.microsoft.com/azure/redis-cache/cache-aspnet-session-state-provider)。

### <a name="add-cartitem-as-a-model-class"></a>將 CartItem 新增為模型類別

稍早在本教學課程系列中，您可以藉由在 [*模型*] 資料夾中建立 `Category` 和 `Product` 類別，來定義分類和產品資料的架構。 現在，新增類別以定義購物車的架構。 稍後在本教學課程中，您將加入一個類別來處理 `CartItem` 資料表的資料存取。 這個類別會供應商業規則來新增、移除及更新購物車中的專案。

1. 以滑鼠右鍵按一下 [*模型*] 資料夾，**然後選取 [** 新增 -&gt;**新專案**]。 

    ![購物車-新專案](shopping-cart/_static/image1.png)
2. 隨即顯示 [ 新增項目] 對話方塊。 選取 [程式**代碼**]，然後選取 [**類別**]。 

    ![購物車-[加入新專案] 對話方塊](shopping-cart/_static/image2.png)
3. 將這個新類別命名為*CartItem.cs*。
4. 按一下 [加入]。  
   新的類別檔案會顯示在編輯器中。
5. 使用下列程式碼來取代預設程式碼：   

    [!code-csharp[Main](shopping-cart/samples/sample1.cs)]

`CartItem` 類別包含會定義使用者新增至購物車之每個產品的架構。 這個類別與您稍早在本教學課程系列中建立的其他架構類別類似。 依照慣例，Entity Framework Code First 預期 `CartItem` 資料表的主鍵會是 `CartItemId` 或 `ID`。 不過，程式碼會使用資料批註 `[Key]` 屬性來覆寫預設行為。 ItemId 屬性的 `Key` 屬性會指定 `ItemID` 屬性是主要索引鍵。

`CartId` 屬性會指定與要購買的專案相關聯之使用者的 `ID`。 當使用者存取購物車時，您會新增程式碼來建立此使用者 `ID`。 此 `ID` 也會儲存為 ASP.NET 會話變數。

### <a name="update-the-product-context"></a>更新產品內容

除了加入 `CartItem` 類別以外，您還需要更新管理實體類別的資料庫內容類別，並提供資料庫的資料存取權。 若要這麼做，您要將新建立的 `CartItem` 模型類別加入至 `ProductContext` 類別。

1. 在**方案總管**中，尋找並開啟 [*模型*] 資料夾中的*ProductCoNtext.cs*檔案。
2. 將反白顯示的程式碼新增至*ProductCoNtext.cs*檔案，如下所示：  

    [!code-csharp[Main](shopping-cart/samples/sample2.cs?highlight=14)]

如先前在本教學課程系列中所述， *ProductCoNtext.cs*檔案中的程式碼會新增 `System.Data.Entity` 命名空間，讓您可以存取 Entity Framework 的所有核心功能。 這項功能包括使用強型別物件來查詢、插入、更新和刪除資料的功能。 `ProductContext` 類別會加入新加入 `CartItem` 模型類別的存取權。

### <a name="managing-the-shopping-cart-business-logic"></a>管理購物車商務邏輯

接下來，您將在新的*邏輯*資料夾中建立 `ShoppingCart` 類別。 `ShoppingCart` 類別會處理 `CartItem` 資料表的資料存取。 類別也會包含商務邏輯，以新增、移除和更新購物車中的專案。

您將新增的購物車邏輯將包含管理下列動作的功能：

1. 將專案新增至購物車
2. 從購物車移除專案
3. 取得購物車識別碼
4. 從購物車中取出專案
5. 匯總所有購物車專案的數量
6. 更新購物車資料

[購物車] 頁面（*ShoppingCart .aspx*）和 [購物車] 類別會一起用來存取購物車資料。 [購物車] 頁面將會顯示使用者新增至購物車的所有專案。 除了 [購物車] 頁面和類別以外，您還會建立一個頁面（*AddToCart .aspx*），將產品新增至購物車。 您也會將程式碼加入至*ProductList*頁面，以及將提供*AddToCart*頁面連結的*ProductDetails*頁面，讓使用者可以將產品新增至購物車。

下圖顯示當使用者將產品新增至購物車時所發生的基本程式。

![購物車-新增至購物車](shopping-cart/_static/image3.png)

當使用者按一下 [ *ProductList* ] 頁面或 [ *ProductDetails* ] 頁面上的 [**新增至購物車**] 連結時，應用程式將會流覽至 [ *AddToCart* ] 頁面，然後自動移至 [ *ShoppingCart* ] 頁面。 *AddToCart*會藉由呼叫 ShoppingCart 類別中的方法，將選取產品新增至購物車。 [ *ShoppingCart* ] 頁面會顯示已新增至「購物車」的產品。

#### <a name="creating-the-shopping-cart-class"></a>建立購物車類別

`ShoppingCart` 類別會加入至應用程式中的個別資料夾，讓模型（模型資料夾）、頁面（根資料夾）和邏輯（邏輯資料夾）之間有清楚的區別。

1. 在**方案總管**中，以滑鼠右鍵按一下**WingtipToys**專案，然後選取 [**加入**-] &gt;[**新增資料夾**]。 將新資料夾命名為*邏輯*。
2. 以滑鼠右鍵按一下*邏輯*資料夾，**然後選取 [** 新增 -&gt;**新專案**]。
3. 新增名為*ShoppingCartActions.cs*的新類別檔案。
4. 使用下列程式碼來取代預設程式碼：   

    [!code-csharp[Main](shopping-cart/samples/sample3.cs)]

`AddToCart` 方法可根據產品 `ID`，將個別產品納入購物車中。 產品會新增至購物車，或如果購物車已經包含該產品的專案，則數量會遞增。

`GetCartId` 方法會傳回使用者 `ID` 的購物車。 購物車 `ID` 用來追蹤使用者在其購物車中的專案。 如果使用者沒有現有的購物車 `ID`，系統就會為他們建立新的購物車 `ID`。 如果使用者是以已註冊的使用者身分登入，購物車 `ID` 會設定為其使用者名稱。 不過，如果使用者未登入，購物車 `ID` 會設定為唯一值（GUID）。 GUID 可確保根據會話，只為每個使用者建立一個購物車。

`GetCartItems` 方法會傳回使用者的購物車專案清單。 稍後在本教學課程中，您會看到使用 `GetCartItems` 方法，將模型系結用於顯示購物車中的購物車專案。

### <a name="creating-the-add-to-cart-functionality"></a>建立「新增至購物車」功能

如先前所述，您將建立名為*AddToCart*的處理頁面，用來將新產品新增至使用者的購物車。 此頁面將會在您剛才建立的 `ShoppingCart` 類別中呼叫 `AddToCart` 方法。 *AddToCart*會預期會將產品 `ID` 傳遞至該頁面。 在 `ShoppingCart` 類別中呼叫 `AddToCart` 方法時，將會使用此產品 `ID`。

> [!NOTE] 
> 
> 您將修改此頁面的程式碼後置（*AddToCart.aspx.cs*），而不是頁面 UI （*AddToCart .aspx*）。

#### <a name="to-create-the-add-to-cart-functionality"></a>若要建立「新增至購物車」功能：

1. 在**方案總管**中，以滑鼠右鍵按一下**WingtipToys**專案，**然後按一下 [** 新增 -&gt;**新專案**]。  
   隨即顯示 [ 新增項目] 對話方塊。
2. 將標準的新頁面（Web Form）新增至名為*AddToCart*的應用程式。 

    ![購物車-新增 Web 表單](shopping-cart/_static/image4.png)
3. 在**方案總管**中，以滑鼠右鍵按一下 [ *AddToCart* ] 頁面，然後按一下 [**查看程式碼**]。 *AddToCart.aspx.cs*程式碼後置檔案會在編輯器中開啟。
4. 將*AddToCart.aspx.cs*程式碼後置中的現有程式碼取代為下列內容：   

    [!code-csharp[Main](shopping-cart/samples/sample4.cs)]

載入*AddToCart .aspx*頁面時，會從查詢字串中抓取產品 `ID`。 接下來，會建立購物車類別的實例，並使用它來呼叫您稍早在本教學課程中新增的 `AddToCart` 方法。 包含在*ShoppingCartActions.cs*檔案中的 `AddToCart` 方法包括將選取的產品新增至購物車的邏輯，或增加所選產品的產品數量。 如果產品尚未新增至「購物車」，則會將產品新增至資料庫的 `CartItem` 資料表。 如果產品已新增至購物車，而使用者新增了相同產品的其他專案，則 [`CartItem`] 資料表中的產品數量會遞增。 最後，頁面會重新導向回到您將在下一個步驟中新增的*ShoppingCart*頁面，使用者會在其中看到購物車中已更新的專案清單。

如先前所述，使用者 `ID` 是用來識別與特定使用者相關聯的產品。 每次使用者將產品新增至購物車時，都會將此 `ID` 新增至 `CartItem` 資料表中的資料列。

### <a name="creating-the-shopping-cart-ui"></a>建立購物車 UI

[ *ShoppingCart* ] 頁面會顯示使用者已新增到其購物車的產品。 它也能讓您新增、移除和更新購物車中的專案。

1. 在**方案總管**中，以滑鼠**按右鍵 [** **WingtipToys**]，然後按一下 [新增 -&gt;**新專案**]。  
   隨即顯示 [ 新增項目] 對話方塊。
2. **使用主版頁面選取 Web 表單**，以新增包含主版頁面的新頁面（Web form）。 將新頁面命名為*ShoppingCart .aspx*。
3. 選取 [**網站**]，將主版頁面附加至新建立的 *.aspx*頁面。
4. 在 [ *ShoppingCart* ] 頁面中，將現有標記取代為下列標記：   

    [!code-aspx[Main](shopping-cart/samples/sample5.aspx)]

*ShoppingCart .aspx*頁面包含名為 `CartList`的**GridView**控制項。 此控制項使用模型系結，將購物車資料從資料庫系結至**GridView**控制項。 當您設定**GridView**控制項的 [`ItemType`] 屬性時，資料系結運算式 `Item` 會出現在控制項的標記中，而控制項則會變成強型別。 如稍早在本教學課程系列中所述，您可以使用 IntelliSense 來選取 `Item` 物件的詳細資料。 若要將資料控制項設定為使用模型系結來選取資料，您必須設定控制項的 `SelectMethod` 屬性。 在上述標記中，您會將 `SelectMethod` 設定為使用 GetShoppingCartItems 方法，以傳回 `CartItem` 物件的清單。 **GridView**資料控制項會在頁面生命週期的適當時間呼叫方法，並自動系結傳回的資料。 您仍然必須加入 `GetShoppingCartItems` 方法。

#### <a name="retrieving-the-shopping-cart-items"></a>正在抓取購物車專案

接下來，您要將程式碼新增至*ShoppingCart.aspx.cs*程式碼後置，以取出並填入購物車 UI。

1. 在**方案總管**中，以滑鼠右鍵按一下 [ *ShoppingCart* ] 頁面，然後按一下 [**查看程式碼**]。 *ShoppingCart.aspx.cs*程式碼後置檔案會在編輯器中開啟。
2. 將現有的程式碼取代為下列程式碼：  

    [!code-csharp[Main](shopping-cart/samples/sample6.cs)]

如前所述，`GridView` 資料控制項會在頁面生命週期的適當時間呼叫 `GetShoppingCartItems` 方法，並自動系結傳回的資料。 `GetShoppingCartItems` 方法會建立 `ShoppingCartActions` 物件的實例。 然後，程式碼會使用該實例，藉由呼叫 `GetCartItems` 方法來傳回購物車中的專案。

### <a name="adding-products-to-the-shopping-cart"></a>將產品新增至購物車

當顯示 [ *ProductList* ] 或 [ *ProductDetails* ] 頁面時，使用者將能夠使用連結將產品新增至購物車。 當他們按一下連結時，應用程式會流覽至名為*AddToCart*的處理頁面。 *AddToCart*會呼叫您稍早在本教學課程中新增的 `ShoppingCart` 類別中的 `AddToCart` 方法。

現在，您會將 [**新增至購物車**] 連結新增至 [ *ProductList* ] 頁面和 [ *ProductDetails* ] 頁面。 此連結會包含從資料庫中抓取的產品 `ID`。

1. 在**方案總管**中，尋找並開啟名為*ProductList*的頁面。
2. 將以黃色反白顯示的標記新增至 [ *ProductList* ] 頁面，讓整個頁面顯示如下：  

    [!code-aspx[Main](shopping-cart/samples/sample7.aspx?highlight=50-54)]

### <a name="testing-the-shopping-cart"></a>測試購物車

執行應用程式，以瞭解如何將產品新增至購物車。

1. 按 **F5** 執行應用程式。  
 在專案重新建立資料庫之後，瀏覽器將會開啟並顯示*default.aspx*頁面。
2. 從 [類別] 流覽功能表中選取 [ **Cars** ]。  
 隨即顯示 [ *ProductList* ] 頁面，只顯示 "Cars" 類別中包含的產品。 

    ![購物車-汽車](shopping-cart/_static/image5.png)
3. 按一下所列第一個產品旁的 [**新增至購物車**] 連結（可轉換的車）。   
 隨即顯示 [ *ShoppingCart* ] 頁面，顯示您的購物車中的選取專案。 

    ![購物車-購物車](shopping-cart/_static/image6.png)
4. 從 [類別] 導覽功能表選取 [**平面**]，以查看其他產品。
5. 按一下所列第一個產品旁的 [**新增至購物車**] 連結。  
 隨即會顯示 [ *ShoppingCart* ] 頁面，其中包含其他專案。
6. 關閉瀏覽器。

### <a name="calculating-and-displaying-the-order-total"></a>計算和顯示訂單總計

除了將產品新增至購物車以外，您還會將 `GetTotal` 方法新增至 [`ShoppingCart`] 類別，並在 [購物車] 頁面中顯示總訂單金額。

1. 在**方案總管**中，開啟*邏輯*資料夾中的*ShoppingCartActions.cs*檔案。
2. 將下列 `GetTotal` 方法以黃色反白顯示 `ShoppingCart` 類別，讓類別顯示如下：   

    [!code-csharp[Main](shopping-cart/samples/sample8.cs?highlight=85-97)]

首先，`GetTotal` 方法會取得使用者的購物車識別碼。 然後，方法會將產品價格乘以購物車中列出之每個產品的產品數量，藉以取得購物車總計。

> [!NOTE] 
> 
> 上述程式碼會使用可為 null 的型別 "`int?`"。 可為 null 的類型可以表示基礎類型的所有值，以及 null 值。 如需詳細資訊，請參閱[使用可為 null 的類型](https://msdn.microsoft.com/library/2cf62fcy(v=vs.110).aspx)。

### <a name="modify-the-shopping-cart-display"></a>修改購物車顯示

接下來，您將修改*ShoppingCart*的程式碼，以呼叫 `GetTotal` 方法，並在頁面載入時，在*ShoppingCart*頁面上顯示該總計。

1. 在**方案總管**中，以滑鼠右鍵按一下 [ *ShoppingCart* ] 頁面，然後選取 [ **View Code**]。
2. 在*ShoppingCart.aspx.cs*檔案中，新增下列以黃色反白顯示的程式碼，以更新 `Page_Load` 處理常式：   

    [!code-csharp[Main](shopping-cart/samples/sample9.cs?highlight=16-31)]

當*ShoppingCart .aspx*頁面載入時，它會載入購物車物件，然後藉由呼叫 `ShoppingCart` 類別的 `GetTotal` 方法來抓取購物車總計。 如果購物車是空的，就會顯示該效果的訊息。

### <a name="testing-the-shopping-cart-total"></a>測試購物車總計

立即執行應用程式，以瞭解您不能只將產品新增至購物車，但可以查看購物車總計。

1. 按 **F5** 執行應用程式。  
 瀏覽器便會開啟並顯示 *Default.aspx* 頁面。
2. 從 [類別] 流覽功能表中選取 [ **Cars** ]。
3. 按一下第一個產品旁的 [**新增至購物車**] 連結。   
 隨即顯示 [ *ShoppingCart* ] 頁面與 [訂單總計]。 

    ![購物車-購物車總計](shopping-cart/_static/image7.png)
4. 將一些其他產品（例如平面）新增至購物車。
5. 隨即會顯示 [ *ShoppingCart* ] 頁面，其中包含您已新增的所有產品的更新總計。 

    ![購物車-多項產品](shopping-cart/_static/image8.png)
6. 關閉瀏覽器視窗以停止執行中的應用程式。

### <a name="adding-update-and-checkout-buttons-to-the-shopping-cart"></a>將 [更新] 和 [簽出] 按鈕新增至購物車

若要允許使用者修改購物車，您要將 [**更新**] 按鈕和 [**結帳**] 按鈕新增至 [購物車] 頁面。 在本教學課程系列稍後的版本中，不會使用 [**簽出**] 按鈕。

1. 在**方案總管**中，開啟 web 應用程式專案根目錄中的 [ *ShoppingCart* ] 頁面。
2. 若要將 [**更新**] 按鈕和 [**簽出**] 按鈕新增至*ShoppingCart*頁面，請將以黃色反白顯示的標記新增至現有的標記，如下列程式碼所示：   

    [!code-aspx[Main](shopping-cart/samples/sample10.aspx?highlight=36-45)]

當使用者按一下 [**更新**] 按鈕時，就會呼叫 `UpdateBtn_Click` 事件處理常式。 這個事件處理常式會呼叫您將在下一個步驟中新增的程式碼。

接下來，您可以更新*ShoppingCart.aspx.cs*檔案中包含的程式碼，以迴圈處理購物車專案，並呼叫 `RemoveItem` 和 `UpdateItem` 方法。

1. 在**方案總管**中，開啟 web 應用程式專案根目錄中的*ShoppingCart.aspx.cs*檔案。
2. 將下列以黃色反白顯示的程式碼區段新增至*ShoppingCart.aspx.cs*檔案：   

    [!code-csharp[Main](shopping-cart/samples/sample11.cs?highlight=9-11,33,44-89)]

當使用者按一下 [ *ShoppingCart* ] 頁面上的 [**更新**] 按鈕時，就會呼叫 UpdateCartItems 方法。 UpdateCartItems 方法會針對購物車中的每個專案取得更新的值。 然後，UpdateCartItems 方法會呼叫 `UpdateShoppingCartDatabase` 方法（在下一個步驟中新增並說明），以從購物車新增或移除專案。 一旦更新資料庫以反映購物車的更新之後， **gridview**控制項就會藉由呼叫**gridview**的 `DataBind` 方法，在 [購物車] 頁面上更新。 此外，[購物車] 頁面上的 [總訂單數量] 也會更新，以反映專案的更新清單。

### <a name="updating-and-removing-shopping-cart-items"></a>更新和移除購物車專案

在 [ *ShoppingCart* ] 頁面上，您可以看到已加入的控制項，用於更新專案的數量和移除專案。 現在，請新增程式碼，讓這些控制項能夠正常執行。

1. 在**方案總管**中，開啟*邏輯*資料夾中的*ShoppingCartActions.cs*檔案。
2. 將下列以黃色反白顯示的程式碼新增至*ShoppingCartActions.cs*類別檔案：   

    [!code-csharp[Main](shopping-cart/samples/sample12.cs?highlight=99-213)]

`UpdateShoppingCartDatabase` 方法（從 [ *ShoppingCart.aspx.cs* ] 頁面上的 [`UpdateCartItems`] 方法呼叫）包含從 [購物車] 更新或移除專案的邏輯。 `UpdateShoppingCartDatabase` 方法會逐一查看購物車清單中的所有資料列。 如果已標示要移除的購物車專案，或數量小於一，則會呼叫 `RemoveItem` 方法。 否則，在呼叫 `UpdateItem` 方法時，會檢查購物車專案是否有更新。 移除或更新購物車專案之後，就會儲存資料庫變更。

`ShoppingCartUpdates` 結構用來保存所有購物車專案。 `UpdateShoppingCartDatabase` 方法會使用 `ShoppingCartUpdates` 結構來判斷是否需要更新或移除任何專案。

在下一個教學課程中，您將使用 `EmptyCart` 方法來清除購買產品後的購物車。 但現在，您將使用剛新增至*ShoppingCartActions.cs*檔案的 `GetCount` 方法，來判斷購物車中有多少專案。

### <a name="adding-a-shopping-cart-counter"></a>加入購物車計數器

若要允許使用者查看購物車中的總專案數，您要將計數器新增至 [*網站*] 頁面。 此計數器也會做為購物車的連結。

1. 在**方案總管**中，開啟 [*網站*] 頁面。
2. 將 [購物車] 計數器連結新增至導覽區段，以修改標記，如下所示：  

    [!code-html[Main](shopping-cart/samples/sample13.html?highlight=6)]
3. 接下來，新增以黃色反白顯示的程式碼，以更新*Site.Master.cs*檔案的程式碼後置，如下所示：  

    [!code-csharp[Main](shopping-cart/samples/sample14.cs?highlight=11,77-84)]

將頁面轉譯為 HTML 之前，會引發 `Page_PreRender` 事件。 在 `Page_PreRender` 處理常式中，購物車的總計數是藉由呼叫 `GetCount` 方法來決定。 傳回的值會加入至*網站主版*頁面的標記所包含的 `cartCount` 範圍內。 `<span>` 標記可正確呈現內部元素。 當網站的任何頁面顯示時，將會顯示購物車總計。 使用者也可以按一下 [購物車總計]，以顯示 [購物車]。

## <a name="testing-the-completed-shopping-cart"></a>測試已完成的購物車

您可以立即執行應用程式，以瞭解如何在「購物車」中新增、刪除及更新專案。 購物車總計會反映購物車中所有專案的總成本。

1. 按 **F5** 執行應用程式。  
 瀏覽器會開啟並顯示*default.aspx*頁面。
2. 從 [類別] 流覽功能表中選取 [ **Cars** ]。
3. 按一下第一個產品旁的 [**新增至購物車**] 連結。   
 隨即顯示 [ *ShoppingCart* ] 頁面與 [訂單總計]。
4. 從 [類別] 導覽功能表選取 [**平面**]。
5. 按一下第一個產品旁的 [**新增至購物車**] 連結。
6. 將購物車中第一個專案的數量設定為3，然後選取第二個專案的 [**移除專案**] 核取方塊。<a id="a"></a>
7. 按一下 [**更新**] 按鈕以更新 [購物車] 頁面，並顯示新的訂單總計。 

    ![購物車-購物車更新](shopping-cart/_static/image9.png)

## <a name="summary"></a>總結

在本教學課程中，您已建立 Wingtip 玩具 Web Forms 範例應用程式的購物車。 在本教學課程中，您已使用 Entity Framework Code First、資料批註、強型別資料控制和模型系結。

購物車支援新增、刪除和更新使用者已選取要購買的專案。 除了執行購物車功能以外，您也已瞭解如何在**GridView**控制項中顯示購物車專案，並計算訂單總計。

若要瞭解所述的功能在實際商務應用程式中的運作方式，您可以觀看[nopCommerce](https://github.com/nopSolutions/nopCommerce) -ASP.NET 型開放原始碼電子商務購物車的範例。 原本，它是建立在 Web form 上，而過去幾年來，它會移至 MVC，現在 ASP.NET Core。

## <a name="addition-information"></a>額外資訊

[ASP.NET 工作階段狀態概觀](https://msdn.microsoft.com/library/ms178581.aspx)

> [!div class="step-by-step"]
> [上一頁](display_data_items_and_details.md)
> [下一頁](checkout-and-payment-with-paypal.md)
