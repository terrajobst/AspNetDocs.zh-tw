---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12
title: 使用 Visual Studio 或 Visual Web Developer 的 SQL Server Compact 部署 ASP.NET Web 應用程式： Web.config 檔案轉換-12 之 3 |Microsoft Docs
author: tdykstra
description: 這一系列的教學課程會示範如何使用 Visual Stu 部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案 。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 2b0df3d9-450b-4ea6-b315-4c9650722cad
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12
msc.type: authoredcontent
ms.openlocfilehash: fe71e6cfb0f4c5f1d99b326e9d90edb6c8c5feee
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600502"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-webconfig-file-transformations---3-of-12"></a>使用 Visual Studio 或 Visual Web Developer 的 SQL Server Compact 部署 ASP.NET Web 應用程式： Web.config 檔案轉換-12 的3

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載入門專案](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 這一系列的教學課程會示範如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，來部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案。 如果您安裝 Web 發佈更新，也可以使用 Visual Studio 2010。 如需此系列的簡介，請參閱[本系列的第一個教學](deployment-to-a-hosting-provider-introduction-1-of-12.md)課程。
> 
> 如需示範在 Visual Studio 2012 的 RC 版本後引進部署功能的教學課程，說明如何部署 SQL Server Compact 以外的 SQL Server 版本，並示範如何部署到 Azure App Service Web Apps，請參閱[使用 Visual Studio ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。

## <a name="overview"></a>概觀

本教學課程會示範如何在您*將 web.config 檔案*部署到不同的目的地環境時，自動化該檔案的變更程式。 大部分的應用程式都有*web.config*檔案中的設定，在部署應用程式時必須不同。 將進行這些變更的程式自動化，讓您不必在每次部署時都必須手動執行，這會很繁瑣且容易出錯。

提醒：如果您在進行本教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解][頁面](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>Web.config 轉換與 Web Deploy 參數的比較

有兩種方式可將變更*web.config*檔案設定的程式自動化： [web.config 轉換](https://msdn.microsoft.com/library/dd465326.aspx)和[Web Deploy 參數](https://msdn.microsoft.com/library/ff398068.aspx)。 Web.config*轉換檔案*包含 XML 標記，可指定在部署 web.config 檔案時，如何*變更 web.config 檔案*。 您可以針對特定的組建設定和特定的發行設定檔，指定不同的變更。 預設組建設定為 [Debug] 和 [Release]，而您可以建立自訂群組建設定。 發行設定檔通常會對應至目的地環境。 （您將在[部署至 IIS 作為測試環境](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)教學課程中深入瞭解發行設定檔）。

Web Deploy 參數可以用來指定在部署期間必須設定的許多不同類型的設定，*包括在 web.config*檔案中找到的設定。 當用來指定*web.config*檔案變更時，Web Deploy 參數會更複雜，但當您在部署之前不知道要設定的值時，它們會很有用。 例如，在企業環境中，您可能會建立*部署套件*，並將其提供給 it 部門中的人員，以在實際執行環境中安裝，而且該人員必須能夠輸入不知道的連接字串或密碼。

在本教學課程涵蓋的案例中，您知道必須*對 web.config 檔案*進行的所有作業，因此您不需要使用 Web Deploy 參數。 您將會根據所使用的組建設定進行一些不同的轉換，並根據使用的發行設定檔而有所不同。

## <a name="creating-transformation-files-for-publish-profiles"></a>建立發行設定檔的轉換檔案

在**方案總管**中，*展開 [web.config]* 以查看預設為兩個預設組建*設定所建立的 web.config 和 web.config* *轉換檔案。*

![Web. config_transform_files](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image1.png)

您可以用滑鼠右鍵按一下 Web.config 檔案，然後從內容功能表選擇 [**新增設定轉換**]，來建立自訂群組建設定的轉換檔案，但在本教學課程中，您不需要這麼做。

您需要兩個更多的轉換檔案，以設定與部署目的地相關的變更，而不是設定為組建設定。 這種設定的典型範例是測試與生產環境不同的 WCF 端點。 在稍後的教學課程中，您將建立名為 Test 和生產的發行設定檔，因此您需要一個*web.config*檔案*和一個 web.config*檔案。

必須以手動方式建立系結至發行設定檔的轉換檔案。 在**方案總管**中，以滑鼠右鍵按一下 ContosoUniversity 專案，然後選取 [**在 Windows Explorer 中開啟資料夾**]。

![Open_folder_in_Windows_Explorer](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image2.png)

在**Windows Explorer**中，選取*web.config*檔案、複製檔案，然後貼上兩個複本。 將這些複本重新命名為*web.config* *和 web.config，然後*關閉**Windows Explorer**。

在**方案總管**中，**按一下 [** 重新整理] 以查看新的檔案。

選取新的檔案，按一下滑鼠右鍵，然後在內容功能表中按一下 [**包含在專案中**]。

![在專案中包含測試和生產設定檔案](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image3.png)

若要避免部署這些檔案，請在**方案總管**中選取這些檔案，然後在 [**屬性**] 視窗中，將 [**組建動作**] 屬性從 [**內容**] 變更為 [**無**]。 （以組建設定為基礎的轉換檔案會自動防止部署）。

您現在已準備好在*web.config 轉換檔案中輸入*web.config*轉換。*

## <a name="limiting-error-log-access-to-administrators"></a>限制系統管理員的錯誤記錄檔存取

如果應用程式執行時發生錯誤，應用程式會顯示一般錯誤頁面來取代系統產生的錯誤頁面，並使用[Elmah NuGet 封裝](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)來進行錯誤記錄和報告。 *Web.config 檔案*中的 `customErrors` 元素會指定錯誤頁面：

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample1.xml)]

若要查看錯誤頁面，請暫時將 `customErrors` 元素的 `mode` 屬性從 "RemoteOnly" 變更為 "On"，然後從 Visual Studio 執行應用程式。 藉由要求不正確 URL （例如*Studentsxxx*）導致錯誤。 您會看到 [ *GenericErrorPage* ] 頁面，而不是 IIS 產生的「找不到網頁」錯誤頁面。

[![Error_page](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image5.png)](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image4.png)

若要查看錯誤記錄檔，請將 URL 中的所有內容取代為*elmah. axd* （如螢幕擷取畫面中的範例，`http://localhost:51130/elmah.axd`），然後按 enter 鍵：

[![Elmah_log_page](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image7.png)](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image6.png)

當您完成時，別忘了將 `customErrors` 元素設回 "RemoteOnly" 模式。

在您的開發電腦上，允許免費存取錯誤記錄檔頁面，但在生產環境中會有安全性風險。 針對生產網站，您可以在*web.config*檔案中設定轉換，藉此新增授權規則，以限制只有系統管理員才能存取錯誤記錄檔。

開啟*web.config，並*在開啟的 `configuration` 標記之後加入新的 `location` 元素，如下所示。 （請確定您僅新增 [`location`] 專案，而不只是為了提供一些內容而顯示的周圍標記。）

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample2.xml?highlight=2-9)]

"Insert" 的 `Transform` 屬性值會導致此 `location` 元素當做*web.config*檔案中任何現有 `location` 元素的同級加入。 （已有一個 `location` 元素指定 [**更新信用額度**] 頁面的授權規則）。當您在部署後測試生產網站時，您會進行測試以確認此授權規則有效。

您不需要在測試環境中限制錯誤記錄檔存取，因此不需要將此程式碼加入至*web.config*檔案。

> [!NOTE] 
> 
> **安全性注意事項**絕對不要在實際執行應用程式中顯示公用的錯誤詳細資料，或將該資訊儲存在公用位置。 攻擊者可以使用錯誤資訊來探索網站中的弱點。 如果您在自己的應用程式中使用 ELMAH，請務必調查可設定 ELMAH 以將安全性風險降至最低的方式。 本教學課程中的 ELMAH 範例不應視為建議的設定。 這是為了說明如何處理應用程式必須能夠在中建立檔案的資料夾，所選擇的範例。

## <a name="setting-an-environment-indicator"></a>設定環境指標

常見的案例是在您部署的每個環境中，都必須有不同的*web.config*檔案設定。 例如，呼叫 WCF 服務的應用程式在測試和生產環境中可能需要不同的端點。 Contoso 大學應用程式也包含此類型的設定。 此設定會控制網站頁面上的可見指標，告訴您您所在的環境（例如開發、測試或生產）。 設定值會決定應用程式是否要將 "（Dev）" 或 "（Test）" 附加至*網站*主版頁面中的主要標題：

[![Environment_indicator](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image9.png)](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image8.png)

當應用程式在生產環境中執行時，會省略環境指示器。

Contoso 大學網頁會讀取*web.config*檔案 `appSettings` 中設定的值，以判斷應用程式執行所在的環境：

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample3.xml)]

在測試環境中，此值應為「測試」，而在生產環境中則為「生產」。

開啟*web.config，並在*您稍早新增的 `location` 元素的開頭標記前面加入 `appSettings` 元素：

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample4.xml)]

`xdt:Transform` 屬性值 "SetAttributes" 表示此轉換的目的是要變更*web.config*檔案中現有元素的屬性值。 `xdt:Locator` 屬性值 "Match （key）" 表示要修改的專案是其 `key` 屬性符合這裡指定之 `key` 屬性的元素。 `add` 專案的唯一另一個屬性是 `value`，這就是在已部署的*web.config*檔案中將會變更的專案。 此程式碼會在部署至生產*環境的 web.config*檔案中，將 `Environment` `appSettings` 元素的 `value` 屬性設定為「生產」。

接下來，將相同的變更套用至*web.config*檔案，但將 `value` 設定為 "test"，而不是 [生產]。 當您完成時，web.config 中的 `appSettings` 區段看*起來會像*下列範例：

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample5.xml)]

## <a name="disabling-debug-mode"></a>停用 Debug 模式

針對發行組建，不論您要部署到哪個環境，都不想啟用「偵測」。 根據預設，會使用從 `compilation` 元素移除 `debug` 屬性的程式碼自動建立*web.config 轉換檔案*：

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample6.xml)]

當您部署發行組建時，`Transform` 屬性會導致已部署的*web.config*檔案中省略 `debug` 屬性。

這個相同的轉換是在測試和實際執行的轉換檔案中，因為您會藉由複製發行轉換檔案來建立它們。 您不需要在該處重複此專案，因此請開啟每個檔案，移除**編譯**元素，然後儲存並關閉每個檔案。

## <a name="setting-connection-strings"></a>設定連接字串

在大部分情況下，您不需要設定連接字串轉換，因為您可以在發行設定檔中指定連接字串。 但是當您部署 SQL Server Compact 資料庫，而且使用 Entity Framework Code First 移轉更新目的地伺服器上的資料庫時，就會發生例外狀況。 在此情況下，您必須指定要在伺服器上用來更新資料庫架構的其他連接字串。 若要設定此轉換，請在*web.config*和*web.config 轉換檔案*中的開啟 **&lt;設定&gt;** 標記之後，立即加入 **&lt;connectionStrings&gt;** 元素：

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample7.xml)]

`Transform` 屬性指定此連接字串將會加入至已部署的*web.config*檔案中的*connectionStrings*元素。 （如果發行程式不存在，則會自動為您建立這個額外的連接字串，但根據預設， **providerName**屬性會設定為 `System.Data.SqlClient`，這不適用 SQL Server Compact。 藉由手動新增連接字串，您可以讓部署程式不會建立具有錯誤提供者名稱的連接字串元素）。

您現在已指定部署 Contoso 大學應用程式來測試和生產所需的所有*web.config*轉換。 在下列教學課程中，您將會負責需要設定專案屬性的部署設定工作。

## <a name="more-information"></a>更多資訊

如需本教學課程涵蓋之主題的詳細資訊，請參閱[ASP.NET 部署內容對應](https://msdn.microsoft.com/library/bb386521.aspx)中的 web.config 轉換案例。

> [!div class="step-by-step"]
> [上一頁](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)
> [下一頁](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)
