---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
title: 使用 Visual Studio ASP.NET Web 部署：部署資料庫更新 |Microsoft Docs
author: tdykstra
description: 本教學課程系列將示範如何透過互動，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商主機服務提供者。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 9cad0833-486a-4474-a7f3-7715542ec4ce
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
msc.type: authoredcontent
ms.openlocfilehash: 805eb84c24764cf921291f89054435601dbac48e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78547737"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-database-update"></a>使用 Visual Studio ASP.NET Web 部署：部署資料庫更新

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載入門專案](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本教學課程系列說明如何使用 Visual Studio 2012 或 Visual Studio 2010，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商裝載提供者。 如需有關數列的詳細資訊，請參閱[本系列的第一個教學](introduction.md)課程。

## <a name="overview"></a>概觀

在本教學課程中，您會進行資料庫變更和相關的程式碼變更、在 Visual Studio 中測試變更，然後將更新部署到測試、預備和生產環境。

本教學課程會先示範如何更新 Code First 移轉所管理的資料庫，然後再說明如何使用 dbDacFx 提供者更新資料庫。

提醒：如果您在進行本教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解][頁面](troubleshooting.md)。

## <a name="deploy-a-database-update-by-using-code-first-migrations"></a>使用 Code First 移轉部署資料庫更新

在本節中，您會將「出生日期」資料行加入 `Student` 和 `Instructor` 實體的 `Person` 基類。 接著，您會更新顯示講師資料的頁面，使其顯示新的資料行。 最後，您會將變更部署到測試、預備和生產環境。

### <a name="add-a-column-to-a-table-in-the-application-database"></a>將資料行新增至應用程式資料庫中的資料表

1. 在*ContosoUniversity*專案中，開啟*Person.cs* ，並在 `Person` 類別的結尾處新增下列屬性（後面應該有兩個右大括弧）：

    [!code-csharp[Main](deploying-a-database-update/samples/sample1.cs)]

    接下來，更新 `Seed` 方法，讓它提供新資料行的值。 開啟*Migrations\Configuration.cs* ，並將開始 `var instructors = new List<Instructor>` 的程式碼區塊取代為下列包含出生日期資訊的程式碼區塊：

    [!code-csharp[Main](deploying-a-database-update/samples/sample2.cs)]
2. 建立解決方案，然後開啟 [**套件管理員主控台**] 視窗。 請確定 [ContosoUniversity] 仍然選取為 [**預設專案**]。
3. 在 [**套件管理員主控台**] 視窗中，選取 [ **ContosoUniversity** ] 做為**預設專案**，然後輸入下列命令：

    [!code-powershell[Main](deploying-a-database-update/samples/sample3.ps1)]

    當此命令完成時，Visual Studio 會開啟定義新 `DbMigration` 類別的類別檔案，而在 `Up` 方法中，您可以看到建立新資料行的程式碼。 當您執行變更時，`Up` 方法會建立資料行，而 `Down` 方法則會在您回復變更時刪除資料行。

    ![AddBirthDate_migration_code](deploying-a-database-update/_static/image1.png)
4. 建立解決方案，然後在 [**套件管理員主控台**] 視窗中輸入下列命令（請確定仍已選取 [ContosoUniversity] 專案）：

    [!code-powershell[Main](deploying-a-database-update/samples/sample4.ps1)]

    Entity Framework 會執行 `Up` 方法，然後執行 `Seed` 方法。

### <a name="display-the-new-column-in-the-instructors-page"></a>在 [講師] 頁面中顯示新的資料行

1. 在 ContosoUniversity 專案中，開啟 [ *default.aspx* ]，然後新增 [範本] 欄位以顯示出生日期。 將其新增至 [雇用日期] 和 [辦公室指派]：

    [!code-aspx[Main](deploying-a-database-update/samples/sample5.aspx?highlight=9-17)]

    （如果程式碼縮排無法同步處理，您可以按下 CTRL-K，然後按 CTRL-D 自動重新格式化檔案）。
2. 執行應用程式，然後按一下 [**講師**] 連結。

    當頁面載入時，您會看到它有新的出生日期欄位。

    ![具有生日的講師頁面](deploying-a-database-update/_static/image2.png)
3. 關閉瀏覽器。

### <a name="deploy-the-database-update"></a>部署資料庫更新

1. 在**方案總管**選取 [ContosoUniversity] 專案。
2. 在 Web 單鍵的 [**發行**] 工具列中，按一下 [**測試**發行設定檔]，然後按一下 [**發佈 Web**]。 （如果工具列已停用，請在**方案總管**中選取 ContosoUniversity 專案）。

    Visual Studio 會部署已更新的應用程式，且瀏覽器會開啟至首頁。
3. 執行 [**講師**] 頁面，確認已成功部署更新。

    當應用程式嘗試存取此頁面的資料庫時，Code First 會更新資料庫架構，並執行 `Seed` 方法。 當頁面顯示時，您會看到 [預期的**出生日期] 資料**行中有日期。
4. 在 Web 單鍵的 [**發行**] 工具列中，按一下 [**臨時**發行] 設定檔，然後按一下 [**發佈 Web**]。
5. 在預備環境中執行**講師**頁面，確認已成功部署更新。
6. 在 Web 單鍵的 [**發行**] 工具列中，按一下 [**生產**] 發行設定檔，然後按一下 [**發佈 Web**]。
7. 在生產環境中執行**講師**頁面，確認已成功部署更新。

    對於包含資料庫變更的實際生產應用程式更新，您通常也會在 *\_* 部署期間讓應用程式離線，如您在上一個教學課程中所見。

## <a name="deploy-a-database-update-by-using-the-dbdacfx-provider"></a>使用 dbDacFx 提供者來部署資料庫更新

在本節中，您會將 [*批註*] 資料行新增至成員資格資料庫中的*使用者*資料表，並建立一個頁面，讓您顯示和編輯每個使用者的批註。 然後，將變更部署到測試、預備和生產環境。

### <a name="add-a-column-to-a-table-in-the-membership-database"></a>將資料行加入至成員資格資料庫中的資料表

1. 在 Visual Studio 中，開啟**SQL Server 物件總管**。
2. 依序展開 **[（localdb）] \v11.0、[** **資料庫**] 和 [ **aspnet-ContosoUniversity** （不是**aspnet-ContosoUniversity-生產**）]，然後展開 [**資料表]** 。

    如果您在 [ **SQL Server** ] 節點底下看不到 [ **（localdb）] \v11.0** ，請以滑鼠右鍵按一下 [ **SQL Server** ] 節點，然後按一下 [**新增 SQL Server**]。 在 [**連接到伺服器**] 對話方塊中，輸入 *（localdb） \V11.0*做為**伺服器名稱**，然後按一下 **[連接]** 。

    如果您看不到 [ **aspnet-ContosoUniversity**]，請執行專案並使用系統*管理員*認證登入（密碼是*devpwd*），然後重新整理 [ **SQL Server 物件總管**] 視窗。
3. 以滑鼠右鍵按一下 [**使用者**] 資料表，然後按一下 [**視圖設計**工具]。

    ![SSOX 視圖設計工具](deploying-a-database-update/_static/image3.png)
4. 在設計工具中，新增 [*批註*] 資料行，並將它設為*Nvarchar （128）* 且可為 null，然後按一下 [**更新**]。

    ![加入批註資料行](deploying-a-database-update/_static/image4.png)
5. 在 [**預覽資料庫更新**] 方塊中，按一下 [**更新資料庫**]。

    ![預覽資料庫更新](deploying-a-database-update/_static/image5.png)

### <a name="create-a-page-to-display-and-edit-the-new-column"></a>建立頁面以顯示和編輯新的資料行

1. 在**方案總管**中，以滑鼠右鍵按一下 ContosoUniversity 專案中的 [**帳戶**] 資料夾，按一下 [**加入**]，然後按一下 [**新增專案**]。
2. **使用主版頁面建立新的 Web 表單**，並將其命名為*使用者名稱 .aspx*。 接受預設的*網站*檔案作為主版頁面。
3. 將下列標記複製到 `MainContent` `Content` 元素（3個 `Content` 元素的最後一個）：

    [!code-aspx[Main](deploying-a-database-update/samples/sample6.aspx)]
4. 以滑鼠右鍵按一下 [*使用者資訊 .aspx* ] 頁面，然後按一下 [**在瀏覽器中查看**]。
5. 使用您的系統*管理員*使用者認證登入（密碼為*devpwd*），並為使用者新增一些批註，以確認網頁是否正常運作。

    ![使用者資訊頁面](deploying-a-database-update/_static/image6.png)
6. 關閉瀏覽器。

## <a name="deploy-the-database-update"></a>部署資料庫更新

若要使用 dbDacFx 提供者進行部署，您只需要選取發行設定檔中的 [**更新資料庫**] 選項。 不過，在使用此選項時，您也設定了一些額外的 SQL 腳本來執行：那些仍在設定檔中，因此您必須避免它們再次執行。

1. 以滑鼠右鍵按一下 [ContosoUniversity] 專案，然後按一下 [**發佈**]，以開啟 [**發佈 Web** wizard]。
2. 選取**測試**設定檔。
3. 按一下 [設定] 索引標籤。
4. 在 [ **DefaultConnection**] 底下，選取 [**更新資料庫**]。
5. 停用您設定為初始部署執行的其他腳本：

    1. 按一下 [**設定資料庫更新**]。
    2. 在 [**設定資料庫更新**] 對話方塊中，清除 [*授與 .sql* ] 和 [ *aspnet-data-dev*] 旁的核取方塊。
    3. 按一下 [ **關閉**]。
6. 按一下 **預覽** 索引標籤。
7. 在 [**資料庫**] 底下的 [ **DefaultConnection**] 右邊，按一下 [**預覽資料庫**] 連結。

    ![資料庫預覽](deploying-a-database-update/_static/image7.png)

    [預覽] 視窗會顯示將在目的地資料庫中執行的腳本，讓該資料庫架構符合源資料庫的架構。 此腳本包含可加入新資料行的 ALTER TABLE 命令。
8. 關閉 [**資料庫預覽**] 對話方塊，然後按一下 [**發佈**]。

    Visual Studio 會部署已更新的應用程式，且瀏覽器會開啟至首頁。
9. 執行 [使用者資訊] 頁面（將*帳戶/使用者資訊*類型新增至首頁 URL），以確認更新已成功部署。 您必須輸入*admin*和*devpwd*來登入。

    根據預設，資料表中的資料不會部署，而且您不會設定要執行的資料部署腳本，因此您不會發現在開發中新增的批註。 您現在可以在預備環境中加入新的批註，以確認變更已部署至資料庫，且網頁運作正常。
10. 遵循相同的程式部署至預備和生產環境。

    別忘了停用額外的腳本。 與測試組態檔相較之下，唯一的差別在於，您只會在預備和生產設定檔中停用一個腳本，因為它們已設定為僅執行*aspnet-prod-data。*

    預備和生產的認證是 admin 和 prodpwd。

    對於包含資料庫變更的實際生產應用程式更新，您通常也會在部署期間將應用程式離線，方法是先上傳應用程式 *\_離線*，然後再發佈和刪除它，如同您在[上一個教學](deploying-a-code-update.md)課程中所見。

## <a name="summary"></a>總結

您現在已部署應用程式更新，其中包含使用 Code First 移轉和 dbDacFx 提供者的資料庫變更。

![具有生日的講師頁面](deploying-a-database-update/_static/image8.png)

![使用者資訊頁面](deploying-a-database-update/_static/image9.png)

下一個教學課程說明如何使用命令列執行部署。

> [!div class="step-by-step"]
> [上一頁](deploying-a-code-update.md)
> [下一頁](command-line-deployment.md)
