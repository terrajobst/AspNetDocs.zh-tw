---
uid: signalr/overview/older-versions/persistent-connection-authorization
title: SignalR 持續連線的驗證和授權（SignalR 1.x） |Microsoft Docs
author: bradygaster
description: 本主題描述如何在持續連線上強制執行授權。 如需將安全性整合至 SignalR 應用程式的一般資訊,。
ms.author: bradyg
ms.date: 10/21/2013
ms.assetid: c34bc627-41af-4c21-a817-e97a19a7f252
msc.legacyurl: /signalr/overview/older-versions/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 9ccc59e3ea502daf12ce82382ab30ca73ca0f9b5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536537"
---
# <a name="authentication-and-authorization-for-signalr-persistent-connections-signalr-1x"></a><span data-ttu-id="f6069-104">SignalR 持續連線的驗證與授權 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="f6069-104">Authentication and Authorization for SignalR Persistent Connections (SignalR 1.x)</span></span>

<span data-ttu-id="f6069-105">由一[Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="f6069-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="f6069-106">本主題描述如何在持續連線上強制執行授權。</span><span class="sxs-lookup"><span data-stu-id="f6069-106">This topic describes how to enforce authorization on a persistent connection.</span></span> <span data-ttu-id="f6069-107">如需將安全性整合到 SignalR 應用程式的一般資訊，請參閱[安全性簡介](index.md)。</span><span class="sxs-lookup"><span data-stu-id="f6069-107">For general information about integrating security into a SignalR application, see [Introduction to Security](index.md).</span></span>

## <a name="enforce-authorization"></a><span data-ttu-id="f6069-108">強制執行授權</span><span class="sxs-lookup"><span data-stu-id="f6069-108">Enforce authorization</span></span>

<span data-ttu-id="f6069-109">若要在使用[PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx)時強制執行授權規則，您必須覆寫 `AuthorizeRequest` 方法。</span><span class="sxs-lookup"><span data-stu-id="f6069-109">To enforce authorization rules when using a [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="f6069-110">您不能將 `Authorize` 屬性與持續性連接搭配使用。</span><span class="sxs-lookup"><span data-stu-id="f6069-110">You cannot use the `Authorize` attribute with persistent connections.</span></span> <span data-ttu-id="f6069-111">SignalR 架構會在每個要求之前呼叫 `AuthorizeRequest` 方法，以確認使用者已獲授權執行要求的動作。</span><span class="sxs-lookup"><span data-stu-id="f6069-111">The `AuthorizeRequest` method is called by the SignalR Framework before every request to verify that the user is authorized to perform the requested action.</span></span> <span data-ttu-id="f6069-112">不會從用戶端呼叫 `AuthorizeRequest` 方法;相反地，您會透過應用程式的標準驗證機制來驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="f6069-112">The `AuthorizeRequest` method is not called from the client; instead, you authenticate the user through your application's standard authentication mechanism.</span></span>

<span data-ttu-id="f6069-113">下列範例顯示如何將要求限制為已驗證的使用者。</span><span class="sxs-lookup"><span data-stu-id="f6069-113">The example below shows how to limit requests to authenticated users.</span></span>

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

<span data-ttu-id="f6069-114">您可以在 AuthorizeRequest 方法中新增任何自訂的授權邏輯;例如，檢查使用者是否屬於特定的角色。</span><span class="sxs-lookup"><span data-stu-id="f6069-114">You can add any customized authorization logic in the AuthorizeRequest method; such as, checking whether a user belongs to a particular role.</span></span>
