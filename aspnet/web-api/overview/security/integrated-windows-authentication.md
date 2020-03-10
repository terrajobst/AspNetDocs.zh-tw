---
uid: web-api/overview/security/integrated-windows-authentication
title: 整合式 Windows 驗證 |Microsoft Docs
author: MikeWasson
description: 描述如何在 ASP.NET Web API 中使用整合式 Windows 驗證。
ms.author: riande
ms.date: 12/18/2012
ms.assetid: 71ee4c78-c500-4d1c-b761-b4e161a291b5
msc.legacyurl: /web-api/overview/security/integrated-windows-authentication
msc.type: authoredcontent
ms.openlocfilehash: e4f31f191f3c0fabff308ea5dadb0f1d9ce7d448
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78621741"
---
# <a name="integrated-windows-authentication"></a><span data-ttu-id="2d117-103">整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="2d117-103">Integrated Windows Authentication</span></span>

<span data-ttu-id="2d117-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2d117-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="2d117-105">整合式 Windows 驗證可讓使用者使用 Kerberos 或 NTLM，以其 Windows 認證登入。</span><span class="sxs-lookup"><span data-stu-id="2d117-105">Integrated Windows authentication enables users to log in with their Windows credentials, using Kerberos or NTLM.</span></span> <span data-ttu-id="2d117-106">用戶端會在授權標頭中傳送認證。</span><span class="sxs-lookup"><span data-stu-id="2d117-106">The client sends credentials in the Authorization header.</span></span> <span data-ttu-id="2d117-107">Windows 驗證最適合內部網路環境。</span><span class="sxs-lookup"><span data-stu-id="2d117-107">Windows authentication is best suited for an intranet environment.</span></span> <span data-ttu-id="2d117-108">如需詳細資訊，請參閱 [Windows 驗證](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication)。</span><span class="sxs-lookup"><span data-stu-id="2d117-108">For more information, see [Windows Authentication](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication).</span></span>

| <span data-ttu-id="2d117-109">優點</span><span class="sxs-lookup"><span data-stu-id="2d117-109">Advantages</span></span> | <span data-ttu-id="2d117-110">缺點</span><span class="sxs-lookup"><span data-stu-id="2d117-110">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="2d117-111">-內建于 IIS 中。</span><span class="sxs-lookup"><span data-stu-id="2d117-111">- Built into IIS.</span></span> <span data-ttu-id="2d117-112">-不會傳送要求中的使用者認證。</span><span class="sxs-lookup"><span data-stu-id="2d117-112">- Does not send the user credentials in the request.</span></span> <span data-ttu-id="2d117-113">-如果用戶端電腦屬於網域（例如，內部網路應用程式），使用者就不需要輸入認證。</span><span class="sxs-lookup"><span data-stu-id="2d117-113">- If the client computer belongs to the domain (for example, intranet application), the user does not need to enter credentials.</span></span> | <span data-ttu-id="2d117-114">-不建議用於網際網路應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d117-114">- Not recommended for Internet applications.</span></span> <span data-ttu-id="2d117-115">-需要用戶端中的 Kerberos 或 NTLM 支援。</span><span class="sxs-lookup"><span data-stu-id="2d117-115">- Requires Kerberos or NTLM support in the client.</span></span> <span data-ttu-id="2d117-116">-用戶端必須在 Active Directory 網域中。</span><span class="sxs-lookup"><span data-stu-id="2d117-116">- Client must be in the Active Directory domain.</span></span> |

> [!NOTE]
> <span data-ttu-id="2d117-117">如果您的應用程式裝載于 Azure 上，而且您有內部部署 Active Directory 網域，請考慮將您的內部部署 AD 與 Azure Active Directory 同盟。</span><span class="sxs-lookup"><span data-stu-id="2d117-117">If your application is hosted on Azure and you have an on-premise Active Directory domain, consider federating your on-premise AD with Azure Active Directory.</span></span> <span data-ttu-id="2d117-118">如此一來，使用者就可以使用其內部部署認證登入，但驗證是由 Azure AD 執行。</span><span class="sxs-lookup"><span data-stu-id="2d117-118">That way, users can log in with their on-premise credentials, but the authentication is performed by Azure AD.</span></span> <span data-ttu-id="2d117-119">如需詳細資訊，請參閱[Azure 驗證](../../../visual-studio/overview/2012/windows-azure-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="2d117-119">For more information, see [Azure Authentication](../../../visual-studio/overview/2012/windows-azure-authentication.md).</span></span>

<span data-ttu-id="2d117-120">若要建立使用整合式 Windows 驗證的應用程式，請選取 [MVC 4 專案] wizard 中的 [內部網路應用程式] 範本。</span><span class="sxs-lookup"><span data-stu-id="2d117-120">To create an application that uses Integrated Windows authentication, select the "Intranet Application" template in the MVC 4 project wizard.</span></span> <span data-ttu-id="2d117-121">此專案範本會將下列設定放在 Web.config 檔案中：</span><span class="sxs-lookup"><span data-stu-id="2d117-121">This project template puts the following setting in the Web.config file:</span></span>

[!code-xml[Main](integrated-windows-authentication/samples/sample1.xml)]

<span data-ttu-id="2d117-122">在用戶端上，整合式 Windows 驗證可與任何支援[Negotiate](http://www.ietf.org/rfc/rfc4559.txt)驗證配置的瀏覽器搭配使用，其中包括大部分的主要瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="2d117-122">On the client side, Integrated Windows authentication works with any browser that supports the [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) authentication scheme, which includes most major browsers.</span></span> <span data-ttu-id="2d117-123">針對 .NET 用戶端應用程式， **HttpClient**類別支援 Windows 驗證：</span><span class="sxs-lookup"><span data-stu-id="2d117-123">For .NET client applications, the **HttpClient** class supports Windows authentication:</span></span>

[!code-csharp[Main](integrated-windows-authentication/samples/sample2.cs)]

<span data-ttu-id="2d117-124">Windows 驗證容易遭受跨網站偽造要求（CSRF）攻擊。</span><span class="sxs-lookup"><span data-stu-id="2d117-124">Windows authentication is vulnerable to cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="2d117-125">請參閱[防止跨網站偽造要求（CSRF）攻擊](preventing-cross-site-request-forgery-csrf-attacks.md)。</span><span class="sxs-lookup"><span data-stu-id="2d117-125">See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>
