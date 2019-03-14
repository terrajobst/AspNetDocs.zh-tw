---
ms.openlocfilehash: dc6c86c48cfb4dd7e27c03ae29519417e60eac5b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57168623"
---
## <a name="multiple-authentication-providers"></a><span data-ttu-id="71ff3-101">多個驗證提供者</span><span class="sxs-lookup"><span data-stu-id="71ff3-101">Multiple authentication providers</span></span>

<span data-ttu-id="71ff3-102">當應用程式需要多個提供者時，請在 [AddAuthentication](/dotnet/api/microsoft.extensions.dependencyinjection.authenticationservicecollectionextensions.addauthentication) 之後鏈結提供者擴充方法：</span><span class="sxs-lookup"><span data-stu-id="71ff3-102">When the app requires multiple providers, chain the provider extension methods behind [AddAuthentication](/dotnet/api/microsoft.extensions.dependencyinjection.authenticationservicecollectionextensions.addauthentication):</span></span>

```csharp
services.AddAuthentication()
    .AddMicrosoftAccount(microsoftOptions => { ... })
    .AddGoogle(googleOptions => { ... })
    .AddTwitter(twitterOptions => { ... })
    .AddFacebook(facebookOptions => { ... });
```
