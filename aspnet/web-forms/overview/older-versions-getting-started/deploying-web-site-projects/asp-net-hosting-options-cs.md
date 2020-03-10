---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/asp-net-hosting-options-cs
title: ASP.NET 裝載選項（C#） |Microsoft Docs
author: rick-anderson
description: ASP.NET web 應用程式通常是在本機開發環境中設計、建立和測試，而且需要部署到實際執行環境（o） 。
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 89a1d2bc-fdfd-4c5c-a3b0-49a08baaf63a
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/asp-net-hosting-options-cs
msc.type: authoredcontent
ms.openlocfilehash: 2eafa750167d89fa996a442633e79dce3d5b85bd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637169"
---
# <a name="aspnet-hosting-options-c"></a>ASP.NET 裝載選項 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載 PDF](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial01_Basics_cs.pdf)

> ASP.NET web 應用程式通常是在本機開發環境中設計、建立和測試，而且必須在準備好發行之後，部署到生產環境。 本教學課程提供部署流程的高階總覽，並作為本教學課程系列的簡介。

## <a name="introduction"></a>簡介

Web 應用程式通常是在開發環境中設計、建立和測試，只有在網站上工作的程式設計人員可以存取。 一旦準備好要發行應用程式之後，就會將它移到生產環境，讓網際網路上的任何人都能存取該網站。 這個部署程式引進了幾項挑戰：

- 生產環境必須存在並正確設定，才可部署 ASP.NET 應用程式;此外，生產環境必須透過最新的安全性修補程式保持在最新狀態。
- 正確的標記檔案、程式碼檔案和支援檔案集合必須從開發環境複製到生產環境。 對於資料驅動的應用程式，這可能需要複製資料庫架構和/或資料。
- 這兩個環境之間可能會有設定差異。 在開發環境中使用的資料庫連接字串或電子郵件伺服器，可能會與生產環境不同。 更多的是，應用程式的行為可能會因環境而異。 例如，在開發期間發生錯誤時，畫面上可能會顯示錯誤的詳細資料，但在生產環境中發生錯誤時，應該改為顯示使用者易記的錯誤頁面，並將錯誤詳細資料以電子郵件傳送給開發人員。

若要排除第一個挑戰-設定和維護生產環境-許多個人和企業會將其生產環境外包給*虛擬主機服務提供者*。 Web 主控提供者是代表您管理生產環境的公司。 有無數的 web 主機提供者，各有不同的價格和服務等級;如需尋找這類服務提供者的秘訣，請參閱「尋找 Web 主機提供者」一節。

這是一系列教學課程中的第一篇，探討將 ASP.NET web 應用程式部署到 web 主機服務提供者所管理之生產環境的相關步驟。 在這些教學課程中，我們將探討：

- 哪些檔案需要部署到 web 主機提供者。
- 簡化部署程式的工具。
- 如何部署資料庫。
- 部署使用[SQL 型成員資格和角色提供者](../../older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs.md)之資料庫的秘訣，以及在生產環境中模擬網站管理工具的方式。
- 使用開發期間所做的變更，在生產環境中順利更新資料庫的策略。
- 用於記錄生產環境中發生之錯誤的技術，以及在發生錯誤時通知開發人員的方式。

這些教學課程的目的是要精簡，並提供逐步指示，讓您能以視覺化方式逐步完成整個流程。 本執筆教學課程提供 ASP.NET 部署程式的總覽，以及尋找 web 主控提供者的建議。 現在就開始吧！

## <a name="an-overview-of-the-aspnet-deployment-process"></a>ASP.NET 部署流程的總覽

簡言之，部署 ASP.NET 應用程式包含下列三個步驟：

1. 在生產環境中設定 web 應用程式、網頁伺服器和資料庫。
2. 同步處理 ASP.NET 網頁、程式碼檔案、`Bin` 資料夾中的元件，以及 CSS 和 JavaScript 檔案之類的 HTML 相關支援檔案。
3. 同步處理資料庫架構和/或資料。

Web 應用程式的設定資訊通常位於 `Web.config` 檔案中，其中包含資料庫連接字串、錯誤處理準則、URL 重寫規則，以及電子郵件伺服器資訊。 在開發中的應用程式與生產環境中的相同應用程式，通常會有不同的這項資訊。 比方說，在開發應用程式時，最好使用開發資料庫，這樣您就不會對生產資料庫進行測試。 因此，開發和生產應用程式之間的資料庫連接字串通常會不同。 由於這些差異，部署的一部分牽涉到對 web 應用程式的設定資訊進行變更。

除了 web 應用程式設定變更之外，步驟1也可能需要 web 伺服器和資料庫的設定。 例如，如果 ASP.NET 網頁在 web 伺服器上建立或刪除目錄中的檔案，則必須將網頁伺服器設定為允許這些檔案系統修改。 同樣地，可能會有需要對資料庫進行的許可權或驗證設定。

步驟2牽涉到在開發與生產環境之間同步處理一組重要的 ASP.NET 網頁和支援檔案。 需要在兩個環境之間同步處理的一組特定 ASP.NET 相關檔案，取決於您在 Visual Studio 中建立的專案類型，而在下一個教學課程中，則是[*決定需要部署哪些*](determining-what-files-need-to-be-deployed-cs.md)檔案的討論。 第三和第四個教學課程-[*使用 FTP 部署您的網站*](deploying-your-site-using-an-ftp-client-cs.md)，並[*使用 Visual Studio*](deploying-your-site-using-visual-studio-cs.md)檢查不同的工具和技術來同步處理這些檔案。

建立資料驅動應用程式時，通常會使用兩個資料庫：一個用於開發，另一個用於生產環境。 在開發期間，您可能會修改開發資料庫的架構，以包含新的資料表、資料行、預存程式和觸發程式，或者可以修改來移除或重新命名現有的資料庫物件。 在進行這些變更的時間與將應用程式部署到生產環境的時間之間，開發和生產資料庫不同步。此非同步必須在部署過程中修正。 這些挑戰將在未來的教學課程中進行檢查。

## <a name="finding-a-web-host-provider"></a>尋找 Web 主機提供者

ASP.NET 應用程式可以部署到已安裝 .NET Framework 和 Internet Information Services （IIS）的任何 web 伺服器。 您可以從個人電腦主控網站，假設您有網際網路的寬頻連線，而且知道如何設定路由器以允許傳入的 web 要求。 您也可以從內部網路中的電腦主控網站，就像許多公司一樣。 不過，這些教學課程的重點是使用 web 主機服務提供者來裝載您的網站。

> [!NOTE]
> [IIS](https://www.iis.net/)是 Microsoft 的企業級 web 伺服器。 它隨附于 windows 的非家用版本，例如 Windows Server 2008 和 Windows Vista 的特定版本。 您不需要安裝 IIS 來提供開發環境中的 ASP.NET 應用程式，因為 Visual Studio 包含 ASP.NET 開發 Web 服務器。 不過，ASP.NET 開發網頁伺服器只接受本機連線，因此無法用於生產環境中。

在您將網站部署到 web 主機提供者之前，您必須先決定要執行業務的公司。 Marketplace 中有無數的 web 主控公司;搜尋「虛擬主機公司」會傳回超過5000000的結果。 您要如何找出最適合您的方法？ 您慣用的搜尋引擎是很好的起點，像是[TopHosts](http://www.tophosts.com/)和[HostCritique](http://www.hostcritique.net/)之類的網站，它會比較和對比各種主機服務。 我也建議詢問同事和同事是否有任何建議;您也可以在這裡的[ASP.NET 論壇](https://forums.asp.net/)，詢問有關[裝載 Open 論壇](https://forums.asp.net/158.aspx)的建議。

虛擬主機的公司通常會提供共用的主控方案和專用的主控方案。 共用裝載的單一 web 伺服器裝載數十個（如果不是數百個不同的網站）。 有了專用主機，您就可以從公司租用一部電腦，讓您的網站和網站獨立服務。 共用的主控方案可能包括 ASP.NET 網頁的支援、使用 Microsoft Access 資料庫的能力、5 GB 的磁碟空間，以及每月 $9.95 100 GB 的每月頻寬流量。 另一個共用的主控方案可能包括對 ASP.NET 網頁的支援、Microsoft SQL Server 2008 資料庫伺服器的存取、10 GB 的磁碟空間，以及每月 $19.95 250 GB 的每月頻寬流量。 專用的主控方案通常會更昂貴，每個月會花費數百美元的成本，但可提供比共用裝載選項更好的效能和更多控制。 您所選擇的計畫取決於您的預算、網站接收的流量，以及您預期需要的功能。

選擇 web 主機提供者時，有兩個重要的考慮是客戶服務和服務品質。 如果您有問題或設定問題，將問題提交給 web 主機的技術服務人員需要多久的時間才會收到回應？ 公司服務有多可靠？ 他們經常有資料庫中斷嗎？ 其電子郵件伺服器離線的頻率為何？ 您一律可以要求公司提供有關其執行時間的詳細資料，並詢問其客戶服務原則，但更笑話的方法是要求目前和過去客戶的意見反應，您可以透過線上論壇、新聞群組和電子郵件 listservs.

> [!NOTE]
> 有些 web 主控公司將其業務專注于特定的技術堆疊，例如 .NET 或[燈泡](http://en.wikipedia.org/wiki/LAMP_stack)（**L** **inux、Apache、** **M** ySQL 和**P** HP），因此請確定您選取的公司會裝載 ASP.NET 應用程式。 另請檢查並確定其支援您用來建立應用程式的 ASP.NET 版本。 如果您要建立資料驅動應用程式，請確定 web 主機提供您所使用的相同資料庫伺服器和版本。

## <a name="summary"></a>總結

ASP.NET web 應用程式通常是在本機開發環境中設計、建立和測試。 一旦版本準備好發行之後，它就會移到生產環境。 雖然您可以在個人電腦或公司內的伺服器上裝載 ASP.NET 網站，但許多企業和個人都選擇將其裝載外包給 web 主機提供者。

本教學課程系列會檢查將 ASP.NET 應用程式部署至 web 主機提供者的步驟，以探索常見的挑戰。 本教學課程提供 ASP.NET 部署程式的高階總覽，以及尋找適當 web 主機提供者的秘訣。 下一個教學課程將探討部署網站時，需要將哪些 ASP.NET 相關檔案複製到生產環境。

快樂的程式設計！

### <a name="special-thanks-to"></a>特別感謝 。

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Teresa Murphy。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)的那一行下拉式。

> [!div class="step-by-step"]
> [下一個](determining-what-files-need-to-be-deployed-cs.md)
