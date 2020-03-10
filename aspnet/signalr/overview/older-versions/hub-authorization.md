---
uid: signalr/overview/older-versions/hub-authorization
title: SignalR 中樞的驗證和授權（SignalR 1.x） |Microsoft Docs
author: bradygaster
description: 本主題說明如何限制哪些使用者或角色可以存取中樞方法。
ms.author: bradyg
ms.date: 10/17/2013
ms.assetid: 3d2dfc0e-eac2-4076-a468-325d3d01cc7b
msc.legacyurl: /signalr/overview/older-versions/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: 8182677c8931f060d98d17008b16ad545bee4e69
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558531"
---
# <a name="authentication-and-authorization-for-signalr-hubs-signalr-1x"></a><span data-ttu-id="32f4c-103">SignalR 中樞的驗證與授權 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="32f4c-103">Authentication and Authorization for SignalR Hubs (SignalR 1.x)</span></span>

<span data-ttu-id="32f4c-104">由一[Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="32f4c-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="32f4c-105">本主題說明如何限制哪些使用者或角色可以存取中樞方法。</span><span class="sxs-lookup"><span data-stu-id="32f4c-105">This topic describes how to restrict which users or roles can access hub methods.</span></span>

## <a name="overview"></a><span data-ttu-id="32f4c-106">概觀</span><span class="sxs-lookup"><span data-stu-id="32f4c-106">Overview</span></span>

<span data-ttu-id="32f4c-107">本主題包含下列各節：</span><span class="sxs-lookup"><span data-stu-id="32f4c-107">This topic contains the following sections:</span></span>

- [<span data-ttu-id="32f4c-108">授權屬性</span><span class="sxs-lookup"><span data-stu-id="32f4c-108">Authorize attribute</span></span>](#authorizeattribute)
- [<span data-ttu-id="32f4c-109">所有中樞都需要驗證</span><span class="sxs-lookup"><span data-stu-id="32f4c-109">Require authentication for all hubs</span></span>](#requireauth)
- [<span data-ttu-id="32f4c-110">自訂授權</span><span class="sxs-lookup"><span data-stu-id="32f4c-110">Customized authorization</span></span>](#custom)
- [<span data-ttu-id="32f4c-111">將驗證資訊傳遞給用戶端</span><span class="sxs-lookup"><span data-stu-id="32f4c-111">Pass authentication information to clients</span></span>](#passauth)
- [<span data-ttu-id="32f4c-112">.NET 用戶端的驗證選項</span><span class="sxs-lookup"><span data-stu-id="32f4c-112">Authentication options for .NET clients</span></span>](#authoptions)

    - [<span data-ttu-id="32f4c-113">使用表單驗證的 Cookie</span><span class="sxs-lookup"><span data-stu-id="32f4c-113">Cookie with Forms Authentication</span></span>](#cookie)
    - [<span data-ttu-id="32f4c-114">Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="32f4c-114">Windows Authentication</span></span>](#windows)
    - [<span data-ttu-id="32f4c-115">連接標頭</span><span class="sxs-lookup"><span data-stu-id="32f4c-115">Connection header</span></span>](#header)
    - <span data-ttu-id="32f4c-116">[[MSSQLSERVER 的通訊協定內容]](#certificate)</span><span class="sxs-lookup"><span data-stu-id="32f4c-116">[Certificate](#certificate)</span></span>

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a><span data-ttu-id="32f4c-117">授權屬性</span><span class="sxs-lookup"><span data-stu-id="32f4c-117">Authorize attribute</span></span>

<span data-ttu-id="32f4c-118">SignalR 提供[授權](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx)屬性，以指定哪些使用者或角色可以存取中樞或方法。</span><span class="sxs-lookup"><span data-stu-id="32f4c-118">SignalR provides the [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) attribute to specify which users or roles have access to a hub or method.</span></span> <span data-ttu-id="32f4c-119">這個屬性位於 `Microsoft.AspNet.SignalR` 命名空間中。</span><span class="sxs-lookup"><span data-stu-id="32f4c-119">This attribute is located in the `Microsoft.AspNet.SignalR` namespace.</span></span> <span data-ttu-id="32f4c-120">您會將 `Authorize` 屬性套用至中樞或集線器中的特定方法。</span><span class="sxs-lookup"><span data-stu-id="32f4c-120">You apply the `Authorize` attribute to either a hub or particular methods in a hub.</span></span> <span data-ttu-id="32f4c-121">當您將 `Authorize` 屬性套用至中樞類別時，指定的授權需求會套用至中樞內的所有方法。</span><span class="sxs-lookup"><span data-stu-id="32f4c-121">When you apply the `Authorize` attribute to a hub class, the specified authorization requirement is applied to all of the methods in the hub.</span></span> <span data-ttu-id="32f4c-122">您可以套用的不同授權需求類型如下所示。</span><span class="sxs-lookup"><span data-stu-id="32f4c-122">The different types of authorization requirements that you can apply are shown below.</span></span> <span data-ttu-id="32f4c-123">如果沒有 `Authorize` 屬性，中樞上的所有公用方法都可供連線至中樞的用戶端使用。</span><span class="sxs-lookup"><span data-stu-id="32f4c-123">Without the `Authorize` attribute, all public methods on the hub are available to a client that is connected to the hub.</span></span>

<span data-ttu-id="32f4c-124">如果您已在 web 應用程式中定義名為 "Admin" 的角色，您可以指定只有該角色中的使用者可以使用下列程式碼來存取中樞。</span><span class="sxs-lookup"><span data-stu-id="32f4c-124">If you have defined a role named "Admin" in your web application, you could specify that only users in that role can access a hub with the following code.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

<span data-ttu-id="32f4c-125">或者，您可以指定中樞包含一個可供所有使用者使用的方法，以及第二個只提供給已驗證使用者的方法，如下所示。</span><span class="sxs-lookup"><span data-stu-id="32f4c-125">Or, you can specify that a hub contains one method that is available to all users, and a second method that is only available to authenticated users, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

<span data-ttu-id="32f4c-126">下列範例會解決不同的授權案例：</span><span class="sxs-lookup"><span data-stu-id="32f4c-126">The following examples address different authorization scenarios:</span></span>

- <span data-ttu-id="32f4c-127">`[Authorize]` –只有已驗證的使用者</span><span class="sxs-lookup"><span data-stu-id="32f4c-127">`[Authorize]` – only authenticated users</span></span>
- <span data-ttu-id="32f4c-128">`[Authorize(Roles = "Admin,Manager")]` –只有指定角色中的已驗證使用者</span><span class="sxs-lookup"><span data-stu-id="32f4c-128">`[Authorize(Roles = "Admin,Manager")]` – only authenticated users in the specified roles</span></span>
- <span data-ttu-id="32f4c-129">`[Authorize(Users = "user1,user2")]` –只有具有指定使用者名稱的已驗證使用者</span><span class="sxs-lookup"><span data-stu-id="32f4c-129">`[Authorize(Users = "user1,user2")]` – only authenticated users with the specified user names</span></span>
- <span data-ttu-id="32f4c-130">`[Authorize(RequireOutgoing=false)]` –只有經過驗證的使用者才可以叫用中樞，但只有特定使用者可以傳送訊息時，才會限制從伺服器到用戶端的呼叫（例如），而其他人則可以接收訊息。</span><span class="sxs-lookup"><span data-stu-id="32f4c-130">`[Authorize(RequireOutgoing=false)]` – only authenticated users can invoke the hub, but calls from the server back to clients are not limited by authorization, such as, when only certain users can send a message but all others can receive the message.</span></span> <span data-ttu-id="32f4c-131">RequireOutgoing 屬性只能套用至整個中樞，而不能套用至中樞內的個別方法。</span><span class="sxs-lookup"><span data-stu-id="32f4c-131">The RequireOutgoing property can only be applied to the entire hub, not on individuals methods within the hub.</span></span> <span data-ttu-id="32f4c-132">當 RequireOutgoing 未設定為 false 時，只會從伺服器呼叫符合授權需求的使用者。</span><span class="sxs-lookup"><span data-stu-id="32f4c-132">When RequireOutgoing is not set to false, only users that meet the authorization requirement are called from the server.</span></span>

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a><span data-ttu-id="32f4c-133">所有中樞都需要驗證</span><span class="sxs-lookup"><span data-stu-id="32f4c-133">Require authentication for all hubs</span></span>

<span data-ttu-id="32f4c-134">您可以在應用程式啟動時呼叫[RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx)方法，以要求應用程式中所有中樞和中樞方法的驗證。</span><span class="sxs-lookup"><span data-stu-id="32f4c-134">You can require authentication for all hubs and hub methods in your application by calling the [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="32f4c-135">當您有多個中樞，而且想要強制執行所有的驗證需求時，您可以使用此方法。</span><span class="sxs-lookup"><span data-stu-id="32f4c-135">You might use this method when you have multiple hubs and want to enforce an authentication requirement for all of them.</span></span> <span data-ttu-id="32f4c-136">使用此方法時，您無法指定角色、使用者或傳出授權。</span><span class="sxs-lookup"><span data-stu-id="32f4c-136">With this method, you cannot specify role, user, or outgoing authorization.</span></span> <span data-ttu-id="32f4c-137">您只能指定將中樞方法的存取限制為已驗證的使用者。</span><span class="sxs-lookup"><span data-stu-id="32f4c-137">You can only specify that access to the hub methods is restricted to authenticated users.</span></span> <span data-ttu-id="32f4c-138">不過，您仍然可以將授權屬性套用至中樞或方法，以指定其他需求。</span><span class="sxs-lookup"><span data-stu-id="32f4c-138">However, you can still apply the Authorize attribute to hubs or methods to specify additional requirements.</span></span> <span data-ttu-id="32f4c-139">除了驗證的基本需求之外，還會套用您在屬性中指定的任何需求。</span><span class="sxs-lookup"><span data-stu-id="32f4c-139">Any requirement you specify in attributes is applied in addition to the basic requirement of authentication.</span></span>

<span data-ttu-id="32f4c-140">下列範例顯示 global.asax 檔案，其會將所有中樞方法限制為已驗證的使用者。</span><span class="sxs-lookup"><span data-stu-id="32f4c-140">The following example shows a Global.asax file which restricts all hub methods to authenticated users.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

<span data-ttu-id="32f4c-141">如果您在處理 SignalR 要求後呼叫 `RequireAuthentication()` 方法，SignalR 將會擲回 `InvalidOperationException` 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="32f4c-141">If you call the `RequireAuthentication()` method after a SignalR request has been processed, SignalR will throw a `InvalidOperationException` exception.</span></span> <span data-ttu-id="32f4c-142">因為在叫用管線之後無法將模組加入至 HubPipeline，所以會擲回這個例外狀況。</span><span class="sxs-lookup"><span data-stu-id="32f4c-142">This exception is thrown because you cannot add a module to the HubPipeline after the pipeline has been invoked.</span></span> <span data-ttu-id="32f4c-143">先前的範例示範如何在 `Application_Start` 方法中呼叫 `RequireAuthentication` 方法，這會在處理第一個要求之前執行一次。</span><span class="sxs-lookup"><span data-stu-id="32f4c-143">The previous example shows calling the `RequireAuthentication` method in the `Application_Start` method which is executed one time prior to handling the first request.</span></span>

<a id="custom"></a>

## <a name="customized-authorization"></a><span data-ttu-id="32f4c-144">自訂授權</span><span class="sxs-lookup"><span data-stu-id="32f4c-144">Customized authorization</span></span>

<span data-ttu-id="32f4c-145">如果您需要自訂如何判斷授權，您可以建立衍生自 `AuthorizeAttribute` 的類別，並覆寫[UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="32f4c-145">If you need to customize how authorization is determined, you can create a class that derives from `AuthorizeAttribute` and override the [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) method.</span></span> <span data-ttu-id="32f4c-146">會針對每個要求呼叫這個方法，以判斷使用者是否有權完成要求。</span><span class="sxs-lookup"><span data-stu-id="32f4c-146">This method is called for each request to determine whether the user is authorized to complete the request.</span></span> <span data-ttu-id="32f4c-147">在覆寫的方法中，您會為您的授權案例提供必要的邏輯。</span><span class="sxs-lookup"><span data-stu-id="32f4c-147">In the overridden method, you provide the necessary logic for your authorization scenario.</span></span> <span data-ttu-id="32f4c-148">下列範例示範如何透過宣告式身分識別來強制執行授權。</span><span class="sxs-lookup"><span data-stu-id="32f4c-148">The following example shows how to enforce authorization through claims-based identity.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a><span data-ttu-id="32f4c-149">將驗證資訊傳遞給用戶端</span><span class="sxs-lookup"><span data-stu-id="32f4c-149">Pass authentication information to clients</span></span>

<span data-ttu-id="32f4c-150">在用戶端上執行的程式碼中，您可能需要使用驗證資訊。</span><span class="sxs-lookup"><span data-stu-id="32f4c-150">You may need to use authentication information in the code that runs on the client.</span></span> <span data-ttu-id="32f4c-151">在用戶端上呼叫方法時，您會傳遞所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="32f4c-151">You pass the required information when calling the methods on the client.</span></span> <span data-ttu-id="32f4c-152">例如，聊天應用程式方法可以將張貼訊息之人員的使用者名稱當做參數傳遞，如下所示。</span><span class="sxs-lookup"><span data-stu-id="32f4c-152">For example, a chat application method could pass as a parameter the user name of the person posting a message, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

<span data-ttu-id="32f4c-153">或者，您可以建立物件來代表驗證資訊，並將該物件當做參數傳遞，如下所示。</span><span class="sxs-lookup"><span data-stu-id="32f4c-153">Or, you can create an object to represent the authentication information and pass that object as a parameter, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

<span data-ttu-id="32f4c-154">您絕對不應該將一個用戶端的連線識別碼傳遞給其他用戶端，因為惡意使用者可能會使用它來模擬來自該用戶端的要求。</span><span class="sxs-lookup"><span data-stu-id="32f4c-154">You should never pass one client's connection id to other clients, as a malicious user could use it to mimic a request from that client.</span></span>

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a><span data-ttu-id="32f4c-155">.NET 用戶端的驗證選項</span><span class="sxs-lookup"><span data-stu-id="32f4c-155">Authentication options for .NET clients</span></span>

<span data-ttu-id="32f4c-156">當您的 .NET 用戶端（例如主控台應用程式）與受限於已驗證使用者的中樞互動時，您可以在 cookie、連接標頭或憑證中傳遞驗證認證。</span><span class="sxs-lookup"><span data-stu-id="32f4c-156">When you have a .NET client, such as a console app, which interacts with a hub that is limited to authenticated users, you can pass the authentication credentials in a cookie, the connection header, or a certificate.</span></span> <span data-ttu-id="32f4c-157">本節中的範例示範如何使用這些不同的方法來驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="32f4c-157">The examples in this section show how to use those different methods for authenticating a user.</span></span> <span data-ttu-id="32f4c-158">它們不是功能完整的 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="32f4c-158">They are not fully-functional SignalR apps.</span></span> <span data-ttu-id="32f4c-159">如需有關使用 SignalR 的 .NET 用戶端詳細資訊，請參閱[中樞 API 指南-.Net 用戶端](../guide-to-the-api/hubs-api-guide-net-client.md)。</span><span class="sxs-lookup"><span data-stu-id="32f4c-159">For more information about .NET clients with SignalR, see [Hubs API Guide - .NET Client](../guide-to-the-api/hubs-api-guide-net-client.md).</span></span>

<a id="cookie"></a>

### <a name="cookie"></a><span data-ttu-id="32f4c-160">Cookie</span><span class="sxs-lookup"><span data-stu-id="32f4c-160">Cookie</span></span>

<span data-ttu-id="32f4c-161">當您的 .NET 用戶端與使用 ASP.NET 表單驗證的中樞互動時，您必須手動設定連線上的驗證 cookie。</span><span class="sxs-lookup"><span data-stu-id="32f4c-161">When your .NET client interacts with a hub that uses ASP.NET Forms Authentication, you will need to manually set the authentication cookie on the connection.</span></span> <span data-ttu-id="32f4c-162">您會將 cookie 新增至[HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx)物件上的 `CookieContainer` 屬性。</span><span class="sxs-lookup"><span data-stu-id="32f4c-162">You add the cookie to the `CookieContainer` property on the [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) object.</span></span> <span data-ttu-id="32f4c-163">下列範例顯示主控台應用程式，它會從網頁抓取驗證 cookie，並將該 cookie 新增至連接。</span><span class="sxs-lookup"><span data-stu-id="32f4c-163">The following example shows a console app that retrieves an authentication cookie from a web page and adds that cookie to the connection.</span></span> <span data-ttu-id="32f4c-164">範例中的 URL `https://www.contoso.com/RemoteLogin` 會指向您必須建立的網頁。</span><span class="sxs-lookup"><span data-stu-id="32f4c-164">The URL `https://www.contoso.com/RemoteLogin` in the example points to a web page that you would need to create.</span></span> <span data-ttu-id="32f4c-165">頁面會抓取張貼的使用者名稱和密碼，並嘗試以認證登入使用者。</span><span class="sxs-lookup"><span data-stu-id="32f4c-165">The page would retrieve the posted user name and password, and attempt to log in the user with the credentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

<span data-ttu-id="32f4c-166">主控台應用程式會將認證張貼至 www.contoso.com/RemoteLogin，而這可能會參考包含下列程式碼後置檔案的空白頁面。</span><span class="sxs-lookup"><span data-stu-id="32f4c-166">The console app posts the credentials to www.contoso.com/RemoteLogin which could refer to an empty page that contains the following code-behind file.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a><span data-ttu-id="32f4c-167">Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="32f4c-167">Windows authentication</span></span>

<span data-ttu-id="32f4c-168">使用 Windows 驗證時，您可以使用[DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx)屬性傳遞目前使用者的認證。</span><span class="sxs-lookup"><span data-stu-id="32f4c-168">When using Windows authentication, you can pass the current user's credentials by using the [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) property.</span></span> <span data-ttu-id="32f4c-169">您可以將連接的認證設定為 DefaultCredentials 的值。</span><span class="sxs-lookup"><span data-stu-id="32f4c-169">You set the credentials for the connection to the value of the DefaultCredentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a><span data-ttu-id="32f4c-170">連接標頭</span><span class="sxs-lookup"><span data-stu-id="32f4c-170">Connection header</span></span>

<span data-ttu-id="32f4c-171">如果您的應用程式未使用 cookie，您可以在連接標頭中傳遞使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="32f4c-171">If your application is not using cookies, you can pass user information in the connection header.</span></span> <span data-ttu-id="32f4c-172">例如，您可以在連接標頭中傳遞權杖。</span><span class="sxs-lookup"><span data-stu-id="32f4c-172">For example, you can pass a token in the connection header.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

<span data-ttu-id="32f4c-173">然後，在中樞內，您會驗證使用者的權杖。</span><span class="sxs-lookup"><span data-stu-id="32f4c-173">Then, in the hub, you would verify the user's token.</span></span>

<a id="certificate"></a>

### <a name="certificate"></a><span data-ttu-id="32f4c-174">憑證</span><span class="sxs-lookup"><span data-stu-id="32f4c-174">Certificate</span></span>

<span data-ttu-id="32f4c-175">您可以傳遞用戶端憑證來驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="32f4c-175">You can pass a client certificate to verify the user.</span></span> <span data-ttu-id="32f4c-176">您會在建立連接時新增憑證。</span><span class="sxs-lookup"><span data-stu-id="32f4c-176">You add the certificate when creating the connection.</span></span> <span data-ttu-id="32f4c-177">下列範例只會顯示如何將用戶端憑證新增至連線;它不會顯示完整的主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="32f4c-177">The following example shows only how to add a client certificate to the connection; it does not show the full console app.</span></span> <span data-ttu-id="32f4c-178">它會使用[X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx)類別，它會提供數種不同的方式來建立憑證。</span><span class="sxs-lookup"><span data-stu-id="32f4c-178">It uses the [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) class which provides several different ways to create the certificate.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
