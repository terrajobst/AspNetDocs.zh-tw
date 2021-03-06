---
uid: web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
title: 將商務邏輯層新增至使用模型系結和 web forms 的專案 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程系列示範使用模型系結搭配 ASP.NET Web Forms 專案的基本層面。 模型系結讓資料互動更為直接-。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 7ef664b3-1cc8-4cbf-bb18-9f0f3a3ada2b
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
msc.type: authoredcontent
ms.openlocfilehash: a824d06d3781e11706f2a48d44ea3ad89bdb7c8b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634831"
---
# <a name="adding-business-logic-layer-to-a-project-that-uses-model-binding-and-web-forms"></a>將商務邏輯層新增至使用模型系結和 web form 的專案

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本教學課程系列示範使用模型系結搭配 ASP.NET Web Forms 專案的基本層面。 模型系結可讓資料互動比處理資料來源物件（例如 ObjectDataSource 或 SqlDataSource）更直接。 此系列從簡介材料開始，並在稍後的教學課程中移至更先進的概念。
> 
> 本教學課程說明如何搭配商務邏輯層使用模型系結。 您將設定 OnCallingDataMethods 成員，以指定目前頁面以外的物件用來呼叫資料方法。
> 
> 本教學課程是根據在系列的[先前](retrieving-data.md)部分中所建立的專案來建立。
> 
> 您可以[download](https://go.microsoft.com/fwlink/?LinkId=286116)在或 VB 中C#下載完整專案。 可下載的程式碼適用于 Visual Studio 2012 或 Visual Studio 2013。 它會使用 Visual Studio 2012 範本，這與本教學課程中所顯示的 Visual Studio 2013 範本稍有不同。

## <a name="what-youll-build"></a>您將建立的內容

模型系結可讓您將資料互動程式碼放在網頁的程式碼後置檔案或個別的商業邏輯類別中。 先前的教學課程已示範如何將程式碼後置檔案用於資料互動程式碼。 這種方法適用于小型網站，但在維護大型網站時，可能會導致程式碼重複和更困難。 您也可能很難以以程式設計方式測試位於程式碼後置檔案中的程式碼，因為沒有抽象層。

若要集中資料互動程式碼，您可以建立商務邏輯層，其中包含與資料互動的所有邏輯。 然後從您的網頁呼叫商務邏輯層。 本教學課程示範如何將您在先前的教學課程中撰寫的所有程式碼移至商務邏輯層，然後從頁面使用該程式碼。

在本教學課程中，您將會：

1. 將程式碼後置檔案中的程式碼移至商務邏輯層
2. 變更您的資料繫結控制項，以呼叫商務邏輯層中的方法

## <a name="create-business-logic-layer"></a>建立商務邏輯層

現在，您將建立從網頁呼叫的類別。 此類別中的方法看起來類似于您在先前的教學課程中使用的方法，並包含值提供者屬性。

首先，新增名為**BLL**的新資料夾。

![新增資料夾](adding-business-logic-layer/_static/image1.png)

在 [BLL] 資料夾中，建立名為**SchoolBL.cs**的新類別。 它將包含原本位於程式碼後置檔案中的所有資料作業。 方法幾乎與程式碼後置檔案中的方法相同，但會包含一些變更。

要注意的最重要變更是您不再從**Page**類別的實例中執行程式碼。 Page 類別包含**TryUpdateModel**方法和**ModelState**屬性。 當此程式碼移至商務邏輯層時，您就不再有 Page 類別的實例可以呼叫這些成員。 若要解決此問題，您必須將**ModelMethodCoNtext**參數新增至任何存取 TryUpdateModel 或 ModelState 的方法。 您可以使用這個 ModelMethodCoNtext 參數來呼叫 TryUpdateModel 或取出 ModelState。 您不需要變更網頁中的任何專案來考慮這個新的參數。

將 SchoolBL.cs 中的程式碼取代為下列程式碼。

[!code-csharp[Main](adding-business-logic-layer/samples/sample1.cs)]

## <a name="revise-existing-pages-to-retrieve-data-from-business-logic-layer"></a>修訂現有頁面以從商務邏輯層取出資料

最後，您會將 AddStudent 的頁面從程式碼後置檔案中的查詢轉換成使用商務邏輯層。

在學生、AddStudent 和課程的程式碼後置檔案中，刪除或批註下列查詢方法：

- studentsGrid\_的
- studentsGrid\_UpdateItem
- studentsGrid\_DeleteItem
- addStudentForm\_InsertItem
- coursesGrid\_的

在程式碼後置檔案中，您現在不應該有與資料作業相關的程式碼。

**OnCallingDataMethods**事件處理常式可讓您指定要用於資料方法的物件。 在 [student] 中，為該事件處理常式新增一個值，並將資料方法的名稱變更為商務邏輯類別中的方法名稱。

[!code-aspx[Main](adding-business-logic-layer/samples/sample2.aspx?highlight=3-4,8)]

在 default.aspx 的程式碼後置檔案中，定義 CallingDataMethods 事件的事件處理常式。 在這個事件處理常式中，您可以指定資料作業的商務邏輯類別。

[!code-csharp[Main](adding-business-logic-layer/samples/sample3.cs)]

在 AddStudent 中進行類似的變更。

[!code-aspx[Main](adding-business-logic-layer/samples/sample4.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample5.cs)]

在 default.aspx 中，進行類似的變更。

[!code-aspx[Main](adding-business-logic-layer/samples/sample6.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample7.cs)]

執行應用程式，並注意所有頁面的運作方式都與先前相同。 驗證邏輯也會正確運作。

## <a name="conclusion"></a>結論

在本教學課程中，您會重新結構化應用程式以使用資料存取層和商務邏輯層。 您指定資料控制項使用的物件不是資料作業的目前頁面。

> [!div class="step-by-step"]
> [上一步](using-query-string-values-to-retrieve-data.md)
