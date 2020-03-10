---
uid: signalr/overview/guide-to-the-api/working-with-groups
title: 在 SignalR 中使用群組 |Microsoft Docs
author: bradygaster
description: 本主題說明如何使用中樞 API 來保存群組成員資格資訊。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: cd378ecd-3e9e-4236-b902-65916d85a048
msc.legacyurl: /signalr/overview/guide-to-the-api/working-with-groups
msc.type: authoredcontent
ms.openlocfilehash: 46dd952fc4902b37c981a111dfa344dad79bb668
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558580"
---
# <a name="working-with-groups-in-signalr"></a>使用 SignalR 的群組

由一[Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本主題說明如何將使用者新增至群組，並保存群組成員資格資訊。
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

## <a name="overview"></a>概觀

SignalR 中的群組提供一種方法，可將訊息廣播到已連線用戶端的指定子集。 群組可以有任意數目的用戶端，而用戶端可以是任意數目群組的成員。 您不需要明確建立群組。 實際上，當您第一次在群組的呼叫中指定其名稱時，會自動建立群組。 [加入] 會在您從其中的成員資格移除最後一個連接時刪除。 如需使用群組的簡介，請參閱《中樞 API-伺服器指南》中的[如何從中樞類別管理群組成員資格](hubs-api-guide-server.md#groupsfromhub)。

沒有 API 可取得群組成員資格清單或群組清單。 SignalR 會根據 pub/sub 模型將訊息傳送至用戶端和群組，而伺服器不會維護群組或群組成員資格的清單。 這有助於最大化擴充性，因為每當您將節點加入至 web 伺服陣列時，SignalR 維護的任何狀態都必須傳播到新的節點。

當您使用 `Groups.Add` 方法將使用者新增至群組時，使用者會在目前的連線期間收到導向該群組的訊息，但該群組中的使用者成員資格不會保存在目前的連線範圍之外。 如果您想要永久保留群組和群組成員資格的相關資訊，您必須將該資料儲存在資料庫或 Azure 資料表儲存體之類的儲存機制中。 然後，每次使用者連線到您的應用程式時，您會從使用者所屬的儲存機制中抓取，並手動將該使用者新增至這些群組。

在暫時中斷之後重新連線時，使用者會自動重新加入先前指派的群組。 自動重新加入群組只有在重新連接時才適用，而不是在建立新的連接時使用。 數位簽署的權杖會從用戶端傳遞，其中包含先前指派之群組的清單。 如果您想要確認使用者是否屬於要求的群組，您可以覆寫預設行為。

本主題包含下列章節：

- [新增和移除使用者](#add)
- [呼叫群組的成員](#call)
- [在資料庫中儲存群組成員資格](#storedatabase)
- [在 Azure 資料表儲存體中儲存群組成員資格](#storeazuretable)
- [重新連接時驗證群組成員資格](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a>新增和移除使用者

若要新增或移除群組中的使用者，您可以呼叫[add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx)或[remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx)方法，並傳入使用者的連接識別碼和群組的名稱作為參數。 當連接結束時，您不需要手動從群組中移除使用者。

下列範例顯示中樞方法中使用的 `Groups.Add` 和 `Groups.Remove` 方法。

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

`Groups.Add` 和 `Groups.Remove` 方法會以非同步方式執行。

如果您想要將用戶端新增至群組，並使用群組立即將訊息傳送至用戶端，您必須確定群組. Add 方法會先完成。 下列程式碼範例示範如何執行這項操作。

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

一般來說，呼叫 `Groups.Remove` 方法時不應該包含 `await`，因為您嘗試移除的連線識別碼可能無法再使用。 在此情況下，會在要求超時之後擲回 `TaskCanceledException`。如果您的應用程式必須在將訊息傳送至群組之前，確保已從群組中移除使用者，您可以在 `Groups.Remove`之前加入 `await`，然後攔截可能會擲回的 `TaskCanceledException` 例外狀況。

<a id="call"></a>

## <a name="calling-members-of-a-group"></a>呼叫群組的成員

您可以將訊息傳送給群組的所有成員，或只傳送給群組的指定成員，如下列範例所示。

- 指定群組中**所有**已連線的用戶端。

    [!code-css[Main](working-with-groups/samples/sample3.css)]
- 指定群組中所有已連線的用戶端，**但指定的用戶端除外，但**由連接識別碼識別。

    [!code-csharp[Main](working-with-groups/samples/sample4.cs)]
- 指定群組中的所有已連線用戶端 **（呼叫用戶端除外**）。

    [!code-css[Main](working-with-groups/samples/sample5.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a>在資料庫中儲存群組成員資格

下列範例示範如何在資料庫中保留群組和使用者資訊。 您可以使用任何資料存取技術;不過，下列範例顯示如何使用 Entity Framework 定義模型。 這些實體模型會對應到資料庫資料表和欄位。 視應用程式的需求而定，您的資料結構可能會有很大的差異。 這個範例包含名為 `ConversationRoom` 的類別，這對應用程式而言是唯一的，可讓使用者加入有關不同主題（例如運動或園藝）的交談。 此範例也包含連接的類別。 不一定需要連接類別來追蹤群組成員資格，但通常是追蹤使用者的健全解決方案的一部分。

[!code-csharp[Main](working-with-groups/samples/sample6.cs)]

然後，在中樞內，您可以從資料庫中取出群組和使用者資訊，並手動將使用者新增至適當的群組。 此範例不包含用於追蹤使用者連接的程式碼。 在此範例中，`await` 關鍵字不會在 `Groups.Add` 之前套用，因為訊息不會立即傳送給群組的成員。 如果您想要在加入新成員之後立即傳送訊息給群組的所有成員，您會想要套用 `await` 關鍵字，以確保非同步作業已完成。

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a>在 Azure 資料表儲存體中儲存群組成員資格

使用 Azure 資料表儲存體來儲存群組和使用者資訊與使用資料庫類似。 下列範例顯示的資料表實體會儲存使用者名稱和組名。

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

在中樞中，您會在使用者連接時，抓取指派的群組。

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a>重新連接時驗證群組成員資格

根據預設，SignalR 會在中斷連線時，自動將使用者重新指派給適當的群組，例如在連接逾時之前卸載並重新建立連接。重新連接時，會在權杖中傳遞使用者的群組資訊，而且該權杖會在伺服器上進行驗證。 如需重新加入使用者對群組之驗證程式的相關資訊，請參閱重新[連接時重新加入群組](../security/introduction-to-security.md#rejoingroup)。

一般而言，您應該在重新連線時使用自動重新加入群組的預設行為。 SignalR 群組不是用於限制敏感性資料存取的安全性機制。 不過，如果您的應用程式必須在重新連接時再次檢查使用者的群組成員資格，您可以覆寫預設行為。 變更預設行為可能會增加資料庫的負擔，因為必須針對每個重新連線抓取使用者的群組成員資格，而不是只有在使用者連線時才進行。

如果您必須在重新連接時驗證群組成員資格，請建立新的中樞管線模組，以傳回指派群組的清單，如下所示。

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

然後，將該模組新增至中樞管線，如下所示。

[!code-csharp[Main](working-with-groups/samples/sample11.cs?highlight=4)]
