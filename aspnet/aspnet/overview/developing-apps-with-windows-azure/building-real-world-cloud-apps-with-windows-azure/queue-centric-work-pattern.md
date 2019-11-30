---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern
title: 以佇列為中心的工作模式（使用 Azure 建立真實世界的雲端應用程式） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 電子書建立真實世界的雲端應用程式，是以 Scott Guthrie 所開發的簡報為基礎。 它會說明13個模式和實務，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: cc1ad51b-40c3-4c68-8620-9aaa0fd1f6cf
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern
msc.type: authoredcontent
ms.openlocfilehash: c73b070f11366e781bcea70ffc84fd49a47d469a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74582754"
---
# <a name="queue-centric-work-pattern-building-real-world-cloud-apps-with-azure"></a>以佇列為中心的工作模式（使用 Azure 建立真實世界的雲端應用程式）

由[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom 作者: dykstra](https://github.com/tdykstra)

[下載 Fix It 專案](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下載電子書](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 電子書建立真實世界的雲端應用程式**，是以 Scott Guthrie 所開發的簡報為基礎。 其中說明13種模式和作法，可協助您成功開發雲端 web 應用程式。 如需電子書的相關資訊，請參閱[第一章](introduction.md)。

稍早，我們看到使用多個服務可能會產生「複合」 SLA，其中應用程式的有效 SLA 是個別 Sla 的*產品*。 例如，Fix It 應用程式會使用網站、儲存體和 SQL Database。 如果其中任何一項服務失敗，應用程式將會對使用者傳回錯誤。

快取是處理唯讀內容的暫時性失敗的好方法。 但如果您的應用程式需要執行工作，該怎麼辦？ 例如，當使用者提交新的 [修正 It] 工作時，應用程式就不能只是將工作放入快取中。 應用程式必須將 Fix It 工作寫入持續性資料存放區，才能進行處理。

這就是以佇列為中心的工作模式。 此模式可讓 web 層和後端服務之間的鬆散結合。

以下是模式的運作方式。 當應用程式取得要求時，它會將工作專案放在佇列上，並立即傳迴響應。 接著，個別的後端程序會將工作項目從佇列拉出並執行工作。

以佇列為中心的工作模式適用于：

- 耗費時間的工作（高延遲）。
- 需要外部服務的工作，可能永遠無法使用。
- 需要大量資源的工作（高 CPU）。
- 可受益于比率調節的工作（受限於突然的負載高載）。

## <a name="reduced-latency"></a>降低延遲

當您執行耗時的工作時，佇列會很有用。 如果工作需要幾秒鐘或更久的時間，而不是封鎖終端使用者，請將工作專案放入佇列中。 告訴使用者「我們正在處理它」，然後使用佇列接聽程式在背景中處理工作。

例如，當您在線上零售商購買某個專案時，網站會立即確認您的訂單。 但這並不表示您的東西已經在交付卡車中。 他們會在佇列中放入一項工作，而在背景中，他們會進行信用檢查、準備要運送的專案等等。

對於延遲較短的案例，端對端時間總計可能會比使用佇列更長，相較于同步執行工作。 但是就算如此，其他優點也可能超過該缺點。

## <a name="increased-reliability"></a>提高可靠性

在修正此問題的版本中，web 前端會與 SQL Database 後端緊密結合在一起。 如果 SQL database 服務無法使用，使用者會收到錯誤。 如果重試無效（也就是失敗不是暫時性），您唯一可以做的就是顯示錯誤，並要求使用者稍後再試一次。

![顯示 SQL Database 後端失敗時的 web 前端失敗的圖表](queue-centric-work-pattern/_static/image1.png)

使用佇列，當使用者提交 Fix It 工作時，應用程式會將訊息寫入佇列。 訊息承載是工作的[JSON](http://json.org/)標記法。 一旦訊息寫入佇列，應用程式就會傳回，並立即向使用者顯示成功訊息。

如果任何後端服務（例如 SQL database 或佇列接聽程式）離線，使用者仍然可以提交新的 Fix It 工作。 訊息只會排入佇列，直到後端服務再次可用為止。 此時，後端服務會趕上待處理專案。

![顯示 web 前端在發生 SQL Database 錯誤時繼續運作的圖表](queue-centric-work-pattern/_static/image2.png)

此外，您現在可以新增更多後端邏輯，而不需擔心前端的復原。 例如，您可能會想要在每次指派新的修正程式時，傳送電子郵件或 SMS 訊息給擁有者。 如果電子郵件或 SMS 服務變得無法使用，您可以處理其他所有專案，然後將訊息放入不同的佇列，以便傳送電子郵件/SMS 訊息。

在過去，我們的有效 SLA 已 Web Apps &times; 儲存體 &times; SQL Database = 99.7%。 （請參閱[設計到存活的失敗](design-to-survive-failures.md)）。

當我們將應用程式變更為使用佇列時，web 前端只會相依于 Web Apps 和儲存體，以取得99.8% 的複合 SLA。 （請注意，佇列是 Azure 儲存體服務的一部分，因此包含在與 blob 儲存體相同的 SLA 中）。

如果您的需求高於99.8%，您可以在兩個不同的區域中建立兩個佇列。 指定一個做為主要，另一個做為次要。 在您的應用程式中，如果主要佇列無法使用，則故障切換至次要佇列。 同時無法使用的機會很小。

## <a name="rate-leveling-and-independent-scaling"></a>比率調節和獨立調整

佇列也適用于所謂的*速率調節*或*負載調節*。

Web 應用程式通常會受到流量突然激增的影響。 雖然您可以使用自動調整來自動新增網頁伺服器，以處理增加的網路流量，但自動調整可能無法快速回應，以處理負載突然尖峰的情況。 如果 web 伺服器可以藉由將訊息寫入佇列來卸載他們必須執行的工作，則可以處理更多的流量。 後端服務可以從佇列讀取訊息並加以處理。 佇列的深度會隨著傳入負載的變化而成長或縮小。

由於許多耗時的工作都已登出後端服務，因此 web 層可以更輕鬆地回應流量突然激增的情況。 而且您可以節省成本，因為有任何特定數量的流量可由較少的 web 伺服器處理。

您可以獨立調整 web 層和後端服務。 例如，您可能需要三部 web 伺服器，但只能有一個伺服器處理佇列訊息。 或者，如果您在背景執行大量運算工作，可能需要更多的後端伺服器。

![](queue-centric-work-pattern/_static/image3.png)

自動調整適用于後端服務以及 web 層。 根據後端 Vm 的 CPU 使用量，您可以相應增加或相應減少正在佇列中處理工作的 Vm 數目。 或者，您可以根據佇列中的專案數自動調整。 例如，您可以指示自動調整以嘗試在佇列中保留10個以上的專案。 如果佇列有10個以上的專案，自動調整將會新增 Vm。 當他們趕上時，自動調整將會卸載額外的 Vm。

## <a name="adding-queues-to-the-fix-it-application"></a>將佇列新增至修正 It 應用程式

若要執行佇列模式，我們必須對 Fix It 應用程式進行兩個變更。

- 當使用者提交新的 Fix It 工作時，請將工作放在佇列中，而不是將它寫入資料庫中。
- 建立後端服務，以處理佇列中的訊息。

對於佇列，我們將使用[Azure 佇列儲存體服務](https://www.windowsazure.com/develop/net/how-to-guides/queue-service/)。 另一個選項是使用[Azure 服務匯流排](https://docs.microsoft.com/azure/service-bus/)。

若要決定要使用哪個佇列服務，請考慮您的應用程式需要在佇列中傳送和接收訊息的方式：

- 如果您有合作的生產者和競爭取用者，請考慮使用 Azure 佇列儲存體服務。 「合作的產生者」表示多個進程正在將訊息新增至佇列。 「競爭取用者」表示多個進程會從佇列中提取訊息來處理它們，但是任何指定的訊息只能由一個「取用者」處理。 如果您需要的輸送量比單一佇列所能取得的更多，請使用額外的佇列和/或其他儲存體帳戶。
- 如果您需要[發行/訂閱模型](http://en.wikipedia.org/wiki/Publish/subscribe)，請考慮使用 Azure 服務匯流排的佇列。

修正 It 應用程式會符合合作的產生者和競爭取用者模型。

另一個考慮是應用程式可用性。 佇列儲存體服務是我們用於 blob 儲存體之相同服務的一部分，因此使用它不會影響我們的 SLA。 Azure 服務匯流排是個別的服務，具有自己的 SLA。 如果我們使用服務匯流排的佇列，我們必須考慮額外的 SLA 百分比，而我們的複合 SLA 會較低。 當您選擇佇列服務時，請確定您瞭解您對應用程式可用性所做的影響。 如需詳細資訊，請參閱[Resources](#resources)一節。

## <a name="creating-queue-messages"></a>建立佇列訊息

若要在佇列上放置 Fix It 工作，web 前端會執行下列步驟：

1. 建立[CloudQueueClient](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueueclient.aspx)實例。 `CloudQueueClient` 實例是用來對佇列服務執行要求。
2. 建立佇列（如果尚不存在）。
3. 序列化 Fix It 工作。
4. 呼叫[CloudQueue. AddMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.addmessageasync.aspx) ，將訊息放入佇列。

我們將在新 `FixItQueueManager` 類別的函式和 `SendMessageAsync` 方法中執行這項工作。

[!code-csharp[Main](queue-centric-work-pattern/samples/sample1.cs?highlight=11-12,16,18-25)]

在這裡，我們會使用[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)程式庫，將 fixit 序列化為 Json 格式。 您可以使用您偏好的任何序列化方法。 JSON 的優點是人們可讀取，而比 XML 較不詳細。

生產品質的程式碼會新增錯誤處理邏輯、在資料庫變得無法使用時暫停、更明確地處理復原、在應用程式啟動時建立佇列，以及管理「[有害」訊息](https://msdn.microsoft.com/library/ms789028(v=vs.110).aspx)。 （有害訊息是因為某些原因而無法處理的訊息。 您不希望有害訊息位於佇列中，背景工作角色會持續嘗試處理、失敗、再試一次、失敗等等）。

在前端 MVC 應用程式中，我們需要更新建立新工作的程式碼。 請不要將工作放入存放庫中，而是呼叫如上所示的 `SendMessageAsync` 方法。

[!code-csharp[Main](queue-centric-work-pattern/samples/sample2.cs?highlight=10)]

## <a name="processing-queue-messages"></a>處理佇列訊息

為了處理佇列中的訊息，我們將建立後端服務。 後端服務將會執行無限迴圈，以執行下列步驟：

1. 取得佇列中的下一個訊息。
2. 將訊息還原序列化為 Fix It 工作。
3. 將 [修正 It] 工作寫入資料庫。

為了裝載後端服務，我們將建立包含背景*工作角色*的 Azure 雲端服務。 背景工作角色是由一或多個可執行後端處理的 Vm 所組成。 在這些 Vm 中執行的程式碼會在佇列可供使用時，從佇列中提取訊息。 針對每個訊息，我們會將 JSON 承載還原序列化，並使用我們稍早在 web 層中使用的相同存放庫，將 Fix It 工作實體的實例寫入資料庫。

下列步驟示範如何將背景工作角色專案新增至具有標準 Web 專案的方案。 這些步驟已在您可以下載的修正 It 專案中完成。

首先，將雲端服務專案新增至 Visual Studio 解決方案。 以滑鼠右鍵按一下方案，然後依序選取 [**加入**] 和 [**新增專案**]。 在左窗格中，展開 **[ C#視覺效果**]，然後選取 [**雲端**]。

[![](queue-centric-work-pattern/_static/image5.png)](queue-centric-work-pattern/_static/image4.png)

在 [**新增 Azure 雲端服務**] 對話方塊中，展開左窗格上的 [**視覺效果C#**  ] 節點。 選取 [背景**工作角色**]，然後按一下向右箭號圖示。

![](queue-centric-work-pattern/_static/image6.png)

（請注意，您也可以新增*web 角色*。 我們可以在同一個雲端服務中的前端進行修正，而不是在 Azure 網站中執行。 這對於在前端和後端之間進行連線的優勢更容易協調。 不過，為了簡化此示範，我們會將前端保留在 Azure App Service Web 應用程式中，並只在雲端服務中執行後端。）

預設名稱會指派給背景工作角色。 若要變更名稱，請將滑鼠游標移至右窗格中的背景工作角色上方，然後按一下鉛筆圖示。

![](queue-centric-work-pattern/_static/image7.png)

按一下 **[確定**] 以完成對話方塊。 這會將兩個專案新增至 Visual Studio 解決方案。

- 定義雲端服務的 Azure 專案，包括設定資訊。
- 定義背景工作角色的背景工作角色專案。

![](queue-centric-work-pattern/_static/image8.png)

如需詳細資訊，請參閱[使用 Visual Studio 建立 Azure 專案。](https://msdn.microsoft.com/library/windowsazure/ee405487.aspx)

在背景工作角色中，我們會藉由呼叫我們稍早所見 `FixItQueueManager` 類別的 `ProcessMessageAsync` 方法來輪詢訊息。

[!code-csharp[Main](queue-centric-work-pattern/samples/sample3.cs?highlight=25)]

`ProcessMessagesAsync` 方法會檢查是否有訊息正在等待。 如果有的話，它會將訊息還原序列化為 `FixItTask` 的實體，並將實體儲存在資料庫中。 它會迴圈，直到佇列是空的為止。

[!code-csharp[Main](queue-centric-work-pattern/samples/sample4.cs)]

輪詢佇列訊息會產生較小的交易費用，因此，當沒有訊息等候處理時，背景工作角色的 `RunAsync` 方法會等待一秒，再呼叫 `Task.Delay(1000)`再次輪詢。

在 Web 專案中，新增非同步程式碼可以自動改善效能，因為 IIS 會管理有限的執行緒集區。 背景工作角色專案中不會發生這種情況。 若要改善背景工作角色的擴充性，您可以撰寫多執行緒程式碼，或使用非同步程式碼來執行[平行程式設計](https://msdn.microsoft.com/library/ff963553.aspx)。 此範例不會執行平行程式設計，但會示範如何讓程式碼非同步，讓您可以執行平行程式設計。

## <a name="summary"></a>總結

在本章中，您已瞭解如何藉由執行以佇列為中心的工作模式來改善應用程式回應性、可靠性和擴充性。

這是本電子書中涵蓋的13種模式的最後一項，但當然還有許多其他模式和作法可協助您建立成功的雲端應用程式。 [最後一章](more-patterns-and-guidance.md)提供尚未在這13種模式中涵蓋之主題的資源連結。

<a id="resources"></a>
## <a name="resources"></a>資源

如需佇列的詳細資訊，請參閱下列資源。

文件：

- [Microsoft Azure 儲存體佇列第1部分：消費者入門](https://www.red-gate.com/simple-talk/cloud/platform-as-a-service/microsoft-azure-storage-queues-part-1-getting-started/)。 依羅馬字 Schacherl 的文章。
- [執行背景](https://msdn.microsoft.com/library/ff803365.aspx)工作，從 Microsoft 的模式和實務[將應用程式移至雲端的第](https://msdn.microsoft.com/library/ff728592.aspx)5 章。 （尤其是「[使用 Azure 儲存體的佇列](https://msdn.microsoft.com/library/ff803365.aspx#sec7)」一節）。
- [Azure 上以佇列為基礎的訊息解決方案最大化擴充性和成本效益的最佳作法](https://msdn.microsoft.com/library/windowsazure/hh697709.aspx)。 白皮書： Valery Mizonov。
- [比較 Azure 佇列和服務匯流排佇列](https://msdn.microsoft.com/magazine/jj159884.aspx)。 MSDN 雜誌文章提供其他資訊，可協助您選擇要使用的佇列服務。 本文提及服務匯流排相依于用於驗證的 ACS，這表示當 ACS 無法使用時，您的 SB 佇列將無法使用。 不過，由於文章已撰寫，因此 SB 已變更為可讓您使用[SAS 權杖](https://msdn.microsoft.com/library/windowsazure/dn170477.aspx)作為 ACS 的替代方案。
- [Microsoft 模式和實務-Azure 指引](https://msdn.microsoft.com/library/dn568099.aspx)。 請參閱非同步訊息入門、管道和篩選模式、補償交易模式、競爭取用者模式、CQRS 模式。
- [CQRS 旅程](https://msdn.microsoft.com/library/jj554200)。 電子書，依據 Microsoft 的模式與實務來介紹 CQRS。

影片：

- [防安全功能：建立可擴充、可復原的雲端服務](https://channel9.msdn.com/Series/FailSafe)。 Ulrich Homann、Marc Mercuri 和 Mark Simm 的九個部分影片系列。 以非常容易存取且有趣的方式呈現高階概念和架構原則，並提供 Microsoft 客戶諮詢小組（CAT）體驗與實際客戶的故事。 如需 Azure 儲存體服務和佇列的簡介，請參閱第5集，從35:13 開始。

> [!div class="step-by-step"]
> [上一頁](distributed-caching.md)
> [下一頁](more-patterns-and-guidance.md)
