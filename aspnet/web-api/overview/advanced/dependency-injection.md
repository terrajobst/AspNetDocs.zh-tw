---
uid: web-api/overview/advanced/dependency-injection
title: ASP.NET Web API 2-ASP.NET 4.x 中的相依性插入
author: MikeWasson
description: 本教學課程說明如何將相依性插入 ASP.NET 4.x 的 ASP.NET Web API 控制器。
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: e3d3e7ba-87f0-4032-bdd3-31f3c1aa9d9c
msc.legacyurl: /web-api/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: f9c212af92168ac02644625b9aa8ec1bef329cab
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622602"
---
# <a name="dependency-injection-in-aspnet-web-api-2"></a>ASP.NET Web API 2 中的相依性插入

由[Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-468ee148)

> 本教學課程說明如何將相依性插入 ASP.NET Web API 控制器。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - Web API 2
> - [Unity 應用程式區塊](https://www.nuget.org/packages/Unity/)
> - Entity Framework 6 （第5版也適用）

## <a name="what-is-dependency-injection"></a>什麼是相依性插入？

「相依性」是另一個物件所需的任何物件。 例如，一般會定義處理資料存取的[儲存](http://martinfowler.com/eaaCatalog/repository.html)機制。 讓我們使用範例來說明。 首先，我們會定義領域模型：

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

以下是簡單的存放庫類別，會使用 Entity Framework 將專案儲存在資料庫中。

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

現在，讓我們定義 Web API 控制器，以支援 `Product` 實體的 GET 要求。 （為了簡單起見，我要保留 POST 和其他方法）。第一次嘗試：

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

請注意，控制器類別取決於 `ProductRepository`，而我們會讓控制器建立 `ProductRepository` 實例。 不過，以這種方式硬編碼相依性是不好的主意，原因有好幾個。

- 如果您想要以不同的執行取代 `ProductRepository`，您也需要修改控制器類別。
- 如果 `ProductRepository` 有相依性，您必須在控制器內設定這些相依性。 對於具有多個控制器的大型專案，您的設定程式碼會散佈在您的專案中。
- 這很難進行單元測試，因為控制器是以硬式編碼方式來查詢資料庫。 針對單元測試，您應該使用模擬或存根存放庫，這在目前的設計中無法使用。

我們可以藉由將存放*庫插入控制器*來解決這些問題。 首先，將 `ProductRepository` 類別重構為介面：

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

然後提供 `IProductRepository` 做為「函式」參數：

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

這個範例使用的是[函數插入](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)。 您也可以使用*setter 插入*，您可以在其中透過 setter 方法或屬性來設定相依性。

但現在有問題，因為您的應用程式不會直接建立控制器。 Web API 會在路由要求時建立控制器，而 Web API 並不知道 `IProductRepository`的任何內容。 這是 Web API 相依性解析程式的來源。

## <a name="the-web-api-dependency-resolver"></a>Web API 相依性解析程式

Web API 會定義用來解析相依性的**IDependencyResolver**介面。 以下是介面的定義：

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

**IDependencyScope**介面有兩個方法：

- **GetService**會建立一個類型的實例。
- **GetServices**會建立指定之類型的物件集合。

**IDependencyResolver**方法會繼承**IDependencyScope** ，並新增**BeginScope**方法。 我稍後會在本教學課程中討論範圍。

當 Web API 建立控制器實例時，它會先呼叫**IDependencyResolver GetService**，並傳入控制器類型。 您可以使用此擴充性攔截來建立控制器，並解析任何相依性。 如果**GetService**傳回 Null，Web API 會在控制器類別上尋找無參數的函式。

## <a name="dependency-resolution-with-the-unity-container"></a>Unity 容器的相依性解析

雖然您可以從頭開始撰寫完整的**IDependencyResolver**實作為，但介面其實是設計成在 Web API 與現有 IoC 容器之間做為橋樑。

IoC 容器是負責管理相依性的軟體元件。 您會向容器註冊類型，然後使用容器來建立物件。 容器會自動將相依性關聯到圖形。 許多 IoC 容器也可讓您控制物件存留期和範圍之類的專案。

> [!NOTE]
> 「IoC」代表「反轉控制」，這是架構呼叫應用程式程式碼的一般模式。 IoC 容器會為您構造物件，這會「反轉」一般控制流程。

在本教學課程中，我們將使用 Microsoft 模式的[Unity](https://msdn.microsoft.com/library/ff647202.aspx) &amp; 實務。 （其他熱門程式庫包括[Castle Windsor](http://www.castleproject.org/)、 [Spring.Net](http://www.springframework.net/)、 [Autofac](https://code.google.com/p/autofac/)、 [Ninject](http://www.ninject.org/)和[StructureMap](http://structuremap.github.io/documentation/)）。您可以使用 NuGet 套件管理員來安裝 Unity。 從 Visual Studio 的 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。 在 [套件管理員主控台] 視窗中，輸入下列命令：

[!code-console[Main](dependency-injection/samples/sample7.cmd)]

以下是包裝 Unity 容器的**IDependencyResolver**的執行。

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

> [!NOTE]
> 如果**GetService**方法無法解析類型，它應該會傳回**null**。 如果**GetServices**方法無法解析類型，它應該會傳回空的集合物件。 不擲回未知類型的例外狀況。

## <a name="configuring-the-dependency-resolver"></a>設定相依性解析程式

在全域**HttpConfiguration**物件的**DependencyResolver**屬性上設定相依性解析程式。

下列程式碼會向 Unity 註冊 `IProductRepository` 介面，然後建立 `UnityResolver`。

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

## <a name="dependency-scope-and-controller-lifetime"></a>相依性範圍和控制器存留期

系統會針對每個要求建立控制器。 為了管理物件存留期， **IDependencyResolver**會使用*範圍*的概念。

附加至**HttpConfiguration**物件的相依性解析程式具有全域範圍。 當 Web API 建立控制器時，它會呼叫**BeginScope**。 這個方法會傳回代表子範圍的**IDependencyScope** 。

然後，Web API 會在子範圍上呼叫**GetService**來建立控制器。 當要求完成時，Web API 會呼叫子範圍的**Dispose** 。 使用**dispose**方法來處置控制器的相依性。

您執行**BeginScope**的方式取決於 IoC 容器。 針對 Unity，範圍會對應至子容器：

[!code-csharp[Main](dependency-injection/samples/sample10.cs)]

大部分的 IoC 容器都有類似的對應專案。
