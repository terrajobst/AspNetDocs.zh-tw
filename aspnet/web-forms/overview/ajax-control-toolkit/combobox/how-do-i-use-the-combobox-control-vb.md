---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-vb
title: 如何? 使用 ComboBox 控制項嗎？ （VB） |Microsoft Docs
author: microsoft
description: ComboBox 是一個 ASP.NET 的 AJAX 控制項，結合文字方塊的彈性與使用者可以選擇的選項清單。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: e887e7b2-a6e7-4a28-a134-ba334494badb
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 468063a72253cce55a02bfaef1219bff03d06418
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554485"
---
# <a name="how-do-i-use-the-combobox-control-vb"></a>如何? 使用 ComboBox 控制項嗎？ (VB)

由[Microsoft](https://github.com/microsoft)

> ComboBox 是一個 ASP.NET 的 AJAX 控制項，結合文字方塊的彈性與使用者可以選擇的選項清單。

本教學課程的目的是要說明 AJAX Control 工具組 ComboBox 控制項。 下拉式方塊的運作方式就像是標準 ASP.NET DropDownList 控制項與 TextBox 控制項的組合。 您可以從預先存在的專案清單中選取，或輸入新的專案。

ComboBox 類似于自動完成控制項擴充項，但控制項用於不同的案例。 自動完成擴充項會查詢 web 服務，以取得相符的專案。 相反地，ComboBox 控制項會以一組專案初始化。 當您使用 ComboBox 控制項時，使用「自動完成擴充功能」是很合理的，但在處理小型資料集（數十個汽車元件）時，這是合理的作法。

## <a name="selecting-from-a-static-list-of-items"></a>從靜態專案清單中選取

讓我們從使用 ComboBox 控制項的簡單範例開始。 假設您想要在下拉式清單中顯示專案的靜態清單。 不過，您想要讓清單不完整的可能性保持開啟。 您想要允許使用者在清單中輸入自訂值。

我們會建立新的 ASP.NET Web form 頁面，並在頁面中使用 ComboBox 控制項。 將新的 [ASP.NET] 頁面新增至您的專案，並切換至 [設計檢視]。

如果您想要在頁面中使用 ComboBox 控制項，則必須將 ScriptManager 控制項加入至頁面。 將 [AJAX 延伸模組] 索引標籤底下的 ScriptManager 控制項拖曳至設計工具介面。 您應該在頁面頂端新增 ScriptManager 控制項;您可以將它加入開頭伺服器端 &lt;表單&gt; 標記的正下方。

接下來，將 ComboBox 控制項拖曳至頁面上。 您可以使用其他 AJAX 控制項工具組控制項和控制項擴充項，在 [工具箱] 中找到 ComboBox 控制項（請參閱 ..data 圖1）。

[![簡單的表單建立名片](how-do-i-use-the-combobox-control-vb/_static/image1.jpg)](how-do-i-use-the-combobox-control-vb/_static/image1.png)

**圖 01**：從 [工具箱] 選取 ComboBox 控制項（[按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-vb/_static/image2.png)）

我們會使用 ComboBox 控制項來顯示靜態選項清單。 使用者可以從下列三個選項的清單中，選取其食物的特定 spiciness 層級： [輕度]、[中] 和 [熱門] （請參閱 [圖 2]）。

[![從專案的靜態清單中選取](how-do-i-use-the-combobox-control-vb/_static/image2.jpg)](how-do-i-use-the-combobox-control-vb/_static/image3.png)

**圖 02**：從靜態專案清單中選取（[按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-vb/_static/image4.png)）

有兩種方式可以將這些加入宣告 ComboBox 控制項。 首先，當滑鼠游標停留在設計檢視中的控制項上，然後開啟專案編輯器（請參閱 [圖 3]）時，請選取 [編輯選項] 工作選項。

[編輯 ComboBox 專案 ![](how-do-i-use-the-combobox-control-vb/_static/image3.jpg)](how-do-i-use-the-combobox-control-vb/_static/image5.png)

**圖 03**：編輯 ComboBox 專案（[按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-vb/_static/image6.png)）

第二個選項是在來源視圖的 [開頭] 和 [關閉] &lt;[asp：] ComboBox&gt; 標記之間新增專案清單。 [清單 1] 中的頁面包含已更新的 ComboBox，其中含有專案的清單。

**清單 1-靜態 .aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-vb/samples/sample1.aspx)]

當您開啟 [清單 1] 中的頁面時，您可以從下拉式方塊中選取其中一個既有的選項。 換句話說，ComboBox 的運作方式就像 DropDownList 控制項一樣。

不過，您也可以選擇輸入不在現有清單中的新選擇（例如，超級 Spicy）。 因此，ComboBox 也適用于 TextBox 控制項。

不論您是選擇既有的專案，還是輸入自訂專案，當您提交表單時，您的選擇都會出現在 [標籤] 控制項中。 當您提交表單時，btnSubmit\_按一下 處理常式 會執行並更新標籤（請參閱 圖 4）。

[![顯示選取的專案](how-do-i-use-the-combobox-control-vb/_static/image4.jpg)](how-do-i-use-the-combobox-control-vb/_static/image7.png)

**圖 04**：顯示選取的專案（[按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-vb/_static/image8.png)）

在提交表單之後，ComboBox 可支援與 DropDownList 控制項相同的屬性，以便用來抓取選取的專案：

- SelectedItem：顯示所選取專案之 Text 屬性的值。
- SelectedItem：顯示所選取專案的 Value 屬性值，或顯示在 ComboBox 中輸入的文字。
- SelectedValue-與 SelectedItem 相同，不同之處在于此屬性可讓您指定預設（初始）選取的專案。

如果您在 ComboBox 中輸入自訂選擇，則會將自訂選擇指派給 SelectedItem 和 SelectedItem 屬性。

## <a name="selecting-the-list-of-items-from-the-database"></a>從資料庫中選取專案清單

您可以從資料庫中取出下拉式方塊所顯示的專案清單。 例如，您可以將 ComboBox 系結至 SqlDataSource 控制項、ObjectDataSource 控制項、LinqDataSource 或 EntityDataSource。

假設您想要在 ComboBox 中顯示電影清單。 您想要從電影資料庫資料表中取出電影清單。 請依照下列步驟：

1. 建立名為「電影 .aspx」的頁面
2. 將 scriptmanager 控制項從 [工具箱] 中的 [AJAX 延伸模組] 索引標籤拖曳到頁面上，將其新增至頁面。
3. 將下拉式方塊拖曳至頁面上，將 ComboBox 控制項加入至頁面。
4. 在設計檢視中，將滑鼠停留在 ComboBox 控制項上方，然後選取 [**選擇資料來源**] 工作選項（請參閱 [圖 5]）。 [資料來源設定] 已啟動。
5. 在 [**選擇資料來源**] 步驟中，選取 [&lt;新增資料來源&gt;] 選項。
6. 在 [**選擇資料來源類型**] 步驟中，選取 [資料庫]。
7. 在 [**選擇您的資料連線**] 步驟中，選取您的資料庫（例如，MoviesDB）。
8. 在 [將**連接字串儲存到應用程式佈建檔**] 步驟中，選取儲存連接字串的選項。
9. 在 [**設定 Select 語句**] 步驟中，選取 [電影資料庫] 資料表並選取所有資料行。
10. 在 [**測試查詢**] 步驟中，按一下 [完成] 按鈕。
11. 回到 [**選擇資料來源**] 步驟，選取要顯示之欄位的 [標題] 資料行，以及資料欄位的 [識別碼] 資料行（請參閱 [圖]）。
12. 按一下 [確定] 按鈕以關閉嚮導。

[選擇資料來源 ![](how-do-i-use-the-combobox-control-vb/_static/image5.jpg)](how-do-i-use-the-combobox-control-vb/_static/image9.png)

**圖 05**：選擇資料來源（[按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-vb/_static/image10.png)）

[選擇 [資料文字] 和 [值] 欄位 ![](how-do-i-use-the-combobox-control-vb/_static/image6.jpg)](how-do-i-use-the-combobox-control-vb/_static/image11.png)

**圖 06**：選擇 [資料] 文字和 [值] 欄位（[按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-vb/_static/image12.png)）

完成上述步驟之後，ComboBox 會系結至代表電影資料庫資料表中電影的 SqlDataSource 控制項。 頁面的來源看起來像是 [清單 2] （我清除了一些小部分的格式）。

**清單 2-電影 .aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-vb/samples/sample2.aspx)]

請注意，ComboBox 控制項具有指向 SqlDataSource 控制項的 DataSourceID 屬性。 當您在瀏覽器中開啟頁面時，會顯示資料庫中的電影清單（請參閱 [圖 7]）。 您可以從清單中挑選電影，或在下拉式方塊中輸入電影來進入新電影。

[顯示電影清單 ![](how-do-i-use-the-combobox-control-vb/_static/image7.jpg)](how-do-i-use-the-combobox-control-vb/_static/image13.png)

**圖 07**：顯示電影清單（[按一下以觀看完整大小的影像](how-do-i-use-the-combobox-control-vb/_static/image14.png)）

## <a name="setting-the-dropdownstyle"></a>設定 DropDownStyle

您可以使用 ComboBox DropDownStyle 屬性來變更 ComboBox 的行為。 這個屬性會接受可能的值：

- 下拉式清單-（預設值）當您按一下箭號時，ComboBox 會顯示下拉式清單，而您可以輸入自訂值。
- 簡單-ComboBox 會自動顯示下拉式清單，您可以輸入自訂值。
- DropDownList-ComboBox 的運作方式就像 DropDownList 控制項一樣。

下拉式清單和簡單的不同之處在于顯示專案清單的時間。 在簡單的情況下，當您將焦點移至 ComboBox 時，會立即顯示清單。 在下拉式清單中，您必須按一下箭號以查看專案的清單。

DropDownList 值會使 ComboBox 控制項的作用就像標準 DropDownList 控制項一樣。 不過，這裡有一個重要的差異。 較舊版本的 Internet Explorer 會顯示具有無限 z 索引的 DropDownList 控制項，因此控制項會顯示在其前方的任何控制項前面。 由於 ComboBox 會轉譯 HTML &lt;div&gt; 標記，而不是 HTML &lt;選取 [&gt; 標記]，ComboBox 會正確遵循 z 順序。

## <a name="setting-the-autocompletemode"></a>設定 AutoCompleteMode

您可以使用 ComboBox AutoCompleteMode 屬性，指定當有人在 ComboBox 中輸入文字時，會發生什麼事。 這個屬性會接受下列可能的值：

- 無-（預設值） ComboBox 不會提供任何自動完成行為。
- 建議-下拉式方塊會顯示清單，並反白顯示清單中的相符專案（請參閱 [圖 8]）。
- Append-下拉式方塊不會顯示清單，而且它會將清單中的相符專案附加至您所輸入的內容（請參閱 [圖 9]）。
- SuggestAppend-ComboBox 會顯示清單，並將清單中的相符專案附加至您所輸入的內容（請參閱 [圖 10]）。

[![ComboBox 提出建議](how-do-i-use-the-combobox-control-vb/_static/image8.jpg)](how-do-i-use-the-combobox-control-vb/_static/image15.png)

**圖 08**： ComboBox 會提出建議（[按一下以觀看完整大小的影像](how-do-i-use-the-combobox-control-vb/_static/image16.png)）

[![ComboBox 會附加符合的文字](how-do-i-use-the-combobox-control-vb/_static/image9.jpg)](how-do-i-use-the-combobox-control-vb/_static/image17.png)

**圖 09**： ComboBox 會附加符合的文字（[按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-vb/_static/image18.png)）

[![ComboBox 建議和附加的](how-do-i-use-the-combobox-control-vb/_static/image10.jpg)](how-do-i-use-the-combobox-control-vb/_static/image19.png)

**圖 10**：下拉式方塊的建議和附加（[按一下以觀看完整大小的影像](how-do-i-use-the-combobox-control-vb/_static/image20.png)）

## <a name="summary"></a>總結

在本教學課程中，您已瞭解如何使用 ComboBox 控制項來顯示一組固定的專案。 我們將 ComboBox 控制項系結至一組靜態專案，並系結至資料庫資料表。 最後，您已瞭解如何藉由設定 DropDownStyle 和 AutoCompleteMode 屬性來修改 ComboBox 的行為。

> [!div class="step-by-step"]
> [上一篇](how-do-i-use-the-combobox-control-cs.md)
