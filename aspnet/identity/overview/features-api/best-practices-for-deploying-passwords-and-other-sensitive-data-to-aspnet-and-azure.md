---
uid: identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure
title: 將密碼和其他機密資料部署至 ASP.NET 和 Azure App Service-ASP.NET 4。x
author: Rick-Anderson
description: 本教學課程會示範您的程式碼如何安全地儲存和存取安全資訊。 最重要的一點是，您絕對不應該儲存密碼或其他 sen 。
ms.author: riande
ms.date: 05/21/2015
ms.assetid: 97902c66-cb61-4d11-be52-73f962f2db0a
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure
msc.type: authoredcontent
ms.openlocfilehash: 8356a90611f791779cc4ff4730038d82cd76242f
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457046"
---
# <a name="best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure-app-service"></a>將密碼和其他敏感性資料部署到 ASP.NET 和 Azure App Service 的最佳做法

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教學課程會示範您的程式碼如何安全地儲存和存取安全資訊。 最重要的一點是，您絕對不應該將密碼或其他敏感性資料儲存在原始程式碼中，而且您不應該在開發和測試模式中使用生產秘密。
> 
> 範例程式碼是簡單的 WebJob 主控台應用程式，以及需要存取資料庫連接字串 password、Twilio、Google 及 SendGrid 安全金鑰的 ASP.NET MVC 應用程式。
> 
> 同時也會提及內部部署設定和 PHP。

- [在開發環境中使用密碼](#pwd)
- [在開發環境中使用連接字串](#con)
- [Webjob 主控台應用程式](#wj)
- [將秘密部署至 Azure](#da)
- [內部部署和 PHP 的注意事項](#not)
- [其他資源](#addRes)

<a id="pwd"></a>
## <a name="working-with-passwords-in-the-development-environment"></a>在開發環境中使用密碼

教學課程經常會在原始程式碼中顯示敏感性資料，希望您必須注意，您絕對不應該在原始程式碼中儲存機密資料。 例如，[使用 SMS 和電子郵件2FA 的 ASP.NET MVC 5 應用程式](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)教學課程會在*web.config*檔案中顯示下列內容：

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample1.xml)]

Web.config*檔案*是原始碼，因此這些秘密永遠不會儲存在該檔案中。 幸運的是，`<appSettings>` 元素具有 `file` 屬性，可讓您指定包含敏感性應用程式設定的外部檔案。 只要外部檔案未簽入您的來源樹狀結構，您就可以將所有的秘密移至外部檔案。 例如，在下列標記中， *AppSettingsSecrets*檔案包含所有的應用程式秘密：

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample2.xml)]

外部檔案中的標記（在此範例中為*AppSettingsSecrets* ）是*在 web.config 檔案*中找到的相同標記：

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample3.xml)]

ASP.NET 執行時間會將外部檔案的內容與 &lt;appSettings&gt; 元素中的標記合併。 如果找不到指定的檔案，則執行階段會略過檔案屬性。

> [!WARNING]
> 安全性-請勿將您的*秘密 .config*檔案新增至您的專案，或將它簽入原始檔控制。 根據預設，Visual Studio 會將 `Build Action` 設定為 `Content`，這表示已部署檔案。 如需詳細資訊，請參閱[為什麼我的專案資料夾中的所有檔案都不會被部署？](https://msdn.microsoft.com/library/ee942158(v=vs.110).aspx#can_i_exclude_specific_files_or_folders_from_deployment) 雖然您可以使用*秘密 .config*檔案的任何擴充功能，但最好是將它保留為 .config，因為 IIS 不會提供設定檔案 *。* 另請注意， *AppSettingsSecrets*檔案是*來自 web.config 檔案*的兩個目錄層級，因此完全不在方案目錄中。 藉由將檔案移出方案目錄，&quot;git 新增 \*&quot; 不會將它新增至您的存放庫。

<a id="con"></a>
## <a name="working-with-connection-strings-in-the-development-environment"></a>在開發環境中使用連接字串

Visual Studio 會建立使用[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)的新 ASP.NET 專案。 LocalDB 是專為開發環境所建立。 它不需要密碼，因此您不需要執行任何動作，即可防止秘密簽入您的原始程式碼。 某些開發小組會使用需要密碼的 SQL Server （或其他 DBMS）的完整版本。

您可以使用 `configSource` 屬性來取代整個 `<connectionStrings>` 標記。 不同于合併標記的 `<appSettings>` `file` 屬性，`configSource` 屬性會取代標記。 下列標記顯示*web.config*檔案中的 `configSource` 屬性：

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample4.xml?highlight=1)]

> [!NOTE]
> 如果您使用如上所示的 `configSource` 屬性將連接字串移到外部檔案，並讓 Visual Studio 建立新的網站，則無法偵測到您使用的是資料庫，而且當您從 Visual Studio 發佈至 Azure 時，將無法設定資料庫。 如果您使用 `configSource` 屬性，您可以使用 PowerShell 來建立及部署您的網站和資料庫，也可以在發佈之前，在入口網站中建立網站和資料庫。 [New-AzureWebsitewithDB](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3)腳本會建立新的網站和資料庫。

> [!WARNING]
> 安全性-與*AppSettingsSecrets*不同的是，外部連接字串檔案必須位於*與根 web.config*檔案相同的目錄中，因此您必須採取預防措施，以確保您不會將它簽入來源存放庫。

> [!NOTE]
> **秘密檔案的安全性警告：** 最佳做法是不要在測試和開發中使用生產秘密。 在測試或開發中使用生產環境密碼會洩漏這些秘密。

<a id="wj"></a>
## <a name="webjobs-console-apps"></a>Webjob 主控台應用程式

主控台應用程式所使用的*app.config*檔案不支援相對路徑，但它支援絕對路徑。 您可以使用絕對路徑，將您的秘密移出項目目錄。 下列標記會顯示*C:\secrets\AppSettingsSecrets.config*檔案中的秘密，以及*app.config*檔案中的非機密資料。

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample5.xml?highlight=2)]

<a id="da"></a>
## <a name="deploying-secrets-to-azure"></a>將秘密部署至 Azure

當您將 web 應用程式部署至 Azure 時，將不會部署*AppSettingsSecrets* （這就是您想要的）。 您可以移至[Azure 管理入口網站](https://azure.microsoft.com/services/management-portal/)並手動加以設定，以執行下列動作：

1. 移至[https://portal.azure.com](https://portal.azure.com)，然後使用您的 Azure 認證登入。
2. 按一下 **[流覽 &gt; Web Apps]** ，然後按一下您的 Web 應用程式名稱。
3. 按一下 [**所有設定] &gt; [應用程式設定**]。

**應用程式設定**和**連接字串**值會覆寫*web.config*檔案中的相同設定。 在我們的範例中，我們不會將這些設定部署至 Azure，但如果這些金鑰位於*web.config*檔案中，則入口網站上所顯示的設定會優先執行。

最佳做法是遵循[DevOps 的工作流程](../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything.md)，並使用[Azure PowerShell](https://azure.microsoft.com/documentation/articles/install-configure-powershell/) （或[Chef](http://www.opscode.com/chef/)或[Puppet](http://puppetlabs.com/puppet/what-is-puppet)等其他架構），在 Azure 中自動設定這些值。 下列 PowerShell 腳本會使用[CliXml](http://www.powershellcookbook.com/recipe/PukO/securely-store-credentials-on-disk) ，將加密的秘密匯出到磁片：

[!code-powershell[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample6.ps1)]

在上述腳本中，' Name ' 是秘密金鑰的名稱，例如 '&quot;FB\_AppSecret&quot; 或 "TwitterSecret"。 您可以在瀏覽器中，查看腳本所建立的 "credential" 檔案。 下列程式碼片段會測試每個認證檔案，並設定已命名 web 應用程式的秘密：

[!code-powershell[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample7.ps1)]

> [!WARNING]
> 安全性-不要在 PowerShell 腳本中包含密碼或其他秘密，這麼做會使使用 PowerShell 腳本來部署敏感性資料的目的失效。 [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) Cmdlet 提供安全的機制來取得密碼。 使用 UI 提示可能會導致密碼洩漏。

### <a name="deploying-db-connection-strings"></a>部署 DB 連接字串

DB 連接字串的處理方式類似于應用程式設定。 如果您從 Visual Studio 部署 web 應用程式，則會為您設定連接字串。 您可以在入口網站中確認這項功能。 設定連接字串的建議方式是使用 PowerShell。 如需 PowerShell 腳本的範例，請建立網站和資料庫，並在網站中設定連接字串，從[Azure 腳本程式庫](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure)下載[New-AzureWebsitewithDB](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) 。

<a id="not"></a>
## <a name="notes-for-php"></a>PHP 的相關注意事項

因為**應用程式設定**和**連接字串**的機碼值組會儲存在 Azure App Service 的環境變數中，所以使用任何 web 應用程式架構（例如 PHP）的開發人員可以輕鬆地取得這些值。 請參閱 Stefan Schackow 的[Windows Azure 網站：應用程式字串和連接字串如何運作](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)blog 文章，其中會顯示可讀取應用程式設定和連接字串的 PHP 程式碼片段。

## <a name="notes-for-on-premises-servers"></a>內部部署伺服器的注意事項

如果您要部署到內部部署 web 伺服器，您可以[加密設定檔的設定區段](https://msdn.microsoft.com/library/ff647398.aspx)，以協助保護秘密。 或者，您可以使用適用于 Azure 網站的相同方法： [保留設定檔中的開發設定]，並針對 [生產] 設定使用環境變數值。 不過，在此情況下，您必須撰寫應用程式程式碼，以取得 Azure 網站中自動的功能：從環境變數抓取設定，並使用這些值來取代設定檔案設定，或在下列情況使用設定檔設定找不到環境變數。

<a id="addRes"></a>
## <a name="additional-resources"></a>其他資源

如需建立 web 應用程式 + 資料庫的 PowerShell 腳本範例，設定連接字串 + 應用程式設定，請從[Azure 腳本程式庫](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure)下載[New-AzureWebsitewithDB。](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) 

請參閱 Stefan Schackow 的[Windows Azure 網站：應用程式字串與連接字串的運作方式](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)

特別感謝 Barry Dorrans （ [@blowdart](https://twitter.com/blowdart) ）和 Carlos Farre 進行審核。
