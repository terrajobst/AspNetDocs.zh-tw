---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
title: 使用視圖主版頁面建立頁面配置C#（） |Microsoft Docs
author: microsoft
description: 在本教學課程中，您將瞭解如何利用 view 主版頁面，在應用程式中建立多個頁面的一般頁面配置。 您可以使用 。
ms.author: riande
ms.date: 10/16/2008
ms.assetid: dff54fcb-68b1-4488-89a2-ca97532d6a4c
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 026e3efb4ebf84016aa0f6a5fda4af549fdadfcb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74594065"
---
# <a name="creating-page-layouts-with-view-master-pages-c"></a>使用檢視主版頁面建立頁面配置 (C#)

由[Microsoft](https://github.com/microsoft)

[下載 PDF](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_CS.pdf)

> 在本教學課程中，您將瞭解如何利用 view 主版頁面，在應用程式中建立多個頁面的一般頁面配置。 例如，您可以使用視圖主版頁面來定義兩個數據行的頁面配置，並針對 web 應用程式中的所有頁面使用兩個數據行的版面配置。

## <a name="creating-page-layouts-with-view-master-pages"></a>使用視圖主版頁面建立頁面配置

在本教學課程中，您將瞭解如何利用 view 主版頁面，在應用程式中建立多個頁面的一般頁面配置。 例如，您可以使用視圖主版頁面來定義兩個數據行的頁面配置，並針對 web 應用程式中的所有頁面使用兩個數據行的版面配置。

您也可以利用 view 主版頁面，在應用程式的多個頁面之間共用通用內容。 例如，您可以將網站標誌、導覽連結和橫幅廣告放在視圖主版頁面中。 如此一來，應用程式中的每個頁面都會自動顯示此內容。

在本教學課程中，您將瞭解如何建立新的視圖主版頁面，並根據主版頁面建立新的視圖內容頁面。

### <a name="creating-a-view-master-page"></a>建立視圖主版頁面

讓我們從建立定義兩個數據行版面配置的視圖主版頁面開始。 以滑鼠右鍵按一下 [Views\Shared] 資料夾，選取功能表選項 [**加入]、[新增專案**]，然後選取 [ **MVC 視圖主版] 頁面**範本（請參閱 [圖 1]），即可將新的視圖主版頁面加入至 MVC 專案。

[![加入視圖主版頁面](creating-page-layouts-with-view-master-pages-cs/_static/image2.png)](creating-page-layouts-with-view-master-pages-cs/_static/image1.png)

**圖 01**：加入視圖主版頁面（[按一下以觀看完整大小的影像](creating-page-layouts-with-view-master-pages-cs/_static/image3.png)）

您可以在應用程式中建立一個以上的視圖主版頁面。 每個 view 主版頁面都可以定義不同的頁面配置。 例如，您可能想要讓特定頁面具有兩個數據行的配置，而其他頁面具有三個數據行的版面配置。

視圖主版頁面看起來非常類似標準的 ASP.NET MVC 視圖。 不過，不同于一般的視圖，視圖主版頁面包含一個或多個 `<asp:ContentPlaceHolder>` 標記。 `<contentplaceholder>` 標籤是用來標示可在個別內容頁面中覆寫之主版頁面的區域。

例如，[清單 1] 中的 [視圖主版] 頁面會定義兩個數據行的版面配置。 其中包含兩個 `<contentplaceholder>` 標記。 每個資料行都有一個 `<ContentPlaceHolder>`。

**清單1– `Views\Shared\Site.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample1.aspx)]

[清單 1] 中視圖主版頁面的主體包含兩個對應至兩個數據行的 `<div>` 標記。 級聯樣式表資料行類別會同時套用至 `<div>` 標記。 這個類別定義于主版頁面頂端所宣告的樣式表單中。 您可以藉由切換至設計檢視，來預覽視圖主版頁面的呈現方式。 按一下原始程式碼編輯器左下方的 [設計] 索引標籤（請參閱 [圖 2]）。

[![預覽設計工具中的主版頁面](creating-page-layouts-with-view-master-pages-cs/_static/image5.png)](creating-page-layouts-with-view-master-pages-cs/_static/image4.png)

**圖 02**：在設計工具中預覽主版頁面（[按一下以觀看完整大小的影像](creating-page-layouts-with-view-master-pages-cs/_static/image6.png)）

### <a name="creating-a-view-content-page"></a>建立視圖內容頁面

建立視圖主版頁面之後，您可以根據 [視圖主版] 頁面建立一或多個 view 內容頁。 例如，您可以在 [Views\Home] 資料夾上按一下滑鼠右鍵，選取 [**加入]、[新增專案**]、選取 [ **MVC 視圖內容] 頁面**範本、輸入名稱為 default.aspx，然後按一下 [**新增**] 按鈕（請參閱 [圖 3]），以建立主控制器的索引視圖內容頁面。

[![加入視圖內容頁面](creating-page-layouts-with-view-master-pages-cs/_static/image8.png)](creating-page-layouts-with-view-master-pages-cs/_static/image7.png)

**圖 03**：加入視圖內容頁面（[按一下以觀看完整大小的影像](creating-page-layouts-with-view-master-pages-cs/_static/image9.png)）

按一下 [新增] 按鈕之後，就會出現新的對話方塊，讓您選取要與 [視圖內容] 頁面建立關聯的視圖主版頁面（請參閱 [圖 4]）。 您可以流覽至我們在上一節中建立的主版視圖主版頁面。

[選取主版頁面 ![](creating-page-layouts-with-view-master-pages-cs/_static/image11.png)](creating-page-layouts-with-view-master-pages-cs/_static/image10.png)

**圖 04**：選取主版頁面（[按一下以觀看完整大小的影像](creating-page-layouts-with-view-master-pages-cs/_static/image12.png)）

根據網站主要頁面建立新的 view 內容頁面之後，您會在 [清單 2] 中取得檔案。

**清單2– `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample2.aspx)]

請注意，此視圖包含對應至 [視圖主版] 頁面中每個 `<asp:ContentPlaceHolder>` 標記的 `<asp:Content>` 標記。 每個 `<asp:Content>` 標籤都包含 ContentPlaceHolderID 屬性，指向它所覆寫的特定 `<asp:ContentPlaceHolder>`。

此外，請注意，[清單 2] 中的 [內容視圖] 頁面不包含任何標準的開頭和結尾 HTML 標籤。 例如，它不包含開頭和結尾 `<html>` 或 `<head>` 標記。 所有標準的開頭和結束記號都包含在視圖主版頁面中。

您想要顯示在 [視圖內容] 頁面中的任何內容都必須放在 `<asp:Content>` 標籤中。 如果您將任何 HTML 或其他內容放在這些標籤之外，當您嘗試查看頁面時，將會收到錯誤。

您不需要從內容視圖頁面中的主版頁面覆寫每個 `<asp:ContentPlaceHolder>` 標記。 當您想要將標記取代為特定內容時，您只需要覆寫 `<asp:ContentPlaceHolder>` 標記。

例如，[清單 3] 中修改過的索引視圖只包含兩個 `<asp:Content>` 標記。 每個 `<asp:Content>` 標記都包含一些文字。

**清單3– `Views\Home\Index.aspx (modified)`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample3.aspx)]

當要求 [清單 3] 中的視圖時，它會呈現 [圖 5] 中的頁面。 請注意，此視圖會呈現包含兩個數據行的頁面。 此外，也請注意，[view content] 頁面中的內容會與 [視圖主版] 頁面中的內容合併

[![[索引視圖內容] 頁面](creating-page-layouts-with-view-master-pages-cs/_static/image14.png)](creating-page-layouts-with-view-master-pages-cs/_static/image13.png)

**圖 05**： [索引視圖內容] 頁面（[按一下以查看完整大小的影像](creating-page-layouts-with-view-master-pages-cs/_static/image15.png)）

### <a name="modifying-view-master-page-content"></a>修改視圖主版頁面內容

當您使用 view 主版頁面時，幾乎會立即遇到的問題之一，就是在要求不同的視圖內容頁面時，修改視圖主版頁面內容的問題。 例如，您希望 web 應用程式中的每個頁面都有唯一的標題。 不過，標題是在視圖主版頁面中宣告，而不是在 [視圖內容] 頁面中宣告。 那麼，您要如何自訂每個視圖內容頁面的頁面標題呢？

有兩種方式可讓您修改 [視圖內容] 頁面所顯示的標題。 首先，您可以將頁面標題指派給在 [視圖內容] 頁面頂端宣告之 `<%@ page %>` 指示詞的 [標題] 屬性。 例如，如果您想要將頁面標題「超級絕佳網站」指派給索引視圖，您可以在索引視圖的頂端加入下列指示詞：

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample4.aspx)]

當索引視圖呈現到瀏覽器時，所需的標題會出現在瀏覽器標題列中：

[![瀏覽器標題列](creating-page-layouts-with-view-master-pages-cs/_static/image17.png)](creating-page-layouts-with-view-master-pages-cs/_static/image16.png)

主要視圖頁面必須滿足其中一項重要的需求，title 屬性才能正常執行。 視圖主版頁面必須包含 `<head runat="server">` 標記，而不是其標頭的一般 `<head>` 標記。 如果 `<head>` 標記不包含 runat = "server" 屬性，則不會出現標題。 預設的視圖主版頁面包含必要的 `<head runat="server">` 標記。

從個別視圖內容頁面修改主版頁面內容的替代方法是將您想要在 `<asp:ContentPlaceHolder>` 標籤中修改的區域換行。 例如，假設您想要變更主要視圖頁面所轉譯的標題，而不只是中繼標記。 [清單 4] 中的 [主要視圖] 頁面包含其 `<head>` 標記內的 `<asp:ContentPlaceHolder>` 標記。

**清單4– `Views\Shared\Site2.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample5.aspx)]

請注意，[清單 4] 中的 `<asp:ContentPlaceHolder>` 標籤包含預設的內容：預設標題和預設的中繼標記。 如果您未覆寫個別 [內容] 頁面中的此 `<asp:ContentPlaceHolder>` 標記，則會顯示預設內容。

[清單 5] 中的 [內容視圖] 頁面會覆寫 `<asp:ContentPlaceHolder>` 標記，以顯示自訂標題和自訂中繼標記。

**清單5– `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample6.aspx)]

### <a name="summary"></a>總結

本教學課程提供您「觀看主版頁面」和「觀看內容頁面」的基本簡介。 您已瞭解如何建立新的視圖主版頁面，並根據它們建立視圖內容頁面。 我們也探討了如何從特定的視圖內容頁面修改視圖主版頁面的內容。

> [!div class="step-by-step"]
> [上一頁](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
> [下一頁](passing-data-to-view-master-pages-cs.md)
