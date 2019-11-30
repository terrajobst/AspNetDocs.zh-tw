---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
title: 使用 Azure 建立真實世界的雲端應用程式 |Microsoft Docs
author: MikeWasson
description: 本電子書將逐步引導您建立以模式為基礎的方法，以建立真實世界的雲端解決方案。 這些模式適用于開發進程以及 。
ms.author: riande
ms.date: 06/12/2014
ms.assetid: accfa16a-ab15-4c26-9ad4-babdc2a77d2e
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
msc.type: authoredcontent
ms.openlocfilehash: 8a4ef3aa37a9296e92fbeb513968e3abeee072d0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74585525"
---
# <a name="building-real-world-cloud-apps-with-azure"></a>使用 Azure 建立真實世界的雲端應用程式

由[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom 作者: dykstra](https://github.com/tdykstra)

[下載 Fix It 專案](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下載電子書](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> 本電子書將逐步引導您建立以模式為基礎的方法，以建立真實世界的雲端解決方案。 這些模式適用于開發程式以及架構和程式碼撰寫實務。
> 
> 內容是以 Scott Guthrie 開發的簡報為基礎，並由他在2013年6月（第[1](http://vimeo.com/68215538)部分，[第 2](http://vimeo.com/68215602)部分）和 Microsoft Tech Ed 2013 澳大利亞（第[1](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324)部，第[2](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325)部分）的「挪威開發人員會議」（NDC）提供。 [許多人](more-patterns-and-guidance.md#acknowledgments)都會更新並增強內容，同時將它從影片轉換成書面形式。

## <a name="intended-audience"></a>適用對象

對於想要針對雲端進行開發的開發人員而言，考慮移至雲端或雲端開發的新手，會大致瞭解他們需要知道的最重要概念和做法。 概念會以具體範例來說明，而每個章節都會連結至其他資源，以取得更深入的資訊。 這些範例和其他資源的連結適用于 Microsoft 架構和服務，但說明的原則也適用于其他 網頁程式開發架構和雲端環境。

已針對雲端進行開發的開發人員可能會在這裡找到有助於使其更成功的想法。 系列中的每個章節都可以獨立讀取，因此您可以挑選並選擇您感興趣的主題。

有人監看 Scott Guthrie*使用 Azure 簡報建立真實世界的雲端應用程式*，並想要更多詳細資料和更新的資訊，請參閱這裡。

<a id="patterns"></a>
## <a name="cloud-development-patterns"></a>雲端開發模式

這本電子書會針對雲端開發說明13個建議模式。 在這裡使用「模式」，是指執行事項的建議方式：如何開發、設計和編碼雲端應用程式。 這些是重要的模式，可協助您在後續追蹤「成功」的情況。

- 將[所有專案自動化](automate-everything.md)。

    - 使用腳本來最大化效率，並將重複性進程中的錯誤降至最低。
    - 示範： Azure 管理腳本。
- [原始檔控制](source-control.md)。 

    - 在原始檔控制中設定分支結構，以加速 DevOps 工作流程。
    - 示範：將腳本加入至原始檔控制。
    - 示範：將敏感性資料從原始檔控制中排除。
    - 示範：在 Visual Studio 中使用 Git。
- [持續整合與傳遞](continuous-integration-and-continuous-delivery.md)。 

    - 使用每個原始檔控制簽入，將組建和部署自動化。
- [Web 開發最佳作法](web-development-best-practices.md)。 

    - 保持 web 層無狀態。
    - 示範： Azure App Service 中的 Web Apps 縮放和自動調整。
    - 避免會話狀態。
    - 當 CDN 無法使用時，請將 CDN 與 fallback 搭配使用。
    - 使用非同步程式設計模型。
    - 示範：在 ASP.NET MVC 和 Entity Framework 中非同步。
- [單一登入](single-sign-on.md)。 

    - Azure Active Directory 簡介。
    - 示範：建立使用 Azure Active Directory 的 ASP.NET 應用程式。
- [資料儲存選項](data-storage-options.md)。 

    - 資料存放區的類型。
    - 如何選擇正確的資料存放區。
    - 示範： Azure SQL Database。
- [資料分割策略](data-partitioning-strategies.md)。 

    - 以垂直、水準或兩者的方式分割資料，以加速調整關係資料庫。
- [非結構化 blob 儲存體](unstructured-blob-storage.md)。 

    - 使用 blob 服務將檔案儲存在雲端。
    - 示範：在修正 It 應用程式中使用 blob 儲存體。
- [設計到存活的失敗](design-to-survive-failures.md)。 

    - 失敗的類型。
    - 失敗範圍。
    - 瞭解 Sla。
- [監視和遙測](monitoring-and-telemetry.md)。 

    - 為什麼您應該同時購買遙測應用程式，並撰寫自己的程式碼來檢測您的應用程式。
    - 示範： Azure 的新 New relic
    - 示範：在修正 It 應用程式中記錄程式碼。
    - 示範：修正 It 應用程式中的相依性插入。
    - 示範： Azure 中的內建記錄支援。
- [暫時性錯誤處理](transient-fault-handling.md)。 

    - 使用智慧型重試/轉型邏輯來減輕暫時性失敗的影響。
    - 示範： Entity Framework 6 中的 [重試]/[關閉]。
- [分散式](distributed-caching.md)快取。 

    - 使用分散式快取來改善擴充性並降低資料庫交易成本。
- 以[佇列為中心的工作模式](queue-centric-work-pattern.md)。 

    - 藉由鬆散結合 web 和背景工作角色層，啟用高可用性並改善擴充性。
    - 示範：修正 It 應用程式中的 Azure 儲存體佇列。
- [更多雲端應用程式模式和指導](more-patterns-and-guidance.md)方針。
- [附錄︰修正範例應用程式](the-fix-it-sample-application.md)

    - 已知問題
    - 最佳做法
    - 如何下載、建立、執行和部署。

這些模式適用于所有雲端環境，但我們將使用以 Microsoft 技術和服務為基礎的範例（例如 Visual Studio、Team Foundation Service、ASP.NET 和 Azure）加以說明。

本章節的其餘部分將介紹 fix it 應用程式執行所在 Azure App Service 雲端環境中的修正 It 範例應用程式和 Web Apps。

<a id="fixit"></a>
## <a name="the-fix-it-sample-application"></a>修正 it 範例應用程式

本電子書中所顯示的大部分螢幕擷取畫面和程式碼範例，都是以[Scott Guthrie](https://weblogs.asp.net/scottgu/)最初開發的修正 It 應用程式為基礎，以示範建議的雲端應用程式開發模式和實務。

![修正 It 應用程式首頁](introduction/_static/image1.png)

範例應用程式是簡單的工作專案票證系統。 當您需要固定的專案時，您會建立票證並將它指派給其他人，而其他人可以登入並查看指派給他們的票證，並在工作完成時將票證標示為已完成。

這是標準的 Visual Studio Web 專案。 它是以 ASP.NET MVC 為基礎，並使用 SQL Server 資料庫。 它可以在 IIS Express 本機執行，並可部署至 Azure 網站以在雲端中執行。 您可以使用表單驗證和本機資料庫，或使用社交提供者（例如 Google）來登入。 （稍後我們也會示範如何使用 Active Directory 組織帳戶登入。）

![登入頁面](introduction/_static/image2.png)

登入之後，您可以建立票證，將它指派給其他人，並上傳您想要修正的圖片。

![建立 Fix It 工作](introduction/_static/image3.png)

![修正已建立的 It 工作](introduction/_static/image4.png)

您可以追蹤所建立之工作專案的進度、查看指派給您的票證、查看票證詳細資料，以及將專案標示為已完成。

這是從功能觀點來看的一個非常簡單的應用程式，但您會瞭解如何建立它，讓它可以擴充至數百萬名使用者，並可復原資料庫失敗和連接終止等專案。 您也將瞭解如何建立自動化和敏捷式開發工作流程，讓您能夠輕鬆地啟動簡單的應用程式，並以有效率且快速的方式反復執行開發週期。

<a id="waws"></a>
## <a name="web-apps-in-azure-app-service"></a>Azure App Service 中的 Web Apps

用於修正 It 應用程式的雲端環境是我們稱之為「網站」的 Azure 服務。 此服務可讓您在 Azure 中裝載自己的 web 應用程式，而不需要建立 Vm 並保持其更新、安裝和設定 IIS 等。我們會在 Vm 上裝載您的網站，並自動為您提供備份和復原和其他服務。 Web Sites 服務適用于 ASP.NET、node.js、PHP 和 Python。 它可讓您使用 Visual Studio、Web Deploy、FTP、Git 或 TFS，非常快速地進行部署。 在您開始部署的時間和透過網際網路提供更新的時間之間，通常只需要幾秒鐘的時間。 免費開始使用，而且您可以隨著流量成長而相應增加。

在幕後，如果您要在自己的 Vm 上使用 IIS 來裝載網站，則 Azure App Service 中的 Web Apps 會提供許多您必須自行建立的架構元件和功能。 其中一個元件是部署端點，會自動設定 IIS，並在您想要執行網站的多個 Vm 上安裝您的應用程式。

![部署服務](introduction/_static/image5.png)

當使用者叫用網站時，他們不會直接叫用 IIS Vm，而是透過[應用程式要求路由（ARR）](https://www.iis.net/downloads/microsoft/application-request-routing)負載平衡器。 您可以在自己的伺服器上使用這些資訊，但此處的優點是它們是自動設定的。 他們使用智慧型啟發學習法來考慮因素，例如會話親和性、IIS 中的佇列深度，以及每部電腦上的 CPU 使用量，以將流量導向裝載您網站的 Vm。

![ARR 負載平衡器](introduction/_static/image6.png)

如果電腦停止運作，Azure 會自動從輪替中提取該機器、加速新的 VM 實例，並開始將流量導向至新的實例--所有應用程式都不會停機。

![從電腦失敗中自動復原](introduction/_static/image7.png)

這一切都是自動進行。 您只需要建立網站，然後使用 Windows PowerShell、Visual Studio 或 Azure 管理入口網站，將您的應用程式部署到其中。

如需示範如何在 Visual Studio 中建立 web 應用程式並將其部署至 Azure 網站的快速簡單逐步教學課程，請參閱[開始使用 azure 和 ASP.NET](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)。

<a id="summary"></a>
## <a name="summary"></a>總結

本簡介已提供本書將涵蓋的主題清單、範例應用程式的螢幕擷取畫面，以及 Azure App Service 雲端環境中 Web Apps 的簡短總覽。 在和雲端中開發應用程式的其中一個絕佳優點，就是可以輕鬆地自動化重複的開發工作，例如建立測試環境，並將程式碼部署到其中。 這是[下一章](automate-everything.md)的主題。

## <a name="resources"></a>資源

如需本章所涵蓋之主題的詳細資訊，請參閱下列資源。

文件：

- [Azure App Service 中的 Web Apps](https://azure.microsoft.com/services/app-service/web/)。 關於 Web Apps 的 Azure 檔入口網站頁面。
- [Web Apps、雲端服務和 Vm：使用時機？](https://azure.microsoft.com/documentation/articles/choose-web-site-cloud-service-vm/) 如本章所示，WAWS 只是您可以在 Azure 中執行 web 應用程式的三種方法之一。 本文說明三種方式之間的差異，並提供如何選擇哪一個最適合您案例的指引。 就像 Web Sites，雲端服務是 Azure 的 PaaS 功能。 Vm 是 IaaS 功能。 如需 PaaS 與 IaaS 的說明，請參閱[資料選項](data-storage-options.md#paasiaas)一章。

影片：

- [Scott Guthrie 從步驟0開始，什麼是 Azure 雲端 OS？](https://azure.microsoft.com/documentation/videos/what-is-the-cloud-os-scottgu/)
- [Web Sites 架構-使用 Stefan Schackow](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)。
- [Azure 網站內部的 Nir Mashkowski](https://channel9.msdn.com/Shows/Web+Camps+TV/Windows-Azure-Web-Sites-Internals-with-Nir-Mashkowski)。

> [!div class="step-by-step"]
> [下一步](automate-everything.md)
