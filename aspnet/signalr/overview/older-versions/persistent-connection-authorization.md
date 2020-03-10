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
# <a name="authentication-and-authorization-for-signalr-persistent-connections-signalr-1x"></a>SignalR 持續連線的驗證與授權 (SignalR 1.x)

由一[Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本主題描述如何在持續連線上強制執行授權。 如需將安全性整合到 SignalR 應用程式的一般資訊，請參閱[安全性簡介](index.md)。

## <a name="enforce-authorization"></a>強制執行授權

若要在使用[PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx)時強制執行授權規則，您必須覆寫 `AuthorizeRequest` 方法。 您不能將 `Authorize` 屬性與持續性連接搭配使用。 SignalR 架構會在每個要求之前呼叫 `AuthorizeRequest` 方法，以確認使用者已獲授權執行要求的動作。 不會從用戶端呼叫 `AuthorizeRequest` 方法;相反地，您會透過應用程式的標準驗證機制來驗證使用者。

下列範例顯示如何將要求限制為已驗證的使用者。

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

您可以在 AuthorizeRequest 方法中新增任何自訂的授權邏輯;例如，檢查使用者是否屬於特定的角色。
