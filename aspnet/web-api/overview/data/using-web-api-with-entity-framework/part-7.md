---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-7
title: 建立視圖（UI） |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: b2445062-a1fe-4133-8994-f510280f6d9a
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-7
msc.type: authoredcontent
ms.openlocfilehash: 62c4523c2c6fb399cfbc3716309a1379996d601c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557299"
---
# <a name="create-the-view-ui"></a>建立檢視 (UI)

由[Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://github.com/MikeWasson/BookService)

在本節中，您將開始定義應用程式的 HTML，並在 HTML 和 view 模型之間加入資料系結。

開啟檔案 Views/Home/Index. cshtml。 將該檔案的整個內容取代為下列程式。

[!code-cshtml[Main](part-7/samples/sample1.cshtml)]

大部分的 `div` 元素都是針對[啟動](http://getbootstrap.com/)程式樣式。 重要的專案是具有 `data-bind` 屬性的元素。 這個屬性會將 HTML 連結至視圖模型。

例如:

[!code-html[Main](part-7/samples/sample2.html)]

在此範例中，&quot;`text`&quot; 系結會導致 `<p>` 專案顯示視圖模型中 `error` 屬性的值。 回想一下，`error` 宣告為 `ko.observable`：

[!code-javascript[Main](part-7/samples/sample3.js)]

每當有新的值指派給 `error`時，挖不會更新 `<p>` 元素中的文字。

`foreach` 系結會告訴挖的會在 `books` 陣列的內容中執行迴圈。 針對陣列中的每個專案，挖的會建立新的 &lt;li&gt; 元素。 `foreach` 內容中的系結會參考陣列專案上的屬性。 例如:

[!code-html[Main](part-7/samples/sample4.html)]

在這裡，`text` 系結會讀取每一本書的作者屬性。

如果您現在執行應用程式，它看起來應該像這樣：

![](part-7/_static/image1.png)

在頁面載入之後，會以非同步方式載入書籍清單。 目前，&quot;詳細資料&quot; 連結無法運作。 我們將在下一節新增這項功能。

> [!div class="step-by-step"]
> [上一頁](part-6.md)
> [下一頁](part-8.md)
