---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-the-production-web-application-to-use-the-production-database-cs
title: 設定生產環境 Web 應用程式使用生產資料庫（C#） |Microsoft Docs
author: rick-anderson
description: 如先前的教學課程中所述，在開發與生產環境之間，設定資訊的差異並不罕見。 這是 es 。
ms.author: riande
ms.date: 04/23/2009
ms.assetid: 0177dabd-d888-449f-91b2-24190cf5e842
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-the-production-web-application-to-use-the-production-database-cs
msc.type: authoredcontent
ms.openlocfilehash: 89941bb6db52316a259ad5f5577721e36f19bd84
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78631527"
---
# <a name="configuring-the-production-web-application-to-use-the-production-database-c"></a>設定生產環境 Web 應用程式使用生產資料庫 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_08_CS.zip)或[下載 PDF](https://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial08_DBConfig_cs.pdf)

> 如先前的教學課程中所述，在開發與生產環境之間，設定資訊的差異並不罕見。 這特別適用于資料驅動的 web 應用程式，因為開發與生產環境之間的資料庫連接字串不同。 本教學課程會探索如何設定生產環境，以更詳細的方式包含適當的連接字串。

## <a name="introduction"></a>簡介

資料驅動的 web 應用程式通常會在開發時使用不同的資料庫，而不是在生產環境中。 對於由 web 主機服務提供者裝載並在本機開發的應用程式，開發資料庫通常會位於開發人員的電腦上，而生產資料庫則裝載于虛擬主機公司設施的資料庫伺服器上。 部署資料驅動 web 應用程式時，需要將開發資料庫複製到實際執行的資料庫伺服器。 在上一個教學課程中，我們探討了完成此步驟的方法。

Web 應用程式會使用*連接字串*中的資訊來建立與資料庫的連接。 連接字串通常會儲存在 `Web.config`中，會指定資料庫伺服器名稱、資料庫名稱、安全性內容和其他資訊。 由於 web 應用程式所使用的資料庫取決於 web 應用程式是在開發或生產環境中執行，因此這兩個環境之間的連接字串必須不同。

在開發和生產環境之間，設定資訊的差異並不罕見。 *開發與生產*教學課程的常見設定差異討論了在這兩個環境之間維護個別設定資訊的技巧，以及有關資料庫連接字串的簡短討論。 本教學課程會探索如何設定生產環境，以更詳細的方式包含適當的連接字串。

## <a name="examining-the-connection-string-information"></a>檢查連接字串資訊

書籍審查 web 應用程式所使用的連接字串會儲存在應用程式的設定檔中，`Web.config`。 `Web.config` 包含儲存連接字串的特殊區段，名為[&lt;connectionStrings&gt;](https://msdn.microsoft.com/library/bf7sd233.aspx)的恰如其。 書籍審查網站的 `Web.config` 檔案中，有一個在此區段中定義的連接字串，名為 `ReviewsConnectionString`：

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-cs/samples/sample1.xml)]

連接字串-資料來源 = .\SQLEXPRESS;AttachDbFilename = |DataDirectory | \Reviews.mdf; 整合式安全性 = True;User Instance = True-由數個選項和值所組成，並以分號分隔選項/值組，並以等號分隔每個選項和值。 此連接字串中使用的四個選項包括：

- `Data Source`-指定資料庫伺服器的位置和資料庫伺服器實例名稱（如果有的話）。 `.\SQLEXPRESS`的值是一個範例，其中有資料庫伺服器和實例名稱。 此期間指定資料庫伺服器與應用程式位於相同的電腦上;實例名稱為 `SQLEXPRESS`。
- `AttachDbFilename`-指定資料庫檔案的位置。 值包含預留位置 `|DataDirectory|`，它會在執行時間解析為應用程式 `App_Data` 資料夾的完整路徑。
- `Integrated Security`-布林值，指出連接到資料庫（false）或目前 Windows 帳號憑證（true）時，是否要使用指定的使用者名稱/密碼。
- `User Instance`-SQL Server Express 版本特有的設定選項，表示是否允許本機電腦上的非系統管理使用者連接及連接到 SQL Server Express Edition 資料庫。 如需此設定的詳細資訊，請參閱[SQL Server Express 的使用者實例](https://msdn.microsoft.com/library/ms254504.aspx)。

允許的連接字串選項取決於您所連接的資料庫，以及所使用的 ADO.NET 資料庫提供者。 例如，用於連接到 Microsoft SQL Server 資料庫的連接字串，與用來連接到 Oracle 資料庫的連接字串不同。 同樣地，使用 SqlClient 提供者連接到 Microsoft SQL Server 資料庫時，會使用與使用 OLE DB 提供者時不同的連接字串。

您可以手動使用[ConnectionStrings.com](http://www.connectionstrings.com/)之類的網站來建立資料庫連接字串，以取得可用選項的資源。 不過，較簡單的方法是將資料庫新增至 Visual Studio 中的伺服器總管，然後從屬性視窗抓取連接字串。 讓我們使用這個第二種技術來建立實際執行資料庫伺服器的連接字串。

開啟 Visual Studio，然後流覽至 [伺服器總管] 視窗（在 Visual Web Developer 中，此視窗稱為資料庫總管）。 以滑鼠右鍵按一下 [資料連線] 選項，然後從內容功能表中選擇 [加入連接] 選項。 這會顯示如 [圖 1] 所示的 wizard。 選擇適當的資料來源，然後按一下 [繼續]。

[![選擇將新的資料庫加入至伺服器總管](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image2.jpg)](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image1.jpg) 

**圖 1**：選擇將新的資料庫新增至伺服器總管（[按一下以查看完整大小的影像](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image3.jpg)）

接下來，指定各種資料庫連接資訊（請參閱 [圖 2]）。 當您向虛擬主機公司註冊時，他們應該已提供有關如何連接到資料庫的資訊-資料庫伺服器名稱、資料庫名稱、用來連接資料庫的使用者名稱和密碼等等。 輸入此資訊之後，請按一下 [確定] 以完成此嚮導，並將資料庫新增至伺服器總管。

[![指定資料庫連接資訊](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image5.jpg)](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image4.jpg) 

**圖 2**：指定資料庫連接資訊（[按一下以查看完整大小的影像](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image6.jpg)）

生產環境資料庫現在應該會列在伺服器總管中。 從 伺服器總管選取資料庫，然後移至 屬性視窗。 您會在這裡找到名為 [連接字串] 的屬性與資料庫的連接字串。 假設您在生產環境和 SqlClient 提供者上使用 Microsoft SQL Server 資料庫，您的連接字串看起來應該如下所示：

<strong>資料來源 =<em>伺服器名稱</em>;初始目錄 =<em>databaseName</em>;保存安全性資訊 = True;使用者識別碼 =<em>username</em>;密碼 =*密碼</strong>*

其中*serverName*、 *databaseName*、 *username*和*password*的值為資料庫伺服器名稱、資料庫名稱，以及您的 web 主機公司提供給您的使用者名稱和密碼。

## <a name="deploying-the-book-reviews-web-application"></a>部署書籍審查 Web 應用程式

先前的教學課程逐步解說如何將開發資料庫複製到生產環境，但不會探索部署資料驅動應用程式。 此時，生產環境會包含資料庫，但會使用版本的書籍審查應用程式搭配靜態評論。 我們需要將新的資料驅動應用程式部署到實際伺服器，以及更新的設定資訊。

請花點時間將開發環境中的資料驅動應用程式部署到生產環境。 此程式在先前的教學課程中有詳細的討論。 如果您需要重新整理程式，請參閱*使用 FTP 用戶端部署您的網站*或*使用 Visual Studio 教學課程來部署您的網站*。 您必須確定生產資料庫連接字串是用於生產環境中，這表示必須部署替代的 `Web.config` 檔案。 具體而言，這個修改過的 `Web.config` 檔案 s `<connectionStrings>` 元素必須包含生產資料庫連接字串，而且看起來應該如下所示：

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-cs/samples/sample2.xml)]

請注意，`<connectionStrings>` 元素中的連接字串名稱相同（`ReviewsConnectionString`），但現在包含生產資料庫連接字串，而不是開發資料庫連接字串。

除非您有更正規化的部署工作流程，否則請手動修改 `Web.config` 檔案，在部署之前先使用生產資料庫連接字串（請記得先將它還原成使用開發資料庫連接字串），或使用在部署程式中上傳至生產環境的生產環境設定資訊來維護個別的 `Web.config` 檔案。

> [!NOTE]
> 如果您不小心部署包含開發資料庫連接字串的 `Web.config` 檔案，當生產環境中的應用程式嘗試連接到資料庫時，就會發生錯誤。 此錯誤會顯示為 `SqlException`，並回報伺服器找不到或無法存取的訊息。

將網站部署到生產環境之後，請透過瀏覽器造訪生產網站。 您應該會看到並享有與在本機執行資料驅動應用程式相同的使用者體驗。 當然，當您在生產環境中流覽網站時，網站是由實際執行的資料庫伺服器所提供，而在開發環境中造訪網站會使用開發中的資料庫。 [圖 3] 顯示從生產環境中的網站，讓*您自己 ASP.NET 3.5 24 小時*審核頁面（請注意瀏覽器的網址列中的 URL）。

[![現在可以在生產環境中使用資料驅動應用程式！](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image8.jpg)](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image7.jpg) 

**圖 3**：資料驅動應用程式現在已可在生產環境中使用！ （[按一下以查看完整大小的影像](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image9.jpg)）

### <a name="storing-connection-strings-in-a-separate-configuration-file"></a>將連接字串儲存在不同的設定檔中

在開發和生產環境上維護個別設定資訊的常見技巧，是要有兩個版本的 `Web.config`：一個用於開發環境，另一個用於生產環境。 在部署階段，可以將適當的 `Web.config` 版本複製到生產環境。 在理想的情況下，此程式會自動作為部署工作流程的一部分。

您可以選擇性地提供更細微的差異，而不是維護兩個不同的 `Web.config` 檔案。 組成 `Web.config` 檔案的元素可以在外部設定檔中定義，然後在 `Web.config` 檔案中參考該檔案。 簡言之，您可以為兩個參考 databaseConnectionStrings 檔案的環境提供一個 `Web.config` 檔案，其中會包含應用程式所使用的連接字串，而且對每個環境而言都是唯一的。 我發現將不同的設定資訊分隔成不同的檔案，可以提供整齊且簡單的 `Web.config` 檔案，更清楚地列出開發與生產環境之間的設定差異。

若要使用這項技術，請先在名為 `ConfigSections`的 web 應用程式中建立新的資料夾。 接下來，將兩個檔案新增至名為 databaseConnectionStrings 的這個新資料夾和 databaseConnectionStrings。接下來，將 `<connectionStrings>` 專案從 `Web.config` 複製到 databaseConnectionStrings 和 databaseConnectionStrings 檔案中，然後修改 databaseConnectionStrings 檔案中的連接字串，讓它指定生產資料庫的連接字串。 例如，databaseConnectionStrings 應該只包含具有參考開發資料庫之連接字串的 `<connectionStrings>` 元素：

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-cs/samples/sample3.xml)]

同樣地，databaseConnectionStrings 應該只包含一個 `<connectionStrings>` 元素，但其中一個專案具有生產資料庫連接字串。

建立 databaseConnectionStrings 的複本，並將其命名為 databaseConnectionStrings。

> [!NOTE]
> 如果您想要的話，您可以將設定檔命名為 databaseConnectionStrings 以外的名稱，例如 `connectionStrings.config` 或 `dbInfo.config`。 不過，請務必以 `.config` 副檔名來命名檔案，因為 `.config` 檔案預設為，ASP.NET 引擎不會提供此檔案。 如果您將檔案命名為其他內容（例如 `connectionStrings.txt`），使用者可能會指向其瀏覽器以[www.yoursite.com/ConfigSettings/connectionStrings.txt](http://www.yoursite.com/ConfigSettings/connectionStrings.txt)並查看檔案的內容！

此時，[`ConfigSections`] 資料夾應該會包含三個檔案（請參閱 [圖 4]）。 DatabaseConnectionStrings 會分別包含適用于開發和生產環境的連接字串，以及 databaseConnectionStrings。 DatabaseConnectionStrings 會包含 web 應用程式在執行時間所使用的連接字串資訊。 因此，databaseConnectionStrings 應該與開發環境中的 databaseConnectionStrings 相同，而在實際執行時，databaseConnectionStrings 的 web.config 檔案應該與databaseConnectionStrings。

[![ConfigSections](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image11.jpg)](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image10.jpg) 

**圖 4**： ConfigSections （[按一下以觀看完整大小的影像](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image12.jpg)）

我們現在需要指示 `Web.config` 將 databaseConnectionStrings 用於其連接字串存放區。 開啟 `Web.config` 並使用下列內容取代現有的 `<connectionStrings>` 元素：

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-cs/samples/sample4.xml)]

`configSource` 屬性會指定相對於 `Web.config` 檔案的實體路徑。 如果外部 `.config` 檔案與 `Web.config` 在相同的目錄中，則請將此屬性設定為 `.config` 檔的檔案名。 如果它是在子目錄中（如同 databaseConnectionStrings），請使用反斜線來指定子資料夾來分隔資料夾和檔案名，例如 ConfigSections\databaseConnectionStrings.config。

進行這種修改後，開發和生產環境會包含相同的 `Web.config` 檔案。 現在唯一的差異在於 databaseConnectionStrings。 將 databaseConnectionStrings 複製到生產環境，並將它重新命名為 databaseConnectionStrings。在未來，如果生產資料庫連接字串有變更，您必須將其設為 databaseConnectionStrings，然後將該檔案上傳到生產環境，並將其重新命名為 databaseConnectionStrings。

> [!NOTE]
> 您可以指定個別檔案中任何 `Web.config` 元素的資訊，並使用 `configSource` 屬性，從 `Web.config`內參考該檔案。

## <a name="summary"></a>總結

資料驅動應用程式通常會在開發和生產環境中使用不同的資料庫。 因此，儲存在 web 應用程式中的資料庫連接字串在每個環境中都必須是唯一的。 在本教學課程中，我們探討了如何判斷生產資料庫連接字串，以及在兩個環境中維護唯一連接字串資訊的方式。

快樂的程式設計！

#### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [連接字串和組態檔](https://msdn.microsoft.com/library/ms254494.aspx)
- [資料庫設定字串資訊 @ ConnectionStrings.com](http://www.connectionstrings.com/)
- [將設定從 web.config 檔案移出](http://www.asp101.com/tips/index.asp?id=154)
- [&lt;connectionStrings&gt; 元素的技術檔](https://msdn.microsoft.com/library/bf7sd233.aspx)

> [!div class="step-by-step"]
> [上一頁](deploying-a-database-cs.md)
> [下一頁](configuring-a-website-that-uses-application-services-cs.md)
