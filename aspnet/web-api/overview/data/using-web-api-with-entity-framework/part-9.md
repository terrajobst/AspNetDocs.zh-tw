---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-9
title: 將新專案新增至資料庫 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0967c29e-e124-4db0-a788-c45d0ff5aff2
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-9
msc.type: authoredcontent
ms.openlocfilehash: 692269a2c11e529af78f24feca74bba704b5b54b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557285"
---
# <a name="add-a-new-item-to-the-database"></a>將新項目新增至資料庫

由[Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://github.com/MikeWasson/BookService)

在本節中，您將新增可讓使用者建立新書籍的功能。 在 node.js 中，將下列程式碼新增至視圖模型：

[!code-javascript[Main](part-9/samples/sample1.js)]

在 [Index. cshtml] 中，取代下列標記：

[!code-html[Main](part-9/samples/sample2.html)]

成為：

[!code-html[Main](part-9/samples/sample3.html)]

此標記會建立表單，以提交新的作者。 [作者] 下拉式清單的值會系結至 view 模型中 `authors` 可觀察的資料。 針對其他表單輸入，值會系結至視圖模型的 `newBook` 屬性。

表單上的提交處理常式會系結至 `addBook` 函數：

[!code-html[Main](part-9/samples/sample4.html)]

`addBook` 函式會讀取資料系結表單輸入的目前值，以建立 JSON 物件。 然後，它會將 JSON 物件張貼到 `/api/books`。

> [!div class="step-by-step"]
> [上一頁](part-8.md)
> [下一頁](part-10.md)
