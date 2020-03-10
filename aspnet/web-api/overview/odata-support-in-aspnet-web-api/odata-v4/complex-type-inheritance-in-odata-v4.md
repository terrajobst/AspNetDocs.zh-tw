---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: OData v4 中具有 ASP.NET Web API 的複雜類型繼承 |Microsoft Docs
author: microsoft
description: 根據 OData v4 規格，複雜型別可以繼承自另一個複雜型別。 （複雜型別是沒有索引鍵的結構化型別）。Web API 。
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 3d90216c8e594055f77577eb6d8b1d978ae4c24d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556305"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a>具有 ASP.NET Web API 的 OData v4 中的複雜類型繼承

由[Microsoft](https://github.com/microsoft)

> 根據 OData v4[規格](http://www.odata.org/documentation/odata-version-4-0/)，複雜型別可以繼承自另一個複雜型別。 （*複雜*型別是沒有索引鍵的結構化型別）。Web API OData 5.3 支援複雜類型繼承。
> 
> 本主題說明如何建立具有複雜繼承類型的 entity data model （EDM）。 如需完整的原始程式碼，請參閱[OData 複雜型別繼承範例](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - Web API OData 5。3
> - OData v4

## <a name="model-hierarchy"></a>模型階層

為了說明複雜型別繼承，我們將使用下列類別階層架構。

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

`Shape` 是抽象的複雜類型。 `Rectangle`、`Triangle`和 `Circle` 是衍生自 `Shape`的複雜類型，而 `RoundRectangle` 衍生自 `Rectangle`。 `Window` 是實體類型，且包含 `Shape` 實例。

以下是定義這些類型的 CLR 類別。

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a>建立 EDM 模型

若要建立 EDM，您可以使用**ODataConventionModelBuilder**，它會推斷 CLR 類型的繼承關聯性。

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

您也可以使用**用**，明確地建立 EDM。 這會產生更多的程式碼，但可讓您更充分掌控 EDM。

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

這兩個範例會建立相同的 EDM 架構。

## <a name="metadata-document"></a>元資料檔案

以下是 OData 元資料檔案，其中顯示覆雜型別繼承。

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

在元資料檔案中，您可以看到：

- `Shape` 複雜型別是抽象的。
- `Rectangle`、`Triangle`和 `Circle` 複雜類型具有基底類型 `Shape`。
- `RoundRectangle` 型別具有 `Rectangle`的基底型別。

## <a name="casting-complex-types"></a>轉換複雜類型

現在支援在複雜類型上轉換。 例如，下列查詢會將 `Shape` 轉換成 `Rectangle`。

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

回應承載如下：

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
