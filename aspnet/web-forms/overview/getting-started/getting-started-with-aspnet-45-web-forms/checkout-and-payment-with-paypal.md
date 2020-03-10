---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
title: 簽出與使用 PayPal 付款 |Microsoft Docs
author: Erikre
description: 本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 為我們建立 ASP.NET Web Forms 應用程式的基本概念 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 664ec95e-b0c9-4f43-a39f-798d0f2a7e08
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
msc.type: authoredcontent
ms.openlocfilehash: 62d00a86c6c5845fb894896df65002c7086d039f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78565405"
---
# <a name="checkout-and-payment-with-paypal"></a>簽出與使用 PayPal 付款

依[Erik Reitan](https://github.com/Erikre)

[下載 Wingtip 玩具範例專案（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下載電子書（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 建立 ASP.NET Web Forms 應用程式的基本概念。 本教學課程系列隨附有[ C#原始程式碼](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 專案。

本教學課程說明如何修改 Wingtip 玩具範例應用程式，以包含使用 PayPal 的使用者授權、註冊和付款。 只有登入的使用者才會擁有購買產品的授權。 ASP.NET 4.5 Web form 專案範本的內建使用者註冊功能已包含您所需的大部分內容。 您將新增 PayPal 快速簽出功能。 在本教學課程中，您將使用 PayPal 開發人員測試環境，因此不會傳輸實際的資金。 在本教學課程結束時，您將會藉由選取要加入購物車的產品、按一下 [結帳] 按鈕，然後將資料傳送到 PayPal 測試網站，來測試應用程式。 在 PayPal 測試網站上，您將會確認您的寄送和付款資訊，然後返回當地的 Wingtip 玩具範例應用程式，以確認並完成購買。

有幾個經驗豐富的協力廠商付款處理器，專門用來解決擴充性和安全性的線上購物。 ASP.NET 開發人員應該先考慮使用協力廠商付款解決方案的優點，再執行購物和購買解決方案。

> [!NOTE] 
> 
> Wingtip 玩具範例應用程式的設計，是為了示範 ASP.NET 網頁程式開發人員所能使用的特定 ASP.NET 概念和功能。 這個範例應用程式未針對擴充性和安全性方面的所有可能情況進行優化。

## <a name="what-youll-learn"></a>您將學到什麼：

- 如何限制對資料夾中特定頁面的存取。
- 如何從匿名購物車建立已知的購物車。
- 如何為專案啟用 SSL。
- 如何將 OAuth 提供者新增至專案。
- 如何使用 paypal 來購買使用 PayPal 測試環境的產品。
- 如何在**DetailsView**控制項中顯示 PayPal 的詳細資料。
- 如何使用從 PayPal 取得的詳細資料來更新 Wingtip 玩具應用程式的資料庫。

## <a name="adding-order-tracking"></a>新增訂單追蹤

在本教學課程中，您將建立兩個新的類別，以根據使用者建立的順序來追蹤資料。 這些類別會追蹤有關運送資訊、購買總計和付款確認的資料。

### <a name="add-the-order-and-orderdetail-model-classes"></a>加入 Order 和 OrderDetail 模型類別

稍早在本教學課程系列中，您可以藉由在 [*模型*] 資料夾中建立 `Category`、`Product`和 `CartItem` 類別，來定義類別目錄、產品和購物車專案的架構。 現在您將加入兩個新的類別，以定義產品訂單的架構和訂單的詳細資料。

1. 在 [**模型**] 資料夾中，加入名為*Order.cs*的新類別。   
   新的類別檔案會顯示在編輯器中。
2. 使用下列項目取代預設程式碼：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample1.cs)]
3. 將*OrderDetail.cs*類別新增至 [*模型*] 資料夾。
4. 使用下列程式碼來取代預設程式碼：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample2.cs)]

`Order` 和 `OrderDetail` 類別包含用來定義用於購買和出貨之訂單資訊的架構。

此外，您還需要更新管理實體類別的資料庫內容類別，並提供資料庫的資料存取權。 若要這樣做，您要將新建立的順序和 `OrderDetail` 模型類別加入 `ProductContext` 類別。

1. 在**方案總管**中，尋找並開啟*ProductCoNtext.cs*檔案。
2. 將反白顯示的程式碼新增至*ProductCoNtext.cs*檔案，如下所示：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample3.cs?highlight=14-15)]

如先前在本教學課程系列中所述， *ProductCoNtext.cs*檔案中的程式碼會新增 `System.Data.Entity` 命名空間，讓您可以存取 Entity Framework 的所有核心功能。 這項功能包括使用強型別物件來查詢、插入、更新和刪除資料的功能。 在 `ProductContext` 類別中的上述程式碼會加入 Entity Framework 存取新增的 `Order` 和 `OrderDetail` 類別。

## <a name="adding-checkout-access"></a>新增簽出存取權

Wingtip 玩具範例應用程式可讓匿名使用者進行審查，並將產品新增至購物車。 不過，當匿名使用者選擇購買他們新增至購物車的產品時，他們必須登入網站。 登入之後，他們就可以存取處理結帳和購買程式的 Web 應用程式限制頁面。 這些限制的頁面會包含在應用程式的 [*結帳*] 資料夾中。

### <a name="add-a-checkout-folder-and-pages"></a>新增簽出資料夾和頁面

您現在將會建立 [*結帳*] 資料夾，以及客戶會在結帳程式中看到的頁面。 您稍後會在本教學課程中更新這些頁面。

1. 在**方案總管**中，以滑鼠右鍵按一下專案名稱（**Wingtip 玩具**），然後選取 [**新增資料夾**]。 

    ![使用 PayPal 簽出和付款-新的資料夾](checkout-and-payment-with-paypal/_static/image1.png)
2. 將新資料夾命名為*Checkout*。
3. 以滑鼠右鍵按一下 [*簽出*] 資料夾，**然後選取 [** 新增-&gt;**新專案**]。 

    ![使用 PayPal 簽出和付款-新專案](checkout-and-payment-with-paypal/_static/image2.png)
4. 隨即顯示 [ 新增項目] 對話方塊。
5. 選取左側的 [ **Visual C#**  -&gt; **Web**範本] 群組。 然後，在中間窗格中，選取 [**使用主版頁面的 Web 表單**]，並將它命名為*CheckoutStart .aspx*。 

    ![使用 PayPal 簽出和付款-加入新專案對話方塊](checkout-and-payment-with-paypal/_static/image3.png)
6. 如先前所示，請選取 [*網站*] 檔案作為主版頁面。
7. 使用上述相同步驟，將下列其他頁面新增至 [*簽出*] 資料夾：   

    - CheckoutReview .aspx
    - CheckoutComplete .aspx
    - CheckoutCancel .aspx
    - CheckoutError .aspx

### <a name="add-a-webconfig-file"></a>新增 Web.config 檔案

藉由*將新的 web.config 檔案*新增至 [*簽出*] 資料夾，您就能夠限制對該資料夾中包含的所有頁面進行存取。

1. 以滑鼠右鍵按一下 [*簽出*] 資料夾，**然後選取 [** 新增 -&gt;**新專案**]。  
   隨即顯示 [ 新增項目] 對話方塊。
2. 選取左側的 [ **Visual C#**  -&gt; **Web**範本] 群組。 然後，在中間窗格中選取 [ **Web 設定檔**]，接受*web.config*的預設名稱，然後選取 [**新增**]。
3. 使用下列內容來取代 *Web.config* 檔案中的現有 XML 內容：  

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample4.xml)]
4. 儲存 *Web.config* 檔案。

Web.config*檔案*會指定 web 應用程式的所有未知使用者都必須被拒絕存取*簽出*資料夾中包含的頁面。 不過，如果使用者已註冊帳戶並登入，他們會是已知的使用者，而且可以存取 [*簽出*] 資料夾中的頁面。

請務必注意，ASP.NET 設定會遵循階層，其中每個*web.config*檔案會將設定值套用至其所在的資料夾，以及其底下的所有子目錄。

<a id="SSLWebForms"></a>
## <a name="enable-ssl-for-the-project"></a>對專案啟用 SSL

 安全通訊端層 (SSL) 是一種定義的通訊協定，允許 Web 伺服器和 Web 用戶端透過加密，以更安全的方式進行通訊。 未使用 SSL 時，在用戶端和伺服器之間傳送的資料會開放給任何可實體存取網路的人員進行封包探查。 此外，數種常見驗證結構描述在一般的 HTTP 上並不是很安全。 尤其是，基本驗證和表單驗證會傳送未加密的認證。 為了安全的理由，這些驗證結構描述必須使用 SSL。 

1. 在**方案總管**中，按一下 [ **WingtipToys** ] 專案，然後按**F4**顯示 [**屬性**] 視窗。
2. 將 [ **SSL 已啟用**] 變更為 `true`。
3. 複製 **SSL URL** ，以便稍後使用。   
 除非您先前已建立 SSL 網站（如下所示），否則 SSL URL 將會 `https://localhost:44300/`。   
    ![專案屬性](checkout-and-payment-with-paypal/_static/image4.png)
4. 在**方案總管**中，以滑鼠右鍵按一下**WingtipToys**專案，然後按一下 [**屬性**]。
5. 在左側索引標籤中按一下 [Web]。
6. 將 [**專案 Url** ] 變更為使用您稍早儲存的**SSL Url** 。   
    ![專案 Web 屬性](checkout-and-payment-with-paypal/_static/image5.png)
7. 按 **CTRL+S**儲存頁面。
8. 按 **CTRL+F5** 執行應用程式。 Visual Studio 將會顯示可避開 SSL 警告的選項。
9. 按一下 [ **是** ] 以信任 IIS Express SSL 憑證並繼續。   
    ![IIS Express SSL 憑證資訊](checkout-and-payment-with-paypal/_static/image6.png)  
 隨即顯示一則安全性警告。
10. 按一下 [ **是** ] 將憑證安裝到您的 localhost。   
    ![[安全性警告] 對話方塊](checkout-and-payment-with-paypal/_static/image7.png)  
 瀏覽器視窗隨即出現。

您現在可以使用 SSL，輕鬆地在本機測試 Web 應用程式。

<a id="OAuthWebForms"></a>
## <a name="add-an-oauth-20-provider"></a>新增 OAuth 2.0 提供者

ASP.NET Web Forms 提供成員資格和驗證的增強功能選項。 這些增強功能包括 OAuth。 OAuth 是一種開放式通訊協定，可讓 Web、行動和桌面應用程式以簡單、標準的方法執行安全授權。 ASP.NET Web Forms 範本會使用 OAuth 將 Facebook、Twitter、Google 和 Microsoft 公開為驗證提供者。 雖然本教學課程僅使用 Google 作為驗證提供者，但您可以輕易修改程式碼來使用任何提供者。 實作其他提供者的步驟，與您將在本教學課程中看到的步驟極為類似。

除了驗證，本教學課程也會使用角色來實作授權。 只有您新增至 `canEdit` 角色的使用者才能建立、編輯或刪除連絡人。

> [!NOTE] 
> 
> Windows Live 應用程式只接受工作網站的即時 URL，因此您無法使用本機網站 URL 來測試登入。

下列步驟可新增 Google 驗證提供者。

1. 開啟*應用程式\_Start\Startup.Auth.cs*檔案。
2. 移除 `app.UseGoogleAuthentication()` 方法中的註解字元，然後此方法會顯示如下： 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample5.cs)]
3. 瀏覽至 [Google Developers Console](https://console.developers.google.com/)。 您還需要使用您的 Google 開發人員電子郵件帳戶 (gmail.com) 登入。 如果您沒有 Google 帳戶，請選取 [ **建立帳戶** ] 連結。   
   接下來，您會看到 [ **Google 開發人員主控台**]。   
    ![Google Developers Console](checkout-and-payment-with-paypal/_static/image8.png)
4. 按一下 [**建立專案**] 按鈕，然後輸入 [專案名稱] 和 [識別碼] （您可以使用預設值）。 然後按一下 [**合約] 核取方塊**和 [**建立**] 按鈕。  

    ![Google-新增專案](checkout-and-payment-with-paypal/_static/image9.png)

   幾秒鐘內即可建立新的專案，您的瀏覽器便會顯示新的專案頁面。
5. 在左側索引標籤中，按一下 [ **api &amp; auth**]，然後按一下 [**認證**]。
6. 按一下 [ **OAuth**] 底下的 [**建立新的用戶端識別碼**]。   
   [ **建立用戶端識別碼** ] 對話方塊隨即出現。   
    ![Google -  建立用戶端識別碼](checkout-and-payment-with-paypal/_static/image10.png)
7. 在 [**建立用戶端識別碼**] 對話方塊中，保留應用程式類型的預設**Web 應用程式**。
8. 將**授權的 JavaScript 來源**設定為您稍早在本教學課程中使用的 SSL URL （除非您已建立其他 SSL 專案，否則`https://localhost:44300/`）。   
   此 URL 會是應用程式的原始來源。 在此範例中，您將僅輸入 localhost 測試 URL。 不過，您可以輸入多個 Url 來考慮 localhost 和生產環境。
9. 將 [Authorized Redirect URI] 設定如下： 

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample6.html)]

   此值是 ASP.NET OAuth 使用者與 Google OAuth 伺服器進行通訊的 URI。 請記住您先前使用的 SSL URL （除非您已建立其他 SSL 專案，否則 `https://localhost:44300/`）。
10. 按一下 [**建立用戶端識別碼**] 按鈕。
11. 在 Google 開發人員主控台的左側功能表上，按一下 [**同意畫面**] 功能表項目，然後設定您的電子郵件地址和產品名稱。 當您完成表單時，請按一下 [**儲存**]。
12. 按一下 [ **api** ] 功能表項目、向下流覽，然後按一下 [ **Google + API**] 旁的 [**關閉**] 按鈕。   
    接受此選項將會啟用 Google + API。
13. 您也必須將**Owin** NuGet 套件更新為版本3.0.0。   
    從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**管理方案的 NuGet 套件**]。  
    從 [**管理 NuGet 封裝**] 視窗中，尋找**Owin**套件並將其更新為版本3.0.0。
14. 在 Visual Studio 中，將**用戶端識別碼**和**用戶端密碼**複製並貼到方法中，以更新*Startup.Auth.cs*頁面的 `UseGoogleAuthentication` 方法。 以下顯示的**用戶端識別碼**和**用戶端秘密**值為範例，因此無法使用。 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample7.cs?highlight=64-65)]
15. 按 **CTRL+F5** 以建置並執行應用程式。 按一下 [登入] 連結。
16. 在 [**使用其他服務登入**] 底下，按一下 [ **Google**]。  
    ![登入](checkout-and-payment-with-paypal/_static/image11.png)
17. 如果您需要輸入認證，您會被重新導向至 Google 網站，您可以在此輸入認證。  
    ![Google - 登入](checkout-and-payment-with-paypal/_static/image12.png)
18. 在您輸入認證之後，系統會提示您將許可權授與您剛建立的 web 應用程式。  
    ![專案預設服務帳戶](checkout-and-payment-with-paypal/_static/image13.png)
19. 按一下 [接受]。 您現在會重新導向回到**WingtipToys**應用程式的 [**註冊**] 頁面，您可以在其中註冊 Google 帳戶。  
    ![以您的 Google 帳戶註冊](checkout-and-payment-with-paypal/_static/image14.png)
20. 您可以選擇變更用於 Gmail 帳戶的本機電子郵件註冊名稱，但您通常會想保留預設電子郵件別名 (也就是，您用來驗證的名稱)。 按一下 [**登入**]，如上所示。

### <a name="modifying-login-functionality"></a>修改登入功能

如先前在本教學課程系列中所述，大部分的使用者註冊功能已包含在 ASP.NET Web form 範本中，預設為。 現在您將修改預設的*Login* ，並*註冊 .aspx*頁面來呼叫 `MigrateCart` 方法。 `MigrateCart` 方法會將新登入的使用者與匿名購物車產生關聯。 藉由建立使用者和購物車的關聯，Wingtip 玩具範例應用程式將能夠在造訪間維護使用者的購物車。

1. 在**方案總管**中，尋找並開啟 [*帳戶*] 資料夾。
2. 修改名為*Login.aspx.cs*的程式碼後置頁面，以包含以黃色反白顯示的程式碼，讓它看起來如下：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample8.cs?highlight=41-43)]
3. 儲存*Login.aspx.cs*檔案。

現在，您可以忽略 `MigrateCart` 方法沒有定義的警告。 稍後在本教學課程中，您將會新增它。

*Login.aspx.cs*程式碼後置檔案支援登入方法。 藉由檢查 Login .aspx 頁面，您會看到此頁面包含 [登入] 按鈕，當您按一下 [在程式碼後置時觸發 `LogIn` 處理常式]。

呼叫*Login.aspx.cs*上的 `Login` 方法時，會建立名為 `usersShoppingCart` 的購物車的新實例。 購物車的識別碼（GUID）會被取出並設定為 `cartId` 變數。 然後，會呼叫 `MigrateCart` 方法，同時將 `cartId` 和登入使用者的名稱傳遞給這個方法。 遷移購物車時，用來識別匿名購物車的 GUID 會以使用者名稱取代。

除了修改*Login.aspx.cs*程式碼後置檔案，以在使用者登入時遷移購物車時，您也必須修改*Register.aspx.cs 程式碼後*置檔案，以在使用者建立新帳戶並登入時遷移購物車。

1. 在 [*帳戶*] 資料夾中，開啟名為*Register.aspx.cs*的程式碼後置檔案。
2. 以黃色包含程式碼來修改程式碼後置檔案，讓它看起來如下所示：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample9.cs?highlight=28-32)]
3. 儲存*Register.aspx.cs*檔案。 同樣地，忽略有關 `MigrateCart` 方法的警告。

請注意，您在 `CreateUser_Click` 事件處理常式中使用的程式碼，與您在 `LogIn` 方法中使用的程式碼非常類似。 當使用者註冊或登入網站時，將會進行 `MigrateCart` 方法的呼叫。

## <a name="migrating-the-shopping-cart"></a>遷移購物車

現在您已更新登入和註冊程式，您可以使用 `MigrateCart` 方法來新增程式碼，以遷移購物車。

1. 在**方案總管**中，尋找*邏輯*資料夾並開啟*ShoppingCartActions.cs*類別檔案。
2. 將黃色反白顯示的程式碼新增至*ShoppingCartActions.cs*檔案中的現有程式碼，讓*ShoppingCartActions.cs*檔案中的程式碼顯示如下：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample10.cs?highlight=215-224)]

`MigrateCart` 方法會使用現有的 cartId 來尋找使用者的購物車。 接下來，程式碼會迴圈處理所有的購物車專案，並以登入的使用者名稱取代 `CartId` 屬性（如 `CartItem` 架構所指定）。

### <a name="updating-the-database-connection"></a>正在更新資料庫連接

如果您使用**預先**建立的 Wingtip 玩具範例應用程式來遵循本教學課程，就必須重新建立預設的成員資格資料庫。 藉由修改預設連接字串，將會在下一次執行應用程式時建立成員資格資料庫。

1. 開啟位於專案根目錄的*web.config*檔案。
2. 更新預設連接字串，讓它看起來如下所示：   

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample11.xml)]

<a id="PayPalWebForms"></a>
## <a name="integrating-paypal"></a>整合 PayPal

PayPal 是以網路為基礎的計費平臺，可接受線上商家的付款。 本教學課程將說明如何將 PayPal 的「快速簽出」功能整合到您的應用程式中。 「快速簽出」可讓您的客戶使用 PayPal 來支付他們已新增至購物車的專案。

### <a name="create-paypal-test-accounts"></a>建立 PayPal 測試帳戶

若要使用 PayPal 測試環境，您必須建立並驗證開發人員測試帳戶。 您將使用開發人員測試帳戶來建立買方測試帳戶和賣方測試帳戶。 開發人員測試帳號憑證也會允許 Wingtip 玩具範例應用程式存取 PayPal 測試環境。

1. 在瀏覽器中，流覽至 PayPal 開發人員測試網站：   
    [https://developer.paypal.com](https://developer.paypal.com/)
2. 如果您沒有 PayPal 開發人員帳戶，請按一下 [**註冊**] 並遵循註冊步驟來建立新的帳戶。 如果您有現有的 PayPal 開發人員帳戶，請按一下 [**登入**] 來登入。 稍後在本教學課程中，您將需要 PayPal 開發人員帳戶來測試 Wingtip 玩具範例應用程式。
3. 如果您剛註冊 PayPal 開發人員帳戶，您可能需要使用 PayPal 來驗證您的 PayPal 開發人員帳戶。 您可以遵循 PayPal 傳送至您的電子郵件帳戶的步驟來驗證您的帳戶。 確認您的 PayPal 開發人員帳戶之後，請重新登入 PayPal 開發人員測試網站。
4. 使用您的 PayPal 開發人員帳戶登入 PayPal 開發人員網站之後，您必須建立 PayPal 買方測試帳戶（如果還沒有的話）。 若要建立買方測試帳戶，請在 PayPal 網站上按一下 [**應用程式**] 索引標籤，然後按一下 [**沙箱帳戶**]。   
 [**沙箱測試帳戶**] 頁面隨即顯示。   

    > [!NOTE] 
    > 
    > PayPal 開發人員網站已經供應商家測試帳戶。

    ![使用 PayPal 簽出和付款-沙箱測試帳戶](checkout-and-payment-with-paypal/_static/image15.png)
5. 在 [沙箱測試帳戶] 頁面上，按一下 [**建立帳戶**]。
6. 在 [**建立測試帳戶**] 頁面上，選擇您選擇的買方測試帳戶電子郵件和密碼。   

    > [!NOTE] 
    > 
    > 在本教學課程結尾處，您將需要購買者的電子郵件地址和密碼，才能測試 Wingtip 玩具範例應用程式。

    ![使用 PayPal 簽出和付款-沙箱測試帳戶](checkout-and-payment-with-paypal/_static/image16.png)
7. 按一下 [**建立帳戶**] 按鈕，以建立買方測試帳戶。  
 [**沙箱測試帳戶**] 頁面隨即顯示。 

    ![使用 PayPal 簽出和付款-PayPal 帳戶](checkout-and-payment-with-paypal/_static/image17.png)
8. 在 [**沙箱測試帳戶**] 頁面上，按一下 [**主持**者電子郵件帳戶]。  
    [**設定檔**] 和 [**通知**] 選項隨即出現。
9. 選取 [**設定檔**] 選項，然後按一下 [ **API 認證**] 以查看您的商家測試帳戶的 api 認證。
10. 將測試 API 認證複製到 [記事本]。

您將需要顯示的傳統測試 API 認證（使用者名稱、密碼和簽章），以從 Wingtip 玩具範例應用程式對 PayPal 測試環境進行 API 呼叫。 您會在下一個步驟中新增認證。

### <a name="add-paypal-class-and-api-credentials"></a>新增 PayPal 類別和 API 認證

您會將大部分的 PayPal 程式碼放入單一類別中。 此類別包含用來與 PayPal 通訊的方法。 此外，您也會將您的 PayPal 認證新增至此類別。

1. 在 Visual Studio 內的 Wingtip 玩具範例應用程式中，以滑鼠右鍵按一下**邏輯**資料夾，**然後選取 [** 新增 -&gt;**新專案**]。   
   隨即顯示 [ 新增項目] 對話方塊。
2. 在左側 [**已安裝**] 窗格中的 [**視覺效果C#**  ] 底下，選取 [程式**代碼**]。
3. 從中間窗格中，選取 [**類別**]。 將這個新類別命名為**PayPalFunctions.cs**。
4. 按一下 [新增]。  
   新的類別檔案會顯示在編輯器中。
5. 使用下列程式碼來取代預設程式碼：  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample12.cs)]
6. 新增您稍早在本教學課程中所顯示的商家 API 認證（使用者名稱、密碼和簽章），讓您可以對 PayPal 測試環境進行函式呼叫。  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample13.cs)]

> [!NOTE] 
> 
> 在此範例應用程式中，您只需將C#認證新增至檔案（.cs）。 不過，在已實行的解決方案中，您應該考慮在設定檔中加密您的認證。

NVPAPICaller 類別包含大部分的 PayPal 功能。 類別中的程式碼提供從 PayPal 測試環境進行測試購買所需的方法。 下列三個 PayPal 函數可用來進行購買：

- `SetExpressCheckout` 函式
- `GetExpressCheckoutDetails` 函式
- `DoExpressCheckoutPayment` 函式

`ShortcutExpressCheckout` 方法會從購物車收集測試購買資訊和產品詳細資料，並呼叫 `SetExpressCheckout` PayPal 函數。 `GetCheckoutDetails` 方法會確認購買詳細資料，並在進行測試之前，先呼叫 `GetExpressCheckoutDetails` PayPal 函數。 `DoCheckoutPayment` 方法會藉由呼叫 `DoExpressCheckoutPayment` PayPal 函式，從測試環境完成測試購買。 其餘的程式碼支援 PayPal 方法和程式，例如編碼字串、解碼字串、處理陣列，以及判斷認證。

> [!NOTE] 
> 
> PayPal 可讓您根據[paypal 的 API 規格](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout)，包含選擇性的購買詳細資料。 藉由在 Wingtip 玩具範例應用程式中擴充程式碼，您可以包含當地語系化詳細資料、產品描述、稅金、客戶服務編號，以及其他許多選用欄位。

請注意，在**ShortcutExpressCheckout**方法中指定的傳回和取消 url 會使用通訊埠編號。

[!code-html[Main](checkout-and-payment-with-paypal/samples/sample14.html)]

當 Visual Web Developer 使用 SSL 執行 Web 專案時，通常會將埠44300用於 web 伺服器。 如上所示，埠號碼是44300。 當您執行應用程式時，可能會看到不同的埠號碼。 您必須在程式碼中正確設定您的埠號碼，才能在本教學課程結尾處成功執行 Wingtip 玩具範例應用程式。 本教學課程的下一節將說明如何取出本機主機埠號碼，並更新 PayPal 類別。

### <a name="update-the-localhost-port-number-in-the-paypal-class"></a>更新 PayPal 類別中的 LocalHost 埠號碼

Wingtip 玩具範例應用程式會藉由流覽至 PayPal 測試網站，並返回您的 Wingtip 玩具範例應用程式的本機實例來購買產品。 為了讓 PayPal 回到正確的 URL，您必須在上述 PayPal 代碼中指定本機執行中範例應用程式的埠號碼。

1. 以滑鼠右鍵按一下**方案總管**中的專案名稱（**WingtipToys**），然後選取 [**屬性**]。
2. 在左欄中，選取 [ **Web** ] 索引標籤。
3. 從 [**專案 Url** ] 方塊中取出埠號碼。
4. 如有需要，請更新*PayPalFunctions.cs*檔案中 PayPal 類別（`NVPAPICaller`）的 `returnURL` 和 `cancelURL`，以使用 web 應用程式的埠號碼：   

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample15.html?highlight=1-2)]

現在，您所新增的程式碼會符合本機 Web 應用程式的預期通訊埠。 PayPal 將能夠回到您本機電腦上正確的 URL。

### <a name="add-the-paypal-checkout-button"></a>新增 [PayPal 結帳] 按鈕

現在，主要 PayPal 函式已新增至範例應用程式，您可以開始加入呼叫這些函式所需的標記和程式碼。 首先，您必須新增使用者會在 [購物車] 頁面上看到的 [結帳] 按鈕。

1. 開啟*ShoppingCart .aspx*檔案。
2. 流覽至檔案底部，並尋找 `<!--Checkout Placeholder -->` 批註。
3. 將批註取代為 `ImageButton` 控制項，讓 mark 的標記取代如下：  

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample16.aspx)]
4. 在*ShoppingCart.aspx.cs*檔案中，在接近檔案結尾的 `UpdateBtn_Click` 事件處理常式之後，新增 `CheckOutBtn_Click` 事件處理常式：  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample17.cs)]
5. 此外，在*ShoppingCart.aspx.cs*檔案中，新增 `CheckoutBtn`的參考，以便參考新的影像按鈕，如下所示：  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample18.cs?highlight=18)]
6. 將您的變更儲存至*ShoppingCart .aspx*檔案和*ShoppingCart.aspx.cs*檔案。
7. 從功能表中，選取  **Debug**- &gt;**組建 WingtipToys**。  
   專案會以新加入的**ImageButton**控制項重建。

### <a name="send-purchase-details-to-paypal"></a>將購買詳細資料傳送至 PayPal

當使用者按一下 [購物車] 頁面（*ShoppingCart .aspx*）上的 [**結帳**] 按鈕時，他們會開始購買程式。 下列程式碼會呼叫購買產品所需的第一個 PayPal 函數。

1. 從 [*簽出*] 資料夾中，開啟名為*CheckoutStart.aspx.cs*的程式碼後置檔案。   
   請務必開啟程式碼後置檔案。
2. 將現有的程式碼取代為下列程式碼：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample19.cs)]

當應用程式的使用者按一下 [購物車] 頁面上的 [**結帳**] 按鈕時，瀏覽器將會流覽至 [ *CheckoutStart* ] 頁面。 當*CheckoutStart .aspx*頁面載入時，會呼叫 `ShortcutExpressCheckout` 方法。 此時，使用者會轉移至 PayPal 測試網站。 在 PayPal 網站上，使用者輸入其 PayPal 認證、審查購買詳細資料、接受 PayPal 合約，然後回到 `ShortcutExpressCheckout` 方法完成的 Wingtip 玩具範例應用程式。 當 `ShortcutExpressCheckout` 方法完成時，它會將使用者重新導向至 `ShortcutExpressCheckout` 方法中指定的*CheckoutReview .aspx*頁面。 這可讓使用者從 Wingtip 玩具範例應用程式中，檢查訂單詳細資料。

### <a name="review-order-details"></a>審核順序詳細資料

從 PayPal 傳回之後，Wingtip 玩具範例應用程式的 [ *CheckoutReview* ] 頁面會顯示訂單詳細資料。 此頁面可讓使用者在購買產品前，先檢查訂單詳細資料。 *CheckoutReview*的建立方式必須如下所示：

1. 在 [*簽出*] 資料夾中，開啟名為*CheckoutReview*的頁面。
2. 以下列內容取代現有的標記：   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample20.aspx)]
3. 開啟名為*CheckoutReview.aspx.cs*的程式碼後置頁面，並將現有的程式碼取代為下列內容：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample21.cs)]

**DetailsView**控制項是用來顯示已從 PayPal 傳回的訂單詳細資料。 此外，上述程式碼也會將訂單詳細資料儲存至 Wingtip 玩具資料庫，做為 `OrderDetail` 物件。 當使用者按一下 [**完成訂單**] 按鈕時，系統會將他們重新導向至*CheckoutComplete .aspx*頁面。

> [!NOTE] 
> 
> **秘訣**
> 
> 請注意，在*CheckoutReview*的標記中，會使用 `<ItemStyle>` 標記來變更**DetailsView**控制項（接近頁面底部）中的專案樣式。 藉由在 [**設計檢視**] 中查看頁面（在 Visual Studio 的左下角選取 [**設計**]），然後選取 [ **DetailsView** ] 控制項，然後選取 [**智慧標籤**] （控制項右上方的箭號圖示），您就能夠看到**DetailsView**工作。
> 
> ![使用 PayPal 簽出和付款-編輯欄位](checkout-and-payment-with-paypal/_static/image18.png)
> 
> 藉由選取 [**編輯欄位**]，將會顯示 [**欄位**] 對話方塊。 在此對話方塊中，您可以輕鬆地控制**DetailsView**控制項的視覺屬性，例如**ItemStyle**。
> 
> ![使用 PayPal-[欄位] 對話方塊簽出和付款](checkout-and-payment-with-paypal/_static/image19.png)

### <a name="complete-purchase"></a>完成購買

*CheckoutComplete .aspx*頁面會向 PayPal 購買。 如上所述，使用者必須按一下 [**完整訂單**] 按鈕，應用程式才會流覽至*CheckoutComplete .aspx*頁面。

1. 在 [*簽出*] 資料夾中，開啟名為*CheckoutComplete*的頁面。
2. 以下列內容取代現有的標記：   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample22.aspx)]
3. 開啟名為*CheckoutComplete.aspx.cs*的程式碼後置頁面，並將現有的程式碼取代為下列內容：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample23.cs)]

載入*CheckoutComplete .aspx*頁面時，會呼叫 `DoCheckoutPayment` 方法。 如先前所述，`DoCheckoutPayment` 方法會從 PayPal 測試環境完成購買。 一旦 PayPal 完成訂單的購買後，[ *CheckoutComplete* ] 頁面就會顯示購買者 `ID` 的付款交易。

### <a name="handle-cancel-purchase"></a>處理取消購買

如果使用者決定取消購買，他們會被導向至 [ *CheckoutCancel* ] 頁面，他們會看到他們的訂單已取消。

1. 在 [*簽出*] 資料夾中，開啟名為*CheckoutCancel*的頁面。
2. 以下列內容取代現有的標記：   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample24.aspx)]

### <a name="handle-purchase-errors"></a>處理購買錯誤

在購買程式期間的錯誤將由*CheckoutError*處理。 *CheckoutStart*的程式碼後置、 *CheckoutReview*頁面和*CheckoutComplete*頁面會在發生錯誤時，每個都會重新導向至*CheckoutError .aspx*頁面。

1. 在 [*簽出*] 資料夾中，開啟名為*CheckoutError*的頁面。
2. 以下列內容取代現有的標記：   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample25.aspx)]

當簽出程式期間發生錯誤時，會顯示 [ *CheckoutError* ] 頁面，其中包含錯誤詳細資料。

## <a name="running-the-application"></a>執行應用程式

執行應用程式，以瞭解如何購買產品。 請注意，您將會在 PayPal 測試環境中執行。 不會交換實際的金錢。

1. 請確定所有檔案都儲存在 Visual Studio 中。
2. 開啟網頁瀏覽器，並流覽至[https://developer.paypal.com](https://developer.paypal.com/)。
3. 使用您稍早在本教學課程中建立的 PayPal 開發人員帳戶登入。  
   對於 PayPal 的開發人員沙箱，您必須在[https://developer.paypal.com](https://developer.paypal.com/)登入，以測試快速簽出。 這僅適用于 PayPal 的沙箱測試，而不適用於 PayPal 的即時環境。
4. 在 Visual Studio 中，按**F5**執行 Wingtip 玩具範例應用程式。  
   重建資料庫之後，瀏覽器將會開啟並顯示*default.aspx*頁面。
5. 藉由選取產品類別（例如「汽車」），然後按一下每個產品旁的 [**新增至購物車**]，將三個不同的產品新增至購物車。  
   購物車會顯示您所選取的產品。
6. 按一下 [ **PayPal** ] 按鈕以簽出。 

    ![使用 PayPal 的結帳和付款-購物車](checkout-and-payment-with-paypal/_static/image20.png)

   簽出將會要求您必須擁有 Wingtip 玩具範例應用程式的使用者帳戶。
7. 按一下頁面右側的 [ **Google** ] 連結，以使用現有的 gmail.com 電子郵件帳戶登入。  
   如果您沒有 gmail.com 帳戶，可以在[www.gmail.com](https://www.gmail.com/)建立一個用於測試的用途。 您也可以按一下 [註冊]，以使用標準的本機帳戶。 

    ![簽出與使用 PayPal 付款-登入](checkout-and-payment-with-paypal/_static/image21.png)
8. 使用您的 gmail 帳戶和密碼登入。 

    ![使用 PayPal 進行簽出和付款-Gmail 登入](checkout-and-payment-with-paypal/_static/image22.png)
9. 按一下 [**登入**] 按鈕，向您的 Wingtip 玩具範例應用程式使用者名稱註冊您的 gmail 帳戶。 

    ![使用 PayPal 簽出和付款-註冊帳戶](checkout-and-payment-with-paypal/_static/image23.png)
10. 在 PayPal 測試網站上，新增您稍早在本教學課程中建立的**買方**電子郵件地址和密碼，然後按一下 [**登入**] 按鈕。 

    ![使用 PayPal 簽出和付款-PayPal 登入](checkout-and-payment-with-paypal/_static/image24.png)
11. 同意 PayPal 原則，然後按一下 [**同意並繼續**] 按鈕。  
    請注意，只有當您第一次使用此 PayPal 帳戶時，才會顯示此頁面。 同樣地，請注意這是測試帳戶，並不會交換真正的金錢。 

    ![使用 PayPal 簽出和付款-PayPal 原則](checkout-and-payment-with-paypal/_static/image25.png)
12. 請參閱 PayPal 測試環境審查頁面上的訂單資訊，然後按一下 [**繼續**]。 

    ![簽出與使用 PayPal 的款項-審查資訊](checkout-and-payment-with-paypal/_static/image26.png)
13. 在 [ *CheckoutReview* ] 頁面上，確認訂單金額，並查看產生的寄送位址。 然後，按一下 [**完成訂單**] 按鈕。 

    ![使用 PayPal-訂單審查簽出和付款](checkout-and-payment-with-paypal/_static/image27.png)
14. 隨即會顯示 [ **CheckoutComplete** ] 頁面，其中包含付款交易識別碼。 

    ![使用 PayPal 簽出和付款-結帳完成](checkout-and-payment-with-paypal/_static/image28.png)

<a id="ReviewDBWebForms"></a>
## <a name="reviewing-the-database"></a>檢查資料庫

在執行應用程式後，藉由在 Wingtip 玩具範例應用程式資料庫中查看更新的資料，您可以看到應用程式已成功記錄產品的購買。

您可以使用 [**資料庫總管**] 視窗（Visual Studio 中的 [**伺服器總管**] 視窗），檢查*Wingtiptoys*中包含的資料，就像您先前在本教學課程系列中所做的一樣。

1. 如果瀏覽器視窗仍為開啟狀態，請將它關閉。
2. 在 Visual Studio 中，選取**方案總管**頂端的 [**顯示所有**檔案] 圖示，以讓您展開**應用程式\_** 資料夾。
3. 展開**應用程式\_[Data** ] 資料夾。  
 您可能需要選取資料夾的 [**顯示所有**檔案] 圖示。
4. 以滑鼠右鍵按一下*Wingtiptoys .mdf*資料庫檔案，然後選取 [**開啟**]。  
    隨即顯示 [**伺服器總管**]。
5. 展開 **[資料表]** 資料夾。
6. 以滑鼠右鍵按一下**Orders**資料表，然後選取 [**顯示資料表資料**]。  
 [**訂單**] 資料表隨即顯示。
7. 檢查**PaymentTransactionID**資料行以確認交易成功。 

    ![簽出和付款使用 PayPal-審核資料庫](checkout-and-payment-with-paypal/_static/image29.png)
8. 關閉 [ **Orders** ] 資料表視窗。
9. 在 伺服器總管中，以滑鼠右鍵按一下**OrderDetails**資料表，然後選取 **顯示資料表資料**。
10. 檢查**OrderDetails**資料表中的 `OrderId` 和 `Username` 值。 請注意，這些值符合**Orders**資料表中包含的 `OrderId` 和 `Username` 值。
11. 關閉 [ **OrderDetails**資料表] 視窗。
12. 以滑鼠右鍵按一下 Wingtip 玩具資料庫檔案（*Wingtiptoys .mdf*），然後選取 [**關閉連接**]。
13. 如果您看不到 **方案總管** 視窗，請按一下 **伺服器總管** 視窗底部的 **方案總管**，再次顯示**方案總管**。

## <a name="summary"></a>總結

在本教學課程中，您已新增訂單和訂單詳細資料架構來追蹤產品的購買。 您也可以將 PayPal 功能整合到 Wingtip 玩具範例應用程式中。

## <a name="additional-resources"></a>其他資源

[ASP.NET 設定總覽](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)  
[將具有成員資格、OAuth 和 SQL Database 的安全 ASP.NET Web Forms 應用程式部署至 Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)

## <a name="disclaimer"></a>免責聲明

本教學課程包含範例程式碼。 這類範例程式碼是以「原樣」提供，不含任何種類的擔保。 因此，Microsoft 不保證範例程式碼的精確度、完整性或品質。 您同意以自己的風險使用範例程式碼。 在任何情況下，Microsoft 不會針對任何範例程式碼、內容（包括但不限於任何範例程式碼、內容，或任何因使用任何範例程式碼而產生的任何類型遺失或損毀），以任何方式對您造成任何問題。 您將會收到通知，並據此同意補償、儲存及保存 Microsoft 免于任何遺失的損害、遺失的索賠、傷害或任何種類的損害，包括或因您張貼的資料而產生的 occasioned、傳輸、使用或依賴包含（但不限於）其中所表示的觀點。

> [!div class="step-by-step"]
> [上一頁](shopping-cart.md)
> [下一頁](membership-and-administration.md)
