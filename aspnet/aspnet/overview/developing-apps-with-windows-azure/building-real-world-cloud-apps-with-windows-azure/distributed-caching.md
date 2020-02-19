---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
title: 分散式快取（使用 Azure 建立真實世界的雲端應用程式） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 電子書建立真實世界的雲端應用程式，是以 Scott Guthrie 所開發的簡報為基礎。 它會說明13個模式和實務，
ms.author: riande
ms.date: 07/20/2015
ms.assetid: 406518e9-3817-49ce-8b90-e82bc461e2c0
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
msc.type: authoredcontent
ms.openlocfilehash: 87a7516415895e761d1589fd459b93e5c15c0f85
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456994"
---
# <a name="distributed-caching-building-real-world-cloud-apps-with-azure"></a>分散式快取（使用 Azure 建立真實世界的雲端應用程式）

由[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom 作者: dykstra](https://github.com/tdykstra)

[下載 Fix It 專案](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下載電子書](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 電子書建立真實世界的雲端應用程式**，是以 Scott Guthrie 所開發的簡報為基礎。 其中說明13種模式和作法，可協助您成功開發雲端 web 應用程式。 如需電子書的相關資訊，請參閱[第一章](introduction.md)。

上一章探討了暫時性錯誤處理，並將快取視為斷路器策略。 本章提供快取的更多背景，包括何時使用它、使用它的常見模式，以及如何在 Azure 中執行。

## <a name="what-is-distributed-caching"></a>什麼是分散式快取

快取會藉由將資料儲存在記憶體中，提供常存取之應用程式資料的高輸送量、低延遲存取。 針對雲端應用程式，最有用的快取類型為分散式快取，這表示資料不會儲存在個別的 web 伺服器記憶體中，而是在其他雲端資源上，而且快取的資料會提供給所有應用程式的 web 伺服器（或 ar 的其他雲端 Vm）使用e 由應用程式使用）。

![此圖顯示存取相同快取伺服器的多部 web 伺服器](distributed-caching/_static/image1.png)

當應用程式藉由新增或移除伺服器進行調整時，或由於升級或錯誤而取代伺服器時，所有執行應用程式的伺服器都可以存取快取的資料。

藉由避免持續性資料存放區的高延遲資料存取，快取可大幅提升應用程式的回應能力。 例如，從快取中抓取資料的速度，比從關係資料庫中抓取資料更快。

快取的一項優點是減少對持續性資料存放區的流量，而當持續性資料存放區有資料輸出費用時，這可能會降低成本。

## <a name="when-to-use-distributed-caching"></a>使用分散式快取的時機

快取最適合用來讀取比寫入資料更多的應用程式工作負載，以及資料模型支援您用來在快取中儲存和取出資料的索引鍵/值組織。 當應用程式使用者共用許多常見的資料時，也會更有用。例如，如果每個使用者通常會抓取該使用者特有的資料，快取就不會提供更多的好處。 快取可能非常有用的範例是產品目錄，因為資料不會經常變更，而且所有客戶都會查看相同的資料。

快取的優點變得越來越明顯，因為持續性資料存放區的輸送量限制和延遲延遲，會使整體應用程式效能的限制變得更大。 不過，您可能會因為其他原因而執行快取，而非效能。 對於向使用者顯示的資料，如果您不需要完全保持最新狀態，則當持續性資料存放區沒有回應或無法使用時，快取存取可以做為斷路器。

## <a name="popular-cache-population-strategies"></a>熱門的快取擴展策略

為了能夠從快取取得資料，您必須先將它儲存在該處。 有數個策略可將您需要的資料放入快取中：

- 視需要/快取

    應用程式會嘗試從快取抓取資料，而當快取沒有資料（「遺漏」）時，應用程式會將資料儲存在快取中，以便下一次可供使用。 下次應用程式嘗試取得相同的資料時，它會發現它在快取中尋找的內容（「點擊」）。 若要避免提取已在資料庫上變更的快取資料，您可以在對資料存放區進行變更時使快取失效。
- 背景資料推送

    背景服務會定期將資料推送至快取，而應用程式一律會從快取中提取。 這種方法很適合用在高延遲的資料來源，您不需要一律傳回最新的資料。
- 斷路器

    應用程式通常會直接與持續性資料存放區通訊，但當持續性資料存放區有可用性問題時，應用程式會從快取中抓取資料。 資料可能已使用快取或背景資料推送策略放入快取中。 這是一種錯誤處理策略，而不是提升效能的策略。

為了讓快取中的資料保持在最新，您可以在應用程式建立、更新或刪除資料時，刪除相關的快取專案。 如果您的應用程式有時會取得稍微過期的資料，您可以依賴可設定的到期時間，來設定舊快取資料的限制。

您可以設定絕對到期（自快取專案建立後的時間量）或滑動期限（自上次存取快取專案之後的時間量）。 當您根據快取到期機制來防止資料變得太過時時，會使用絕對到期。 在修正 It 應用程式中，我們將手動收回過時的快取專案，我們將使用滑動到期時間，將最新的資料保留在快取中。 無論您選擇的到期原則為何，快取都會在達到快取的記憶體限制時，自動收回最舊的（最近最少使用或 LRU）專案。

## <a name="sample-cache-aside-code-for-fix-it-app"></a>用於修正 It 應用程式的範例快取程式碼

在下列範例程式碼中，我們會先檢查快取，然後再抓取「Fix It」工作。 如果在快取中找到工作，我們會將它傳回;如果找不到，我們會從資料庫取得它，並將它儲存在快取中。 您為了將快取新增至 `FindTaskByIdAsync` 方法所做的變更會反白顯示。

[!code-csharp[Main](distributed-caching/samples/sample1.cs?highlight=5,9-11,13-15,19)]

當您更新或刪除 Fix It 工作時，您必須讓（移除）快取的工作失效。 否則，未來嘗試讀取該工作將會繼續從快取取得舊資料。

[!code-csharp[Main](distributed-caching/samples/sample2.cs?highlight=7)]

這些是說明簡單快取程式碼的範例;尚未在可下載的 Fix It 專案中執行快取。

## <a name="azure-caching-services"></a>Azure caching 服務

Azure 提供下列快取服務： [Azure Redis](https://msdn.microsoft.com/library/dn690523.aspx)快取和[azure 受控](https://msdn.microsoft.com/library/dn386094.aspx)快取。 Azure Redis 快取是以常用的[開放原始碼 Redis](http://redis.io/)快取為基礎，而且是大部分快取案例的第一種選擇。

<a id="sessionstate"></a>
## <a name="aspnet-session-state-using-a-cache-provider"></a>使用快取提供者 ASP.NET 會話狀態

如[網頁程式開發最佳做法一章](web-development-best-practices.md)所述，最佳作法是避免使用會話狀態。 如果您的應用程式需要會話狀態，則下一個最佳作法是避免預設的記憶體內部提供者，因為這並不會啟用 scale out （web 伺服器的多個實例）。 ASP.NET SQL Server 會話狀態提供者可讓在多部 web 伺服器上執行的網站使用會話狀態，但相較于記憶體內部提供者，它會產生高延遲的成本。 如果您必須使用會話狀態，最好的解決方案是使用快取提供者，例如 Azure 快取的[會話狀態提供者](https://msdn.microsoft.com/library/windowsazure/gg185668.aspx)。

## <a name="summary"></a>摘要

您已瞭解修正 It 應用程式可以如何執行快取以改善回應時間和擴充性，以及讓應用程式在資料庫無法使用時，能夠繼續回應讀取作業。 在[下一章](queue-centric-work-pattern.md)中，我們將示範如何進一步改善擴充性，並讓應用程式繼續回應寫入作業。

## <a name="resources"></a>資源

如需快取的詳細資訊，請參閱下列資源。

文件

- [Azure](https://msdn.microsoft.com/library/gg278356.aspx)快取。 關於在 Azure 中快取的官方 MSDN 檔。
- [Microsoft 模式和實務-Azure 指引](https://msdn.microsoft.com/library/dn568099.aspx)。 請參閱快取指引和另行快取模式。
- [損毀修復：具有恢復功能的雲端架構指引](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx)。 白皮書： Marc Mercuri、Ulrich Homann 和 Andrew Townhill。 請參閱快取一節。
- [Azure 上大規模服務設計的最佳作法雲端服務](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 W. 以標記 Simm 和 Michael Thomassy 的技術白皮書。 請參閱分散式快取一節。
- 分散式快取，[指向擴充性的路徑](https://msdn.microsoft.com/magazine/dd942840.aspx)。 舊版（2009）的 MSDN 雜誌文章，但已清楚撰寫分散式快取的簡介;更深入探討防安全和最佳做法白皮書的快取區段。

影片

- [防安全功能：建立可擴充、可復原的雲端服務](https://channel9.msdn.com/Series/FailSafe)。 Ulrich Homann、Marc Mercuri 和 Mark Simm 的九部分系列。 提供如何架構雲端應用程式的400層級觀點。 這一系列的重點在於理論和原因;如需詳細的作法詳細資料，請參閱以標記 Simm 建立大數列。 從1:24:14 開始，參閱第3集的 caching 討論。
- [打造 Big：從 Azure 客戶學到的經驗-第一部分](https://channel9.msdn.com/Events/Build/2012/3-029)。Simon Davies 將討論從46:00 開始的分散式快取。 類似于防故障的系列，並深入探討如何詳細說明。 簡報已于2012年10月31日提供，因此不會涵蓋2013中所引進 Azure App Service Web Apps 的快取服務。

程式碼範例

- [Azure 中的雲端服務基本](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)概念。 執行分散式快取的範例應用程式。 請參閱隨附的 blog 文章[雲端服務基礎–快取基本概念](https://blogs.msdn.com/b/windowsazure/archive/2013/10/03/cloud-service-fundamentals-caching-basics.aspx)。

> [!div class="step-by-step"]
> [上一頁](transient-fault-handling.md)
> [下一頁](queue-centric-work-pattern.md)
