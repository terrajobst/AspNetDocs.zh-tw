---
uid: web-api/overview/security/working-with-ssl-in-web-api
title: 在 Web API 中使用 SSL |Microsoft Docs
author: MikeWasson
description: 說明如何搭配 ASP.NET Web API 使用 SSL，包括使用 SSL 用戶端憑證。
ms.author: riande
ms.date: 02/22/2019
ms.assetid: 97f6164f-59cf-45c0-b820-e4aa29b45396
msc.legacyurl: /web-api/overview/security/working-with-ssl-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 31589b3713b1f1a9b98d12906bfef81f8bf5e3f9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598634"
---
# <a name="working-with-ssl-in-web-api"></a><span data-ttu-id="d275b-103">在 Web API 中使用 SSL</span><span class="sxs-lookup"><span data-stu-id="d275b-103">Working with SSL in Web API</span></span>

<span data-ttu-id="d275b-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="d275b-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="d275b-105">有數個常見的驗證配置不會受到一般 HTTP 的保護。</span><span class="sxs-lookup"><span data-stu-id="d275b-105">Several common authentication schemes are not secure over plain HTTP.</span></span> <span data-ttu-id="d275b-106">尤其是，基本驗證和表單驗證會傳送未加密的認證。</span><span class="sxs-lookup"><span data-stu-id="d275b-106">In particular, Basic authentication and forms authentication send unencrypted credentials.</span></span> <span data-ttu-id="d275b-107">為了安全，這些驗證配置*必須*使用 SSL。</span><span class="sxs-lookup"><span data-stu-id="d275b-107">To be secure, these authentication schemes *must* use SSL.</span></span> <span data-ttu-id="d275b-108">此外，您還可以使用 SSL 用戶端憑證來驗證用戶端。</span><span class="sxs-lookup"><span data-stu-id="d275b-108">In addition, SSL client certificates can be used to authenticate clients.</span></span>

## <a name="enabling-ssl-on-the-server"></a><span data-ttu-id="d275b-109">在伺服器上啟用 SSL</span><span class="sxs-lookup"><span data-stu-id="d275b-109">Enabling SSL on the Server</span></span>

<span data-ttu-id="d275b-110">若要在 IIS 7 或更新版本中設定 SSL：</span><span class="sxs-lookup"><span data-stu-id="d275b-110">To set up SSL in IIS 7 or later:</span></span>

- <span data-ttu-id="d275b-111">建立或取得憑證。</span><span class="sxs-lookup"><span data-stu-id="d275b-111">Create or get a certificate.</span></span> <span data-ttu-id="d275b-112">若要進行測試，您可以建立自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="d275b-112">For testing, you can create a self-signed certificate.</span></span>
- <span data-ttu-id="d275b-113">新增 HTTPS 系結。</span><span class="sxs-lookup"><span data-stu-id="d275b-113">Add an HTTPS binding.</span></span>

<span data-ttu-id="d275b-114">如需詳細資訊，請參閱[如何在 IIS 7 上設定 SSL](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)。</span><span class="sxs-lookup"><span data-stu-id="d275b-114">For details, see [How to Set Up SSL on IIS 7](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis).</span></span>

<span data-ttu-id="d275b-115">若要進行本機測試，您可以從 Visual Studio 啟用 IIS Express 中的 SSL。</span><span class="sxs-lookup"><span data-stu-id="d275b-115">For local testing, you can enable SSL in IIS Express from Visual Studio.</span></span> <span data-ttu-id="d275b-116">在 屬性視窗中，將  **SSL 已啟用** 設定為  **True**。</span><span class="sxs-lookup"><span data-stu-id="d275b-116">In the Properties window, set **SSL Enabled** to **True**.</span></span> <span data-ttu-id="d275b-117">記下 [ **SSL URL**] 的值;使用此 URL 來測試 HTTPS 連接。</span><span class="sxs-lookup"><span data-stu-id="d275b-117">Note the value of **SSL URL**; use this URL for testing HTTPS connections.</span></span>

![](working-with-ssl-in-web-api/_static/image1.png)

### <a name="enforcing-ssl-in-a-web-api-controller"></a><span data-ttu-id="d275b-118">在 Web API 控制器中強制執行 SSL</span><span class="sxs-lookup"><span data-stu-id="d275b-118">Enforcing SSL in a Web API Controller</span></span>

<span data-ttu-id="d275b-119">如果您同時有 HTTPS 和 HTTP 系結，用戶端仍然可以使用 HTTP 來存取網站。</span><span class="sxs-lookup"><span data-stu-id="d275b-119">If you have both an HTTPS and an HTTP binding, clients can still use HTTP to access the site.</span></span> <span data-ttu-id="d275b-120">您可能會允許某些資源透過 HTTP 提供，而其他資源則需要 SSL。</span><span class="sxs-lookup"><span data-stu-id="d275b-120">You might allow some resources to be available through HTTP, while other resources require SSL.</span></span> <span data-ttu-id="d275b-121">在此情況下，請使用動作篩選準則來要求保護資源的 SSL。</span><span class="sxs-lookup"><span data-stu-id="d275b-121">In that case, use an action filter to require SSL for the protected resources.</span></span> <span data-ttu-id="d275b-122">下列程式碼顯示會檢查 SSL 的 Web API 驗證篩選︰</span><span class="sxs-lookup"><span data-stu-id="d275b-122">The following code shows a Web API authentication filter that checks for SSL:</span></span>

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample1.cs)]

<span data-ttu-id="d275b-123">將此篩選新增至任何需要 SSL 的 Web API 動作︰</span><span class="sxs-lookup"><span data-stu-id="d275b-123">Add this filter to any Web API actions that require SSL:</span></span>

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample2.cs)]

## <a name="ssl-client-certificates"></a><span data-ttu-id="d275b-124">SSL 用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="d275b-124">SSL Client Certificates</span></span>

<span data-ttu-id="d275b-125">SSL 會使用公開金鑰基礎結構憑證來提供驗證。</span><span class="sxs-lookup"><span data-stu-id="d275b-125">SSL provides authentication by using Public Key Infrastructure certificates.</span></span> <span data-ttu-id="d275b-126">伺服器必須提供可向用戶端驗證服務器的憑證。</span><span class="sxs-lookup"><span data-stu-id="d275b-126">The server must provide a certificate that authenticates the server to the client.</span></span> <span data-ttu-id="d275b-127">用戶端不常提供憑證給伺服器，但這是驗證用戶端的一個選項。</span><span class="sxs-lookup"><span data-stu-id="d275b-127">It is less common for the client to provide a certificate to the server, but this is one option for authenticating clients.</span></span> <span data-ttu-id="d275b-128">若要使用用戶端憑證搭配 SSL，您需要有方法將已簽署的憑證散發給您的使用者。</span><span class="sxs-lookup"><span data-stu-id="d275b-128">To use client certificates with SSL, you need a way to distribute signed certificates to your users.</span></span> <span data-ttu-id="d275b-129">對於許多應用程式類型而言，這並不是很好的使用者體驗，但在某些環境（例如企業）中，這可能是可行的。</span><span class="sxs-lookup"><span data-stu-id="d275b-129">For many application types, this will not be a good user experience, but in some environments (for example, enterprise) it may be feasible.</span></span>

| <span data-ttu-id="d275b-130">優點</span><span class="sxs-lookup"><span data-stu-id="d275b-130">Advantages</span></span> | <span data-ttu-id="d275b-131">缺點</span><span class="sxs-lookup"><span data-stu-id="d275b-131">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="d275b-132">-憑證認證比使用者名稱/密碼更強。</span><span class="sxs-lookup"><span data-stu-id="d275b-132">- Certificate credentials are stronger than username/password.</span></span> <span data-ttu-id="d275b-133">-SSL 提供完整的安全通道，其中包含驗證、訊息完整性和訊息加密。</span><span class="sxs-lookup"><span data-stu-id="d275b-133">- SSL provides a complete secure channel, with authentication, message integrity, and message encryption.</span></span> | <span data-ttu-id="d275b-134">-您必須取得並管理 PKI 憑證。</span><span class="sxs-lookup"><span data-stu-id="d275b-134">- You must obtain and manage PKI certificates.</span></span> <span data-ttu-id="d275b-135">-用戶端平臺必須支援 SSL 用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="d275b-135">- The client platform must support SSL client certificates.</span></span> |

<span data-ttu-id="d275b-136">若要設定 IIS 以接受用戶端憑證，請開啟 IIS 管理員，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d275b-136">To configure IIS to accept client certificates, open IIS Manager and perform the following steps:</span></span>

1. <span data-ttu-id="d275b-137">按一下樹狀檢視中的 [網站] 節點。</span><span class="sxs-lookup"><span data-stu-id="d275b-137">Click the site node in the tree view.</span></span>
2. <span data-ttu-id="d275b-138">按兩下中間窗格中的 [ **SSL 設定**] 功能。</span><span class="sxs-lookup"><span data-stu-id="d275b-138">Double-click the **SSL Settings** feature in the middle pane.</span></span>
3. <span data-ttu-id="d275b-139">在 [**用戶端憑證**] 底下，選取下列其中一個選項：</span><span class="sxs-lookup"><span data-stu-id="d275b-139">Under **Client Certificates**, select one of these options:</span></span> 

    - <span data-ttu-id="d275b-140">**接受**： IIS 會接受來自用戶端的憑證，但不需要一個。</span><span class="sxs-lookup"><span data-stu-id="d275b-140">**Accept**: IIS will accept a certificate from the client, but does not require one.</span></span>
    - <span data-ttu-id="d275b-141">**需要**：需要用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="d275b-141">**Require**: Require a client certificate.</span></span> <span data-ttu-id="d275b-142">（若要啟用此選項，您也必須選取 [需要 SSL]）</span><span class="sxs-lookup"><span data-stu-id="d275b-142">(To enable this option, you must also select "Require SSL")</span></span>

<span data-ttu-id="d275b-143">您也可以在 Applicationhost.config 檔案中設定這些選項：</span><span class="sxs-lookup"><span data-stu-id="d275b-143">You can also set these options in the ApplicationHost.config file:</span></span>

[!code-xml[Main](working-with-ssl-in-web-api/samples/sample3.xml)]

<span data-ttu-id="d275b-144">**目的 sslnegotiatecert**旗標表示 iis 會接受來自用戶端的憑證，但不需要它（相當於 IIS 管理員中的 [接受] 選項）。</span><span class="sxs-lookup"><span data-stu-id="d275b-144">The **SslNegotiateCert** flag means IIS will accept a certificate from the client, but does not require one (equivalent to the "Accept" option in IIS Manager).</span></span> <span data-ttu-id="d275b-145">若要要求憑證，請設定**在**旗標。</span><span class="sxs-lookup"><span data-stu-id="d275b-145">To require a certificate, set the **SslRequireCert** flag.</span></span> <span data-ttu-id="d275b-146">若要進行測試，您也可以在本機 applicationhost.config 的 IIS Express 中設定這些選項。設定檔，位於 "Documents\IISExpress\config"。</span><span class="sxs-lookup"><span data-stu-id="d275b-146">For testing, you can also set these options in IIS Express, in the local applicationhost.Config file, located in "Documents\IISExpress\config".</span></span>

### <a name="creating-a-client-certificate-for-testing"></a><span data-ttu-id="d275b-147">建立用於測試的用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="d275b-147">Creating a Client Certificate for Testing</span></span>

<span data-ttu-id="d275b-148">基於測試目的，您可以使用[MakeCert](/windows/desktop/SecCrypto/makecert)來建立用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="d275b-148">For testing purposes, you can use [MakeCert.exe](/windows/desktop/SecCrypto/makecert) to create a client certificate.</span></span> <span data-ttu-id="d275b-149">首先，建立測試根目錄授權單位：</span><span class="sxs-lookup"><span data-stu-id="d275b-149">First, create a test root authority:</span></span>

[!code-console[Main](working-with-ssl-in-web-api/samples/sample4.cmd)]

<span data-ttu-id="d275b-150">Makecert 會提示您輸入私密金鑰的密碼。</span><span class="sxs-lookup"><span data-stu-id="d275b-150">Makecert will prompt you to enter a password for the private key.</span></span>

<span data-ttu-id="d275b-151">接下來，將憑證新增至測試伺服器的「受信任的根憑證授權單位」存放區，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d275b-151">Next, add the certificate to the test server's "Trusted Root Certification Authorities" store, as follows:</span></span>

1. <span data-ttu-id="d275b-152">開啟 MMC。</span><span class="sxs-lookup"><span data-stu-id="d275b-152">Open MMC.</span></span>
2. <span data-ttu-id="d275b-153">在 **[** 檔案] 底下，選取 [**新增/移除嵌入式管理單元**]。</span><span class="sxs-lookup"><span data-stu-id="d275b-153">Under **File**, select **Add/Remove Snap-In**.</span></span>
3. <span data-ttu-id="d275b-154">選取 [**電腦帳戶**]。</span><span class="sxs-lookup"><span data-stu-id="d275b-154">Select **Computer Account**.</span></span>
4. <span data-ttu-id="d275b-155">選取 [**本機電腦**]，然後完成嚮導。</span><span class="sxs-lookup"><span data-stu-id="d275b-155">Select **Local computer** and complete the wizard.</span></span>
5. <span data-ttu-id="d275b-156">在流覽窗格中，展開 [信任的根憑證授權單位] 節點。</span><span class="sxs-lookup"><span data-stu-id="d275b-156">Under the navigation pane, expand the "Trusted Root Certification Authorities" node.</span></span>
6. <span data-ttu-id="d275b-157">在 [**動作**] 功能表上，指向 [**所有**工作]，然後按一下 [匯**入**] 以啟動 [憑證匯入嚮導]。</span><span class="sxs-lookup"><span data-stu-id="d275b-157">On the **Action** menu, point to **All Tasks**, and then click **Import** to start the Certificate Import Wizard.</span></span>
7. <span data-ttu-id="d275b-158">流覽至憑證檔案（TempCA. .cer）。</span><span class="sxs-lookup"><span data-stu-id="d275b-158">Browse to the certificate file, TempCA.cer.</span></span>
8. <span data-ttu-id="d275b-159">按一下 [**開啟**]，然後按 **[下一步**] 並完成嚮導。</span><span class="sxs-lookup"><span data-stu-id="d275b-159">Click **Open**, then click **Next** and complete the wizard.</span></span> <span data-ttu-id="d275b-160">（系統會提示您重新輸入密碼。）</span><span class="sxs-lookup"><span data-stu-id="d275b-160">(You will be prompted to re-enter the password.)</span></span>

<span data-ttu-id="d275b-161">現在，建立由第一個憑證簽署的用戶端憑證：</span><span class="sxs-lookup"><span data-stu-id="d275b-161">Now create a client certificate that is signed by the first certificate:</span></span>

[!code-console[Main](working-with-ssl-in-web-api/samples/sample5.cmd)]

### <a name="using-client-certificates-in-web-api"></a><span data-ttu-id="d275b-162">在 Web API 中使用用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="d275b-162">Using Client Certificates in Web API</span></span>

<span data-ttu-id="d275b-163">在伺服器端上，您可以藉由在要求訊息上呼叫[GetClientCertificate](https://msdn.microsoft.com/library/system.net.http.httprequestmessageextensions.getclientcertificate.aspx)來取得用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="d275b-163">On the server side, you can get the client certificate by calling [GetClientCertificate](https://msdn.microsoft.com/library/system.net.http.httprequestmessageextensions.getclientcertificate.aspx) on the request message.</span></span> <span data-ttu-id="d275b-164">如果沒有用戶端憑證，此方法會傳回 null。</span><span class="sxs-lookup"><span data-stu-id="d275b-164">The method returns null if there is no client certificate.</span></span> <span data-ttu-id="d275b-165">否則，它會傳回**X509Certificate2**實例。</span><span class="sxs-lookup"><span data-stu-id="d275b-165">Otherwise, it returns an **X509Certificate2** instance.</span></span> <span data-ttu-id="d275b-166">使用此物件來取得憑證的資訊，例如簽發者和主旨。</span><span class="sxs-lookup"><span data-stu-id="d275b-166">Use this object to get information from the certificate, such as the issuer and subject.</span></span> <span data-ttu-id="d275b-167">然後您可以使用此資訊進行驗證和/或授權。</span><span class="sxs-lookup"><span data-stu-id="d275b-167">Then you can use this information for authentication and/or authorization.</span></span>

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample6.cs)]
