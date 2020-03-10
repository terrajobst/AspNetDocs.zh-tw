---
uid: whitepapers/aspnet-web-deployment-content-map
title: ASP.NET Web 部署-建議的資源 |Microsoft Docs
author: rick-anderson
description: 本主題提供有關如何使用 Visual Studio 2010，Visual Web De，將 web 應用程式部署（發佈）至 IIS 的檔資源連結
ms.author: riande
ms.date: 03/14/2014
ms.assetid: 58b583cd-c4ab-47a3-8527-8c92c298c91f
msc.legacyurl: /whitepapers/aspnet-web-deployment-content-map
msc.type: content
ms.openlocfilehash: 96873c8f2b0ad2415f371aceb651400c801a3338
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78636987"
---
# <a name="aspnet-web-deployment---recommended-resources"></a>ASP.NET Web 部署 - 建議資源

> 本主題提供有關如何使用 Visual Studio 2010、Visual Web Developer 2010 和更新版本，將 web 應用程式部署（發佈）至 IIS 的檔資源連結。
> 
> 如果您知道絕佳的 blog 文章、 [stackoverflow](http://stackoverflow.com)執行緒或任何其他有用的連結，請傳送含有連結的[電子郵件給我們](mailto:aspnetue@microsoft.com?subject=Deployment%20Content%20Map)。
> 
> > [!NOTE] 
> > 
> > 其中有許多資源會描述只有在您安裝最新版本的[Visual Studio Web 發行更新](https://go.microsoft.com/fwlink/?LinkID=208120)時才可使用的部署功能。 某些功能僅適用于 Visual Studio 2012 或 Visual Studio 2013。

本主題包含下列各節：

- [瞭解 Web 專案的部署選項](#understanding)
- [尋找 ASP.NET 應用程式的主控提供者](#findinghosting)
- [從 Visual Studio 部署 web 應用程式](#fromvs)
- [藉由建立和安裝 web 部署套件來部署 web 應用程式](#package)
- [使用持續整合（CI）流程部署 web 應用程式](#ci)
- [在部署期間使用 web.config 轉換來變更目的地 Web.config 檔案或 app.config 檔案中的設定](#transforms)
- [在部署期間使用 Web Deploy 參數來變更目的地 Web 應用程式中的設定](#webdeployparms)
- [確定應用程式在部署期間離線](#appoffline)
- [在 web 應用程式部署過程中，將資料庫或變更部署至資料庫](#databasewithweb)
- [將資料庫與 web 應用程式部署分開部署](#databaseseparate)
- [部署使用 ASP.NET 應用程式服務（例如成員資格和分析）的 web 應用程式](#aspnetmembership)
- [用於部署的先行編譯](#precompiling)
- [部署內部網路 web 應用程式](#intranet)
- [自動化未自動推出的一般部署工作](#automating)
- [設定網頁伺服器，讓開發人員可以使用 Web Deploy 來部署 web 應用程式](#configuringservers)
- [設定主控提供者的伺服器](#hostingprovider)
- [針對部署問題進行疑難排解](#troubleshooting)
- [取得特定部署問題的協助](#gettinghelp)
- [其他資源](#additional)

<a id="understanding"></a>

## <a name="understanding-deployment-options-for-web-projects"></a>瞭解 Web 專案的部署選項

- [Visual Studio 和 ASP.NET 的 Web 部署總覽](https://msdn.microsoft.com/library/dd394698.aspx)（MSDN）。
- [如何部署 Windows Azure](https://docs.microsoft.com/azure/app-service-web/web-sites-deploy)網站。 說明將 Web 專案部署至 Windows Azure 網站的資源選項和連結，包括[持續傳遞](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)（從原始檔[控制](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)自動化）以及使用 Visual Studio。
- [Visual Studio 2012 Web 發佈改良功能](../visual-studio/overview/2012/visual-studio-2012-web-publishing-improvements.md)（透過 Scott Hanselman 的影片）。
- [VS 2010 中 Web 部署的總覽文章](http://vishaljoshi.blogspot.com/2009/09/overview-post-for-web-deployment-in-vs.html)（Vishal Joshi 的 blog）。 較舊的 blog 文章，但其所連結的部分 Visual Studio 2010 資源具有 Visual Studio 2012 仍相關的資訊。

<a id="findinghosting"></a>

## <a name="finding-hosting-providers-for-an-aspnet-application"></a>尋找 ASP.NET 應用程式的主控提供者

- [ASP.NET 裝載](https://asp.net/hosting)

<a id="fromvs"></a>

## <a name="deploying-a-web-application-from-visual-studio"></a>從 Visual Studio 部署 web 應用程式

- [如何部署 Windows Azure](https://docs.microsoft.com/azure/app-service-web/web-sites-deploy)網站。 說明選項，並提供將 Web 專案部署至 Windows Azure 網站的資源連結。 包含有關從 Visual Studio 部署的區段。
- [使用 Visual Studio 的 ASP.NET Web 部署](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)。 12部分教學課程系列說明如何使用 SQL Server 資料庫部署 web 應用程式。 針對資料庫部署，會同時使用 dbDacFx 提供者和 Entity Framework Code First 移轉。 也包含 web.config 檔案[轉換](../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md)、[部署個別](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md#specificfiles)檔案、[命令列部署](../web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment.md)，以及[如何藉由 .pubxml 檔案自訂 Visual Studio web 發佈管線的](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files.md)相關資訊。 適用于所有 ASP.NET Web 專案，包括 Web Forms、MVC 和 Web API。）
- [如何：在 Visual Studio 中使用單鍵發佈來部署 Web 專案](https://msdn.microsoft.com/library/dd465337.aspx)（Visual Studio Web 發佈嚮導的參考資訊）。
- [使用 Visual Studio 部署具有 SQL Server Compact 的 ASP.NET Web 應用程式](../web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md)。 這是舊版的**ASP.NET Web 部署，使用**本節頂端列出的 Visual Studio。 現在很有用，可取得如何部署 SQL Server Compact 資料庫，以及如何從 SQL Server Compact 遷移至完整版 SQL Server 的相關資訊。
- [使用儲存體資料表、佇列和 blob （Microsoft Azure 網站）的 .Net 多層式應用程式](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)。 5部分教學課程系列，示範如何建立 MVC 專案，並將其部署至 Windows Azure 雲端服務。

<a id="package"></a>
## <a name="deploying-a-web-application-by-creating-and-installing-a-web-deployment-package"></a>藉由建立和安裝 web 部署套件來部署 web 應用程式

- [如何：在 Visual Studio （MSDN）中建立 Web 部署套件](https://msdn.microsoft.com/library/dd465323.aspx)。
- [如何：使用 Visual Studio （MSDN）建立的部署 .cmd 檔案來安裝部署套件](https://msdn.microsoft.com/library/ff356104.aspx)。
- [使用 Web Deploy 封裝，在 dev box 和協力廠商主機](http://sedodream.com/2011/11/08/UsingAWebDeployPackageToDeployToIISOnTheDevBoxAndToAThirdPartyHost.aspx)（Sayed Hashimi 的 blog）上部署到 IIS。 如何使用 IIS 管理員，在本機電腦和支援 IIS 管理員進行遠端系統管理的主控公司上，安裝 IIS 中的部署套件。
- [從 Visual Studio 2010](https://www.iis.net/learn/publish/using-web-deploy/building-a-web-deploy-package-from-visual-studio-2010) （IIS.NET 網站）建立 Web Deploy 套件。 包含建立和安裝命令列套件的指示。
- [套件一次發佈到任何地方](http://sedodream.com/2012/03/14/PackageWebUpdatedAndVideoBelow.aspx)（Sayed Hashimi 的 blog）。 引進的 NuGet 套件會自動化轉換多個目的地環境之 web.config 檔案的程式，讓您可以將一個封裝部署到多部伺服器。 另請參閱[PackageWeb video](https://www.youtube.com/watch?v=-LvUJFI8CzM) By Sayed Hashimi。

另請參閱下一節。

<a id="ci"></a>

## <a name="deploying-a-web-application-using-a-continuous-integration-ci-process"></a>使用持續整合（CI）流程部署 web 應用程式

- [持續整合與持續傳遞（使用 Windows Azure 建立真實世界的雲端應用程式）。](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) 介紹持續整合和持續傳遞的電子書章節。
- [如何部署 Windows Azure](https://docs.microsoft.com/azure/app-service-web/web-sites-deploy)網站。 說明將 Web 專案部署至 Windows Azure 網站的選項和資源連結。 包含有關從原始檔控制自動化部署的區段。
- [在企業案例中部署 Web 應用程式](../web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。 40-部分教學課程系列，說明如何使用 Visual Studio 2010 和 Team Foundation Server 2010，在 CI 程式中自動進行部署。
- 在[Microsoft Build Engine 內：使用 MSBuild 和 Team Foundation Build，方法是 Sayed Hashimi 和 William Bartholomew](http://msbuildbook.com)。 這是一本書，而不是 web 資源，但它是瞭解如何設定 MSBuild 以進行持續整合案例的基本指南。
- [MSBuild 延伸模組套件](https://github.com/mikefourie/MSBuildExtensionPack)。 包含部署工作。
- [Team Foundation Build 自訂指南](https://aka.ms/vsarsolutions)。 由 ALM Ranger 設定 Team Foundation Server 涵蓋 web 部署的檔，並包含教學課程和影片。
- [從 CI 伺服器 SLOWCHEETAH XML 轉換](http://sedodream.com/2011/12/12/SlowCheetahXMLTransformsFromACIServer.aspx)（Sayed Hashimi 的 blog）。 說明如何使用 SlowCheetah，這是用於轉換 app.config 和其他 XML 檔案的 Visual Studio 增益集。

另請參閱此頁面稍後的[部署期間，請確定應用程式已離線](aspnet-web-deployment-content-map.md#appoffline)。

<a id="transforms"></a>

## <a name="using-webconfig-transformations-to-change-settings-in-the-destination-webconfig-file-or-appconfig-file-during-deployment"></a>在部署期間使用 web.config 轉換來變更目的地 Web.config 檔案或 app.config 檔案中的設定

- Web.config 檔案[轉換](../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md)。
- [使用 Visual Studio （MSDN）進行 Web 專案部署的 Web.config 轉換語法](https://msdn.microsoft.com/library/dd465326.aspx)。
- [Web 工具 2012.2-web.config 轉換](https://www.youtube.com/watch?v=HdPK8mxpKEI)（Sayed Hashimi 的 YouTube video）。 說明如何設定和預覽 Web.config 轉換。
- [如何? 停用 Web.config 轉換嗎？](https://msdn.microsoft.com/library/ee942158.aspx#disable_web_config_transformation) （MSDN）。
- [我何時應該使用 Web Deploy 參數，而不是 Web.config 轉換？](https://msdn.microsoft.com/library/ee942158.aspx#web_deploy_parameters) （MSDN）。
- Codeplex.com （.Net Web 開發和工具 blog）[上發行的 XDT （XML 檔轉換）](https://blogs.msdn.com/b/webdev/archive/2013/04/23/xdt-xml-document-transform-released-on-codeplex-com.aspx) 。 宣佈 Web.config 檔案轉換引擎原始程式碼的可用性，並列出一些使用此程式碼的工具。
- [Windows Azure 網站：應用程式字串與連接字串的運作方式](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)（Microsoft Azure 的 blog）。 如果您的目的地環境是 Windows Azure 網站，而您想要轉換 `appSettings` 或 `connectionStrings`，則 web.config 的替代方法是轉換。

<a id="webdeployparms"></a>

## <a name="using-web-deploy-parameters-to-change-settings-in-the-destination-web-application-during-deployment"></a>在部署期間使用 Web Deploy 參數來變更目的地 Web 應用程式中的設定

- [如何：在 Web 部署套件中使用 Web Deploy 參數](https://msdn.microsoft.com/library/ff398068.aspx)（MSDN）。
- [Msdeploy.exe：如何根據發行設定檔（Sayed Hashimi 的 blog）更新發佈上的應用程式設定](http://sedodream.com/2013/03/02/MSDeployHowToUpdateAppSettingsOnPublishBasedOnThePublishProfile.aspx)。 說明如何將 Web deploy 參數整合到 Visual Studio 發行設定檔中。
- [Web Deploy 參數](https://www.iis.net/learn/publish/using-web-deploy/web-deploy-parameterization)化（IIS.NET 網站）。
- [動作中的 Web Deploy 參數](http://vishaljoshi.blogspot.com/2010/07/web-deploy-parameterization-in-action.html)化（Vishal Joshi 的 blog）。
- [Web Deploy 參數化與 Web.config 轉換](http://vishaljoshi.blogspot.com/2010/06/parameterization-vs-webconfig.html)（Vishal Joshi 的 blog）。
- [Windows Azure 網站：應用程式字串與連接字串的運作方式](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)（Microsoft Azure 的 blog）。 如果您的目的地環境是 Windows Azure 網站，而您想要將 `appSettings` 或 `connectionStrings`參數化，Web deploy 參數的替代方案。

<a id="appoffline"></a>

## <a name="making-sure-an-application-is-off-line-during-deployment"></a>確定應用程式在部署期間離線

- [使用 Visual Studio ASP.NET Web 部署：部署程式碼更新](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md)。 請參閱在**部署期間讓應用程式離線**的一節。
- [在發佈之前讓應用程式離線](https://www.iis.net/learn/publish/deploying-application-packages/taking-an-application-offline-before-publishing)（IIS.net 網站）。 說明 Web Deploy 3.0 內建的功能，可將應用程式\_離線的 .htm 檔案自動處理。 這項功能無法搭配自訂應用程式\_離線 .htm 檔案使用。
- [如何讓您的 web 應用程式在發佈期間離線](http://sedodream.com/2012/01/08/HowToTakeYourWebAppOfflineDuringPublishing.aspx)（Sayed Hashimi 的 blog）。 如何自動執行使用自訂應用程式\_離線 .htm 檔案的流程。
- [離線和 usechecksum 應用程式的 Web 發佈更新](https://blogs.msdn.com/b/webdev/archive/2013/10/30/web-publishing-updates-for-app-offline-and-usechecksum.aspx)（Microsoft Web 開發 blog）。 自動使用應用程式\_離線 .htm 檔案的另一個選項。
- [Web Deploy 3.5 RTW](https://blogs.iis.net/msdeploy/archive/2013/07/09/webdeploy-3-5-rtw.aspx) （IIS.net 網站）。 Web Deploy 3.5 中的新功能，適用于自訂應用程式\_離線 .htm 檔案。

<a id="databasewithweb"></a>

## <a name="deploying-a-database-or-changes-to-a-database-as-part-of-web-application-deployment"></a>在 web 應用程式部署過程中，將資料庫或變更部署至資料庫

- [在 Visual Studio 中設定資料庫部署](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment)（MSDN）。 概述使用 Web 專案部署資料庫的選項。
- [使用 Visual Studio 的 ASP.NET Web 部署](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)。 12部分教學課程系列，使用 dbDacFx 提供者和 Entity Framework Code First 移轉顯示資料庫部署。
- [如何：在 Visual Studio （MSDN）中使用單鍵發佈來部署 Web 專案](https://msdn.microsoft.com/library/dd465337.aspx)。
- 將[具有成員資格、OAuth 和 SQL Database 的 Secure ASP.NET MVC 5 應用程式部署到 Windows Azure 網站](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 這個長的教學課程會建立及部署應用程式，以針對成員資格和應用程式資料使用單一 SQL Server 資料庫。
- [使用 Visual Studio 部署具有 SQL Server Compact 的 ASP.NET Web 應用程式](../web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md)。 12部分教學課程系列會示範如何部署 SQL Server Compact 資料庫，以及如何從 SQL Server Compact 遷移至 SQL Server 的完整版本。

另請參閱本頁先前的使用持續整合（CI）程式來建立和安裝 web 部署封裝和部署 web 應用程式，以部署 web 應用程式。

<a id="databaseseparate"></a>

## <a name="deploying-a-database-separately-from-web-application-deployment"></a>將資料庫與 web 應用程式部署分開部署

- [SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx) （MSDN）。
- [包含 SQL Server 資料庫專案中的資料](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx)（SQL Server Data Tools team blog）。 部署資料庫時，如何部署架構和資料。
- [如何將資料庫部署至 Windows Azure](https://docs.microsoft.com/azure/sql-database/sql-database-cloud-migrate) （Microsoft Azure 網站）
- [將資料庫移轉至 Windows Azure SQL Database （先前稱為 SQL Azure）](https://msdn.microsoft.com/library/windowsazure/ee730904.aspx) （MSDN）。
- 使用 SSDT （SQL Server Data Tools team blog）[將資料庫移轉至 SQL Azure](https://blogs.msdn.com/b/ssdt/archive/2012/04/19/migrating-a-database-to-sql-azure-using-ssdt.aspx) 。
- [將以資料為中心的應用程式遷移至 Windows Azure](https://msdn.microsoft.com/library/jj156154.aspx) （MSDN）。
- [將 SQL Server 資料庫移轉至 Windows Azure SQL Database](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx) （MSDN）。

<a id="aspnetmembership"></a>

## <a name="deploying-a-web-application-that-uses-aspnet-application-services-such-as-membership-and-profiling"></a>部署使用 ASP.NET 應用程式服務（例如成員資格和分析）的 web 應用程式

- 將[具有成員資格、OAuth 和 SQL Database 的 Secure ASP.NET MVC 5 應用程式部署到 Windows Azure 網站](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 這個長的教學課程會建立及部署應用程式，以針對成員資格和應用程式資料使用單一 SQL Server 資料庫。
- [ASP.NET Identity](https://asp.net/identity/)。 ASP.NET Identity 的資源。
- [使用 Visual Studio 的 ASP.NET Web 部署](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)。 12部分教學課程系列說明如何部署 ASP.NET 成員資格資料庫。
- 設定[使用應用程式服務的網站](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-cs.md)。 適用于網站專案，但也與 web 應用程式專案有關。
- [生產網站上的使用者和角色](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs.md)。 適用于網站專案，但也與 web 應用程式專案有關。

<a id="precompiling"></a>

## <a name="precompiling-for-deployment"></a>用於部署的先行編譯

- [ASP.NET Web 應用程式專案先行編譯總覽](https://msdn.microsoft.com/library/aa983464.aspx)（MSDN）。
- [[封裝/發行 Web] 索引標籤，專案屬性](https://msdn.microsoft.com/library/dd410108.aspx)（MSDN）。
- [ [Advanced 先行編譯設定] 對話方塊](https://msdn.microsoft.com/library/hh475319.aspx)（MSDN）。

<a id="intranet"></a>

## <a name="deploying-an-intranet-web-application"></a>部署內部網路 web 應用程式

- 在 Visual Studio 2013 （Blog by Vittorio Bertocci）[中使用內部部署組織驗證選項（ADFS）搭配 ASP.NET](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/) 。
- [如何使用 ASP.NET MVC 建立內部網路網站](https://msdn.microsoft.com/library/gg703322(VS.98).aspx)（MSDN）。 Visual Studio 2010 的舊版逐步解說寫入不會反映 Visual Studio 2013 中引進之內部網路專案範本的主要變更。

<a id="automating"></a>

## <a name="automating-common-deployment-tasks-that-are-not-automated-out-of-the-box"></a>自動化未自動推出的一般部署工作

- [使用 Visual Studio ASP.NET Web 部署：部署額外](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files.md)的檔案。
- [在 Web Publish 上設定資料夾許可權](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx)（Sayed Hashimi 的 blog）。
- [如何擴充目標檔案以包含 Web 專案封裝的登錄設定](https://blogs.msdn.com/webdevtools/archive/2010/02/09/how-to-extend-target-file-to-include-registry-settings-for-web-project-package.aspx)（Web 開發工具 blog）。
- [擴充 XML （web.config）轉換](http://sedodream.com/2010/09/09/ExtendingXMLWebconfigConfigTransformation.aspx)（Sayed Hashimi 的 blog）。 說明如何建立自訂 XDT 轉換。
- [Web Deployment Tool （msdeploy.exe）自訂提供者需要 1](http://sedodream.com/2010/03/11/WebDeploymentToolMSDeployCustomProviderTake1.aspx) （Sayed Hashimi 的 blog）。 說明如何建立 Web Deploy 自訂提供者。
- [如何封裝和部署 COM 元件](https://blogs.msdn.com/webdevtools/archive/2010/03/03/how-to-package-and-deploy-com-component.aspx)（Web 開發工具 blog）。
- [如何封裝 .net 元件](https://blogs.msdn.com/webdevtools/archive/2010/02/19/how-to-package-com-component.aspx)（Web 開發工具 blog）。 如何將元件部署至 GAC。
- [編寫所有專案的腳本-使用 IIS、Web Deploy 和其他東西（Tugberk Ugurlu 的 blog）為您的 Web 服務器初始化您的 Windows AZURE VM](http://www.tugberkugurlu.com/archive/script-out-everything-initialize-your-windows-azure-vm-for-your-web-server-with-iis-web-deploy-and-other-stuff) 。

<a id="configuringservers"></a>

## <a name="configuring-web-servers-so-that-developers-can-deploy-web-applications-to-them-using-web-deploy"></a>設定網頁伺服器，讓開發人員可以使用 Web Deploy 來部署 web 應用程式

- [安裝和設定系統管理員和非系統管理員部署的 Web Deploy](https://www.iis.net/learn/install/installing-publishing-technologies/installing-and-configuring-web-deploy) （IIS.net 網站）。

<a id="hostingprovider"></a>

## <a name="configuring-servers-for-a-hosting-provider"></a>設定主控提供者的伺服器

- [Microsoft ASP.NET 4 裝載部署指南](https://go.microsoft.com/fwlink/?LinkId=191365)（Microsoft 下載中心）。
- [產生設定檔 XML 檔案](https://www.iis.net/learn/web-hosting/joining-the-web-hosting-gallery/generate-a-profile-xml-file)（IIS.net 網站）。

<a id="troubleshooting"></a>

## <a name="troubleshooting-deployment-problems"></a>針對部署問題進行疑難排解

- Visual Studio （Microsoft Azure 網站）[中的 Windows Azure 網站疑難排解](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)。
- [使用 Visual Studio ASP.NET Web 部署：疑難排解](../web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting.md)。
- 針對[Web Deploy 常見問題進行疑難排解](https://www.iis.net/learn/publish/troubleshooting-web-deploy/troubleshooting-common-problems-with-web-deploy)。
- [Web Deploy 錯誤碼](https://www.iis.net/learn/publish/troubleshooting-web-deploy/web-deploy-error-codes)（IIS.net 網站）。
- [Visual Studio 和 ASP.NET 的 Web 部署常見問題](https://msdn.microsoft.com/library/ee942158.aspx)（MSDN）。
- [IIS 與 ASP.NET 程式開發伺服器之間的核心差異](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md)。
- [開發與生產環境間的常見設定差異](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-cs.md)。
- [以中型信任裝載 ASP.NET 應用程式](http://www.4guysfromrolla.com/articles/100307-1.aspx)（來自 Rolla 網站的4人）。

<a id="gettinghelp"></a>

## <a name="getting-help-with-a-specific-deployment-question"></a>取得特定部署問題的協助

- [ASP.NET 設定及部署論壇](https://forums.asp.net/26.aspx/1?Configuration and Deployment)。
- [StackOverflow.com](http://www.StackOverflow.com)。

<a id="additional"></a>

## <a name="additional-resources"></a>其他資源

本節提供其他資源的連結，可説明您深入瞭解如何使用 Visual Studio 和 IIS 部署工具。

下列 blog 經常包含 Visual Studio web 部署的相關資訊：

- [Microsoft blog 的 Web 開發工具](https://blogs.msdn.com/b/webdevtools/)。
- [Sayed Hashimi 的 blog](http://www.sedodream.com/)。

下列資源提供 Web Deploy 的相關檔，Visual Studio 用來執行 Web 應用程式專案部署工作的 IIS 架構。 您可以在 IIS.net 網站上的[Web 部署工具論壇](https://go.microsoft.com/fwlink/?LinkId=149411)中詢問有關 Web Deploy 的問題。

- [Web Deploy 簡介](https://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy)。
- [安裝和設定 Web Deploy](https://www.iis.net/learn/install/installing-publishing-technologies/installing-and-configuring-web-deploy)。
- [用於自動化 Web Deploy 安裝程式的 PowerShell 腳本](https://www.iis.net/learn/publish/using-web-deploy/powershell-scripts-for-automating-web-deploy-setup)。
- [Web 部署工具](https://go.microsoft.com/fwlink/?LinkId=151481)。 TechNet 網站上 Web Deploy 檔的最上層目錄節點。 包含有用的參考資訊，但大部分的 TechNet 頁面尚未更新數年。
- [Microsoft Web.config 命名空間](https://go.microsoft.com/fwlink/?LinkId=148630)。 自1.0 版起，API 檔集尚未更新。
- [Microsoft Web Deployment Team blog](https://blogs.iis.net/msdeploy/default.aspx)。
- [IIS.net 網站中的 [發佈]](https://www.iis.net/learn/publish)索引標籤。
