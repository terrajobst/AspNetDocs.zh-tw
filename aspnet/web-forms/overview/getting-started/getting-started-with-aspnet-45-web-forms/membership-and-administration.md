---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/membership-and-administration
title: 成員資格和管理 |Microsoft Docs
author: Erikre
description: 本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 為我們建立 ASP.NET Web Forms 應用程式的基本概念 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 732a2316-e49f-4f72-becd-0cd72f14457e
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/membership-and-administration
msc.type: authoredcontent
ms.openlocfilehash: ab00bc90bfc767d06e747be6dfb973245b5aae88
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615463"
---
# <a name="membership-and-administration"></a>成員資格及系統管理

依[Erik Reitan](https://github.com/Erikre)

[下載 Wingtip 玩具範例專案（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下載電子書（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 建立 ASP.NET Web Forms 應用程式的基本概念。 本教學課程系列隨附有[ C#原始程式碼](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 專案。

本教學課程說明如何更新 Wingtip 玩具範例應用程式，以新增自訂角色並使用 ASP.NET Identity。 它也會示範如何執行系統管理頁面，其中具有自訂角色的使用者可以從網站新增和移除產品。

[ASP.NET Identity](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md)是用來建立 ASP.NET web 應用程式的成員資格系統，並可在 ASP.NET 4.5 中取得。 ASP.NET Identity 用於 Visual Studio 2013 Web form 專案範本，以及用來[ASP.NET MVC](../../../../mvc/index.md)、 [ASP.NET Web API](../../../../web-api/index.md)和[ASP.NET 單一頁面應用程式](../../../../single-page-application/index.md)的範本。 當您開始使用空白 Web 應用程式時，也可以使用 NuGet 來特別安裝 ASP.NET Identity 系統。 不過，在本教學課程系列中，您會使用**Web Forms**projecttemplate，其中包含 ASP.NET Identity 系統。 ASP.NET Identity 可讓您輕鬆地整合使用者特定的設定檔資料與應用程式資料。 此外，ASP.NET Identity 可讓您選擇應用程式中使用者設定檔的持續性模型。 您可以將資料儲存在 SQL Server 資料庫或其他資料存放區中，包括*NoSQL*資料存放區，例如 Windows Azure 儲存體資料表。

本教學課程是以先前的教學課程為基礎，在 Wingtip 玩具教學課程系列中的「簽出與使用 PayPal 付款」。

## <a name="what-youll-learn"></a>您將瞭解的內容：

- 如何使用程式碼將自訂角色和使用者新增至應用程式。
- 如何限制對管理資料夾和頁面的存取。
- 如何為屬於自訂角色的使用者提供導覽。
- 如何使用模型系結來填入具有產品類別目錄的[DropDownList](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist(v=vs.110).aspx)控制項。
- 如何使用[FileUpload](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload(v=vs.110).aspx)控制項將檔案上傳至 web 應用程式。
- 如何使用驗證控制項來執行輸入驗證。
- 如何在應用程式中新增和移除產品。

## <a name="these-features-are-included-in-the-tutorial"></a>這些功能包含在教學課程中：

- ASP.NET Identity
- 設定和授權
- 模型繫結
- 不顯眼的驗證

ASP.NET Web Forms 提供成員資格功能。 藉由使用預設範本，您可以在應用程式執行時立即使用內建的成員資格功能。 本教學課程說明如何使用 ASP.NET Identity 新增自訂角色，並將使用者指派給該角色。 您將瞭解如何限制系統管理資料夾的存取權。 您將會在 [系統管理] 資料夾中新增一個頁面，讓具有自訂角色的使用者新增和移除產品，以及在新增產品後進行預覽。

## <a name="adding-a-custom-role"></a>新增自訂角色

使用 ASP.NET Identity，您可以加入自訂角色，並使用程式碼將使用者指派給該角色。

1. 在**方案總管**中，以滑鼠右鍵按一下*邏輯*資料夾，然後建立新的類別。
2. 將新類別命名為*RoleActions.cs*。
3. 修改程式碼，使其看起來如下所示：  

    [!code-csharp[Main](membership-and-administration/samples/sample1.cs?highlight=8)]
4. 在**方案總管**中，開啟*Global.asax.cs*檔案。
5. 藉由新增黃色反白顯示的程式碼來修改*Global.asax.cs*檔案，讓它看起來如下所示：  

    [!code-csharp[Main](membership-and-administration/samples/sample2.cs?highlight=11,26-28)]
6. 請注意，`AddUserAndRole` 會以紅色加上底線。 按兩下 [AddUserAndRole] 程式碼。  
   反白顯示方法開頭的字母 "A" 會加上底線。
7. 將滑鼠停留在字母 "A" 上，然後按一下 UI，讓您為 `AddUserAndRole` 方法產生方法 stub。 

    ![成員資格和管理-產生方法 Stub](membership-and-administration/_static/image1.png)
8. 按一下標題為的選項：  
    `Generate method stub for "AddUserAndRole" in "WingtipToys.Logic.RoleActions"`
9. 從*邏輯*資料夾中開啟*RoleActions.cs*檔案。  
   `AddUserAndRole` 方法已新增至類別檔案。
10. 移除 `NotImplementedException` 並新增以黃色反白顯示的程式碼，以修改*RoleActions.cs*檔，使其看起來如下所示：  

    [!code-csharp[Main](membership-and-administration/samples/sample3.cs?highlight=5-7,15-51)]

上述程式碼會先建立成員資格資料庫的資料庫內容。 成員資格資料庫也會儲存為*應用程式\_Data*資料夾中的 *.mdf*檔案。 當第一位使用者登入此 web 應用程式之後，您就能夠看到此資料庫。 

> [!NOTE] 
> 
> 如果您想要儲存成員資格資料和產品資料，您可以考慮使用您用來在上述程式碼中儲存產品資料的相同**DbCoNtext** 。

 *Internal*關鍵字是類型（例如類別）和類型成員（例如方法或屬性）的存取修飾詞。 內部類型或成員只能在包含于相同元件 *（.dll*檔案）中的檔案內進行存取。 當您建立應用程式時，會建立元件檔 *（.dll*），其中包含執行應用程式時所執行的程式碼。 

提供角色管理的 `RoleStore` 物件會根據資料庫內容來建立。

> [!NOTE] 
> 
> 請注意，建立 `RoleStore` 物件時，它會使用泛型 `IdentityRole` 類型。 這表示 `RoleStore` 只允許包含 `IdentityRole` 物件。 此外，藉由使用泛型，記憶體中的資源會以更好的方式處理。

接下來，會根據您剛才建立的 `RoleStore` 物件來建立 `RoleManager` 物件。 `RoleManager` 物件會公開角色相關的 API，可用來自動將變更儲存至 `RoleStore`。 `RoleManager` 只允許包含 `IdentityRole` 物件，因為程式碼會使用 `<IdentityRole>` 的泛型型別。

您可以呼叫 `RoleExists` 方法，判斷成員資格資料庫中是否有 "canEdit" 角色。 如果不是，您可以建立角色。

建立 `UserManager` 物件比 `RoleManager` 控制項更複雜，但幾乎相同。 它只會在一行上進行編碼，而不是數個。 在這裡，您要傳遞的參數會具現化為括弧中包含的新物件。

接下來，建立新的 `ApplicationUser` 物件來建立 "canEditUser" 使用者。 然後，如果您成功建立使用者，請將使用者新增至新角色。

> [!NOTE] 
> 
> 錯誤處理將會在本教學課程系列稍後的「ASP.NET 錯誤處理」教學課程中更新。

下次應用程式啟動時，名為 "canEditUser" 的使用者會新增為應用程式名稱為 "canEdit" 的角色。 稍後在本教學課程中，您將以「canEditUser」使用者的身分登入，以顯示您將在本教學課程中新增的其他功能。 如需有關 ASP.NET Identity 的 API 詳細資料，請參閱[Microsoft AspNet. Identity 命名空間](https://msdn.microsoft.com/library/microsoft.aspnet.identity(v=vs.111).aspx)。 如需有關初始化 ASP.NET Identity 系統的其他詳細資訊，請參閱[AspnetIdentitySample](https://github.com/rustd/AspnetIdentitySample/blob/master/AspnetIdentitySample/App_Start/IdentityConfig.cs)。

### <a name="restricting-access-to-the-administration-page"></a>限制系統管理頁面的存取權

Wingtip 玩具範例應用程式可讓匿名使用者和已登入的使用者查看和購買產品。 不過，具有自訂 "canEdit" 角色的登入使用者可以存取受限制的頁面，以便新增和移除產品。

#### <a name="add-an-administration-folder-and-page"></a>新增系統管理資料夾和頁面

接下來，您將為屬於 Wingtip 玩具範例應用程式自訂角色的 "canEditUser" 使用者建立名為*Admin*的資料夾。

1. 在**方案總管**中，以滑鼠右鍵按一下專案名稱（**Wingtip 玩具**），**然後選取 [** 新增 -&gt;**新資料夾**]。
2. 將新資料夾命名為*Admin*。
3. 在 [系統*管理*] 資料夾上按一下滑鼠右鍵，**然後選取 [** 新增 -&gt;**新專案**]。   
   隨即顯示 [ 新增項目] 對話方塊。
4. 選取左側的 [ <strong>Visual C#</strong> -&gt; <strong>Web</strong>範本] 群組。 從中間清單中，選取 [<strong>具有主版的 Web 表單</strong>]，將它命名為<em>AdminPage .aspx</em><strong>，</strong>然後選取 [<strong>新增</strong>]。
5. 選取*網站*檔案作為主版頁面，然後選擇 **[確定]** 。

#### <a name="add-a-webconfig-file"></a>新增 Web.config 檔案

藉由將*web.config*檔案新增至*Admin*資料夾，您可以限制對資料夾中所含頁面的存取。

1. 以滑鼠右鍵按一下 [系統*管理*] 資料夾，**然後選取 [** 新增 -&gt;**新專案**]。  
   隨即顯示 [ 新增項目] 對話方塊。
2. 從C#視覺 web 範本清單中，從中間清單選取 [ <strong>web 設定檔</strong>]，接受 web.config 的預設名稱<strong>，然後</strong>選取 [<strong>新增</strong>]。
3. 將*web.config*檔案中的現有 XML 內容取代為下列各項：  

    [!code-xml[Main](membership-and-administration/samples/sample4.xml)]

儲存 web.config*檔案*。 Web.config*檔案*會指定只有屬於應用程式 "canEdit" 角色的使用者才能存取*Admin*資料夾中包含的頁面。

### <a name="including-custom-role-navigation"></a>包括自訂角色導覽

若要讓自訂 "canEdit" 角色的使用者流覽至應用程式的 [管理] 區段，您必須新增 [*網站*] 頁面的連結。 只有屬於 "canEdit" 角色的使用者才能夠看到系統**管理員**連結並存取 [管理] 區段。

1. 在方案總管中，尋找並開啟 [*網站*] 頁面。
2. 若要為 "canEdit" 角色的使用者建立連結，請將以黃色反白顯示的標記新增至下列未排序清單 `<ul>` 元素，讓清單顯示如下：  

    [!code-html[Main](membership-and-administration/samples/sample5.html?highlight=2-3)]
3. 開啟*Site.Master.cs*檔案。 將以黃色反白顯示的程式碼新增至 `Page_Load` 處理常式，讓系統**管理員**連結只對 "canEditUser" 使用者顯示。 `Page_Load` 處理常式將會如下所示：   

    [!code-csharp[Main](membership-and-administration/samples/sample6.cs?highlight=3-6)]

當頁面載入時，程式碼會檢查登入的使用者是否具有 "canEdit" 的角色。 如果使用者屬於 "canEdit" 角色，則會顯示包含*AdminPage*頁面連結的 span 元素（以及範圍內的連結）。

### <a name="enabling-product-administration"></a>啟用產品管理

到目前為止，您已建立「canEdit」角色，並新增了「canEditUser」使用者、「管理」資料夾和管理頁面。 您已設定 [系統管理] 資料夾和頁面的存取權限，並已將 "canEdit" 角色的使用者導覽連結新增至應用程式。 接下來，您會將標記加入至*AdminPage* ，並將程式碼新增至*AdminPage.aspx.cs*程式碼後置檔案，讓具有 "canEdit" 角色的使用者可以新增和移除產品。

1. 在**方案總管**中，從 [系統*管理*] 資料夾開啟*AdminPage .aspx*檔案。
2. 以下列內容取代現有的標記：  

    [!code-aspx[Main](membership-and-administration/samples/sample7.aspx)]
3. 接下來，開啟*AdminPage.aspx.cs*程式碼後置檔案，方法是以滑鼠右鍵按一下*AdminPage* ，然後按一下 [ **View code**]。
4. 將*AdminPage.aspx.cs*程式碼後置檔案中的現有程式碼取代為下列程式碼：  

    [!code-csharp[Main](membership-and-administration/samples/sample8.cs)]

在您為*AdminPage.aspx.cs*程式碼後置檔案輸入的程式碼中，名為 `AddProducts` 的類別會執行將產品新增至資料庫的實際工作。 此類別尚不存在，因此您現在將會建立它。

1. 在**方案總管**中，以滑鼠右鍵按一下*邏輯*資料夾，然後**選取 [** 新增 -&gt;**新專案**]。   
   隨即顯示 [ 新增項目] 對話方塊。
2. 選取左側的 [ **Visual C#**  -&gt; 程式**代碼**範本] 群組。 然後，從中間清單中選取 [**類別**]，並將其命名為*AddProducts.cs*。   
   隨即顯示新的類別檔案。
3. 將現有的程式碼取代為下列程式碼：  

    [!code-csharp[Main](membership-and-administration/samples/sample9.cs)]

*AdminPage*可以讓屬於 "canEdit" 角色的使用者新增和移除產品。 新增產品時，會驗證產品的詳細資料，然後將其輸入至資料庫。 新產品會立即提供給 web 應用程式的所有使用者使用。

#### <a name="unobtrusive-validation"></a>不顯眼的驗證

使用者在*AdminPage .aspx*頁面上提供的產品詳細資料，會使用驗證控制項（`RequiredFieldValidator` 和 `RegularExpressionValidator`）進行驗證。 這些控制項會自動使用不顯眼的驗證。 不顯眼的驗證可讓驗證控制項針對用戶端驗證邏輯使用 JavaScript，這表示頁面不需要通過伺服器的驗證。 根據預設，不顯眼的驗證會包含*在 web.config 檔案*中，以下列設定為基礎：

[!code-xml[Main](membership-and-administration/samples/sample10.xml)]

#### <a name="regular-expressions"></a>規則運算式

[ *AdminPage* ] 頁面上的產品價格會使用**RegularExpressionValidator**控制項進行驗證。 此控制項會驗證相關聯的輸入控制項值（"AddProductPrice" TextBox）是否符合正則運算式所指定的模式。 正則運算式是模式比對標記法，可讓您快速尋找並比對特定的字元模式。 **RegularExpressionValidator**控制項包含名為 `ValidationExpression` 的屬性，其中包含用來驗證價格輸入的正則運算式，如下所示：

[!code-aspx[Main](membership-and-administration/samples/sample11.aspx)]

#### <a name="fileupload-control"></a>FileUpload 控制項

除了 [輸入] 和 [驗證] 控制項以外，您還將**FileUpload**控制項新增至 [ *AdminPage* ] 頁面。 此控制項提供上傳檔案的功能。 在此情況下，您只允許上傳影像檔案。 在程式碼後置檔案（*AdminPage.aspx.cs*）中，按一下 `AddProductButton` 時，程式碼會檢查**FileUpload**控制項的 `HasFile` 屬性。 如果控制項有檔案，而且允許檔案類型（以副檔名為依據），則會將影像儲存至應用程式的*images*資料夾和*images/拇指*資料夾。

#### <a name="model-binding"></a>模型繫結

稍早在本教學課程中，您已使用模型系結來填入**ListView**控制項、 **FormsView**控制項、 **GridView**控制項和**detailview 之**控制項。 在本教學課程中，您會使用模型系結，以產品類別目錄清單填入**DropDownList**控制項。

您新增至*AdminPage .aspx*檔案的標記包含名為 `DropDownAddCategory`的**DropDownList**控制項：

[!code-aspx[Main](membership-and-administration/samples/sample12.aspx)]

您可以使用模型系結來填入這個**DropDownList** ，方法是設定 `ItemType` 屬性和 `SelectMethod` 屬性。 `ItemType` 屬性指定在填入控制項時使用 `WingtipToys.Models.Category` 類型。 您已在本教學課程系列的開頭定義此型別，方法是建立 `Category` 類別（如下所示）。 `Category` 類別位於*Category.cs*檔案內的 [*模型*] 資料夾中。

[!code-csharp[Main](membership-and-administration/samples/sample13.cs)]

**DropDownList**控制項的 `SelectMethod` 屬性會指定您使用程式碼後置檔案（*AdminPage.aspx.cs*）中所包含的 `GetCategories` 方法（如下所示）。

[!code-csharp[Main](membership-and-administration/samples/sample14.cs)]

這個方法會指定使用 `IQueryable` 介面來評估 `Category` 類型的查詢。 傳回的值會用來填入頁面標記中的**DropDownList** （*AdminPage .aspx*）。

針對清單中的每個專案所顯示的文字，是藉由設定 `DataTextField` 屬性來指定。 `DataTextField` 屬性會使用 `Category` 類別（如上所示）的 `CategoryName`，在**DropDownList**控制項中顯示每個類別目錄。 在**DropDownList**控制項中選取專案時所傳遞的實際值是以 `DataValueField` 屬性為基礎。 `DataValueField` 屬性會設定為 `CategoryID`，做為 `Category` 類別中的定義（如上所示）。

### <a name="how-the-application-will-work"></a>應用程式的工作方式

當屬於 "canEdit" 角色的使用者第一次流覽至頁面時，會如上面所述填入 `DropDownAddCategory`**DropDownList**控制項。 `DropDownRemoveProduct`**DropDownList**控制項也會使用相同的方法填入產品。 屬於 "canEdit" 角色的使用者會選取類別目錄類型，並新增產品詳細資料（**名稱**、**描述**、**價格**和**影像檔**案）。 當屬於 "canEdit" 角色的使用者按一下 [**加入產品**] 按鈕時，就會觸發 `AddProductButton_Click` 事件處理常式。 位於程式碼後置檔案（*AdminPage.aspx.cs*）中的 `AddProductButton_Click` 事件處理常式會檢查影像檔案，確認它符合允許的檔案類型 *（.gif*、 *.png*、 *jpeg*或 *.jpg*）。 然後，影像檔案會儲存到 Wingtip 玩具範例應用程式的資料夾中。 接下來，新的產品會新增至資料庫。 為了完成新產品的加入，會建立 `AddProducts` 類別的新實例，並將其命名為 products。 `AddProducts` 類別具有名為 `AddProduct`的方法，而 products 物件會呼叫這個方法，將產品加入至資料庫。

[!code-csharp[Main](membership-and-administration/samples/sample15.cs)]

如果程式碼成功將新產品加入至資料庫，則會使用查詢字串值 `ProductAction=add`重載該頁面。

[!code-csharp[Main](membership-and-administration/samples/sample16.cs)]

當頁面重載時，查詢字串會包含在 URL 中。 藉由重載頁面，屬於 "canEdit" 角色的使用者可以立即在*AdminPage*頁面上看到**DropDownList**控制項中的更新。 此外，藉由包含 URL 的查詢字串，頁面可以向屬於 "canEdit" 角色的使用者顯示成功訊息。

當*AdminPage 載入 .aspx*頁面時，會呼叫 `Page_Load` 事件。

[!code-csharp[Main](membership-and-administration/samples/sample17.cs)]

`Page_Load` 事件處理常式會檢查查詢字串值，並決定是否要顯示成功訊息。

## <a name="running-the-application"></a>執行應用程式

您可以立即執行應用程式，以瞭解如何在「購物車」中新增、刪除及更新專案。 購物車總計會反映購物車中所有專案的總成本。

1. 在方案總管中，按**F5**執行 Wingtip 玩具範例應用程式。  
   瀏覽器會開啟並顯示*default.aspx*頁面。
2. 按一下頁面頂端的 [**登入**] 連結。 

    ![成員資格和管理-登入連結](membership-and-administration/_static/image2.png)

   [*登入 .aspx* ] 頁面隨即顯示。
3. 使用下列使用者名稱和密碼：  
   使用者名稱： canEditUser@wingtiptoys.com  
   密碼： Pa $ $word 1 

    ![成員資格和管理-登入頁面](membership-and-administration/_static/image3.png)
4. 按一下靠近頁面底部的 [**登入**] 按鈕。
5. 在下一個頁面的頂端，選取 [**管理**] 連結以流覽至 [ *AdminPage* ] 頁面。 

    ![成員資格和管理-系統管理員連結](membership-and-administration/_static/image4.png)
6. 若要測試輸入驗證，請按一下 [**新增產品**] 按鈕，而不新增任何產品詳細資料。 

    ![成員資格和管理-系統管理頁面](membership-and-administration/_static/image5.png)

   請注意，會顯示必要的欄位訊息。
7. 新增新產品的詳細資料，然後按一下 [**新增產品**] 按鈕。 

    ![成員資格和管理-新增產品](membership-and-administration/_static/image6.png)
8. 從頂端導覽功能表中選取 [**產品**]，以查看您新增的新產品。 

    ![成員資格和管理-顯示新產品](membership-and-administration/_static/image7.png)
9. 按一下 [系統**管理員**] 連結以返回 [管理] 頁面。
10. 在頁面的 [**移除產品**] 區段中，選取您在**DropDownListBox**中新增的新產品。
11. 按一下 [**移除產品**] 按鈕，從應用程式中移除新的產品。 

    ![成員資格和管理-移除產品](membership-and-administration/_static/image8.png)
12. 從頂端導覽功能表中選取 [**產品**]，確認已移除產品。
13. 按一下 **[登出]** 以存在系統管理模式。   
    請注意，上方流覽窗格不會再顯示 [**管理**] 功能表項目。

## <a name="summary"></a>總結

在本教學課程中，您已新增自訂角色和屬於自訂角色的使用者、限制存取管理資料夾和頁面，並為屬於自訂角色的使用者提供導覽。 您已使用模型系結來填入具有資料的**DropDownList**控制項。 您已執行**FileUpload**控制項和驗證控制項。 此外，您也已瞭解如何從資料庫新增和移除產品。 在下一個教學課程中，您將瞭解如何執行 ASP.NET 路由。

## <a name="additional-resources"></a>其他資源

[Web.config-authorization 元素](https://msdn.microsoft.com/library/8d82143t(v=vs.100).aspx)  
[ASP.NET Identity](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md)  
[將具有成員資格、OAuth 和 SQL Database 的安全 ASP.NET Web Forms 應用程式部署至 Azure 網站](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> [上一頁](checkout-and-payment-with-paypal.md)
> [下一頁](url-routing.md)
