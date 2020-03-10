---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
title: 使用 Visual Studio ASP.NET Web 部署：部署程式碼更新 |Microsoft Docs
author: tdykstra
description: 本教學課程系列將示範如何透過互動，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商主機服務提供者。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: c76dbc35-a914-4ee3-919c-4f4d1fa05104
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
msc.type: authoredcontent
ms.openlocfilehash: 3881833bfe2a50a38a357614f92f434a04a8ab08
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78567400"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-code-update"></a>使用 Visual Studio ASP.NET Web 部署：部署程式碼更新

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載入門專案](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本教學課程系列說明如何使用 Visual Studio 2012 或 Visual Studio 2010，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商裝載提供者。 如需有關數列的詳細資訊，請參閱[本系列的第一個教學](introduction.md)課程。

## <a name="overview"></a>概觀

在初始部署之後，您維護和開發網站的工作會繼續進行，而且在很久之前，您會想要部署更新。 本教學課程會引導您完成將更新部署至應用程式程式碼的流程。 您在本教學課程中執行及部署的更新不會牽涉到資料庫變更;在下一個教學課程中，您會看到部署資料庫變更的不同之處。

提醒：如果您在進行本教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解][頁面](troubleshooting.md)。

## <a name="make-a-code-change"></a>進行程式碼變更

做為應用程式更新的簡單範例，您會將所選講師所教授的課程清單新增到**講師**頁面。

如果您執行 [**講師**] 頁面，您會發現方格中有 [**選取**] 連結，但它們不會執行任何動作，而是讓資料列背景變成灰色。

![具有選取專案的講師頁面](deploying-a-code-update/_static/image1.png)

現在您將新增在按一下 [**選取**] 連結時執行的程式碼，並顯示所選講師所教授的課程清單。

1. 在 [ **ErrorMessageLabel** ] `Label` 控制項之後，于 [ *.aspx*] 中立即新增下列標記：

    [!code-aspx[Main](deploying-a-code-update/samples/sample1.aspx)]
2. 執行頁面，然後選取講師。 您會看到該講師所教授的課程清單。

    ![講師頁面包含教授的課程](deploying-a-code-update/_static/image2.png)
3. 關閉瀏覽器。

## <a name="deploy-the-code-update-to-the-test-environment"></a>將程式碼更新部署到測試環境

在您可以使用發行設定檔部署到測試、預備和生產環境之前，您需要變更資料庫發行選項。 您不再需要執行成員資格資料庫的授與和資料部署腳本。

1. 以滑鼠右鍵按一下 [ContosoUniversity] 專案，然後按一下 [**發佈**]，以開啟 [**發佈 Web** wizard]。
2. 按一下 [**配置**檔] 下拉式清單中的**測試**設定檔。
3. 按一下 [設定] 索引標籤。
4. 在 [**資料庫**] 區段的 [ **DefaultConnection** ] 下，清除 [**更新資料庫**] 核取方塊。
5. 按一下 [**設定檔**] 索引標籤，然後按一下 [**配置**檔] 下拉式清單中的**暫存**設定檔。
6. 當系統詢問您是否要儲存對**測試**設定檔所做的變更時，請按一下 **[是]** 。
7. 在暫存設定檔中進行相同的變更。
8. 重複此程式，在生產設定檔中進行相同的變更。
9. 關閉 [**發行 Web** wizard]。

部署到測試環境現在很簡單，只要執行一次 [發佈] 即可。 若要讓此程式更快速，您可以使用 Web 單鍵 [**發行**] 工具列。

1. 在 [ **View** ] 功能表中，選擇 [**工具列**]，然後選取 [ **Web One**] [發佈]。

    ![Selecting_One_Click_Publish_toolbar](deploying-a-code-update/_static/image3.png)
2. 在 **方案總管**中，選取 ContosoUniversity 專案。
3. Web 單鍵 [**發行**] 工具列，選擇 [**測試**發行設定檔]，然後按一下 [**發佈 Web** ] （箭號向左和向右的圖示）。

    ![Web_One_Click_Publish_toolbar](deploying-a-code-update/_static/image4.png)
4. Visual Studio 會部署已更新的應用程式，且瀏覽器會自動開啟至首頁。
5. 執行 [講師] 頁面，然後選取講師以確認更新已成功部署。

您通常也會進行迴歸測試（也就是測試網站的其餘部分，以確保新的變更不會中斷任何現有的功能）。 但是在本教學課程中，您會略過該步驟，並繼續將更新部署至預備和生產環境。

當您重新部署時，Web Deploy 會自動判斷哪些檔案已變更，而且只會將已變更的檔案複製到伺服器。 根據預設，Web Deploy 會在檔案上使用上次變更的日期，以判斷哪些檔案已變更。 某些原始檔控制系統會變更檔案的日期，即使您未變更檔案內容也一樣。 在這種情況下，您可能會想要設定 Web Deploy 使用檔案總和檢查碼來判斷哪些檔案已變更。 如需詳細資訊，請參閱 ASP.NET 部署常見問題中的[為何所有檔案都已重新部署，但我並未變更它們？](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum) 。

## <a name="take-the-application-offline-during-deployment"></a>在部署期間讓應用程式離線

您要部署的變更現在是單一頁面的簡單變更。 但有時候您會部署較大的變更，或部署程式碼和資料庫變更，而且如果使用者在部署完成之前要求頁面，網站可能會不正確地運作。 若要防止使用者在部署進行時存取網站，您可以使用*應用程式\_離線 .htm*檔案。 當您在應用程式的根資料夾中，將名為 app 的檔案 *\_離線*時，IIS 會自動顯示該檔案，而不是執行您的應用程式。 因此，若要在部署期間防止存取，您可以將*應用程式\_離線的 .htm* ，執行部署程式，然後在部署成功之後，將*應用程式\_離線。*

您可以設定 Web Deploy 自動將預設*應用\_程式*放在伺服器上的離線 .htm 檔案中，然後在完成時將其移除。 若要這麼做，您只需要將下列 XML 元素新增至您的發行設定檔（. .pubxml）檔案：

[!code-xml[Main](deploying-a-code-update/samples/sample2.xml)]

在本教學課程中，您將瞭解如何建立及使用自訂*應用程式\_離線 .htm*檔案。

不需要在預備網站中使用*應用程式\_離線*，因為您沒有存取暫存網站的使用者。 但最好是使用預備環境，以您計畫在生產環境中部署的方式來測試所有專案。

### <a name="create-app_offlinehtm"></a>建立離線應用程式\_.htm

1. 在**方案總管**中，以滑鼠右鍵按一下方案，然後按一下 [**加入**]，再按一下 [**新增專案**]。
2. 建立名為*應用程式\_離線*的**html 網頁**（在 Visual Studio 預設建立的 *.html*副檔名中刪除最後的 "l"）。
3. 將範本標記取代為下列標記：

    [!code-html[Main](deploying-a-code-update/samples/sample3.html)]
4. 儲存並關閉檔案。

### <a name="copy-app_offlinehtm-to-the-root-folder-of-the-web-site"></a>將應用程式\_離線複製到網站的根資料夾

您可以使用任何 FTP 工具將檔案複製到網站。 [FileZilla](http://filezilla-project.org/)是常用的 FTP 工具，會顯示在螢幕擷取畫面中。

若要使用 FTP 工具，您需要三個專案： FTP URL、使用者名稱和密碼。

URL 會顯示在 Azure 管理入口網站中網站的 [儀表板] 頁面上，而 FTP 的 [使用者名稱] 和 [密碼] 可在您稍早下載的 *.publishsettings*檔案中找到。 下列步驟顯示如何取得這些值。

1. 在 Azure 管理入口網站中，按一下 [**網站**] 索引標籤，然後按一下暫存網站。
2. 在 [**儀表板**] 頁面上，向下流覽至 [**快速概覽**] 區段中的 [FTP 主機名稱]。

    ![FTP 主機名稱](deploying-a-code-update/_static/image5.png)
3. 在 [記事本] 或其他文字編輯器中開啟 *.publishsettings*檔案。
4. 尋找 FTP 設定檔的 `publishProfile` 元素。
5. 複製 `userName` 和 `userPWD` 值。

    ![FTP 認證](deploying-a-code-update/_static/image6.png)
6. 開啟您的 FTP 工具並登入 FTP URL。
7. 將*應用程式\_離線*，從 [方案] 資料夾複製到預備網站中的 [ */site/wwwroot* ] 資料夾。

    ![複製 app_offline](deploying-a-code-update/_static/image7.png)
8. 流覽至您的預備網站 URL。 您會看到*應用程式\_離線 .htm*  頁面，而不是您的首頁。

    ![瀏覽器視窗中的 app_offline .htm](deploying-a-code-update/_static/image8.png)

您現在已準備好部署至預備環境。

## <a name="deploy-the-code-update-to-staging-and-production"></a>將程式碼更新部署至預備和生產環境

1. 在 Web 單鍵的 [**發行**] 工具列中，選擇**預備**發行設定檔，然後按一下 [**發佈 Web**]。

    Visual Studio 會部署已更新的應用程式，並將瀏覽器開啟至網站的首頁。 隨即顯示*應用程式\_離線的 .htm*檔案。 您必須先移除*應用程式\_離線 .htm*檔案，才能進行測試以確認部署是否成功。
2. 返回您的 FTP 工具，並從預備網站刪除**應用程式\_離線 .htm** 。
3. 在瀏覽器中，開啟預備網站中的 [講師] 頁面，然後選取講師以確認更新已成功部署。
4. 依照您針對預備環境所做的相同程式進行操作。

<a id="specificfiles"></a>

## <a name="reviewing-changes-and-deploying-specific-files"></a>檢查變更和部署特定檔案

Visual Studio 2012 也讓您能夠部署個別檔案。 針對選取的檔案，您可以查看本機版本與已部署版本之間的差異、將檔案部署到目的地環境，或將檔案從目的地環境複製到本機專案。 在本教學課程的這一節中，您會瞭解如何使用這些功能。

### <a name="make-a-change-to-deploy"></a>進行部署的變更

1. 開啟*Content/.css*，然後尋找 `body` 標記的區塊。
2. 將 `background-color` 的值從 `#fff` 變更為 `darkblue`。

    [!code-css[Main](deploying-a-code-update/samples/sample4.css?highlight=2)]

### <a name="view-the-change-in-the-publish-preview-window"></a>在 [發行預覽] 視窗中查看變更

當您使用 [**發行 Web** wizard] 發行專案時，您可以在 [**預覽**] 視窗中按兩下該檔案，以查看即將發行的變更。

1. 以滑鼠右鍵按一下 ContosoUniversity 專案，然後按一下 [**發佈**]。
2. 從 [**設定檔**] 下拉式清單中，選取 [**測試**發行設定檔]。
3. 按一下 [**預覽**]，然後按一下 [**開始預覽**]。
4. 在**預覽**窗格中，按兩下 [ **Site .css**]。

    ![按兩下 [網站 .css]](deploying-a-code-update/_static/image9.png)

    [**預覽變更**] 對話方塊會顯示即將部署之變更的預覽。

    ![網站 .css 的預覽變更](deploying-a-code-update/_static/image10.png)

    如果您*按兩下 web.config 檔案*，[**預覽變更**] 對話方塊會顯示組建設定轉換和發行設定檔轉換的效果。 此時，您未做任何會導致伺服器上的*web.config*檔案變更的動作，因此您預期不會有任何變更。 不過，[**預覽變更**] 視窗會錯誤地顯示兩個變更。 這看起來會移除兩個 XML 元素。 當您在 Code First 內容類別的**應用程式啟動上選取 [執行 Code First 移轉**] 時，發佈程式會新增這些元素。 比較是在發行程式新增這些元素之前完成，因此它似乎已被移除，但不會被移除。 此錯誤將在未來的版本中修正。
5. 按一下 [ **關閉**]。
6. 按一下 [發行]。
7. 當瀏覽器開啟至測試網站的首頁時，請按 CTRL + F5 以進行硬重新整理，以便查看 CSS 變更的效果。

    ![CSS 變更的效果](deploying-a-code-update/_static/image11.png)
8. 關閉瀏覽器。

### <a name="publish-specific-files-from-solution-explorer"></a>從方案總管發行特定檔案

假設您不喜歡藍色背景，而且想要還原成原始的色彩。 在本節中，您將直接從**方案總管**發佈特定檔案，以還原原始設定。

1. 開啟*Content/Site .css* ，然後將 `background-color` 設定還原為 [`#fff`]。
2. 在**方案總管**中，以滑鼠右鍵按一下*內容/網站 .css*檔案。

    內容功能表會顯示三個 [發行] 選項。

    ![從方案總管發佈選項](deploying-a-code-update/_static/image12.png)
3. 按一下 [**預覽變更] 至 [網站 .css**]。

    視窗隨即開啟，以顯示本機檔案與其在目的地環境中的版本之間的差異。

    ![Diff-Content/Site .css](deploying-a-code-update/_static/image13.png)
4. 在**方案總管**中，再次以滑鼠右鍵按一下 [**網站 .css** ]，然後按一下 [**發行網站 .css**]。

    [ **Web 發行活動**] 視窗會顯示檔案已發行。

    ![[Web 發行活動] 視窗](deploying-a-code-update/_static/image14.png)
5. 開啟瀏覽器並前往 [`http://localhost/contosouniversity` URL]，然後按 CTRL + F5 以進行硬重新整理，以便查看 CSS 變更的效果。

    ![具有一般 CSS 的首頁](deploying-a-code-update/_static/image15.png)
6. 關閉瀏覽器。

## <a name="summary"></a>總結

您現在已瞭解幾種部署應用程式更新的方式，而不需要變更資料庫，而且您已瞭解如何預覽變更，以確認會更新的內容是您的預期。 [講師] 頁面現在有 [**課程教授**] 區段。

![講師頁面包含教授的課程](deploying-a-code-update/_static/image16.png)

下一個教學課程會示範如何部署資料庫變更：您會將 [出生日期] 欄位加入至資料庫和 [講師] 頁面。

> [!div class="step-by-step"]
> [上一頁](deploying-to-production.md)
> [下一頁](deploying-a-database-update.md)
