---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
title: 第9部分：註冊和簽出 |Microsoft Docs
author: jongalloway
description: 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第9部分涵蓋註冊和簽出。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: d65c5c2b-a039-463f-ad29-25cf9fb7a1ba
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
msc.type: authoredcontent
ms.openlocfilehash: 040bc0ccef889fb9a7c3d9b5ce88c75b7b754248
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559532"
---
# <a name="part-9-registration-and-checkout"></a>第9部分：註冊和簽出

依[Jon Galloway](https://github.com/jongalloway)

> MVC 音樂存放區是教學課程應用程式，其仲介紹如何使用 ASP.NET MVC 和 Visual Studio 進行 web 程式開發的逐步解說。  
>   
> MVC 音樂存放區是輕量的範例商店執行，可在線上銷售音樂專輯，並實行基本的網站管理、使用者登入和購物車功能。  
>   
> 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第9部分涵蓋註冊和簽出。

在本節中，我們將建立 CheckoutController，其會收集購物者的位址和付款資訊。 我們會要求使用者在簽出之前向我們的網站註冊，因此此控制站將需要授權。

使用者可以按一下 [結帳] 按鈕，從購物車流覽至結帳程式。

![](mvc-music-store-part-9/_static/image1.jpg)

如果使用者未登入，系統會提示他們輸入。

![](mvc-music-store-part-9/_static/image1.png)

成功登入後，使用者就會顯示在 [位址] 和 [付款] 視圖中。

![](mvc-music-store-part-9/_static/image2.png)

填寫表單並提交訂單後，就會顯示在 [訂單確認] 畫面上。

![](mvc-music-store-part-9/_static/image3.png)

嘗試查看不存在的順序或不屬於您的順序時，將會顯示錯誤視圖。

![](mvc-music-store-part-9/_static/image4.png)

## <a name="migrating-the-shopping-cart"></a>遷移購物車

當購物程式是匿名的時，當使用者按一下 [結帳] 按鈕時，就必須註冊並登入。 使用者會預期我們會在造訪之間維護其購物車資訊，因此，當他們完成註冊或登入時，我們需要將購物車資訊與使用者建立關聯。

這其實非常簡單，因為我們的 ShoppingCart 類別已經有一個方法，可將目前購物車中的所有專案與使用者名稱產生關聯。 只有在使用者完成註冊或登入時，才需要呼叫這個方法。

開啟我們在設定成員資格和授權時所新增的**AccountController**類別。 加入參考 MvcMusicStore 的 using 語句，然後新增下列 MigrateShoppingCart 方法：

[!code-csharp[Main](mvc-music-store-part-9/samples/sample1.cs)]

接下來，修改登入 post 動作，以在使用者經過驗證後呼叫 MigrateShoppingCart，如下所示：

[!code-csharp[Main](mvc-music-store-part-9/samples/sample2.cs)]

在成功建立使用者帳戶之後，立即對 [註冊 post] 動作進行相同的變更：

[!code-csharp[Main](mvc-music-store-part-9/samples/sample3.cs)]

這就是-現在匿名購物車會在成功註冊或登入時自動轉移到使用者帳戶。

## <a name="creating-the-checkoutcontroller"></a>建立 CheckoutController

以滑鼠右鍵按一下 [控制器] 資料夾，然後使用空白控制器範本，將新的控制器新增至名為 CheckoutController 的專案。

![](mvc-music-store-part-9/_static/image5.png)

首先，將 [授權] 屬性新增至控制器類別宣告上方，以要求使用者在簽出前先進行註冊：

[!code-csharp[Main](mvc-music-store-part-9/samples/sample4.cs)]

*注意：這與先前對 StoreManagerController 所做的變更類似，但在此情況下，授權屬性需要使用者必須是系統管理員角色。在結帳控制器中，我們要求使用者登入，但不要求他們是系統管理員。*

為了簡單起見，我們不會在本教學課程中處理付款資訊。 相反地，我們允許使用者使用促銷代碼來簽出。 我們會使用名為促銷代碼的常數來儲存此促銷代碼。

如同在 StoreController 中，我們會宣告一個欄位來保存 MusicStoreEntities 類別的實例，名為 storeDB。 若要使用 MusicStoreEntities 類別，我們必須為 MvcMusicStore 命名空間加入 using 語句。 我們的結帳控制器頂端會顯示如下。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample5.cs)]

CheckoutController 將會有下列控制器動作：

**AddressAndPayment （GET 方法）** 會顯示一個表單，讓使用者輸入其資訊。

**AddressAndPayment （POST 方法）** 會驗證輸入並處理訂單。

**完成**將會在使用者成功完成簽出程式之後顯示。 此視圖會包含使用者的訂單號碼，做為確認。

首先，讓我們將索引控制器動作（在我們建立控制器時產生）重新命名為 AddressAndPayment。 此控制器動作只會顯示簽出表單，因此不需要任何模型資訊。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample6.cs)]

我們的 AddressAndPayment 文章方法將遵循我們在 StoreManagerController 中使用的相同模式：它會嘗試接受表單提交並完成訂單，如果失敗，將會重新顯示表單。

驗證表單輸入符合訂單的驗證需求之後，我們會直接檢查促銷代碼表單值。 假設一切都正確，我們將以訂單儲存更新後的資訊，告訴 ShoppingCart 物件完成訂單程式，然後重新導向至完整的動作。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample7.cs)]

成功完成結帳程式後，系統會將使用者重新導向至完整的控制器動作。 此動作會執行簡單的檢查，以驗證訂單確實屬於已登入的使用者，然後才將訂單號碼顯示為確認。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample8.cs)]

*注意：當我們開始專案時，會在/Views/Shared 資料夾中自動為我們建立錯誤視圖。*

完整的 CheckoutController 程式碼如下所示：

[!code-csharp[Main](mvc-music-store-part-9/samples/sample9.cs)]

## <a name="adding-the-addressandpayment-view"></a>新增 AddressAndPayment 視圖

現在，讓我們建立 AddressAndPayment view。 以滑鼠右鍵按一下其中一個 [AddressAndPayment 控制器] 動作，並新增名為 AddressAndPayment 的視圖，其強型別為訂單並使用編輯範本，如下所示。

![](mvc-music-store-part-9/_static/image6.png)

此視圖會使用我們在建立 StoreManagerEdit view 時所查看的兩種技術：

- 我們將使用 EditorForModel （）來顯示訂單模型的表單欄位
- 我們將使用順序類別搭配驗證屬性來運用驗證規則

首先，我們將更新表單程式碼來使用 EditorForModel （），然後再加上促銷代碼的額外文字方塊。 AddressAndPayment view 的完整程式碼如下所示。

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample10.cshtml)]

## <a name="defining-validation-rules-for-the-order"></a>定義訂單的驗證規則

我們已設定好我們的視圖，接下來我們會設定訂單模型的驗證規則，就像先前針對專輯模型所做的一樣。 以滑鼠右鍵按一下 [模型] 資料夾，然後新增名為 Order 的類別。 除了我們先前針對專輯使用的驗證屬性以外，我們也會使用正則運算式來驗證使用者的電子郵件地址。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample11.cs)]

嘗試提交具有遺失或無效資訊的表單，現在會使用用戶端驗證來顯示錯誤訊息。

![](mvc-music-store-part-9/_static/image7.png)

好的，我們已完成簽出程式的大部分困難的工作;我們只會有一些機率，並結束完成。 我們需要新增兩個簡單的視圖，而且我們需要在登入程式期間，負責交付購物車資訊。

## <a name="adding-the-checkout-complete-view"></a>加入結帳完整視圖

[結帳完成] 視圖非常簡單，因為它只需要顯示訂單識別碼。 以滑鼠右鍵按一下 [完成控制器] 動作，並新增名為 [完成] 的視圖，其強型別為 int。

![](mvc-music-store-part-9/_static/image8.png)

現在，我們將更新 view 程式碼以顯示訂單識別碼，如下所示。

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample12.cshtml)]

## <a name="updating-the-error-view"></a>正在更新錯誤視圖

預設範本會在 [共用的 views] 資料夾中包含錯誤視圖，以便在網站中的其他地方重複使用。 這個錯誤視圖包含非常簡單的錯誤，而且不會使用我們的網站版面配置，所以我們會進行更新。

由於這是一般錯誤網頁，內容非常簡單。 如果使用者想要重新嘗試其動作，我們會包含訊息和連結，以流覽至歷程記錄中的上一頁。

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample13.cshtml)]

> [!div class="step-by-step"]
> [上一頁](mvc-music-store-part-8.md)
> [下一頁](mvc-music-store-part-10.md)
