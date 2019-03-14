---
ms.openlocfilehash: 476580d4bc2435f73ef37c5344ab7fea4b67b9b8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57032495"
---
<span data-ttu-id="b7450-101">藉由執行下列命令來信任 HTTPS 開發憑證：</span><span class="sxs-lookup"><span data-stu-id="b7450-101">Trust the HTTPS development certificate by running the following command:</span></span>

```console
dotnet dev-certs https --trust
```

<span data-ttu-id="b7450-102">上述命令會顯示以下對話方塊：</span><span class="sxs-lookup"><span data-stu-id="b7450-102">The preceding command displays the following dialog:</span></span>

![安全性警告對話方塊](~/getting-started/_static/cert.png)

<span data-ttu-id="b7450-104">若您同意信任開發憑證，請選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="b7450-104">Select **Yes** if you agree to trust the development certificate.</span></span>

<span data-ttu-id="b7450-105">如需詳細資訊，請參閱[信任 ASP.NET Core HTTPS 開發憑證](xref:security/enforcing-ssl#trust-the-aspnet-core-https-development-certificate-on-windows-and-macos)。</span><span class="sxs-lookup"><span data-stu-id="b7450-105">See [Trust the ASP.NET Core HTTPS development certificate](xref:security/enforcing-ssl#trust-the-aspnet-core-https-development-certificate-on-windows-and-macos) for more information.</span></span>