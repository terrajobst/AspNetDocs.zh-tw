---
uid: signalr/overview/older-versions/mapping-users-to-connections
title: 將 SignalR 使用者對應至 SignalR 1.x 中的連接 |Microsoft Docs
author: bradygaster
description: 本主題說明如何保留使用者和其連線的相關資訊。
ms.author: bradyg
ms.date: 10/17/2013
ms.assetid: ebbc93a8-e6c4-4122-8e0d-3aa42293c747
msc.legacyurl: /signalr/overview/older-versions/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: 9d948495e9b8821fcb465611b6926603c3756a19
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558482"
---
# <a name="mapping-signalr-users-to-connections-in-signalr-1x"></a>將 SignalR 使用者對應至 SignalR 1.x 的連線

由一[Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本主題說明如何保留使用者和其連線的相關資訊。

## <a name="introduction"></a>簡介

連線至中樞的每個用戶端都會傳遞唯一的連線識別碼。您可以在中樞內容的 `Context.ConnectionId` 屬性中取得此值。 如果您的應用程式需要將使用者對應到連接識別碼並保存該對應，您可以使用下列其中一項：

- [記憶體內部儲存體](#inmemory)（例如字典）
- [每位使用者的 SignalR 群組](#groups)
- [永久的外部儲存體](#database)，例如資料庫資料表或 Azure 資料表儲存體

本主題會顯示每個這些實作為。 您可以使用 `Hub` 類別的 `OnConnected`、`OnDisconnected`和 `OnReconnected` 方法來追蹤使用者連接狀態。

應用程式的最佳做法取決於：

- 裝載應用程式的網頁伺服器數目。
- 您是否需要取得目前已連線使用者的清單。
- 當應用程式或伺服器重新開機時，是否需要保存群組和使用者資訊。
- 呼叫外部伺服器的延遲是否有問題。

下表顯示這些考慮適用的方法。

|  | 一部以上的伺服器 | 取得目前已連線使用者的清單 | 重新開機之後保存資訊 | 最佳效能 |
| --- | --- | --- | --- | --- |
| 記憶體中 |  | ![](mapping-users-to-connections/_static/image1.png) |  | ![](mapping-users-to-connections/_static/image2.png) |
| 單一使用者群組 | ![](mapping-users-to-connections/_static/image3.png) |  |  | ![](mapping-users-to-connections/_static/image4.png) |
| 永久、外部 | ![](mapping-users-to-connections/_static/image5.png) | ![](mapping-users-to-connections/_static/image6.png) | ![](mapping-users-to-connections/_static/image7.png) |  |

<a id="inmemory"></a>

## <a name="in-memory-storage"></a>記憶體內部儲存體

下列範例示範如何在儲存于記憶體中的字典中保留連接和使用者資訊。 字典會使用 `HashSet` 來儲存連接識別碼。任何時候，使用者都可以有一個以上的 SignalR 應用程式連接。 例如，透過多個裝置或多個瀏覽器索引標籤連線的使用者，會有一個以上的連接識別碼。

如果應用程式關閉，則會遺失所有資訊，但會在使用者重新建立其連接時重新填入。 如果您的環境包含一部以上的 web 伺服器，記憶體內部儲存體就無法運作，因為每部伺服器都有不同的連線集合。

第一個範例顯示的類別會管理使用者與連接的對應。 HashSet 的索引鍵將會是使用者的名稱。

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

下一個範例顯示如何使用中樞的連線對應類別。 類別的實例會儲存在 `_connections`的變數名稱中。

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a>單一使用者群組

您可以為每個使用者建立群組，然後在您只想要觸達該使用者時，傳送一則訊息給該群組。 每個群組的名稱都是使用者的名稱。 如果使用者有一個以上的連線，每個連線識別碼都會新增至使用者的群組。

當使用者中斷連線時，您不應該手動從群組中移除使用者。 SignalR 架構會自動執行此動作。

下列範例顯示如何執行單一使用者群組。

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a>永久的外部儲存體

本主題說明如何使用資料庫或 Azure 資料表儲存體來儲存連接資訊。 當您有多部網頁伺服器時，這個方法就可以運作，因為每個 web 伺服器都能與相同的資料存放庫互動。 如果您的 web 伺服器停止運作，或應用程式重新開機，則不會呼叫 `OnDisconnected` 方法。 因此，您的資料存放庫可能會有不再有效之連接識別碼的記錄。 若要清除這些孤立的記錄，您可能會想要讓在與您的應用程式相關的時間範圍以外建立的任何連接失效。 本節中的範例包含一個值，可在建立連接時進行追蹤，但不會顯示如何清除舊記錄，因為您可能會想要做為背景進程。

### <a name="database"></a>資料庫

下列範例示範如何在資料庫中保留連接和使用者資訊。 您可以使用任何資料存取技術;不過，下列範例顯示如何使用 Entity Framework 定義模型。 這些實體模型會對應到資料庫資料表和欄位。 視應用程式的需求而定，您的資料結構可能會有很大的差異。

第一個範例示範如何定義可以與許多連接實體相關聯的使用者實體。

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

然後，您可以從中樞使用如下所示的程式碼，追蹤每個連線的狀態。

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

### <a name="azure-table-storage"></a>Azure 表格儲存體

下列 Azure 資料表儲存體範例類似于資料庫範例。 它不包含開始使用 Azure 表格儲存體服務所需的所有資訊。 如需相關資訊，請參閱[如何使用 .net 的資料表儲存體](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)。

下列範例顯示用來儲存連接資訊的資料表實體。 它會依使用者名稱分割資料，並依連接識別碼來識別每個實體，讓使用者可以隨時擁有多個連接。

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

在中樞中，您可以追蹤每個使用者連接的狀態。

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]
