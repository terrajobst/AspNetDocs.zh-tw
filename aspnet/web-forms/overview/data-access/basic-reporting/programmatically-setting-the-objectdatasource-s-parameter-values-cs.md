---
uid: web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs
title: 以程式設計方式設定 ObjectDataSource 的參數C#值（） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將探討如何將方法新增至我們的 DAL 和 BLL，以接受單一輸入參數並傳回資料。 此範例會設定此參數 。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 1c4588bb-255d-4088-b319-5208da756f4d
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs
msc.type: authoredcontent
ms.openlocfilehash: 8aa57172abcfc779fa74b128ad76d42c41dc5b98
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78577081"
---
# <a name="programmatically-setting-the-objectdatasources-parameter-values-c"></a>以程式設計方式設定 ObjectDataSource 的參數值 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_6_CS.exe)或[下載 PDF](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/datatutorial06cs1.pdf)

> 在本教學課程中，我們將探討如何將方法新增至我們的 DAL 和 BLL，以接受單一輸入參數並傳回資料。 此範例會以程式設計方式設定此參數。

## <a name="introduction"></a>簡介

如[先前的教學](declarative-parameters-cs.md)課程中所見，有許多選項可用於以宣告方式將參數值傳遞給 ObjectDataSource 的方法。 如果參數值為硬式編碼，則來自網頁上的 Web 控制項，或位於資料來源 `Parameter` 物件可讀取的任何其他來源中，例如，該值可以系結至輸入參數，而不需要撰寫任何一行程式碼。

不過有時候，當參數值來自某個內建資料來源 `Parameter` 物件的部分來源時，就可能會發生此情況。 如果我們的網站支援的使用者帳戶，我們可能會想要根據目前登入的訪客使用者識別碼來設定參數。 或者，我們可能需要自訂參數值，然後再將它傳送給 ObjectDataSource 的基礎物件的方法。

每當叫用 ObjectDataSource 的 `Select` 方法時，ObjectDataSource 就會先引發其[選取的事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting%28VS.80%29.aspx)。 接著會叫用 ObjectDataSource 的基礎物件的方法。 一旦完成，ObjectDataSource 的[選取事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selected%28VS.80%29.aspx)就會引發（[圖 1] 說明這一系列的事件）。 您可以在 `Selecting` 事件的事件處理常式中，設定或自訂傳遞至 ObjectDataSource 基礎物件之方法的參數值。

[![ObjectDataSource 的選取和選取的事件會在其基礎物件的方法叫用前後引發](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image2.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image1.png)

**圖 1**： ObjectDataSource 的 `Selected` 和 `Selecting` 事件會在其基礎物件的方法被叫用前後引發（[按一下以查看完整大小的影像](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image3.png)）

在本教學課程中，我們將探討如何將方法新增至我們的 DAL 和 BLL，以接受 `Month``int` 類型的單一輸入參數，並傳回 `EmployeesDataTable` 物件，並在指定的 `Month`中，填入其雇用周年的員工。 我們的範例會根據目前月份以程式設計方式設定此參數，並顯示「本月員工周年紀念日」的清單。

現在就開始吧！

## <a name="step-1-adding-a-method-toemployeestableadapter"></a>步驟1：將方法加入至`EmployeesTableAdapter`

在第一個範例中，我們需要新增一種方法來抓取 `HireDate` 在指定月份中發生的員工。 為了根據我們的架構提供這項功能，我們必須先在 `EmployeesTableAdapter` 中建立對應至適當 SQL 語句的方法。 若要完成這項操作，請從開啟 Northwind 類型資料集開始。 以滑鼠右鍵按一下 [`EmployeesTableAdapter`] 標籤，然後選擇 [加入查詢]。

[![將新的查詢加入至 EmployeesTableAdapter](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image5.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image4.png)

**圖 2**：將新的查詢加入至 `EmployeesTableAdapter` （[按一下以查看完整大小的影像](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image6.png)）

加入宣告會傳回資料列的 SQL 語句。 當您到達 [指定 `SELECT` 語句] 畫面時，`EmployeesTableAdapter` 的預設 `SELECT` 語句就已載入。 只要在 `WHERE` 子句中新增： `WHERE DATEPART(m, HireDate) = @Month`。 [DATEPART](https://msdn.microsoft.com/library/ms174420.aspx)是一個 t-sql 函數，會傳回 `datetime` 類型的特定日期部分;在此情況下，我們會使用 `DATEPART` 來傳回 `HireDate` 資料行的月份。

[![只傳回 [雇用日期] 資料行小於或等於 @HiredBeforeDate 參數的資料列](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image8.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image7.png)

**圖 3**：只傳回 `HireDate` 資料行小於或等於 `@HiredBeforeDate` 參數的資料列（[按一下以查看完整大小的影像](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image9.png)）

最後，將 `FillBy` 和 `GetDataBy` 方法名稱分別變更為 `FillByHiredDateMonth` 和 `GetEmployeesByHiredDateMonth`。

[![選擇比 FillBy 和 GetDataBy 更適當的方法名稱](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image11.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image10.png)

**圖 4**：選擇更適當的方法名稱，而不是 `FillBy` 和 `GetDataBy` （[按一下以查看完整大小的影像](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image12.png)）

按一下 [完成] 以完成嚮導，並返回資料集的設計介面。 `EmployeesTableAdapter` 現在應包含一組新的方法，供您存取在指定月份雇用的員工。

[![新方法會出現在資料集的 Design Surface](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image14.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image13.png)

**圖 5**：新的方法會出現在資料集的 Design Surface 中（[按一下以查看完整大小的影像](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image15.png)）

## <a name="step-2-adding-thegetemployeesbyhireddatemonthmonthmethod-to-the-business-logic-layer"></a>步驟2：將`GetEmployeesByHiredDateMonth(month)`方法加入至商務邏輯層

因為我們的應用程式架構會針對商務邏輯和資料存取邏輯使用不同的層級，所以我們需要將方法新增至我們的 BLL，以向下呼叫 DAL，以取出在指定日期之前雇用的員工。 開啟 `EmployeesBLL.cs` 檔案，並新增下列方法：

[!code-csharp[Main](programmatically-setting-the-objectdatasource-s-parameter-values-cs/samples/sample1.cs)]

就像這個類別中的其他方法一樣，`GetEmployeesByHiredDateMonth(month)` 只是向下呼叫 DAL 並傳回結果。

## <a name="step-3-displaying-employees-whose-hiring-anniversary-is-this-month"></a>步驟3：顯示此月份雇用周年年度的員工

此範例的最後一個步驟，是顯示在本月雇用周年的員工。 首先，將 GridView 新增至 [`BasicReporting`] 資料夾中的 [`ProgrammaticParams.aspx`] 頁面，並加入新的 ObjectDataSource 作為其資料來源。 將 ObjectDataSource 設定為使用 `EmployeesBLL` 類別，並將 `SelectMethod` 設為 `GetEmployeesByHiredDateMonth(month)`。

[![使用 EmployeesBLL 類別](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image17.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image16.png)

**圖 6**：使用 `EmployeesBLL` 類別（[按一下以觀看完整大小的影像](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image18.png)）

[![從 GetEmployeesByHiredDateMonth （month）方法選取](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image20.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image19.png)

**圖 7**：從 `GetEmployeesByHiredDateMonth(month)` 方法中選取（[按一下以查看完整大小的影像](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image21.png)）

最後一個畫面會要求我們提供 `month` 參數值的來源。 因為我們將以程式設計方式設定此值，所以請將參數來源設定為預設值 None 選項，然後按一下 [完成]。

[![讓參數來源設定為 [無]](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image23.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image22.png)

**圖 8**：將 [參數來源] 設定為 [無] （[按一下以查看完整大小的影像](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image24.png)）

這會在 ObjectDataSource 的 `SelectParameters` 集合中建立未指定值的 `Parameter` 物件。

[!code-aspx[Main](programmatically-setting-the-objectdatasource-s-parameter-values-cs/samples/sample2.aspx)]

若要以程式設計方式設定這個值，我們需要為 ObjectDataSource 的 `Selecting` 事件建立事件處理常式。 若要完成此動作，請移至設計檢視，然後按兩下 [ObjectDataSource]。 或者，選取 [ObjectDataSource]，移至 [屬性視窗]，然後按一下閃電圖示。 接下來，在 [`Selecting`] 事件旁邊的文字方塊中按兩下，或輸入您要使用的事件處理常式名稱。

![按一下 [屬性] 視窗中的閃電圖示，以列出 Web 控制項的事件](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image25.png)

**圖 9**：按一下 [屬性] 視窗中的閃電圖示，以列出 Web 控制項的事件

這兩種方法都會將 ObjectDataSource 的 `Selecting` 事件的新事件處理常式加入至頁面的程式碼後置類別。 在這個事件處理常式中，我們可以使用 `e.InputParameters[parameterName]`來讀取和寫入參數值，其中 *`parameterName`* 是 `<asp:Parameter>` 標記中 `Name` 屬性的值（`InputParameters` 集合也可以編制索引序數，如同 `e.InputParameters[index]`）。 若要將 `month` 參數設定為當月，請將下列專案新增至 `Selecting` 事件處理常式：

[!code-csharp[Main](programmatically-setting-the-objectdatasource-s-parameter-values-cs/samples/sample3.cs)]

透過瀏覽器造訪此頁面時，我們可以看到，只有一位員工在本月（3月）劉娜 Callahan，這是自1994起的公司。

[![顯示此月份周年紀念日的員工](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image27.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image26.png)

[**圖 10**] 顯示此月份周年紀念日的員工（[按一下以觀看完整大小的影像](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image28.png)）

## <a name="summary"></a>總結

雖然 ObjectDataSource 的參數值通常可以透過宣告方式設定，而不需要一行程式碼，但很容易就能以程式設計方式設定參數值。 我們只需要建立 ObjectDataSource 的 `Selecting` 事件的事件處理常式，這會在叫用基礎物件的方法之前引發，並透過 `InputParameters` 集合手動設定一或多個參數的值。

本教學課程會結束 [基本報告] 區段。 [下一個教學](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md)課程會開始進行篩選和主版-詳細資料案例一節，我們將在其中探討允許造訪者篩選資料，並向下切入至詳細報表的技術。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Hilton Giesenow。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](declarative-parameters-cs.md)
> [下一頁](displaying-data-with-the-objectdatasource-vb.md)
