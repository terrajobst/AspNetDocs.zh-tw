---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
title: ASP.NET Web API 的安全性指導方針 2 OData-ASP.NET 4。x
author: MikeWasson
description: 說明在 ASP.NET 4.x 上透過 OData 針對 ASP.NET Web API 2 公開資料集時要考慮的安全性問題。
ms.author: riande
ms.date: 02/06/2013
ms.custom: seoapril2019
ms.assetid: b91e6424-1544-4747-bd0b-d1f8418c9653
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
msc.type: authoredcontent
ms.openlocfilehash: 8194a368cb0629c30e32ec05bf4bed150d442ad8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556494"
---
# <a name="security-guidance-for-aspnet-web-api-2-odata"></a>ASP.NET Web API 2 OData 的安全性指引

由[Mike Wasson](https://github.com/MikeWasson)

本主題說明在 ASP.NET 4.x 上透過 OData 針對 ASP.NET Web API 2 公開資料集時，您應該考慮的一些安全性問題。

## <a name="edm-security"></a>EDM 安全性

查詢的語義是以 entity data model （EDM）為基礎，而不是基礎模型類型。 您可以從 EDM 排除屬性，查詢看不到它。 例如，假設您的模型包含具有薪資屬性的員工類型。 您可能想要從 EDM 排除此屬性，以將它從用戶端隱藏。

有兩種方式可從 EDM 中排除屬性。 您可以在模型類別中的屬性上設定 **[IgnoreDataMember]** 屬性：

[!code-csharp[Main](odata-security-guidance/samples/sample1.cs)]

您也可以透過程式設計方式從 EDM 移除屬性：

[!code-csharp[Main](odata-security-guidance/samples/sample2.cs)]

## <a name="query-security"></a>查詢安全性

惡意或簡單的用戶端可能會建立花費很長時間執行的查詢。 在最糟的情況下，這可能會干擾您的服務存取。

**[可查詢]** 屬性是用來剖析、驗證及套用查詢的動作篩選準則。 篩選準則會將查詢選項轉換成 LINQ 運算式。 當 OData 控制器傳回**iqueryable**類型時， **iqueryable** linq 提供者會將 linq 運算式轉換成查詢。 因此，效能取決於所使用的 LINQ 提供者，以及您的資料集或資料庫架構的特定特性。

如需在 ASP.NET Web API 中使用 OData 查詢選項的詳細資訊，請參閱[支援 OData 查詢選項](supporting-odata-query-options.md)。

如果您知道所有用戶端都是受信任的（例如，在企業環境中），或如果您的資料集很小，則查詢效能可能不會有問題。 否則，您應該考慮下列建議。

- 使用各種查詢來測試您的服務，並分析資料庫。
- 啟用伺服器導向的分頁，以避免在單一查詢中傳回大型資料集。 如需詳細資訊，請參閱[伺服器導向的分頁](supporting-odata-query-options.md#server-paging)。 

    [!code-csharp[Main](odata-security-guidance/samples/sample3.cs)]
- 您需要 $filter 和 $orderby 嗎？ 某些應用程式可能會允許用戶端分頁，使用 $top 和 $skip，但停用其他查詢選項。 

    [!code-csharp[Main](odata-security-guidance/samples/sample4.cs)]
- 請考慮將 $orderby 限制為叢集索引中的屬性。 在沒有叢集索引的情況下排序大型資料會變慢。 

    [!code-csharp[Main](odata-security-guidance/samples/sample5.cs)]
- 節點計數上限： **[可查詢]** 上的**MaxNodeCount**屬性會設定 $filter 語法樹狀結構中所允許的最大節點數目。 預設值為100，但您可能會想要設定較低的值，因為編譯的節點可能會變得很慢。 如果您使用 LINQ to Objects （也就是在記憶體中的集合上執行 LINQ 查詢，而不使用中繼的 LINQ 提供者），這特別適用。 

    [!code-csharp[Main](odata-security-guidance/samples/sample6.cs)]
- 請考慮停用 any （）和 all （）函式，因為這些函式可能會變慢。 

    [!code-csharp[Main](odata-security-guidance/samples/sample7.cs)]
- 如有任何字串屬性包含大型&#8212;字串（例如，產品描述或 blog 專案&#8212;），請考慮停用字串函數。 

    [!code-csharp[Main](odata-security-guidance/samples/sample8.cs)]
- 考慮禁止篩選導覽屬性。 根據您的資料庫架構而定，篩選導覽屬性可能會導致聯結，這可能會很慢。 下列程式碼顯示可防止篩選導覽屬性的查詢驗證程式。 如需查詢驗證程式的詳細資訊，請參閱[查詢驗證](supporting-odata-query-options.md#query-validation)。 

    [!code-csharp[Main](odata-security-guidance/samples/sample9.cs)]
- 請考慮撰寫針對您的資料庫自訂的驗證程式，以限制 $filter 查詢。 例如，請考慮下列兩個查詢： 

  - 具有姓氏開頭為 ' A ' 之動作專案的所有電影。
  - 1994中發行的所有電影。

    除非電影是由動作專案編制索引，否則第一個查詢可能需要資料庫引擎掃描整個電影清單。 雖然第二個查詢可能是可接受的，但假設電影是以發行年份進行編制索引。

    下列程式碼顯示允許篩選 "ReleaseYear" 和 "Title" 屬性，但沒有其他屬性的驗證器。

    [!code-csharp[Main](odata-security-guidance/samples/sample10.cs)]
- 一般來說，請考慮您需要的 $filter 功能。 如果您的用戶端不需要 $filter 的完整表達，您可以限制允許的功能。
