---
uid: web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
title: 使用查詢字串值來篩選模型系結和 web form 的資料 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程系列示範使用模型系結搭配 ASP.NET Web Forms 專案的基本層面。 模型系結讓資料互動更為直接-。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: b90978bd-795d-4871-9ade-1671caff5730
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
msc.type: authoredcontent
ms.openlocfilehash: 143ddcb40b576a3129e659b90bfc8321c061a547
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639094"
---
# <a name="using-query-string-values-to-filter-data-with-model-binding-and-web-forms"></a>使用查詢字串值，以模型系結和 web form 來篩選資料

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本教學課程系列示範使用模型系結搭配 ASP.NET Web Forms 專案的基本層面。 模型系結可讓資料互動比處理資料來源物件（例如 ObjectDataSource 或 SqlDataSource）更直接。 此系列從簡介材料開始，並在稍後的教學課程中移至更先進的概念。
> 
> 本教學課程說明如何在查詢字串中傳遞值，並使用該值透過模型系結來抓取資料。
> 
> 本教學課程是根據在系列的[先前](retrieving-data.md)部分中所建立的專案來建立。
> 
> 您可以[download](https://go.microsoft.com/fwlink/?LinkId=286116)在或 VB 中C#下載完整專案。 可下載的程式碼適用于 Visual Studio 2012 或 Visual Studio 2013。 它會使用 Visual Studio 2012 範本，這與本教學課程中所顯示的 Visual Studio 2013 範本稍有不同。

## <a name="what-youll-build"></a>您將建立的內容

在本教學課程中，您將會：

1. 新增頁面以顯示學生註冊的課程
2. 根據查詢字串中的值，抓取所選學生的已註冊課程
3. 將具有查詢字串值的超連結從方格視圖加入至新頁面

本教學課程中的步驟與您在先前的[教學](sorting-paging-and-filtering-data.md)課程中所做的類似，是根據下拉式清單中的使用者選擇來篩選顯示的學生。 在該教學課程中，您已使用 select 方法中的**control**屬性來指定參數值來自控制項。 在本教學課程中，您將使用 select 方法中的**QueryString**屬性來指定參數值來自查詢字串。

## <a name="add-new-page-for-displaying-a-students-courses"></a>新增用於顯示學生課程的頁面

加入新的 web 表單，以使用 [網站主要] 頁面，並將頁面命名為**課程**。

在**課程 .aspx**檔案中，新增方格視圖，以顯示所選學生的課程。

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample1.aspx)]

## <a name="define-the-select-method"></a>定義 select 方法

在**Courses.aspx.cs**中，您會使用您在方格視圖的 [ **SelectMethod** ] 屬性中指定的名稱來新增 select 方法。 在該方法中，您將定義用來抓取學生課程的查詢，並指定參數來自與參數名稱相同的查詢字串值。

首先，您必須加入下列**using**語句。

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample2.cs)]

然後，將下列程式碼新增至 Courses.aspx.cs：

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample3.cs)]

QueryString 屬性工作表示名為 StudentID 的查詢字串值會自動指派給這個方法中的參數。

## <a name="add-hyperlink-with-query-string-value"></a>使用查詢字串值新增超連結

在 [student] 的方格視圖中，您將會新增連結至新課程頁面的超連結欄位。 超連結將包含含有學生識別碼的查詢字串值。

在 [student] 中，將下欄欄位加入至 [方格視圖] 欄中的 [總點數] 欄位正下方。

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample4.aspx?highlight=7-8)]

執行應用程式，並注意方格視圖現在包含 [課程] 連結。

![新增超連結](using-query-string-values-to-retrieve-data/_static/image1.png)

當您按一下其中一個連結時，您會看到學生註冊的課程。

![顯示課程](using-query-string-values-to-retrieve-data/_static/image2.png)

## <a name="conclusion"></a>結論

在本教學課程中，您已新增包含查詢字串值的連結。 您已在 select 方法中，使用該查詢字串值做為參數值。

在下一個[教學](adding-business-logic-layer.md)課程中，您會將程式碼後置檔案中的程式碼移至商務邏輯層和資料存取層。

> [!div class="step-by-step"]
> [上一頁](integrating-jquery-ui.md)
> [下一頁](adding-business-logic-layer.md)
