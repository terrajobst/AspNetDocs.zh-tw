---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
title: 顯示資料項目和詳細資料 |Microsoft Docs
author: Erikre
description: 本教學課程系列將示範如何使用 ASP.NET 4.7 和 Microsoft Visual Studio 2017 建立 ASP.NET Web Forms 應用程式的基本概念
ms.author: riande
ms.date: 1/04/2019
ms.assetid: 64a491a8-0ed6-4c2f-9c1c-412962eb6006
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
msc.type: authoredcontent
ms.openlocfilehash: 130c9ffd29df612dac5bb954830a2eb9b738aaf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641110"
---
# <a name="display-data-items-and-details"></a>顯示資料項目及詳細資料

依[Erik Reitan](https://github.com/Erikre)

> 本教學課程系列會教您使用 ASP.NET 4.7 和 Microsoft Visual Studio 2017 建立 ASP.NET Web Forms 應用程式的基本概念。

在本教學課程中，您將瞭解如何使用 ASP.NET Web Forms 和 Entity Framework Code First 來顯示資料項目和資料項目詳細資料。 本教學課程是以先前的「UI 和流覽」教學課程為基礎，做為 Wingtip 玩具商店教學課程系列的一部分。 完成本教學課程之後，您會在 [ *ProductsList* ] 頁面上看到產品，以及*ProductDetails*的產品詳細資料。

## <a name="youll-learn-how-to"></a>您將了解如何：

- 新增資料控制項以顯示資料庫中的產品
- 將資料控制項連接到選取的資料
- 新增資料控制項，以顯示資料庫中的產品詳細資料
- 從查詢字串抓取值，並使用該值來限制從資料庫抓取的資料

### <a name="features-introduced-in-this-tutorial"></a>本教學課程中引進的功能：

- 模型繫結
- 值提供者

## <a name="add-a-data-control"></a>新增資料控制項

您可以使用幾個不同的選項，將資料系結至伺服器控制項。 最常見的包括：

* 加入資料來源控制項
* 手動加入程式碼
* 使用模型系結

### <a name="use-a-data-source-control-to-bind-data"></a>使用資料來源控制項來系結資料

加入資料來源控制項可讓您將資料來源控制項連結至顯示資料的控制項。 透過這種方法，您可以用宣告方式（而不是以程式設計方式）將伺服器端控制項連接到資料來源。

### <a name="code-by-hand-to-bind-data"></a>手動撰寫程式碼以系結資料

手動撰寫程式碼包含：

1. 讀取值
2. 檢查其是否為 null
3. 將它轉換成適當的類型
4. 檢查轉換成功
5. 使用查詢中的值 

這種方法可讓您完全掌控您的資料存取邏輯。

### <a name="use-model-binding-to-bind-data"></a>使用模型系結來系結資料

模型系結可讓您以較少的程式碼來系結結果，並讓您能夠在整個應用程式中重複使用此功能。 它可簡化使用以程式碼為主的資料存取邏輯，同時仍然提供豐富的資料系結架構。

## <a name="display-products"></a>顯示產品

在本教學課程中，您將使用模型系結來系結資料。 若要將資料控制項設定為使用模型系結來選取資料，請將控制項的 `SelectMethod` 屬性設為頁面程式碼中的方法名稱。 資料控制項會在頁面生命週期的適當時間呼叫方法，並自動系結傳回的資料。 不需要明確地呼叫 `DataBind` 方法。

1. 在**方案總管**中，開啟*ProductList。*
2. 以下列標記取代現有標記：   

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample1.aspx)]

此程式碼會使用名為 `productList` 的**ListView**控制項來顯示產品。

[!code-aspx-csharp[Main](display_data_items_and_details/samples/sample2.aspx)]

使用範本和樣式，您可以定義**ListView**控制項顯示資料的方式。 這適用于任何重複結構中的資料。 雖然此**ListView**範例只會顯示資料庫資料，但您也可以不使用程式碼，讓使用者編輯、插入和刪除資料，以及排序和分頁資料。

藉由設定**ListView**控制項中的 [`ItemType`] 屬性，就可以使用資料系結運算式 `Item`，而且控制項會成為強型別。 如先前的教學課程中所述，您可以使用 IntelliSense 選取專案物件詳細資料，例如指定 `ProductName`：

![顯示資料項目和詳細資料-IntelliSense](display_data_items_and_details/_static/image1.png)

您也會使用模型系結來指定 `SelectMethod` 值。 這個值（`GetProducts`）會對應至您要新增至程式碼後置的方法，以在下一個步驟中顯示產品。

### <a name="add-code-to-display-products"></a>新增程式碼以顯示產品

在此步驟中，您將新增程式碼，以在**ListView**控制項中填入資料庫的產品資料。 此程式碼支援顯示所有產品和個別類別產品。

1. 在**方案總管**中，以滑鼠右鍵按一下 [ *ProductList* ]，然後選取 [ **View Code**]。
2. 將*ProductList.aspx.cs*檔案中的現有程式碼取代為下列內容：   

    [!code-csharp[Main](display_data_items_and_details/samples/sample3.cs)]

這段程式碼顯示**ListView**控制項的 `ItemType` 屬性在*ProductList*中參考的 `GetProducts` 方法。 若要將結果限制為特定的資料庫類別，程式碼會在流覽*ProductList .aspx*頁面時，從傳遞至*ProductList*的查詢字串值設定 `categoryId` 值。 `System.Web.ModelBinding` 命名空間中的 `QueryStringAttribute` 類別是用來抓取查詢字串變數 `id`的值。 這會指示模型系結嘗試在執行時間將值從查詢字串系結至 `categoryId` 參數。

當有效的類別目錄當做查詢字串傳遞至頁面時，查詢的結果會限制為資料庫中符合 `categoryId` 值的產品。 例如，如果*ProductsList .aspx*頁面 URL 為：

[!code-console[Main](display_data_items_and_details/samples/sample4.cmd)]

此頁面只會顯示 `categoryId` 等於 `1`的產品。

如果呼叫*ProductList .aspx*頁面時未包含任何查詢字串，則會顯示所有產品。

這些方法的值來源稱為*值提供*者（例如*QueryString*），而參數屬性會指出要使用的值提供者稱為*值提供者屬性*（例如 `id`）。 ASP.NET 包含 Web Forms 應用程式中所有一般使用者輸入來源的值提供者和對應屬性，例如查詢字串、cookie、表單值、控制項、檢視狀態、會話狀態和配置檔案屬性。 您也可以撰寫自訂值提供者。

### <a name="run-the-application"></a>執行應用程式

立即執行應用程式，以查看所有產品或類別的產品。

1. 在 Visual Studio 中按**F5**鍵，以執行應用程式。  
   瀏覽器會開啟並顯示*default.aspx*頁面。

2. 從 [產品類別] 流覽功能表中選取 [ **Cars** ]。  
   [ *ProductList* ] 頁面會顯示 [僅顯示**車輛**類別目錄] 產品。 稍後在本教學課程中，您將會顯示產品詳細資料。  

    ![顯示資料項目和詳細資料-Cars](display_data_items_and_details/_static/image2.png)

3. 從頂端的導覽功能表中，選取 [**產品**]。  
   同樣地， *ProductList*會顯示 [default.aspx] 頁面，不過這次它會顯示完整的產品清單。   

    ![顯示資料項目和詳細資料-產品](display_data_items_and_details/_static/image3.png)

4. 關閉瀏覽器並返回 Visual Studio。

### <a name="add-a-data-control-to-display-product-details"></a>新增資料控制項以顯示產品詳細資料

接下來，您將修改您在上一個教學課程中新增的*ProductDetails*頁面中的標記，以顯示特定的產品資訊。

1. 在**方案總管**中，開啟*ProductDetails。*

2. 以下列標記取代現有標記：

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample5.aspx)] 

    這段程式碼會使用**FormView**控制項來顯示特定的產品詳細資料。 此標記會使用方法，就像在*ProductList .aspx*頁面中用來顯示資料的方法一樣。 **FormView**控制項是用來一次從資料來源顯示單一記錄。 當您使用**FormView**控制項時，您會建立範本來顯示和編輯資料系結值。 這些範本包含控制項、系結運算式，以及定義表單外觀和功能的格式。

將先前的標記連接到資料庫需要額外的程式碼。

1. 在**方案總管**中，以滑鼠右鍵按一下 [ *ProductDetails* ]，然後按一下 [ **View Code**]。  
   隨即會顯示*ProductDetails.aspx.cs*檔案。

2. 使用下列程式碼取代現有的程式碼：   

    [!code-csharp[Main](display_data_items_and_details/samples/sample6.cs)]

此程式碼會檢查 "`productID`" 查詢字串值。 如果找到有效的查詢字串值，則會顯示相符的產品。 如果找不到查詢字串，或其值無效，則不會顯示任何產品。

### <a name="run-the-application"></a>執行應用程式

現在您可以執行應用程式，以查看根據產品識別碼顯示的個別產品。

1. 在 Visual Studio 中按**F5**鍵，以執行應用程式。  
   瀏覽器會開啟並顯示*default.aspx*頁面。

2. 從 [類別] 導覽功能表中，選取 [ **Boats** ]。  
   隨即顯示 [ *ProductList* ] 頁面。

3. 從 [產品] 清單中選取 [**紙張船**]。
   隨即顯示 [ *ProductDetails* ] 頁面。

    ![顯示資料項目和詳細資料-產品](display_data_items_and_details/_static/image4.png)
    
4. 關閉瀏覽器。

## <a name="additional-resources"></a>其他資源

[使用模型系結和 web forms 來抓取和顯示資料](../../presenting-and-managing-data/model-binding/retrieving-data.md)

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已新增標記和程式碼，以顯示產品和產品詳細資料。 您已瞭解強型別資料控制、模型系結和值提供者。 在下一個教學課程中，您會將購物車新增至 Wingtip 玩具範例應用程式。 

> [!div class="step-by-step"]
> [上一頁](ui_and_navigation.md)
> [下一頁](shopping-cart.md)
