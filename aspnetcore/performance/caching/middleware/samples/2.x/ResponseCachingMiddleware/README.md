---
ms.openlocfilehash: 93bda587eebc438e5da36b07cb7e4a37df8a91eb
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57062715"
---
# <a name="aspnet-core-response-caching-sample"></a><span data-ttu-id="b9990-101">ASP.NET Core 回應快取範例</span><span class="sxs-lookup"><span data-stu-id="b9990-101">ASP.NET Core Response Caching Sample</span></span>

<span data-ttu-id="b9990-102">此範例說明如何使用 ASP.NET Core[回應快取中介軟體](https://docs.microsoft.com/aspnet/core/performance/caching/middleware)。</span><span class="sxs-lookup"><span data-stu-id="b9990-102">This sample illustrates the usage of ASP.NET Core [Response Caching Middleware](https://docs.microsoft.com/aspnet/core/performance/caching/middleware).</span></span>

<span data-ttu-id="b9990-103">應用程式的回應使用其索引 頁面中，包括`Cache-Control`標頭，若要設定快取行為。</span><span class="sxs-lookup"><span data-stu-id="b9990-103">The app responds with its Index page, including a `Cache-Control` header to configure caching behavior.</span></span> <span data-ttu-id="b9990-104">應用程式也會設定`Vary`標頭來設定快取服務的回應才`Accept-Encoding`後續的要求標頭符合原始要求。</span><span class="sxs-lookup"><span data-stu-id="b9990-104">The app also sets the `Vary` header to configure the cache to serve the response only if the `Accept-Encoding` header of subsequent requests matches that from the original request.</span></span>

<span data-ttu-id="b9990-105">當執行範例時，[索引] 頁面會提供從快取時儲存，並快取最多 10 秒。</span><span class="sxs-lookup"><span data-stu-id="b9990-105">When running the sample, the Index page is served from cache when stored and cached for up to 10 seconds.</span></span>
