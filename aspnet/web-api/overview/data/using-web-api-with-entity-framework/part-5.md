---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-5
title: 建立資料傳輸物件（Dto） |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0fd07176-b74b-48f0-9fac-0f02e3ffa213
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-5
msc.type: authoredcontent
ms.openlocfilehash: fc0463420207eba764014b8ec7123c5150e38247
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445765"
---
# <a name="create-data-transfer-objects-dtos"></a>建立資料傳輸物件 (DTO)

由[Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://github.com/MikeWasson/BookService)

現在，我們的 Web API 會向用戶端公開資料庫實體。 用戶端會接收直接對應至資料庫資料表的資料。 不過，這不一定是不錯的主意。 有時候您會想要變更傳送給用戶端之資料的圖形。 例如，您可能會要：

- 移除迴圈參考（請參閱上一節）。
- 隱藏用戶端不應查看的特定屬性。
- 省略某些屬性，以減少承載大小。
- 將包含嵌套物件的物件圖形壓平合併，使其更方便用戶端。
- 避免「過度張貼」的弱點。 （如需過度張貼的討論，請參閱[模型驗證](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md)。）
- 將您的服務層與您的資料庫層分離。

若要完成此動作，您可以定義*資料傳輸物件*（DTO）。 DTO 是一種物件，可定義如何透過網路來傳送資料。 我們來看一下該如何與 Book 實體搭配運作。 在 [模型] 資料夾中，新增兩個 DTO 類別：

[!code-csharp[Main](part-5/samples/sample1.cs)]

`BookDetailDto` 類別包含書籍模型中的所有屬性，不同之處在于 `AuthorName` 是會保存作者名稱的字串。 `BookDto` 類別包含來自 `BookDetailDto`的屬性子集。

接下來，將 `BooksController` 類別中的兩個 GET 方法取代為傳回 Dto 的版本。 我們將使用 LINQ **Select**語句，從書籍實體轉換成 dto。

[!code-csharp[Main](part-5/samples/sample2.cs)]

以下是新的 `GetBooks` 方法所產生的 SQL。 您可以看到 EF 將 LINQ **Select**轉換成 SQL select 語句。

[!code-sql[Main](part-5/samples/sample3.sql)]

最後，修改 `PostBook` 方法以傳回 DTO。

[!code-csharp[Main](part-5/samples/sample4.cs)]

> [!NOTE]
> 在本教學課程中，我們會在程式碼中以手動方式轉換為 Dto。 另一個選項是使用程式庫（例如[AutoMapper](http://automapper.org/) ）來自動處理轉換。
> 
> [!div class="step-by-step"]
> [上一頁](part-4.md)
> [下一頁](part-6.md)
