---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling
title: 暫時性錯誤處理（使用 Azure 建立真實世界的雲端應用程式） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 電子書建立真實世界的雲端應用程式，是以 Scott Guthrie 所開發的簡報為基礎。 它會說明13個模式和實務，
ms.author: riande
ms.date: 11/03/2015
ms.assetid: 7ead83bc-c08c-4b26-8617-00e07292e35c
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling
msc.type: authoredcontent
ms.openlocfilehash: fc281e3d8f7c9edd4d98b029a67e58113132a8b3
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74583649"
---
# <a name="transient-fault-handling-building-real-world-cloud-apps-with-azure"></a>暫時性錯誤處理（使用 Azure 建立真實世界的雲端應用程式）

由[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom 作者: dykstra](https://github.com/tdykstra)

[下載 Fix It 專案](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下載電子書](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 電子書建立真實世界的雲端應用程式**，是以 Scott Guthrie 所開發的簡報為基礎。 其中說明13種模式和作法，可協助您成功開發雲端 web 應用程式。 如需電子書的相關資訊，請參閱[第一章](introduction.md)。

當您設計真實世界的雲端應用程式時，您必須考慮的其中一件事就是如何處理暫時性的服務中斷。 此問題在雲端應用程式中是唯一重要的，因為您會相依于網路連線和外部服務。 您經常會遇到很難自我修復的問題，而且如果您未準備好以智慧方式處理它們，就會導致客戶不佳的體驗。

## <a name="causes-of-transient-failures"></a>暫時性失敗的原因

在雲端環境中，您會發現失敗和卸載的資料庫連接會定期發生。 這是因為相較于您的 web 伺服器和資料庫伺服器具有直接實體連線的內部部署環境，您會經歷更多的負載平衡器。 此外，有時候當您相依于多租使用者服務時，您會看到服務的呼叫速度變慢或更久，因為其他使用服務的人經常遇到這種情況。 在其他情況下，您可能是經常遇到服務的使用者，而服務故意對您進行節流–拒絕連線–以防止您對其他服務租使用者造成負面影響。

## <a name="use-smart-retryback-off-logic-to-mitigate-the-effect-of-transient-failures"></a>使用智慧型重試/轉型邏輯來減輕暫時性失敗的影響

您可以辨識通常是暫時性的錯誤，並自動重試導致錯誤的作業，而不會擲回例外狀況，並將無法使用的或錯誤頁面顯示給客戶。 在大部分的情況下，作業會在第二次嘗試時成功，而且您會從錯誤中復原，而不需要客戶知道發生問題。

有數種方式可以執行智慧型重試邏輯。

- Microsoft 模式 &amp; 實務群組具有[暫時性錯誤處理應用程式區塊](https://msdn.microsoft.com/library/dn440719(v=pandp.60).aspx)，如果您使用 ADO.NET 進行 SQL Database 存取（而不是透過 Entity Framework），就會為您執行所有工作。 您只需要設定重試的原則–重試查詢或命令的次數，以及嘗試之間等待的時間長度，然後將您的 SQL 程式碼包裝在*using*區塊中。

    [!code-csharp[Main](transient-fault-handling/samples/sample1.cs)]

    TFH 也支援[Azure 角色中](https://msdn.microsoft.com/library/windowsazure/dn386103.aspx)快取和[服務匯流排](https://azure.microsoft.com/services/service-bus/)。
- 當您使用 Entity Framework 通常不會直接使用 SQL 連線，因此您不能使用此模式和實務封裝，但 Entity Framework 6 會將這類的重試邏輯立即建立在架構中。 以您指定重試策略的類似方式，然後 EF 會在存取資料庫時使用該策略。

    若要在修正 It 應用程式中使用這項功能，我們只需要新增一個衍生自*DbConfiguration*的類別，然後開啟重試邏輯。

    [!code-csharp[Main](transient-fault-handling/samples/sample2.cs)]

    針對架構識別為一般暫時性錯誤的 SQL Database 例外狀況，顯示的程式碼會指示 EF 將作業重試最多3次，並在重試之間加上指數輪詢延遲，並將延遲上限設為5秒。 指數退避表示在每次失敗後重試之後，它會等候較長的時間，然後再試一次。 如果資料列中有三個嘗試失敗，則會擲回例外狀況。 下一節有關斷路器的說明為何您需要指數輪詢和有限的重試次數。

    當您使用 Azure 儲存體服務時，可能會有類似的問題，因為 Fix It 應用程式適用于 Blob，而 .NET 儲存體用戶端 API 已經實作用相同類型的邏輯。 您只需指定重試原則，如果您對預設設定感到滿意，就不需要這麼做。

<a id="circuitbreakers"></a>
## <a name="circuit-breakers"></a>斷路器

有幾個原因會導致您不想要在一段時間內重試太多次：

- 太多使用者持續重試失敗的要求，可能會降低其他使用者的體驗。 如果有數百萬人進行重複的重試要求，您可能會佔用 IIS 分派佇列，並防止您的應用程式服務要求，否則可能會成功處理。
- 如果每個人都因服務失敗而重試，可能會有許多要求排入佇列中，而服務會在開始復原時收到溢位。
- 如果錯誤是因為節流而造成，而且有一段時間會讓服務用於節流，則繼續重試可能會將該視窗移出，並導致節流繼續進行。
- 您可能有等待網頁呈現的使用者。 讓人們的等候時間太長可能會更麻煩，因為這種情況很快就會通知他們稍後再試一次。

指數退避會藉由限制服務可從您的應用程式取得的重試頻率，來解決其中一些問題。 但您也需要有*斷路*器：這表示在特定的重試臨界值中，您的應用程式會停止重試，並採取其他動作，例如下列其中一項：

- 自訂回退。 如果您無法從路透社取得股票價格，或許可以從 Bloomberg 取得。或者，如果您無法從資料庫取得資料，或許您可以從快取取得資料。
- 失敗無訊息。 如果您的應用程式所需的服務不是全部，或不是任何內容，則當您無法取得資料時，只會傳回 null。 如果您要顯示 [修正 It] 工作，而且 Blob 服務沒有回應，您可以顯示不含影像的工作詳細資料。
- 快速失敗。 錯誤使用者，以避免因為重試要求而導致服務中斷，這可能會造成其他使用者的服務中斷或擴充節流時段。 您可以顯示易記的「稍後再試一次」訊息。

沒有任何大小合適的重試原則。 您可以重試多次，並在非同步背景工作進程中等候較長的時間，而不是在使用者等待回應的同步 web 應用程式中。 您可以在關係資料庫服務的重試之間等候較長的時間，而不是快取服務。 以下是一些建議的重試原則範例，讓您瞭解數位可能有所不同的方式。 （「第一次快速」表示第一次重試之前不會延遲。

![範例重試原則](transient-fault-handling/_static/image1.png)

如 SQL Database 重試原則指引，請參閱針對[暫時性錯誤和連接錯誤進行疑難排解，以 SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-connectivity-issues/)。

## <a name="summary"></a>總結

重試/退轉關閉策略可以協助客戶在最短時間內看不到暫時性錯誤，而 Microsoft 提供的架構可讓您在使用 ADO.NET、Entity Framework 或 Azure 儲存體服務時，將執行策略的工作降至最低。

在[下一章](distributed-caching.md)中，我們將探討如何使用分散式快取來改善效能和可靠性。

## <a name="resources"></a>資源

如需詳細資訊，請參閱下列資源：

Documentation

- [Azure 上大規模服務設計的最佳作法雲端服務](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 以標記 Simm 和 Michael Thomassy 的技術白皮書。 類似于防故障的系列，並深入探討如何詳細說明。 請參閱遙測和診斷一節。
- [損毀修復：具有恢復功能的雲端架構指引](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx)。 白皮書： Marc Mercuri、Ulrich Homann 和 Andrew Townhill。 網頁版的防安全影片系列。
- [Microsoft 模式和實務-Azure 指引](https://msdn.microsoft.com/library/dn568099.aspx)。 請參閱重試模式、排程器代理程式監督員模式。
- [Azure SQL Database 中的容錯功能](https://blogs.msdn.com/b/windowsazure/archive/2012/07/30/fault-tolerance-in-windows-azure-sql-database.aspx)。 Tony Petrossian 的 Blog 文章。
- [Entity Framework-連接恢復/重試邏輯](https://msdn.microsoft.com/data/dn456835)。 如何使用和自訂 Entity Framework 6 的暫時性錯誤處理功能。
- [在 ASP.NET MVC 應用程式中使用 Entity Framework 的連接恢復功能和命令攔截](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)。 第四個在9部分的教學課程系列中，示範如何設定 SQL Database 的 EF 6 連接恢復功能。

Videos

- [防安全功能：建立可擴充、可復原的雲端服務](https://channel9.msdn.com/Series/FailSafe)。 Ulrich Homann、Marc Mercuri 和 Mark Simm 的九部分系列。 以非常容易存取且有趣的方式呈現高階概念和架構原則，並提供 Microsoft 客戶諮詢小組（CAT）體驗與實際客戶的故事。 從40:55 開始，請參閱第3集的斷路器討論。
- [打造 Big：從 Azure 客戶學到的經驗-第二部](https://channel9.msdn.com/Events/Build/2012/3-030)。 Mark Simm 討論如何設計失敗、暫時性錯誤處理和檢測所有專案。

程式碼範例

- [Azure 中的雲端服務基本](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)概念。 Microsoft Azure 客戶諮詢小組所建立的範例應用程式，示範如何使用[企業程式庫暫時性錯誤處理區塊](http://nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)（TFH）。 如需詳細資訊，請參閱[雲端服務基礎資料存取層–暫時性錯誤處理](https://social.technet.microsoft.com/wiki/contents/articles/18665.cloud-service-fundamentals-data-access-layer-transient-fault-handling.aspx)。 建議使用 TFH （不使用 Entity Framework）直接進行資料庫存取。

> [!div class="step-by-step"]
> [上一頁](monitoring-and-telemetry.md)
> [下一頁](distributed-caching.md)
