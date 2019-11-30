---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12
title: 使用 Visual Studio 部署具有 SQL Server Compact 的 ASP.NET Web 應用程式：簡介-12 的 1 |Microsoft Docs
author: tdykstra
description: 這一系列的教學課程會示範如何使用 Visual Stu 部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案 。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a2d7f33b-8c4a-4b48-9fb1-9139cf9b9878
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12
msc.type: authoredcontent
ms.openlocfilehash: ea88da1e6d510f706fc7ca370cfa32974c1243f8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74587762"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-introduction---1-of-12"></a>使用 Visual Studio 部署具有 SQL Server Compact 的 ASP.NET Web 應用程式：簡介-12 的1

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載入門專案](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 這一系列的教學課程會示範如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，來部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案。 如果您安裝 Web 發佈更新，也可以使用 Visual Studio 2010。
> 
> 如需示範在 Visual Studio 2012 的 RC 版本後引進部署功能的教學課程，說明如何部署 SQL Server Compact 以外的 SQL Server 版本，並示範如何部署到 Azure App Service Web Apps，請參閱[使用 Visual Studio ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。
> 
> 這些教學課程會引導您在本機開發電腦上先部署 IIS 以進行測試，然後再進行協力廠商主機服務提供者。 您將部署的應用程式會使用應用程式資料庫和 ASP.NET 成員資格資料庫。 您開始使用 SQL Server Compact 並部署至 SQL Server Compact，稍後的教學課程會示範如何部署資料庫變更，以及如何遷移至 SQL Server。
> 
> 本教學課程假設您知道如何在 Visual Studio 中使用 ASP.NET。 如果您沒有這麼做，最好的起點是[基本的 ASP.NET Web Form 教學](../tailspin-spyworks/tailspin-spyworks-part-1.md)課程或[基本的 ASP.NET MVC 教學](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)課程。
> 
> 如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET 部署論壇](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment)。

## <a name="overview"></a>概觀

這些教學課程會引導您在本機開發電腦上先部署 IIS 以進行測試，然後再進行協力廠商主機服務提供者。 您將部署的應用程式會使用應用程式資料庫和 ASP.NET 成員資格資料庫。 您開始使用 SQL Server Compact 並部署至 SQL Server Compact，稍後的教學課程會示範如何部署資料庫變更，以及如何遷移至 SQL Server。

教學課程的數目–11在所有加上疑難排解頁面，可能會讓部署程式看起來很困難。 事實上，部署網站的基本程式會構成本教學課程集的一個相對較小部分。 不過，在真實世界的情況下，您通常需要一些關於部署的小型但重要額外層面的資訊，例如，在目標伺服器上設定資料夾許可權。 我們在教學課程中包含了許多其他的技巧，希望教學課程不會省略可能會讓您無法成功部署實際應用程式的資訊。

教學課程的設計是依序執行，而且每個元件都是在上一個部分建立。 不過，您可以略過與您的情況無關的元件。 （略過部分可能需要您調整稍後教學課程中的程式）。

## <a name="intended-audience"></a>適用對象

這些教學課程的目標是在小型組織或其他環境中工作的 ASP.NET 開發人員，其中：

- 不會使用持續整合程式（自動化組建和部署）。
- 生產環境是協力廠商主機服務提供者。
- 一個人通常會填滿多個角色（相同人員的開發、測試和部署）。

在企業環境中，更常見的做法是執行持續整合程式，而生產環境通常是由公司自己的伺服器所主控。 不同的人通常也會執行不同的角色。 如需企業部署的相關資訊，請參閱[在企業案例中部署 Web 應用程式](../../deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。

各種規模的組織也可以將 web 應用程式部署至 Azure，而這些教學課程中所顯示的大部分程式也適用于 Web Apps Azure App 服務。 如需 Azure 的簡介，請參閱[https://azure.microsoft.com](https://azure.microsoft.com)。

## <a name="the-hosting-provider-shown-in-the-tutorials"></a>教學課程中顯示的主控提供者

本教學課程會引導您完成設定主控公司帳戶，以及將應用程式部署至該主控提供者的流程。 選擇特定的主控公司，讓教學課程可以說明部署至即時網站的完整體驗。 每個主控公司都提供不同的功能，而部署到其伺服器的經驗則有所不同。不過，本教學課程中所述的程式對整體程式而言是一般的。

本教學課程所使用的裝載提供者（Cytanium.com）是其中一種可用的，而在本教學課程中使用時，不會構成背書或建議。

## <a name="deploying-web-site-projects"></a>部署網站專案

Contoso 大學是 Visual Studio web 應用程式專案。 本教學課程中所示範的大部分部署方法和工具並不適用于[網站專案](https://msdn.microsoft.com/library/dd547590.aspx)。 如需如何部署網站專案的詳細資訊，請參閱[ASP.NET 部署內容對應](https://msdn.microsoft.com/library/bb386521.aspx#deployment_for_web_site_projects)。

## <a name="deploying-aspnet-mvc-projects"></a>部署 ASP.NET MVC 專案

在本教學課程中，您將部署 ASP.NET Web form 專案，但您瞭解如何執行的所有動作也適用于 ASP.NET MVC。 Visual Studio MVC 專案只是另一種形式的 web 應用程式專案。 唯一的不同之處在于，如果您要部署至不支援 ASP.NET MVC 或目標版本的主控提供者，您必須確定您已在專案中安裝適當的（[MVC 3](http://nuget.org/packages/AspNetMvc/3.0.20105.0)或[mvc 4](http://nuget.org/packages/aspnetmvc)） NuGet 套件。

## <a name="programming-language"></a>程式設計語言

範例應用程式會C#使用C#，但教學課程不需要知識，而教學課程所顯示的部署技巧則不是語言特定的。

## <a name="troubleshooting-during-this-tutorial"></a>本教學課程期間的疑難排解

當部署期間發生錯誤，或部署的網站未正確執行時，錯誤訊息不一定會提供解決方案。 為了協助您處理一些常見的問題，您可以使用[疑難排解參考頁面](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。 如果您在進行教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解] 頁面。

## <a name="comments-welcome"></a>歡迎留言

歡迎您提供教學課程的批註，而更新教學課程時，將會針對教學課程批註中提供的改進進行修正或建議。

## <a name="prerequisites"></a>必要條件：

開始之前，請確定您有 Windows 7 或更新版本，以及電腦上安裝的下列其中一項產品：

- [Visual Studio 2010 SP1](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)
- [Visual Web Developer Express 2010 SP1](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VWD2010SP1Pack)
- [適用于 Web 的 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC](https://go.microsoft.com/fwlink/?LinkId=240162)

如果您有 Visual Studio 2010 SP1 或 Visual Web Developer Express 2010 SP1，請同時安裝下列產品：

- [AZURE SDK for .net （VS 2010 SP1）](https://go.microsoft.com/fwlink/?LinkID=208120) （包含 Web 發佈更新）
- [適用于 SQL Server Compact 4.0 的 Microsoft Visual Studio 2010 SP1 工具](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCEVSTools)

需要其他軟體才能完成本教學課程，但您還不需要載入。 本教學課程將逐步引導您在需要時進行安裝的步驟。

## <a name="downloading-the-sample-application"></a>下載範例應用程式

您將部署的應用程式名稱為 Contoso 大學，而且已經為您建立。 這是一個簡化版的大學網站，以鬆散于[ASP.NET 網站上 Entity Framework 教學](https://asp.net/entity-framework/tutorials)課程中所述的 Contoso 大學應用程式為基礎。

當您已安裝必要條件時，請下載[Contoso 大學 web 應用程式](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)。 *.Zip*檔案包含多個版本的專案，以及包含所有12個教學課程的 PDF 檔案。 若要逐步執行教學課程的步驟，請從 ContosoUniversity-Begin 開始。 若要在教學課程結束時查看專案的外觀，請開啟 ContosoUniversity-End。 若要在教學課程10的完整 SQL Server 之前查看專案看起來的樣子，請開啟 ContosoUniversity-AfterTutorial09。

若要準備逐步執行教學課程步驟，請將 ContosoUniversity-開始儲存至您用來處理 Visual Studio 專案的任何資料夾。 根據預設，這會是下列資料夾：

`C:\Users\<username>\Documents\Visual Studio 2012\Projects`

（針對本教學課程中的螢幕擷取畫面，專案資料夾位於 `C`：磁片磁碟機的根目錄中）。

啟動 Visual Studio，開啟專案，然後按下 CTRL-F5 加以執行。

[![Home_page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image2.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image1.png)

網站頁面可從功能表列存取，並可讓您執行下列功能：

- 顯示學生統計資料（[關於] 頁面）。
- 顯示、編輯、刪除及新增學生。
- 顯示和編輯課程。
- 顯示和編輯講師。
- 顯示和編輯部門。

以下是幾個代表性頁面的螢幕擷取畫面。

[![Students_Page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image4.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image3.png)

[![Add_Students_Page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image6.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image5.png)

## <a name="reviewing-application-features-that-affect-deployment"></a>查看會影響部署的應用程式功能

應用程式的下列功能會影響您部署它的方式，或是您必須如何部署它。 本系列的下列教學課程會更詳細地說明每一項。

- Contoso 大學會使用 SQL Server Compact 資料庫來儲存應用程式資料，例如學生和講師姓名。 資料庫包含測試資料與生產資料的混合，而且當您部署到生產環境時，您需要排除測試資料。 稍後在教學課程系列中，您將從 SQL Server Compact 遷移至 SQL Server。
- 應用程式會使用 ASP.NET 成員資格系統，將使用者帳戶資訊儲存在 SQL Server Compact 資料庫中。 應用程式會定義可存取某些受限制資訊的系統管理員使用者。 您需要部署成員資格資料庫，但不含測試帳戶，而是使用一個系統管理員帳戶。
- 因為應用程式資料庫和成員資格資料庫使用 SQL Server Compact 做為資料庫引擎，所以您必須將 database engine 部署至主控提供者以及資料庫本身。
- 應用程式會使用 ASP.NET 通用成員資格提供者，讓成員資格系統可以將其資料儲存在 SQL Server Compact 資料庫中。 包含通用成員資格提供者的元件必須與應用程式一起部署。
- 應用程式會使用 Entity Framework 5.0 來存取應用程式資料庫中的資料。 包含 Entity Framework 5.0 的元件必須與應用程式一起部署。
- 應用程式會使用協力廠商的錯誤記錄和報告公用程式。 這個公用程式是在必須與應用程式一起部署的元件中提供。
- 錯誤記錄公用程式會將 XML 檔案中的錯誤資訊寫入檔案資料夾。 您必須確定 ASP.NET 在部署的網站中執行的帳戶具有此資料夾的寫入權限，而且您必須從部署中排除此資料夾。 （否則，測試環境中的錯誤記錄檔資料可能會部署到生產和/或生產錯誤記錄檔）。
- 應用程式包含一些必須在部署的*web.config*檔案中變更的設定，視目的地環境（測試或生產）而定，以及其他必須根據組建設定（Debug 或 Release）變更的設定而定。
- Visual Studio 解決方案包含類別庫專案。 只應部署此專案所產生的元件，而不是專案本身。

在此系列的第一個教學課程中，您已下載 Visual Studio 專案的範例，以及會影響您如何部署應用程式的網站功能。 在下列教學課程中，您會設定要自動處理的某些專案，以準備進行部署。 您手動處理的其他人。

> [!div class="step-by-step"]
> [下一步](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)
