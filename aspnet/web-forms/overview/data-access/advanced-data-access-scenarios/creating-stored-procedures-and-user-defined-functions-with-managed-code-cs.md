---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-cs
title: 使用受控碼建立預存程式和使用者定義函數（C#） |Microsoft Docs
author: rick-anderson
description: Microsoft SQL Server 2005 與 .NET Common Language Runtime 整合，可讓開發人員透過 managed 程式碼建立資料庫物件。 本教學課程 。
ms.author: riande
ms.date: 08/03/2007
ms.assetid: 213eea41-1ab4-4371-8b24-1a1a66c515de
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-cs
msc.type: authoredcontent
ms.openlocfilehash: c6aec9ca70fe3ab568b3d17fea6bfd56671edc03
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78533534"
---
# <a name="creating-stored-procedures-and-user-defined-functions-with-managed-code-c"></a>使用受控碼建立預存程序和使用者定義函式 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_75_CS.zip)或[下載 PDF](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/datatutorial75cs1.pdf)

> Microsoft SQL Server 2005 與 .NET Common Language Runtime 整合，可讓開發人員透過 managed 程式碼建立資料庫物件。 本教學課程示範如何使用您的 Visual Basic 或C#程式碼，建立 managed 預存程式和受管理的使用者定義函數。 我們也會看到這些版本的 Visual Studio 如何讓您進行這類的 managed 資料庫物件的調試。

## <a name="introduction"></a>簡介

Microsoft SQL Server 2005 這類資料庫使用[結構化查詢語言 (SQL) transact-sql](http://en.wikipedia.org/wiki/Transact-SQL)來插入、修改和抓取資料。 大部分的資料庫系統都包含組成一系列 SQL 語句的結構，這些語句可以做為單一、可重複使用的單位來執行。 預存程式是其中一個範例。 另一個是*使用者定義函數*（udf），這是我們將在步驟9中更詳細地檢查的結構。

就核心而言，SQL 是針對使用資料集而設計的。 `SELECT`、`UPDATE`和 `DELETE` 語句原本就適用于對應資料表中的所有記錄，而且只受其 `WHERE` 子句的限制。 但有許多語言功能是設計用來一次處理一筆記錄，以及用來操作純量資料。 [`CURSOR` s](http://www.sqlteam.com/item.asp?ItemID=553)允許一組記錄一次迴圈一筆。 `LEFT`、`CHARINDEX`和 `PATINDEX` 等字串操作函式可處理純量資料。 SQL 也包含控制流程語句，例如 `IF` 和 `WHILE`。

在 Microsoft SQL Server 2005 之前，預存程式和 Udf 只能定義為 T-sql 語句的集合。 不過，SQL Server 2005 是設計用來提供與[Common Language Runtime （CLR）](https://msdn.microsoft.com/netframework/aa497266.aspx)的整合，這是所有 .net 元件所使用的執行時間。 因此，可以使用 managed 程式碼來建立 SQL Server 2005 資料庫中的預存程式和 Udf。 也就是說，您可以建立預存程式或 UDF，做為C#類別中的方法。 這可讓這些預存程式和 Udf 利用 .NET Framework 中的功能，以及自訂的類別。

在本教學課程中，我們將探討如何建立 managed 預存程式和使用者定義函數，以及如何將它們整合到 Northwind 資料庫中。 讓我們開始吧！

> [!NOTE]
> 受管理的資料庫物件在 SQL 對應專案方面提供了一些優點。 語言豐富、熟悉，以及重複使用現有程式碼和邏輯的能力，都是主要的優點。 但是，當使用的資料集不牽涉到許多程式邏輯時，managed 資料庫物件的效率可能較低。 如需使用 managed 程式碼與 T-sql 之優點的詳細討論，請參閱[使用 managed 程式碼建立資料庫物件的優點](https://msdn.microsoft.com/library/k2e1fb36(VS.80).aspx)。

## <a name="step-1-moving-the-northwind-database-out-ofapp_data"></a>步驟1：將 Northwind 資料庫移出`App_Data`

到目前為止，我們所有的教學課程都已使用 web 應用程式 `App_Data` 資料夾中的 Microsoft SQL Server 2005 Express Edition 資料庫檔案。 將資料庫放在 `App_Data` 簡化散發和執行這些教學課程，因為所有檔案都位於一個目錄中，而且不需要額外的設定步驟來測試教學課程。

不過，在本教學課程中，我們會將 Northwind 資料庫移出 `App_Data`，並明確地向 SQL Server 2005 Express Edition 資料庫實例註冊它。 雖然我們可以使用 `App_Data` 資料夾中的資料庫來執行本教學課程的步驟，但透過 SQL Server 2005 Express Edition 資料庫實例明確註冊資料庫，有幾個步驟會變得更簡單。

本教學課程的下載包含兩個資料庫檔案-`NORTHWND.MDF`，並 `NORTHWND_log.LDF` 放在名為 `DataFiles`的資料夾中。 如果您遵循自己的教學課程執行，請關閉 Visual Studio，並將 `NORTHWND.MDF` 和 `NORTHWND_log.LDF` 網站 `App_Data` 資料夾中的檔案移至網站以外的資料夾。 資料庫檔案一旦移至另一個資料夾，就必須向 SQL Server 2005 Express Edition 資料庫實例註冊 Northwind 資料庫。 這可以從 SQL Server Management Studio 完成。 如果您的電腦上已安裝非 Express Edition 的 SQL Server 2005，表示您可能已經安裝 Management Studio。 如果您的電腦上只有 SQL Server 2005 Express Edition，請花一點時間下載並安裝[Microsoft SQL Server Management Studio Express](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796)。

啟動 SQL Server Management Studio。 如 [圖 1] 所示，Management Studio 一開始會詢問要連接的伺服器。 在 [伺服器名稱] 中輸入 localhost\SQLExpress，選擇 [驗證] 下拉式清單中的 [Windows 驗證]，然後按一下 [連接]。

![連接到適當的資料庫實例](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image1.png)

**圖 1**：連接到適當的資料庫實例

連接之後，[物件總管] 視窗會列出 SQL Server 2005 Express Edition 資料庫實例的相關資訊，包括資料庫、安全性資訊、管理選項等等。

我們需要將 Northwind 資料庫附加到 `DataFiles` 資料夾中（或您可能已將它移到其中的任何位置）至 SQL Server 2005 Express Edition 資料庫實例。 以滑鼠右鍵按一下 [資料庫] 資料夾，然後從內容功能表選擇 [附加] 選項。 這會顯示 [附加資料庫] 對話方塊。 按一下 [新增] 按鈕，向下切入至適當的 `NORTHWND.MDF` 檔案，然後按一下 [確定]。 此時，您的畫面看起來應該像 [圖 2]。

[![連接到適當的資料庫實例](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image3.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image2.png)

**圖 2**：連接到適當的資料庫實例（[按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image4.png)）

> [!NOTE]
> 透過連接到 SQL Server 2005 Express Edition 實例時 Management Studio [附加資料庫] 對話方塊不允許您向下切入到使用者設定檔目錄，例如 [我的文件]。 因此，請務必將 `NORTHWND.MDF` 和 `NORTHWND_log.LDF` 檔案放在非使用者設定檔目錄中。

按一下 [確定] 按鈕以附加資料庫。 [附加資料庫] 對話方塊將會關閉，而物件總管現在應該會列出剛附加的資料庫。 Northwind 資料庫的名稱可能如 `9FE54661B32FDD967F51D71D0D5145CC_LINE ARTICLES\DATATUTORIALS\VOLUME 3\CSHARP\73\ASPNET_DATA_TUTORIAL_75_CS\APP_DATA\NORTHWND.MDF`。 以滑鼠右鍵按一下資料庫，然後選擇 [重新命名]，將資料庫重新命名為 Northwind。

![將資料庫重新命名為 Northwind](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image5.png)

**圖 3**：將資料庫重新命名為 Northwind

## <a name="step-2-creating-a-new-solution-and-sql-server-project-in-visual-studio"></a>步驟2：在 Visual Studio 中建立新的方案和 SQL Server 專案

若要在 SQL Server 2005 中建立 managed 預存程式或 Udf，我們將在類別中撰寫C#預存程式和 udf 邏輯當做程式碼。 撰寫程式碼之後，我們必須將此類別編譯成元件（`.dll` 檔案）、向 SQL Server 資料庫註冊元件，然後在資料庫中建立指向元件中對應方法的預存程式或 UDF 物件。 這些步驟都可以手動執行。 我們可以在任何文字編輯器中建立程式碼、使用C#編譯器（[`csc.exe`](https://msdn.microsoft.com/library/ms379563(vs.80).aspx)）從命令列進行編譯、使用[`CREATE ASSEMBLY`](https://msdn.microsoft.com/library/ms189524.aspx)命令或從 Management Studio 向資料庫註冊，以及透過類似的方式新增預存程式或 UDF 物件。 幸運的是，Professional 和 Team 系統的 Visual Studio 版本包括可自動執行這些工作的 SQL Server 專案類型。 在本教學課程中，我們將逐步解說如何使用 SQL Server 專案類型來建立 managed 預存程式和 UDF。

> [!NOTE]
> 如果您使用的是 Visual Web Developer 或 Standard edition 的 Visual Studio，就必須改為使用手動方法。 步驟13提供手動執行這些步驟的詳細指示。 在閱讀步驟13之前，我建議您先閱讀步驟2到12，因為這些步驟包含重要的 SQL Server 設定指示，不論您使用的是哪一個版本的 Visual Studio 都必須套用。

從開啟 Visual Studio 開始。 從 [檔案] 功能表中，選擇 [新增專案] 以顯示 [新增專案] 對話方塊（請參閱 [圖 4]）。 向下切入到資料庫專案類型，然後從右邊列出的範本中，選擇建立新的 SQL Server 專案。 我選擇將此專案命名為 `ManagedDatabaseConstructs` 並放在名為 `Tutorial75`的方案中。

[![建立新的 SQL Server 專案](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image7.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image6.png)

**圖 4**：建立新的 SQL Server 專案（[按一下以觀看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image8.png)）

按一下 [新增專案] 對話方塊中的 [確定] 按鈕，以建立方案並 SQL Server 專案。

SQL Server 專案會系結至特定的資料庫。 因此，在建立新的 SQL Server 專案之後，系統會立即要求您指定此資訊。 [圖 5] 顯示 [新增資料庫參考] 對話方塊，其中已填入以指向我們在步驟1中向 SQL Server 2005 Express Edition 資料庫實例註冊的 Northwind 資料庫。

![建立 SQL Server 專案與 Northwind 資料庫的關聯](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image9.png)

**圖 5**：將 SQL Server 專案與 Northwind 資料庫產生關聯

為了要在此專案中建立 managed 預存程式和 Udf，我們必須啟用連接的 SQL/CLR 偵錯工具支援。 每當 SQL Server 專案與新的資料庫產生關聯時（如 [圖 5] 所示），Visual Studio 會詢問我們是否要在連接上啟用 SQL/CLR 調試（請參閱 [圖 6]）。 按一下 [是]。

![啟用 SQL/CLR 調試](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image10.png)

**圖 6**：啟用 SQL/CLR 調試

此時，新的 SQL Server 專案已加入至方案中。 它包含名為 `Test Scripts` 的資料夾，其中含有名為 `Test.sql`的檔案，可用來對在專案中建立的 managed 資料庫物件進行偵錯工具。 我們將在步驟12中探討調試。

我們現在可以在這個專案中加入新的 managed 預存程式和 Udf，但是在我們開始之前，我們先在解決方案中加入現有的 web 應用程式。 從 [檔案] 功能表選取 [新增] 選項，然後選擇 [現有的網站]。 流覽至適當的網站資料夾，然後按一下 [確定]。 如 [圖 7] 所示，這會更新方案以包含兩個專案：網站和 `ManagedDatabaseConstructs` SQL Server 專案。

![方案總管現在包含兩個專案](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image11.png)

**圖 7**：方案總管現在包含兩個專案

`Web.config` 中的 `NORTHWNDConnectionString` 值目前參考 `App_Data` 資料夾中的 `NORTHWND.MDF` 檔案。 因為我們已從 `App_Data` 中移除此資料庫，並在 SQL Server 2005 Express Edition 資料庫實例中明確註冊它，所以我們需要相應更新 `NORTHWNDConnectionString` 值。 開啟網站中的 `Web.config` 檔案，然後變更 `NORTHWNDConnectionString` 值，讓連接字串讀取： `Data Source=localhost\SQLExpress;Initial Catalog=Northwind;Integrated Security=True`。 在這項變更之後，`Web.config` 中的 `<connectionStrings>` 區段看起來應該如下所示：

[!code-xml[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample1.xml)]

> [!NOTE]
> 如[先前的教學](debugging-stored-procedures-cs.md)課程中所述，從用戶端應用程式（例如 ASP.NET 網站）進行 SQL Server 物件的調試時，我們需要停用連接共用。 如上所示的連接字串會停用連接共用（`Pooling=false`）。 如果您不打算從 ASP.NET 網站對 managed 預存程式和 Udf 進行程式設計，請啟用連接共用。

## <a name="step-3-creating-a-managed-stored-procedure"></a>步驟3：建立 Managed 預存程式

若要將 managed 預存程式加入至 Northwind 資料庫，我們必須先在 SQL Server 專案中建立預存程式做為方法。 在 方案總管中，以滑鼠右鍵按一下 `ManagedDatabaseConstructs` 專案名稱，然後加入宣告新專案。 這會顯示 [加入新專案] 對話方塊，其中會列出可加入至專案的 managed 資料庫物件類型。 如 [圖 8] 所示，這包括預存程式和使用者定義函式，還有其他函數。

首先，我們要加入一個預存程式，只傳回所有已中止的產品。 將新的預存程式檔案命名為 `GetDiscontinuedProducts.cs`。

[![新增名為 GetDiscontinuedProducts.cs 的預存程式](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image13.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image12.png)

**圖 8**：加入名為 `GetDiscontinuedProducts.cs` 的新預存程式（[按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image14.png)）

這會建立新C#的類別檔案，其中包含下列內容：

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample2.cs)]

請注意，預存程式會實作為 `partial` 類別檔案中名為 `StoredProcedures`的 `static` 方法。 此外，`GetDiscontinuedProducts` 方法是以 `SqlProcedure attribute`裝飾，這會將方法標記為預存程式。

下列程式碼會建立 `SqlCommand` 物件，並將其 `CommandText` 設定為 `SELECT` 查詢，以傳回 `Discontinued` 欄位等於1之產品的 `Products` 資料表中的所有資料行。 然後，它會執行命令，並將結果傳回用戶端應用程式。 將此程式碼新增至 `GetDiscontinuedProducts` 方法。

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample3.cs)]

所有的 managed 資料庫物件都可以存取代表呼叫端內容的[`SqlContext` 物件](https://msdn.microsoft.com/library/ms131108.aspx)。 `SqlContext` 透過其[`Pipe` 屬性](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlcontext.pipe.aspx)來提供[`SqlPipe` 物件](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.aspx)的存取權。 這個 `SqlPipe` 物件是用來 ferry SQL Server 資料庫與呼叫應用程式之間的資訊。 正如其名， [`ExecuteAndSend` 方法](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.executeandsend.aspx)會執行傳入的 `SqlCommand` 物件，並將結果傳回用戶端應用程式。

> [!NOTE]
> 受控資料庫物件最適用于使用程式邏輯的預存程式和 Udf，而不是以集合為基礎的邏輯。 程式邏輯牽涉到以逐列方式使用資料集，或處理純量資料。 不過，我們剛才建立的 `GetDiscontinuedProducts` 方法不包含程式邏輯。 因此，最理想的做法是將它實作為 T-sql 預存程式。 它會實作為 managed 預存程式，以示範建立和部署 managed 預存程式所需的步驟。

## <a name="step-4-deploying-the-managed-stored-procedure"></a>步驟4：部署 Managed 預存程式

完成此程式碼後，我們即可將它部署至 Northwind 資料庫。 部署 SQL Server 專案會將程式碼編譯成元件、向資料庫註冊元件，並在資料庫中建立對應的物件，並將它們連結至元件中的適當方法。 [部署] 選項所執行的一組確切工作，在步驟13中更精確。 以滑鼠右鍵按一下 方案總管中的 `ManagedDatabaseConstructs` 專案名稱，然後選擇 部署 選項。 不過，部署因下列錯誤而失敗： ' EXTERNAL ' 附近的語法不正確。 您可能要將目前資料庫的相容性層級設成高一點的值，以啟用這項功能。 請參閱預存程式 `sp_dbcmptlevel`的說明。

嘗試在 Northwind 資料庫中註冊元件時，會出現這個錯誤訊息。 為了向 SQL Server 2005 資料庫註冊元件，資料庫的相容性層級必須設定為90。 根據預設，新的 SQL Server 2005 資料庫的相容性層級為90。 不過，使用 Microsoft SQL Server 2000 建立的資料庫具有預設的相容性層級80。 由於 Northwind 資料庫最初是 Microsoft SQL Server 2000 資料庫，因此其相容性層級目前設定為80，因此必須增加至90，才能註冊 managed 資料庫物件。

若要更新資料庫的相容性層級，請在 Management Studio 中開啟新的查詢視窗，然後輸入：

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample4.sql)]

按一下工具列中的 [執行] 圖示，以執行上述查詢。

[![更新 Northwind 資料庫的相容性層級](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image16.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image15.png)

**圖 9**：更新 Northwind 資料庫的相容性層級（[按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image17.png)）

更新相容性層級之後，請重新部署 SQL Server 專案。 此時，部署應該會完成，而不會發生錯誤。

返回 SQL Server Management Studio，以滑鼠右鍵按一下物件總管中的 Northwind 資料庫，然後選擇 [重新整理]。 接下來，向下切入至 [可程式性] 資料夾，然後展開 [元件] 資料夾。 如 [圖 10] 所示，Northwind 資料庫現在包含了 `ManagedDatabaseConstructs` 專案所產生的元件。

![ManagedDatabaseConstructs 元件現在已向 Northwind 資料庫註冊](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image18.png)

**圖 10**： `ManagedDatabaseConstructs` 元件現在已向 Northwind 資料庫註冊

同時展開 [預存程式] 資料夾。 您會看到名為 `GetDiscontinuedProducts`的預存程式。 這個預存程式是由部署進程所建立，並指向 `ManagedDatabaseConstructs` 元件中的 `GetDiscontinuedProducts` 方法。 執行 `GetDiscontinuedProducts` 預存程式時，它會接著執行 `GetDiscontinuedProducts` 方法。 由於這是 managed 預存程式，因此無法透過 Management Studio 編輯（因此，預存程式名稱旁邊的鎖定圖示）。

![GetDiscontinuedProducts 預存程式會列在 [預存程式] 資料夾中](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image19.png)

**圖 11**： `GetDiscontinuedProducts` 預存程式會列在 [預存程式] 資料夾中

在呼叫 managed 預存程式之前，我們必須先克服一項障礙：資料庫已設定為防止執行 managed 程式碼。 請開啟新的查詢視窗，並執行 `GetDiscontinuedProducts` 預存程式，以確認這項操作。 您會收到下列錯誤訊息：已停用 .NET Framework 中的使用者程式碼執行。 [啟用 clr 已啟用] 設定選項。

若要檢查 Northwind 資料庫的設定資訊，請在查詢視窗中輸入並執行命令 `exec sp_configure`。 這會顯示 [clr 已啟用] 設定目前設定為0。

[![[clr 已啟用] 設定目前設定為0](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image21.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image20.png)

**圖 12**： [clr 已啟用] 設定目前設定為0（[按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image22.png)）

請注意，[圖 12] 中的每個設定都有四個與它一起列出的值：最小值和最大值，以及 config 和 run 值。 若要更新已啟用 clr 設定的 config 值，請執行下列命令：

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample5.sql)]

如果您重新執行 `exec sp_configure` 您會看到上述語句將 clr enabled 設定值更新為1，但執行值仍設為0。 為了讓此設定變更生效，我們需要執行[`RECONFIGURE` 命令](https://msdn.microsoft.com/library/ms176069.aspx)，這會將執行值設為目前的設定值。 直接在查詢視窗中輸入 `RECONFIGURE`，然後按一下工具列中的 [執行] 圖示。 如果您執行 `exec sp_configure` 現在您應該會看到 [已啟用 clr] 設定的值為1，並執行 [值]。

在啟用 clr 的設定完成後，我們就可以開始執行 managed `GetDiscontinuedProducts` 預存程式。 在查詢視窗中，輸入並執行命令 `exec` `GetDiscontinuedProducts`。 叫用預存程式會導致 `GetDiscontinuedProducts` 方法中的對應 managed 程式碼執行。 此程式碼會發出 `SELECT` 查詢，以傳回已停止的所有產品，並將此資料傳回給呼叫應用程式，這在此實例中 SQL Server Management Studio。 Management Studio 接收這些結果，並將它們顯示在 [結果] 視窗中。

[![GetDiscontinuedProducts 預存程式傳回所有已停止的產品](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image24.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image23.png)

**圖 13**： `GetDiscontinuedProducts` 預存程式會傳回所有已停止[的產品（按一下以觀看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image25.png)）

## <a name="step-5-creating-managed-stored-procedures-that-accept-input-parameters"></a>步驟5：建立接受輸入參數的 Managed 預存程式

我們在這些教學課程中建立的許多查詢和預存程式都已使用*參數*。 例如，在為具[類型資料集的 Tableadapter 建立新的預存程式](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)教學課程中，我們建立了名為 `GetProductsByCategoryID` 的預存程式，接受名為 `@CategoryID`的輸入參數。 然後，預存程式會傳回其 `CategoryID` 欄位符合所提供 `@CategoryID` 參數值的所有產品。

若要建立可接受輸入參數的 managed 預存程式，只要在方法 s 定義中指定這些參數即可。 為了說明這一點，讓我們將另一個 managed 預存程式新增至名為 `GetProductsWithPriceLessThan`的 `ManagedDatabaseConstructs` 專案。 此 managed 預存程式將會接受指定價格的輸入參數，並傳回其 `UnitPrice` 欄位小於參數 s 值的所有產品。

若要將新的預存程式加入至專案，請以滑鼠右鍵按一下 `ManagedDatabaseConstructs` 專案名稱，然後加入宣告新的預存程式。 開啟 `GetProductsWithPriceLessThan.cs` 檔案。 如我們在步驟3中所見，這會建立C#新的類別檔案，其中包含名為的方法 `GetProductsWithPriceLessThan` 放在 `partial` 類別 `StoredProcedures`內。

更新 `GetProductsWithPriceLessThan` 方法的定義，使其接受名為 `price` 的[`SqlMoney`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.aspx)輸入參數，並撰寫程式碼以執行並傳回查詢結果：

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample6.cs)]

`GetProductsWithPriceLessThan` 方法的定義和程式碼，與步驟3中所建立之 `GetDiscontinuedProducts` 方法的定義和程式碼十分相似。 唯一的差異在於 `GetProductsWithPriceLessThan` 方法會接受做為輸入參數（`price`），`SqlCommand` s 查詢包含參數（`@MaxPrice`），而將參數新增至 `SqlCommand` s `Parameters` 集合，並指派 `price` 變數的值。

加入此程式碼之後，請重新部署 SQL Server 專案。 接下來，返回 SQL Server Management Studio 並重新整理 [預存程式] 資料夾。 您應該會看到新的專案，`GetProductsWithPriceLessThan`。 從查詢視窗中，輸入並執行命令 `exec GetProductsWithPriceLessThan 25`，這會列出小於 $25 的所有產品，如 [圖 14] 所示。

[顯示 $25 底下的 ![產品](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image27.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image26.png)

**圖 14**：顯示 $25 底下的產品（[按一下以觀看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image28.png)）

## <a name="step-6-calling-the-managed-stored-procedure-from-the-data-access-layer"></a>步驟6：從資料存取層呼叫 Managed 預存程式

此時，我們已將 `GetDiscontinuedProducts` 和 `GetProductsWithPriceLessThan` managed 預存程式新增至 `ManagedDatabaseConstructs` 專案，並使用 Northwind SQL Server 資料庫來註冊它們。 我們也從 SQL Server Management Studio 叫用這些 managed 預存程式（請參閱 [圖 s 13] 和 [14]）。 不過，為了讓 ASP.NET 應用程式使用這些 managed 預存程式，我們需要將它們新增至架構中的資料存取和商務邏輯層。 在此步驟中，我們會將兩個新方法加入 `NorthwindWithSprocs` 型別資料集的 `ProductsTableAdapter` 中，一開始是在針對具型別[資料集 tableadapter 教學課程建立新的預存程式](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)中建立的。 在步驟7中，我們會將對應的方法新增到 BLL。

在 Visual Studio 中開啟 `NorthwindWithSprocs` 類型資料集，並從將新方法新增至名為 `GetDiscontinuedProducts`的 `ProductsTableAdapter` 開始。 若要將新的方法加入至 TableAdapter，請以滑鼠右鍵按一下設計工具中的 TableAdapter 名稱，然後從內容功能表中選擇 [加入查詢] 選項。

> [!NOTE]
> 因為我們已將 Northwind 資料庫從 `App_Data` 資料夾移至 SQL Server 2005 Express Edition 資料庫實例，所以 Web.config 中對應的連接字串必須更新以反映這項變更。 在步驟2中，我們討論了更新 `Web.config`中的 `NORTHWNDConnectionString` 值。 如果您忘記進行此更新，您會看到錯誤訊息 [無法加入查詢]。 嘗試將新方法加入至 TableAdapter 時，在對話方塊中找不到物件 `Web.config` 的連接 `NORTHWNDConnectionString`。 若要解決此錯誤，請按一下 [確定]，然後移至 `Web.config` 並更新 `NORTHWNDConnectionString` 值，如步驟2中所述。 然後嘗試將方法重新加入至 TableAdapter。 這次它應該會正常執行，而不會發生錯誤。

新增方法會啟動 [TableAdapter 查詢設定向導]，我們在過去的教學課程中已使用過多次。 第一個步驟會要求我們指定 TableAdapter 應如何存取資料庫：透過臨機操作 SQL 語句，或經由新的或現有的預存程式。 因為我們已經使用資料庫建立並註冊 `GetDiscontinuedProducts` 的 managed 預存程式，所以請選擇 [使用現有的預存程式] 選項，然後按 [下一步]。

[![選擇 [使用現有的預存程式] 選項](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image30.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image29.png)

**圖 15**：選擇 [使用現有的預存程式] 選項（[按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image31.png)）

下一個畫面會提示我們輸入方法將叫用的預存程式。 從下拉式清單中選擇 [`GetDiscontinuedProducts` managed 預存程式]，然後按 [下一步]。

[![選取 GetDiscontinuedProducts Managed 預存程式](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image33.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image32.png)

**圖 16**：選取 `GetDiscontinuedProducts` Managed 預存程式（[按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image34.png)）

接著，我們會要求您指定預存程式是否會傳回資料列、單一值或不傳回任何資料。 由於 `GetDiscontinuedProducts` 會傳回已停止的產品資料列集，請選擇第一個選項（表格式資料），然後按 [下一步]。

[![選取表格式資料選項](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image36.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image35.png)

**圖 17**：選取表格式資料選項（[按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image37.png)）

最後的 wizard 畫面可讓我們指定所使用的資料存取模式，以及所產生之方法的名稱。 將兩個核取方塊保持為已核取，並將方法命名為 `FillByDiscontinued` 和 `GetDiscontinuedProducts`。 按一下 [完成] 完成精靈。

[![將方法命名為 FillByDiscontinued 和 GetDiscontinuedProducts](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image39.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image38.png)

**圖 18**：命名方法 `FillByDiscontinued` 和 `GetDiscontinuedProducts` （[按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image40.png)）

重複這些步驟，以建立名為 `FillByPriceLessThan` 的方法，並在 `GetProductsWithPriceLessThan` managed 預存程式的 `ProductsTableAdapter` 中 `GetProductsWithPriceLessThan`。

[圖 19] 顯示在將方法加入至 `GetDiscontinuedProducts` 和 `GetProductsWithPriceLessThan` managed 預存程式的 `ProductsTableAdapter` 之後，DataSet 設計工具的螢幕擷取畫面。

[![ProductsTableAdapter 包含在此步驟中新增的方法](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image42.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image41.png)

**圖 19**： `ProductsTableAdapter` 包含在此步驟中新增的方法（[按一下以觀看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image43.png)）

## <a name="step-7-adding-corresponding-methods-to-the-business-logic-layer"></a>步驟7：將對應的方法加入至商務邏輯層

既然我們已將資料存取層更新為包含呼叫步驟4和5中所新增之 managed 預存程式的方法，我們必須將對應的方法加入至商務邏輯層。 將下列兩個方法新增至 `ProductsBLLWithSprocs` 類別：

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample7.cs)]

這兩種方法只會呼叫對應的 DAL 方法，並傳回 `ProductsDataTable` 實例。 每個方法上方的 `DataObjectMethodAttribute` 標記會使這些方法包含在 [ObjectDataSource] [設定資料來源] 嚮導的 [選取] 索引標籤的下拉式清單中。

## <a name="step-8-invoking-the-managed-stored-procedures-from-the-presentation-layer"></a>步驟8：從展示層叫用 Managed 預存程式

藉由增強商務邏輯和資料存取層，以包含呼叫 `GetDiscontinuedProducts` 和 `GetProductsWithPriceLessThan` managed 預存程式的支援，我們現在可以透過 ASP.NET 網頁顯示這些預存程式結果。

開啟 [`AdvancedDAL`] 資料夾中的 [`ManagedFunctionsAndSprocs.aspx`] 頁面，然後從 [工具箱] 將 GridView 拖曳至設計工具。 將 GridView 的 `ID` 屬性設定為 `DiscontinuedProducts`，並將其從智慧標籤系結至名為 `DiscontinuedProductsDataSource`的新 ObjectDataSource。 設定 ObjectDataSource 以從 `ProductsBLLWithSprocs` 類別的 `GetDiscontinuedProducts` 方法提取其資料。

[![將 ObjectDataSource 設定為使用 ProductsBLLWithSprocs 類別](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image45.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image44.png)

**圖 20**：設定 ObjectDataSource 使用 `ProductsBLLWithSprocs` 類別（[按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image46.png)）

[![從 [選取] 索引標籤的下拉式清單中選擇 [GetDiscontinuedProducts] 方法](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image48.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image47.png)

**圖 21**：從 [選取] 索引標籤的下拉式清單中選擇 [`GetDiscontinuedProducts`] 方法（[按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image49.png)）

由於此方格只會用來顯示產品資訊，因此請將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]，然後按一下 [完成]。

完成嚮導後，Visual Studio 會自動為 `ProductsDataTable`中的每個資料欄位新增 BoundField 或 CheckBoxField。 請花一些時間移除除了 `ProductName` 和 `Discontinued`以外的所有欄位，此時您的 GridView 和 ObjectDataSource 宣告標記看起來應該像下面這樣：

[!code-aspx[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample8.aspx)]

請花點時間透過瀏覽器觀看此頁面。 流覽頁面時，ObjectDataSource 會呼叫 `ProductsBLLWithSprocs` 類別 s `GetDiscontinuedProducts` 方法。 如我們在步驟7中所見，這個方法會向下呼叫 DAL s `ProductsDataTable` 類別的 `GetDiscontinuedProducts` 方法，它會叫用 `GetDiscontinuedProducts` 的預存程式。 這個預存程式是 managed 預存程式，會執行我們在步驟3中建立的程式碼，傳回已停止的產品。

Managed 預存程式所傳回的結果會封裝到 DAL 的 `ProductsDataTable` 中，然後傳回給 BLL，然後將它們傳給其系結至 GridView 並顯示的展示層。 如預期般，方格會列出已停止的產品。

[列出已停止的產品 ![](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image51.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image50.png)

**圖 22**：已停止的產品會列出（[按一下以觀看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image52.png)）

如需進一步的作法，請在頁面中新增 TextBox 和另一個 GridView。 讓此 GridView 藉由呼叫 `ProductsBLLWithSprocs` 類別的 `GetProductsWithPriceLessThan` 方法，來顯示小於文字方塊中輸入的產品數量。

## <a name="step-9-creating-and-calling-t-sql-udfs"></a>步驟9：建立和呼叫 T-sql Udf

使用者定義函式（或 Udf）是資料庫物件，可在程式設計語言中密切模擬函式的語法。 如同中C#的函式，udf 可以包含可變數目的輸入參數，並傳回特定類型的值。 UDF 可以傳回純量資料（字串、整數，依此類推或表格式資料）。 讓我們快速查看這兩種類型的 Udf，從會傳回純量資料類型的 UDF 開始。

下列 UDF 會計算特定產品清查的預估值。 它會採用三個輸入參數，也就是特定產品的 `UnitPrice`、`UnitsInStock`和 `Discontinued` 值，並傳回 `money`類型的值。 它會藉由將 `UnitPrice` 乘以 `UnitsInStock`，來計算清查的預估值。 若為已停止的專案，此值為減半。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample9.sql)]

一旦將此 UDF 新增至資料庫之後，就可以藉由展開 [可程式性] 資料夾、[函數] 和 [純量值函式]，透過 Management Studio 來找到它。 它可以用在 `SELECT` 查詢中，如下所示：

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample10.sql)]

我已將 `udf_ComputeInventoryValue` UDF 新增至 Northwind 資料庫;[圖 23] 顯示透過 Management Studio 觀看時，上述 `SELECT` 查詢的輸出。 另請注意，UDF 會列在物件總管中的 [純量值函式] 資料夾底下。

[列出每個產品的清查值 ![](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image54.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image53.png)

**圖 23**：列出每個產品的清查值（[按一下以觀看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image55.png)）

Udf 也可以傳回表格式資料。 例如，我們可以建立一個 UDF，以傳回屬於特定類別的產品：

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample11.sql)]

`udf_GetProductsByCategoryID` UDF 會接受 `@CategoryID` 輸入參數，並傳回指定之 `SELECT` 查詢的結果。 建立之後，就可以在 `SELECT` 查詢的 `FROM` （或 `JOIN`）子句中參考此 UDF。 下列範例會傳回每個飲料的 `ProductID`、`ProductName`和 `CategoryID` 值。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample12.sql)]

我已將 `udf_GetProductsByCategoryID` UDF 新增至 Northwind 資料庫;[圖 24] 顯示透過 Management Studio 觀看時，上述 `SELECT` 查詢的輸出。 傳回表格式資料的 Udf 可以在物件總管 s 資料表值函式資料夾中找到。

[![會針對每個飲料列出 ProductID、ProductName 和類別名稱](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image57.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image56.png)

**圖 24**：每個飲料都會列出 `ProductID`、`ProductName`和 `CategoryID` （[按一下以觀看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image58.png)）

> [!NOTE]
> 如需建立和使用 Udf 的詳細資訊，請參閱[使用者定義函數簡介](http://www.sqlteam.com/item.asp?ItemID=1955)。 另請參閱[使用者定義函數的優點和缺點](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)。

## <a name="step-10-creating-a-managed-udf"></a>步驟10：建立受控 UDF

在上述範例中建立的 `udf_ComputeInventoryValue` 和 `udf_GetProductsByCategoryID` Udf 是 T-sql 資料庫物件。 SQL Server 2005 也支援受控 Udf，可以加入至 `ManagedDatabaseConstructs` 專案，就像步驟3和5中的 managed 預存程式一樣。 在此步驟中，讓 s 在受控碼中執行 `udf_ComputeInventoryValue` UDF。

若要將受控 UDF 新增至 `ManagedDatabaseConstructs` 專案，請在方案總管中的專案名稱上按一下滑鼠右鍵，然後加入宣告新的專案。 從 [加入新專案] 對話方塊中選取使用者定義的範本，並將新的 UDF 檔案命名為 `udf_ComputeInventoryValue_Managed.cs`。

[![將新的受控 UDF 新增至 ManagedDatabaseConstructs 專案](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image60.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image59.png)

**圖 25**：將新的受控 UDF 新增至 `ManagedDatabaseConstructs` 專案（[按一下以觀看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image61.png)）

使用者定義函式範本會建立一個名為 `UserDefinedFunctions` 的 `partial` 類別，其名稱與類別檔案的名稱（在此例中為`udf_ComputeInventoryValue_Managed`）相同。 這個方法是使用[`SqlFunction` 屬性](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlfunctionattribute.aspx)裝飾的，它會將方法標記為受控 UDF。

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample13.cs)]

`udf_ComputeInventoryValue` 方法目前會傳回[`SqlString` 物件](https://msdn.microsoft.com/library/system.data.sqltypes.sqlstring.aspx)，而且不接受任何輸入參數。 我們需要更新方法定義，使其接受三個輸入參數，`UnitPrice`、`UnitsInStock`和 `Discontinued`，並傳回 `SqlMoney` 物件。 用來計算清查值的邏輯與 T-sql `udf_ComputeInventoryValue` UDF 中的相同。

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample14.cs)]

請注意，UDF 方法的輸入參數是其對應的 SQL 類型： `SqlMoney` 用於 `UnitPrice` 欄位、 [`SqlInt16`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlint16.aspx)用於 `UnitsInStock`， [`SqlBoolean`用於 `Discontinued`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlboolean.aspx) 。 這些資料類型會反映 `Products` 資料表中所定義的類型： `UnitPrice` 資料行的類型是 `money`、類型 `smallint`的 `UnitsInStock` 資料行，以及 `Discontinued` 類型的 `bit`資料行。

程式碼一開始會建立一個名為 `inventoryValue` 的 `SqlMoney` 實例，指派0的值。 `Products` 資料表允許 `UnitsInPrice` 和 `UnitsInStock` 資料行中的資料庫 `NULL` 值。 因此，我們必須先檢查這些值是否包含 `NULL` s，我們會透過 `SqlMoney` 物件 s [`IsNull` 屬性](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.isnull.aspx)來執行此動作。 如果 `UnitPrice` 和 `UnitsInStock` 都包含非`NULL` 的值，則我們會將 `inventoryValue` 計算為兩者的乘積。 然後，如果 `Discontinued` 為 true，則會可以藉減半值。

> [!NOTE]
> `SqlMoney` 物件只允許將兩個 `SqlMoney` 實例相乘在一起。 它不允許 `SqlMoney` 實例乘以常值浮點數。 因此，若要可以藉減半 `inventoryValue` 我們會將它乘以具有值0.5 的新 `SqlMoney` 實例。

## <a name="step-11-deploying-the-managed-udf"></a>步驟11：部署受控 UDF

現在已建立受控 UDF，我們已準備好將它部署至 Northwind 資料庫。 如我們在步驟4中所見，在方案總管中的專案名稱上按一下滑鼠右鍵，然後從內容功能表中選擇 [部署] 選項，即可部署 SQL Server 專案中的 managed 物件。

部署專案之後，請返回 SQL Server Management Studio 並重新整理純量值函式資料夾。 您現在應該會看到兩個專案：

- `dbo.udf_ComputeInventoryValue`-在步驟9中建立的 T-sql UDF，以及
- `dbo.udf ComputeInventoryValue_Managed`-剛部署的步驟10中所建立的受控 UDF。

若要測試此受管理的 UDF，請從 Management Studio 中執行下列查詢：

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample15.sql)]

此命令會使用 managed `udf ComputeInventoryValue_Managed` UDF，而不是 T-sql `udf_ComputeInventoryValue` UDF，但輸出會相同。 請回到 [圖 23] 查看 UDF 輸出的螢幕擷取畫面。

## <a name="step-12-debugging-the-managed-database-objects"></a>步驟12：調試 Managed 資料庫物件

在[偵錯工具預存程式](debugging-stored-procedures-cs.md)教學課程中，我們討論了三個選項，可讓您透過 Visual Studio 進行 SQL Server 的偵錯工具：直接資料庫的偵測、應用程式的偵錯工具，以及從 SQL Server 專案 Managed 資料庫物件無法透過直接資料庫的偵錯工具來進行調試，但可以從用戶端應用程式以及直接從 SQL Server 專案進行調試。 不過，為了讓偵錯工具能夠正常執行，SQL Server 2005 資料庫必須允許 SQL/CLR 的偵錯工具。 回想一下，當我們第一次建立 `ManagedDatabaseConstructs` 專案時 Visual Studio 詢問我們是否要啟用 SQL/CLR 偵錯工具（請參閱步驟2中的 [圖 6]）。 以滑鼠右鍵按一下 [伺服器總管] 視窗中的資料庫，即可修改此設定。

![確定資料庫允許 SQL/CLR 的偵錯工具](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image62.png)

**圖 26**：確定資料庫允許 SQL/CLR 的偵錯工具

想像一下，我們想要進行 `GetProductsWithPriceLessThan` managed 預存程式的偵錯工具。 我們會先在 `GetProductsWithPriceLessThan` 方法的程式碼內設定中斷點。

[![在 GetProductsWithPriceLessThan 方法中設定中斷點](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image64.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image63.png)

**圖 27**：在 `GetProductsWithPriceLessThan` 方法中設定中斷點（[按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image65.png)）

讓我們先從 SQL Server 專案中，查看 managed 資料庫物件的調試。 由於我們的解決方案包含兩個專案，因此 `ManagedDatabaseConstructs` SQL Server 專案和我們的網站-為了從 SQL Server 專案進行 debug，我們必須指示在開始進行調試時，Visual Studio 啟動 `ManagedDatabaseConstructs` SQL Server 專案。 以滑鼠右鍵按一下方案總管中的 `ManagedDatabaseConstructs` 專案，然後從內容功能表選擇 [設定為啟始專案] 選項。

從偵錯工具啟動 `ManagedDatabaseConstructs` 專案時，它會執行 `Test.sql` 檔案中的 SQL 語句，該檔案位於 `Test Scripts` 資料夾中。 例如，若要測試 `GetProductsWithPriceLessThan` managed 預存程式，請將現有的 `Test.sql` 檔案內容取代為下列語句，這會叫用 `GetProductsWithPriceLessThan` managed 預存程式，並以14.95 的 `@CategoryID` 值進行傳遞：

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample16.sql)]

在您將上述腳本輸入 `Test.sql`之後，請前往 [偵錯工具] 功能表，然後選擇 [開始偵測]，或在工具列中按下 F5 或綠色播放圖示來開始進行偵錯工具。 這會在方案中建立專案、將 managed 資料庫物件部署到 Northwind 資料庫，然後執行 `Test.sql` 腳本。 此時會叫用中斷點，我們可以逐步執行 `GetProductsWithPriceLessThan` 方法，檢查輸入參數的值等等。

[已達到 GetProductsWithPriceLessThan 方法中的中斷點 ![](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image67.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image66.png)

**圖 28**：已達到 `GetProductsWithPriceLessThan` 方法中的中斷點（[按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image68.png)）

為了讓 SQL database 物件可以透過用戶端應用程式進行調試，必須將資料庫設定為支援應用程式的偵測。 以滑鼠右鍵按一下伺服器總管中的資料庫，並確定已核取 [應用程式偵錯工具] 選項。 此外，我們還需要設定 ASP.NET 應用程式，使其與 SQL 偵錯工具整合並停用連接共用。 這些步驟已在「[偵錯工具預存程式](debugging-stored-procedures-cs.md)」教學課程的步驟2中詳細討論。

在您設定 ASP.NET 應用程式和資料庫之後，請將 ASP.NET 網站設為啟始專案，並開始進行偵錯工具。 如果您造訪的頁面會呼叫其中一個具有中斷點的 managed 物件，應用程式將會停止，並將控制權轉換成偵錯工具，您可以在其中逐步執行程式碼，如圖28所示。

## <a name="step-13-manually-compiling-and-deploying-managed-database-objects"></a>步驟13：手動編譯和部署受管理的資料庫物件

SQL Server 專案可讓您輕鬆地建立、編譯和部署受管理的資料庫物件。 可惜的是，SQL Server 專案僅適用于 Visual Studio 的 Professional 和 Team 系統版本。 如果您使用的是 Visual Web Developer 或 Standard Edition 的 Visual Studio，而且想要使用受管理的資料庫物件，您必須手動建立及部署它們。 這牽涉到四個步驟：

1. 建立檔案，其中包含 managed 資料庫物件的原始程式碼。
2. 將物件編譯成元件，
3. 向 SQL Server 2005 資料庫註冊元件，並
4. 在 SQL Server 中建立資料庫物件，以指向元件中的適當方法。

為了說明這些工作，讓我們建立新的 managed 預存程式，以傳回 `UnitPrice` 大於指定值的產品。 在電腦上建立名為 `GetProductsWithPriceGreaterThan.cs` 的新檔案，並在檔案中輸入下列程式碼（您可以使用 Visual Studio、記事本或任何文字編輯器來完成這項操作）：

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample17.cs)]

這段程式碼與在步驟5中建立的 `GetProductsWithPriceLessThan` 方法完全相同。 唯一的差異在於方法名稱、`WHERE` 子句，以及查詢中所使用的參數名稱。 回到 `GetProductsWithPriceLessThan` 方法中，`WHERE` 子句會讀取： `WHERE UnitPrice < @MaxPrice`。 在這裡，我們會在 `GetProductsWithPriceGreaterThan`中使用： `WHERE UnitPrice > @MinPrice`。

我們現在需要將此類別編譯成元件。 從命令列中，流覽至您儲存 `GetProductsWithPriceGreaterThan.cs` 檔案的目錄，並使用C#編譯器（`csc.exe`）將類別檔案編譯成元件：

[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample18.cmd)]

如果包含 `csc.exe` 的資料夾不在系統 s `PATH`中，您就必須完整參考其路徑，`%WINDOWS%\Microsoft.NET\Framework\version\`，如下所示：

[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample19.cmd)]

[![將 GetProductsWithPriceGreaterThan.cs 編譯成元件](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image70.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image69.png)

**圖 29**：將 `GetProductsWithPriceGreaterThan.cs` 編譯成元件（[按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image71.png)）

`/t` 旗標會指定C#類別檔案應該編譯成 DLL （而不是可執行檔）。 `/out` 旗標會指定所產生元件的名稱。

> [!NOTE]
> 您也可以使用[ C# Visual Express edition](https://msdn.microsoft.com/vstudio/express/visualcsharp/) ，或在 Visual Studio Standard Edition 中建立個別的類別庫專案，而不是從命令列編譯 `GetProductsWithPriceGreaterThan.cs` 類別檔案。 S ren Jacob Lauritsen 已提供這類 Visual C# Express Edition 專案，其中包含 `GetProductsWithPriceGreaterThan` 預存程式的程式碼，以及在步驟3、5和10中建立的兩個 managed 預存程式和 UDF。 S ren 專案也包含加入對應資料庫物件所需的 T-sql 命令。

當程式碼編譯成元件時，我們就可以在 SQL Server 2005 資料庫內註冊元件。 這可以透過 T-sql、使用命令 `CREATE ASSEMBLY`，或透過 SQL Server Management Studio 來執行。 讓我們專注于使用 Management Studio。

在 [Management Studio] 中，展開 Northwind 資料庫的 [可程式性] 資料夾。 其中一個子資料夾是元件。 若要手動將新的元件加入至資料庫，請以滑鼠右鍵按一下 [元件] 資料夾，然後從內容功能表中選擇 [新增元件]。 這會顯示 [新增元件] 對話方塊（請參閱 [圖 30]）。 按一下 [流覽] 按鈕，選取剛才編譯的 `ManuallyCreatedDBObjects.dll` 元件，然後按一下 [確定] 將元件加入至資料庫。 您不應該在物件總管中看到 `ManuallyCreatedDBObjects.dll` 元件。

[![將 ManuallyCreatedDBObjects 元件新增至資料庫](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image73.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image72.png)

**圖 30**：將 `ManuallyCreatedDBObjects.dll` 元件新增至資料庫（[按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image74.png)）

![ManuallyCreatedDBObjects 會列在物件總管](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image75.png)

**圖 31**： `ManuallyCreatedDBObjects.dll` 列在物件總管

雖然我們已將元件加入 Northwind 資料庫，但我們尚未將預存程式與元件中的 `GetProductsWithPriceGreaterThan` 方法建立關聯。 若要完成這項操作，請開啟新的查詢視窗，並執行下列腳本：

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample20.sql)]

這會在 Northwind 資料庫中建立名為 `GetProductsWithPriceGreaterThan` 的新預存程式，並將它與 managed `GetProductsWithPriceGreaterThan` 方法（位於元件 `ManuallyCreatedDBObjects`中的類別 `StoredProcedures`）產生關聯。

執行上述腳本之後，請重新整理物件總管中的 [預存程式] 資料夾。 您應該會看到新的預存程式專案-`GetProductsWithPriceGreaterThan`-它旁邊有一個鎖定圖示。 若要測試此預存程式，請在查詢視窗中輸入並執行下列腳本：

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample21.sql)]

如圖32所示，上述命令會顯示 `UnitPrice` 大於 $24.95 之產品的資訊。

[![ManuallyCreatedDBObjects 列于物件總管](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image77.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image76.png)

**圖 32**： `ManuallyCreatedDBObjects.dll` 列在物件總管（[按一下以觀看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image78.png)）

## <a name="summary"></a>總結

Microsoft SQL Server 2005 提供與 Common Language Runtime （CLR）的整合，可讓您使用 managed 程式碼建立資料庫物件。 之前，這些資料庫物件只能使用 T-sql 建立，但我們現在可以使用 .NET 程式設計語言（例如C#）來建立這些物件。 在本教學課程中，我們建立了兩個 managed 預存程式和一個受控的使用者定義函數。

Visual Studio 的 SQL Server 專案類型可協助建立、編譯和部署受管理的資料庫物件。 此外，它還提供豐富的調試支援。 不過，SQL Server 專案類型僅適用于 Visual Studio 的 Professional 和 Team 系統版本。 對於使用 Visual Web Developer 或 Standard Edition Visual Studio 的，必須手動執行建立、編譯和部署步驟，如我們在步驟13中所見。

快樂的程式設計！

## <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [使用者定義函數的優點和缺點](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)
- [在 Managed 程式碼中建立 SQL Server 2005 物件](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [在 SQL Server 2005 中使用 Managed 程式碼建立觸發程式](http://www.15seconds.com/issue/041006.htm)
- [如何：建立和執行 CLR SQL Server 預存程式](https://msdn.microsoft.com/library/5czye81z(VS.80).aspx)
- [如何：建立和執行 CLR SQL Server 使用者定義函數](https://msdn.microsoft.com/library/w2kae45k(VS.80).aspx)
- [如何：編輯 `Test.sql` 腳本以執行 SQL 物件](https://msdn.microsoft.com/library/ms233682(VS.80).aspx)
- [使用者定義函數簡介](http://www.sqlteam.com/item.asp?ItemID=1955)
- [Managed 程式碼和 SQL Server 2005 （影片）](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [Transact-SQL 參考](https://msdn.microsoft.com/library/aa299742(SQL.80).aspx)
- [逐步解說：在 Managed 程式碼中建立預存程式](https://msdn.microsoft.com/library/zxsa8hkf(VS.80).aspx)

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Jacob Lauritsen。 除了複習本文外，S ren 也會建立本文下載的C# Visual Express Edition 專案，以手動編譯受控資料庫物件。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](debugging-stored-procedures-cs.md)
> [下一頁](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)
