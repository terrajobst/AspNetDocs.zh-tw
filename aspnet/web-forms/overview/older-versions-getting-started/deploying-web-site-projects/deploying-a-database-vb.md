---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-a-database-vb
title: 部署資料庫（VB） |Microsoft Docs
author: rick-anderson
description: 部署 ASP.NET web 應用程式需要從開發環境取得必要的檔案和資源到生產環境。 針對 da 。
ms.author: riande
ms.date: 04/23/2009
ms.assetid: 96ac3e69-04c7-4917-ad06-5f8968c3fbf1
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-a-database-vb
msc.type: authoredcontent
ms.openlocfilehash: 8221025bec06e052016070f74deabb3e6d936045
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74643746"
---
# <a name="deploying-a-database-vb"></a>部署資料庫 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_07_VB.zip)或[下載 PDF](https://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial07_DeployDB_vb.pdf)

> 部署 ASP.NET web 應用程式需要從開發環境取得必要的檔案和資源到生產環境。 對於資料驅動的 web 應用程式，這包括資料庫架構和資料。 本教學課程是一系列文章中的第一個，它會探索將資料庫從開發環境成功部署到生產所需的步驟。

### <a name="introduction"></a>簡介

部署 ASP.NET web 應用程式需要從開發環境取得必要的檔案和資源到生產環境。 在過去六個教學課程中，我們探討了如何部署簡單的書籍評論 web 應用程式。 這個示範網站是由數個伺服器端資源（ASP.NET 網頁、設定檔、`Web.sitemap` 檔案等）以及用戶端資源（例如影像和 CSS 檔案）所組成。 但是資料驅動的 web 應用程式呢？ 部署使用資料庫的 web 應用程式時，必須採取哪些額外的步驟？

在接下來的幾個教學課程中，我們將討論部署資料驅動 web 應用程式所需的步驟。 本教學課程一開始會先檢查如何從開發環境取得資料庫的架構和內容到生產環境，而後續的教學課程會探討所需的設定變更。 之後，我們將探索部署使用應用程式服務（成員資格、角色、設定檔等）之資料庫的挑戰。

## <a name="examining-the-updated-book-reviews-web-application"></a>檢查更新的書籍評論 Web 應用程式

為了示範如何部署資料驅動的 web 應用程式，我已將書籍審查 web 應用程式從簡單的靜態網站更新為數據驅動型網站。 如先前所述，本教學課程中有兩個版本的應用程式下載：一個使用 Web 應用程式專案模型，另一個則使用網站專案模型。

更新的書籍評論 web 應用程式會使用[SQL Server 2008 Express Edition](https://www.microsoft.com/express/sql/default.aspx)資料庫，其儲存在網站 s `App_Data` 資料夾（`~/App_Data/Reviews.mdf`）中。 如果您的電腦上已安裝 SQL Server 2008，則示範應該會執行，而不會發生錯誤。 如果您有舊版的 SQL Server 您可以安裝免費的 SQL Server 2008 Express Edition，也可以使用本教學課程下載中提供的資料庫腳本，自行建立資料庫。

`Reviews.mdf` 資料庫包含四個數據表：

- `Genres`-包含每個內容類型的記錄，例如技術、小說和商務。
- `Books`-包含每項審查的記錄，其中包含 `Title`、`GenreId`、`ReviewDate`和 `Review`等資料行，還有其他欄位。
- `Authors`-包含每位作者參與已審查書籍的相關資訊。
- `BooksAuthors`-多對多聯結資料表，指定作者撰寫了哪些書籍。

[圖 1] 顯示這四個數據表的 ER 圖表。

[![書審查 Web 應用程式的資料庫由四個數據表組成](deploying-a-database-vb/_static/image2.jpg)](deploying-a-database-vb/_static/image1.jpg) 

**圖 1**：本書審查 Web 應用程式的資料庫是由四個數據表組成（[按一下以觀看完整大小的影像](deploying-a-database-vb/_static/image3.jpg)）

前一版的書籍評論網站針對每本書各有不同的 ASP.NET 網頁。 例如，有一個名為 `~/Tech/TYASP35.aspx` 的頁面，其中包含了*在24小時內 ASP.NET 3.5*的審查。 這個新的資料驅動版本網站有儲存在資料庫中的評論，還有一個 ASP.NET 網頁 [複習 .aspx？ ID =*d*]，它會顯示指定之書籍的審查。 同樣地，還有一個 [.aspx？ ID =*genreId* ] 頁面，其中列出指定之內容類型中已審核的書籍。

[圖 2] 和 [圖 3] 顯示作用中的 `Genre.aspx` 和 `Review.aspx` 頁面。 請注意每個頁面的網址列中的 URL。 在 [圖 2] 中，it 的內容類型 .aspx？ ID = 85d164ba-1123-4c47-82a0-c8ec75de7e0e。 由於85d164ba-1123-4c47-82a0-c8ec75de7e0e 是技術類型的 `GenreId` 值，因此頁面的標題會顯示「技術評論」，而項目符號清單會列舉網站上屬於此類型的評論。

[![技術內容類型頁面](deploying-a-database-vb/_static/image5.jpg)](deploying-a-database-vb/_static/image4.jpg) 

**圖 2**：技術內容類型頁面（[按一下以觀看完整大小的影像](deploying-a-database-vb/_static/image6.jpg)）

[![在24小時內讓自己 ASP.NET 3.5 的審查](deploying-a-database-vb/_static/image8.jpg)](deploying-a-database-vb/_static/image7.jpg) 

**圖 3**：讓*自己在24小時內 ASP.NET 3.5*的審查（[按一下以觀看完整大小的影像](deploying-a-database-vb/_static/image9.jpg)）

本書審查 web 應用程式也包含管理區段，讓系統管理員可以在其中新增、編輯和刪除內容、評論和撰寫資訊。 目前，任何訪客都可以存取 [管理] 區段。 在未來的教學課程中，我們將新增對使用者帳戶的支援，並僅允許授權的使用者進入系統管理頁面。

如果您下載書籍審查應用程式，請記住，其目的是要示範如何部署資料驅動應用程式。 它不會展現應用程式設計的最佳作法。 例如，沒有個別的資料存取層（DAL）;ASP.NET 網頁會透過其程式碼後置類別中的 SqlDataSource 控制項或 ADO.NET 程式碼，直接與資料庫通訊。 若要深入瞭解如何使用階層式架構來建立資料驅動應用程式，請參閱我的使用[*資料*教學](../../data-access/index.md)課程。

## <a name="databases-on-development-versus-production"></a>開發上的資料庫與生產環境

當您在資料驅動的 web 應用程式上開始開發時，您必須指定資料庫連接字串，其中提供如何連接到資料庫的應用程式詳細資料。 此連接字串會指定資料庫伺服器、資料庫名稱和安全性資訊等其他專案。 最常見的情況是，應用程式在開發期間所使用的資料庫，與生產環境中所使用的資料庫不同。 在開發與生產環境中使用不同的資料庫有許多好處。 在開發中使用不同的資料庫，表示您不必擔心不小心修改或刪除即時資料。 它也可讓您放入虛擬的測試資料，或對資料模型進行重大變更，而不需要擔心對生產環境中的應用程式所造成的影響。 在開發和生產環境中擁有不同資料庫的缺點是，當應用程式部署資料庫時，也必須部署資料庫架構或資料的任何相關變更。

在第一次部署之前，資料庫只有一個實例，而該實例位於開發環境中。 當第一次將應用程式部署至生產環境時，我們不能只複製必要的伺服器端和用戶端檔案，也不能將資料庫從開發環境複製到實際執行環境。 這就是我們現在在書籍審查 web 應用程式中的位置：資料庫位於開發環境中的 `App_Data` 資料夾，但尚未推送到生產環境。

一旦部署應用程式，就會有兩個資料庫複本。 隨著應用程式成熟，可能會加入新功能、強制資料模型的變更（例如將新的資料行加入至現有的資料表、變更現有資料行、加入新的資料表等等）。 下次部署 web 應用程式時，在上一次部署之後，套用至開發環境中資料庫的變更，必須套用至生產資料庫。 在後續的教學課程中，會討論管理此程式的一些策略。 本教學課程著重于將整個資料庫從開發環境部署到生產環境。

## <a name="deploying-the-database-to-the-production-environment"></a>將資料庫部署到生產環境

本教學課程的其餘部分將探討如何將資料庫從開發環境部署到生產環境。 如果您遵循此動作，則必須確定您的 web 主機提供者帳戶包含 Microsoft SQL Server 資料庫支援。 您也需要有一些資訊，也就是資料庫伺服器名稱、資料庫名稱，以及用來連接資料庫的使用者名稱和密碼。

如本教學課程稍早所述，本書會回顧網站資料庫是儲存在 `App_Data` 資料夾中的 SQL Server 2008 Express Edition 資料庫。 這種情況的原因是，部署這類資料庫就像是將 `App_Data` 資料夾從開發環境複製到生產環境一樣簡單。 不過，大部分的 web 主機提供者都不支援在 `App_Data` 資料夾中裝載資料庫，因為安全性的緣故。 Web 主機會改在其環境中的 SQL Server 資料庫伺服器上提供帳戶。 將資料庫從您的開發環境部署到生產環境，需要在您的 web 主機 s 資料庫伺服器上註冊資料庫。

那麼，您要如何將資料庫從開發環境移至生產環境？ 有幾種方式可以完成這項工作，視您的 web 主機所提供的服務而定。 在某些主機（例如 DiscountASP.NET）中，您可以將資料庫的備份或實際的 `.mdf` 檔案 FTP 至您的網站，然後從 [控制台]，將備份檔案還原，或將 `.mdf` 檔案附加至 SQL Server 資料庫伺服器。 使用這類工具來部署資料庫，就像將 `App_Data` 資料夾複製到生產環境，然後透過 [控制台] 進行附加一樣簡單。 這可能是第一次發行資料庫最簡單快速的方式。

另一種方法是使用「資料庫發佈嚮導」。 [資料庫發佈嚮導] 是 Windows 桌面應用程式，會產生 SQL 命令來建立您的資料庫架構，也就是資料表、預存程式、視圖、使用者定義函數等等，並選擇性地將資料放在資料表中。 接著，您可以透過 SQL Server Management Studio 連接到 web 主機提供者的資料庫伺服器，然後執行此腳本，在生產環境上複製資料庫。 更棒的是，如果您的 web 主機提供者支援 Microsoft 的[資料庫發行服務](http://www.codeplex.com/sqlhost/Wiki/View.aspx?title=Database%20Publishing%20Services&amp;referringTitle=Home)，您可以讓資料庫發佈嚮導所產生的腳本代表您自動在資料庫伺服器上執行。 由於「資料庫發佈嚮導」產生的腳本會建立資料庫的架構和資料，因此不論您的 web 主機提供者是否提供附加已上傳 `.mdf` 檔案等功能，都能正常執行。

### <a name="generating-the-sql-commands-to-create-the-database-schema-and-data-using-the-database-publishing-wizard"></a>使用資料庫發行嚮導產生 SQL 命令以建立資料庫架構和資料

讓我們逐步解說如何使用 [資料庫發佈嚮導]，將書籍審核資料庫部署到生產環境。 如果您使用 Visual Studio 2008 或更高版本，則已安裝資料庫發行嚮導。 如果您使用 Visual Studio 2005，就必須先[下載並安裝](https://www.microsoft.com/downloads/details.aspx?familyid=56E5B1C5-BF17-42E0-A410-371A838E570A&amp;displaylang=en)嚮導。

開啟 Visual Studio，然後流覽至 `Reviews.mdf` 資料庫。 如果您使用的是 Visual Web Developer，請移至資料庫總管;如果您使用 Visual Studio，請使用伺服器總管。 [圖 4] 顯示 Visual Web Developer 資料庫總管中的 `Reviews.mdf` 資料庫。 如 [圖 4] 所示，`Reviews.mdf` 資料庫是由四個數據表、三個預存程式和一個使用者定義函數所組成。

[![在資料庫總管或伺服器總管中尋找資料庫](deploying-a-database-vb/_static/image11.jpg)](deploying-a-database-vb/_static/image10.jpg) 

**圖 4**：在資料庫總管或伺服器總管中尋找資料庫（[按一下以查看完整大小的影像](deploying-a-database-vb/_static/image12.jpg)）

以滑鼠右鍵按一下資料庫名稱，然後從內容功能表選擇 [發行至提供者] 選項。 這會啟動 [資料庫發佈嚮導] （請參閱 [圖 5]）。 按 [下一步]，前進到啟動顯示畫面。

[![資料庫發佈嚮導啟動顯示畫面](deploying-a-database-vb/_static/image14.jpg)](deploying-a-database-vb/_static/image13.jpg) 

**圖 5**：資料庫發佈嚮導啟動顯示畫面（[按一下以觀看完整大小的影像](deploying-a-database-vb/_static/image15.jpg)）

Wizard 中的第二個畫面會列出資料庫發行嚮導可存取的資料庫，並讓您選擇是否要編寫所選資料庫中所有物件的腳本，或挑選要編寫腳本的物件。 選取適當的資料庫，並核取 [為選取的資料庫中的所有物件編寫腳本] 選項。

> [!NOTE]
> 當您在 [圖 6] 所示的畫面中按一下 [下一步] 時，如果您看到錯誤：「此嚮導的資料庫*databaseName*中沒有任何物件」，請確定您資料庫檔案的路徑不太長。 如[此討論專案](http://www.codeplex.com/sqlhost/Thread/View.aspx?ThreadId=11014)的 [資料庫發佈嚮導] 專案頁面所述，如果資料庫檔案的路徑太長，可能會發生此錯誤。

[![資料庫發佈嚮導啟動顯示畫面](deploying-a-database-vb/_static/image17.jpg)](deploying-a-database-vb/_static/image16.jpg) 

**圖 6**：資料庫發佈嚮導啟動顯示畫面（[按一下以觀看完整大小的影像](deploying-a-database-vb/_static/image18.jpg)）

在下一個畫面中，您可以產生腳本檔案，或者，如果您的 web 主機支援它，請將資料庫直接發行到 web 主機提供者的資料庫伺服器。 如 [圖 7] 所示，我將腳本寫入檔案 `C:\REVIEWS.MDF.sql`。

[![將資料庫編寫成檔案，或將它直接發行到 Web 主機提供者](deploying-a-database-vb/_static/image20.jpg)](deploying-a-database-vb/_static/image19.jpg) 

**圖 7**：將資料庫編寫成檔案，或將它直接發行至您的 Web 主機提供者（[按一下以觀看完整大小的影像](deploying-a-database-vb/_static/image21.jpg)）

後續畫面會提示您提供各種腳本選項。 您可以指定腳本是否應包含 drop 語句來移除這些現有的物件。 這會預設為 True，這在第一次部署資料庫時是正常的。 您也可以指定目標資料庫是 SQL Server 2000、SQL Server 2005 或 SQL Server 2008。 最後，您可以指出是否要撰寫架構和資料的腳本、只編寫資料，或只撰寫架構。 架構是資料庫物件、資料表、預存程式、視圖等的集合。 資料是位於資料表中的資訊。

如 [圖 8] 所示，我已設定 wizard 來卸載現有的資料庫物件、產生 SQL Server 2008 資料庫的腳本，以及發行架構和資料。

[![指定發行選項](deploying-a-database-vb/_static/image23.jpg)](deploying-a-database-vb/_static/image22.jpg) 

**圖 8**：指定發行選項（[按一下以查看完整大小的影像](deploying-a-database-vb/_static/image24.jpg)）

最後兩個畫面會匯總即將採取的動作，然後顯示腳本的狀態。 執行 wizard 的最後結果是，我們有一個腳本檔案，其中包含在生產環境中建立資料庫，並使用與開發時相同的資料來填入所需的 SQL 命令。

### <a name="executing-the-sql-commands-on-the-production-environment-database"></a>在生產環境資料庫上執行 SQL 命令

既然我們已經有包含 SQL 命令的腳本來建立資料庫及其資料，剩下的就是在生產資料庫上執行腳本。 有些 web 主機提供者會在其 [控制台] 中提供一個文字方塊，您可以在其中輸入要在資料庫上執行的 SQL 命令。 如果您有非常大的腳本檔案，這個選項可能無法使用（例如，`REVIEWS.MDF.sql` 腳本檔案大小超過 425 KB）。

較好的方法是使用 SQL Server Management Studio （SSMS）直接連接到生產資料庫伺服器。 如果您的電腦上已安裝非 Express 版本的 SQL Server，則您可能已經安裝 SSMS。 否則，您可以[下載並安裝](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)免費的 SQL Server Management Studio Express Edition 複本。

啟動 SSMS，並使用 web 主機提供者所提供的資訊連接到您的 web 主機資料庫伺服器。

[![連接到您的 Web 主機提供者資料庫伺服器](deploying-a-database-vb/_static/image26.jpg)](deploying-a-database-vb/_static/image25.jpg) 

**圖 9**：連接到您的 Web 主機服務提供者的資料庫伺服器（[按一下以查看完整大小的影像](deploying-a-database-vb/_static/image27.jpg)）

展開 [資料庫] 索引標籤，然後找出您的資料庫。 按一下工具列左上角的 [新增查詢] 按鈕，並貼上資料庫發行嚮導所建立之腳本檔案中的 SQL 命令，然後按一下 [執行] 按鈕，在生產環境資料庫伺服器上執行這些命令。 如果您的腳本檔案特別大，可能需要幾分鐘的時間來執行命令。

[![連接到您的 Web 主機提供者資料庫伺服器](deploying-a-database-vb/_static/image29.jpg)](deploying-a-database-vb/_static/image28.jpg) 

**圖 10**：連接到您的 Web 主機服務提供者的資料庫伺服器（[按一下以查看完整大小的影像](deploying-a-database-vb/_static/image30.jpg)）

這樣就大功告成了！ 此時，開發資料庫已複製到生產環境。 如果您在 SSMS 中重新整理資料庫，您應該會看到新的資料庫物件。 [圖 11] 顯示生產資料庫的資料表、預存程式和使用者定義函數，這些函式會在開發資料庫上進行鏡像。 而且因為我們指示資料庫發佈嚮導發行資料，所以生產資料庫的資料表與執行 Wizard 時的開發資料庫資料表具有相同的資料。 [圖 12] 顯示生產資料庫上 `Books` 資料表中的資料。

[![資料庫物件在生產資料庫上已重複](deploying-a-database-vb/_static/image32.jpg)](deploying-a-database-vb/_static/image31.jpg) 

**圖 11**：資料庫物件在生產資料庫上已重複（[按一下以查看完整大小的影像](deploying-a-database-vb/_static/image33.jpg)）

[![生產資料庫包含與開發資料庫相同的資料](deploying-a-database-vb/_static/image35.jpg)](deploying-a-database-vb/_static/image34.jpg) 

**圖 12**：生產資料庫包含與開發資料庫相同的資料（[按一下以查看完整大小的影像](deploying-a-database-vb/_static/image36.jpg)）

此時，我們只會將開發資料庫部署到生產環境。 我們尚未探討如何部署 web 應用程式本身，或檢查應用程式在生產環境中使用生產資料庫所需的設定變更。 我們會在下一個教學課程中討論這些問題！

## <a name="summary"></a>總結

部署資料驅動 web 應用程式時，需要將在開發期間使用的資料庫複製到生產環境。 許多 web 主機提供者都提供工具，以簡化部署資料庫的程式。 例如，您可以使用 DiscountASP.NET，將資料庫 FTP `.mdf` 檔案（或備份），然後從 [控制台] 將資料庫附加到資料庫伺服器。 無論您的 web 主機提供者所提供的功能為何，另一個可行的選項是 Microsoft 的資料庫發佈嚮導工具，它會產生 SQL 命令的腳本來建立開發資料庫的架構和資料。 產生此腳本之後，您就可以在生產資料庫上執行它。

既然本書回顧了 web 應用程式的資料庫，就可以部署應用程式了。 不過，web 應用程式的設定資訊會指定資料庫的連接字串，而該連接字串會參考開發資料庫。 將網站部署到生產環境時，我們需要更新此連接字串資訊。 下一個教學課程會探討這些設定差異，並逐步解說將資料驅動的書籍評論網站發佈到生產環境所需的步驟。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [下載 Microsoft SQL Server 資料庫發佈嚮導1。1](https://www.microsoft.com/downloads/details.aspx?familyid=56E5B1C5-BF17-42E0-A410-371A838E570A&amp;displaylang=en)
- [下載 Microsoft SQL Server Management Studio Express Edition](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)

> [!div class="step-by-step"]
> [上一頁](core-differences-between-iis-and-the-asp-net-development-server-vb.md)
> [下一頁](configuring-the-production-web-application-to-use-the-production-database-vb.md)
