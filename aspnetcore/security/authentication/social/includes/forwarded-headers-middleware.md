---
ms.openlocfilehash: d7ef9b11af8ee11e4ec84404f8cdeb0b89384a3c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57130446"
---
## <a name="forward-request-information-with-a-proxy-or-load-balancer"></a><span data-ttu-id="46562-101">轉寄要求使用 proxy 的資訊或負載平衡器</span><span class="sxs-lookup"><span data-stu-id="46562-101">Forward request information with a proxy or load balancer</span></span>

<span data-ttu-id="46562-102">如果應用程式部署 proxy 伺服器或負載平衡器後方時，原始的要求資訊的一些可能會轉送給要求標頭中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="46562-102">If the app is deployed behind a proxy server or load balancer, some of the original request information might be forwarded to the app in request headers.</span></span> <span data-ttu-id="46562-103">這項資訊通常包括安全的要求配置 (`https`)，主機和用戶端 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="46562-103">This information usually includes the secure request scheme (`https`), host, and client IP address.</span></span> <span data-ttu-id="46562-104">應用程式不會自動讀取這些探索及使用原始的要求資訊的要求標頭。</span><span class="sxs-lookup"><span data-stu-id="46562-104">Apps don't automatically read these request headers to discover and use the original request information.</span></span>

<span data-ttu-id="46562-105">配置用於連結產生會影響使用外部提供者的驗證流程。</span><span class="sxs-lookup"><span data-stu-id="46562-105">The scheme is used in link generation that affects the authentication flow with external providers.</span></span> <span data-ttu-id="46562-106">遺失的安全的配置 (`https`) 會導致產生不正確不安全的重新導向 Url 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="46562-106">Losing the secure scheme (`https`) results in the app generating incorrect insecure redirect URLs.</span></span>

<span data-ttu-id="46562-107">將原始的要求資訊提供給要求處理的應用程式中使用轉送標頭中介軟體。</span><span class="sxs-lookup"><span data-stu-id="46562-107">Use Forwarded Headers Middleware to make the original request information available to the app for request processing.</span></span>

<span data-ttu-id="46562-108">如需詳細資訊，請參閱<xref:host-and-deploy/proxy-load-balancer>。</span><span class="sxs-lookup"><span data-stu-id="46562-108">For more information, see <xref:host-and-deploy/proxy-load-balancer>.</span></span>
