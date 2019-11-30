---
uid: web-forms/overview/older-versions-getting-started/master-pages/control-id-naming-in-content-pages-vb
title: 內容頁中的控制項識別碼命名（VB） |Microsoft Docs
author: rick-anderson
description: 說明 ContentPlaceHolder 控制項如何作為命名容器，並因此以程式設計方式使用控制項，而不容易（透過 FindControl） 。
ms.author: riande
ms.date: 06/10/2008
ms.assetid: dbb024a6-f043-4fc5-ad66-56556711875b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/control-id-naming-in-content-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 3cb8dec47040bc65f1a024325c91590729ffbdb7
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74586637"
---
# <a name="control-id-naming-in-content-pages-vb"></a>內容頁中的控制項識別碼命名 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_05_VB.zip)或[下載 PDF](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_05_VB.pdf)

> 說明 ContentPlaceHolder 控制項如何作為命名容器，並因此以程式設計方式使用控制項，而不容易（透過 FindControl）。 查看這個問題和因應措施。 同時討論如何以程式設計方式存取產生的 ClientID 值。

## <a name="introduction"></a>簡介

所有的 ASP.NET 伺服器控制項都包含可唯一識別控制項的 `ID` 屬性，而這是控制項在程式碼後置類別中以程式設計方式存取的方法。 同樣地，HTML 檔案中的元素可能會包含可唯一識別專案的 `id` 屬性;這些 `id` 值通常會在用戶端腳本中用來以程式設計方式參考特定的 HTML 專案。 在此情況下，您可能會假設當 ASP.NET 伺服器控制項轉譯為 HTML 時，它的 `ID` 值會當做轉譯 HTML 專案的 `id` 值使用。 這不一定是這樣的情況，因為在某些情況下，具有單一 `ID` 值的單一控制項可能會出現在轉譯的標記中多次。 假設有一個 GridView 控制項，其中包含具有 `ID` 值 `ProductName`之標籤 Web 控制項的 TemplateField。 當 GridView 在執行時間系結至其資料來源時，此標籤會針對每個 GridView 資料列重複一次。 每個呈現的標籤都需要唯一的 `id` 值。

為了處理這類案例，ASP.NET 允許將特定控制項表示為命名容器。 命名容器可作為新的 `ID` 命名空間。 出現在命名容器中的任何伺服器控制項，其轉譯的 `id` 值前面會加上命名容器控制項的 `ID`。 例如，`GridView` 和 `GridViewRow` 類別都是命名容器。 因此，在 GridView TemplateField 中使用 `ID` `ProductName` 所定義的標籤控制項，會得到 `GridViewID_GridViewRowID_ProductName`的轉譯 `id` 值。 由於*GridViewRowID*對於每個 GridView 資料列都是唯一的，因此產生的 `id` 值是唯一的。

> [!NOTE]
> [`INamingContainer` 介面](https://msdn.microsoft.com/library/system.web.ui.inamingcontainer.aspx)是用來指出特定的 ASP.NET 伺服器控制項應該當做命名容器來運作。 `INamingContainer` 介面不會將伺服器控制項必須執行的任何方法拼出來;相反地，它是用來做為標記。 在產生轉譯的標記時，如果控制項會執行此介面，則 ASP.NET 引擎會自動將其 `ID` 值前置到其呈現 `id` 屬性值的子代。 在步驟2中，將會更詳細地討論此程式。

命名容器不僅會變更轉譯的 `id` 屬性值，也會影響控制項在 ASP.NET 網頁的程式碼後置類別中，如何以程式設計方式參考。 `FindControl("controlID")` 方法通常用來以程式設計方式參考 Web 控制項。 不過，`FindControl` 不會透過命名容器來進行。 因此，您無法直接使用 `Page.FindControl` 方法來參考 GridView 或其他命名容器中的控制項。

您可能有猜得到，主版頁面和 ContentPlaceHolders 都實作為命名容器。 在本教學課程中，我們將探討主版頁面如何影響 HTML 專案的 `id` 值，以及如何使用 `FindControl`以程式設計方式參考內容頁面中的 Web 控制項。

## <a name="step-1-adding-a-new-aspnet-page"></a>步驟1：加入新的 ASP.NET 網頁

為了示範本教學課程中所討論的概念，讓我們將新的 ASP.NET 網頁新增至我們的網站。 在根資料夾中建立名為 `IDIssues.aspx` 的新內容頁面，並將其系結至 `Site.master` 主版頁面。

![將內容頁 IDIssues 新增至根資料夾](control-id-naming-in-content-pages-vb/_static/image1.png)

**圖 01**：將內容頁面 `IDIssues.aspx` 新增至根資料夾

Visual Studio 會自動為每個主版頁面的四個 ContentPlaceHolders 建立內容控制項。 如[*多 ContentPlaceHolders 和預設內容*](multiple-contentplaceholders-and-default-content-vb.md)教學課程中所述，如果內容控制項不存在，則會改為發出主版頁面的預設 ContentPlaceHolder 內容。 因為 `QuickLoginUI` 和 `LeftColumnContent` ContentPlaceHolders 包含適用于此頁面的適當預設標記，所以請繼續進行，並從 `IDIssues.aspx`移除其對應的內容控制項。 此時，內容頁面的宣告式標記看起來應該如下所示：

[!code-aspx[Main](control-id-naming-in-content-pages-vb/samples/sample1.aspx)]

在[*主版頁面教學課程中指定標題、中繼標記和其他 HTML 標頭*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md)中，我們建立了自訂的基底頁面類別（`BasePage`），它會自動設定頁面的標題（如果未明確設定）。 若要讓 `IDIssues.aspx` 頁面採用這項功能，頁面的程式碼後置類別必須衍生自 `BasePage` 類別（而不是 `System.Web.UI.Page`）。 修改程式碼後置類別的定義，使其看起來如下所示：

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample2.vb)]

最後，更新 `Web.sitemap` 檔案以包含此新課程的專案。 新增 `<siteMapNode>` 專案，並將其 `title` 和 `url` 屬性分別設定為 [控制識別碼命名問題] 和 [`~/IDIssues.aspx`]。 進行這項新增之後，您的 `Web.sitemap` 檔案的標記看起來應該如下所示：

[!code-xml[Main](control-id-naming-in-content-pages-vb/samples/sample3.xml)]

如 [圖 2] 所示，`Web.sitemap` 中的新網站地圖專案會立即反映在左欄的 [課程] 區段中。

![[課程] 區段現在包含 &quot;控制項 ID 命名問題的連結&quot;](control-id-naming-in-content-pages-vb/_static/image2.png)

**圖 02**： [課程] 區段現在包含「控制項 ID 命名問題」的連結

## <a name="step-2-examining-the-renderedidchanges"></a>步驟2：檢查呈現的`ID`變更

為了進一步瞭解 ASP.NET 引擎對伺服器控制項轉譯的 `id` 值所做的修改，讓我們將幾個 Web 控制項新增至 [`IDIssues.aspx`] 頁面，然後再查看傳送至瀏覽器的轉譯標記。 具體來說，請輸入「請輸入您的年齡：」文字，後面接著 TextBox Web 控制項。 在頁面上進一步向下新增按鈕 Web 控制項和標籤 Web 控制項。 將 TextBox 的 `ID` 和 `Columns` 屬性分別設定為 [`Age`] 和 [3]。 將按鈕的 [`Text`] 和 [`ID` 屬性] 設定為 [提交] 和 [`SubmitButton`]。 清除標籤的 [`Text`] 屬性，並將其 `ID` 設定為 [`Results`]。

此時，內容控制項的宣告式標記看起來應該如下所示：

[!code-aspx[Main](control-id-naming-in-content-pages-vb/samples/sample4.aspx)]

[圖 3] 顯示透過 Visual Studio 的設計工具觀看的頁面。

[![頁面包含三個 Web 控制項：文字方塊、按鈕和標籤](control-id-naming-in-content-pages-vb/_static/image4.png)](control-id-naming-in-content-pages-vb/_static/image3.png)

**圖 03**：此頁面包含三個 Web 控制項： [TextBox]、[Button] 和 [標籤] （[按一下以查看完整大小的影像](control-id-naming-in-content-pages-vb/_static/image5.png)）

透過瀏覽器造訪頁面，然後觀看 HTML 原始檔。 如下列標記所示，TextBox、Button 和 Label Web 控制項之 HTML 專案的 `id` 值是 Web 控制項 `ID` 值的組合，以及頁面中命名容器的 `ID` 值。

[!code-html[Main](control-id-naming-in-content-pages-vb/samples/sample5.html)]

如本教學課程稍早所述，主版頁面和其 ContentPlaceHolders 都作為命名容器。 因此，兩者都會提供其嵌套控制項的呈現 `ID` 值。 採用 TextBox 的 `id` 屬性，例如： `ctl00_MainContent_Age`。 回想一下 TextBox 控制項的 `ID` 值是 `Age`。 其前面會加上其 ContentPlaceHolder 控制項的 `ID` 值，`MainContent`。 此外，此值的前面會加上主版頁面的 `ID` 值，`ctl00`。 淨效果是由主版頁面、ContentPlaceHolder 控制項和 TextBox 本身的 `ID` 值所組成的 `id` 屬性值。

[圖 4] 說明此行為。 若要判斷 `Age` 文字方塊的轉譯 `id`，請從 TextBox 控制項的 `ID` 值開始，`Age`。 接下來，在控制項階層中往上一步。 在每個命名容器（具有 peach 色彩的節點）上，使用命名容器的 `id`在目前轉譯的 `id` 前面加上前置詞。

![呈現的 id 屬性是以命名容器的識別碼值為基礎](control-id-naming-in-content-pages-vb/_static/image6.png)

**圖 04**：呈現的 `id` 屬性是以命名容器的 `ID` 值為基礎

> [!NOTE]
> 如我們所討論，轉譯 `id` 屬性的 `ctl00` 部分會構成主版頁面的 `ID` 值，但您可能會想知道此 `ID` 值的呈現方式。 我們並未在主要或內容頁面中的任何位置指定它。 ASP.NET 網頁中的大部分伺服器控制項都是透過頁面的宣告式標記明確加入。 `MainContent` ContentPlaceHolder 控制項已在 `Site.master`的標記中明確指定;`IDIssues.aspx`的標記已定義 [`Age`] 文字方塊。 我們可以透過屬性視窗或從宣告式語法，指定這些控制項類型的 `ID` 值。 其他控制項（例如主版頁面本身）並未定義于宣告式標記中。 因此，必須為我們自動產生其 `ID` 值。 ASP.NET 引擎會在執行時間為尚未明確設定其識別碼的控制項設定 `ID` 值。 它會使用命名模式 `ctlXX`，其中*XX*是連續增加的整數值。

因為主版頁面本身會當做命名容器，所以主頁面中定義的 Web 控制項也已改變 `id` 屬性值轉譯。 例如，在[*使用主版頁面建立全網站版面*](creating-a-site-wide-layout-using-master-pages-vb.md)配置教學課程中，我們新增至主版頁面的 `DisplayDate` 標籤具有下列轉譯的標記：

[!code-html[Main](control-id-naming-in-content-pages-vb/samples/sample6.html)]

請注意，`id` 屬性同時包含主版頁面的 `ID` 值（`ctl00`），以及標籤 Web 控制項（`DateDisplay`）的 `ID` 值。

## <a name="step-3-programmatically-referencing-web-controls-viafindcontrol"></a>步驟3：透過`FindControl` 以程式設計方式參考 Web 控制項

每個 ASP.NET 伺服器控制項都包含一個 `FindControl("controlID")` 方法，可在控制項的子代中搜尋名為*controlID*的控制項。 如果找到這類控制項，則會傳回;如果找不到相符的控制項，`FindControl` 會傳回 `Nothing`。

`FindControl` 在需要存取控制項但沒有直接參考的情況下很有用。 例如，當使用像是 GridView 的資料 Web 控制項時，GridView 的欄位內的控制項會在宣告式語法中定義一次，但在執行時間，會針對每個 GridView 資料列建立控制項的實例。 因此，在執行時間產生的控制項會存在，但我們沒有從程式碼後置類別提供的直接參考。 因此，我們需要使用 `FindControl`，以程式設計方式處理 GridView 欄位內的特定控制項。 （如需使用 `FindControl` 來存取資料 Web 控制項範本內之控制項的詳細資訊，請參閱以[資料為基礎的自訂格式](../../data-access/custom-formatting/custom-formatting-based-upon-data-vb.md)）。當您以動態方式將 Web 控制項新增至 Web 表單時，就會發生這種情況，這是[建立動態資料輸入使用者介面](https://msdn.microsoft.com/library/aa479330.aspx)中所討論的主題。

為了說明如何使用 `FindControl` 方法來搜尋內容頁面中的控制項，請為 `SubmitButton`的 `Click` 事件建立事件處理常式。 在事件處理常式中，加入下列程式碼，以程式設計方式參考 [`Age`] 文字方塊，並使用 `FindControl` 方法來 `Results` 標籤，然後根據使用者的輸入，在 `Results` 中顯示訊息。

> [!NOTE]
> 當然，我們不需要使用 `FindControl` 來參考此範例的標籤和 TextBox 控制項。 我們可以透過其 `ID` 屬性值直接參考它們。 我在這裡使用 `FindControl` 來說明從內容頁面使用 `FindControl` 時，會發生什麼事。

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample7.vb)]

雖然用來呼叫 `FindControl` 方法的語法在 `SubmitButton_Click`的前兩行中稍有不同，但它們在語義上是相等的。 回想一下，所有的 ASP.NET 伺服器控制項都包含一個 `FindControl` 方法。 這包括 `Page` 類別，所有 ASP.NET 程式碼後置類別都必須從中衍生。 因此，如果您未覆寫程式碼後置類別或自訂基類中的 `FindControl` 方法，則呼叫 `FindControl("controlID")` 相當於呼叫 `Page.FindControl("controlID")`。

輸入此程式碼之後，請造訪瀏覽器中的 [`IDIssues.aspx`] 頁面，輸入您的年齡，然後按一下 [提交] 按鈕。 按一下 [提交] 按鈕時，會引發 `NullReferenceException` （請參閱 [圖 5]）。

[![引發 NullReferenceException](control-id-naming-in-content-pages-vb/_static/image8.png)](control-id-naming-in-content-pages-vb/_static/image7.png)

**圖 05**：引發 `NullReferenceException` （[按一下以觀看完整大小的影像](control-id-naming-in-content-pages-vb/_static/image9.png)）

如果您在 `SubmitButton_Click` 事件處理常式中設定中斷點，您會看到 `FindControl` 的兩個呼叫都會傳回 `Nothing`。 當我們嘗試存取 `Age` TextBox 的 `Text` 屬性時，就會引發 `NullReferenceException`。

問題在於，`Control.FindControl` 只會搜尋位於相同命名容器中的*控制項*子代。 因為主版頁面構成新的命名容器，所以 `Page.FindControl("controlID")` 的呼叫永遠不會 permeates 主版頁面物件 `ctl00`。 （請回到 [圖 4] 來觀看控制項階層，其中顯示 `Page` 物件做為主版頁面物件的父系 `ctl00`）。因此，找不到 [`Results` 標籤] 和 [`Age`] 文字方塊，`ResultsLabel` 和 `AgeTextBox` 指派 `Nothing`的值。

這項挑戰有兩種因應措施：我們可以向下切入，一次一個命名容器，到適當的控制項;或者，我們也可以建立自己的 `FindControl` 方法來 permeates 命名容器。 讓我們來檢查每個選項。

### <a name="drilling-into-the-appropriate-naming-container"></a>深入探索適當的命名容器

若要使用 `FindControl` 來參考 `Results` 標籤或 `Age` TextBox，我們必須從相同命名容器中的祖系控制項呼叫 `FindControl`。 如 [圖 4] 所示，`MainContent` ContentPlaceHolder 控制項是相同命名容器內 `Results` 或 `Age` 的唯一祖系。 換句話說，從 `MainContent` 控制項呼叫 `FindControl` 方法（如下列程式碼片段所示），會正確地傳回 `Results` 或 `Age` 控制項的參考。

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample8.vb)]

不過，我們無法使用上述語法來處理內容頁面的程式碼後置類別中的 `MainContent` ContentPlaceHolder，因為 ContentPlaceHolder 是在主版頁面中定義。 相反地，我們必須使用 `FindControl` 來取得 `MainContent`的參考。 將 `SubmitButton_Click` 事件處理常式中的程式碼取代為下列修改：

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample9.vb)]

如果您透過瀏覽器造訪頁面，請輸入您的年齡，然後按一下 [Submit （提交）] 按鈕，就會引發 `NullReferenceException`。 如果您在 `SubmitButton_Click` 事件處理常式中設定中斷點，您會看到在嘗試呼叫 `MainContent` 物件的 `FindControl` 方法時，會發生這個例外狀況。 `MainContent` 物件等於 `Nothing`，因為 `FindControl` 方法找不到名為 "MainContent" 的物件。 根本原因與 [`Results` 標籤] 和 [`Age` TextBox] 控制項相同： `FindControl` 從控制項階層的頂端開始搜尋，而不會滲透命名容器，但 `MainContent` ContentPlaceHolder 是在主版頁面內，也就是命名容器。

我們必須先參考主版頁面控制項，才可以使用 `FindControl` 取得 `MainContent`的參考。 參考主版頁面之後，我們就可以透過 `FindControl` 取得 `MainContent` ContentPlaceHolder 的參考，並從該處參考 `Results` 標籤和 `Age` TextBox （同樣地，使用 `FindControl`）。 但是，我們要如何取得主版頁面的參考？ 藉由檢查所轉譯標記中的 `id` 屬性，很明顯地 `ctl00`主版頁面的 `ID` 值。 因此，我們可以使用 `Page.FindControl("ctl00")` 取得主版頁面的參考，然後使用該物件取得 `MainContent`的參考，依此類推。 下列程式碼片段說明此邏輯：

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample10.vb)]

雖然這段程式碼肯定可行，但它會假設主版頁面自動產生的 `ID` 一律會 `ctl00`。 最好不要對自動產生的值進行假設。

幸運的是，主版頁面的參考可透過 `Page` 類別的 `Master` 屬性來存取。 因此，我們可以改為使用 `Page.Master.FindControl("MainContent")`，而不需要使用 `FindControl("ctl00")` 來取得主版頁面的參考，以便存取 `MainContent` ContentPlaceHolder。 使用下列程式碼更新 `SubmitButton_Click` 事件處理常式：

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample11.vb)]

此時，透過瀏覽器造訪頁面、輸入您的年齡，然後按一下 [提交] 按鈕，就會如預期般在 [`Results`] 標籤中顯示訊息。

[![使用者的年齡會顯示在標籤中](control-id-naming-in-content-pages-vb/_static/image11.png)](control-id-naming-in-content-pages-vb/_static/image10.png)

**圖 06**：使用者的年齡會顯示在標籤中（[按一下以觀看完整大小的影像](control-id-naming-in-content-pages-vb/_static/image12.png)）

### <a name="recursively-searching-through-naming-containers"></a>以遞迴方式搜尋命名容器

先前的程式碼範例從主版頁面參考 `MainContent` ContentPlaceHolder 控制項，然後 `MainContent`的 [`Results` 標籤] 和 [`Age` TextBox] 控制項，是因為 `Control.FindControl` 方法只會在*控制項*的命名容器中搜尋。 在大部分的情況下，讓 `FindControl` 保持在命名容器內是合理的，因為兩個不同的命名容器中的兩個控制項可能會有相同的 `ID` 值。 請考慮 GridView 的案例，其會在其中一個 TemplateFields 中定義名為 `ProductName` 的標籤 Web 控制項。 當資料在執行時間系結至 GridView 時，會為每個 GridView 資料列建立一個 `ProductName` 標籤。 如果 `FindControl` 搜尋所有的命名容器，而我們呼叫 `Page.FindControl("ProductName")`，`FindControl` 會傳回哪個標籤實例？ 第一個 GridView 資料列中的 `ProductName` 標籤？ 最後一個資料列中的那一個？

因此，讓 `Control.FindControl` 搜尋只是*控制項*的命名容器，在大多數情況下都是合理的。 但還有其他案例，例如，我們在所有命名容器中都有唯一的 `ID`，而且想要避免必須精心參考控制項階層中的每個命名容器來存取控制項。 擁有會以遞迴方式搜尋所有命名容器的 `FindControl` variant 也是合理的。 可惜的是，.NET Framework 不包含這種方法。

好消息是，我們可以建立自己的 `FindControl` 方法，以遞迴方式搜尋所有的命名容器。 事實上，使用*擴充方法*時，我們可以將 `FindControlRecursive` 方法加到 `Control` 類別，以伴隨其現有的 `FindControl` 方法。

> [!NOTE]
> 擴充方法是C# 3.0 和 Visual Basic 9 的新功能，這是隨附于 .NET Framework 3.5 版和 Visual Studio 2008 的語言。 簡單地說，擴充方法可讓開發人員透過特殊語法，為現有的類別類型建立新的方法。 如需這項實用功能的詳細資訊，請參閱我的文章[使用擴充方法擴充基底類型功能](http://aspnet.4guysfromrolla.com/articles/120507-1.aspx)。

若要建立擴充方法，請將新檔案新增至名為 `PageExtensionMethods.vb`的 `App_Code` 資料夾。 新增名為 `FindControlRecursive` 的擴充方法，以接受名為 `controlID`的 `String` 參數作為輸入。 若要讓擴充方法正常運作，請務必將類別標記為 `Module`，而且擴充方法的前面會加上 `<Extension()>` 屬性。 此外，所有擴充方法都必須接受延伸方法所套用之類型的物件做為其第一個參數。

將下列程式碼新增至 `PageExtensionMethods.vb` 檔案，以定義此 `Module` 和 `FindControlRecursive` 擴充方法：

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample12.vb)]

將此程式碼備妥之後，請返回 `IDIssues.aspx` 頁面的程式碼後置類別，並將目前的 `FindControl` 方法呼叫標記為批註。 以 `Page.FindControlRecursive("controlID")`的呼叫來取代它們。 擴充方法的最棒之處在于，它們會直接出現在 IntelliSense 下拉式清單中。 如 [圖 7] 所示，當您輸入 `Page` 然後按下句點時，`FindControlRecursive` 方法會連同其他 `Control` 類別方法一起包含在 IntelliSense 下拉式集中。

[IntelliSense 下拉式清單中包含 ![擴充方法](control-id-naming-in-content-pages-vb/_static/image14.png)](control-id-naming-in-content-pages-vb/_static/image13.png)

**圖 07**：擴充方法包含在 [IntelliSense] 下拉式清單中（[按一下以觀看完整大小的影像](control-id-naming-in-content-pages-vb/_static/image15.png)）

在 `SubmitButton_Click` 事件處理常式中輸入下列程式碼，然後藉由造訪頁面並輸入您的年齡，然後按一下 [提交] 按鈕進行測試。 如 [圖 6] 所示，產生的輸出將會是「您的年齡年份已過時！」訊息。

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample13.vb)]

> [!NOTE]
> 由於擴充方法是C# 3.0 和 Visual Basic 9 的新功能，因此如果您使用 Visual Studio 2005，就無法使用擴充方法。 相反地，您必須在 helper 類別中執行 `FindControlRecursive` 方法。 [Rick Strahl](http://www.west-wind.com/WebLog/default.aspx)在他的 blog 文章中有這類的範例， [ASP.NET 的微波激頁和 `FindControl`](http://www.west-wind.com/WebLog/posts/5127.aspx)。

## <a name="step-4-using-the-correctidattribute-value-in-client-side-script"></a>步驟4：在用戶端腳本中使用正確的`id`屬性值

如本教學課程簡介中所述，在用戶端腳本中，通常會使用 Web 控制項的轉譯 `id` 屬性，以程式設計方式參考特定的 HTML 專案。 例如，下列 JavaScript 會依 `id` 參考 HTML 專案，然後在強制回應訊息框中顯示其值：

[!code-csharp[Main](control-id-naming-in-content-pages-vb/samples/sample14.cs)]

回想一下，在不包含命名容器的 ASP.NET 網頁中，呈現的 HTML 專案的 `id` 屬性與 Web 控制項的 `ID` 屬性值相同。 因此，在 JavaScript 程式碼中，將 `id` 屬性值中的硬程式碼很吸引人。 也就是說，如果您知道您想要透過用戶端腳本來存取 `Age` TextBox Web 控制項，請藉由呼叫 `document.getElementById("Age")`來執行此動作。

這種方法的問題在於，使用主版頁面（或其他命名容器控制項）時，轉譯的 HTML `id` 與 Web 控制項的 `ID` 屬性不同義。 您的第一步可能是透過瀏覽器造訪頁面，並查看來源以判斷實際的 `id` 屬性。 一旦知道轉譯的 `id` 值，您就可以將它貼入 `getElementById` 的呼叫中，以存取您需要透過用戶端腳本使用的 HTML 元素。 這種方法並不理想，因為對頁面的控制項階層進行某些變更，或對命名控制項的 `ID` 屬性所做的變更，將會改變產生的 `id` 屬性，進而中斷您的 JavaScript 程式碼。

好消息是，您可以透過 Web 控制項的[`ClientID` 屬性](https://msdn.microsoft.com/library/system.web.ui.control.clientid.aspx)，在伺服器端程式碼中存取所呈現的 `id` 屬性值。 您應該使用這個屬性來判斷用戶端腳本中使用的 `id` 屬性值。 例如，若要將 JavaScript 函式加入至頁面，當呼叫時，會在強制回應訊息框中顯示 `Age` 文字方塊的值，將下列程式碼加入 `Page_Load` 事件處理常式：

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample15.vb)]

上述程式碼會將 `Age` TextBox 的 `ClientID` 屬性值插入至 `getElementById`的 JavaScript 呼叫中。 如果您透過瀏覽器造訪此頁面並觀看 HTML 原始碼，您會發現下列 JavaScript 程式碼：

[!code-html[Main](control-id-naming-in-content-pages-vb/samples/sample16.html)]

請注意，在 `getElementById`的呼叫中會出現正確的 `id` 屬性值 `ctl00_MainContent_Age`。 因為這個值是在執行時間計算的，所以不論頁面控制項階層的後續變更為何，都可以運作。

> [!NOTE]
> 這個 JavaScript 範例只示範如何新增 JavaScript 函式，該函式會正確地參考伺服器控制項所呈現的 HTML 元素。 若要使用此函式，您必須撰寫額外的 JavaScript，以便在檔載入時或特定的使用者動作過大幅簡化時呼叫函式。 如需這些和相關主題的詳細資訊，請參閱[使用用戶端腳本](https://msdn.microsoft.com/library/aa479302.aspx)。

## <a name="summary"></a>總結

某些 ASP.NET 伺服器控制項的作用是命名容器，這會影響其子控制項的轉譯 `id` 屬性值，以及 `FindControl` 方法所 canvassed 的控制項範圍。 與主版頁面相關的是，主版頁面本身和其 ContentPlaceHolder 控制項都是命名容器。 因此，我們需要使用 `FindControl`，在內容頁面中以程式設計方式參考控制項。 在本教學課程中，我們探討了兩種技術：深入探索 ContentPlaceHolder 控制項並呼叫其 `FindControl` 方法;並輪流執行自己的 `FindControl` 執行，以遞迴方式搜尋所有的命名容器。

除了參考 Web 控制項的伺服器端問題命名容器之外，也有用戶端問題。 在沒有命名容器的情況下，Web 控制項的 `ID` 屬性值和轉譯的 `id` 屬性值都是同一個。 但是在新增命名容器之後，轉譯的 `id` 屬性會同時包含 Web 控制項的 `ID` 值和其控制項階層上階中的命名容器。 只要您使用 Web 控制項的 `ClientID` 屬性來判斷用戶端腳本中轉譯的 `id` 屬性值，這些命名問題就不會有問題。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [ASP.NET 主版頁面和 `FindControl`](http://www.west-wind.com/WebLog/posts/5127.aspx)
- [建立動態資料輸入使用者介面](https://msdn.microsoft.com/library/aa479330.aspx)
- [使用擴充方法擴充基底類型功能](http://aspnet.4guysfromrolla.com/articles/120507-1.aspx)
- [如何：參考 ASP.NET 主版頁面內容](https://msdn.microsoft.com/library/xxwa0ff0.aspx)
- [宿主頁面：秘訣、訣竅和陷阱](http://www.odetocode.com/articles/450.aspx)
- [使用用戶端腳本](https://msdn.microsoft.com/library/aa479302.aspx)

### <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有多個 ASP/ASP. NET 書籍和創辦人的4GuysFromRolla.com。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 3.5*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 Scott 可以在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)或透過他在[http://ScottOnWriting.NET](http://scottonwriting.net/)的 blog。

### <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Zack，Suchi Barnerjee。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)的那一行下拉式。

> [!div class="step-by-step"]
> [上一頁](urls-in-master-pages-vb.md)
> [下一頁](interacting-with-the-master-page-from-the-content-page-vb.md)
