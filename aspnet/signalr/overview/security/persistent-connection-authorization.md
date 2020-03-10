---
uid: signalr/overview/security/persistent-connection-authorization
title: SignalR 持續連線的驗證和授權 |Microsoft Docs
author: bradygaster
description: 本主題描述如何在持續連線上強制執行授權。 如需將安全性整合至 SignalR 應用程式的一般資訊,。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: e264677b-9c01-47ec-94f9-3cd8f08f94af
msc.legacyurl: /signalr/overview/security/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 7e69d3c1a18f1239142891734ba58cd2b0078f84
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578873"
---
# <a name="authentication-and-authorization-for-signalr-persistent-connections"></a><span data-ttu-id="622c8-104">SignalR 持續連線的驗證和授權</span><span class="sxs-lookup"><span data-stu-id="622c8-104">Authentication and Authorization for SignalR Persistent Connections</span></span>

<span data-ttu-id="622c8-105">由一[Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="622c8-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="622c8-106">本主題描述如何在持續連線上強制執行授權。</span><span class="sxs-lookup"><span data-stu-id="622c8-106">This topic describes how to enforce authorization on a persistent connection.</span></span> <span data-ttu-id="622c8-107">如需將安全性整合到 SignalR 應用程式的一般資訊，請參閱[安全性簡介](introduction-to-security.md)。</span><span class="sxs-lookup"><span data-stu-id="622c8-107">For general information about integrating security into a SignalR application, see [Introduction to Security](introduction-to-security.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="622c8-108">本主題中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="622c8-108">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="622c8-109">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="622c8-109">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="622c8-110">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="622c8-110">.NET 4.5</span></span>
> - <span data-ttu-id="622c8-111">SignalR 第2版</span><span class="sxs-lookup"><span data-stu-id="622c8-111">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="622c8-112">本主題的先前版本</span><span class="sxs-lookup"><span data-stu-id="622c8-112">Previous versions of this topic</span></span>
>
> <span data-ttu-id="622c8-113">如需舊版 SignalR 的詳細資訊，請參閱[SignalR 較舊的版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="622c8-113">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="622c8-114">問題與意見</span><span class="sxs-lookup"><span data-stu-id="622c8-114">Questions and comments</span></span>
>
> <span data-ttu-id="622c8-115">請留下有關您喜歡本教學課程的意見反應，以及我們可以在頁面底部的批註中改進的內容。</span><span class="sxs-lookup"><span data-stu-id="622c8-115">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="622c8-116">如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="622c8-116">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="enforce-authorization"></a><span data-ttu-id="622c8-117">強制執行授權</span><span class="sxs-lookup"><span data-stu-id="622c8-117">Enforce authorization</span></span>

<span data-ttu-id="622c8-118">若要在使用[PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx)時強制執行授權規則，您必須覆寫 `AuthorizeRequest` 方法。</span><span class="sxs-lookup"><span data-stu-id="622c8-118">To enforce authorization rules when using a [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="622c8-119">您不能將 `Authorize` 屬性與持續性連接搭配使用。</span><span class="sxs-lookup"><span data-stu-id="622c8-119">You cannot use the `Authorize` attribute with persistent connections.</span></span> <span data-ttu-id="622c8-120">SignalR 架構會在每個要求之前呼叫 `AuthorizeRequest` 方法，以確認使用者已獲授權執行要求的動作。</span><span class="sxs-lookup"><span data-stu-id="622c8-120">The `AuthorizeRequest` method is called by the SignalR Framework before every request to verify that the user is authorized to perform the requested action.</span></span> <span data-ttu-id="622c8-121">不會從用戶端呼叫 `AuthorizeRequest` 方法;相反地，您會透過應用程式的標準驗證機制來驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="622c8-121">The `AuthorizeRequest` method is not called from the client; instead, you authenticate the user through your application's standard authentication mechanism.</span></span>

<span data-ttu-id="622c8-122">下列範例顯示如何將要求限制為已驗證的使用者。</span><span class="sxs-lookup"><span data-stu-id="622c8-122">The example below shows how to limit requests to authenticated users.</span></span>

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

<span data-ttu-id="622c8-123">您可以在 AuthorizeRequest 方法中新增任何自訂的授權邏輯;例如，檢查使用者是否屬於特定的角色。</span><span class="sxs-lookup"><span data-stu-id="622c8-123">You can add any customized authorization logic in the AuthorizeRequest method; such as, checking whether a user belongs to a particular role.</span></span>
