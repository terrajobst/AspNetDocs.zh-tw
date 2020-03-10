---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
title: 使用資料批註驗證程式進行驗證（VB） |Microsoft Docs
author: microsoft
description: 利用資料批註模型系結器，在 ASP.NET MVC 應用程式中執行驗證。 瞭解如何使用不同類型的驗證程式 。
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 0d23ff2b-f2ec-434a-be3b-1180beeccba3
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
msc.type: authoredcontent
ms.openlocfilehash: 00150575baabc659f7dd0c07349cde52105f6c8b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78542081"
---
# <a name="validation-with-the-data-annotation-validators-vb"></a>驗證與資料註解驗證器 (VB)

由[Microsoft](https://github.com/microsoft)

> 利用資料批註模型系結器，在 ASP.NET MVC 應用程式中執行驗證。 瞭解如何使用不同類型的驗證程式屬性，並在 Microsoft Entity Framework 中使用它們。

在本教學課程中，您將瞭解如何使用資料批註驗證程式，在 ASP.NET MVC 應用程式中執行驗證。 使用資料批註驗證器的優點是，它們可讓您藉由將一或多個屬性（例如 Required 或 StringLength 屬性）新增至類別屬性來執行驗證。

在您可以使用資料批註驗證程式之前，您必須先下載資料批註模型系結器。 您可以按一下[這裡](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471)，從 CodePlex 網站下載資料批註模型系結器範例。

請務必瞭解資料批註模型系結器不是 Microsoft ASP.NET MVC 架構的官方部分。 雖然資料批註模型系結器是由 Microsoft ASP.NET MVC 小組所建立，但 Microsoft 不會針對本教學課程中所述和使用的資料批註模型系結器提供正式的產品支援。

## <a name="using-the-data-annotation-model-binder"></a>使用資料注釋模型系結器

若要在 ASP.NET 的 MVC 應用程式中使用資料批註模型系結器，您必須先加入 DataAnnotations 的參考和 System.workflow.componentmodel.activity. DataAnnotations .dll 元件中。 選取功能表選項 [**專案]、[加入參考**]。 接著，按一下 [**流覽**] 索引標籤，並流覽至您下載（和解壓縮）資料批註模型系結器範例的位置（請參閱 [**圖 1**]）。

[![](validation-with-the-data-annotation-validators-vb/_static/image2.png)](validation-with-the-data-annotation-validators-vb/_static/image1.png)

**圖 1**：加入資料批註模型系結器的參考（[按一下以查看完整大小的影像](validation-with-the-data-annotation-validators-vb/_static/image3.png)）

選取 DataAnnotations 元件和 System.workflow.componentmodel.activity. DataAnnotations .dll 元件，然後按一下 **確定**按鈕。

您無法使用 .NET Framework Service Pack 1 隨附的 DataAnnotations 和資料批註模型系結器。 您必須使用包含在資料批註模型系結器範例下載中的 System.workflow.componentmodel.activity. DataAnnotations .dll 元件版本。

最後，您必須在 global.asax 檔案中註冊 DataAnnotations 模型系結器。 將下列程式程式碼新增至應用程式\_Start （）事件處理常式，讓應用程式\_Start （）方法看起來像這樣：

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample1.vb)]

這一行程式碼會將 DataAnnotationsModelBinder 註冊為整個 ASP.NET MVC 應用程式的預設模型系結器。

## <a name="using-the-data-annotation-validator-attributes"></a>使用資料批註驗證程式屬性

當您使用資料批註模型系結器時，您會使用驗證程式屬性來執行驗證。 System.workflow.componentmodel.activity. DataAnnotations 命名空間包含下列驗證程式屬性：

- 範圍–可讓您驗證屬性的值是否落在指定的值範圍之間。
- RegularExpression –可讓您驗證屬性的值是否符合指定的正則運算式模式。
- 必要–可讓您將屬性標示為必要。
- StringLength –可讓您指定字串屬性的最大長度。
- 驗證–所有驗證程式屬性的基類。

> [!NOTE] 
> 
> 如果任何標準驗證程式都不符合您的驗證需求，則您一律可以選擇從基底驗證屬性繼承新的驗證程式屬性，以建立自訂的驗證程式屬性。

[**清單 1** ] 中的 [Product] 類別說明如何使用這些驗證程式屬性。 [名稱]、[描述] 和 [單價] 屬性會標示為必要。 Name 屬性的字串長度必須小於10個字元。 最後，[單價] 屬性必須符合代表貨幣金額的正則運算式模式。

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample2.vb)]

**清單 1**： Models\Product.vb

Product 類別說明如何使用一個額外的屬性： DisplayName 屬性。 當屬性顯示在錯誤訊息中時，DisplayName 屬性可讓您修改屬性的名稱。 您可以顯示錯誤訊息「需要價格欄位」，而不是顯示錯誤訊息「需要單價欄位」。

> [!NOTE] 
> 
> 如果您想要完全自訂驗證程式所顯示的錯誤訊息，您可以將自訂錯誤訊息指派給驗證器的 ErrorMessage 屬性，如下所示： `<Required(ErrorMessage:="This field needs a value!")>`

您可以使用 [**清單 1** ] 中的 [Product] 類別搭配 [**清單 2**] 中的 Create （）控制器動作。 當模型狀態包含任何錯誤時，此控制器動作會重新顯示 [建立] 視圖。

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample3.vb)]

**清單 2**： Controllers\ProductController.vb

最後，您可以用滑鼠右鍵按一下 [建立] （）動作，然後選取功能表選項 [**加入視圖**]，在 [**清單 3** ] 中建立此視圖。 建立具有 Product 類別的強型別視圖做為模型類別。 從 [視圖內容] 下拉式清單中選取 [**建立**] （請參閱 [**圖 2**]）。

[![](validation-with-the-data-annotation-validators-vb/_static/image5.png)](validation-with-the-data-annotation-validators-vb/_static/image4.png)

**圖 2**：新增 Create View

[!code-aspx[Main](validation-with-the-data-annotation-validators-vb/samples/sample4.aspx)]

**清單 3**： Views\Product\Create.aspx

> [!NOTE] 
> 
> 從 [**加入視圖**] 功能表選項所產生的 [建立] 表單中移除 [識別碼] 欄位。 因為識別碼欄位對應到識別欄位，所以您不會想要允許使用者輸入此欄位的值。

如果您提交表單以建立產品，但未在必要欄位中輸入值，則會顯示 [**圖 3** ] 中的驗證錯誤訊息。

[![](validation-with-the-data-annotation-validators-vb/_static/image7.png)](validation-with-the-data-annotation-validators-vb/_static/image6.png)

**圖 3**：遺漏必要欄位

如果您輸入不正確貨幣金額，則會顯示 [**圖 4** ] 中的錯誤訊息。

[![](validation-with-the-data-annotation-validators-vb/_static/image9.png)](validation-with-the-data-annotation-validators-vb/_static/image8.png)

**圖 4**：不正確貨幣金額

## <a name="using-data-annotation-validators-with-the-entity-framework"></a>搭配 Entity Framework 使用資料批註驗證程式

如果您使用 Microsoft Entity Framework 來產生資料模型類別，則無法直接將驗證程式屬性套用至您的類別。 因為 Entity Framework Designer 會產生模型類別，所以您對模型類別所做的任何變更將會在下一次於設計工具中進行任何變更時遭到覆寫。

如果您想要將驗證程式與 Entity Framework 產生的類別搭配使用，則需要建立中繼資料類別。 您可以將驗證程式套用至中繼資料類別，而不是將驗證程式套用至實際的類別。

例如，假設您已使用 Entity Framework 建立電影類別（請參閱 [**圖 5**]）。 想像一下，您想要讓電影標題和主管屬性都需要屬性。 在這種情況下，您可以在 [**清單 4**] 中建立部分類別和中繼資料類別。

[![](validation-with-the-data-annotation-validators-vb/_static/image11.png)](validation-with-the-data-annotation-validators-vb/_static/image10.png)

**圖 5**： Entity Framework 產生的 Movie 類別

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample5.vb)]

**清單 4**： Models\Movie.vb

[**清單 4** ] 中的檔案包含兩個名為 Movie 和 MovieMetaData 的類別。 Movie 類別是部分類別。 它會對應到 DataModel 所產生的部分類別，這些是由包含在 .vb 檔案中的 Entity Framework。

目前，.NET framework 不支援部分屬性。 因此，您無法將驗證程式屬性套用至 DataModel 中定義的 Movie 類別屬性，方法是將驗證程式屬性套用至**清單 4**中所定義之 movie 類別的屬性。

請注意，Movie 部分類別會以指向 MovieMetaData 類別的 MetadataType 屬性裝飾。 MovieMetaData 類別包含 Movie 類別屬性的 proxy 屬性。

驗證程式屬性會套用至 MovieMetaData 類別的屬性。 Title、Director 和 DateReleased 屬性都會標示為必要屬性。 必須指派包含少於5個字元的字串給 Director 屬性。 最後，DisplayName 屬性會套用至 DateReleased 屬性，以顯示錯誤訊息，例如「需要發行日期欄位」。 而不是「需要 DateReleased 欄位」錯誤。

> [!NOTE] 
> 
> 請注意，MovieMetaData 類別中的 proxy 屬性不需要表示與 Movie 類別中的對應屬性相同的類型。 例如，Director 屬性是 Movie 類別中的字串屬性和 MovieMetaData 類別中的物件屬性。

[**圖 6** ] 中的頁面說明當您為電影內容輸入不正確值時，所傳回的錯誤訊息。

[![](validation-with-the-data-annotation-validators-vb/_static/image13.png)](validation-with-the-data-annotation-validators-vb/_static/image12.png)

**圖 6**：搭配 Entity Framework 使用驗證程式（[按一下以觀看完整大小的影像](validation-with-the-data-annotation-validators-vb/_static/image14.png)）

## <a name="summary"></a>總結

在本教學課程中，您已瞭解如何利用資料批註模型系結器，在 ASP.NET MVC 應用程式中執行驗證。 您已瞭解如何使用不同類型的驗證程式屬性，例如 Required 和 StringLength 屬性。 您也已瞭解如何在使用 Microsoft Entity Framework 時使用這些屬性。

> [!div class="step-by-step"]
> [上一篇](validating-with-a-service-layer-vb.md)
