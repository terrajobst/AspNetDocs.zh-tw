---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/debugging-stored-procedures-cs
title: 偵錯工具預存C#程式（） |Microsoft Docs
author: rick-anderson
description: Visual Studio Professional 和 Team System 版本可讓您在 SQL Server 內設定中斷點，並逐步執行預存程式，讓偵錯工具得以儲存 。
ms.author: riande
ms.date: 08/03/2007
ms.assetid: c655c324-2ffa-4c21-8265-a254d79a693d
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/debugging-stored-procedures-cs
msc.type: authoredcontent
ms.openlocfilehash: 12a8500b107345b9cc9ab457016fdef09ca1bb9d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78533275"
---
# <a name="debugging-stored-procedures-c"></a>針對預存程序進行偵錯 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_74_CS.zip)或[下載 PDF](debugging-stored-procedures-cs/_static/datatutorial74cs1.pdf)

> Visual Studio Professional 和 Team System 版本可讓您設定中斷點，並逐步執行 SQL Server 中的預存程式，讓偵錯工具的預存程式輕鬆完成，就像在偵錯工具中的程式碼一樣。 本教學課程示範預存程式的直接資料庫偵錯工具和應用程式調試。

## <a name="introduction"></a>簡介

Visual Studio 提供豐富的調試經驗。 只要按幾下滑鼠按鍵，就可以使用中斷點來停止執行程式，並檢查其狀態和控制流程。 除了偵錯工具程式碼，Visual Studio 還支援從 SQL Server 內對預存程式進行偵錯工具。 就像中斷點可以在 ASP.NET 程式碼後置類別或商務邏輯層類別的程式碼中設定，因此也可以將它們放在預存程式中。

在本教學課程中，我們將探討如何從 Visual Studio 內的伺服器總管逐步執行預存程式，以及如何設定在從執行中的 ASP.NET 應用程式呼叫預存程式時所叫用的中斷點。

> [!NOTE]
> 可惜的是，預存程式只能透過 Visual Studio 的 Professional 和 Team 系統版本進行逐步執行和調試。 如果您使用的是 Visual Web Developer 或 standard 版本的 Visual Studio，就可以在我們逐步執行檢查預存程式所需的步驟時進行閱讀，但是您無法在電腦上複寫這些步驟。

## <a name="sql-server-debugging-concepts"></a>SQL Server 的調試概念

Microsoft SQL Server 2005 的設計，是為了提供與[Common Language Runtime （CLR）](https://msdn.microsoft.com/netframework/aa497266.aspx)的整合，這是所有 .net 元件所使用的執行時間。 因此，SQL Server 2005 支援 managed 資料庫物件。 也就是說，您可以建立像是C#預存程式和使用者定義函數（udf）等資料庫物件，做為類別中的方法。 這可讓這些預存程式和 Udf 利用 .NET Framework 中的功能，以及自訂的類別。 當然，SQL Server 2005 也提供 T-sql 資料庫物件的支援。

SQL Server 2005 提供 T-sql 和 managed 資料庫物件的偵錯工具支援。 不過，這些物件只能透過 Visual Studio 2005 Professional 和 Team Systems 版本進行調試。 在本教學課程中，我們將檢查 T-sql 資料庫物件的調試。 後續的教學課程將探討如何對 managed 資料庫物件進行調試。

[SQL Server 2005 CLR 整合小組](https://blogs.msdn.com/sqlclr/default.aspx)的[SQL Server 2005 blog 專案中的 T-sql 和 CLR 調試功能總覽](https://blogs.msdn.com/sqlclr/archive/2006/06/29/651644.aspx)，強調了三種從 Visual Studio 進行 SQL Server 2005 物件的方式：

- **直接資料庫偵錯工具（DDD）** -從伺服器總管我們可以逐步執行任何 t-sql 資料庫物件，例如預存程式和 udf。 我們將在步驟1中檢查 DDD。
- **應用程式偵錯工具**-我們可以在資料庫物件內設定中斷點，然後執行我們的 ASP.NET 應用程式。 執行資料庫物件時，將會叫用中斷點，並將控制權移交給偵錯工具。 請注意，透過應用程式的偵錯工具，我們無法從應用程式代碼逐步執行資料庫物件。 我們必須在要讓偵錯工具停止的預存程式或 Udf 中明確設定中斷點。 從步驟2開始就會檢查應用程式的偵錯工具。
- **從 SQL Server 專案**Visual Studio Professional 和 Team Systems 版本進行的偵錯工具包含一個常用來建立受控資料庫物件的 SQL Server 專案類型。 我們將在下一個教學課程中，使用 SQL Server 專案和其內容進行檢查。

Visual Studio 可以在本機和遠端 SQL Server 實例上，進行預存程式的 debug。 本機 SQL Server 實例是與 Visual Studio 安裝在同一部電腦上的實例。 如果您使用的 SQL Server 資料庫不在開發電腦上，則會將它視為遠端實例。 在這些教學課程中，我們使用了本機 SQL Server 實例。 在遠端 SQL server 實例上執行的預存程式比對本機實例上的預存程式時，需要更多的設定步驟。

如果您使用本機 SQL Server 實例，您可以從步驟1開始，並逐步完成本教學課程。 不過，如果您使用的是遠端 SQL Server 實例，您必須先確定在進行偵錯工具時，您會使用在遠端實例上具有 SQL Server 登入的 Windows 使用者帳戶，來記錄到您的開發電腦。 此外，此資料庫登入和用來從執行中 ASP.NET 應用程式連接到資料庫的資料庫登入，都必須是 `sysadmin` 角色的成員。 如需有關設定 Visual Studio 和 SQL Server 來檢查遠端實例的詳細資訊，請參閱本教學課程結尾處的「遠端實例上的 SQL Database 物件的偵錯工具」一節。

最後要瞭解的是，對 T-sql 資料庫物件的偵錯工具支援不像 .NET 應用程式的偵錯工具支援一樣功能豐富。 例如，中斷點條件和篩選器不受支援，只有一部分的偵錯工具視窗可用，您無法使用 [編輯後繼續]，[即時運算] 視窗也不會呈現無用，依此類推。 如需詳細資訊，請參閱[偵錯工具命令和功能的限制](https://msdn.microsoft.com/library/ms165035(VS.80).aspx)。

## <a name="step-1-directly-stepping-into-a-stored-procedure"></a>步驟1：直接逐步執行預存程式

Visual Studio 可讓您輕鬆地直接進行資料庫物件的 debug。 讓我們看看如何使用直接資料庫的偵錯工具（DDD）功能，逐步執行 Northwind 資料庫中的 `Products_SelectByCategoryID` 預存程式。 正如其名，`Products_SelectByCategoryID` 會傳回特定分類的產品資訊;它是在使用具[類型資料集的現有預存程式 tableadapter](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)教學課程中建立的。 一開始請前往伺服器總管，然後展開 Northwind 資料庫節點。 接下來，向下切入至 [預存程式] 資料夾，以滑鼠右鍵按一下 [`Products_SelectByCategoryID` 預存程式]，然後從內容功能表選擇 [逐步執行預存程式] 選項。 這會啟動偵錯工具。

因為 `Products_SelectByCategoryID` 預存程式預期會有 `@CategoryID` 的輸入參數，所以我們會要求您提供此值。 輸入1，這會傳回飲料的相關資訊。

![針對 @CategoryID 參數使用值1](debugging-stored-procedures-cs/_static/image1.png)

**圖 1**：使用值1做為 `@CategoryID` 參數

提供 `@CategoryID` 參數的值之後，就會執行預存程式。 不過，偵錯工具不會執行到完成，而是在第一個語句上暫停執行。 請注意邊界中的黃色箭號，表示預存程式中的目前位置。 您可以透過監看式視窗或將滑鼠停留在預存程式的參數名稱上，來查看和編輯參數值。

[![偵錯工具已在預存程式的第一個語句上暫停](debugging-stored-procedures-cs/_static/image3.png)](debugging-stored-procedures-cs/_static/image2.png)

**圖 2**：偵錯工具已在預存程式的第一個語句上暫停（[按一下以查看完整大小的影像](debugging-stored-procedures-cs/_static/image4.png)）

若要一次逐步執行預存程式一個語句，請按一下工具列中的 [不進入函式] 按鈕，或按 F10 鍵。 `Products_SelectByCategoryID` 預存套裝程式含單一 `SELECT` 語句，因此按 F10 會跳過單一語句，並完成預存程式的執行。 在預存程式完成之後，其輸出會出現在 [輸出] 視窗中，而偵錯工具將會終止。

> [!NOTE]
> T-sql 調試會在語句層級進行;您不能逐步執行 `SELECT` 語句。

## <a name="step-2-configuring-the-website-for-application-debugging"></a>步驟2：設定網站進行應用程式的偵錯工具

雖然直接從伺服器總管調試預存程式很方便，但在許多情況下，我們會比較興趣在 ASP.NET 應用程式中呼叫預存程式。 我們可以在 Visual Studio 中，將中斷點新增至預存程式，然後開始 ASP.NET 應用程式的偵錯工具。 從應用程式叫用含有中斷點的預存程式時，執行將會在中斷點中斷，而我們可以查看和變更預存程式的參數值，並逐步執行其語句，就像我們在步驟1中所做的一樣。

我們必須先指示 ASP.NET web 應用程式與 SQL Server 偵錯工具整合，才能開始從應用程式呼叫名為的預存程式。 首先，以滑鼠右鍵按一下 方案總管（`ASPNET_Data_Tutorial_74_CS`）中的網站名稱。 從操作功能表中選擇 [屬性頁] 選項，選取左側的 [啟動選項] 專案，然後勾選 [偵錯工具] 區段中的 [SQL Server] 核取方塊（請參閱 [圖 3]）。

[![核取 [應用程式] 屬性頁中的 [SQL Server] 核取方塊](debugging-stored-procedures-cs/_static/image6.png)](debugging-stored-procedures-cs/_static/image5.png)

**圖 3**：核取應用程式的屬性頁中的 [SQL Server] 核取方塊（[按一下以查看完整大小的影像](debugging-stored-procedures-cs/_static/image7.png)）

此外，我們還需要更新應用程式所使用的資料庫連接字串，以便停用連接共用。 當資料庫的連接關閉時，對應的 `SqlConnection` 物件會放在可用連接的集區中。 建立資料庫的連接時，可以從這個集區抓取可用的連線物件，而不需要建立和建立新的連接。 此連線物件共用是一種效能增強功能，而且預設為啟用。 不過，在進行偵錯工具時，我們想要關閉連接共用，因為使用從集區取得的連接時，不會正確地重新建立偵錯工具基礎結構。

若要停用連接共用，請更新 `Web.config` 中的 `NORTHWNDConnectionString`，使其包含 `Pooling=false` 的設定。

[!code-xml[Main](debugging-stored-procedures-cs/samples/sample1.xml)]

> [!NOTE]
> 一旦完成 ASP.NET 應用程式的 SQL Server 的偵錯工具，請務必從連接字串移除 `Pooling` 設定（或將它設定為 `Pooling=true`），以恢復連接共用。

此時，已將 ASP.NET 應用程式設定為允許 Visual Studio 在透過 web 應用程式叫用時，SQL Server 資料庫物件進行 debug。 現在剩下的工作就是將中斷點新增至預存程式，然後開始進行偵錯工具！

## <a name="step-3-adding-a-breakpoint-and-debugging"></a>步驟3：加入中斷點和調試

開啟 `Products_SelectByCategoryID` 預存程式，並在 `SELECT` 的語句開頭處設定中斷點，方法是按一下適當位置的邊界，或將游標放在 `SELECT` 語句的開頭，然後按 F9。 如 [圖 4] 所示，中斷點會顯示為邊界中的紅色圓圈。

[![在 Products_SelectByCategoryID 預存程式中設定中斷點](debugging-stored-procedures-cs/_static/image9.png)](debugging-stored-procedures-cs/_static/image8.png)

**圖 4**：在 `Products_SelectByCategoryID` 預存程式中設定中斷點（[按一下以查看完整大小的影像](debugging-stored-procedures-cs/_static/image10.png)）

為了讓 SQL database 物件可以透過用戶端應用程式進行調試，必須將資料庫設定為支援應用程式的偵測。 當您第一次設定中斷點時，應該會自動開啟此設定，但仔細檢查會很謹慎。 以滑鼠右鍵按一下伺服器總管中的 [`NORTHWND.MDF`] 節點。 內容功能表應該包含一個已核取的功能表項目，名為 [應用程式偵錯工具]。

![確定已啟用 [應用程式偵錯工具] 選項](debugging-stored-procedures-cs/_static/image11.png)

**圖 5**：確定已啟用應用程式偵錯工具選項

在設定中斷點並啟用應用程式偵錯工具的情況下，我們就可以在從 ASP.NET 應用程式呼叫預存程式時，進行偵錯工具。 請前往 [偵錯工具] 功能表，然後選擇 [開始偵測]、按 F5，或按一下工具列中的綠色播放圖示，來啟動偵錯工具。 這會啟動偵錯工具並啟動網站。

[使用具類型資料集 tableadapter 教學課程的現有預存程式](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)，在中建立 `Products_SelectByCategoryID` 預存程式。 其對應的網頁（`~/AdvancedDAL/ExistingSprocs.aspx`）包含一個 GridView，其中顯示此預存程式所傳回的結果。 透過瀏覽器造訪此頁面。 到達頁面時，將會叫用 `Products_SelectByCategoryID` 預存程式中的中斷點，並將控制權傳回給 Visual Studio。 就像在步驟1中一樣，您可以逐步執行預存程式的語句，並查看和修改參數值。

[![[ExistingSprocs] 頁面一開始會顯示飲料](debugging-stored-procedures-cs/_static/image13.png)](debugging-stored-procedures-cs/_static/image12.png)

**圖 6**： [`ExistingSprocs.aspx`] 頁面一開始會顯示飲料（[按一下以觀看完整大小的影像](debugging-stored-procedures-cs/_static/image14.png)）

[已達到預存程式的中斷點 ![](debugging-stored-procedures-cs/_static/image16.png)](debugging-stored-procedures-cs/_static/image15.png)

**圖 7**：已達到預存程式的中斷點（[按一下以查看完整大小的影像](debugging-stored-procedures-cs/_static/image17.png)）

如 [圖 7] 中的監看式視窗所示，`@CategoryID` 參數的值為1。 這是因為 [`ExistingSprocs.aspx`] 頁面一開始會顯示飲料類別目錄中的產品，其 `CategoryID` 值為1。 從下拉式清單中選擇不同的類別。 這麼做會導致回傳，並重新執行 `Products_SelectByCategoryID` 預存程式。 會再次叫用中斷點，但這次 `@CategoryID` 參數 s 值會反映選取的下拉式清單專案 `CategoryID`。

[![從下拉式清單中選擇不同的類別](debugging-stored-procedures-cs/_static/image19.png)](debugging-stored-procedures-cs/_static/image18.png)

**圖 8**：從下拉式清單中選擇不同的類別（[按一下以查看完整大小的影像](debugging-stored-procedures-cs/_static/image20.png)）

[![@CategoryID 參數反映從網頁選取的類別目錄](debugging-stored-procedures-cs/_static/image22.png)](debugging-stored-procedures-cs/_static/image21.png)

**圖 9**： `@CategoryID` 參數反映從網頁選取的類別（[按一下以觀看完整大小的影像](debugging-stored-procedures-cs/_static/image23.png)）

> [!NOTE]
> 造訪 [`ExistingSprocs.aspx`] 頁面時，如果未叫用 `Products_SelectByCategoryID` 預存程式中的中斷點，請確定已在 [ASP.NET] 應用程式的 [屬性] 頁面的 [偵錯工具] 區段中核取 [SQL Server] 核取方塊、已停用該連接共用，而且已啟用 [資料庫 s 應用程式偵錯工具] 選項。 如果您仍然遇到問題，請重新開機 Visual Studio，然後再試一次。

## <a name="debugging-t-sql-database-objects-on-remote-instances"></a>在遠端實例上對 T SQL Database 物件進行調試

當 SQL Server 資料庫實例與 Visual Studio 在同一部電腦上時，透過 Visual Studio 的調試資料庫物件相當簡單。 不過，如果 SQL Server 和 Visual Studio 位於不同的電腦上，則需要謹慎設定，才能讓所有專案都能正常運作。 我們面臨兩個核心工作：

- 確定用來透過 ADO.NET 連接到資料庫的登入屬於 `sysadmin` 角色。
- 請確定開發電腦上 Visual Studio 所使用的 Windows 使用者帳戶是屬於 `sysadmin` 角色的有效 SQL Server 登入帳戶。

第一個步驟相當簡單。 首先，識別用來從 ASP.NET 應用程式連接到資料庫的使用者帳戶，然後從 SQL Server Management Studio 將該登入帳戶加入 `sysadmin` 角色。

第二個工作需要您用來對應用程式進行 debug 錯的 Windows 使用者帳戶，是遠端資料庫上的有效登入。 不過，您用來登入工作站的 Windows 帳戶很可能不是 SQL Server 的有效登入。 較好的選擇是將某些 Windows 使用者帳戶指定為 SQL Server 的偵錯工具，而不是將您的特定登入帳戶新增至 SQL Server。 然後，若要對遠端 SQL Server 實例的資料庫物件進行偵錯工具，您可以使用該 Windows 登入帳戶的認證來執行 Visual Studio。

範例應該有助於闡明事項。 假設 Windows 網域中有一個名為 `SQLDebug` 的 Windows 帳戶。 此帳戶必須加入至遠端 SQL Server 實例，做為有效的登入，以及 `sysadmin` 角色的成員。 然後，若要從 Visual Studio 中將遠端 SQL Server 實例進行調試，我們必須以 `SQLDebug` 使用者的身分執行 Visual Studio。 這可以藉由登出我們的工作站來完成，以 `SQLDebug`重新登入，然後啟動 Visual Studio，但更簡單的方法是使用自己的認證登入我們的工作站，然後使用 `runas.exe` 以 `SQLDebug` 使用者的身分啟動 Visual Studio。 `runas.exe` 允許在不同使用者帳戶的假借下執行特定的應用程式。 若要啟動 Visual Studio 做為 `SQLDebug`，您可以在命令列中輸入下列語句：

[!code-console[Main](debugging-stored-procedures-cs/samples/sample2.cmd)]

如需有關此程式的詳細說明，請參閱[William Vaughn](http://betav.com/BLOG/billva/) s*漫遊 s Visual Studio 和 SQL Server，第七版，* 以及[如何：設定偵錯工具的 SQL Server 許可權](https://msdn.microsoft.com/library/w1bhybwz(VS.80).aspx)。

> [!NOTE]
> 如果您的開發機器執行的是 Windows XP Service Pack 2，您必須設定網際網路連線防火牆以允許遠端偵錯程式。 [如何：啟用 SQL Server 2005 的調試](https://msdn.microsoft.com/library/s0fk6z6e(VS.80).aspx)程式一文，請注意，這牽涉到 Visual Studio 主機電腦上的兩個步驟：（a），您必須將 `Devenv.exe` 新增至例外清單並開啟 TCP 135 埠;和（b）在遠端（SQL）電腦上，您必須開啟 TCP 135 埠，並將 `sqlservr.exe` 新增至例外清單。 如果您的網域原則需要透過 IPSec 完成網路通訊，您必須開啟 UDP 4500 和 UDP 500 埠。

## <a name="summary"></a>總結

除了提供 .NET 應用程式程式碼的偵錯工具支援之外，Visual Studio 也提供 SQL Server 2005 的各種偵錯工具選項。 在本教學課程中，我們探討了兩個選項：直接資料庫的偵錯工具和應用程式的偵錯工具。 若要直接檢查 T-sql 資料庫物件，請透過伺服器總管找出物件，然後以滑鼠右鍵按一下它，然後選擇 [逐步執行]。 這會啟動偵錯工具，並在資料庫物件中的第一個語句上暫停，此時您可以逐步執行物件的語句，並查看和修改參數值。 在步驟1中，我們使用此方法來逐步執行 `Products_SelectByCategoryID` 預存程式。

應用程式的偵錯工具可讓您直接在資料庫物件內設定中斷點。 從用戶端應用程式（例如 ASP.NET web 應用程式）叫用含有中斷點的資料庫物件時，程式會在偵錯工具接管時停止。 應用程式的調試很有用，因為它更清楚地顯示哪些應用程式動作會造成特定資料庫物件被叫用。 不過，它比直接資料庫的偵錯工具需要更多的設定和安裝。

您也可以透過 SQL Server 專案來調試資料庫物件。 在下一個教學課程中，我們將探討如何使用 SQL Server 專案，以及如何使用它們來建立和偵測受管理的資料庫物件。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一頁](protecting-connection-strings-and-other-configuration-information-cs.md)
> [下一頁](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs.md)
