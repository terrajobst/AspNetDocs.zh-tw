---
uid: web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
title: 使用 Visual Studio： web.config 檔案轉換來 ASP.NET Web 部署 |Microsoft Docs
author: tdykstra
description: 本教學課程系列將示範如何透過互動，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商主機服務提供者。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 5a2a927b-14cb-40bc-867a-f0680f9febd7
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
msc.type: authoredcontent
ms.openlocfilehash: a9d39547c94a63003442ba6fe1257693dde24b05
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621781"
---
# <a name="aspnet-web-deployment-using-visual-studio-webconfig-file-transformations"></a>使用 Visual Studio： web.config 檔案轉換來 ASP.NET Web 部署

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載入門專案](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本教學課程系列說明如何使用 Visual Studio 2012 或 Visual Studio 2010，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商裝載提供者。 如需有關數列的詳細資訊，請參閱[本系列的第一個教學](introduction.md)課程。

## <a name="overview"></a>概觀

本教學課程會示範如何在您*將 web.config 檔案*部署到不同的目的地環境時，自動化該檔案的變更程式。 大部分的應用程式都有*web.config*檔案中的設定，在部署應用程式時必須不同。 將進行這些變更的程式自動化，讓您不必在每次部署時都必須手動執行，這會很繁瑣且容易出錯。

提醒：如果您在進行本教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解][頁面](troubleshooting.md)。

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>Web.config 轉換與 Web Deploy 參數的比較

有兩種方式可將變更*web.config*檔案設定的程式自動化： [web.config 轉換](https://msdn.microsoft.com/library/dd465326.aspx)和[Web Deploy 參數](https://msdn.microsoft.com/library/ff398068.aspx)。 Web.config*轉換檔案*包含 XML 標記，可指定在部署 web.config 檔案時，如何*變更 web.config 檔案*。 您可以針對特定的組建設定和特定的發行設定檔，指定不同的變更。 預設組建設定為 [Debug] 和 [Release]，而您可以建立自訂群組建設定。 發行設定檔通常會對應至目的地環境。 （您將在[部署至 IIS 作為測試環境](deploying-to-iis.md)教學課程中深入瞭解發行設定檔）。

Web Deploy 參數可以用來指定在部署期間必須設定的許多不同類型的設定，*包括在 web.config*檔案中找到的設定。 當用來指定*web.config*檔案變更時，Web Deploy 參數會更複雜，但當您在部署之前不知道要設定的值時，它們會很有用。 例如，在企業環境中，您可能會建立*部署套件*，並將其提供給 it 部門中的人員，以在實際執行環境中安裝，而且該人員必須能夠輸入不知道的連接字串或密碼。

在本教學課程系列涵蓋的案例中，您事先知道必須*對 web.config 檔案*進行的所有作業，因此您不需要使用 Web Deploy 參數。 您將會根據所使用的組建設定進行一些不同的轉換，並根據使用的發行設定檔而有所不同。

<a id="watransforms"></a>

## <a name="specifying-webconfig-settings-in-azure"></a>在 Azure 中指定 Web.config 設定

如果您想要變更的*web.config*檔案設定是在 `<connectionStrings>` 或 `<appSettings>` 元素中，而且如果您要部署到 Azure App Service 中的 Web Apps，您可以選擇在部署期間自動化變更的另一個選項。 您可以在 web 應用程式的管理入口網站頁面的 [**設定**] 索引標籤中，輸入您想要在 Azure 中生效的設定（向下流覽至 [**應用程式設定**] 和 [**連接字串**] 區段）。 當您部署專案時，Azure 會自動套用變更。 如需詳細資訊，請參閱[Windows Azure 網站：應用程式字串和連接字串的運作方式](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)。

## <a name="default-transformation-files"></a>預設轉換檔案

在**方案總管**中，*展開 [web.config]* 以查看預設為兩個預設組建*設定所建立的 web.config 和 web.config* *轉換檔案。*

![Web. config_transform_files](web-config-transformations/_static/image1.png)

您可以用滑鼠右鍵按一下 Web.config 檔案，然後從內容功能表選擇 [**新增設定轉換**]，來建立自訂群組建設定的轉換檔案。 在本教學課程中，您不需要這麼做，而且功能表選項會停用，因為您尚未建立任何自訂群組建設定。

稍後您將會建立三個更多的轉換檔案，分別用於測試、預備和生產發行設定檔。 您會在發行設定檔轉換檔案中處理的一般設定範例，因為它相依于目的地環境，是測試與實際執行的不同 WCF 端點。 建立發行設定檔之後，您將在稍後的教學課程中建立發佈設定檔轉換檔案。

## <a name="disable-debug-mode"></a>停用 debug 模式

`debug` 屬性是相依于組建設定而非目的地環境之設定的範例。 針對發行組建，您通常會想要停用此功能，而不論您要部署到哪個環境。 因此，Visual Studio 專案範本預設會以從 `compilation` 專案移除 `debug` 屬性的程式碼，建立*web.config*轉換檔案。 以下是預設的*web.config*：除了批註化的一些範例轉換程式碼之外，它還會在移除 `debug` 屬性的 `compilation` 元素中包含程式碼：

[!code-xml[Main](web-config-transformations/samples/sample1.xml?highlight=18)]

`xdt:Transform="RemoveAttributes(debug)"` 屬性指定您想要從已部署的*web.config*檔案中的 `system.web/compilation` 元素移除 `debug` 屬性。 這會在您每次部署發行組建時完成。

## <a name="limit-error-log-access-to-administrators"></a>限制系統管理員的錯誤記錄檔存取

如果應用程式執行時發生錯誤，應用程式會顯示一般錯誤頁面來取代系統產生的錯誤頁面，並使用[Elmah NuGet 封裝](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)來進行錯誤記錄和報告。 應用程式*web.config*檔案中的 `customErrors` 元素會指定錯誤頁面：

[!code-xml[Main](web-config-transformations/samples/sample2.xml)]

若要查看錯誤頁面，請暫時將 `customErrors` 元素的 `mode` 屬性從 "RemoteOnly" 變更為 "On"，然後從 Visual Studio 執行應用程式。 藉由要求不正確 URL （例如*Studentsxxx*）導致錯誤。 您會看到 [ *GenericErrorPage* ] 頁面，而不是 IIS 產生的「找不到資源」錯誤頁面。

![錯誤頁面](web-config-transformations/_static/image2.png)

若要查看錯誤記錄檔，請將 URL 中的所有內容取代為*elmah. axd* （例如 `http://localhost:51130/elmah.axd`），然後按 enter 鍵：

![ELMAH 頁面](web-config-transformations/_static/image3.png)

當您完成時，別忘了將 `customErrors` 元素設回 "RemoteOnly" 模式。

在您的開發電腦上，允許免費存取錯誤記錄檔頁面，但在生產環境中會有安全性風險。 針對生產網站，您想要新增授權規則來限制系統管理員的錯誤記錄檔存取，並確保限制也能在測試和接移時使用。 因此，這是您每次部署發行組建時要執行的另一項變更，因此屬於*web.config*檔案。

開啟*web.config，並*在結尾 `configuration` 標記前面加入新的 `location` 元素，如下所示。

[!code-xml[Main](web-config-transformations/samples/sample3.xml?highlight=27-34)]

"Insert" 的 `Transform` 屬性值會導致此 `location` 元素當做*web.config*檔案中任何現有 `location` 元素的同級加入。 （已有一個 `location` 元素指定 [**更新信用額度**] 頁面的授權規則）。

現在您可以預覽轉換，以確保正確編碼。

在**方案總管**中，以滑鼠右鍵按一下 [ *web.config* ]，然後按一下 [**預覽轉換**]。

![預覽轉換功能表](web-config-transformations/_static/image4.png)

隨即開啟一個頁面，其中會顯示左側的開發 web.config 檔案，以及已醒目提示已*部署* *的 web.config 檔案*在右邊的樣子。

![Debug 轉換的預覽](web-config-transformations/_static/image5.png)

![位置轉換預覽](web-config-transformations/_static/image6.png)

（在預覽版中，您可能會注意到您未寫入轉換的一些其他變更：這些變更通常包含移除不影響功能的空白字元）。

當您在部署後測試網站時，您也會進行測試以確認授權規則有效。

> [!NOTE] 
> 
> **安全性注意事項**絕對不要在實際執行應用程式中顯示公用的錯誤詳細資料，或將該資訊儲存在公用位置。 攻擊者可以使用錯誤資訊來探索網站中的弱點。 如果您在自己的應用程式中使用 ELMAH，請設定 ELMAH 以將安全性風險降至最低。 本教學課程中的 ELMAH 範例不應視為建議的設定。 這是為了說明如何處理應用程式必須能夠在中建立檔案的資料夾，所選擇的範例。 如需詳細資訊，請參閱[保護 ELMAH 端點](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)。

## <a name="a-setting-that-youll-handle-in-publish-profile-transformation-files"></a>您將在發行設定檔轉換檔案中處理的設定

常見的案例是在您部署的每個環境中，都必須有不同的*web.config*檔案設定。 例如，呼叫 WCF 服務的應用程式在測試和生產環境中可能需要不同的端點。 Contoso 大學應用程式也包含此類型的設定。 此設定會控制網站頁面上的可見指標，告訴您您所在的環境（例如開發、測試或生產）。 設定值會決定應用程式是否要將 "（Dev）" 或 "（Test）" 附加至*網站*主版頁面中的主要標題：

![環境指標](web-config-transformations/_static/image7.png)

當應用程式在預備或生產環境中執行時，會省略環境指示器。

Contoso 大學網頁會讀取*web.config*檔案 `appSettings` 中設定的值，以判斷應用程式執行所在的環境：

[!code-xml[Main](web-config-transformations/samples/sample4.xml)]

測試環境中的值應該是「測試」，而「生產」則是用於預備與生產。

轉換檔案中的下列程式碼將會執行此轉換：

[!code-xml[Main](web-config-transformations/samples/sample5.xml)]

`xdt:Transform` 屬性值 "SetAttributes" 表示此轉換的目的是要變更*web.config*檔案中現有元素的屬性值。 `xdt:Locator` 屬性值 "Match （key）" 表示要修改的專案是其 `key` 屬性符合這裡指定之 `key` 屬性的元素。 `add` 專案的唯一另一個屬性是 `value`，這就是在已部署的*web.config*檔案中將會變更的專案。 此處顯示的程式碼會在*部署的 web.config*檔案中，將 `Environment` `appSettings` 元素的 `value` 屬性設定為 "Test"。

這項轉換屬於尚未建立的發行設定檔轉換檔案。 當您建立測試、預備和生產環境的發行設定檔時，您將會建立並更新執行這種變更的轉換檔案。 您會在[部署至 IIS](deploying-to-iis.md)和[部署至生產](deploying-to-production.md)教學課程中執行此動作。

> [!NOTE]
> 因為此設定是在 `<appSettings>` 元素中，所以當您部署至中的 Web Apps 時，您可以使用另一個替代方式來指定轉換 Azure App Service 請參閱本主題稍早在[Azure 中指定 web.config 設定](#watransforms)。

## <a name="setting-connection-strings"></a>設定連接字串

雖然預設的轉換檔案包含示範如何更新連接字串的範例，但在大多數情況下，您不需要設定連接字串轉換，因為您可以在發行設定檔中指定連接字串。 您會在[部署至 IIS](deploying-to-iis.md)和[部署至生產](deploying-to-production.md)教學課程中執行此動作。

## <a name="summary"></a>總結

在建立發行設定檔之前，您已完成*與 web.config 轉換相同*的作業，而且您已瞭解已部署的 web.config 檔案中會有哪些內容的預覽。

![位置轉換預覽](web-config-transformations/_static/image8.png)

在下列教學課程中，您將會負責需要設定專案屬性的部署設定工作。

## <a name="more-information"></a>更多資訊

如需本教學課程涵蓋之主題的詳細資訊，請參閱在 Visual Studio 和 ASP.NET 的 Web 部署內容對應中[部署期間，使用 web.config 轉換來變更目的地 web.config 檔案或 app.config 檔案中的設定](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms)。

> [!div class="step-by-step"]
> [上一頁](preparing-databases.md)
> [下一頁](project-properties.md)
