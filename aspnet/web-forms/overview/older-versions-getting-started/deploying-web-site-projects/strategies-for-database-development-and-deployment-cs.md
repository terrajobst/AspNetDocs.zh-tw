---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/strategies-for-database-development-and-deployment-cs
title: 資料庫開發和部署策略（C#） |Microsoft Docs
author: rick-anderson
description: 第一次部署資料驅動應用程式時，您可以在開發環境中將資料庫複製到生產環境。 B 。
ms.author: riande
ms.date: 04/23/2009
ms.assetid: 3e8b0627-3eb7-488e-807e-067cba7cec05
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/strategies-for-database-development-and-deployment-cs
msc.type: authoredcontent
ms.openlocfilehash: 4d9dbaf41926b43af171619ee34f58da84b5dab1
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74582223"
---
# <a name="strategies-for-database-development-and-deployment-c"></a>資料庫開發及部署策略 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載 PDF](https://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial10_DBDevel_cs.pdf)

> 第一次部署資料驅動應用程式時，您可以在開發環境中將資料庫複製到生產環境。 但在後續部署中執行密件複製，將會覆寫進入生產資料庫的任何資料。 相反地，部署資料庫牽涉到在最後一次部署到實際執行資料庫之後，套用對開發資料庫所做的變更。 本教學課程會檢查這些挑戰，並提供各種策略來協助 chronicling，並套用自上次部署後對資料庫所做的變更。

## <a name="introduction"></a>簡介

如先前的教學課程所述，部署 ASP.NET 應用程式需要將相關的內容從開發環境複製到生產環境。 部署不是一次性的事件，而是在每次發行新版本的軟體時，或是在識別並解決 bug 或安全性問題時所發生的事情。 將 ASP.NET 網頁、影像、JavaScript 檔案和其他這類檔案複製到生產環境時，您不需要擔心這些檔案在上次部署後的變更方式。 您可以盲目地將檔案複製到生產環境，並覆寫現有的內容。 可惜的是，這種簡單性並不會延伸到部署資料庫。

第一次部署資料驅動應用程式時，您可以在開發環境中將資料庫複製到生產環境。 但在後續部署中執行密件複製，將會覆寫進入生產資料庫的任何資料。 相反地，部署資料庫牽涉到在最後一次部署到實際執行資料庫之後，套用對開發資料庫所做的*變更*。 本教學課程會檢查這些挑戰，並提供各種策略來協助 chronicling，並套用自上次部署後對資料庫所做的變更。

## <a name="the-challenges-of-deploying-a-database"></a>部署資料庫的挑戰

第一次部署資料驅動應用程式之前，只有一個資料庫（也就是開發環境中的資料庫），這就是為什麼第一次部署資料驅動應用程式時，您可以在生產環境的開發環境。 但是一旦部署應用程式，就會有兩個資料庫複本：一個在開發中，另一個在生產環境中。

在部署之間，開發和生產資料庫可能會不同步。雖然生產資料庫的架構維持不變，但是在新增新功能時，開發資料庫的架構可能會變更。 您可以加入或移除資料行、資料表、views 或預存程式。 可能也會有重要的資料加入至開發資料庫。 許多資料驅動型應用程式都包含以硬式編碼、應用程式特定資料（不是使用者可編輯）填入的查閱資料表。 例如，拍賣網站可能會有一個下拉式清單，其中包含描述所 auctioned 專案之條件的選項： [新增]、[良好] 和 [公平]。 您不需要直接在下拉式清單中對這些選項進行硬式編碼，而是將它們放在資料庫資料表中，通常會比較好。 如果在開發期間，將名為 [差] 的新條件加入至資料表，則在部署應用程式時，必須將此相同的記錄加入至生產資料庫中的查閱資料表。

在理想的情況下，部署資料庫會牽涉到將資料庫從開發工作複製到生產環境。 但請記住，在您部署應用程式並繼續開發之後，實際執行的資料庫將會填入真實使用者實際的資料。 因此，如果您只是在下一次部署時將資料庫從開發複製到生產環境，您會覆寫生產資料庫並遺失其現有資料。 最後的結果是，將資料庫部署到下一個部署之後，再套用對開發資料庫所做的變更。

因為部署資料庫牽涉到套用架構中的變更，而且可能是上次部署後的資料，所以必須維護變更的歷程記錄（或在部署階段判斷），以便在生產環境上套用這些變更。 有各種技術可用於管理和套用資料模型的變更。

### <a name="defining-the-baseline"></a>定義基準

若要維護對應用程式資料庫所做的變更，您需要有一些啟動狀態，也就是套用變更的基準。 在一個極端的情況下，啟動狀態可能是空的資料庫，沒有資料表、views 或預存程式。 這類基準會導致大型變更記錄檔，因為它必須包含建立所有資料庫的資料表、視圖和預存程式，以及在初始部署之後所做的任何變更。 在頻譜的另一端，您可以將基準設定為一開始部署到生產環境的資料庫版本。 此選擇會產生較小的變更記錄檔，因為它只包含在第一次部署之後對資料庫所做的變更。 這是我慣用的方法。 當然，您可以選擇更多的道路方法，將基準定義為初始建立資料庫與第一次部署資料庫的時間點。

一旦您選擇基準，請考慮產生可執行檔 SQL 腳本，以重新建立基準版本。 這類腳本可以快速地重新建立資料庫的基準版本。 這項功能在大型專案中特別有用，其中可能有多個開發人員處理專案或其他環境（例如測試或預備），而每個都需要自己的資料庫複本。

有各種工具可供您使用，以產生基準版本的 SQL 腳本。 在 SQL Server Management Studio （SSMS）中，您可以在資料庫上按一下滑鼠右鍵，移至 [工作] 子功能表，然後選擇 [產生腳本] 選項。 這會啟動腳本嚮導，您可以指示產生一個檔案，其中包含用來建立資料庫物件的 SQL 命令。 另一個選項是 [資料庫發佈嚮導]，它可以產生 SQL 命令，而不只是建立資料庫架構，也會產生資料庫資料表中的資料。 資料庫發佈嚮導已在*部署資料庫*教學課程中詳細地回顧。 無論您使用哪一種工具，在最後，您應該會有一個腳本檔案，您可以用它來重新建立資料庫的基準版本（如果有需要的話）。

## <a name="documenting-the-database-changes-in-prose"></a>記錄 Prose 中的資料庫變更

在開發階段維護資料模型變更記錄的最簡單方式，就是在 prose 中記錄變更。 例如，如果在開發已部署的應用程式期間，將新的資料行加入至 `Employees` 資料表、從 `Orders` 資料表中移除資料行，然後加入新的資料表（`ProductCategories`），您將會保留包含下列歷程記錄的文字檔或 Microsoft Word 檔：

<a id="0.4_table01"></a>

| **變更日期** | **變更詳細資料** |
| --- | --- |
| 2009-02-03： | 已將資料行 `DepartmentID` （`int`，非 Null）新增至 `Employees` 資料表。 已將外鍵條件約束從 `Departments.DepartmentID` 新增至 `Employees.DepartmentID`。 |
| 2009-02-05： | 已從 `Orders` 資料表中移除資料行 `TotalWeight`。 已在相關聯的 `OrderDetails` 記錄中捕捉到的資料。 |
| 2009-02-12： | 建立 `ProductCategories` 資料表。 有三個數據行： `ProductCategoryID` （`int`、`IDENTITY`、`NOT NULL`）、`CategoryName` （`nvarchar(50)`、`NOT NULL`）和 `Active` （`bit`，`NOT NULL`）。 將 primary key 條件約束新增至 `ProductCategoryID`，並將預設值1加入 `Active`。 |

這種方法有一些缺點。 對於初學者來說，不希望自動化。 每當需要將這些變更套用至資料庫時（例如部署應用程式時），開發人員都必須手動執行每一項變更，一次一個。 此外，如果您需要使用變更記錄檔，從基準重新建立特定版本的資料庫，則在記錄檔大小增加時，這麼做會花費更多時間。 此方法的另一個缺點是，每個變更記錄專案的清楚程度和細節層級會留給記錄變更的人員。 在具有多個開發人員的小組中，有些人可能會產生比其他專案更詳細、更容易閱讀或更精確的專案。 此外，錯誤和其他人為相關的資料輸入錯誤也是可行的。

在 prose 中記錄資料庫變更的主要優點是簡單明瞭。 您不需要熟悉用來建立和改變資料庫物件的 SQL 語法。 相反地，您可以在 prose 中記錄變更，並透過 SQL Server Management Studio 的圖形化使用者介面加以執行。

在 prose 中維護您的變更記錄是不可否認的，而且不是非常複雜，也不適用於某些專案，例如範圍很大、經常變更資料模型，或牽涉到多個開發人員的工作。 但是我已經看過，這種方法非常適用于只有資料模型偶爾變更的小型、一項專案，而在此情況下，在建立和改變資料庫物件的 SQL 語法中，其中的重要開發人員並沒有強大的背景。

> [!NOTE]
> 雖然變更記錄檔中的資訊在技術上只需要到部署時間，但建議您保留變更的歷程記錄。 但是，您應該考慮為每個資料庫版本提供不同的變更記錄檔，而不是維護單一、不斷成長的變更記錄檔。 一般來說，您會想要在每次部署資料庫時進行版本。 藉由維護變更記錄的記錄，您可以從基準開始，藉由執行從第1版開始的變更記錄腳本來重新建立任何資料庫版本，並繼續進行，直到您到達需要重新建立的版本為止。

## <a name="recording-the-sql-change-statements"></a>記錄 SQL 變更語句

在 prose 中維護變更記錄的主要缺點是缺乏自動化。 理想的情況是，在部署階段對生產資料庫執行資料庫變更，就像按一下按鈕來執行腳本一樣簡單，而不需要手動執行資訊清單。 藉由維護變更記錄檔，其中包含用來改變資料模型的 SQL 命令，就可以進行這類自動化。

SQL 語法包含許多用來建立和修改各種資料庫物件的語句。 例如，當[*CREATE TABLE 語句*](https://msdn.microsoft.com/library/ms174979.aspx)執行時，會使用指定的資料行和條件約束來建立新的資料表。 [*ALTER table 語句*](https://msdn.microsoft.com/library/ms190273.aspx)會修改現有的資料表、加入、移除或修改其資料行或條件約束。 另外還有一些語句可建立、修改和卸載索引、視圖、使用者定義函數、預存程式、觸發程式和其他資料庫物件。

回到先前的範例，在開發已部署的應用程式期間，您會將新的資料行加入 `Employees` 資料表、從 `Orders` 資料表中移除資料行，然後加入新的資料表（`ProductCategories`）。 這類動作會產生含有下列 SQL 命令的變更記錄檔：

[!code-sql[Main](strategies-for-database-development-and-deployment-cs/samples/sample1.sql)]

在部署階段將這些變更推送至生產資料庫是單鍵作業：開啟 SQL Server Management Studio、連接到您的實際執行資料庫、開啟新的查詢視窗、貼上變更記錄檔的內容，然後按一下 [執行] 來執行腳本。

## <a name="using-a-comparison-tool-to-synchronize-the-data-models"></a>使用比較工具來同步處理資料模型

記錄 prose 中的資料庫變更很簡單，但執行變更時，開發人員必須一次對生產資料庫進行一項變更;記錄變更 SQL 命令，可讓您在生產資料庫上執行這些變更，就像按一下按鈕一樣簡單又快速，但需要學習並掌握 SQL 語句和語法來建立和改變資料庫物件。 資料庫比較工具充分發揮這兩種方法，並捨棄最差。

資料庫比較工具會比較兩個資料庫的架構或資料，並顯示摘要報告，顯示資料庫有何差異。 然後，只要按一下按鈕，您就可以產生 SQL 命令來同步處理一個或多個資料庫物件。 簡言之，您可以在部署時使用資料庫比較工具來比較開發和生產資料庫，產生一個包含 SQL 命令的檔案，當執行時，它會將變更套用至生產資料庫的架構，讓它能夠鏡像開發資料庫的架構。

許多不同的廠商都提供各種協力廠商資料庫比較工具。 其中一個範例是[*SQL 比較*](http://www.red-gate.com/products/SQL_Compare/)，[*紅色閘道軟體*](http://www.red-gate.com/)。 讓我們逐步解說使用 SQL 比較來比較和同步處理開發和生產資料庫架構的程式。

> [!NOTE]
> 在撰寫本文時，SQL 比較的目前版本是7.1 版，標準版的成本為 $395。 您可以透過下載免費的14天試用版來追蹤。

當 SQL 比較開始時，會開啟 [比較專案] 對話方塊，顯示已儲存的 SQL 比較專案。 建立新的專案。 這會啟動 [專案設定] wizard，提示您提供要比較之資料庫的相關資訊（請參閱 [圖 1]）。 輸入開發和生產環境資料庫的資訊。

[![比較開發與生產資料庫](strategies-for-database-development-and-deployment-cs/_static/image2.jpg)](strategies-for-database-development-and-deployment-cs/_static/image1.jpg)

**圖 1**：比較開發和生產資料庫（[按一下以觀看完整大小的影像](strategies-for-database-development-and-deployment-cs/_static/image3.jpg)）

> [!NOTE]
> 如果您的開發環境資料庫是網站 [`App_Data`] 資料夾中的 SQL Express Edition 資料庫檔案，您將需要在 SQL Server Express 資料庫伺服器中註冊資料庫，才能從 [圖 1] 所示的對話方塊中選取它。 完成此動作的最簡單方式是開啟 SQL Server Management Studio （SSMS）、連接到 SQL Server Express 資料庫伺服器，然後附加資料庫。 如果您的電腦上未安裝 SSMS，您可以下載並安裝免費的[*SQL Server 2008 Management Studio Basic 版本*](https://www.microsoft.com/downloads/details.aspx?FamilyId=7522A683-4CB2-454E-B908-E805E9BD4E28&amp;displaylang=en)。

除了選取要比較的資料庫之外，您也可以從 [選項] 索引標籤指定各種比較設定。您可能要開啟的一個選項是「忽略條件約束和索引名稱」。 回想一下，在上一個教學課程中，我們將應用程式服務資料庫物件新增到開發和生產資料庫中。 如果您使用 `aspnet_regsql.exe` 工具在生產資料庫上建立這些物件，則您會發現主要索引鍵和唯一條件約束名稱在開發與生產資料庫之間有所不同。 因此，SQL 比較會將所有應用程式服務資料表標示為不同。 您可以取消核取 [忽略條件約束和索引名稱] 並同步處理條件約束名稱，或指示 SQL 比較來忽略這些差異。

選取要比較的資料庫（並查看比較選項）之後，請按一下 [立即比較] 按鈕，開始進行比較。 在接下來的幾秒內，SQL 比較會檢查這兩個資料庫的架構，並產生其差異的報告。 我特意對開發資料庫做了一些修改，以顯示 SQL 比較介面中記錄這類差異的方式。 如 [圖 2] 所示，我在 `Authors` 資料表中加入了 `BirthDate` 資料行，從 `Books` 資料表中移除 `ISBN` 的資料行，並加入了新的資料表 `Ratings`，這是為了讓使用者造訪網站速率審查的書籍。

> [!NOTE]
> 本教學課程中所做的資料模型變更已完成，以說明如何使用資料庫比較工具。 在未來的教學課程中，您將不會在資料庫中找到這些變更。

[![SQL 比較列出開發與生產資料庫之間的差異](strategies-for-database-development-and-deployment-cs/_static/image5.jpg)](strategies-for-database-development-and-deployment-cs/_static/image4.jpg)

**圖 2**： SQL 比較列出開發與生產資料庫之間的差異（[按一下以觀看完整大小的影像](strategies-for-database-development-and-deployment-cs/_static/image6.jpg)）

SQL 比較會將資料庫物件分解成群組，快速顯示兩個資料庫中有哪些物件存在但不同，哪些物件存在於一個資料庫中，而另一個則是相同的物件。 如您所見，這兩個資料庫中有兩個物件存在，但不同： `Authors` 資料表（已加入資料行），以及 `Books` 資料表（已移除一個）。 有一個物件只存在於開發資料庫中，也就是新建立的 `Ratings` 資料表。 而且兩個資料庫中都有117個相同的物件。

選取資料庫物件會顯示 [SQL 差異] 視窗，其中會顯示這些物件的差異。 [圖 2] 底部顯示的 [SQL 差異] 視窗，強調了開發資料庫中的 `Authors` 資料表具有 [`BirthDate`] 資料行，但在生產資料庫的 [`Authors`] 資料表中找不到。

在檢查差異並選取您想要同步處理的物件之後，下一步就是產生更新生產資料庫的架構所需的 SQL 命令，使其符合開發資料庫。 這是透過 [同步處理嚮導] 來完成。 同步處理嚮導會確認要同步處理哪些物件，並摘要說明動作計畫（請參閱 [圖 3]）。 您可以立即同步處理資料庫，或使用可在您休閒中執行的 SQL 命令來產生腳本。

[![使用同步處理嚮導來同步處理您的資料庫架構](strategies-for-database-development-and-deployment-cs/_static/image8.jpg)](strategies-for-database-development-and-deployment-cs/_static/image7.jpg)

**圖 3**：使用 [同步處理嚮導] 同步處理您的資料庫架構（[按一下以查看完整大小的影像](strategies-for-database-development-and-deployment-cs/_static/image9.jpg)）

像是 Red 閘道軟體的資料庫比較工具 SQL 比較，會將對開發資料庫架構的變更套用至實際執行資料庫，如同 point，然後按一下。

> [!NOTE]
> SQL 比較會比較和同步處理兩個資料庫*架構*。 可惜的是，它不會比較和同步處理兩個資料庫資料表中的資料。 Red 閘道軟體提供名為[*SQL Data Compare*](http://www.red-gate.com/products/SQL_Data_Compare/)的產品，它會比較和同步處理兩個資料庫之間的資料，但它是 sql 比較的個別產品，而成本另一個 $395。

## <a name="taking-the-application-offline-during-deployment"></a>在部署期間讓應用程式離線

如我們在這些教學課程中所見，部署是包含多個步驟的程式：將 ASP.NET 網頁、主版頁面、CSS 檔案、JavaScript 檔案、影像和其他必要內容從開發環境複製到生產環境環境視需要複製生產環境特定的設定資訊;並在上次部署後將變更套用至資料模型。 視檔案數目和資料庫的複雜度而定，這些步驟可能需要數秒到數分鐘的時間才能完成。 在此期間，web 應用程式會在 flux 中，而造訪網站的使用者可能會遇到錯誤或非預期的行為。

部署網站時，最好讓 web 應用程式「離線」，直到部署完成為止。 讓應用程式離線（並在部署程式完成後使其恢復運作）就像上傳檔案，然後刪除它一樣簡單。 從 ASP.NET 2.0 開始，在應用程式的根目錄中，只有名為 `app_offline.htm` 的檔案才會讓整個網站「離線」。 該網站上 ASP.NET 網頁的任何要求都會自動回應 `app_offline.htm` 檔案的內容。 一旦移除該檔案之後，應用程式就會重新上線。

在部署期間讓應用程式離線，就像在開始部署程式之前，將 `app_offline.htm` 檔案上傳到生產環境的根目錄一樣簡單，然後在部署完成後將它刪除（或重新命名為其他專案）。 如需這項技術的詳細資訊，請參閱 John Peterson 文章，讓[*ASP.NET 應用程式離線*](http://www.15seconds.com/issue/061207.htm)。

## <a name="summary"></a>總結

部署以資料為導向的應用程式中心時，主要的挑戰在於部署資料庫。 由於資料庫有兩個版本：一個在開發環境中，另一個在生產環境中，這兩個資料庫架構可能會因為開發中新增的新功能而無法同步。 更多的是，因為生產資料庫是以實際使用者的實際資料填入，所以您無法以修改過的開發資料庫來覆寫生產資料庫，如同部署組成應用程式的檔案（ASP.NET 網頁，影像檔等）。 相反地，部署資料庫需要在上一次部署之後，針對生產資料庫上的開發資料庫執行一組精確的變更。

本教學課程探討了用來維護和套用資料庫變更記錄檔的三種技術。 最簡單的方法是在 prose 中記錄變更。 雖然這個策略會在生產資料庫上進行這些變更，以進行手動程式，但它不需要知道用來建立和改變資料庫物件的 SQL 命令。 更複雜的方法，以及在具有多位開發人員的大型專案或專案中更可行的方式，是將變更記錄為一系列的 SQL 命令。 這會大幅 hastens 將這些變更推出至目標資料庫。 這兩種方法的最佳作法，都可以使用資料庫比較工具來達成，例如 Red 閘道 Software s SQL 比較。

本教學課程的重點在於如何部署資料驅動應用程式。 下一組教學課程會探討如何回應生產環境中的錯誤。 我們將探討如何顯示易記的錯誤頁面，而不是螢幕上的黃色畫面。 我們會瞭解如何記錄錯誤的詳細資料，以及如何在這類錯誤發生時發出警示。

快樂的程式設計！

> [!div class="step-by-step"]
> [上一頁](configuring-a-website-that-uses-application-services-cs.md)
> [下一頁](displaying-a-custom-error-page-cs.md)
