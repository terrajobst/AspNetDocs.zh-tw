---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 應用程式：部署 SQL Server 資料庫更新-11/12 |Microsoft Docs
author: tdykstra
description: 這一系列的教學課程會示範如何使用 Visual Stu 部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案 。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 5e2bb092-cb22-4511-ad0a-22ae12dd99b3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
msc.type: authoredcontent
ms.openlocfilehash: 0894c0ac24737e66b6960ef3d48aa17f78c6aa1d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621059"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-sql-server-database-update---11-of-12"></a>使用 Visual Studio 或 Visual Web Developer 的 SQL Server Compact 部署 ASP.NET Web 應用程式：部署 SQL Server 資料庫更新-11/12

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載入門專案](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 這一系列的教學課程會示範如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，來部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案。 如果您安裝 Web 發佈更新，也可以使用 Visual Studio 2010。 如需此系列的簡介，請參閱[本系列的第一個教學](deployment-to-a-hosting-provider-introduction-1-of-12.md)課程。
> 
> 如需示範在 Visual Studio 2012 的 RC 版本後引進部署功能的教學課程，說明如何部署 SQL Server Compact 以外的 SQL Server 版本，並示範如何部署至 Windows Azure 網站，請參閱[使用 Visual Studio ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。

## <a name="overview"></a>概觀

本教學課程說明如何將資料庫更新部署至完整的 SQL Server 資料庫。 由於 Code First 移轉會執行更新資料庫的所有工作，因此程式與您在[部署資料庫更新](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)教學課程中所做的 SQL Server Compact 程式幾乎完全相同。

提醒：如果您在進行本教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解][頁面](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="adding-a-new-column-to-a-table"></a>將新的資料行加入至資料表

在本教學課程的這一節中，您將會進行資料庫變更和對應的程式碼變更，然後在 Visual Studio 中進行測試，以準備將它們部署至測試和生產環境。 變更牽涉到將 `OfficeHours` 資料行加入 `Instructor` 實體，並在**講師**網頁中顯示新資訊。

在 ContosoUniversity 專案中，開啟*Instructor.cs* ，並在 `HireDate` 和 `Courses` 屬性之間新增下列屬性：

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample1.cs)]

更新初始化運算式類別，使其植入具有測試資料的新資料行。 開啟*Migrations\Configuration.cs* ，並將開始 `var instructors = new List<Instructor>` 的程式碼區塊取代為下列包含新資料行的程式碼區塊：

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample2.cs)]

在 ContosoUniversity 專案中，開啟 [ *default.aspx* ]，然後在第一個 `GridView` 控制項的 [結束 `</Columns>`] 標籤之前，加入 office 小時的新範本欄位：

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample3.aspx)]

建置方案。

開啟 [**套件管理員主控台**] 視窗，然後選取 [ContosoUniversity] 做為**預設專案**。

輸入下列命令：

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample4.ps1)]

執行應用程式，然後選取 [**講師**] 頁面。 網頁需要比平常更長的時間才能載入，因為 Entity Framework 會重新建立資料庫，並植入測試資料。

[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)

## <a name="deploying-the-database-update-to-the-test-environment"></a>將資料庫更新部署到測試環境

當您使用 Code First 移轉時，用於將資料庫變更部署至 SQL Server 的方法，與 SQL Server Compact 的方式相同。 不過，您必須變更測試發行設定檔，因為它仍然設定為從 SQL Server Compact 遷移至 SQL Server。

第一個步驟是移除您在上一個教學課程中建立的連接字串轉換。 因為您會在發行設定檔中指定連接字串轉換，就像您在設定 [**封裝/發行 SQL** ] 索引標籤以進行遷移到 SQL Server 之前所做的一樣，因此不再需要這些設定。

開啟*web.config*檔案，並移除 `connectionStrings` 元素。 *Web.config*檔案中唯一剩餘的轉換，是 `appSettings` 元素中的 `Environment` 值。

現在您可以更新發行設定檔，併發布至測試環境。

開啟 [**發行 Web** wizard]，然後切換至 [**設定檔**] 索引標籤。

選取 [**測試**發行設定檔]。

選取 [設定] 索引標籤。

按一下 **[啟用新的資料庫發行增強功能**]。

在 [ **SchoolCoNtext**] 的 [連接字串] 方塊中，輸入您在上一個教學課程的*web.config 轉換檔案*中使用的相同值：

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample5.cmd)]

選取**執行 Code First 移轉（在應用程式啟動時執行）** 。 （在您的 Visual Studio 版本中，此核取方塊可能標示為 [套用**Code First 移轉**]）。

在 [ **DefaultConnection**] 的 [連接字串] 方塊中，輸入您在上一個教學課程的*web.config 轉換檔案*中使用的相同值：

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample6.cmd)]

將**更新資料庫**保留為已清除。

按一下 [發行]。

Visual Studio 會將程式碼變更部署至測試環境，並將瀏覽器開啟至 Contoso 大學首頁。

選取 [講師] 頁面。

當應用程式執行此頁面時，它會嘗試存取資料庫。 Code First 移轉檢查資料庫是否為最新的，並找出最近尚未套用的遷移。 Code First 移轉會套用最新的遷移、執行 `Seed` 方法，然後網頁會正常執行。 您會看到新的 [Office 小時] 資料行與植入的資料。

[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)

## <a name="deploying-the-database-update-to-the-production-environment"></a>將資料庫更新部署至生產環境

您也必須變更生產環境的發行設定檔。 在此情況下，您將移除現有的設定檔，並藉由匯入更新的 .publishsettings 檔案來建立一個新的。 更新的檔案將包含 Cytanium 之 SQL Server 資料庫的連接字串。

如您在部署到測試環境時所看到的，您不再需要在*web.config*轉換檔案中進行連接字串轉換。 開啟該檔案，並移除 `connectionStrings` 元素。 其餘的轉換適用于 `appSettings` 元素中的 `Environment` 值，以及限制對 Elmah 錯誤報表存取的 `location` 元素。

在您為生產環境建立新的發行設定檔之前，請下載更新過的 .publishsettings 檔案，方法與您稍早在[部署至生產環境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教學課程中所做的相同。 （在 [Cytanium] 控制台中，按一下 [**網站**]，然後按一下 [ **contosouniversity.com** ] 網站。 選取 [ **Web 發行**] 索引標籤，然後按一下 [**下載此網站的發行設定檔**]）。這麼做的原因是要在 .publishsettings 檔案中挑選資料庫連接字串。 第一次下載檔案時無法使用連接字串，因為您仍在使用 SQL Server Compact，而且尚未在 Cytanium 建立 SQL Server 資料庫。

現在您可以更新發行設定檔，併發布到生產環境。

開啟 [**發行 Web** wizard]，然後切換至 [**設定檔**] 索引標籤。

按一下 [**管理設定檔**]，然後刪除生產設定檔。

關閉 [**發行 Web** wizard] 以儲存此變更。

再次開啟 [**發佈 Web**嚮導]，然後按一下 [匯**入**]。

如果您使用的是暫存 URL，請在 [**連接**] 索引標籤上，將 [**目的地 URL** ] 變更為適當的值。

按 [ **下一步**]。

在 [**設定**] 索引標籤上，按一下 [**啟用新的資料庫發行增強功能**]。

在 [ **SchoolCoNtext**] 的 [連接字串] 下拉式清單中，選取 [Cytanium] 連接字串。

![Selecting_Cytanium_connection_string](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image5.png)

選取 **[執行 Code First 遷移（在應用程式啟動時執行）** ]。

在 [ **DefaultConnection**] 的 [連接字串] 下拉式清單中，選取 [Cytanium] 連接字串。

選取 [**設定檔**] 索引標籤，按一下 [**管理設定檔**]，然後將設定檔從 "Web Deploy contosouniversity.com" 重新命名為「生產」。

關閉發行設定檔以儲存變更，然後重新開啟。

按一下 [發行]。 （針對實際生產網站，您會將*應用程式\_離線 .htm*複製到生產環境，並在發行之前將它放在您的專案資料夾中，然後在部署完成時將它移除）。

Visual Studio 會將程式碼變更部署至測試環境，並將瀏覽器開啟至 Contoso 大學首頁。

選取 [講師] 頁面。

Code First 移轉以在測試環境中的相同方式更新資料庫。 您會看到新的 [Office 小時] 資料行與植入的資料。

![Instructors_page_with_OfficeHours_Prod](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image6.png)

您現在已成功部署包含資料庫變更的應用程式更新，並使用 SQL Server 資料庫。

## <a name="more-information"></a>更多資訊

這會完成這一系列的教學課程，將 ASP.NET web 應用程式部署到協力廠商裝載提供者。 如需這些教學課程中所涵蓋之任何主題的詳細資訊，請參閱 MSDN 網站上的[ASP.NET 部署內容對應](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx)。

## <a name="acknowledgements"></a>致謝

我想感謝下列人對本教學課程系列的內容做出重大貢獻：

- [Alberto Poblacion，MVP &amp; MCT，西班牙](https://mvp.support.microsoft.com/profile/Alberto)
- Jarod Ferguson，資料平臺開發 MVP，美國
- Microsoft 的 Mittal
- [Kristina Olson，Microsoft](https://blogs.iis.net/krolson/default.aspx)
- [Mike Pope，Microsoft](http://www.mikepope.com/blog/DisplayBlog.aspx)
- Mohit Srivastava，Microsoft
- [Raffaele Rialdi，義大利](http://www.iamraf.net/)
- [Rick Anderson，Microsoft](https://blogs.msdn.com/b/rickandy/)
- [Sayed Hashimi，Microsoft](http://sedodream.com/default.aspx)（twitter： [@sayedihashimi](http://twitter.com/sayedihashimi)）
- [Scott Hanselman](http://www.hanselman.com/blog/) （twitter： [@shanselman](http://twitter.com/shanselman)）
- [Scott Hunter，Microsoft](https://blogs.msdn.com/b/scothu/) （twitter： [@coolcsh](http://twitter.com/coolcsh)）
- [Srđan Božović，塞爾維亞](http://msforge.net/blogs/zmajcek/)
- [Vishal Joshi，Microsoft](http://vishaljoshi.blogspot.com/) （twitter： [@vishalrjoshi](http://twitter.com/vishalrjoshi)）

> [!div class="step-by-step"]
> [上一頁](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
> [下一頁](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)
