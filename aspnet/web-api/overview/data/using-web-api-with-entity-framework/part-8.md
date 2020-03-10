---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-8
title: 顯示專案詳細資料 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 75ef94b1-bbec-4681-9210-452dba816144
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-8
msc.type: authoredcontent
ms.openlocfilehash: 3f48c5ad73ceb9a4873fbbb621b518553a498966
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557320"
---
# <a name="display-item-details"></a>顯示項目詳細資料

由[Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://github.com/MikeWasson/BookService)

在本節中，您將新增可查看每一本書詳細資料的功能。 在 node.js 中，將下列程式碼新增至視圖模型：

[!code-javascript[Main](part-8/samples/sample1.js)]

在 Views/Home/Index. cshtml 中，將資料繫結項新增至 Details 連結：

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

這會將 &lt;&gt; 元素的 click 處理常式系結至視圖模型上的 `getBookDetail` 函數。

在相同的檔案中，取代下列標記：

[!code-html[Main](part-8/samples/sample3.html)]

取代為這個：

[!code-html[Main](part-8/samples/sample4.html)]

此標記會建立資料系結至視圖模型中可觀察之 `detail` 屬性的資料表。

"&lt;!--ko--&gt;&quot; 語法可讓您在 DOM 元素之外包含挖式系結。 在此情況下，`if` 系結只會在 `details` 為非 null 時，才會顯示標記的區段。

[!code-html[Main](part-8/samples/sample5.html)]

現在，如果您執行應用程式，然後按一下其中一個 &quot;詳細資料&quot; 連結，應用程式將會顯示書籍詳細資料。

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

> [!div class="step-by-step"]
> [上一頁](part-7.md)
> [下一頁](part-9.md)
