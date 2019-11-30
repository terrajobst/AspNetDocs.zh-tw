---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
title: 建立資料存取層 |Microsoft Docs
author: Erikre
description: 本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 為我們建立 ASP.NET Web Forms 應用程式的基本概念 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 0bbf7a6e-d7eb-4091-91e4-fff892777f32
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
msc.type: authoredcontent
ms.openlocfilehash: 0fcf050474a57be9ed53ec0783a6d6b7dde2bf4c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575756"
---
# <a name="create-the-data-access-layer"></a>建立資料存取層

依[Erik Reitan](https://github.com/Erikre)

[下載 Wingtip 玩具範例專案（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下載電子書（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 建立 ASP.NET Web Forms 應用程式的基本概念。 本教學課程系列隨附有[ C#原始程式碼](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 專案。

本教學課程說明如何使用 ASP.NET Web Forms 和 Entity Framework Code First，從資料庫建立、存取和審核資料。 本教學課程是以上一個教學課程「建立專案」為基礎，屬於 Wingtip 玩具商店教學課程系列。 當您完成本教學課程時，您將會在專案的 [*模型*] 資料夾中，建立一組資料存取類別。

## <a name="what-youll-learn"></a>您將瞭解的內容：

- 如何建立資料模型。
- 如何初始化和植入資料庫。
- 如何更新及設定應用程式以支援資料庫。

### <a name="these-are-the-features-introduced-in-the-tutorial"></a>這些是教學課程中引進的功能：

- Entity Framework Code First
- LocalDB
- 資料註釋

## <a name="creating-the-data-models"></a>建立資料模型

[Entity Framework](https://msdn.microsoft.com/data/aa937723)是物件關聯式對應（ORM）架構。 它可讓您以物件的形式使用關聯式資料，以排除通常需要撰寫的大部分資料存取程式碼。 使用 Entity Framework，您可以使用[LINQ](https://msdn.microsoft.com/library/bb397926.aspx)發出查詢，然後將資料當作強型別物件來取得和操作。 LINQ 提供查詢和更新資料的模式。 使用 Entity Framework 可讓您專注于建立應用程式的其餘部分，而不是專注于資料存取基本概念。 稍後在本教學課程系列中，我們將示範如何使用資料來填入導覽和產品查詢。

Entity Framework 支援稱為*Code First*的開發範例。 Code First 可讓您使用類別來定義您的資料模型。 類別是一種結構，可讓您將其他類型、方法和事件的變數群組在一起，以建立您自己的自訂類型。 您可以將類別對應至現有的資料庫，或使用它們來產生資料庫。 在本教學課程中，您將藉由撰寫資料模型類別來建立資料模型。 然後，您可以讓 Entity Framework 從這些新的類別即時建立資料庫。

首先，您會建立定義 Web form 應用程式之資料模型的實體類別。 接著，您將建立一個內容類別來管理實體類別，並提供資料庫的資料存取權。 您也會建立將用來填入資料庫的初始化運算式類別。

### <a name="entity-framework-and-references"></a>Entity Framework 和參考

根據預設，當您使用**Web Forms**範本建立新的**ASP.NET Web 應用程式**時，會包含 Entity Framework。 Entity Framework 可以安裝、卸載及更新為 NuGet 套件。

此 NuGet 套件包含您專案內的下列**運行**時間元件：

- EntityFramework-Entity Framework 使用的所有通用執行時間程式碼
- EntityFramework-Entity Framework 的 Microsoft SQL Server 提供者

### <a name="entity-classes"></a>實體類別

您建立用來定義資料架構的類別稱為「實體類別」（entity class）。 如果您不熟悉資料庫設計，請將實體類別視為資料庫的資料表定義。 類別中的每個屬性都會在資料庫的資料表中指定一個資料行。 這些類別會在物件導向程式碼與資料庫的關聯式資料表結構之間，提供輕量的物件關聯式介面。

在本教學課程中，您將從新增代表產品和類別架構的簡單實體類別開始。 Products 類別將包含每個產品的定義。 Product 類別的每個成員名稱將會是 `ProductID`、`ProductName`、`Description`、`ImagePath`、`UnitPrice`、`CategoryID`和 `Category`。 Category 類別將包含產品可屬於之每個類別的定義，例如汽車、船或平面。 Category 類別的每個成員名稱將會是 `CategoryID`、`CategoryName`、`Description`和 `Products`。 每個產品都屬於其中一個類別。 這些實體類別會加入至專案的 [現有*模型*] 資料夾。

1. 在**方案總管**中，以滑鼠右鍵按一下 [*模型*] 資料夾，**然後選取 [** 新增 -&gt;**新專案**]。 

    ![建立資料存取層-新增專案功能表](create_the_data_access_layer/_static/image1.png)

   隨即顯示 [ 新增項目] 對話方塊。
2. 在左側 [**已安裝**] 窗格中的 [**視覺效果C#**  ] 底下，選取 [程式**代碼**]。 

    ![建立資料存取層-新增專案功能表](create_the_data_access_layer/_static/image2.png)
3. 從中間窗格選取 [**類別**]，並將此新類別命名為*Product.cs*。
4. 按一下 [加入]。  
   新的類別檔案會顯示在編輯器中。
5. 將預設程式碼取代為下列程式碼：   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample1.cs)]
6. 重複步驟1到4來建立另一個類別，不過，將新類別命名為*Category.cs* ，並將預設程式碼取代為下列程式碼：  

    [!code-csharp[Main](create_the_data_access_layer/samples/sample2.cs)]

如先前所述，`Category` 類別代表應用程式設計用來銷售的產品類型（例如<a id="a"></a>&quot;Cars&quot;、&quot;Boats&quot;、&quot;Rockets&quot;等等），而 `Product` 類別則代表資料庫中的個別產品（玩具）。 `Product` 物件的每個實例都會對應到關係資料庫資料表中的一個資料列，而 Product 類別的每個屬性都會對應到關係資料庫資料表中的資料行。 稍後在本教學課程中，您將會檢查資料庫中包含的產品資料。

### <a name="data-annotations"></a>資料註釋

您可能已經注意到，類別的某些成員有屬性指定成員的詳細資料，例如 `[ScaffoldColumn(false)]`。 這些是*資料批註*。 資料批註屬性可以描述如何驗證該成員的使用者輸入、指定其格式，以及指定在建立資料庫時模型化的方式。

### <a name="context-class"></a>Context 類別

若要開始使用類別進行資料存取，您必須定義內容類別。 如先前所述，內容類別會管理實體類別（例如 `Product` 類別和 `Category` 類別），並提供資料庫的資料存取權。

此程式會將新C#的內容類別加入至 [*模型*] 資料夾。

1. 以滑鼠右鍵按一下 [*模型*] 資料夾，**然後選取 [** 新增 -&gt;**新專案**]。   
   隨即顯示 [ 新增項目] 對話方塊。
2. 從中間窗格選取 [**類別**]，將其命名為*ProductCoNtext.cs* ，然後按一下 [**新增**]。
3. 將包含在類別中的預設程式碼取代為下列程式碼：   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample3.cs)]

這段程式碼會加入 `System.Data.Entity` 命名空間，讓您可以存取 Entity Framework 的所有核心功能，其中包括使用強型別物件來查詢、插入、更新和刪除資料的功能。

`ProductContext` 類別代表 Entity Framework 的產品資料庫內容，它會處理資料庫中 `Product` 類別實例的提取、儲存和更新。 `ProductContext` 類別衍生自 Entity Framework 所提供的 `DbContext` 基類。

### <a name="initializer-class"></a>初始化運算式類別

您必須在第一次使用內容時，執行一些自訂邏輯來初始化資料庫。 這可讓植入資料新增至資料庫，讓您可以立即顯示產品和類別。

此程式會將新C#的初始化運算式類別加入至 [*模型*] 資料夾。

1. 在 [*模型*] 資料夾中建立另一個 `Class`，並將其命名為*ProductDatabaseInitializer.cs*。
2. 將包含在類別中的預設程式碼取代為下列程式碼：   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample4.cs)]

如您在上述程式碼中所見，當建立並初始化資料庫時，會覆寫並設定 `Seed` 屬性。 設定 [`Seed`] 屬性時，會使用類別和產品的值來填入資料庫。 如果您嘗試在建立資料庫之後修改上述程式碼來更新種子資料，當您執行 Web 應用程式時，將不會看到任何更新。 原因是上述程式碼會使用 `DropCreateDatabaseIfModelChanges` 類別的執行來辨識模型（架構）在重設種子資料之前是否已經變更。 如果 `Category` 和 `Product` 實體類別不會進行任何變更，則不會以種子資料重新初始化資料庫。

> [!NOTE] 
> 
> 如果您想要在每次執行應用程式時重新建立資料庫，您可以使用 `DropCreateDatabaseAlways` 類別，而不是 `DropCreateDatabaseIfModelChanges` 類別。 不過，在此教學課程系列中，請使用 `DropCreateDatabaseIfModelChanges` 類別。

此時，在本教學課程中，您將會有一個 [*模型*] 資料夾，其中包含四個新類別和一個預設類別：

![建立資料存取層-模型資料夾](create_the_data_access_layer/_static/image3.png)

### <a name="configuring-the-application-to-use-the-data-model"></a>設定應用程式以使用資料模型

現在您已建立代表資料的類別，您必須將應用程式設定為使用類別。 在*global.asax*檔案中，您可以加入初始化模型的程式碼。 在 web.config*檔案*中，您可以新增資訊，告訴應用程式您將用來儲存新資料類別所表示之資料的資料庫。 *Global.asax*檔案可以用來處理應用程式事件或方法。 Web.config*檔案*可讓您控制 ASP.NET Web 應用程式的設定。

#### <a name="updating-the-globalasax-file"></a>更新 global.asax 檔案

若要在應用程式啟動時初始化資料模型，您將會更新*Global.asax.cs*檔中的 `Application_Start` 處理常式。

> [!NOTE] 
> 
> 在方案總管中，您可以選取*global.asax*檔案或*Global.asax.cs*檔案，以編輯*Global.asax.cs*檔案。

1. 將下列以黃色反白顯示的程式碼新增至*Global.asax.cs*檔案中的 `Application_Start` 方法。   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample5.cs?highlight=9-10,22-23)]

> [!NOTE] 
> 
> 在瀏覽器中觀看此教學課程系列時，您的瀏覽器必須支援 HTML5 來觀看以黃色醒目提示的程式碼。

如上述程式碼所示，當應用程式啟動時，應用程式會指定第一次存取資料時要執行的初始化運算式。 需要兩個額外的命名空間，才能存取 `Database` 物件和 `ProductDatabaseInitializer` 物件。

 修改 Web.config 檔案 

雖然 Entity Framework Code First 會在資料庫填入種子資料時，于預設位置為您產生資料庫，但將您自己的連接資訊新增至您的應用程式，可讓您控制資料庫位置。 您可以使用專案根目錄之應用*程式 web.config 檔案*中的連接字串，來指定這個資料庫連接。 藉由加入新的連接字串，您可以將資料庫（*wingtiptoys*）的位置導向至應用程式的資料目錄（*應用程式\_資料*），而不是其預設位置。 進行這項變更可讓您在本教學課程稍後尋找及檢查資料庫檔案。

1. 在**方案總管**中，尋找並開啟*web.config 檔案*。
2. 將以黃色反白顯示的連接字串加入*web.config*檔案的 `<connectionStrings>` 區段，如下所示：  

    [!code-xml[Main](create_the_data_access_layer/samples/sample6.xml?highlight=4-7)]

第一次執行應用程式時，它會在連接字串所指定的位置上建立資料庫。 但在執行應用程式之前，讓我們先建立它。

## <a name="building-the-application"></a>建置應用程式

若要確定您的 Web 應用程式的所有類別和變更都能正常執行，您應該建立應用程式。

1. 從 [**調試**] 功能表中，選取 [**組建 WingtipToys**]。  
 [**輸出**] 視窗隨即顯示，如果一切順利，您就會看到 [*成功*] 訊息。  

    ![建立資料存取層-輸出視窗](create_the_data_access_layer/_static/image4.png)

如果您遇到錯誤，請重新檢查上述步驟。 [**輸出**] 視窗中的資訊會指出有問題的檔案，以及檔案中需要變更的位置。 這項資訊可讓您判斷在您的專案中，必須檢查和修正上述步驟的哪個部分。

## <a name="summary"></a>總結

在此系列的本教學課程中，您已建立資料模型，以及新增將用來初始化和植入資料庫的程式碼。 您也已將應用程式設定為在應用程式執行時使用資料模型。

在下一個教學課程中，您將更新 UI、加入導覽，以及從資料庫中取出資料。 這會導致根據您在本教學課程中建立的實體類別自動建立資料庫。

## <a name="additional-resources"></a>其他資源

[Entity Framework 總覽](https://msdn.microsoft.com/library/bb399567.aspx)   
[ADO.NET Entity Framework 的初學者指南](https://msdn.microsoft.com/data/ee712907)   
[使用 Entity Framework 進行 Code First 開發](http://www.msteched.com/2010/Europe/DEV212)（影片）   
[Code First 關聯性流暢的 API](https://msdn.microsoft.com/data/hh134698)   
[Code First 資料批註](https://msdn.microsoft.com/data/gg193958)  
[Entity Framework 的生產力改善](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)

> [!div class="step-by-step"]
> [上一頁](create-the-project.md)
> [下一頁](ui_and_navigation.md)
