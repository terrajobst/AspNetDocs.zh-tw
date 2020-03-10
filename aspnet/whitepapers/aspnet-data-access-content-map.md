---
uid: whitepapers/aspnet-data-access-content-map
title: ASP.NET 資料存取-建議的資源 |Microsoft Docs
author: rick-anderson
description: 本主題提供有關如何在 ASP.NET web 應用程式中存取資料的檔資源連結，主要是使用 Entity Framework 和 SQL Se 。
ms.author: riande
ms.date: 07/25/2013
ms.assetid: f8157be1-4ab9-469e-ad3a-0ccc80b56c00
msc.legacyurl: /whitepapers/aspnet-data-access-content-map
msc.type: content
ms.openlocfilehash: 357851f195bf233c7c34a32bd156e4408d3e1b24
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78633130"
---
# <a name="aspnet-data-access---recommended-resources"></a>ASP.NET 資料存取 - 建議資源

> 本主題提供有關如何在 ASP.NET web 應用程式中存取資料的檔資源連結，主要是使用 Entity Framework 和 SQL Server。
> 
> 如果您知道絕佳的 blog 文章、 [stackoverflow](http://stackoverflow.com)執行緒或任何其他有用的連結，請傳送含有連結的[電子郵件給我們](mailto:aspnetue@microsoft.com?subject=Data Access Content Map)。
> 
> 上次更新4/3/2014

此主題包括下列各節：

- [在 ASP.NET 中使用資料存取消費者入門](#gettingstarted)
- [使用 Entity Framework](#ef)

    - [使用 Entity Framework Code First](#cf)
    - [使用 Entity Framework Code First 移轉](#efcfmigrations)
    - [使用 Entity Framework Database First 或 Model First （EF 設計工具）](#efdbf)
    - [載入 Entity Framework 中的相關資料（消極式載入、積極式載入和明確載入）](#efrelateddata)
    - [優化 Entity Framework 效能](#optimizingef)
    - [處理 Entity Framework 應用程式中的平行存取](#efconcurrency)
    - [關於 Entity Framework 的書籍](#efbooks)
    - [其他 Entity Framework 資源](#otherefresources)
- [ASP.NET Web Forms 應用程式中的資料系結](#wfdatabinding)

    - [使用 Web form 模型系結](#wfmodelbinding)
    - [使用 Web Forms 資料來源控制項](#wfdsc)
    - [使用 Web Forms 資料繫結控制項和資料系結運算式](#wfdbc)
- [使用 SQL Server 資料庫](#sqlserver)

    - [使用 SQL Server Express LocalDB 資料庫](#sslocaldb)
    - [使用 SQL Server Express 資料庫](#sse)
    - [使用 Windows Azure SQL Database](#ssdb)
    - [選擇 SQL Server 和 Windows Azure SQL Database](#ssdbchoosing)
- [使用 NoSQL 資料庫管理系統](#nosql)
- [在 ASP.NET 應用程式中使用 LINQ 查詢](#linq)
- [使用動態資料的樣板](#dd)
- [保護資料存取](#securing)
- [優化資料存取效能](#optimizingdataaccess)
- [部署資料庫](#deploying)
- [透過 Web 服務存取資料](#webservice)
- [其他資源](#additional)

<a id="gettingstarted"></a>

## <a name="getting-started-with-data-access-in-aspnet"></a>在 ASP.NET 中使用資料存取消費者入門

- [資料儲存體選項（使用 Windows Azure 建立真實世界的雲端應用程式）](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md)。 關於針對雲端進行開發的電子書章節。 引進了 NoSQL 資料庫，這是許多熟悉關係資料庫的開發人員通常會忽略的替代方法。 提供有關選擇關聯式或 NoSQL，或選擇特定平臺時應考慮之事項的指導方針。
- [ASP.NET 資料存取選項](https://msdn.microsoft.com/library/ms178359.aspx)（MSDN）。 適用于 ASP.NET 關係資料庫的資料存取選項簡介，以及如何選擇適用于您案例的平臺和存取方法的指引。
- [關係資料庫](http://en.wikipedia.org/wiki/Relational_database)。 維琪百科）。 如果您尚未使用關係資料庫，請參閱此頁面，以取得關係資料庫術語和概念的簡介。 如需 SQL Server 的簡介，請參閱本主題稍後的[使用 SQL Server 資料庫](#sqlserver)。

<a id="ef"></a>

## <a name="using-the-entity-framework"></a>使用 Entity Framework

- [Entity Framework 開發方法](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)（MSDN）。 如何選擇 Entity Framework 開發方法的指引 Database First、Model First 或 Code First。

<a id="cf"></a>

### <a name="using-entity-framework-code-first"></a>使用 Entity Framework Code First

下列教學課程提供可下載的範例應用程式：

- [使用 MVC 5 與 EF 6 消費者入門](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 涵蓋範圍廣泛的 Entity Framework Code First 案例，包括遷移和 EF 6 功能，例如連線復原、命令攔截和非同步。 這是[EF 5/MVC 4 系列](../mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)的更新版本。 先前的系列包含儲存機制的教學課程，以及未包含在新數列中的工作單位模式。
- [ASP.NET MVC 5 簡介](../mvc/overview/getting-started/introduction/getting-started.md)。 涵蓋範圍較窄的 Entity Framework Code First 案例，但會更完整地介紹 MVC 功能。
- [模型系結和 Web 表單](https://go.microsoft.com/fwlink/?LinkId=286117)。 在 Web Forms 應用程式中使用 Code First。
- [使用 ASP.NET 4.5 Web Forms 消費者入門](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)。 Web form 的簡介，其中涵蓋一些 Code First。 使用模型系結。
- [MVC 音樂存放區](../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1.md)。 會在同時執行成員資格和授權的電子商務 MVC 3 應用程式中使用 Code First。 此處使用的 MVC 版本和 ASP.NET 成員資格（驗證和授權）已過期;如需有關 ASP.NET 成員資格的最新資訊，請參閱[https://asp.net/identity](https://asp.net/identity)。

其他資源：

- [Entity Framework Code First 到現有的資料庫](https://msdn.microsoft.com/data/jj200620)。 期. 示範如何搭配現有資料庫使用 Code First 的影片和逐步解說。
- [資料開發人員中心-Entity Framework](https://msdn.microsoft.com/data/ef)。 期. 如需 Entity Framework Entity Framework 小組所建立和維護之檔的指南，請參閱[開始](https://msdn.microsoft.com/data/ee712907)使用連結。

另請參閱本主題稍後[的有關 Entity Framework](#efbooks)和[其他 Entity Framework 資源](#otherefresources)的書籍。

<a id="efcfmigrations"></a>

### <a name="using-entity-framework-code-first-migrations"></a>使用 Entity Framework Code First 移轉

以上所列的大部分 Code First 教學課程涵蓋了遷移。 另請參閱下列資源。

- [使用 Visual Studio 的 ASP.NET Web 部署](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)。 2部分教學課程系列，說明如何使用 Code First 移轉來部署資料庫。
- 將[具有成員資格、OAuth 和 SQL Database 的 Secure ASP.NET MVC 5 應用程式部署到 Windows Azure 網站](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 Microsoft Azure）。 如何使用遷移將成員資格和應用程式資料部署至 Azure。
- [Visual Studio 和 ASP.NET 的 Web 部署總覽](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment)。 如需如何將 Code First 移轉整合至 Visual Studio web 部署功能的說明，請參閱**在 Visual Studio 中設定資料庫部署**一節。
- [資料開發人員中心-Code First 移轉](https://msdn.microsoft.com/data/jj591621)（MSDN）。 Entity Framework 小組的遷移檔。
- [遷移螢幕錄製影片系列](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)。 EF blog）。 Code First 移轉中的三個 advanced 主題影片。
- [ASP.NET Web Pages 網站的 Code First 移轉](http://www.mikesdotnetting.com/Article/217/Code-First-Migrations-With-ASP.NET-Web-Pages-Sites)。 Mikesdotnetting blog）。 示範如何藉由將資料內容放在 Visual Studio 類別庫專案中，使用 ASP.NET Web Pages 網站的 Code First 遷移。

<a id="efdbf"></a>

### <a name="using-entity-framework-database-first-or-model-first-the-ef-designer"></a>使用 Entity Framework Database First 或 Model First （EF 設計工具）

- [使用 MVC 5 的 Entity Framework 6 Database First 消費者入門](../mvc/overview/getting-started/database-first-development/setting-up-database.md)。 在伺服器總管中執行腳本來建立資料庫，然後使用 Entity Framework 設計工具來建立資料模型。 示範如何建立簡單的 CRUD 網頁，針對其他資料處理函式，您可以遵循其中一個 Code First 教學課程，因為所有 EF 工作流程都會使用相同的 DbCoNtext API。

下列是較舊的資源。 如果您想要使用4.0 版的 Entity Framework，而且想要在 Web Forms 應用程式中使用資料來源控制項來進行資料系結，則這些方法很有用。

- [Entity Framework 4.0 的消費者入門](../web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)。 示範如何使用**EntityDataSource**控制項。
- [繼續進行 Entity Framework](../web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)（說明如何使用**ObjectDataSource**控制項。 包含並行處理的教學課程、EF 效能的教學課程，以及 EF 4.0 中新功能的教學課程。

<a id="efrelateddata"></a>

### <a name="handling-related-data-in-entity-framework-lazy-loading-eager-loading-and-explicit-loading"></a>處理 Entity Framework 中的相關資料（消極式載入、積極式載入和明確載入）

- [在 ASP.NET MVC 應用程式中使用 Entity Framework 讀取相關資料](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)。 Code First，MVC 範例應用程式。 所顯示的方法也適用于 Web 表單模型系結和 Database First 工作流程。
- [資料開發人員中心-載入相關實體](https://msdn.microsoft.com/data/jj574232)（MSDN）。 有關載入相關資料的 Entity Framework 小組檔。

<a id="optimizingef"></a>

### <a name="optimizing-entity-framework-performance"></a>優化 Entity Framework 效能

- [ASP.NET 應用程式的 Advanced Entity Framework 案例](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application.md)。 示範如何執行您自己的 SQL 語句或呼叫您自己的預存程式、如何停用變更偵測，以及如何在儲存變更時停用驗證。
- [Entity Framework 5 的效能考慮](https://msdn.microsoft.com/data/hh949853)（MSDN）。
- [效能考慮（Entity Framework）](https://msdn.microsoft.com/library/cc853327) （MSDN）。
- [使用 ASP.NET Web 應用程式中的 Entity Framework，將效能最大化](../web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)。 適用于 Entity Framework 4.0。
- 另請參閱本主題稍後的[優化 ASP.NET 資料存取](#optimizingdataaccess)。

<a id="efconcurrency"></a>

### <a name="handling-concurrency-in-an-entity-framework-application"></a>處理 Entity Framework 應用程式中的平行存取

- [使用 ASP.NET MVC 應用程式中的 Entity Framework 來處理並行](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)存取。 使用 MVC 範例應用程式 Code First DbCoNtext API。
- [資料開發人員中心-開放式平行存取模式](https://msdn.microsoft.com/data/jj592904)（MSDN）。 Entity Framework 小組的並行檔。
- [使用 ASP.NET Web 應用程式中的 Entity Framework 來處理並行](../web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)存取。 適用于 Entity Framework 4.0。 使用 Web Forms 範例應用程式 Database First、ObjectCoNtext API。

<a id="efrepository"></a><a id="efbooks"></a>

### <a name="books-about-the-entity-framework"></a>關於 Entity Framework 的書籍

- 程式[設計 Entity Framework： DbCoNtext](http://shop.oreilly.com/product/0636920022237.do) By Julie Lerman 和 Rowan 莎莎。
- 程式[設計 Entity Framework：](http://shop.oreilly.com/product/0636920022220.do) Julie Lerman 和 Rowan 莎莎的 Code First。

這兩本書皆以目前的建議技術為最新狀態。 除了可在網際網路上使用的資訊之外，它們還提供更全面但容易追蹤的 Entity Framework 簡介。 另一本書是 Julie Lerman 的程式[Entity Framework 設計](http://shop.oreilly.com/product/9780596807252.do)，它更大、更完整，但它的功能較舊，而其中許多所涵蓋的技術，不再是使用 Entity Framework 的建議方式。 另請參閱 MSDN 網站上的[資料開發人員中心](https://msdn.microsoft.com/data/aa937716)的 Entity Framework 小組建議的書籍清單-書籍。

<a id="otherefresources"></a>

### <a name="other-entity-framework-resources"></a>其他 Entity Framework 資源

- [Entity Framework （ADO.NET）小組的 blog](https://blogs.msdn.com/b/adonet/)。 最新資訊的其中一個最佳資源，以及新增強功能的公告。 如需其他 EF 相關的 blog，請參閱[開始使用 Entity Framework](https://msdn.microsoft.com/data/ee712907)的 Blogroll。
- [MSDN 雜誌](https://msdn.microsoft.com/magazine/default.aspx)。 請參閱**資料點**欄，這通常是與 Entity Framework 相關的主題。

<a id="wfdatabinding"></a>

## <a name="data-binding-in-aspnet-web-forms-applications"></a>ASP.NET Web Forms 應用程式中的資料系結

- [ASP.NET Web Forms 資料存取選項](https://msdn.microsoft.com/library/jj822927.aspx)（MSDN）<a id="wfmodelbinding"></a>。

<a id="wfmodelbinding"></a>

### <a name="using-web-forms-model-binding"></a>使用 Web form 模型系結

- [模型系結和 Web 表單](https://go.microsoft.com/fwlink/?LinkId=286117)。 使用 EF Code First 的教學課程系列。
- [Web Form 模型系結第1部分：選取資料](https://weblogs.asp.net/scottgu/archive/2011/09/06/web-forms-model-binding-part-1-selecting-data-asp-net-vnext-series.aspx)（Scott Guthrie 的 blog）。 在這些較舊的 blog 文章中，目前名為 ItemType 的屬性名為 ModelType，但其包含的資訊是有效的。
- [Web Form 模型系結第2部分：篩選資料](https://weblogs.asp.net/scottgu/archive/2011/09/12/web-forms-model-binding-part-2-filtering-data-asp-net-vnext-series.aspx)（Scott Guthrie 的 blog）。
- [Web Form 模型系結第3部分：更新和驗證](https://weblogs.asp.net/scottgu/archive/2011/10/30/web-forms-model-binding-part-3-updating-and-validation-asp-net-4-5-series.aspx)（Scott Guthrie 的 blog）。
- [ASP.NET 4.5 Web Form 模型](../web-forms/videos/aspnet-web-forms-vnext/aspnet-45-web-forms-model-binding.md)系結。 （影片）。
- [模型系結第1部分-選取資料](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-1-selecting-data.md)（影片）。
- [模型系結第2部分-篩選](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-2-filtering.md)（影片）。
- [具有 ASP.NET 4.5 Web form 的消費者入門-顯示資料項目和詳細資料](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md)。

<a id="wfdsc"></a>

### <a name="using-web-forms-data-source-controls"></a>使用 Web Forms 資料來源控制項

- [資料來源 Web 服務器控制項](https://msdn.microsoft.com/library/ms247258.aspx)（MSDN）。
- [宣佈發行動態資料提供者和適用于 Entity Framework 6 的 EntityDataSource 控制項](https://blogs.msdn.com/b/webdev/archive/2014/02/28/announcing-the-release-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx)（Microsoft Web 開發 blog）。

<a id="wfdbc"></a>

### <a name="using-web-forms-data-bound-controls-and-data-binding-expressions"></a>使用 Web Forms 資料繫結控制項和資料系結運算式

- [模型系結和 Web 表單](https://go.microsoft.com/fwlink/?LinkId=286117)。 使用 EF Code First 的教學課程系列。
- [具有 ASP.NET 4.5 Web form 的消費者入門-顯示資料項目和詳細資料](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md)。
- [強型別資料控制](https://weblogs.asp.net/scottgu/archive/2011/09/02/strongly-typed-data-controls-asp-net-vnext-series.aspx)（Scott Guthrie 的 blog）。
- [強型別資料控制](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md)（影片）。
- [ASP.NET 4.5 Web Forms 強型別資料控制](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md)（影片）。
- [資料系結的 Web 服務器控制項](https://msdn.microsoft.com/library/ms228214.aspx)（MSDN）。
- [資料系結運算式總覽](https://msdn.microsoft.com/library/ms178366.aspx)（MSDN）。 此頁面僅涵蓋**Eval**和**Bind**;尚未更新為包含**專案**和**BindItem**。

<a id="sqlserver"></a>

## <a name="working-with-sql-server-databases"></a>使用 SQL Server 資料庫

- [SQL Server 資料庫功能](https://msdn.microsoft.com/library/hh230827.aspx)（MSDN）。 如需各種 SQL Server 主題的一般簡介，請參閱目錄中這個專案底下的專案。
- [SQL Server 版本](https://msdn.microsoft.com/library/ms178359.aspx#sqlserver)（MSDN）。 可用 SQL Server 版本的摘要，其中包含每一項的詳細資訊連結。）
- [SQL Server ASP.NET Web 應用程式的連接字串](https://msdn.microsoft.com/library/jj653752.aspx)（MSDN）。
- [使用適用于 ASP.NET Web 應用程式的 SQL Server Compact](https://msdn.microsoft.com/library/ms247257.aspx) （MSDN）。
- [Microsoft SQL Server：資料庫產品範例](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md)。 範例 AdventureWorks 資料庫。
- [安裝範例資料庫](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md)。 除了此處所示的方法之外，您也可以將其中一個範例 .mdf 檔案下載至 Web 專案的應用程式\_Data 資料夾，將資料庫轉換為 LocalDB，並建立 LocalDB 連接字串。 如需如何執行此動作的詳細資訊，請參閱[如何：升級為 LocalDB](https://msdn.microsoft.com/library/hh873188.aspx)。

另請參閱下列有關使用 SQL Server Express 和 LocalDB 的章節，以及在 SQL Server 和 SQL Database 之間做選擇。

<a id="sslocaldb"></a>

### <a name="working-with-sql-server-express-localdb-databases"></a>使用 SQL Server Express LocalDB 資料庫

- [SQL Server Express 2012 LocalDB](https://msdn.microsoft.com/library/hh510202(v=sql.110).aspx) （MSDN）。 LocalDB 的官方 MSDN 簡介。
- [SQL Server ASP.NET Web 應用程式的連接字串](https://msdn.microsoft.com/library/jj653752.aspx)（MSDN）。
- [如何：升級至 LocalDB](https://msdn.microsoft.com/library/hh873188.aspx) （MSDN）。 如何將 .mdf 檔案從舊版的 SQL Server Express 遷移至 LocalDB。 如果您下載其中一個[SQL Server 2012 範例資料庫](https://go.microsoft.com/fwlink/?linkid=117483)，也必須執行此程式。
- [介紹 LocalDB，這是改良的 SQL Express](https://go.microsoft.com/fwlink/?LinkId=234375) （SQL Server Express 的 blog）。 在建立 LocalDB 時，會有更多背景，而不是 MSDN 所包含的。
- [LocalDB：我的資料庫在哪裡？](https://go.microsoft.com/fwlink/?LinkId=234376) （SQL Server Express 的 blog）。 LocalDB 資料庫檔案建立位置的相關資訊。
- [使用 LocalDB 搭配完整 IIS，第1部分：使用者設定檔](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-1-user-profile.aspx)（SQL Server Express blog）。 LocalDB 並非設計來與 IIS 搭配使用。 這一系列的 blog 文章會說明問題和一些因應措施。

<a id="sse"></a>

### <a name="working-with-sql-server-express-databases"></a>使用 SQL Server Express 資料庫

- [SQL Server ASP.NET Web 應用程式的連接字串](https://msdn.microsoft.com/library/jj653752.aspx)（MSDN）。 如果您使用 AttachDBFileName 連接字串設定搭配 SQL Server Express，請特別參閱本頁的使用者實例一節。
- [如何取得本機 SQL Server Express 2008](https://blogs.msdn.com/b/sqlexpress/archive/2010/02/23/how-to-take-ownership-of-your-local-sql-server-2008-express.aspx) （SQL Server Express blog）的擁有權。 因為您不是 SQL Server Express 實例的系統管理員，所以常見的問題無法使用 SQL Server Express 資料庫。 根據預設，只有安裝 SQL Server Express 的人員是系統管理員。 如果您是電腦上的系統管理員，此 blog 會說明如何讓自己成為 SQL Server Express 系統管理員。
- [我的 ASP.NET web 應用程式可以在生產環境中使用 SQL Server Express 的資料庫嗎？](https://msdn.microsoft.com/library/jj653753.aspx#sql_express_in_production) （MSDN）。

<a id="ssdb"></a>

### <a name="working-with-windows-azure-sql-database"></a>使用 Windows Azure SQL Database

- 將[具有成員資格、OAuth 和 SQL Database 的安全 ASP.NET MVC 應用程式部署到 Windows Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)網站（Microsoft Azure 網站）。
- [SQL 資料庫](https://docs.microsoft.com/azure/sql-database/)（Microsoft Azure 網站）。 快速入門教學課程和操作指南。
- [Windows Azure SQL Database](https://msdn.microsoft.com/library/windowsazure/ee336279.aspx) （MSDN）。 MSDN 中 SQL Database 目錄的最上層節點。
- [Windows Azure SQL Database Technet Wiki 文章索引](https://social.technet.microsoft.com/wiki/contents/articles/2267.windows-azure-sql-database-technet-wiki-articles-index-en-us.aspx)（Microsoft technet 網站）。
- [暫時性錯誤處理應用程式區塊](https://msdn.microsoft.com/library/hh680934(v=PandP.50).aspx)。 一種架構，可讓您處理因節流而產生的暫時性網路錯誤和連接錯誤。 可在 NuGet 套件中取得： [Enterprise Library 5.0-暫時性錯誤處理應用程式區塊](http://nuget.org/packages/EnterpriseLibrary.WindowsAzure.TransientFaultHandling)。
- [SQL Database 和 Entity Framework 的消費者入門](https://msdn.microsoft.com/data/jj556244)（MSDN）。
- [Windows Azure 訓練套件](https://www.microsoft.com/download/details.aspx?id=8396)（Microsoft 下載中心）。 包含 SQL Database 的實際操作實驗室。
- [Windows Azure SQL Database 的社區論壇](https://social.msdn.microsoft.com/Forums/ssdsgetstarted/threads)。
- [移至 Windows Azure SQL Database](https://msdn.microsoft.com/library/ff803375.aspx) （MSDN）。 Microsoft 模式和實務團隊提供全方位端對端案例的一章。 涵蓋您可能想要遷移的原因，以及如何從 SQL Server 遷移至 SQL Database。
- [將 SQL Server 資料庫移轉至 Windows Azure SQL Database](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx) （MSDN）。
- [SQL Database 遷移 Wizard](http://sqlazuremw.codeplex.com/)。 一種開放原始碼工具，可讓您將資料庫移入和移出 SQL Database。

<a id="ssdbchoosing"></a>

### <a name="choosing-between-sql-server-and-windows-azure-sql-database"></a>選擇 SQL Server 和 Windows Azure SQL Database

- [比較 SQL Server 與 Windows Azure SQL Database](https://social.technet.microsoft.com/wiki/contents/articles/996.compare-sql-server-with-windows-azure-sql-database-en-us.aspx) （Microsoft TechNet 網站）。
- [將資料移轉至 Windows Azure SQL Database：工具和技術](https://msdn.microsoft.com/library/windowsazure/hh694043.aspx)（MSDN）。 包含比較 SQL Server 與 SQL Database 的區段，並提供何時從 SQL Server 遷移至 SQL Database 的指引。
- [Windows Azure SQL Database 傳遞指南](https://social.technet.microsoft.com/wiki/contents/articles/3398.windows-azure-sql-database-delivery-guide-en-us.aspx)（Microsoft TechNet 網站）。
- [SQL Server 功能限制（Windows Azure SQL Database）](https://msdn.microsoft.com/library/windowsazure/ff394115.aspx) （MSDN）。
- [Windows Azure 表格儲存體和 windows Azure SQL Database 比較和對比](https://msdn.microsoft.com/library/jj553018.aspx)（MSDN）。 對於您部署至 Windows Azure 的應用程式，Windows Azure 資料表儲存體可能是 Windows Azure SQL Database 的替代方案。 本主題可協助您在這些替代方案之間做出決定。
- [Windows Azure SQL Database](https://msdn.microsoft.com/library/windowsazure/ee336279) （MSDN）。
- [方針和限制（Windows Azure SQL Database）](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx)

<a id="nosql"></a>

## <a name="working-with-nosql-database-management-systems"></a>使用 NoSQL 資料庫管理系統

- [Windows Azure 資料服務](https://www.windowsazure.com/develop/net/data/)（Microsoft Azure 網站）。 請參閱[表格服務功能指南](https://docs.microsoft.com/azure/)和頁面的**Big Data**一節。
- [使用儲存體資料表、佇列和 blob （Microsoft Azure 網站） ASP.NET 多層式應用程式](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)。 具有可下載範例應用程式的端對端教學課程，使用 Windows Azure 儲存體 NoSQL 資料表。

<a id="linq"></a>

## <a name="using-linq-queries-in-aspnet-applications"></a>在 ASP.NET 應用程式中使用 LINQ 查詢

- [ASP.NET 資料存取選項](https://msdn.microsoft.com/library/ms178359.aspx#linq)（MSDN）。 包含 LINQ 簡介。
- [LINQ 訓練](http://www.misfitgeek.com/windows-client-linq-training-videos-20/)影片（Joe Stagner 的 blog）。
- [具有動態 LINQ 資源連結的 ASP.NET 論壇執行緒](https://forums.asp.net/p/1961037/5601994.aspx?Please+suggest+good+books+so+that+one+can+write+and+understand+dynamic+linq)。

<a id="dd"></a>

## <a name="using-dynamic-data-scaffolding"></a>使用動態資料的樣板

- [動態資料專案範本](https://msdn.microsoft.com/library/jj822927.aspx#dynamicdata)（MSDN）。 使用動態資料專案的指引。
- [ASP.NET 動態資料](https://msdn.microsoft.com/library/ee845452.aspx)（MSDN）。

<a id="securing"></a>

## <a name="securing-data-access"></a>保護資料存取

- [保護 ASP.NET （MSDN）中的資料存取](https://msdn.microsoft.com/library/ms178375.aspx)。
- [安全性考慮（Entity Framework）](https://msdn.microsoft.com/library/cc716760.aspx) （MSDN）。
- [如何：在使用資料來源控制項時保護連接字串的安全](https://msdn.microsoft.com/library/ms178372.aspx)（MSDN）。

<a id="optimizingdataaccess"></a>

## <a name="optimizing-data-access-performance"></a>優化資料存取效能

- [ASP.NET 效能總覽](https://msdn.microsoft.com/library/cc668225.aspx)（MSDN）。
- [ASP.NET Caching](https://msdn.microsoft.com/library/xsbfdd8c.aspx) （MSDN）。
- [改善 ASP.NET 效能](https://msdn.microsoft.com/library/ff647787)（MSDN）。 此頁面頂端有「已淘汰的內容」警告，但大部分的資訊仍然相關，而且沒有可比較的更新資源。
- [改善 SQL Server 效能](https://msdn.microsoft.com/library/ff647793)（MSDN）。 與上一個連結相同的批註。

另請參閱本主題稍早的[優化 Entity Framework 效能](#optimizingef)。

<a id="deploying"></a>

## <a name="deploying-a-database"></a>部署資料庫

- [ASP.NET Web 部署-建議的資源](aspnet-web-deployment-content-map.md)（MSDN）。

<a id="webservice"></a>

## <a name="accessing-data-through-a-web-service"></a>透過 Web 服務存取資料

- [透過 Web 服務](https://msdn.microsoft.com/library/ms178359.aspx#webservice)（MSDN）存取資料。 有關何時使用 Web API 與 WCF 的指引。
- [ASP.NET Web API 的消費者入門](../web-api/index.md)。
- [WCF Data Services](https://msdn.microsoft.com/data/bb931106) （MSDN）。

<a id="additional"></a>

## <a name="additional-resources"></a>其他資源

- [ASP.NET 資料存取常見問題](https://msdn.microsoft.com/library/jj653753.aspx)（MSDN）。
- [ASP.NET Web Forms 教學課程-資料](../web-forms/overview/data-access/index.md)。 大部分的教學課程都是相當舊的;請務必先閱讀[ASP.NET 資料存取選項](https://msdn.microsoft.com/library/ms178359.aspx)和[資料儲存選項（使用 Windows Azure 建立真實世界的雲端應用程式）](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md) ，如此一來，您就不會太遠進入不適合您案例的資料存取方法。
- [ASP.NET MVC 內容對應](../mvc/overview/getting-started/recommended-resources-for-mvc.md)。
- [ASP.NET Web Pages 教學課程-資料](../web-pages/overview/data/index.md)。
- [存取 Visual Studio （MSDN）中的資料](https://msdn.microsoft.com/library/wzabh8c4.aspx)。 提供類似于此內容對應的連結清單，但焦點在 Visual Studio 而不是 ASP.NET。
