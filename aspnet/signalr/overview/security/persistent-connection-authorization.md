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
# <a name="authentication-and-authorization-for-signalr-persistent-connections"></a>SignalR 持續連線的驗證和授權

由一[Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本主題描述如何在持續連線上強制執行授權。 如需將安全性整合到 SignalR 應用程式的一般資訊，請參閱[安全性簡介](introduction-to-security.md)。
>
> ## <a name="software-versions-used-in-this-topic"></a>本主題中使用的軟體版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR 第2版
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>本主題的先前版本
>
> 如需舊版 SignalR 的詳細資訊，請參閱[SignalR 較舊的版本](../older-versions/index.md)。
>
> ## <a name="questions-and-comments"></a>問題與意見
>
> 請留下有關您喜歡本教學課程的意見反應，以及我們可以在頁面底部的批註中改進的內容。 如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。

## <a name="enforce-authorization"></a>強制執行授權

若要在使用[PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx)時強制執行授權規則，您必須覆寫 `AuthorizeRequest` 方法。 您不能將 `Authorize` 屬性與持續性連接搭配使用。 SignalR 架構會在每個要求之前呼叫 `AuthorizeRequest` 方法，以確認使用者已獲授權執行要求的動作。 不會從用戶端呼叫 `AuthorizeRequest` 方法;相反地，您會透過應用程式的標準驗證機制來驗證使用者。

下列範例顯示如何將要求限制為已驗證的使用者。

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

您可以在 AuthorizeRequest 方法中新增任何自訂的授權邏輯;例如，檢查使用者是否屬於特定的角色。
