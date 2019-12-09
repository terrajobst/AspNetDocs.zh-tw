---
uid: web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs
title: 在 SQL Server 中建立成員資格架構C#（） |Microsoft Docs
author: rick-anderson
description: 本教學課程一開始會先檢查將必要的架構加入至資料庫以使用 SqlMembershipProvider 的技巧。 之後，我們會將我們的 。
ms.author: riande
ms.date: 01/18/2008
ms.assetid: b4ac129d-1b8e-41ca-a38f-9b19d7c7bb0e
msc.legacyurl: /web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs
msc.type: authoredcontent
ms.openlocfilehash: 97623e7c13ab7799b9dadbb8e52be8e0cd99e252
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595206"
---
# <a name="creating-the-membership-schema-in-sql-server-c"></a>在 SQL Server 中建立成員資格結構描述 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_04_CS.zip)或[下載 PDF](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial04_MembershipSetup_cs.pdf)

> 本教學課程一開始會先檢查將必要的架構加入至資料庫以使用 SqlMembershipProvider 的技巧。 接下來，我們將檢查架構中的重要資料表，並討論其用途和重要性。 本教學課程最後會介紹如何告訴 ASP.NET 應用程式，成員資格架構應該使用哪個提供者。

## <a name="introduction"></a>簡介

先前的兩個教學課程是使用表單驗證來檢查，以識別網站訪客。 表單驗證架構可讓開發人員輕鬆地將使用者登入網站，並透過使用驗證票證的方式在頁面造訪時記住。 `FormsAuthentication` 類別包含產生票證的方法，並將它新增至訪客的 cookie。 `FormsAuthenticationModule` 會檢查所有傳入的要求，對於具有有效驗證票證的要求，會建立 `GenericPrincipal` 和 `FormsIdentity` 物件與目前要求的關聯。 表單驗證只是一種機制，可在登入時將驗證票證授與給訪客，並在後續要求中剖析該票證以判斷使用者的身分識別。 若要讓 web 應用程式支援使用者帳戶，我們仍需要執行使用者存放區，並新增功能來驗證認證、註冊新使用者，以及其他使用者帳戶相關的工作。

在 ASP.NET 2.0 之前，開發人員都是在攔截來執行所有與使用者帳戶相關的工作。 幸運的是，ASP.NET 團隊已辨識這種缺點，並引進了 ASP.NET 2.0 的成員資格架構。 成員資格架構是 .NET Framework 中的一組類別，可提供用來完成核心使用者帳戶相關工作的程式設計介面。 此架構是在[提供者模型](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)之上建立的，可讓開發人員將自訂的執行插入標準化的 API。

如<a id="Tutorial1"> </a>[*安全性基本概念和 ASP.NET 支援*](../introduction/security-basics-and-asp-net-support-cs.md)教學課程中所述，.NET Framework 隨附兩個內建的成員資格提供者： [`ActiveDirectoryMembershipProvider`](https://msdn.microsoft.com/library/system.web.security.activedirectorymembershipprovider.aspx)和[`SqlMembershipProvider`](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx)。 正如其名，`SqlMembershipProvider` 會使用 Microsoft SQL Server 資料庫做為使用者存放區。 為了在應用程式中使用此提供者，我們需要告訴提供者要使用哪個資料庫做為存放區。 您可能會想到，`SqlMembershipProvider` 需要使用者存放區資料庫擁有特定的資料庫資料表、視圖和預存程式。 我們需要將此預期的架構加入至選取的資料庫。

本教學課程一開始會先檢查將必要的架構加入至資料庫的技術，以便使用 `SqlMembershipProvider`。 接下來，我們將檢查架構中的重要資料表，並討論其用途和重要性。 本教學課程最後會介紹如何告訴 ASP.NET 應用程式，成員資格架構應該使用哪個提供者。

讓我們開始吧！

## <a name="step-1-deciding-where-to-place-the-user-store"></a>步驟1：決定要放置使用者存放區的位置

ASP.NET 應用程式的資料通常會儲存在資料庫中的多個資料表。 在執行 `SqlMembershipProvider` 資料庫架構時，我們必須決定是否要將成員資格架構放在與應用程式資料相同的資料庫或替代資料庫中。

基於下列原因，我建議您在與應用程式資料相同的資料庫中尋找成員資格架構：

- 可**維護性**：將資料封裝在一個資料庫中的應用程式，比有兩個不同資料庫的應用程式更容易瞭解、維護和部署。
- **關聯式完整性**：藉由在與應用程式資料表相同的資料庫中尋找成員相關的資料表，可以在成員資格相關資料表和相關應用程式資料表中的主鍵之間建立[外鍵條件約束](http://en.wikipedia.org/wiki/Foreign_key)。

如果您有多個應用程式使用不同的資料庫，但需要共用一般使用者存放區，則將使用者存放區和應用程式資料分離到不同的資料庫只是合理的。

### <a name="creating-a-database"></a>建立資料庫

我們在第二個教學課程之後所建立的應用程式還不需要資料庫。 不過，我們現在需要一個使用者存放區。 讓我們建立一個，然後將 `SqlMembershipProvider` 提供者所需的架構加入其中（請參閱步驟2）。

> [!NOTE]
> 在此教學課程系列中，我們將使用[Microsoft SQL Server 2005 Express Edition](https://msdn.microsoft.com/sql/Aa336346.aspx)資料庫來儲存應用程式資料表和 `SqlMembershipProvider` 架構。 這項決定的原因有兩個：第一種是因為它是免費的，Express Edition 是最 readably 的可存取版本 SQL Server 2005;其次，SQL Server 2005 Express Edition 資料庫可以直接放在 web 應用程式的 [`App_Data`] 資料夾中，讓它成為將資料庫和 web 應用程式封裝在一個 ZIP 檔案中的標準化，並在沒有任何特殊設定指示或設定選項的情況下重新部署它。 如果您想要遵循 SQL Server 的非 Express Edition 版本，歡迎使用。 步驟幾乎完全相同。 `SqlMembershipProvider` 架構將適用于 Microsoft SQL Server 2000 和更新版本。

在 方案總管中，以滑鼠右鍵按一下 `App_Data` 資料夾，然後選擇 加入新專案。 （如果您在專案中看不到 [`App_Data`] 資料夾，請以滑鼠右鍵按一下方案總管中的專案，選取 [新增] [ASP.NET 資料夾]，然後挑選 [`App_Data`]）。從 [加入新專案] 對話方塊中，加入宣告名為 `SecurityTutorials.mdf`的新 SQL Database。 在本教學課程中，我們會將 `SqlMembershipProvider` 架構新增至此資料庫;在後續的教學課程中，我們將建立額外的資料表來捕捉我們的應用程式資料。

[![將名為 SecurityTutorials 的新 SQL Database 新增至 App_Data 資料夾](creating-the-membership-schema-in-sql-server-cs/_static/image2.png)](creating-the-membership-schema-in-sql-server-cs/_static/image1.png)

**圖 1**：將名為 `SecurityTutorials.mdf` 資料庫的新 SQL Database 新增至 [`App_Data`] 資料夾（[按一下以查看完整大小的影像](creating-the-membership-schema-in-sql-server-cs/_static/image3.png)）

將資料庫新增至 [`App_Data`] 資料夾時，會自動將它包含在 [資料庫總管] 視圖中。 （在 Visual Studio 的非 Express Edition 版本中，資料庫總管稱為伺服器總管）。移至 [資料庫總管]，然後展開 [剛新增的 `SecurityTutorials`] 資料庫。 如果您在畫面上看不到 資料庫總管，請移至 View 功能表並選擇 資料庫總管，或按 Ctrl + Alt + S。 如 [圖 2] 所示，`SecurityTutorials` 資料庫是空的，它不包含任何資料表、沒有任何觀點，而且沒有任何預存程式。

[![SecurityTutorials 資料庫目前是空的](creating-the-membership-schema-in-sql-server-cs/_static/image5.png)](creating-the-membership-schema-in-sql-server-cs/_static/image4.png)

**圖 2**： `SecurityTutorials` 資料庫目前是空的（[按一下以查看完整大小的影像](creating-the-membership-schema-in-sql-server-cs/_static/image6.png)）

## <a name="step-2-adding-thesqlmembershipproviderschema-to-the-database"></a>步驟2：將`SqlMembershipProvider`架構加入至資料庫

`SqlMembershipProvider` 需要在使用者存放區資料庫中安裝一組特定的資料表、視圖和預存程式。 您可以使用[`aspnet_regsql.exe` 工具](https://msdn.microsoft.com/library/ms229862.aspx)來新增這些必要的資料庫物件。 這個檔案位於 [`%WINDIR%\Microsoft.Net\Framework\v2.0.50727\`] 資料夾中。

> [!NOTE]
> `aspnet_regsql.exe` 工具提供命令列功能和圖形化使用者介面。 圖形化介面比較方便使用者，我們將在本教學課程中檢查。 當 `SqlMembershipProvider` 架構需要自動化時（例如在組建腳本或自動化測試案例中），命令列介面就很有用。

`aspnet_regsql.exe` 工具是用來在指定的 SQL Server 資料庫中新增或移除*ASP.NET 應用程式服務*。 ASP.NET 應用程式服務包含 `SqlMembershipProvider` 和 `SqlRoleProvider`的架構，以及其他 ASP.NET 2.0 架構之以 SQL 為基礎的提供者架構。 我們需要提供兩個位的資訊給 `aspnet_regsql.exe` 工具：

- 是否要新增或移除應用程式服務，以及
- 要加入或移除應用程式服務架構的資料庫

在提示資料庫使用的情況下，`aspnet_regsql.exe` 工具會要求我們提供資料庫所在的伺服器名稱、用來連接到資料庫的安全性認證，以及資料庫名稱。 如果您使用非 Express 版本的 SQL Server，您應該已經知道這項資訊，因為它是您在透過 ASP.NET 網頁處理資料庫時，必須透過連接字串提供的相同資訊。 不過，在 `App_Data` 資料夾中使用 SQL Server 2005 Express Edition 資料庫時，判斷伺服器和資料庫名稱會比較複雜一點。

下一節將探討在 `App_Data` 資料夾中為 SQL Server 2005 Express Edition 資料庫指定伺服器和資料庫名稱的直接方式。 如果您不是使用 SQL Server 2005 Express Edition 請隨意跳到安裝應用程式服務一節。

### <a name="determining-the-server-and-database-name-for-a-sql-server-2005-express-edition-database-in-theapp_datafolder"></a>判斷`App_Data`資料夾中 SQL Server 2005 Express Edition 資料庫的伺服器和資料庫名稱

為了使用 `aspnet_regsql.exe` 工具，我們需要知道伺服器和資料庫名稱。 伺服器名稱為 `localhost\InstanceName`。 最有可能的是， *InstanceName*是 `SQLExpress`。 不過，如果您以手動方式安裝 SQL Server 2005 Express Edition （也就是在安裝 Visual Studio 時未自動安裝），則您可以選取不同的實例名稱。

資料庫名稱比較難判斷。 [`App_Data`] 資料夾中的資料庫通常會有一個資料庫名稱，其中包含[全域唯一識別碼](http://en.wikipedia.org/wiki/Globally_Unique_Identifier)以及資料庫檔案的路徑。 我們必須判斷此資料庫名稱，才能透過 `aspnet_regsql.exe`新增應用程式服務架構。

若要確定資料庫名稱，最簡單的方式是透過 SQL Server Management Studio 來檢查它。 SQL Server Management Studio 提供用於管理 SQL Server 2005 資料庫的圖形化介面，但不隨附于 SQL Server 2005 的 Express Edition。 好消息是，[您可以下載](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)免費的 Express Edition SQL Server Management Studio。

> [!NOTE]
> 如果您在桌面上也安裝了非 Express Edition 版本的 SQL Server 2005，則可能會安裝 Management Studio 的完整版本。 您可以使用完整版本來判斷資料庫名稱，遵循與下列 Express 版本相同的步驟。

一開始先關閉 Visual Studio，以確保資料庫檔案上 Visual Studio 所加諸的任何鎖定都已關閉。 接下來，啟動 SQL Server Management Studio 並聯機至 SQL Server 2005 Express Edition 的 `localhost\InstanceName` 資料庫。 如先前所述，實例名稱可能 `SQLExpress`。 針對 [驗證] 選項，選取 [Windows 驗證]。

[![連接到 SQL Server 2005 Express Edition 實例](creating-the-membership-schema-in-sql-server-cs/_static/image8.png)](creating-the-membership-schema-in-sql-server-cs/_static/image7.png)

**圖 3**：連接到 SQL Server 2005 Express Edition 實例（[按一下以觀看完整大小的影像](creating-the-membership-schema-in-sql-server-cs/_static/image9.png)）

連接到 SQL Server 2005 Express Edition 實例之後，Management Studio 會顯示資料庫的資料夾、安全性設定、伺服器物件等等。 如果您展開 [資料庫] 索引標籤，就會看到 `SecurityTutorials.mdf` 資料庫*未*在資料庫實例中註冊-我們需要先附加資料庫。

以滑鼠右鍵按一下 [資料庫] 資料夾，然後從內容功能表選擇 [附加]。 這會顯示 [附加資料庫] 對話方塊。 從這裡按一下 [新增] 按鈕，流覽至 [`SecurityTutorials.mdf`] 資料庫，然後按一下 [確定]。 [圖 4] 顯示選取了 `SecurityTutorials.mdf` 資料庫之後的 [附加資料庫] 對話方塊。 [圖 5] 顯示成功附加資料庫之後 Management Studio 的物件總管。

[![附加 SecurityTutorials .mdf 資料庫](creating-the-membership-schema-in-sql-server-cs/_static/image11.png)](creating-the-membership-schema-in-sql-server-cs/_static/image10.png)

**圖 4**：附加 `SecurityTutorials.mdf` 資料庫（[按一下以觀看完整大小的影像](creating-the-membership-schema-in-sql-server-cs/_static/image12.png)）

[![SecurityTutorials 出現在 [資料庫] 資料夾中](creating-the-membership-schema-in-sql-server-cs/_static/image14.png)](creating-the-membership-schema-in-sql-server-cs/_static/image13.png)

**圖 5**： `SecurityTutorials.mdf` 資料庫會出現在 [資料庫] 資料夾中（[按一下以查看完整大小的影像](creating-the-membership-schema-in-sql-server-cs/_static/image15.png)）

如 [圖 5] 所示，`SecurityTutorials.mdf` 資料庫有一個 abstruse 名稱。 讓我們將它變更為較易記（且更容易輸入）名稱。 以滑鼠右鍵按一下資料庫，從內容功能表中選擇 [重新命名]，然後將它重新命名 `SecurityTutorialsDatabase`。 這不會變更檔案名，只有資料庫用來識別其本身以 SQL Server 的名稱。

[![將資料庫重新命名為 SecurityTutorialsDatabase](creating-the-membership-schema-in-sql-server-cs/_static/image17.png)](creating-the-membership-schema-in-sql-server-cs/_static/image16.png)

**圖 6**：將資料庫重新命名為 `SecurityTutorialsDatabase`（[按一下以查看完整大小的影像](creating-the-membership-schema-in-sql-server-cs/_static/image18.png)）

此時，我們知道 `SecurityTutorials.mdf` 資料庫檔案的伺服器和資料庫名稱：分別是 `localhost\InstanceName` 和 `SecurityTutorialsDatabase`。 我們現在已準備好透過 `aspnet_regsql.exe` 工具安裝應用程式服務。

### <a name="installing-the-application-services"></a>安裝應用程式服務

若要啟動 `aspnet_regsql.exe` 工具，請移至 [開始] 功能表，然後選擇 [執行]。 在文字方塊中輸入 `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\aspnet_regsql.exe`，然後按一下 [確定]。 或者，您可以使用 Windows Explorer 向下切入至適當的資料夾，然後按兩下 `aspnet_regsql.exe` 檔案。 任一種方法都會得到相同的結果。

執行 `aspnet_regsql.exe` 工具而不搭配任何命令列引數，會啟動 ASP.NET SQL Server Setup Wizard 圖形化使用者介面。 此嚮導可讓您輕鬆地在指定的資料庫上新增或移除 ASP.NET 應用程式服務。 Wizard 的第一個畫面（如 [圖 7] 所示）描述工具的用途。

[![使用 [ASP.NET SQL Server 安裝精靈] 來新增成員資格架構](creating-the-membership-schema-in-sql-server-cs/_static/image20.png)](creating-the-membership-schema-in-sql-server-cs/_static/image19.png)

**圖 7**：使用 ASP.NET SQL Server 安裝程式嚮導新增成員資格架構（[按一下以觀看完整大小的影像](creating-the-membership-schema-in-sql-server-cs/_static/image21.png)）

Wizard 中的第二個步驟會詢問我們是否要新增應用程式服務或將其移除。 因為我們想要加入 `SqlMembershipProvider`所需的資料表、視圖和預存程式，請選擇 [設定應用程式服務的 SQL Server] 選項。 之後，如果您想要從資料庫中移除此架構，請重新執行此嚮導，但改為選擇 [從現有的資料庫移除應用程式服務資訊] 選項。

[![選擇 [設定應用程式服務的 SQL Server] 選項](creating-the-membership-schema-in-sql-server-cs/_static/image23.png)](creating-the-membership-schema-in-sql-server-cs/_static/image22.png)

**圖 8**：選擇 [設定應用程式服務的 SQL Server] 選項（[按一下以查看完整大小的影像](creating-the-membership-schema-in-sql-server-cs/_static/image24.png)）

第三個步驟會提示您輸入資料庫資訊：伺服器名稱、驗證資訊，以及資料庫名稱。 如果您已遵循本教學課程，並已將 `SecurityTutorials.mdf` 資料庫新增至 `App_Data`，請將其附加至 `localhost\InstanceName`，並將其重新命名為 `SecurityTutorialsDatabase`，然後使用下列值：

- 伺服器： `localhost\InstanceName`
- Windows 驗證
- 資料庫： `SecurityTutorialsDatabase`

[![輸入資料庫資訊](creating-the-membership-schema-in-sql-server-cs/_static/image26.png)](creating-the-membership-schema-in-sql-server-cs/_static/image25.png)

**圖 9**：輸入資料庫資訊（[按一下以查看完整大小的影像](creating-the-membership-schema-in-sql-server-cs/_static/image27.png)）

輸入資料庫資訊之後，請按 [下一步]。 最後一個步驟會摘要說明將採取的步驟。 按 [下一步] 以安裝應用程式服務，然後按 [完成] 以完成嚮導。

> [!NOTE]
> 如果您使用 Management Studio 附加資料庫，並重新命名資料庫檔案，請務必先卸離資料庫並關閉 Management Studio，然後再重新開啟 Visual Studio。 若要卸離 `SecurityTutorialsDatabase` 資料庫，請在資料庫名稱上按一下滑鼠右鍵，然後從 [工作] 功能表中選擇 [卸離]。

完成嚮導後，請返回 Visual Studio 並流覽至資料庫總管。 展開 [資料表] 資料夾。 您應該會看到一系列的資料表，其名稱開頭為前置詞 `aspnet_`。 同樣地，您可以在 [Views] 和 [預存程式] 資料夾底下找到各種不同的視圖和預存程式。 這些資料庫物件會組成應用程式服務架構。 我們將在步驟3中檢查成員資格和角色特定的資料庫物件。

[![已將各種資料表、視圖和預存程式新增至資料庫](creating-the-membership-schema-in-sql-server-cs/_static/image29.png)](creating-the-membership-schema-in-sql-server-cs/_static/image28.png)

**圖 10**：已將各種資料表、視圖和預存程式新增至資料庫（[按一下以查看完整大小的影像](creating-the-membership-schema-in-sql-server-cs/_static/image30.png)）

> [!NOTE]
> `aspnet_regsql.exe` 工具的圖形化使用者介面會安裝整個應用程式服務架構。 但從命令列執行 `aspnet_regsql.exe` 時，您可以指定要安裝的特定應用程式服務元件（或移除）。 因此，如果您只想要加入 `SqlMembershipProvider` 和 `SqlRoleProvider` 提供者所需的資料表、視圖和預存程式，請從命令列執行 `aspnet_regsql.exe`。 或者，您也可以手動執行 `aspnet_regsql.exe`所使用的適當 T-sql 建立腳本子集。 這些腳本位於 [`WINDIR%\Microsoft.Net\Framework\v2.0.50727\`] 資料夾中，其名稱如 `InstallCommon.sql`、`InstallMembership.sql`、`InstallRoles.sql`、`InstallProfile.sql`、`InstallSqlState.sql`等等。

此時，我們已建立 `SqlMembershipProvider`所需的資料庫物件。 不過，我們仍然需要指示成員資格架構應該使用 `SqlMembershipProvider` （而不是 `ActiveDirectoryMembershipProvider`），而且 `SqlMembershipProvider` 應該使用 `SecurityTutorials` 資料庫。 我們將探討如何指定要使用的提供者，以及如何在步驟4中自訂所選提供者的設定。 但是首先，讓我們進一步探討剛建立的資料庫物件。

## <a name="step-3-a-look-at-the-schemas-core-tables"></a>步驟3：查看架構的核心資料表

在 ASP.NET 應用程式中使用成員資格和角色架構時，會由提供者封裝執行詳細資料。 在未來的教學課程中，我們將透過 .NET Framework 的 `Membership` 和 `Roles` 類別，與這些架構進行介面互動。 使用這些高階 Api 時，我們不需要擔心自己的低層級詳細資料，像是執行哪些查詢，或是 `SqlMembershipProvider` 和 `SqlRoleProvider`修改了哪些資料表。

為此，我們可以放心地使用成員資格和角色架構，而不需要探索在步驟2中建立的資料庫架構。 不過，建立資料表以儲存應用程式資料時，我們可能需要建立與使用者或角色相關的實體。 在應用程式資料表與步驟2中所建立的資料表之間建立外鍵條件約束時，有助於熟悉 `SqlMembershipProvider` 和 `SqlRoleProvider` 架構。 此外，在某些罕見的情況下，我們可能需要直接在資料庫層級與使用者和角色存放區進行互動（而不是透過 `Membership` 或 `Roles` 類別）。

### <a name="partitioning-the-user-store-into-applications"></a>將使用者存放區分割成應用程式

成員資格和角色架構的設計，讓單一使用者和角色存放區可以在許多不同的應用程式之間共用。 使用成員資格或角色架構的 ASP.NET 應用程式必須指定要使用的應用程式分割。 簡單地說，多個 web 應用程式可以使用相同的使用者和角色存放區。 [圖 11] 說明分割成三個應用程式的使用者和角色存放區： HRSite、CustomerSite 和 SalesSite。 這三個 web 應用程式都有自己獨特的使用者和角色，但它們都是在相同的資料庫資料表中實際儲存其使用者帳戶和角色資訊。

[![的使用者帳戶可能會分割到多個應用程式](creating-the-membership-schema-in-sql-server-cs/_static/image32.png)](creating-the-membership-schema-in-sql-server-cs/_static/image31.png)

**圖 11**：使用者帳戶可能會分割到多個應用程式（[按一下以查看完整大小的影像](creating-the-membership-schema-in-sql-server-cs/_static/image33.png)）

`aspnet_Applications` 資料表會定義這些資料分割。 每個使用資料庫來儲存使用者帳戶資訊的應用程式，都會以此資料表中的資料列來表示。 `aspnet_Applications` 資料表有四個數據行： `ApplicationId`、`ApplicationName`、`LoweredApplicationName`和 `Description`。 `ApplicationId` 屬於[`uniqueidentifier`](https://msdn.microsoft.com/library/ms187942.aspx)類型，而且是資料表的主鍵;`ApplicationName` 為每個應用程式提供唯一的易記名稱。

其他成員資格和角色相關的資料表會連結回到 `aspnet_Applications`中的 [`ApplicationId`] 欄位。 例如，`aspnet_Users` 資料表（其中包含每個使用者帳戶的記錄）具有 `ApplicationId` 外鍵欄位;`aspnet_Roles` 資料表的 ditto。 這些資料表中的 [`ApplicationId`] 欄位會指定使用者帳戶或角色所屬的應用程式分割。

### <a name="storing-user-account-information"></a>儲存使用者帳戶資訊

使用者帳戶資訊會存放在兩個數據表中： `aspnet_Users` 和 `aspnet_Membership`。 `aspnet_Users` 資料表包含保留重要使用者帳戶資訊的欄位。 三個最相關的資料行為：

- `UserId`
- `UserName`
- `ApplicationId`

`UserId` 是主要索引鍵（和類型 `uniqueidentifier`）。 `UserName` 的類型 `nvarchar(256)`，而且密碼會構成使用者的認證。 （使用者的密碼會儲存在 `aspnet_Membership` 資料表中）。`ApplicationId` 會將使用者帳戶連結至 `aspnet_Applications`中的特定應用程式。 `UserName` 和 `ApplicationId` 資料行上有複合[`UNIQUE` 條件約束](https://msdn.microsoft.com/library/ms191166.aspx)。 這可確保在指定的應用程式中，每個使用者名稱都是唯一的，但允許在不同的應用程式中使用相同的 `UserName`。

`aspnet_Membership` 表包含額外的使用者帳戶資訊，例如使用者的密碼、電子郵件地址、上次登入日期和時間等等。 `aspnet_Users` 和 `aspnet_Membership` 資料表中的記錄之間有一對一的對應關係。 這項關聯性是由 `aspnet_Membership`中的 [`UserId`] 欄位所確保，這會當做資料表的主要索引鍵。 就像 `aspnet_Users` 資料表一樣，`aspnet_Membership` 包含將此資訊系結至特定應用程式分割的 `ApplicationId` 欄位。

### <a name="securing-passwords"></a>保護密碼

密碼資訊會儲存在 `aspnet_Membership` 資料表中。 此 `SqlMembershipProvider` 可讓您使用下列三種技術之一，將密碼儲存在資料庫中：

- **Clear** -密碼會以純文字格式儲存在資料庫中。 我強烈不鼓勵使用此選項。 如果資料庫遭到入侵，則是由尋找後端的駭客或具有資料庫存取權的心存不滿員工所提供-每一位使用者的認證都是在此取得。
- **哈**希-密碼會使用單向雜湊演算法和隨機產生的 salt 值進行雜湊處理。 此雜湊值（連同 salt）會儲存在資料庫中。
- 已**加密**-密碼的加密版本會儲存在資料庫中。

使用的密碼儲存技術取決於 `Web.config`中指定的 `SqlMembershipProvider` 設定。 我們將在步驟4中探討自訂 `SqlMembershipProvider` 設定。 預設行為是儲存密碼的雜湊。

負責儲存密碼的資料行是 `Password`、`PasswordFormat`和 `PasswordSalt`。 `PasswordFormat` 是 `int` 類型的欄位，其值表示用來儲存密碼的技術：0表示清除;1表示雜湊;2表示已加密。 無論所使用的密碼儲存技術為何，都會將隨機產生的字串指派給 `PasswordSalt`。只有在計算密碼的雜湊時，才會使用 `PasswordSalt` 的值。 最後，[`Password`] 欄包含實際的密碼資料，也就是純文字密碼、密碼雜湊或加密的密碼。

[表 1] 說明當儲存密碼 MySecret 時，這三個數據行的外觀可能會類似于各種儲存技術！ 。

| **儲存技術&lt;\_o3a\_p/&gt;** | **密碼&lt;\_o3a\_p/&gt;** | **PasswordFormat&lt;\_o3a\_p/&gt;** | **PasswordSalt&lt;\_o3a\_p/&gt;** |
| --- | --- | --- | --- |
| 清除 | MySecret! | 0 | tTnkPlesqissc2y2SMEygA = = |
| 進行 | 2oXm6sZHWbTHFgjgkGQsc2Ec9ZM = | 1 | wFgjUfhdUFOCKQiI61vtiQ = = |
| 加密 | 62RZgDvhxykkqsMchZ0Yly7HS6onhpaoCYaRxV8g0F4CW56OXUU3e7Inza9j9BKp | 2 | LSRzhGS/aa/oqAXGLHJNBw = = |

**表 1**：儲存密碼時，密碼相關欄位的範例值 MySecret！

> [!NOTE]
> `SqlMembershipProvider` 所使用的特定加密或雜湊演算法是由 `<machineKey>` 元素中的設定所決定。 我們在<a id="Tutorial3"> </a>[*表單驗證設定和 Advanced 主題*](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md)教學課程的步驟3中討論過此設定元素。

### <a name="storing-roles-and-role-associations"></a>儲存角色和角色關聯

Roles 架構可讓開發人員定義一組角色，並指定哪些使用者屬於哪些角色。 這項資訊是在資料庫中透過兩個數據表來捕捉： `aspnet_Roles` 和 `aspnet_UsersInRoles`。 `aspnet_Roles` 資料表中的每筆記錄都代表特定應用程式的角色。 與 `aspnet_Users` 資料表非常類似，`aspnet_Roles` 資料表有三個與我們討論相關的資料行：

- `RoleId`
- `RoleName`
- `ApplicationId`

`RoleId` 是主要索引鍵（和類型 `uniqueidentifier`）。 `RoleName` 是 `nvarchar(256)` 類型。 和 `ApplicationId` 會將使用者帳戶連結至 `aspnet_Applications`中的特定應用程式。 `RoleName` 和 `ApplicationId` 資料行上有一個複合 `UNIQUE` 條件約束，確保在給定的應用程式中，每個角色名稱都是唯一的。

`aspnet_UsersInRoles` 資料表可作為使用者與角色之間的對應。 只有兩個數據行-`UserId` 和 `RoleId`，以及兩者組成複合主鍵。

## <a name="step-4-specifying-the-provider-and-customizing-its-settings"></a>步驟4：指定提供者並自訂其設定

所有支援提供者模型的架構（例如成員資格和角色架構）-缺乏執行詳細資料本身，而是改為將該責任委派給提供者類別。 在成員資格架構的情況下，`Membership` 類別會定義用來管理使用者帳戶的 API，但不會直接與任何使用者存放區互動。 相反地，`Membership` 類別的方法會將要求交給已設定的提供者-我們將使用 `SqlMembershipProvider`。 當我們叫用 `Membership` 類別中的其中一個方法時，成員資格架構如何知道如何將呼叫委派給 `SqlMembershipProvider`？

`Membership` 類別具有[`Providers` 屬性](https://msdn.microsoft.com/library/system.web.security.membership.providers.aspx)，其中包含可供成員資格架構使用之所有已註冊提供者類別的參考。 每個已註冊的提供者都有相關聯的名稱和類型。 此名稱提供了方便的方式來參考 `Providers` 集合中的特定提供者，而類型則會識別提供者類別。 此外，每個已註冊的提供者都可能包含設定。 成員資格架構的設定值包括 `passwordFormat` 和 `requiresUniqueEmail`，還有其他許多專案。 如需 `SqlMembershipProvider`所使用之設定設定的完整清單，請參閱表2。

`Providers` 屬性的內容是透過 web 應用程式的設定來指定。 根據預設，所有 web 應用程式都有一個名為 `AspNetSqlMembershipProvider` 類型為 `SqlMembershipProvider`的提供者。 這個預設成員資格提供者會在 `machine.config` 中註冊（位於 `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG)`：

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample1.xml)]

如上面的標記所示， [`<membership>` 元素](https://msdn.microsoft.com/library/1b9hw62f.aspx)會定義成員資格架構的設定，而[`<providers>` 子項目](https://msdn.microsoft.com/library/6d4936ht.aspx)則指定已註冊的提供者。 您可以使用[`<add>`](https://msdn.microsoft.com/library/whae3t94.aspx)或[`<remove>`](https://msdn.microsoft.com/library/aykw9a6d.aspx)元素來新增或移除提供者;請使用[`<clear>`](https://msdn.microsoft.com/library/t062y6yc.aspx)元素來移除所有目前註冊的提供者。 如上面的標記所示，`machine.config` 會將名為 `AspNetSqlMembershipProvider` 的提供者加入 `SqlMembershipProvider`類型。

除了 `name` 和 `type` 屬性以外，`<add>` 元素還包含屬性，可定義各種設定的值。 [表 2] 列出可用的 `SqlMembershipProvider`特定的設定，以及每個設定的描述。

> [!NOTE]
> [表 2] 中所述的任何預設值都會參考 `SqlMembershipProvider` 類別中定義的預設值。 請注意，`AspNetSqlMembershipProvider` 中的所有設定都不會對應到 `SqlMembershipProvider` 類別的預設值。 例如，如果未在成員資格提供者中指定，`requiresUniqueEmail` 設定會預設為 true。 不過，`AspNetSqlMembershipProvider` 會藉由明確指定 `false`的值來覆寫這個預設值。

| **設定&lt;\_o3a\_p/&gt;** | **描述&lt;\_o3a\_p/&gt;** |
| --- | --- |
| `ApplicationName` | 回想一下，成員架構可讓單一使用者存放區分割成多個應用程式。 此設定表示成員資格提供者所使用的應用程式分割區名稱。 如果未明確指定這個值，則會在執行時間將它設定為應用程式虛擬根路徑的值。 |
| `commandTimeout` | 指定 SQL 命令逾時值（以秒為單位）。 預設值是 30。 |
| `connectionStringName` | 要用來連接到使用者存放區資料庫之 `<connectionStrings>` 元素中的連接字串名稱。 這是必要值。 |
| `description` | 提供已註冊提供者的易記描述。 |
| `enablePasswordRetrieval` | 指定使用者是否可能取得其忘記密碼的密碼。 預設值是 `false`。 |
| `enablePasswordReset` | 指出是否允許使用者重設其密碼。 預設值為 `true`。 |
| `maxInvalidPasswordAttempts` | 在使用者遭到鎖定之前，指定的 `passwordAttemptWindow` 可能發生的失敗登入嘗試次數上限。預設值為5。 |
| `minRequiredNonalphanumericCharacters` | 必須出現在使用者密碼中的非英數位元數目下限。 這個值必須介於0到128之間;預設值為1。 |
| `minRequiredPasswordLength` | 密碼所需的字元數下限。 這個值必須介於0到128之間;預設值為7。 |
| `name` | 已註冊之提供者的名稱。 這是必要值。 |
| `passwordAttemptWindow` | 追蹤登入嘗試失敗的分鐘數。 如果使用者在此指定的視窗內提供不正確登入認證 `maxInvalidPasswordAttempts` 次，就會被鎖定。預設值為10。 |
| `PasswordFormat` | 密碼儲存格式： `Clear`、`Hashed`或 `Encrypted`。 預設為 `Hashed`。 |
| `passwordStrengthRegularExpression` | 如果有提供，則在建立新帳戶或變更其密碼時，會使用此正則運算式來評估使用者所選取密碼的強度。 預設值為空字串。 |
| `requiresQuestionAndAnswer` | 指定使用者在抓取或重設密碼時是否必須回答他的安全性問題。 預設值是 `true`。 |
| `requiresUniqueEmail` | 指出指定之應用程式分割區中的所有使用者帳戶是否都必須有唯一的電子郵件地址。 預設值是 `true`。 |
| `type` | 指定提供者的類型。 這是必要值。 |

**表 2**：成員資格和 `SqlMembershipProvider` 設定

除了 `AspNetSqlMembershipProvider`以外，其他成員資格提供者也可以藉由將類似的標記新增至 `Web.config` 檔案，逐一註冊應用程式。

> [!NOTE]
> 角色架構的運作方式大致相同： `machine.config` 中有預設的已註冊角色提供者，而且可以在 `Web.config`中以應用程式為基礎自訂已註冊的提供者。 在未來的教學課程中，我們將詳細探討角色架構和其設定標記。

### <a name="customizing-thesqlmembershipprovidersettings"></a>自訂`SqlMembershipProvider`設定

預設 `SqlMembershipProvider` （`AspNetSqlMembershipProvider`）將其 `connectionStringName` 屬性設定為 [`LocalSqlServer`]。 與 `AspNetSqlMembershipProvider` 提供者一樣，連接字串名稱 `LocalSqlServer` 是在 `machine.config`中定義。

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample2.xml)]

如您所見，此連接字串會定義位於的 SQL 2005 Express Edition 資料庫 |DataDirectory | aspnetdb.mdf。 字串 |DataDirectory | 會在執行時間轉譯以指向 `~/App_Data/` 目錄，因此資料庫路徑 |DataDirectory | aspnetdb.mdf 會轉譯成 `~/App_Data`/`aspnet.mdf`。

如果我們未在應用程式的 `Web.config` 檔中指定任何成員資格提供者資訊，應用程式會使用預設註冊的成員資格提供者，`AspNetSqlMembershipProvider`。 如果 `~/App_Data/aspnet.mdf` 資料庫不存在，ASP.NET 執行時間會自動建立它並加入應用程式服務架構。 不過，我們不想要使用 `aspnet.mdf` 資料庫;相反地，我們想要使用我們在步驟2中建立的 `SecurityTutorials.mdf` 資料庫。 這項修改可以透過下列兩種方式的其中一種來完成：

- 在<strong>`Web.config`</strong>中<strong>指定</strong><strong>`LocalSqlServer`</strong><strong>連接字串名稱</strong>的值<strong>。</strong> 藉由覆寫 `Web.config`中的 `LocalSqlServer` 連接字串名稱值，我們可以使用預設註冊的成員資格提供者（`AspNetSqlMembershipProvider`），並讓它正確地使用 `SecurityTutorials.mdf` 資料庫。 如果您是具有 `AspNetSqlMembershipProvider`所指定之設定設定的內容，這個方法就沒問題。 如需這項技術的詳細資訊，請參閱[Scott Guthrie](https://weblogs.asp.net/scottgu/)的 blog 文章，[將 ASP.NET 2.0 應用程式服務設定為使用 SQL Server 2000 或 SQL Server 2005](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)。
- <strong>新增`SqlMembershipProvider`類型的已註冊提供者</strong> <strong>，並將其</strong><strong>`connectionStringName`</strong><strong>設定設為指向</strong><strong>`SecurityTutorials.mdf`</strong><strong>資料庫。</strong> 當您想要自訂除了資料庫連接字串以外的其他設定屬性時，這個方法很有用。 在我自己的專案中，我一律會使用這種方法，因為它具有彈性和可讀性。

我們必須先在 `Web.config`的 [`<connectionStrings>`] 區段中新增適當的連接字串值，才可以加入參考 `SecurityTutorials.mdf` 資料庫的新註冊提供者。 下列標記會加入名為 `SecurityTutorialsConnectionString` 的新連接字串，參考 `App_Data` 資料夾中的 SQL Server 2005 Express Edition `SecurityTutorials.mdf` 資料庫。

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample3.xml)]

> [!NOTE]
> 如果您使用的是替代資料庫檔案，請視需要更新連接字串。 如需有關形成正確連接字串的詳細資訊，請參閱[ConnectionStrings.com](http://www.connectionstrings.com/)。

接下來，將下列成員資格設定標記新增至 `Web.config` 檔案。 此標記會註冊名為 `SecurityTutorialsSqlMembershipProvider`的新提供者。

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample4.xml)]

除了註冊 `SecurityTutorialsSqlMembershipProvider` 提供者之外，上述標記也會將 `SecurityTutorialsSqlMembershipProvider` 定義為預設提供者（透過 `<membership>` 元素中的 `defaultProvider` 屬性）。 回想一下，成員資格架構可以有多個已註冊的提供者。 由於 `AspNetSqlMembershipProvider` 會註冊為 `machine.config`中的第一個提供者，因此它會做為預設提供者，除非我們另有指示。

目前，我們的應用程式有兩個已註冊的提供者： `AspNetSqlMembershipProvider` 和 `SecurityTutorialsSqlMembershipProvider`。 不過，在註冊 `SecurityTutorialsSqlMembershipProvider` 提供者之前，我們可能已清除所有先前註冊的提供者，方法是在 `<add>` 元素之前新增[`<clear />` 元素](https://msdn.microsoft.com/library/t062y6yc.aspx)。 這會從已註冊的提供者清單中清除 `AspNetSqlMembershipProvider`，這表示 `SecurityTutorialsSqlMembershipProvider` 會是唯一註冊的成員資格提供者。 如果我們使用這種方法，則不需要將 `SecurityTutorialsSqlMembershipProvider` 標示為預設提供者，因為它會是唯一註冊的成員資格提供者。 如需使用 `<clear />`的詳細資訊，請參閱[在新增提供者時使用 `<clear />`](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx)。

請注意，`SecurityTutorialsSqlMembershipProvider`的 `connectionStringName` 設定會參考剛新增的 `SecurityTutorialsConnectionString` 連接字串名稱，而且其 `applicationName` 設定已設定為 SecurityTutorials 的值。 此外，`requiresUniqueEmail` 設定已設定為 [`true`]。 所有其他設定選項都與 `AspNetSqlMembershipProvider`中的值相同。 如有需要，您可以隨意在此處進行任何設定修改。 例如，您可以藉由要求兩個非英數位元，而不是一個字元，或將密碼長度增加為八個字元，而不是七個字元，藉此加強密碼強度。

> [!NOTE]
> 回想一下，成員架構可讓單一使用者存放區分割成多個應用程式。 成員資格提供者的 `applicationName` 設定會指出提供者在使用使用者存放區時所使用的應用程式。 請務必明確設定 `applicationName` configuration 設定的值，因為如果未明確設定 `applicationName`，它會在執行時間指派給 web 應用程式的虛擬根路徑。 只要應用程式的虛擬根路徑不會變更，這就能正常運作，但如果您將應用程式移到不同的路徑，`applicationName` 設定也會變更。 發生這種情況時，成員資格提供者將會開始使用與先前所用不同的應用程式分割區。 在移動前建立的使用者帳戶會位於不同的應用程式分割區，而那些使用者將無法再登入網站。 如需有關此問題的更深入討論，請參閱[設定 ASP.NET 2.0 成員資格和其他提供者時，一律設定 `applicationName` 屬性](https://weblogs.asp.net/scottgu/443634)。

## <a name="summary"></a>總結

此時，我們有一個資料庫具有已設定的應用程式服務（`SecurityTutorials.mdf`），並已設定 web 應用程式，讓成員資格架構使用我們剛才註冊的 `SecurityTutorialsSqlMembershipProvider` 提供者。 這個已註冊的提供者屬於 `SqlMembershipProvider` 類型，而且其 `connectionStringName` 設定為適當的連接字串（`SecurityTutorialsConnectionString`），且其 `applicationName` 值已明確設定。

我們現在已準備好使用應用程式中的成員資格架構。 在下一個教學課程中，我們將探討如何建立新的使用者帳戶。 接下來，我們將探索驗證使用者、執行以使用者為基礎的授權，以及在資料庫中儲存額外的使用者相關資訊。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [設定 ASP.NET 2.0 成員資格和其他提供者時，一律設定 `applicationName` 屬性](https://weblogs.asp.net/scottgu/443634)
- [將 ASP.NET 2.0 應用程式服務設定為使用 SQL Server 2000 或 SQL Server 2005](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)
- [下載 SQL Server Management Studio Express Edition](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)
- [檢查 ASP.NET 2.0 s 成員資格、角色和設定檔](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [成員資格提供者的 `<add>` 元素](https://msdn.microsoft.com/library/whae3t94.aspx)
- [`<membership>` 元素](https://msdn.microsoft.com/library/1b9hw62f.aspx)
- [成員資格的 `<providers>` 元素](https://msdn.microsoft.com/library/6d4936ht.aspx)
- [新增提供者時使用 `<clear />`](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx)
- [直接使用 `SqlMembershipProvider`](http://aspnet.4guysfromrolla.com/articles/091207-1.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>本教學課程中所含主題的影片訓練

- [了解 ASP.NET 成員資格](../../../videos/authentication/understanding-aspnet-memberships.md)
- [設定 SQL 使用成員資格結構描述](../../../videos/authentication/configuring-sql-to-work-with-membership-schemas.md)
- [變更預設成員資格結構描述中的成員資格設定](../../../videos/authentication/changing-membership-settings-in-the-default-membership-schema.md)

### <a name="about-the-author"></a>關於作者

Scott Mitchell，自1998起，有多個 ASP/ASP. NET 書籍和創辦人的4GuysFromRolla.com。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是 *[在24小時內讓自己的 ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 。 Scott 可以在[mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)或透過他在[http://ScottOnWriting.NET](http://scottonwriting.net/)的 blog。

### <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Alicja Maziarz。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在[mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com)的那一行下拉式。

> [!div class="step-by-step"]
> [下一步](creating-user-accounts-cs.md)
