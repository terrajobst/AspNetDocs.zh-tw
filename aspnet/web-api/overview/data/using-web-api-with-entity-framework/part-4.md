---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-4
title: 處理實體關聯 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: d2f5710c-23c7-40a5-9cd9-5d0516570cba
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-4
msc.type: authoredcontent
ms.openlocfilehash: be4948e5443a5eb4e1824c63dd0c445a7ee1928e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557460"
---
# <a name="handling-entity-relations"></a>處理實體關聯性

由[Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://github.com/MikeWasson/BookService)

本節說明 EF 如何載入相關實體，以及如何在模型類別中處理迴圈導覽屬性的一些詳細資料。 （本節提供背景知識，而且不需要用來完成教學課程。 如果您想要的話，請跳到[第5部分：](part-5.md)）

## <a name="eager-loading-versus-lazy-loading"></a>積極式載入與延遲載入

搭配關係資料庫使用 EF 時，請務必瞭解 EF 如何載入相關資料。

查看 EF 產生的 SQL 查詢也很有用。 若要追蹤 SQL，請將下列程式程式碼新增至 `BookServiceContext` 的函式：

[!code-csharp[Main](part-4/samples/sample1.cs)]

如果您將 GET 要求傳送至/api/books，它會傳回 JSON，如下所示：

[!code-console[Main](part-4/samples/sample2.cmd)]

您可以看到 Author 屬性為 null，即使本書包含有效的作者。 這是因為 EF 不會載入相關的作者實體。 SQL 查詢的追蹤記錄會確認下列事項：

[!code-console[Main](part-4/samples/sample3.sql)]

SELECT 語句取自 [書籍] 資料表，而且不會參考 [作者] 資料表。

以下是傳回書籍清單的 `BooksController` 類別中的方法，供您參考。

[!code-csharp[Main](part-4/samples/sample4.cs)]

我們來看一下如何傳回作者做為 JSON 資料的一部分。 有三種方式可以在 Entity Framework 中載入相關資料：積極式載入、消極式載入和明確載入。 每項技術都有取捨，因此請務必瞭解它們的運作方式。

### <a name="eager-loading"></a>積極式載入

使用*積極式載入*時，EF 會載入相關實體做為初始資料庫查詢的一部分。 若要執行積極式載入，請使用**system.object. Include**擴充方法。

[!code-csharp[Main](part-4/samples/sample5.cs)]

這會告訴 EF 將作者資料包含在查詢中。 如果您進行這類變更並執行應用程式，現在 JSON 資料看起來像這樣：

[!code-console[Main](part-4/samples/sample6.cmd)]

追蹤記錄檔會顯示 EF 在 Book 和 Author 資料表上執行了聯結。

[!code-console[Main](part-4/samples/sample7.cmd)]

### <a name="lazy-loading"></a>消極式載入

使用消極式載入時，EF 會在參考該實體的導覽屬性時，自動載入相關實體。 若要啟用消極式載入，請將導覽屬性設為 [虛擬]。 例如，在 Book 類別中：

[!code-csharp[Main](part-4/samples/sample8.cs?highlight=6)]

現在請考慮下列程式碼：

[!code-csharp[Main](part-4/samples/sample9.cs)]

啟用消極式載入時，存取 `books[0]` 上的 `Author` 屬性會導致 EF 為作者查詢資料庫。

消極式載入需要多個資料庫往返，因為 EF 會在每次抓取相關實體時傳送查詢。 一般來說，您會想要針對序列化的物件停用消極式載入。 序列化程式必須讀取模型上的所有屬性，以觸發載入相關實體。 例如，當 EF 將已啟用消極式載入的書籍清單序列化時，以下是 SQL 查詢。 您可以看到 EF 針對三個作者進行三個不同的查詢。

[!code-console[Main](part-4/samples/sample10.sql)]

有時候，您可能會想要使用消極式載入。 積極式載入可能會導致 EF 產生非常複雜的聯結。 或者，您可能需要一小部分資料的相關實體，而消極式載入會更有效率。

避免序列化問題的其中一種方法是序列化資料傳輸物件（Dto），而不是實體物件。 我稍後會在本文中說明這個方法。

### <a name="explicit-loading"></a>明確式載入

明確載入類似于消極式載入，不同之處在于您明確地取得程式碼中的相關資料。當您存取導覽屬性時，不會自動進行此動作。 明確的載入可讓您更充分掌控載入相關資料的時間，但需要額外的程式碼。 如需明確載入的詳細資訊，請參閱[載入相關實體](https://msdn.microsoft.com/data/jj574232#explicit)。

## <a name="navigation-properties-and-circular-references"></a>導覽屬性和迴圈參考

當我定義書籍和作者模型時，我在 [書籍-作者] 關聯性的 [`Book`] 類別上定義了一個導覽屬性，但是我並未定義另一個方向的導覽屬性。

如果您將對應的導覽屬性加入 `Author` 類別中，會發生什麼事？

[!code-csharp[Main](part-4/samples/sample11.cs?highlight=7)]

可惜的是，當您將模型序列化時，這會造成問題。 如果您載入相關的資料，它會建立迴圈物件圖形。

![](part-4/_static/image1.png)

當 JSON 或 XML 格式器嘗試將圖形序列化時，它會擲回例外狀況。 這兩個格式子會擲回不同的例外狀況訊息。 以下是 JSON 格式器的範例：

[!code-console[Main](part-4/samples/sample12.cmd)]

以下是 XML 格式器：

[!code-xml[Main](part-4/samples/sample13.xml)]

其中一個解決方法是使用 Dto，我在下一節中說明。 或者，您可以設定 JSON 和 XML 格式器來處理圖形週期。 如需詳細資訊，請參閱[處理迴圈物件參考](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)。

在本教學課程中，您不需要 `Author.Book` 導覽屬性，因此您可以將其省略。

> [!div class="step-by-step"]
> [上一頁](part-3.md)
> [下一頁](part-5.md)
