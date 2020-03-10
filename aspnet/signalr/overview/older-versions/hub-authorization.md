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
# <a name="authentication-and-authorization-for-signalr-hubs-signalr-1x"></a>SignalR 中樞的驗證與授權 (SignalR 1.x)

由一[Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本主題說明如何限制哪些使用者或角色可以存取中樞方法。

## <a name="overview"></a>概觀

本主題包含下列各節：

- [授權屬性](#authorizeattribute)
- [所有中樞都需要驗證](#requireauth)
- [自訂授權](#custom)
- [將驗證資訊傳遞給用戶端](#passauth)
- [.NET 用戶端的驗證選項](#authoptions)

    - [使用表單驗證的 Cookie](#cookie)
    - [Windows 驗證](#windows)
    - [連接標頭](#header)
    - [[MSSQLSERVER 的通訊協定內容]](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a>授權屬性

SignalR 提供[授權](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx)屬性，以指定哪些使用者或角色可以存取中樞或方法。 這個屬性位於 `Microsoft.AspNet.SignalR` 命名空間中。 您會將 `Authorize` 屬性套用至中樞或集線器中的特定方法。 當您將 `Authorize` 屬性套用至中樞類別時，指定的授權需求會套用至中樞內的所有方法。 您可以套用的不同授權需求類型如下所示。 如果沒有 `Authorize` 屬性，中樞上的所有公用方法都可供連線至中樞的用戶端使用。

如果您已在 web 應用程式中定義名為 "Admin" 的角色，您可以指定只有該角色中的使用者可以使用下列程式碼來存取中樞。

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

或者，您可以指定中樞包含一個可供所有使用者使用的方法，以及第二個只提供給已驗證使用者的方法，如下所示。

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

下列範例會解決不同的授權案例：

- `[Authorize]` –只有已驗證的使用者
- `[Authorize(Roles = "Admin,Manager")]` –只有指定角色中的已驗證使用者
- `[Authorize(Users = "user1,user2")]` –只有具有指定使用者名稱的已驗證使用者
- `[Authorize(RequireOutgoing=false)]` –只有經過驗證的使用者才可以叫用中樞，但只有特定使用者可以傳送訊息時，才會限制從伺服器到用戶端的呼叫（例如），而其他人則可以接收訊息。 RequireOutgoing 屬性只能套用至整個中樞，而不能套用至中樞內的個別方法。 當 RequireOutgoing 未設定為 false 時，只會從伺服器呼叫符合授權需求的使用者。

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a>所有中樞都需要驗證

您可以在應用程式啟動時呼叫[RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx)方法，以要求應用程式中所有中樞和中樞方法的驗證。 當您有多個中樞，而且想要強制執行所有的驗證需求時，您可以使用此方法。 使用此方法時，您無法指定角色、使用者或傳出授權。 您只能指定將中樞方法的存取限制為已驗證的使用者。 不過，您仍然可以將授權屬性套用至中樞或方法，以指定其他需求。 除了驗證的基本需求之外，還會套用您在屬性中指定的任何需求。

下列範例顯示 global.asax 檔案，其會將所有中樞方法限制為已驗證的使用者。

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

如果您在處理 SignalR 要求後呼叫 `RequireAuthentication()` 方法，SignalR 將會擲回 `InvalidOperationException` 例外狀況。 因為在叫用管線之後無法將模組加入至 HubPipeline，所以會擲回這個例外狀況。 先前的範例示範如何在 `Application_Start` 方法中呼叫 `RequireAuthentication` 方法，這會在處理第一個要求之前執行一次。

<a id="custom"></a>

## <a name="customized-authorization"></a>自訂授權

如果您需要自訂如何判斷授權，您可以建立衍生自 `AuthorizeAttribute` 的類別，並覆寫[UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx)方法。 會針對每個要求呼叫這個方法，以判斷使用者是否有權完成要求。 在覆寫的方法中，您會為您的授權案例提供必要的邏輯。 下列範例示範如何透過宣告式身分識別來強制執行授權。

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a>將驗證資訊傳遞給用戶端

在用戶端上執行的程式碼中，您可能需要使用驗證資訊。 在用戶端上呼叫方法時，您會傳遞所需的資訊。 例如，聊天應用程式方法可以將張貼訊息之人員的使用者名稱當做參數傳遞，如下所示。

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

或者，您可以建立物件來代表驗證資訊，並將該物件當做參數傳遞，如下所示。

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

您絕對不應該將一個用戶端的連線識別碼傳遞給其他用戶端，因為惡意使用者可能會使用它來模擬來自該用戶端的要求。

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a>.NET 用戶端的驗證選項

當您的 .NET 用戶端（例如主控台應用程式）與受限於已驗證使用者的中樞互動時，您可以在 cookie、連接標頭或憑證中傳遞驗證認證。 本節中的範例示範如何使用這些不同的方法來驗證使用者。 它們不是功能完整的 SignalR 應用程式。 如需有關使用 SignalR 的 .NET 用戶端詳細資訊，請參閱[中樞 API 指南-.Net 用戶端](../guide-to-the-api/hubs-api-guide-net-client.md)。

<a id="cookie"></a>

### <a name="cookie"></a>Cookie

當您的 .NET 用戶端與使用 ASP.NET 表單驗證的中樞互動時，您必須手動設定連線上的驗證 cookie。 您會將 cookie 新增至[HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx)物件上的 `CookieContainer` 屬性。 下列範例顯示主控台應用程式，它會從網頁抓取驗證 cookie，並將該 cookie 新增至連接。 範例中的 URL `https://www.contoso.com/RemoteLogin` 會指向您必須建立的網頁。 頁面會抓取張貼的使用者名稱和密碼，並嘗試以認證登入使用者。

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

主控台應用程式會將認證張貼至 www.contoso.com/RemoteLogin，而這可能會參考包含下列程式碼後置檔案的空白頁面。

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a>Windows 驗證

使用 Windows 驗證時，您可以使用[DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx)屬性傳遞目前使用者的認證。 您可以將連接的認證設定為 DefaultCredentials 的值。

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a>連接標頭

如果您的應用程式未使用 cookie，您可以在連接標頭中傳遞使用者資訊。 例如，您可以在連接標頭中傳遞權杖。

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

然後，在中樞內，您會驗證使用者的權杖。

<a id="certificate"></a>

### <a name="certificate"></a>憑證

您可以傳遞用戶端憑證來驗證使用者。 您會在建立連接時新增憑證。 下列範例只會顯示如何將用戶端憑證新增至連線;它不會顯示完整的主控台應用程式。 它會使用[X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx)類別，它會提供數種不同的方式來建立憑證。

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
