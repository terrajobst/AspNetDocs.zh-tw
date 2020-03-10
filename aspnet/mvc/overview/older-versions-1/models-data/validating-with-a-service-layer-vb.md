---
uid: mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-vb
title: 使用服務層進行驗證（VB） |Microsoft Docs
author: StephenWalther
description: 瞭解如何將您的驗證邏輯移出控制器動作並放入個別的服務層。 在本教學課程中，Stephen Walther 將說明您如何 。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 344bb38e-4965-4c47-bda1-f6d29ae5b83a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-vb
msc.type: authoredcontent
ms.openlocfilehash: 704657ffe6f50eaf3eb0d91d0d334567003ab7f4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78542823"
---
# <a name="validating-with-a-service-layer-vb"></a>驗證與服務層 (VB)

依[Stephen Walther](https://github.com/StephenWalther)

> 瞭解如何將您的驗證邏輯移出控制器動作並放入個別的服務層。 在本教學課程中，Stephen Walther 將說明如何藉由將您的服務層與控制器層隔離，來維持明顯的顧慮分離。

本教學課程的目的是要說明在 ASP.NET MVC 應用程式中執行驗證的一種方法。 在本教學課程中，您將瞭解如何將您的驗證邏輯移出您的控制器，並將其移至不同的服務層。

## <a name="separating-concerns"></a>區分考慮

當您建立 ASP.NET MVC 應用程式時，您不應該將資料庫邏輯放在控制器動作內。 混用您的資料庫和控制器邏輯，會讓您的應用程式在一段時間內更難以維護。 建議您將所有的資料庫邏輯放在個別的存放庫層中。

例如，清單1包含名為 ProductRepository 的簡單存放庫。 產品存放庫包含應用程式的所有資料存取程式碼。 此清單也包含產品存放庫所實行的 IProductRepository 介面。

**清單 1-Models\ProductRepository.vb**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample1.vb)]

[清單 2] 中的控制器會在其索引（）和 Create （）動作中使用儲存機制層。 請注意，此控制器不包含任何資料庫邏輯。 建立存放庫層可讓您維持清楚的關注點分離。 控制器負責應用程式流程式控制制邏輯，而存放庫負責資料存取邏輯。

**清單 2-Controllers\ProductController.vb**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample2.vb)]

## <a name="creating-a-service-layer"></a>建立服務層級

因此，應用程式流程式控制制邏輯屬於控制器，而資料存取邏輯則屬於存放庫。 在這種情況下，您要將驗證邏輯放在哪裡？ 其中一個選項是將您的驗證邏輯放在*服務層*中。

服務層是 ASP.NET MVC 應用程式中的另一層，可協調控制器和存放庫層之間的通訊。 服務層包含商務邏輯。 特別是，它包含驗證邏輯。

例如，[清單 3] 中的產品服務層有一個 CreateProduct （）方法。 CreateProduct （）方法會呼叫 ValidateProduct （）方法來驗證新的產品，然後才將產品傳遞至產品存放庫。

**清單 3-Models\ProductService.vb**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample3.vb)]

[清單 4] 中的產品控制器已更新為使用服務層，而不是儲存機制層。 控制器層會與服務層交談。 服務層會與存放庫層交談。 每一層都有個別的責任。

**清單 4-Controllers\ProductController.vb**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample4.vb)]

請注意，產品服務是在產品控制器的程式中建立的。 建立產品服務時，會將模型狀態字典傳遞至服務。 產品服務會使用模型狀態，將驗證錯誤訊息傳回到控制器。

## <a name="decoupling-the-service-layer"></a>將服務層分離

我們無法將控制器和服務層隔離在一個方面。 控制器和服務層會透過模型狀態進行通訊。 換句話說，服務層級相依于 ASP.NET MVC 架構的特定功能。

我們想要盡可能將服務層與控制器層隔離。 理論上，我們應該能夠將服務層與任何類型的應用程式搭配使用，而不只是 ASP.NET 的 MVC 應用程式。 例如，在未來，我們可能會想要為應用程式建立 WPF 前端。 我們應該會找到一種方法，從我們的服務層中移除對 ASP.NET MVC 模型狀態的相依性。

在 [清單 5] 中，服務層已更新，因此不會再使用模型狀態。 相反地，它會使用任何可執行 IValidationDictionary 介面的類別。

**清單 5-Models\ProductService.vb （分離）**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample5.vb)]

IValidationDictionary 介面定義于 [清單 6] 中。 這個簡單介面具有單一方法和單一屬性。

**清單 6-Models\IValidationDictionary.cs**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample6.vb)]

清單7中名為 ModelStateWrapper 類別的類別會執行 IValidationDictionary 介面。 您可以藉由將模型狀態字典傳遞給此函式，來具現化 ModelStateWrapper 類別。

**清單 7-Models\ModelStateWrapper.vb**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample7.vb)]

最後，在 [清單 8] 中更新的控制器在其「函式」中建立服務層時，會使用 ModelStateWrapper。

**清單 8-Controllers\ProductController.vb**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample8.vb)]

使用 IValidationDictionary 介面和 ModelStateWrapper 類別可讓我們將我們的服務層與控制器層完全隔離。 服務層不再相依于模型狀態。 您可以將任何可執行 IValidationDictionary 介面的類別傳遞至服務層。 例如，WPF 應用程式可能會使用簡單的集合類別來執行 IValidationDictionary 介面。

## <a name="summary"></a>總結

本教學課程的目的是要討論在 ASP.NET MVC 應用程式中執行驗證的一種方法。 在本教學課程中，您已瞭解如何將您的所有驗證邏輯移出控制器，並將其移至不同的服務層。 您也已瞭解如何藉由建立 ModelStateWrapper 類別，將您的服務層與控制器層隔離。

> [!div class="step-by-step"]
> [上一頁](validating-with-the-idataerrorinfo-interface-vb.md)
> [下一頁](validation-with-the-data-annotation-validators-vb.md)
