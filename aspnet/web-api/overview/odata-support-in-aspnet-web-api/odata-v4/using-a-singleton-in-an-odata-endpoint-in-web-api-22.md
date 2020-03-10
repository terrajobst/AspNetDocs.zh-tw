---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
title: 使用 Web API 2.2 在 OData v4 中建立單一實例 |Microsoft Docs
author: rick-anderson
description: 本主題說明如何在 Web API 2.2 的 OData 端點中定義 singleton。
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 4064ab14-26ee-4d5c-ae58-1bdda525ad06
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 218449c18759b306e425c55f8e7b573d837b4658
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622084"
---
# <a name="create-a-singleton-in-odata-v4-using-web-api-22"></a>使用 Web API 2.2 在 OData v4 中建立單一

依 Zoe 羅文

> 傳統上，只有當實體封裝于實體集內時，才可以存取它。 但是 OData v4 提供兩個額外的選項，即 Singleton 和內含專案，兩者都是 WebAPI 2.2 支援的。

本文說明如何在 Web API 2.2 的 OData 端點中定義單一專案。 如需單一專案是什麼，以及如何受益于它的詳細資訊，請參閱[使用單一專案來定義您的特殊實體](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx)。 若要在 Web API 中建立 OData V4 端點，請參閱[使用 ASP.NET Web API 2.2 建立 odata V4 端點](create-an-odata-v4-endpoint.md)。 

我們會使用下列資料模型，在您的 Web API 專案中建立 singleton：

![資料模型](using-a-singleton-in-an-odata-endpoint-in-web-api-22/_static/image1.png)

將根據型別 `Company`定義名為 `Umbrella` 的 singleton，並根據型別 `Employee`定義名為 `Employees` 的實體集。

本教學課程中使用的解決方案可以從[CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)下載。

## <a name="define-the-data-model"></a>定義資料模型

1. 定義 CLR 類型。

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample1.cs)]
2. 根據 CLR 類型產生 EDM 模型。

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample2.cs)]

    在這裡，`builder.Singleton<Company>("Umbrella")` 會告知模型產生器在 EDM 模型中建立名為 `Umbrella` 的 singleton。

    產生的中繼資料看起來會像下面這樣：

    [!code-xml[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample3.xml)]

    在中繼資料中，我們可以看到 `Employees` 實體集中 `Company` 的導覽屬性已系結至單一 `Umbrella`。 系結是由 `ODataConventionModelBuilder`自動完成，因為只有 `Umbrella` 具有 `Company` 類型。 如果模型中有任何不明確的情況，您可以使用 `HasSingletonBinding` 明確地將導覽屬性系結至 singleton;`HasSingletonBinding` 與在 CLR 型別定義中使用 `Singleton` 屬性具有相同的效果：

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample4.cs)]

## <a name="define-the-singleton-controller"></a>定義單一控制器

如同 EntitySet 控制器，單一控制器會繼承自 `ODataController`，而單一控制器名稱應該是 `[singletonName]Controller`。

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample5.cs)]

為了處理不同類型的要求，必須在控制器中預先定義動作。 預設會在 WebApi 2.2 中啟用**屬性路由**。 例如，若要定義動作，以使用屬性路由從 `Company` 處理查詢 `Revenue`，請使用下列程式：

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample6.cs)]

如果您不願意定義每個動作的屬性，只需定義遵循[OData 路由慣例](../odata-routing-conventions.md)的動作即可。 由於查詢 singleton 不需要索引鍵，因此在單一控制器中定義的動作與 entityset 控制器中定義的動作有些微不同。

如需參考，單一控制器中每個動作定義的方法簽章如下所示。

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample7.cs)]

基本上，這就是您在服務端必須執行的所有動作。 [範例專案](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)包含方案的所有程式碼，以及顯示如何使用 Singleton 的 OData 用戶端。 用戶端會遵循[建立 OData V4 用戶端應用程式](create-an-odata-v4-client-app.md)中的步驟來建立。

。 

*感謝 Leo Hu 這篇文章的原始內容。*
