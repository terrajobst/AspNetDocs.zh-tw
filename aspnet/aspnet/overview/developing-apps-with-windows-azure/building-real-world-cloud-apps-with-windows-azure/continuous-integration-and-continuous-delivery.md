---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery
title: 持續整合與持續傳遞（使用 Azure 建立真實世界的雲端應用程式） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 電子書建立真實世界的雲端應用程式，是以 Scott Guthrie 所開發的簡報為基礎。 它會說明13個模式和實務，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: eaece9f5-f80c-428b-b771-5db66d275b7d
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery
msc.type: authoredcontent
ms.openlocfilehash: cf3c65ef95528173eed3fb08984035b2512861c4
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457033"
---
# <a name="continuous-integration-and-continuous-delivery-building-real-world-cloud-apps-with-azure"></a>持續整合與持續傳遞（使用 Azure 建立真實世界的雲端應用程式）

由[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom 作者: dykstra](https://github.com/tdykstra)

[下載 Fix It 專案](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下載電子書](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 電子書建立真實世界的雲端應用程式**，是以 Scott Guthrie 所開發的簡報為基礎。 其中說明13種模式和作法，可協助您成功開發雲端 web 應用程式。 如需電子書的相關資訊，請參閱[第一章](introduction.md)。

前兩個建議的開發程式模式會將[所有專案](automate-everything.md)和[原始檔控制](source-control.md)自動化，而第三個進程模式會將它們結合在一起。 持續整合（CI）表示每當開發人員將程式碼簽入來源存放庫時，就會自動觸發組建。 持續傳遞（CD）更進一步：在組建和自動化單元測試成功之後，您會自動將應用程式部署到可執行更深入測試的環境。

雲端可讓您將維護測試環境的成本降到最低，因為只有在使用環境資源時才需要付費。 您的 CD 程式可以在需要時設定測試環境，而且當您完成測試時，可以關閉環境。

## <a name="continuous-integration-and-continuous-delivery-workflow"></a>持續整合與持續傳遞工作流程

一般來說，我們建議您持續傳遞至您的開發和預備環境。 大部分的小組（甚至是 Microsoft）都需要手動審查和核准，才能進行生產環境部署。 針對生產環境部署，您可能會想要確保開發小組的重要人員可支援，或在低流量期間發生。 但是，沒有任何功能可防止您完全自動化您的開發和測試環境，讓開發人員只需要簽入變更，並設定環境來進行接受度測試。

下圖來自[Microsoft 模式和實務電子書關於持續傳遞](https://aka.ms/ReleasePipeline)說明一般工作流程。 按一下影像，以查看其原始內容中的完整大小。

[![持續傳遞工作流程](continuous-integration-and-continuous-delivery/_static/image1.png)](https://msdn.microsoft.com/library/dn449955.aspx)

## <a name="how-the-cloud-enables-cost-effective-ci-and-cd"></a>雲端如何實現符合成本效益的 CI 和 CD

在 Azure 中自動化這些程式很簡單。 因為您是在雲端中執行所有專案，所以您不需要為組建或測試環境購買或管理伺服器。 而且您不需要等候伺服器在上執行測試。 在您執行的每個組建中，您可以使用自動化腳本來加速 Azure 中的測試環境、執行接受度測試或對其進行更深入的測試，然後在完成時將它卸載。 而且，如果您只執行了2小時或8小時或一天的伺服器，就必須支付費用，因為您只需支付機器實際執行的時間。 例如，如果您從免費層級往上移一層，則修正 it 應用程式所需的環境基本上會花費大約每小時1美分的成本。 在一個月的過程中，如果您一次只執行一個小時的環境，則您的測試環境可能會比您在星巴克購買的 latte 還便宜。

## <a name="azure-devops-services"></a>Azure DevOps Services 

Azure DevOps Services 提供許多功能，可協助您從規劃部署進行應用程式開發。

- 它同時支援 Git （分散式）和 TFVC （集中式）原始檔控制。
- 它提供彈性組建服務，這表示它會在需要時動態建立組建伺服器，並在完成時將其關閉。 當有人簽入原始程式碼變更時，您可以自動啟動組建，而且您不需要為自己的組建伺服器進行配置和付費，而是大部分時間都處於閒置狀態。 只要您未超過特定數目的組建，組建服務就是免費的。 如果您預期會執行大量的組建，您可以為保留的組建伺服器額外支付一些費用。
- 它支援持續傳遞至 Azure。
- 它支援自動化的負載測試。 負載測試對雲端應用程式很重要，但通常會被忽略，直到延遲太晚為止。 負載測試會模擬數以千計的使用者大量使用應用程式，讓您在將應用程式發行至生產環境之前，可以找出瓶頸並改善輸送量。
- 它支援小組室共同作業，可協助小型 agile 團隊進行即時通訊和協同作業。
- 它支援 agile 專案管理。

如需 Azure DevOps Services 的持續整合和傳遞功能的詳細資訊，請參閱[Azure DevOps 檔](/azure/devops/index)。

如果您要尋找一個關鍵專案管理、小組共同作業和原始檔控制解決方案，請參閱 Azure DevOps Services。 在[Azure DevOps Services](https://dev.azure.com/)註冊。

## <a name="summary"></a>摘要

前三個雲端開發模式是關於如何以低週期時間執行可重複、可靠且可預測的開發流程。 在[下一章](web-development-best-practices.md)中，我們將開始探討架構和程式碼撰寫模式。

## <a name="resources"></a>資源

如需詳細資訊，請參閱[在 Azure App Service 中部署 web 應用程式](https://azure.microsoft.com/documentation/articles/web-sites-deploy/)。

另請參閱下列資源：

- [使用 Team Foundation Server 2012 建立發行管線](https://aka.ms/ReleasePipeline)。 電子書、實際操作實驗室，以及 Microsoft 模式與實務的範例程式碼，提供持續傳遞的深入介紹。 涵蓋使用 Visual Studio Lab Management 和 Visual Studio Release Management。
- [ALM Ranger DevOps 工具和指引](https://aka.ms/vsarsolutions/)。 ALM Ranger 引進了 DevOps 工作臺範例附屬解決方案，以及與使用*tfs 2012 建立發行管線*的 &amp; 模式共同作業的實務指導方針，這是開始學習 tfs 2012 的 DevOps &amp; Release Management 的概念並開始使用的絕佳方法。 本指南將說明如何建立一次，並部署至多個環境。
- [使用 Visual Studio 2012 來測試持續傳遞](https://msdn.microsoft.com/library/jj159345.aspx)。 Microsoft 的模式和實務電子書，說明如何將自動化測試與持續傳遞整合在一起。
- [WindowsAzureDeploymentTracker](https://github.com/RyanTBerry/WindowsAzureDeploymentTracker)。 專為從 TFS （根據標籤）來捕獲組建而設計的工具原始程式碼、建立它、封裝它、允許 DevOps 角色中的人員設定 it 的特定層面，並將其推送至 Azure。 此工具會追蹤部署程式，以便讓作業「復原」至先前部署的版本。 此工具沒有外部相依性，可以使用 TFS Api 和 Azure SDK 獨立運作。
- [持續傳遞：透過組建、測試和部署自動化，可靠的軟體發行](https://www.amazon.com/Continuous-Delivery-Deployment-Automation-Addison-Wesley/dp/0321601912/ref=sr_1_1?s=books&amp;ie=UTF8&amp;qid=1377126361)。 Book by Jez Humble。
- [發行！設計和部署已準備好用於生產環境的軟體](https://www.amazon.com/Release-It-Production-Ready-Pragmatic-Programmers/dp/0978739213)。 依 Michael T Nygard。

> [!div class="step-by-step"]
> [上一頁](source-control.md)
> [下一頁](web-development-best-practices.md)
