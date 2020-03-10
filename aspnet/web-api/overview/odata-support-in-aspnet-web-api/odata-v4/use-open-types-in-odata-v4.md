---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: 在具有 ASP.NET Web API 的 OData v4 中開啟類型 |Microsoft Docs
author: microsoft
description: 在 OData v4 中，開放式型別是包含動態屬性的結構化型別，以及在型別定義中宣告的任何屬性。 開啟...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 950442c071bf50d2c8c1588971f13f85c4891436
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622175"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a>使用 ASP.NET Web API 在 OData v4 中開啟類型

由[Microsoft](https://github.com/microsoft)

> 在 OData v4 中，*開放式型*別是包含動態屬性的結構化型別，以及在型別定義中宣告的任何屬性。 開放式類型可讓您為資料模型增加彈性。 本教學課程說明如何在 ASP.NET Web API OData 中使用開放式型別。
> 
> 本教學課程假設您已經知道如何在 ASP.NET Web API 中建立 OData 端點。 如果不是，請先閱讀[建立 OData V4 端點](create-an-odata-v4-endpoint.md)一開始。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - Web API OData 5。3
> - OData v4

首先，有些 OData 術語：

- 實體類型：具有索引鍵的結構化類型。
- 複雜型別：不含索引鍵的結構化型別。
- 開啟類型：具有動態屬性的類型。 實體類型和複雜類型都可以開啟。

動態屬性的值可以是基本類型、複雜類型或列舉類型;或其中任何一種類型的集合。 如需有關開放式類型的詳細資訊，請參閱[OData v4 規格](http://www.odata.org/documentation/odata-version-4-0/)。

## <a name="install-the-web-odata-libraries"></a>安裝 Web OData 程式庫

使用 NuGet 套件管理員來安裝最新的 Web API OData 程式庫。 從 [套件管理員主控台] 視窗：

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a>定義 CLR 類型

首先，將 EDM 模型定義為 CLR 類型。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

建立實體資料模型（EDM）時，

- `Category` 是列舉型別。
- `Address` 是複雜型別。 （它沒有索引鍵，因此它不是實體類型）。
- `Customer` 是實體類型。 （它有一個金鑰）。
- `Press` 是開放式複雜型別。
- `Book` 是開放式實體類型。

若要建立開放式型別，CLR 型別必須有一個型別為 `IDictionary<string, object>`的屬性，它會保存動態屬性。

## <a name="build-the-edm-model"></a>建立 EDM 模型

如果您使用**ODataConventionModelBuilder**來建立 EDM，`Press` 和 `Book` 會根據 `IDictionary<string, object>` 屬性是否存在，自動加入為開啟的類型。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

您也可以使用**用**，明確地建立 EDM。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a>新增 OData 控制器

接下來，新增 OData 控制器。 在本教學課程中，我們將使用簡單的控制器，只支援 GET 和 POST 要求，並使用記憶體中的清單來儲存實體。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

請注意，第一個 `Book` 實例沒有動態屬性。 第二個 `Book` 實例具有下列動態屬性：

- 「已發行」：基本類型
- 「作者」：基本類型的集合
- "OtherCategories"：列舉類型的集合。

此外，該 `Book` 實例的 `Press` 屬性具有下列動態屬性：

- 「Blog」：基本類型
- "Address"：複雜類型

## <a name="query-the-metadata"></a>查詢中繼資料

若要取得 OData 元資料檔案，請將 GET 要求傳送至 `~/$metadata`。 回應主體看起來應該像這樣：

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

在元資料檔案中，您可以看到：

- 針對 `Book` 和 `Press` 類型，`OpenType` 屬性的值為 true。 `Customer` 和 `Address` 類型沒有此屬性。
- `Book` 實體類型有三個宣告的屬性： ISBN、Title 和按下。 OData 中繼資料不包含來自 CLR 類別的 `Book.Properties` 屬性。
- 同樣地，`Press` 複雜型別只有兩個宣告的屬性： Name 和 Category。 中繼資料不包含來自 CLR 類別的 `Press.DynamicProperties` 屬性。

## <a name="query-an-entity"></a>查詢實體

若要取得具有等於 "978-0-7356-7942-9" 之 ISBN 的書籍，請將 GET 要求傳送至 `~/Books('978-0-7356-7942-9')`。 回應主體看起來應該如下所示。 （縮排，使其更容易閱讀）。

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

請注意，動態屬性會包含在已宣告屬性的內嵌中。

## <a name="post-an-entity"></a>張貼實體

若要新增書籍實體，請將 POST 要求傳送至 `~/Books`。 用戶端可以在要求承載中設定動態屬性。

以下是範例要求。 請注意「價格」和「已發佈」屬性。

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

如果您在控制器方法中設定中斷點，您可以看到 Web API 已將這些屬性新增至 `Properties` 字典。

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a>其他資源

[OData 開啟類型範例](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
