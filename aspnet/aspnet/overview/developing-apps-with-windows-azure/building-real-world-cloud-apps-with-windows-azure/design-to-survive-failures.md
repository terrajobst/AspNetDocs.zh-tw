---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/design-to-survive-failures
title: 設計到存活的失敗（使用 Azure 建立真實世界的雲端應用程式） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 電子書建立真實世界的雲端應用程式，是以 Scott Guthrie 所開發的簡報為基礎。 它會說明13個模式和實務，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 364ce84e-5af8-4e08-afc9-75a512b01f84
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/design-to-survive-failures
msc.type: authoredcontent
ms.openlocfilehash: 9bf9acb8b4f8521d03c053c124c5fc4a07d6cb9a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74585658"
---
# <a name="design-to-survive-failures-building-real-world-cloud-apps-with-azure"></a>設計到存活的失敗（使用 Azure 建立真實世界的雲端應用程式）

由[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom 作者: dykstra](https://github.com/tdykstra)

[下載 Fix It 專案](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下載電子書](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 電子書建立真實世界的雲端應用程式**，是以 Scott Guthrie 所開發的簡報為基礎。 其中說明13種模式和作法，可協助您成功開發雲端 web 應用程式。 如需電子書的相關資訊，請參閱[第一章](introduction.md)。

當您建立任何類型的應用程式時，必須考慮的其中一件事，特別是在雲端中執行時，有很多人將會用到它，這是如何設計應用程式，讓它能夠正常地處理失敗，並繼續傳遞最多的價值的話. 有足夠的時間，任何環境或任何軟體系統中的事情都會發生錯誤。 您的應用程式如何處理這些情況，會決定您的客戶將會如何取得，以及花多少時間來分析和修正問題。

## <a name="types-of-failures"></a>失敗的類型

您會想要以不同的方式處理失敗的兩個基本類別：

- 暫時性、自我修復的失敗，例如間歇性的網路連線問題。
- 持續需要介入的失敗。

針對暫時性失敗，您可以執行重試原則，以確保應用程式在大部分的時間都能快速且自動復原。 您的客戶可能會注意到稍長的回應時間，否則不會受到影響。 在[暫時性錯誤處理一章](transient-fault-handling.md)中，我們將示範一些方法來處理這些錯誤。

針對持續失敗，您可以執行監視和記錄功能，以便在發生問題時立即通知您，並協助進行根本原因分析。 我們將示範一些方法，協助您在[監視和遙測一章](monitoring-and-telemetry.md)中隨時掌握這類錯誤。

## <a name="failure-scope"></a>失敗範圍

您也必須考慮失敗範圍–單一電腦是否受到影響、整個服務（例如 SQL Database 或儲存體）或整個區域。

![失敗範圍](design-to-survive-failures/_static/image1.png)

### <a name="machine-failures"></a>電腦失敗

在 Azure 中，失敗的伺服器會自動取代為新的，而設計良好的雲端應用程式會自動且快速地從這類失敗中復原。 稍早，我們將無狀態 web 層的擴充性優勢提高，而從故障伺服器復原的便利性則是 statelessness 的另一個優點。 輕鬆復原也是平臺即服務（PaaS）功能的優點之一，例如 SQL Database 和 Azure App Service Web Apps。 硬體失敗很罕見，但當它們發生時，這些服務會自動處理它們;當您使用其中一項服務時，甚至不需要撰寫程式碼來處理電腦失敗。

### <a name="service-failures"></a>服務失敗

雲端應用程式通常會使用多個服務。 例如，Fix It 應用程式會使用 SQL Database 服務、儲存體服務，以及 web 應用程式部署至 Azure App Service。 如果您依賴的其中一個服務失敗，您的應用程式會執行什麼動作？ 對於某些服務失敗而言，「抱歉，稍後再試一次」訊息可能是您的最佳做法。 但是在許多情況下，您可以做得更好。 例如，當您的後端資料存放區關閉時，您可以接受使用者輸入、顯示「已收到您的要求」，並暫時將輸入儲存在其他地方;然後，當您需要的服務再次運作時，您可以取出輸入並加以處理。

以[佇列為中心的工作模式](queue-centric-work-pattern.md)一章會顯示處理這種情況的一種方式。 Fix It 應用程式會將工作儲存在 SQL Database 中，但 SQL Database 關閉時則不需要結束。 在該章節中，我們將瞭解如何在佇列中儲存工作的使用者輸入，並使用背景工作進程來讀取佇列和更新工作。 如果 SQL 已關閉，建立 Fix It 工作的能力不會受到影響;當有 SQL Database 可用時，工作者進程可以等候並處理新的工作。

### <a name="region-failures"></a>區域失敗

整個區域可能會失敗。 自然的嚴重損壞可能會損毀資料中心，它可能會由 meteor 壓平合併，而 farmer burying 可以剪下骨幹等。如果您的應用程式裝載在 stricken 資料中心，您該怎麼做？ 您可以在 Azure 中將應用程式設定為同時在多個區域中執行，如此一來，如果其中一項發生嚴重損壞，您就可以繼續在另一個區域中執行。 這類失敗非常罕見，而且大部分的應用程式都不會跳過輕鬆所需的動作，以確保不會因為這種排序而中斷服務。 請參閱章節結尾的 Resources 一節，以瞭解如何讓您的應用程式即使在區域失敗時仍可供使用的資訊。

Azure 的目標是要讓您更輕鬆地處理所有這些失敗類型，而您會看到一些範例，說明如何在下列章節中執行此作業。

## <a name="slas"></a>滿足

人們經常聽說雲端環境中的服務等級協定（Sla）。 基本上，這些都是公司對其服務的可靠程度所做出的承諾。 99.9% SLA 表示您應該預期服務會正常運作99.9% 的時間。 這是 SLA 的一般價值，而且聽起來像是非常高的值，但您可能不會發現0.1% 實際的金額是多少。 以下表格顯示在一年、一個月和一周內，各種 SLA 百分比的停機時間量。

![SLA 資料表](design-to-survive-failures/_static/image2.png)

因此99.9% 的 SLA 表示您的服務可能會在一年中關閉8.76 小時或每月43.2 分鐘。 這會比大部分人都知道的時間更低。 因此，身為開發人員，您想要注意一定的停機時間，並以正常方式處理它。 有時候，有人會使用您的應用程式，而服務將會關閉，而您想要將對客戶的負面影響降到最低。

有關 SLA 的一件事，就是它所指的是哪一個時間範圍：每週、每個月或每年都會重設時鐘？ 在 Azure 中，我們會每個月重設時鐘，這對您比每年 SLA 更好，因為每年 SLA 可能會以一系列良好的月份來抵銷，而隱藏了不好的月份。

當然，我們一定會渴望比 SLA 更好。通常您會減少很多的時間。 這是因為如果我們停機時間超過最長的停機時間，您可以向後要求金錢。 您所得到的金錢可能無法完全補償您的業務衝擊，但 SLA 的這個層面會作為強制原則，讓您知道我們確實會將它視為非常重要的事。

### <a name="composite-slas"></a>複合 Sla

當您查看 Sla 時，需要考慮的重要事項是在應用程式中使用多個服務的影響，每個服務都有個別的 SLA。 例如，Fix It 應用程式會使用 Azure App Service Web Apps、Azure 儲存體和 SQL Database。 以下是在2013年12月撰寫此電子書的日期時的 SLA 號碼：

![SLA 網站、儲存體、SQL Database](design-to-survive-failures/_static/image3.png)

根據這些服務 Sla，您預期應用程式的最大停機時間為何？ 您可能會認為您的停機時間等於最差的 SLA 百分比，或在此案例中為99.9%。 如果這三個服務總是同時失敗，但這不一定是實際發生的情況，這會是 true。 每個服務可能會在不同時間獨立失敗，因此您必須將個別 SLA 編號相乘來計算複合 SLA。

![複合 SLA](design-to-survive-failures/_static/image4.png)

因此，您的應用程式可能不只是每個月43.2 分鐘，而是每個月的3倍（108分鐘），而且仍在 Azure SLA 限制內。

此問題對 Azure 而言並不獨特。 我們實際上提供了任何可用雲端服務的最佳雲端 Sla，如果您使用任何廠商的雲端服務，就會有類似的問題需要處理。 重點在於思考如何設計應用程式以妥善處理不可避免的服務失敗的重要性，因為它們可能經常會對客戶或使用者造成影響。

### <a name="cloud-slas-compared-to-enterprise-down-time-experience"></a>與企業停機時間相較之下的雲端 Sla

大家有時候會說：「我的企業應用程式中沒有這些問題。」 如果您問到幾個月實際有多少時間，他們通常會說：「嗯，偶爾會發生這種情況。」 如果您詢問多久，他們承認「有時候我們需要備份或安裝新的伺服器或更新軟體。」 當然，這會計算為停機時間。 大部分的企業應用程式（除非它們特別是要徑任務）實際上會停機超過我們的服務 Sla 所允許的時間長度。 但是當您的伺服器和您的基礎結構，以及您對它的控制，您通常會覺得不大停機時間。 在雲端環境中，您會相依于其他人，而且您不知道發生什麼事，因此您可能會想要更擔心。

當企業達到比從雲端 SLA 取得更高的時間百分比時，就會藉由在硬體上花費更多錢來達成此目的。 雲端服務可以執行這項操作，但必須為其服務額外收取更多費用。 相反地，您會利用符合成本效益的服務，並設計您的軟體，讓不可避免的失敗造成客戶最少的中斷。 身為雲端應用程式設計人員的工作並不是為了避免失敗，而是為了避免發生災難，而是把焦點放在軟體上，而不是硬體上。 雖然企業應用程式致力於在失敗之間達到最大的平均時間，但雲端應用程式致力於將復原的平均時間降到最低。

### <a name="not-all-cloud-services-have-slas"></a>並非所有雲端服務都有 Sla

也請注意，並非每個雲端服務甚至都有 SLA。 如果您的應用程式相依于不具時間保證的服務，您可能會比想像更長的時間。 例如，如果您使用社交提供者（例如 Facebook 或 Twitter）來登入您的網站，請洽詢服務提供者以瞭解是否有 SLA，而且您可能會發現沒有任何一項。 但是，如果驗證服務停止運作，或無法支援您在它擲回的要求數量，您的客戶就會被鎖定您的應用程式。 您可以關閉數天或更久的時間。 一個新應用程式的建立者預期會有數百個數百萬次的下載，並相依于 Facebook 驗證，但是在上線之前不會與 Facebook 交談，而且該服務沒有 SLA。

### <a name="not-all-downtime-counts-toward-slas"></a>並非所有停機時間都計入 Sla

如果您的應用程式過度使用，某些雲端服務可能會刻意拒絕服務。 這稱為*節流*。 如果服務有 SLA，它應該會陳述您可能節流的條件，而您的應用程式設計應該避免這些狀況，並在發生時適當地回應節流。 例如，如果當您每秒超過某個數位時，服務的要求開始失敗，您會想要確保自動重試不會快速進行，因為它們會造成節流的繼續。 在[暫時性錯誤處理一章](transient-fault-handling.md)中，我們將會有更多關於節流的資訊。

## <a name="summary"></a>總結

本章已嘗試協助您瞭解如何將真實世界的雲端應用程式設計成可正常地存活失敗。 從[下一章](monitoring-and-telemetry.md)開始，此系列中的其餘模式會詳細說明一些您可以用來執行此動作的策略：

- 有良好的[監視和遙測](monitoring-and-telemetry.md)，讓您快速瞭解需要介入的失敗，而且您有足夠的資訊可以解決這些問題。
- 藉由執行智慧型重試邏輯來[處理暫時性錯誤](transient-fault-handling.md)，讓您的應用程式在可以時自動復原，並在無法時切換回[斷路](transient-fault-handling.md#circuitbreakers)器邏輯。
- 使用[分散式](distributed-caching.md)快取，以將資料庫存取的輸送量、延遲和連接問題降到最低。
- 透過以[佇列為中心的工作模式](queue-centric-work-pattern.md)來執行鬆散耦合，讓您的應用程式前端在後端關閉時仍可繼續運作。

## <a name="resources"></a>資源

如需詳細資訊，請參閱本電子書中的後續章節和下列資源。

文件：

- [損毀修復：具有恢復功能的雲端架構指引](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx)。 白皮書： Marc Mercuri、Ulrich Homann 和 Andrew Townhill。 網頁版的防安全影片系列。
- [Azure 上大規模服務設計的最佳作法雲端服務](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 以標記 Simm 和 Michael Thomassy 的技術白皮書。
- [Azure 業務持續性技術指引](https://msdn.microsoft.com/library/windowsazure/hh873027.aspx)。 Wickline 和 Jason Roth 的技術白皮書。
- [Azure 應用程式的嚴重損壞修復和高可用性](https://msdn.microsoft.com/library/windowsazure/dn251004.aspx)。 由 Michael McKeown、Hanu Kommalapati 和 Jason Roth 所白皮書。
- [Microsoft 模式和實務-Azure 指引](https://msdn.microsoft.com/library/dn568099.aspx)。 請參閱多個資料中心部署指導方針、斷路器模式。
- [Azure 支援-服務等級協定](https://azure.microsoft.com/support/legal/sla/)。
- [Azure SQL Database 中的業務持續性](https://msdn.microsoft.com/library/windowsazure/hh852669.aspx)。 SQL Database 高可用性和嚴重損壞修復功能的相關檔。
- [Azure 虛擬機器中 SQL Server 的高可用性和嚴重損壞修復](https://msdn.microsoft.com/library/windowsazure/jj870962.aspx)。

影片：

- [防安全功能：建立可擴充、可復原的雲端服務](https://channel9.msdn.com/Series/FailSafe)。 Ulrich Homann、Marc Mercuri 和 Mark Simm 的九部分系列。 以非常容易存取且有趣的方式呈現高階概念和架構原則，並提供 Microsoft 客戶諮詢小組（CAT）體驗與實際客戶的故事。 集1和8將深入探討設計雲端應用程式以存活失敗的原因。 另請參閱從49:57 開始的集區2中的節流追蹤討論。從56:05 開始，第2集的失敗點和失敗模式討論，以及從40:55 開始的第3集斷路器討論。
- [打造 Big：從 Azure 客戶學到的經驗-第二部](https://channel9.msdn.com/Events/Build/2012/3-030)。 Mark Simm 討論如何設計失敗和檢測所有專案。 類似于防故障的系列，並深入探討如何詳細說明。

> [!div class="step-by-step"]
> [上一頁](unstructured-blob-storage.md)
> [下一頁](monitoring-and-telemetry.md)
