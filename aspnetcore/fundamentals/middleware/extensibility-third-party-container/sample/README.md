---
ms.openlocfilehash: 282871e5db197dfb4226cc02918f2d6ba1135c04
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57045595"
---
# <a name="aspnet-core-middleware-extensibility-sample"></a><span data-ttu-id="d784e-101">ASP.NET Core 中介軟體擴充性範例</span><span class="sxs-lookup"><span data-stu-id="d784e-101">ASP.NET Core Middleware Extensibility Sample</span></span>

<span data-ttu-id="d784e-102">此範例說明如何以 [IMiddleware](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddleware) 和 [IMiddlewareFactory](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory) 與協力廠商相依性插入容器 [Simple Injector](https://simpleinjector.org) 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="d784e-102">This sample illustrates the use of [IMiddleware](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddleware) and [IMiddlewareFactory](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory) with a 3rd party dependency injection container, [Simple Injector](https://simpleinjector.org).</span></span> <span data-ttu-id="d784e-103">這個範例會示範 [Middleware activation with a third-party container in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/middleware/extensibility-third-party-container) (在 ASP.NET Core 中以協力廠商容器啟用中介軟體) 中所述的功能。</span><span class="sxs-lookup"><span data-stu-id="d784e-103">This sample demonstrates the features described in [Middleware activation with a third-party container in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/middleware/extensibility-third-party-container).</span></span>
