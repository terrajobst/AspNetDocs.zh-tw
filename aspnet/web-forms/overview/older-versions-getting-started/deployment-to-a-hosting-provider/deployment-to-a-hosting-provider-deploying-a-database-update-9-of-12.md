---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 應用程式：部署資料庫更新-9/12 |Microsoft Docs
author: tdykstra
description: 這一系列的教學課程會示範如何使用 Visual Stu 部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案 。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a8d776af-4735-4612-87f6-9f326587f2d3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
msc.type: authoredcontent
ms.openlocfilehash: 3385e1019d9e7a9263fd9513c39b25eb85febbb5
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74581990"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-database-update---9-of-12"></a>使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 應用程式：部署資料庫更新-9/12

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載入門專案](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 這一系列的教學課程會示範如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，來部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案。 如果您安裝 Web 發佈更新，也可以使用 Visual Studio 2010。 如需此系列的簡介，請參閱[本系列的第一個教學](deployment-to-a-hosting-provider-introduction-1-of-12.md)課程。
> 
> 如需示範在 Visual Studio 2012 的 RC 版本後引進部署功能的教學課程，說明如何部署 SQL Server Compact 以外的 SQL Server 版本，並示範如何部署到 Azure App Service Web Apps，請參閱[使用 Visual Studio ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。

## <a name="overview"></a>概觀

在本教學課程中，您會進行資料庫變更和相關的程式碼變更、在 Visual Studio 中測試變更，然後將更新部署到測試和生產環境。

提醒：如果您在進行本教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解][頁面](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="adding-a-new-column-to-a-table"></a>將新的資料行加入至資料表

在本節中，您會將「出生日期」資料行加入 `Student` 和 `Instructor` 實體的 `Person` 基類。 接著，您會更新顯示講師資料的頁面，使其顯示新的資料行。

在*ContosoUniversity*專案中，開啟*Person.cs* ，並在 `Person` 類別的結尾處新增下列屬性（後面應該有兩個右大括弧）：

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample1.cs)]

接下來，請更新種子方法，讓它提供新資料行的值。 開啟*Migrations\Configuration.cs* ，並將開始 `var instructors = new List<Instructor>` 的程式碼區塊取代為下列包含出生日期資訊的程式碼區塊：

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample2.cs)]

在 ContosoUniversity 專案中，開啟 [ *default.aspx* ]，然後新增 [範本] 欄位以顯示出生日期。 將其新增至 [雇用日期] 和 [辦公室指派]：

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample3.aspx)]

（如果程式碼縮排無法同步處理，您可以按下 CTRL-K，然後按 CTRL-D 自動重新格式化檔案）。

建立解決方案，然後開啟 [**套件管理員主控台**] 視窗。 請確定 [ContosoUniversity] 仍然選取為 [**預設專案**]。

在 [**套件管理員主控台**] 視窗中，選取 [ **ContosoUniversity** ] 做為**預設專案**，然後輸入下列命令：

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample4.ps1)]

當此命令完成時，Visual Studio 會開啟定義新 `DbMigration` 類別的類別檔案，而在 `Up` 方法中，您可以看到建立新資料行的程式碼。

![AddBirthDate_migration_code](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image1.png)

建立解決方案，然後在 [**套件管理員主控台**] 視窗中輸入下列命令（請確定仍已選取 [ContosoUniversity] 專案）：

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample5.ps1)]

當命令完成時，請執行應用程式，然後選取 [講師] 頁面。 當頁面載入時，您會看到它有新的出生日期欄位。

[![Instructors_page_with_birth_date](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image3.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image2.png)

## <a name="deploying-the-database-update-to-the-test-environment"></a>將資料庫更新部署到測試環境

在**方案總管**選取 [ContosoUniversity] 專案。

在 Web 單鍵的 [**發行**] 工具列中，選取 [**測試**發行設定檔]，然後按一下 [**發佈 Web**]。 （如果工具列已停用，請在**方案總管**中選取 ContosoUniversity 專案）。

Visual Studio 會部署已更新的應用程式，且瀏覽器會開啟至首頁。 執行 [講師] 頁面，確認已成功部署更新。 當應用程式嘗試存取此頁面的資料庫時，Code First 會更新資料庫架構，並執行 `Seed` 方法。 當頁面顯示時，您會看到 [預期的**出生日期] 資料**行中有日期。

[![Instructors_page_with_birth_date_Test](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image4.png)

## <a name="deploying-the-database-update-to-the-production-environment"></a>將資料庫更新部署至生產環境

您現在可以部署到生產環境。 唯一的差別在於，您將使用*應用程式\_離線的 .htm* ，以防止使用者存取網站，並在您部署變更時更新資料庫。 針對生產環境部署，請執行下列步驟：

- 將*應用程式\_離線 .htm*檔案上傳至生產網站。
- 在 Visual Studio 中，選擇 Web 單鍵 [**發行**] 工具列中的 [生產設定檔]，然後按一下 [**發佈 Web**]。
- 從生產網站刪除*應用程式\_離線 .htm*檔案。

> [!NOTE]
> 當您的應用程式在生產環境中使用時，您應該要執行備份計畫。 也就是，您應該定期將*School-Prod 的 .sdf*和*aspnet-Prod*檔案從生產網站複製到安全的儲存位置，而且您應該保留數個層代的備份。 當您更新資料庫時，您應該在變更之前立即建立備份複本。 然後，如果您犯了錯誤，而且在將它部署到生產環境之後卻找不到它，您仍然可以將資料庫復原到損毀之前的狀態。

當 Visual Studio 在瀏覽器中開啟首頁 URL 時，就會顯示 [ *\_離線的應用程式*] 頁面。 當您刪除*應用程式\_離線的 .htm*檔案之後，您可以再次流覽至您的首頁，以確認更新已成功部署。

[![Instructors_page_with_birth_date_Prod](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image7.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image6.png)

您現在已部署應用程式更新，其中包含對測試和生產環境的資料庫變更。 下一個教學課程會示範如何將您的資料庫從 SQL Server Compact 遷移至 SQL Server Express 和 SQL Server。

> [!div class="step-by-step"]
> [上一頁](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
> [下一頁](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
