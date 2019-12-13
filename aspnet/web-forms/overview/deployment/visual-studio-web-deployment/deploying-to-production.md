---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
title: 使用 Visual Studio ASP.NET Web 部署：部署至生產環境 |Microsoft Docs
author: tdykstra
description: 本教學課程系列將示範如何透過互動，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商主機服務提供者。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 416438a1-3b2f-4d27-bf53-6b76223c33bf
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
msc.type: authoredcontent
ms.openlocfilehash: ddc3d15f0436c4c3a24491cf0377111768da67df
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74617635"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-to-production"></a>使用 Visual Studio ASP.NET Web 部署：部署到生產環境

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載入門專案](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本教學課程系列說明如何使用 Visual Studio 2012 或 Visual Studio 2010，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商裝載提供者。 如需有關數列的詳細資訊，請參閱[本系列的第一個教學](introduction.md)課程。

## <a name="overview"></a>總覽

在本教學課程中，您會設定 Microsoft Azure 帳戶、建立預備和生產環境，以及使用 Visual Studio 單鍵發佈功能，將您的 ASP.NET web 應用程式部署到預備和生產環境。

如果您想要的話，可以部署到協力廠商主機服務提供者。 本教學課程中所述的大部分程式都與主機服務提供者或 Azure 相同，不同之處在于每個提供者都有自己的帳戶和網站管理使用者介面。 您可以在 Microsoft.com 網站的提供者資源[庫](https://www.microsoft.com/web/hosting)中找到主控提供者。

一下如果您在進行本教學課程時收到錯誤訊息或無法使用，請務必查看本教學課程系列中的 [疑難排解] 頁面。

## <a name="get-a-microsoft-azure-account"></a>取得 Microsoft Azure 帳戶

如果您還沒有 Azure 帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資訊，請參閱[Azure 免費試用](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)。

## <a name="create-a-staging-environment"></a>建立預備環境

> [!NOTE]
> 由於本教學課程的撰寫，Azure App Service 新增了新功能，可將建立預備和生產環境的許多進程自動化。 請參閱[在 Azure App Service 中設定 web 應用程式的預備環境](https://azure.microsoft.com/documentation/articles/web-sites-staged-publishing/)。

如[部署至測試環境教學](deploying-to-iis.md)課程中所述，最可靠的測試環境是主控提供者的網站，就像生產網站一樣。 在許多主機服務提供者上，您必須將此項的優點視為額外的成本，但在 Azure 中，您可以建立額外的免費 web 應用程式做為您的預備應用程式。 您也需要資料庫，而超過生產資料庫費用的額外費用將會是 [無] 或 [最小]。 在 Azure 中，您需支付所使用的資料庫儲存體數量，而不是每個資料庫的費用，而您將在預備環境中使用的額外儲存體數量將會降到最低。

如[部署至測試環境教學](deploying-to-iis.md)課程中所述，在預備和生產階段中，您會將兩個資料庫部署到一個資料庫。 如果您想要將它們分開，則程式會相同，不同之處在于您會為每個環境建立額外的資料庫，而且您會在建立發行設定檔時，為每個資料庫選取正確的目的地字串。

在本教學課程的這一節中，您將建立用於預備環境的 web 應用程式和資料庫，而且您會在建立和部署至生產環境之前，先部署至預備和測試。

> [!NOTE]
> 下列步驟示範如何使用 Azure 管理入口網站，在 Azure App Service 中建立 web 應用程式。 在最新版本的 Azure SDK 中，您也可以使用伺服器總管來執行這項操作，而不需要離開 Visual Studio。 在 Visual Studio 2013 中，您也可以直接從 [發佈] 對話方塊建立 web 應用程式。 如需詳細資訊，請參閱[在 Azure App Service 中建立 ASP.NET web 應用程式。](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)

1. 在[Azure 管理入口網站](https://manage.windowsazure.com/)中，按一下 [**網站**]，然後按一下 [**新增**]。
2. 按一下 [**網站**]，然後按一下 [**自訂建立**]。

    **新網站-自訂建立**嚮導隨即開啟。 **自訂建立**嚮導可讓您同時建立網站和資料庫。
3. 在嚮導的 [**建立網站**] 步驟中，于 [ **URL** ] 方塊中輸入字串，以作為應用程式預備環境的唯一 URL。 例如，輸入 ContosoUniversity-staging123 （在結尾包含亂數字，以在採用 ContosoUniversity 時讓它成為唯一的）。

    完整的 URL 將包含您在此處輸入的內容，加上您在文字方塊旁看到的尾碼。
4. 在 [**區域**] 下拉式清單中，選擇最接近您的區域。

    此設定會指定您的 web 應用程式將在哪一個資料中心執行。
5. 在 [**資料庫**] 下拉式清單中，選擇 [**建立新的 SQL Database**]。
6. 在 [ **DB 連接字串名稱**] 方塊中，保留預設值*DefaultConnection*。
7. 按一下方塊底部右側的箭號。

    下圖顯示 [**建立網站**] 對話方塊，其中包含範例值。 您輸入的 URL 和區域將會不同。

    ![建立網站步驟](deploying-to-production/_static/image1.png)

    嚮導會前進至 [**指定資料庫設定**] 步驟。
8. 在 [**名稱**] 方塊中，輸入*ContosoUniversity*加上一個亂數字，讓它成為唯一的，例如*ContosoUniversity123*。
9. 在 [**伺服器**] 方塊中，選取 [**新增 SQL Database 伺服器**]。
10. 輸入系統管理員名稱和密碼。

    您不會在此輸入現有的名稱和密碼。 您正在輸入目前定義的新名稱和密碼，以供稍後存取資料庫時使用。
11. 在 [**區域**] 方塊中，選擇您為 web 應用程式選擇的相同區域。

    將網頁伺服器和資料庫伺服器保留在相同的區域，可提供最佳效能，並將費用降至最低。
12. 按一下方塊底部的核取記號，表示您已經完成。

    下圖顯示 [**指定資料庫設定**] 對話方塊，其中包含範例值。 您所輸入的值可能不同。

    ![新網站的資料庫設定步驟-使用資料庫建立嚮導](deploying-to-production/_static/image2.png)

    管理入口網站會回到 [網站] 頁面，[**狀態**] 欄會顯示正在建立 web 應用程式。 經過一段時間（通常不到一分鐘）之後，[**狀態**] 欄會顯示已成功建立 web 應用程式。 在左側的導覽列中，您帳戶中的 web 應用程式數目會顯示在 [**網站**] 圖示旁，而且資料庫的數目會顯示在 [ **SQL 資料庫**] 圖示旁。

    ![網站管理入口網站的 [web Sites] 頁面，已建立網站](deploying-to-production/_static/image3.png)

    您的 web 應用程式名稱將與圖例中的範例應用程式不同。

## <a name="deploy-the-application-to-staging"></a>將應用程式部署至預備環境

現在，您已建立預備環境的 web 應用程式和資料庫，您可以將專案部署到其中。

> [!NOTE]
> 這些指示會示範如何藉由下載 *.publishsettings*檔案來建立發行設定檔，它不僅適用于 Azure，也適用于協力廠商主機服務提供者。 最新的 Azure SDK 也可讓您從 Visual Studio 直接連線到 Azure，並從您的 Azure 帳戶中所擁有的 web 應用程式清單中選擇。 在 Visual Studio 2013 中，您可以從 [ **Web 發佈**] 對話方塊或從 [**伺服器總管**] 視窗登入 Azure。 如需詳細資訊，請參閱[在 Azure App Service 中建立 ASP.NET web 應用程式](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)。

### <a name="download-the-publishsettings-file"></a>下載 .publishsettings 檔案

1. 按一下您剛建立的 web 應用程式名稱。

    ![按一下網站前往儀表板](deploying-to-production/_static/image4.png)
2. 在 **儀表板** 索引標籤的 **快速概覽** 底下，按一下 **下載發行設定檔**

    ![下載發行設定檔連結](deploying-to-production/_static/image5.png)

    此步驟會下載一個檔案，其中包含您將應用程式部署至 web 應用程式所需的所有設定。 您會將此檔案匯入 Visual Studio，因此您不需要手動輸入此資訊。
3. 將 *.publishsettings*檔案儲存在您可以從 Visual Studio 存取的資料夾中。

    ![儲存 .publishsettings 檔案](deploying-to-production/_static/image6.png)

    > [!WARNING]
    > 安全性- *.publishsettings*檔案包含用來管理 Azure 訂用帳戶和服務的認證（未編碼）。 這個檔案的安全性最佳作法是暫時儲存在來原始目錄之外（例如在 Libraries\Documents 資料夾中），然後在匯入完成後刪除它。 取得 *.publishsettings*檔案存取權的惡意使用者可以編輯、建立和刪除您的 Azure 服務。

### <a name="create-a-publish-profile"></a>建立發行設定檔

1. 在 Visual Studio 中，以滑鼠右鍵按一下**方案總管**中的 ContosoUniversity 專案，然後從內容功能表中選取 [**發佈**]。

    [**發行 Web** wizard] 隨即開啟。
2. 按一下 [**設定檔**] 索引標籤。
3. 按一下 [匯入]。
4. 流覽至您稍早下載的 *.publishsettings*檔案，然後按一下 [**開啟**]。

    ![[匯入發行設定] 對話方塊](deploying-to-production/_static/image7.png)
5. 在 [**連接**] 索引標籤中，按一下 [**驗證**連線] 以確定設定正確。

    當連接經過驗證之後，[**驗證**連線] 按鈕旁會顯示綠色核取記號。

    對於某些主控提供者，當您按一下 [**驗證連接**] 時，可能會看到 [**憑證錯誤**] 對話方塊。 如果您這樣做，請確認伺服器名稱是否符合您的預期。 如果伺服器名稱正確，請選取 [**儲存此憑證以供 Visual Studio 的未來會話**]，然後按一下 [**接受**]。 （此錯誤表示主機服務提供者已選擇避免針對您要部署的 URL 購買 SSL 憑證的費用。 如果您想要使用有效的憑證來建立安全連線，請聯絡您的主機服務提供者）。
6. 按 [ **下一步**]。

    ![連線成功圖示和連線索引標籤中的 [下一步] 按鈕](deploying-to-production/_static/image8.png)
7. 在 [**設定**] 索引標籤中，展開 [檔案] [**發佈選項**]，然後選取 **[從應用程式中排除檔案\_資料夾**]。

    如需 [檔案**發佈選項**] 底下其他選項的詳細資訊，請參閱[部署至 IIS](deploying-to-iis.md)教學課程。 顯示此步驟結果和下列資料庫設定步驟的螢幕擷取畫面位於資料庫設定步驟的結尾。
8. 在 [**資料庫**] 區段的 [ **DefaultConnection** ] 底下，設定成員資格資料庫的資料庫部署。
9. 1. 選取 [**更新資料庫**]。

        **DefaultConnection**正下方的**遠端連線字串**方塊會填入 .publishsettings 檔案中的連接字串。連接字串包含 SQL Server 認證，會以純文字的形式儲存在 *.pubxml*檔案中。 如果您不想要將它們永久儲存在該處，您可以在部署資料庫之後，從發行設定檔中移除它們，並改為將其儲存在 Azure 中。 如需詳細資訊，請參閱 Scott Hanselman 的 blog 中的 <<c0>如何保護您的 ASP.NET 資料庫連接字串的安全從來源部署至 Azure 。
      2. 按一下 [**設定資料庫更新**]。
      3. 在 [**設定資料庫更新**] 對話方塊中，按一下 [**加入 SQL 腳本**]。
      4. 在 [**加入 SQL 腳本**] 方塊中，流覽至您稍早在 [方案] 資料夾中儲存的*aspnet-data-prod*腳本，然後按一下 [**開啟**]。
      5. 關閉 [**設定資料庫更新**] 對話方塊。
10. 在 **資料庫** 區段的  **SchoolCoNtext**  底下，選取 **執行 Code First 移轉（在應用程式啟動時執行）** 。

    Visual Studio 會顯示 `DbContext` 類別的**執行 Code First 移轉**，而不是**更新資料庫**。 如果您想要使用 dbDacFx 提供者而非遷移來部署您使用 `DbContext` 類別存取的資料庫，請參閱 MSDN 上 Visual Studio 和 ASP.NET 的 Web 部署常見問題中的[如何? 部署 Code First 資料庫而不進行遷移？](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) 。

    [**設定**] 索引標籤現在看起來如下列範例所示：

    ![預備環境的 [設定] 索引標籤](deploying-to-production/_static/image9.png)
11. 請執行下列步驟來儲存設定檔，並將它重新命名為*預備*環境：

    1. 按一下 [**設定檔**] 索引標籤，然後按一下 [**管理設定檔**]。
    2. 匯入建立了兩個新的設定檔，一個用於 FTP，另一個用於 Web Deploy。 您已設定 Web Deploy 設定檔：將此設定檔重新命名為*預備*環境。

        ![將設定檔重新命名為預備環境](deploying-to-production/_static/image10.png)
    3. 關閉 [**編輯 Web 發行設定檔**] 對話方塊。
    4. 關閉 [**發行 Web** wizard]。

### <a name="configure-a-publish-profile-transform-for-the-environment-indicator"></a>設定環境指標的發行設定檔轉換

> [!NOTE]
> 本節說明如何設定環境指標的 web.config 轉換。 由於指標是在 `<appSettings>` 專案中，因此當您要部署至 Azure App Service 時，您會有另一個指定轉換的替代方法。 如需詳細資訊，請參閱[在 Azure 中指定 web.config 設定](web-config-transformations.md#watransforms)。

1. 在**方案總管**中，展開 [**屬性**]，然後展開 [ **PublishProfiles**]。
2. 以滑鼠右鍵按一下 [ *.pubxml*]，然後按一下 [**新增設定轉換**]。

    ![新增預備環境的設定轉換](deploying-to-production/_static/image11.png)

    Visual Studio 建立*web.config*轉換檔案並加以開啟。
3. *在 web.config 轉換檔案*中，將下列程式碼插入緊接在開啟的 `configuration` 標記之後。

    [!code-xml[Main](deploying-to-production/samples/sample1.xml)]

    當您使用臨時發行設定檔時，這種轉換會將環境指標設定為「生產」。 在部署的 web 應用程式中，您不會在 "Contoso 大學" H1 標題之後看到任何尾碼，例如 "（Dev）" 或 "（Test）"。
4. 以滑鼠右鍵按一下 [ *web.config*檔案]，然後按一下 [**預覽轉換**]，以確定您編碼的轉換會產生預期的變更。

    [Web.config**預覽**] 視窗會顯示套用*web.config*轉換和進行 web.config 轉換時的結果。

### <a name="prevent-public-use-of-the-test-app"></a>防止測試應用程式的公用使用

預備應用程式的重要考慮是它會在網際網路上上線，但您不想讓公用使用它。 若要將使用者尋找和使用的可能性降到最低，您可以使用下列一或多個方法：

- 設定防火牆規則，只允許從您用來測試預備環境的 IP 位址存取預備應用程式。
- 請使用模糊的 URL，這不可能猜到。
- 建立*機器人 .txt*檔案，以確保搜尋引擎不會編目測試應用程式，並在搜尋結果中報告其連結。

這些方法的第一個是最有效率的，但在本教學課程中並未涵蓋，因為它需要您部署至 Azure 雲端服務，而不是 Azure App Service。 如需有關 Azure 中雲端服務和 IP 限制的詳細資訊，請參閱[計算 Azure 提供的裝載選項](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me)和[封鎖特定的 IP 位址，使其無法存取 Web 角色](https://msdn.microsoft.com/library/windowsazure/jj154098.aspx)。 如果您要部署到協力廠商主機服務提供者，請洽詢提供者以瞭解如何執行 IP 限制。

在本教學課程中，您將建立一個*機器人 .txt*檔案。

1. 在**方案總管**中，以滑鼠右鍵按一下 ContosoUniversity 專案，然後按一下 [**加入新專案**]。
2. 建立名為*機器人*的新**文字檔**，並在其中放入下列文字：

    [!code-console[Main](deploying-to-production/samples/sample2.cmd)]

    [`User-agent`] 行會告訴搜尋引擎，檔案中的規則會套用至所有的搜尋引擎 web 編目程式（機器人），而 [`Disallow`] 行會指定網站上不應編目任何頁面。

    您想要讓搜尋引擎針對您的生產應用程式進行類別目錄，因此您需要從生產環境部署中排除此檔案。 若要這麼做，您會在建立生產發行設定檔時進行設定。

### <a name="deploy-to-staging"></a>部署至預備環境

1. 以滑鼠右鍵按一下 [Contoso 大學] 專案，然後按一下 [**發佈**]，以開啟 [**發佈 Web** wizard]。
2. 請確定已選取 [**暫存**設定檔]。
3. 按一下 [發行]。

    [**輸出**] 視窗會顯示已採取的部署動作，並報告部署已成功完成。 預設瀏覽器會自動開啟至已部署 web 應用程式的 URL。

## <a name="test-in-the-staging-environment"></a>在預備環境中測試

請注意，[] H1 標題後面沒有 [（測試）] 或 [（Dev）]，這表示環境指標的*web.config 轉換成功*。

![首頁預備環境](deploying-to-production/_static/image12.png)

執行 [**學生**] 頁面，確認部署的資料庫沒有任何學生。

執行 [**講師**] 頁面，確認 Code First 植入具有講師資料的資料庫：

從 [**學生**] 功能表選取 [**新增學生**]、新增學生，然後在 [**學生**] 頁面中查看新學生，以確認您可以成功寫入資料庫。

在 [**課程**] 頁面上，按一下 [**更新信用額度**]。 [**更新信用額度**] 頁面需要系統管理員許可權，因此會顯示 [**登入**] 頁面。 輸入您稍早建立的系統管理員帳號憑證（"admin" 和 "prodpwd"）。 隨即顯示 [**更新信用額度**] 頁面，確認您在上一個教學課程中建立的系統管理員帳戶已正確部署到測試環境。

要求不正確 URL，導致 ELMAH 將會追蹤的錯誤，然後要求 ELMAH 錯誤報表。 如果您要部署到協力廠商裝載提供者，您可能會發現報表是空的，因為在上一個教學課程中，它是空的。 您將必須使用主機服務提供者的帳戶管理工具來設定資料夾許可權，以讓 ELMAH 寫入記錄檔資料夾。

您所建立的應用程式現在已在雲端中執行，就像您將用於生產環境的 web 應用程式一樣。 因為所有專案都正常運作，下一步就是部署到生產環境。

## <a name="deploy-to-production"></a>部署到生產環境

建立生產 web 應用程式和部署到生產環境的流程，與預備相同，不同之處在于您需要從部署中排除*機器人 .txt。* 若要這麼做，您將編輯發行設定檔。

### <a name="create-the-production-environment-and-the-production-publish-profile"></a>建立生產環境和生產發行設定檔

1. 在 Azure 中建立生產 web 應用程式和資料庫，遵循您用於預備的相同程式。

    當您建立資料庫時，可以選擇將它放在您稍早建立的相同伺服器上，或建立新的伺服器。
2. 下載 *.publishsettings*檔案。
3. 藉由匯入 *.publishsettings*檔案來建立發行設定檔，請遵循您用於預備的相同程式。

    別忘了在 [**設定**] 索引標籤的 [**資料庫**] 區段中的 [ **DefaultConnection** ] 底下設定資料部署腳本。
4. 將發行設定檔重新命名為*生產環境*。
5. 針對環境指標設定發行設定檔轉換，遵循您用於暫存的相同程式。

### <a name="edit-the-pubxml-file-to-exclude-robotstxt"></a>編輯 .pubxml 檔案以排除機器人 .txt

發行設定檔的名稱是 &lt;profilename&gt; *. .pubxml* ，而且位於*PublishProfiles*資料夾中。 *PublishProfiles*資料夾位於C# web 應用程式專案中的 [ *Properties* ] 資料夾下、在 VB Web 應用程式專案的 [*我的專案*] 資料夾底下，或是在 web 應用程式專案的 [*應用程式\_Data* ] 資料夾下。 每個 *.pubxml*檔案都包含適用于一個發行設定檔的設定。 您在 [發行 Web wizard] 中輸入的值會儲存在這些檔案中，而您可以編輯它們來建立或變更 Visual Studio UI 中未提供的設定。

根據預設，當您建立發行設定檔時，專案中會包含 *.pubxml*檔案，但是您可以將它們從專案中排除，Visual Studio 仍會使用它們。 Visual Studio 會在 *.pubxml*檔案的*PublishProfiles*資料夾中尋找，不論它們是否包含在專案中。

每個 *.pubxml*檔案都有一個 *.pubxml. user*檔案。 如果您選取 [**儲存密碼**] 選項，則 *.pubxml*檔案會包含加密的密碼，而且預設會從專案中排除。

*.Pubxml*檔案包含特定發行設定檔的相關設定。 如果您想要設定適用于所有設定檔的設定，可以建立一個*wpp .targets*檔案。 組建程式會將這些檔案匯入 *.csproj*或 *. vbproj*專案檔中，因此您可以在專案檔中設定的大部分設定都可以在這些檔案中進行設定。 如需有關 *.pubxml*檔案和*wpp .targets*檔案的詳細資訊，請參閱 [how to：編輯發行設定檔（. .pubxml）檔案中的部署設定，以及 Visual Studio Web 專案](https://msdn.microsoft.com/library/ff398069.aspx)中的 wpp .targets 檔案。

1. 在**方案總管**中，展開 [**屬性**]，然後展開 [ **PublishProfiles**]。
2. 以滑鼠右鍵按一下 [ *.pubxml* ]，然後按一下 [**開啟**]。

    ![開啟 .pubxml 檔案](deploying-to-production/_static/image13.png)
3. 以滑鼠右鍵按一下 [ *.pubxml* ]，然後按一下 [**開啟**]。
4. 緊接在結尾 `PropertyGroup` 元素前面新增下列幾行：

    [!code-xml[Main](deploying-to-production/samples/sample3.xml)]

    .Pubxml 檔案現在看起來如下列範例所示：

    [!code-xml[Main](deploying-to-production/samples/sample4.xml?highlight=18-20)]

    如需有關如何排除檔案和資料夾的詳細資訊，請參閱 MSDN 上**Visual Studio 和 ASP.NET 的 Web 部署常見問題**中的「[我可以從部署中排除特定檔案或資料夾嗎？](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment) 」。

### <a name="deploy-to-production"></a>部署到生產環境

1. 開啟 [**發行 Web** wizard]，確認已選取 [**生產**發行] 設定檔，然後按一下 [**預覽**] 索引標籤上的 [**開始預覽**]，確認不會將*機器人 .txt*檔案複製到生產應用程式。

    ![要發行至生產環境的檔案預覽](deploying-to-production/_static/image14.png)

    檢查將要複製的檔案清單。 您會看到所有的 *.cs*檔案（包括*aspx.cs*、 *aspx.designer.cs*、 *Master.cs*和*Master.designer.cs*檔案）都會被省略。 所有此程式碼都已編譯成*ContosoUniversity* ，以及您會在*bin*資料夾中找到的*ContosoUniversity .pdb*檔案。 由於執行應用程式只需要 *.dll* ，而且您稍早指定只應部署執行應用程式所需的檔案，因此不會將 *.cs*檔案複製到目的地環境。 基於相同原因，會省略*obj*資料夾和*ContosoUniversity*和 *.csproj. 使用者*檔案。

    按一下 [**發佈**] 以部署到生產環境。
2. 在生產環境中測試，遵循您用於預備的相同程式。

    除了 URL 和不存在的*機器人 .txt*檔案之外，所有專案都與預備環境相同。

## <a name="summary"></a>總結

您現在已成功部署和測試您的 web 應用程式，而且它可透過網際網路公開取得。

![首頁生產](deploying-to-production/_static/image15.png)

在下一個教學課程中，您將更新應用程式程式碼，並將變更部署到測試、預備和生產環境。

> [!NOTE]
> 當您的應用程式在生產環境中使用時，您應該執行復原方案。 也就是說，您應該定期從生產應用程式將資料庫備份至安全的儲存位置，而且您應該保留數個層代的這類備份。 當您更新資料庫時，您應該在變更之前立即建立備份複本。 然後，如果您犯了錯誤，而且在將它部署到生產環境之後卻找不到它，您仍然可以將資料庫復原到損毀之前的狀態。 如需詳細資訊，請參閱[Azure SQL Database 備份和還原](https://msdn.microsoft.com/library/windowsazure/jj650016.aspx)。
> 
> 
> [!NOTE]
> 在本教學課程中，您要部署的 SQL Server 版本是 Azure SQL Database。 雖然部署程式與其他版本的 SQL Server 類似，但在某些情況下，實際生產應用程式可能會需要特殊的程式碼來進行 Azure SQL Database。 如需詳細資訊，請參閱[使用 Azure SQL Database](../../../../whitepapers/aspnet-data-access-content-map.md#ssdb)和[在 SQL Server 和 Azure SQL Database 之間選擇](../../../../whitepapers/aspnet-data-access-content-map.md#ssdbchoosing)。
> 
> [!div class="step-by-step"]
> [上一頁](setting-folder-permissions.md)
> [下一頁](deploying-a-code-update.md)
