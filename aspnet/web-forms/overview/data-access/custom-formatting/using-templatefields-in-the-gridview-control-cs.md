---
uid: web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-gridview-control-cs
title: 在 GridView 控制項中使用 TemplateFields （C#） |Microsoft Docs
author: rick-anderson
description: 為了提供彈性，GridView 提供了使用範本呈現的 TemplateField。 範本可以混合使用靜態 HTML、Web 控制項和 。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 11de31e8-a78a-4f96-bd75-66e994175902
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-gridview-control-cs
msc.type: authoredcontent
ms.openlocfilehash: ec17a16d7bb487d1c5cacf2d5971bbeffc1ba031
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74627713"
---
# <a name="using-templatefields-in-the-gridview-control-c"></a>在 GridView 控制項中使用 TemplateFields (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_12_CS.exe)或[下載 PDF](using-templatefields-in-the-gridview-control-cs/_static/datatutorial12cs1.pdf)

> 為了提供彈性，GridView 提供了使用範本呈現的 TemplateField。 範本可以混合使用靜態 HTML、Web 控制項和資料系結語法。 在本教學課程中，我們將探討如何使用 TemplateField，透過 GridView 控制項達成更高程度的自訂。

## <a name="introduction"></a>簡介

GridView 是由一組欄位所組成，其中指出要包含在轉譯輸出中的 `DataSource` 屬性以及資料的顯示方式。 最簡單的欄位類型是 BoundField，它會將資料值顯示為文字。 其他欄位類型會使用其他 HTML 元素來顯示資料。 例如，CheckBoxField 會轉譯為 checkbox，其已核取狀態取決於指定之資料欄位的值。ImageField 會呈現影像，其影像來源是以指定的資料欄位為基礎。 您可以使用 HyperLinkField 和 ButtonField 欄位類型來轉譯狀態相依于基礎資料欄值的超連結和按鈕。

雖然 [CheckBoxField]、[ImageField]、[HyperLinkField] 和 [ButtonField] 欄位類型允許資料的替代視圖，但它們的格式仍然相當有限。 CheckBoxField 只能顯示單一核取方塊，而 ImageField 只能顯示單一影像。 如果特定欄位需要顯示某些文字、核取方塊*和*影像，全都以不同的資料欄值為基礎呢？ 或者，如果我們想要使用 [] 核取方塊、[影像]、[超連結] 或 [按鈕] 以外的 Web 控制項來顯示資料呢？ 此外，BoundField 會將其顯示限制為單一資料欄位。 如果我們想要在單一 GridView 資料行中顯示兩個或多個資料欄值呢？

為了配合此彈性層級，GridView 提供了使用*範本*來呈現的 TemplateField。 範本可以混合使用靜態 HTML、Web 控制項和資料系結語法。 此外，TemplateField 也有各種範本，可用來自訂不同情況的呈現。 例如，預設會使用 `ItemTemplate` 來呈現每個資料列的儲存格，但 `EditItemTemplate` 範本可在編輯資料時用來自訂介面。

在本教學課程中，我們將探討如何使用 TemplateField，透過 GridView 控制項達成更高程度的自訂。 在[先前的教學](custom-formatting-based-upon-data-cs.md)課程中，我們已瞭解如何使用 `DataBound` 和 `RowDataBound` 事件處理常式，根據基礎資料自訂格式。 根據基礎資料自訂格式的另一種方式是從範本內呼叫格式化方法。 我們也會在本教學課程中探討這項技術。

在本教學課程中，我們將使用 TemplateFields 來自訂員工清單的外觀。 具體來說，我們會列出所有員工，但會將員工的名字和姓氏顯示在一個資料行中、其在行事曆控制項中的雇用日期，以及一個狀態資料行，指出他們在公司使用了多少天。

[![三個 TemplateFields 用於自訂顯示](using-templatefields-in-the-gridview-control-cs/_static/image2.png)](using-templatefields-in-the-gridview-control-cs/_static/image1.png)

**圖 1**：三個 TemplateFields 用於自訂顯示（[按一下以觀看完整大小的影像](using-templatefields-in-the-gridview-control-cs/_static/image3.png)）

## <a name="step-1-binding-the-data-to-the-gridview"></a>步驟1：將資料系結至 GridView

在您需要使用 TemplateFields 來自訂外觀的報告案例中，我發現最簡單的方法是先建立一個只包含 BoundFields 的 GridView 控制項，然後再加入新的 TemplateFields，或是將現有的 BoundFields 轉換成視需要 TemplateFields。 因此，讓我們開始本教學課程，方法是透過設計工具將 GridView 新增至頁面，並將它系結至會傳回員工清單的 ObjectDataSource。 這些步驟將會為每個員工欄位建立具有 BoundFields 的 GridView。

開啟 [`GridViewTemplateField.aspx`] 頁面，並將 GridView 從 [工具箱] 拖曳至設計工具。 從 GridView 的智慧標籤加入宣告新的 ObjectDataSource 控制項，叫用 `EmployeesBLL` 類別的 `GetEmployees()` 方法。

[![加入新的 ObjectDataSource 控制項來叫用 GetEmployees （）方法](using-templatefields-in-the-gridview-control-cs/_static/image5.png)](using-templatefields-in-the-gridview-control-cs/_static/image4.png)

**圖 2**：加入新的 ObjectDataSource 控制項來叫用 `GetEmployees()` 方法（[按一下以查看完整大小的影像](using-templatefields-in-the-gridview-control-cs/_static/image6.png)）

以這種方式系結 GridView，會自動為每個 employee 屬性加入 BoundField： `EmployeeID`、`LastName`、`FirstName`、`Title`、`HireDate`、`ReportsTo`和 `Country`。 在此報表中，我們不會使用顯示 `EmployeeID`、`ReportsTo`或 `Country` 屬性。 若要移除這些 BoundFields，您可以：

- 使用 [欄位] 對話方塊按一下 GridView 智慧標籤中的 [編輯資料行] 連結，以顯示此對話方塊。 接下來，從左下方清單中選取 BoundFields，然後按一下紅色 X 按鈕來移除 BoundField。
- 以手動方式從來源視圖編輯 GridView 的宣告式語法，並刪除您想要移除之 BoundField 的 `<asp:BoundField>` 元素。

移除 `EmployeeID`、`ReportsTo`和 `Country` BoundFields 之後，GridView 的標記應該如下所示：

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample1.aspx)]

花點時間在瀏覽器中觀看進度。 此時，您應該會看到一個資料表，其中包含每個員工的記錄和四個數據行：一個用於員工的姓氏、一個用於名字、一個用於其職稱，另一個用於員工的姓名。

[![會顯示每個員工的姓氏、名字、標題和雇用日期欄位](using-templatefields-in-the-gridview-control-cs/_static/image8.png)](using-templatefields-in-the-gridview-control-cs/_static/image7.png)

**圖 3**：每個員工都會顯示 [`LastName`]、[`FirstName`]、[`Title`] 和 [`HireDate`] 欄位（[按一下以查看完整大小的影像](using-templatefields-in-the-gridview-control-cs/_static/image9.png)）

## <a name="step-2-displaying-the-first-and-last-names-in-a-single-column"></a>步驟2：在單一資料行中顯示第一個和最後一個名稱

目前，每個員工的名字和姓氏都會顯示在個別的資料行中。 將它們結合成單一資料行可能是很好的方法。 為了達成此目的，我們需要使用 TemplateField。 我們可以加入新的 TemplateField、將其新增至所需的標記和資料系結語法，然後刪除 `FirstName` 並 `LastName` BoundFields，或者我們可以將 `FirstName` BoundField 轉換成 TemplateField，編輯 TemplateField 以包含 `LastName` 值，然後移除 `LastName` BoundField。

這兩種方法都有相同的結果，但我個人還是會在可能的情況下將 BoundFields 轉換成 TemplateFields，因為轉換會自動加入 `ItemTemplate`，`EditItemTemplate` 並使用 Web 控制項和資料系結語法來模擬 BoundField 的外觀和功能。 其優點是，我們需要對 TemplateField 執行較少的工作，因為轉換程式會為我們執行一些工作。

若要將現有的 BoundField 轉換成 TemplateField，請按一下 GridView 的智慧標籤中的 [編輯資料行] 連結，並帶出 [欄位] 對話方塊。 從左下角的清單中選取要轉換的 BoundField，然後按一下右下角的 [將此欄位轉換成 TemplateField] 連結。

[![從 [欄位] 對話方塊將 BoundField 轉換為 TemplateField](using-templatefields-in-the-gridview-control-cs/_static/image11.png)](using-templatefields-in-the-gridview-control-cs/_static/image10.png)

**圖 4**：從 [欄位] 對話方塊將 BoundField 轉換為 TemplateField （[按一下以查看完整大小的影像](using-templatefields-in-the-gridview-control-cs/_static/image12.png)）

繼續進行，並將 `FirstName` BoundField 轉換成 TemplateField。 在這項變更之後，設計工具中不會有任何得的差異。 這是因為將 BoundField 轉換成 TemplateField 時，會建立一個 TemplateField 來維護 BoundField 的外觀與風格。 雖然設計工具中目前沒有任何視覺差異，但此轉換程式已取代 BoundField 的宣告式語法 `<asp:BoundField DataField="FirstName" HeaderText="FirstName" SortExpression="FirstName" />`-使用下列 TemplateField 語法：

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample2.aspx)]

如您所見，TemplateField 是由兩個樣板組成 `ItemTemplate`，其中有一個標籤的 `Text` 屬性設定為 `FirstName` 資料欄位的值，另一個 `EditItemTemplate` 的 TextBox 控制項，其 `Text` 屬性也設定為 `FirstName` 資料欄位。 資料系結語法-`<%# Bind("fieldName") %>`-表示 *`fieldName`* 的資料欄位系結至指定的 Web 控制項屬性。

若要將 `LastName` 資料欄值加入此 TemplateField，我們需要在 `ItemTemplate` 中新增另一個標籤 Web 控制項，並將其 `Text` 屬性系結至 `LastName`。 您可以手動或透過設計工具來完成這項作業。 若要手動執行，只需將適當的宣告式語法新增至 `ItemTemplate`：

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample3.aspx)]

若要透過設計工具新增它，請按一下 GridView 智慧標籤中的 [編輯範本] 連結。 這會顯示 GridView 的範本編輯介面。 在此介面的智慧標籤中，是 GridView 中的範本清單。 由於目前只有一個 TemplateField，因此下拉式清單中唯一列出的範本是 `FirstName` TemplateField 的範本，以及 `EmptyDataTemplate` 和 `PagerTemplate`。 如果已指定，`EmptyDataTemplate` 範本會用來轉譯 GridView 的輸出（如果資料沒有系結至 GridView 的結果）。如有指定，則會使用 `PagerTemplate`來呈現支援分頁之 GridView 的分頁介面。

[![GridView 的範本可以透過設計工具編輯](using-templatefields-in-the-gridview-control-cs/_static/image14.png)](using-templatefields-in-the-gridview-control-cs/_static/image13.png)

**圖 5**： GridView 的範本可以透過設計工具編輯（[按一下以觀看完整大小的影像](using-templatefields-in-the-gridview-control-cs/_static/image15.png)）

若要同時在 [`FirstName`] TemplateField 中顯示 `LastName`，請將 [標籤] 控制項從 [工具箱] 拖曳至 GridView 範本編輯介面中 `FirstName` TemplateField 的 `ItemTemplate`。

[![將標籤 Web 控制項新增至 FirstName TemplateField 的 ItemTemplate](using-templatefields-in-the-gridview-control-cs/_static/image17.png)](using-templatefields-in-the-gridview-control-cs/_static/image16.png)

**圖 6**：將標籤 Web 控制項新增至 `FirstName` TemplateField 的 ItemTemplate （[按一下以查看完整大小的影像](using-templatefields-in-the-gridview-control-cs/_static/image18.png)）

此時，新增至 TemplateField 的標籤 Web 控制項，其 `Text` 屬性會設定為「標籤」。 我們需要變更此屬性，讓這個屬性改為系結至 `LastName` 資料欄位的值。 若要完成這項操作，請按一下 [標籤] 控制項的智慧標籤，然後選擇 [編輯系結] 選項。

[![從標籤的智慧標籤中選擇 [編輯系結] 選項](using-templatefields-in-the-gridview-control-cs/_static/image20.png)](using-templatefields-in-the-gridview-control-cs/_static/image19.png)

**圖 7**：從標籤的智慧標籤選擇 [編輯系結] 選項（[按一下以查看完整大小的影像](using-templatefields-in-the-gridview-control-cs/_static/image21.png)）

這會顯示 [系結] 對話方塊。 在這裡，您可以從左側清單中選取要參與資料系結的屬性，然後從右邊的下拉式清單中選擇要系結資料的欄位。 選擇左側的 [`Text`] 屬性和右邊的 [`LastName`] 欄位，然後按一下 [確定]。

[![將 Text 屬性系結至 LastName 資料欄位](using-templatefields-in-the-gridview-control-cs/_static/image23.png)](using-templatefields-in-the-gridview-control-cs/_static/image22.png)

**圖 8**：將 [`Text`] 屬性系結至 [`LastName` 資料] 欄位（[按一下以查看完整大小的影像](using-templatefields-in-the-gridview-control-cs/_static/image24.png)）

> [!NOTE]
> [資料系結] 對話方塊可讓您指出是否要執行雙向資料系結。 如果您將此項取消核取，將會使用資料系結語法 `<%# Eval("LastName")%>`，而不是 `<%# Bind("LastName")%>`。 這兩種方法都適用于本教學課程。 當插入和編輯資料時，雙向資料系結會變得很重要。 不過，只要顯示資料，這兩種方法的運作方式都一樣。 我們將在未來的教學課程中詳細討論雙向資料系結。

請花點時間透過瀏覽器觀看此頁面。 如您所見，GridView 仍然包含四個數據行;不過，`FirstName` 資料行現在會*同時*列出 `FirstName` 和 `LastName` 的資料欄值。

[![FirstName 和 LastName 值都會顯示在單一資料行中](using-templatefields-in-the-gridview-control-cs/_static/image26.png)](using-templatefields-in-the-gridview-control-cs/_static/image25.png)

**圖 9**： `FirstName` 和 `LastName` 值都會顯示在單一資料行中（[按一下以查看完整大小的影像](using-templatefields-in-the-gridview-control-cs/_static/image27.png)）

若要完成第一個步驟，請移除 `LastName` BoundField，並將 `FirstName` TemplateField 的 `HeaderText` 屬性重新命名為 "Name"。 這些變更之後，GridView 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample4.aspx)]

[![每個員工的名字和姓氏都會顯示在一個資料行中](using-templatefields-in-the-gridview-control-cs/_static/image29.png)](using-templatefields-in-the-gridview-control-cs/_static/image28.png)

**圖 10**：每位員工的名字和姓氏都會顯示在一個資料行中（[按一下以查看完整大小的影像](using-templatefields-in-the-gridview-control-cs/_static/image30.png)）

## <a name="step-3-using-the-calendar-control-to-display-thehireddatefield"></a>步驟3：使用行事曆控制項顯示 [`HiredDate`] 欄位

將資料欄位值顯示為 GridView 中的文字，就像使用 BoundField 一樣簡單。 不過，在某些情況下，最好使用特定的 Web 控制項，而不只是文字來表示資料。 您可以使用 TemplateFields 來自訂資料的顯示。 例如，不是將員工的雇用日期顯示為文字，而是顯示行事曆（使用行事[曆控制項](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar(VS.80).aspx)）並反白顯示其雇用日期。

若要完成這項工作，請先將 `HiredDate` BoundField 轉換成 TemplateField。 只要移至 GridView 的智慧標籤，然後按一下 [編輯資料行] 連結，就會出現 [欄位] 對話方塊。 選取 [`HiredDate`] BoundField，然後按一下 [將此欄位轉換成 TemplateField]。

[![將 HiredDate BoundField 轉換為 TemplateField](using-templatefields-in-the-gridview-control-cs/_static/image32.png)](using-templatefields-in-the-gridview-control-cs/_static/image31.png)

**圖 11**：將 `HiredDate` BoundField 轉換成 TemplateField （[按一下以查看完整大小的影像](using-templatefields-in-the-gridview-control-cs/_static/image33.png)）

如我們在步驟2中所見，這會將 BoundField 取代為包含 `ItemTemplate` 的 TemplateField，並將其 `Text` 屬性會使用資料系結語法 `<%# Bind("HiredDate")%>`系結至 `HiredDate` 值的標籤和文字方塊 `EditItemTemplate`。

若要將文字取代為 Calendar 控制項，請藉由移除標籤並加入行事曆控制項來編輯範本。 從設計工具中，選取 GridView 智慧標籤中的 [編輯範本]，然後從下拉式清單中選擇 `HireDate` TemplateField 的 `ItemTemplate`。 接下來，刪除標籤控制項，並將行事曆控制項從 [工具箱] 拖曳至範本編輯介面。

[![將行事曆控制項加入至雇用 TemplateField 的 ItemTemplate](using-templatefields-in-the-gridview-control-cs/_static/image35.png)](using-templatefields-in-the-gridview-control-cs/_static/image34.png)

**圖 12**：將行事曆控制項加入至 `HireDate` TemplateField 的 `ItemTemplate` （[按一下以觀看完整大小的影像](using-templatefields-in-the-gridview-control-cs/_static/image36.png)）

此時，GridView 中的每個資料列都會在其 `HiredDate` TemplateField 中包含行事曆控制項。 不過，員工的實際 `HiredDate` 值不會設定在行事曆控制項中的任何位置，導致每個行事曆控制項預設為顯示目前的月份和日期。 若要解決此問題，我們必須將每個員工的 `HiredDate` 指派給行事曆控制項的[SelectedDate](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selecteddate(VS.80).aspx)和[VisibleDate](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.visibledate(VS.80).aspx)屬性。

從行事曆控制項的智慧標籤中，選擇 [編輯系結]。 接下來，將 `SelectedDate` 和 `VisibleDate` 屬性系結至 `HiredDate` 的資料欄位。

[![將 SelectedDate 和 VisibleDate 屬性系結至 HiredDate 資料欄位](using-templatefields-in-the-gridview-control-cs/_static/image38.png)](using-templatefields-in-the-gridview-control-cs/_static/image37.png)

**圖 13**：將 `SelectedDate` 和 `VisibleDate` 屬性系結至 `HiredDate` 資料欄位（[按一下以查看完整大小的影像](using-templatefields-in-the-gridview-control-cs/_static/image39.png)）

> [!NOTE]
> 行事曆控制項的選取日期不一定是可見的。 例如，行事曆可能會有8月1日<sup>聖</sup>1999 做為選取的日期，但會顯示目前的月份和年份。 選取的日期和可見日期是由行事曆控制項的 `SelectedDate` 和 `VisibleDate` 屬性所指定。 因為我們想要選取員工的 `HiredDate`，並確定已顯示，所以我們需要將這兩個屬性系結至 [`HireDate` 資料] 欄位。

在瀏覽器中觀看頁面時，行事曆現在會顯示員工雇用日期的月份，並選取該特定日期。

[![員工的 HiredDate 顯示在行事曆控制項中](using-templatefields-in-the-gridview-control-cs/_static/image41.png)](using-templatefields-in-the-gridview-control-cs/_static/image40.png)

**圖 14**：員工的 `HiredDate` 會顯示在行事曆控制項中（[按一下以查看完整大小的影像](using-templatefields-in-the-gridview-control-cs/_static/image42.png)）

> [!NOTE]
> 相反地，我們在本教學課程中看到的所有範例，我們並未*將此*GridView 的 `EnableViewState` 屬性設定為 `false`。 這項決策的原因是因為按一下行事曆控制項的日期會導致回傳，將行事曆的選取日期設定為剛才按下的日期。 不過，如果 GridView 的 view 狀態已停用，則 GridView 的資料會重新系結至其基礎資料來源，這會導致行事曆的選取日期設定*回*員工的 `HireDate`，並覆寫使用者選擇的日期。

在本教學課程中，這是想法的討論，因為使用者無法更新員工的 `HireDate`。 最好是設定 Calendar 控制項，使其日期無法選取。 不論如何，本教學課程會顯示在某些情況下，必須啟用狀態，才能提供特定功能。

## <a name="step-4-showing-the-number-of-days-the-employee-has-worked-for-the-company"></a>步驟4：顯示員工為公司工作的天數

到目前為止，我們已經看過 TemplateFields 的兩個應用程式：

- 將兩個或多個資料欄值結合成一個資料行，以及
- 使用 Web 控制項（而非文字）來表示資料欄位值

TemplateFields 的第三個用法是顯示 GridView 基礎資料的中繼資料。 例如，除了顯示員工的雇用日期以外，我們可能也會想要有一個資料行顯示他們在工作上的總天數。

另一個使用 TemplateFields 的情況，是在基礎資料需要以不同的方式顯示在網頁報表中，而不是儲存在資料庫中的格式。 假設 `Employees` 資料表有一個 `Gender` 欄位，其中儲存了字元 `M` 或 `F` 以指出員工的性別。 在網頁中顯示此資訊時，我們可能會想要將性別顯示為「男」或「女性」，而不只是 "M" 或 "F"。

這兩種情況都可以藉由在 ASP.NET 網頁的程式碼後置類別中建立*格式方法*來處理（或是在個別的類別庫中，並實作為 `static` 方法），以從範本叫用。 這類格式化方法是使用稍早所見的相同資料系結語法，從範本叫用。 格式化方法可以接受任意數目的參數，但必須傳回字串。 這個傳回的字串是插入範本中的 HTML。

為了說明這個概念，讓我們來擴充教學課程，以顯示一個資料行，其中列出員工在工作上的總天數。 此格式化方法會採用 `Northwind.EmployeesRow` 物件，並傳回將員工作為字串使用的天數。 這個方法可以加入至 ASP.NET 網頁的程式碼後置類別，但*必須*標示為 `protected` 或 `public`，才能從範本存取。

[!code-csharp[Main](using-templatefields-in-the-gridview-control-cs/samples/sample5.cs)]

由於 `HiredDate` 欄位可以包含 `NULL` 的資料庫值，因此我們必須先確定不 `NULL` 值，再繼續進行計算。 如果 `NULL``HiredDate` 值，我們只會傳回字串 "Unknown";如果未 `NULL`，我們會計算目前時間與 `HiredDate` 值之間的差異，並傳回天數。

若要利用這個方法，我們必須使用資料系結語法，從 GridView 中的 TemplateField 叫用它。 首先，按一下 GridView 智慧標籤中的 [編輯資料行] 連結，然後加入新的 TemplateField，以將新的 TemplateField 加入 GridView。

[![將新的 TemplateField 新增至 GridView](using-templatefields-in-the-gridview-control-cs/_static/image44.png)](using-templatefields-in-the-gridview-control-cs/_static/image43.png)

**圖 15**：將新的 TemplateField 加入 GridView （[按一下以觀看完整大小的影像](using-templatefields-in-the-gridview-control-cs/_static/image45.png)）

將這個新的 TemplateField 的 `HeaderText` 屬性設定為 [作業上的天數]，並將其 `ItemStyle`的 `HorizontalAlign` 屬性設為 `Center`。 若要從範本呼叫 `DisplayDaysOnJob` 方法，請加入 `ItemTemplate` 並使用下列資料系結語法：

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample6.aspx)]

`Container.DataItem` 會傳回與系結至 `GridViewRow`之 `DataSource` 記錄對應的 `DataRowView` 物件。 其 `Row` 屬性會傳回強型別 `Northwind.EmployeesRow`，傳遞至 `DisplayDaysOnJob` 方法。 這個資料系結語法可以直接出現在 `ItemTemplate` 中（如下面的宣告式語法所示），也可以指派給標籤 Web 控制項的 `Text` 屬性。

> [!NOTE]
> 或者，我們可以使用 `<%# DisplayDaysOnJob(Eval("HireDate")) %>`來傳入 `HireDate` 值，而不是傳入 `EmployeesRow` 實例。 不過，`Eval` 方法會傳回 `object`，因此我們必須變更 `DisplayDaysOnJob` 方法簽章，改為接受 `object`類型的輸入參數。 我們無法盲目地將 `Eval("HireDate")` 呼叫轉型為 `DateTime`，因為 `Employees` 資料表中的 `HireDate` 資料行可以包含 `NULL` 值。 因此，我們必須接受 `object` 做為 `DisplayDaysOnJob` 方法的輸入參數，並檢查它是否有資料庫 `NULL` 值（可以使用 `Convert.IsDBNull(objectToCheck)`來完成），然後再繼續進行。

由於這些微妙差異，我選擇傳入整個 `EmployeesRow` 實例。 在下一個教學課程中，我們會看到一個更適合的範例，說明如何使用 `Eval("columnName")` 語法將輸入參數傳遞至格式化方法。

以下顯示在加入 TemplateField 之後，GridView 的宣告式語法，以及從 `ItemTemplate`呼叫的 `DisplayDaysOnJob` 方法：

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample7.aspx)]

[圖 16] 顯示透過瀏覽器觀看時完成的教學課程。

[![顯示員工已在工作上的天數](using-templatefields-in-the-gridview-control-cs/_static/image47.png)](using-templatefields-in-the-gridview-control-cs/_static/image46.png)

**圖 16**：顯示員工在工作上的天數（[按一下以觀看完整大小的影像](using-templatefields-in-the-gridview-control-cs/_static/image48.png)）

## <a name="summary"></a>總結

GridView 控制項中的 TemplateField 允許比其他欄位控制項提供更高的彈性來顯示資料。 TemplateFields 適用于下列情況：

- 多個資料欄位必須顯示在一個 GridView 資料行中
- 資料最適合使用 Web 控制項而非純文字來表示
- 輸出取決於基礎資料，例如顯示中繼資料或重新格式化資料

除了自訂資料的顯示之外，TemplateFields 也會用來自訂用於編輯和插入資料的使用者介面，如我們在未來的教學課程中所見。

接下來的兩個教學課程會繼續探索範本，一開始請先參閱在 DetailsView 中使用 TemplateFields。 接下來，我們會轉變成 FormView，其使用範本代替欄位來提供資料版面配置和結構的更大彈性。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Dan Jagers。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](custom-formatting-based-upon-data-cs.md)
> [下一頁](using-templatefields-in-the-detailsview-control-cs.md)
