---
ms.openlocfilehash: b6f39dd0dedb38961eb021cde355f7ec83283195
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57024865"
---
# <a name="aspnet-core-web-api-controller-sample"></a><span data-ttu-id="ef508-101">ASP.NET Core Web API 控制器範例</span><span class="sxs-lookup"><span data-stu-id="ef508-101">ASP.NET Core Web API Controller Sample</span></span>

<span data-ttu-id="ef508-102">此範例應用程式包含下列專案：</span><span class="sxs-lookup"><span data-stu-id="ef508-102">This sample app consists of the following projects:</span></span>

- <span data-ttu-id="ef508-103">\**WebApiSample.Api.22*:ASP.NET Core 2.2 專案，目標為.NET Core 2.2。</span><span class="sxs-lookup"><span data-stu-id="ef508-103">\**WebApiSample.Api.22*: An ASP.NET Core 2.2 project targeting .NET Core 2.2.</span></span>
- <span data-ttu-id="ef508-104">**WebApiSample.Api.21**:ASP.NET Core 2.1 的專案，目標為.NET Core 2.1。</span><span class="sxs-lookup"><span data-stu-id="ef508-104">**WebApiSample.Api.21**: An ASP.NET Core 2.1 project targeting .NET Core 2.1.</span></span>
- <span data-ttu-id="ef508-105">**WebApiSample.Api.Pre21**:以.NET Core 2.0 為目標的 ASP.NET Core 2.0 專案。</span><span class="sxs-lookup"><span data-stu-id="ef508-105">**WebApiSample.Api.Pre21**: An ASP.NET Core 2.0 project targeting .NET Core 2.0.</span></span>
- <span data-ttu-id="ef508-106">**WebApiSample.DataAccess**:.NET Standard 2.0 類別庫做為資料存取層的 2 個 Web API 專案。</span><span class="sxs-lookup"><span data-stu-id="ef508-106">**WebApiSample.DataAccess**: A .NET Standard 2.0 class library serving as a data access tier for the 2 Web API projects.</span></span>

<span data-ttu-id="ef508-107">本範例說明建立 Web API 控制器的各種方式：</span><span class="sxs-lookup"><span data-stu-id="ef508-107">This sample illustrates variations of Web API controller creation:</span></span>

- [<span data-ttu-id="ef508-108">來自 ControllerBase 的衍生類別</span><span class="sxs-lookup"><span data-stu-id="ef508-108">Derive class from ControllerBase</span></span>](https://docs.microsoft.com/aspnet/core/web-api#derive-class-from-controllerbase)
- [<span data-ttu-id="ef508-109">以 ApiControllerAttribute 標註類別</span><span class="sxs-lookup"><span data-stu-id="ef508-109">Annotate class with ApiControllerAttribute</span></span>](https://docs.microsoft.com/aspnet/core/web-api#annotate-class-with-apicontrollerattribute)
