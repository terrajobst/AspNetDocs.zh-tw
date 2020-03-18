---
uid: web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
title: 使用模型系結和 web forms 排序、分頁及篩選資料 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程系列示範使用模型系結搭配 ASP.NET Web Forms 專案的基本層面。 模型系結讓資料互動更為直接-。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 266e7866-e327-4687-b29d-627a0925e87d
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
msc.type: authoredcontent
ms.openlocfilehash: f8e64392af6110f36c6af98c4e4e9481c94a0d82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78548059"
---
# <a name="sorting-paging-and-filtering-data-with-model-binding-and-web-forms"></a>使用模型系結和 web forms 排序、分頁及篩選資料

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本教學課程系列示範使用模型系結搭配 ASP.NET Web Forms 專案的基本層面。 模型系結可讓資料互動比處理資料來源物件（例如 ObjectDataSource 或 SqlDataSource）更直接。 此系列從簡介材料開始，並在稍後的教學課程中移至更先進的概念。
> 
> 本教學課程說明如何透過模型系結來加入排序、分頁和篩選資料。
> 
> 本教學課程是以系列第一個[部分](retrieving-data.md)中所建立的專案為基礎。
> 
> 您可以[download](https://go.microsoft.com/fwlink/?LinkId=286116)在或 VB 中C#下載完整專案。 可下載的程式碼適用于 Visual Studio 2012 或 Visual Studio 2013。 它會使用 Visual Studio 2012 範本，這與本教學課程中所顯示的 Visual Studio 2013 範本稍有不同。

## <a name="what-youll-build"></a>您將建立的內容

在本教學課程中，您將會：

1. 啟用資料的排序和分頁
2. 根據使用者的選取專案來啟用資料篩選

## <a name="add-sorting"></a>新增排序

在 GridView 中啟用排序非常簡單。 在 Student .aspx 檔案中，直接在 GridView 中將**AllowSorting**設定為**true** 。 當 DataField 自動使用時，您不需要為每個資料行設定**SortExpression**值。 GridView 會修改查詢，以包含依據選取的值來排序資料。 下列反白顯示的程式碼顯示啟用排序所需的加法。

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample1.aspx?highlight=5)]

執行 web 應用程式，並依據不同資料行中的值來測試排序 student 記錄。

![排序學生](sorting-paging-and-filtering-data/_static/image2.png)

## <a name="add-paging"></a>新增分頁

啟用分頁也非常簡單。 在 GridView 中，將**AllowPaging**屬性設定為**true** ，並將**PageSize**屬性設為您想要在每個頁面上顯示的記錄數目。 在本教學課程中，您可以將它設定為4。

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample2.aspx?highlight=5)]

執行 web 應用程式，並注意現在記錄會分割成多個頁面，而不會在單一頁面上顯示超過4筆記錄。

![新增分頁](sorting-paging-and-filtering-data/_static/image4.png)

延遲的查詢執行可改善應用程式的效率。 GridView 不會抓取整個資料集，而是修改查詢，只抓取目前頁面的記錄。

## <a name="filter-records-by-user-selection"></a>依使用者選擇篩選記錄

模型系結會加入數個屬性，可讓您指定如何在模型系結方法中設定參數的值。 這些屬性位於**ModelBinding**命名空間中。 其中包括：

- 控制項
- Cookie
- 表單
- 設定檔
- QueryString
- RouteData
- 工作階段
- UserProfile
- ViewState

在本教學課程中，您將使用控制項的值來篩選要在 GridView 中顯示的記錄。 您會將**控制項**屬性新增至您稍早建立的查詢方法。 在[稍後](using-query-string-values-to-retrieve-data.md)的教學課程中，您會將**QueryString**屬性套用至參數，以指定參數值來自查詢字串值。

首先，在 ValidationSummary 上，新增下拉式清單來篩選顯示的學生。

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample3.aspx?highlight=3-11)]

在程式碼後置檔案中，修改 select 方法以接收控制項的值，並將參數的名稱設定為提供值的控制項名稱。

您必須為**ModelBinding**命名空間加入**using**語句，才能解析控制項屬性。

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample4.cs)]

下列程式碼顯示 select 方法重新運作，以根據下拉式清單的值來篩選傳回的資料。 在參數之前加入控制項屬性指定此參數的值來自具有相同名稱的控制項。

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample5.cs)]

執行 web 應用程式，並從下拉式清單中選取不同的值，以篩選學生清單。

![篩選學生](sorting-paging-and-filtering-data/_static/image6.png)

## <a name="conclusion"></a>結論

在本教學課程中，您已啟用資料的排序和分頁。 您也啟用了依控制項的值來篩選資料。

在下一個[教學](integrating-jquery-ui.md)課程中，您將會藉由將 JQuery ui widget 整合至動態資料範本來增強 UI。

> [!div class="step-by-step"]
> [上一頁](updating-deleting-and-creating-data.md)
> [下一頁](integrating-jquery-ui.md)
