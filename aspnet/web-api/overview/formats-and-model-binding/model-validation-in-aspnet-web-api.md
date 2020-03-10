---
uid: web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
title: ASP.NET Web API 中的模型驗證-ASP.NET 4。x
author: MikeWasson
description: ASP.NET 4.x 的 ASP.NET Web API 中的模型驗證總覽。
ms.author: riande
ms.date: 07/20/2012
ms.custom: seoapril2019
ms.assetid: 7d061207-22b8-4883-bafa-e89b1e7749ca
msc.legacyurl: /web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 531a66b7ab642bd012663517640f2766f1917f25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557236"
---
# <a name="model-validation-in-aspnet-web-api"></a>ASP.NET Web API 中的模型驗證

由[Mike Wasson](https://github.com/MikeWasson)

本文說明如何標注模型、使用批註進行資料驗證，以及處理 Web API 中的驗證錯誤。 當用戶端將資料傳送至您的 Web API 時，您通常會想要先驗證資料，然後再進行任何處理。 

## <a name="data-annotations"></a>資料註釋

在 ASP.NET Web API 中，您可以使用[system.workflow.componentmodel.activity. DataAnnotations](/dotnet/api/system.componentmodel.dataannotations)命名空間中的屬性，為模型上的屬性設定驗證規則。 請考慮下列模型：

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample1.cs)]

如果您已在 ASP.NET MVC 中使用模型驗證，這看起來應該很熟悉。 **必要**的屬性指出 `Name` 屬性不得為 null。 **範圍**屬性指出 `Weight` 必須介於0到999之間。

假設用戶端傳送具有下列 JSON 標記法的 POST 要求：

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample2.json)]

您可以看到用戶端並未包含 [`Name`] 屬性，這會標示為 [必要]。 當 Web API 將 JSON 轉換成 `Product` 實例時，它會根據驗證屬性來驗證 `Product`。 在您的控制器動作中，您可以檢查模型是否有效：

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample3.cs)]

模型驗證不保證用戶端資料是安全的。 應用程式的其他層可能需要額外的驗證。 （例如，資料層可能會強制執行 foreign key 條件約束）。[使用 WEB API 搭配 Entity Framework](../data/using-web-api-with-entity-framework/part-1.md)的教學課程會探討其中一些問題。

「**張貼**中」：當用戶端離開一些屬性時，就會進行張貼。 例如，假設用戶端傳送下列內容：

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample4.json)]

在這裡，用戶端未指定 `Price` 或 `Weight`的值。 JSON 格式器會將預設值零指派給遺漏的屬性。

![](model-validation-in-aspnet-web-api/_static/image1.png)

模型狀態有效，因為零是這些屬性的有效值。 這是否為問題，取決於您的案例。 例如，在更新作業中，您可能會想要區分「零」和「未設定」。 若要強制用戶端設定值，請將屬性設為 nullable 並設定**必要**的屬性：

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample5.cs?highlight=1-2)]

「**過度張貼**」：用戶端也可以傳送比您預期還要*多*的資料。 例如:

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample6.json)]

在這裡，JSON 包含不存在於 `Product` 模型中的屬性（「色彩」）。 在此情況下，JSON 格式器只會忽略此值。 （XML 格式器會執行相同的工作）。如果您的模型有您想要唯讀的屬性，則過度發佈會導致問題。 例如:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample7.cs)]

您不希望使用者更新 `IsAdmin` 屬性，並將自己提升為系統管理員！ 最安全的策略是使用完全符合允許用戶端傳送的模型類別：

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample8.cs)]

> [!NOTE]
> Brad Wilson 的 blog 文章「[輸入驗證與 ASP.NET MVC 中的模型驗證](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)」，在張貼和過度張貼方面都有很好的討論。 雖然這篇文章是關於 ASP.NET MVC 2，但這些問題仍然與 Web API 有關。

## <a name="handling-validation-errors"></a>處理驗證錯誤

驗證失敗時，Web API 不會自動將錯誤傳回給用戶端。 由控制器動作負責檢查模型狀態並適當地回應。

您也可以在叫用控制器動作之前，建立動作篩選準則來檢查模型狀態。 下列程式碼顯示一個範例：

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample9.cs)]

如果模型驗證失敗，此篩選會傳回包含驗證錯誤的 HTTP 回應。 在這種情況下，就不會叫用控制器動作。

[!code-console[Main](model-validation-in-aspnet-web-api/samples/sample10.cmd)]

若要將此篩選套用至所有 Web API 控制器，請在設定期間，將篩選準則的實例新增至**HttpConfiguration**集合：

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample11.cs)]

另一個選項是將篩選準則設定為個別控制器或控制器動作上的屬性：

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample12.cs)]
