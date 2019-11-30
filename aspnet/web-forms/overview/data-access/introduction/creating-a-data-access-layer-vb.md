---
uid: web-forms/overview/data-access/introduction/creating-a-data-access-layer-vb
title: 建立資料存取層（VB） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將從頭開始，並使用具類型資料集來建立資料存取層（DAL）來存取資料庫中的資訊。
ms.author: riande
ms.date: 04/05/2010
ms.assetid: 6227233a-6254-4b6b-9a89-947efef22330
msc.legacyurl: /web-forms/overview/data-access/introduction/creating-a-data-access-layer-vb
msc.type: authoredcontent
ms.openlocfilehash: 51c9255f80f83a68cf26decf318347752498491a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74635430"
---
# <a name="creating-a-data-access-layer-vb"></a>建立資料存取層 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_1_VB.exe)或[下載 PDF](creating-a-data-access-layer-vb/_static/datatutorial01vb1.pdf)

> 在本教學課程中，我們將從頭開始，並使用具類型資料集來建立資料存取層（DAL）來存取資料庫中的資訊。

## <a name="introduction"></a>簡介

身為 網頁程式開發人員，我們的生活會在處理資料方面。 我們會建立用來儲存資料的資料庫、用來抓取和修改的程式碼，以及用來收集和摘要的 web 網頁。 這是冗長系列中的第一個教學課程，會探索在 ASP.NET 2.0 中執行這些常見模式的技術。 我們將從建立由資料存取層（DAL）組成的[軟體架構](http://en.wikipedia.org/wiki/Software_architecture)，使用具類型的資料集、會強制執行自訂商務規則的商業邏輯層（BLL），以及由共用通用頁面配置的 ASP.NET 網頁組成的展示層。 一旦完成這後端的基礎，我們將移至報告，示範如何顯示、摘要、收集和驗證 web 應用程式中的資料。 這些教學課程的目的是要精簡，並提供逐步指示，讓您能以視覺化方式逐步完成整個流程。 每個教學課程都C#可在和 Visual Basic 版本中取得，並包含下載所使用的完整程式碼。 （第一個教學課程的時間很長，但其餘部分會以更消化的區塊呈現）。

在這些教學課程中，我們將使用放在 `App_Data` 目錄中的 Microsoft SQL Server 2005 Express Edition 版本的 Northwind 資料庫。 除了資料庫檔案以外，如果您想要使用不同的資料庫版本，[`App_Data`] 資料夾也會包含用於建立資料庫的 SQL 腳本。 如果您想要的話，也可以[直接從 Microsoft 下載](https://www.microsoft.com/downloads/details.aspx?FamilyID=06616212-0356-46a0-8da2-eebc53a68034&amp;DisplayLang=en)這些腳本。 如果您使用不同的 SQL Server 版本的 Northwind 資料庫，就必須更新應用程式 `Web.config` 檔中的 `NORTHWNDConnectionString` 設定。 Web 應用程式是使用 Visual Studio 2005 Professional Edition 作為以檔案系統為基礎的網站專案所建立。 不過，所有教學課程都適用于免費版的 Visual Studio 2005、 [Visual Web Developer](https://msdn.microsoft.com/vstudio/express/vwd/)。

在本教學課程中，我們將從頭開始，並建立資料存取層（DAL），接著在第二個教學課程中建立[商務邏輯層（BLL）](creating-a-business-logic-layer-vb.md) ，然後使用第三個[頁面配置和導覽](master-pages-and-site-navigation-vb.md)。 第三個教學課程之後，將會根據前三個所配置的基礎來建立。 在第一個教學課程中，我們有很多討論，所以 Visual Studio，讓我們開始吧！

## <a name="step-1-creating-a-web-project-and-connecting-to-the-database"></a>步驟1：建立 Web 專案並連接到資料庫

在建立資料存取層（DAL）之前，我們必須先建立網站，並設定我們的資料庫。 一開始請先建立新的以檔案系統為基礎的 ASP.NET 網站。 若要完成此動作，請移至 [檔案] 功能表，然後選擇 [新網站]，並顯示 [新網站] 對話方塊。 選擇 [ASP.NET 網站] 範本，將 [位置] 下拉式清單設定為 [檔案系統]，選擇要放置網站的資料夾，然後將語言設定為 [Visual Basic]。

[![建立以檔案系統為基礎的新網站](creating-a-data-access-layer-vb/_static/image2.png)](creating-a-data-access-layer-vb/_static/image1.png)

**圖 1**：建立以檔案系統為基礎的新網站（[按一下以觀看完整大小的影像](creating-a-data-access-layer-vb/_static/image3.png)）

這會建立新的網站，其中包含 `Default.aspx` ASP.NET 頁面、`App_Data` 資料夾和 `Web.config` 檔案。

建立網站後，下一個步驟是在 Visual Studio 的伺服器總管中加入資料庫的參考。 藉由將資料庫加入伺服器總管，您可以從 Visual Studio 內新增資料表、預存程式、views 等等。 您也可以透過 [查詢產生器] 手動或以圖形方式來查看資料表資料或建立自己的查詢。 此外，當我們為 DAL 建立具類型的資料集時，我們必須將 Visual Studio 指向應該用來結構化具類型資料集的資料庫。 雖然我們可以在該時間點提供此連接資訊，Visual Studio 會自動填入伺服器總管中已註冊之資料庫的下拉式清單。

將 Northwind 資料庫新增至伺服器總管的步驟取決於您想要在 `App_Data` 資料夾中使用 SQL Server 2005 Express Edition 資料庫，還是要改為使用 Microsoft SQL Server 2000 或2005資料庫伺服器安裝程式。

## <a name="using-a-database-in-theapp_datafolder"></a>使用`App_Data`資料夾中的資料庫

如果您沒有要連接的 SQL Server 2000 或2005資料庫伺服器，或只是想要避免將資料庫新增至資料庫伺服器，您可以使用位於所下載網站 `App_Data` 資料夾（`NORTHWND.MDF`）中的 SQL Server 2005 Express Edition 版本的 Northwind 資料庫。

放在 [`App_Data`] 資料夾中的資料庫會自動加入至伺服器總管。 假設您已在電腦上安裝 SQL Server 2005 Express Edition，您應該會看到名為 NORTHWND.MDF 檔的節點。MDF 在伺服器總管中，您可以展開並流覽其資料表、視圖、預存程式等（請參閱 [圖 2]）。

[`App_Data`] 資料夾也可以保存 Microsoft Access `.mdb` 檔案，像其 SQL Server 對應專案一樣，會自動新增至伺服器總管。 如果您不想要使用任何 SQL Server 選項，您一律可以[下載 Microsoft Access 版本的 Northwind 資料庫](https://www.microsoft.com/downloads/details.aspx?FamilyID=C6661372-8DBE-422B-8676-C632D66C529C&amp;displaylang=EN)檔案，並放入 `App_Data` 目錄。 不過，請記住，Access 資料庫並不像 SQL Server 的功能豐富，而且不是設計用於網站案例中。 此外，有幾個35個以上的教學課程會利用存取所不支援的某些資料庫層級功能。

## <a name="connecting-to-the-database-in-a-microsoft-sql-server-2000-or-2005-database-server"></a>連接到 Microsoft SQL Server 2000 或2005資料庫伺服器中的資料庫

或者，您也可以連接到安裝在資料庫伺服器上的 Northwind 資料庫。 如果資料庫伺服器尚未安裝 Northwind 資料庫，您必須先執行本教學課程下載所包含的安裝腳本，或直接從 Microsoft 網站[下載 SQL Server 2000 版的 Northwind 和安裝腳本](https://www.microsoft.com/downloads/details.aspx?FamilyID=06616212-0356-46a0-8da2-eebc53a68034&amp;DisplayLang=en)，以將它加入至資料庫伺服器。

安裝資料庫之後，請移至 Visual Studio 中的伺服器總管，以滑鼠右鍵按一下 [資料連線] 節點，然後選擇 [加入連接]。 如果您看不到 伺服器總管移至 View/伺服器總管，或按 Ctrl + Alt + S。 這會顯示 [新增連接] 對話方塊，您可以在其中指定要連接的伺服器、驗證資訊，以及資料庫名稱。 當您成功設定資料庫連接資訊，並按一下 [確定] 按鈕之後，資料庫就會加入為 [資料連線] 節點底下的節點。 您可以展開資料庫節點，以流覽其資料表、視圖、預存程式等等。

![新增連接至資料庫伺服器的 Northwind 資料庫](creating-a-data-access-layer-vb/_static/image4.png)

**圖 2**：將連接新增至資料庫伺服器的 Northwind 資料庫

## <a name="step-2-creating-the-data-access-layer"></a>步驟2：建立資料存取層

使用資料時，其中一個選項是將資料特有的邏輯直接內嵌到展示層（在 web 應用程式中，ASP.NET 網頁會構成展示層）。 這可能會在 ASP.NET 網頁的程式碼部分中撰寫 ADO.NET 程式碼，或使用標記部分的 SqlDataSource 控制項。 不論是哪一種情況，這種方法都會將資料存取邏輯與展示層緊密耦合在一起。 不過，建議的方法是將資料存取邏輯與展示層分開。 這種個別層稱為「資料存取層」，簡稱為 DAL，而且通常會實作為個別的類別庫專案。 此分層架構的優點已妥善記載（請參閱本教學課程結尾處的「進一步閱讀」一節，以取得這些優點的相關資訊），這是我們將在此系列中採用的方法。

基礎資料來源特有的所有程式碼，例如建立資料庫的連接、發行 `SELECT`、`INSERT`、`UPDATE`和 `DELETE` 命令等等，都應該位於 DAL 中。 展示層不應包含任何對這類資料存取程式碼的參考，而應該改為呼叫 DAL 以進行任何和所有資料要求。 資料存取層通常包含存取基礎資料庫資料的方法。 例如，Northwind 資料庫具有 `Products` 和 `Categories` 資料表，可記錄要銷售的產品及其所屬的類別目錄。 在 DAL 中，我們將會有如下的方法：

- `GetCategories(),`，會傳回所有類別的相關資訊
- `GetProducts()`，這會傳回所有產品的相關資訊
- `GetProductsByCategoryID(categoryID)`，會傳回屬於指定分類的所有產品
- `GetProductByProductID(productID)`，這會傳回特定產品的相關資訊

這些方法在叫用時，將會連接到資料庫、發出適當的查詢，然後傳回結果。 我們傳回這些結果的方式很重要。 這些方法可能只會傳回資料庫查詢所填入的資料集或 DataReader，但最好是使用*強型別物件*傳回這些結果。 強型別物件是其架構在編譯時期是嚴格定義的，相反地，是鬆散型別物件，這是在執行時間之前不知道其架構的一個。

例如，DataReader 和資料集（預設值）是鬆散類型的物件，因為其架構是由用來填入它們的資料庫查詢所傳回的資料行所定義。 若要從鬆散類型的 DataTable 存取特定資料行，我們需要使用類似以下的語法： `DataTable.Rows(index)("columnName")`。 在此範例中，DataTable 的鬆散類型是由我們需要使用字串或序數索引來存取資料行名稱的事實所展現。 另一方面，強型別 DataTable 會將它的每個資料行都實作為屬性，產生如下的程式碼： `DataTable.Rows(index).columnName`。

若要傳回強型別物件，開發人員可以建立自己的自訂商務物件或使用具類型的資料集。 開發人員會將商務物件實作為一個類別，其屬性通常會反映商務物件所代表之基礎資料庫資料表的資料行。 具類型資料集是根據資料庫架構 Visual Studio 產生的類別，而且其成員是根據此架構而強型別。 具類型的資料集本身是由擴充 ADO.NET 資料集、DataTable 和 DataRow 類別的類別所組成。 除了強型別的 Datatable，型別資料集現在也包含 Tableadapter，也就是具有方法來填入資料集的 Datatable，並將 Datatable 中的修改傳播回資料庫的類別。

> [!NOTE]
> 如需有關使用具類型資料集與自訂商務物件之優缺點的詳細資訊，請參閱[設計資料層元件和透過層來傳遞資料](https://msdn.microsoft.com/library/ms978496.aspx)。

我們會將強型別資料集用於這些教學課程的架構。 [圖 3] 說明使用具型別資料集之應用程式的不同層之間的工作流程。

[![所有資料存取程式碼都已歸入 DAL](creating-a-data-access-layer-vb/_static/image6.png)](creating-a-data-access-layer-vb/_static/image5.png)

**圖 3**：所有資料存取程式碼都已歸入 DAL （[按一下以觀看完整大小的影像](creating-a-data-access-layer-vb/_static/image7.png)）

## <a name="creating-a-typed-dataset-and-table-adapter"></a>建立具類型的資料集和資料表介面卡

若要開始建立 DAL，我們一開始會先將具型別資料集加入至專案。 若要完成這項操作，請以滑鼠右鍵按一下 方案總管中的專案節點，然後選擇 加入新專案。 從範本清單中選取 [資料集] 選項，並將其命名為 `Northwind.xsd`。

[![選擇將新的資料集加入至您的專案](creating-a-data-access-layer-vb/_static/image9.png)](creating-a-data-access-layer-vb/_static/image8.png)

**圖 4**：選擇將新的資料集加入至您的專案（[按一下以查看完整大小的影像](creating-a-data-access-layer-vb/_static/image10.png)）

按一下 [新增] 之後，當系統提示您將資料集加入 `App_Code` 資料夾時，請選擇 [是]。 然後會顯示具類型資料集的設計工具，並啟動 TableAdapter 設定 Wizard，讓您將第一個 TableAdapter 新增至具類型的資料集。

具類型資料集可做為資料的強型別集合。它是由強型別 DataTable 實例所組成，其中每一個都是由強型別的 DataRow 實例所組成。 我們會針對每個需要在此教學課程系列中使用的基礎資料庫資料表，建立一個強型別 DataTable。 讓我們從建立 `Products` 資料表的 DataTable 開始。

請記住，強型別 Datatable 不會包含有關如何從其基礎資料庫資料表存取資料的任何資訊。 為了抓取資料以填入 DataTable，我們使用 TableAdapter 類別，其作用就像我們的資料存取層。 針對我們的 `Products` DataTable，TableAdapter 會包含要從展示層叫用 `GetProducts()`、`GetProductByCategoryID(categoryID)`等等的方法。 DataTable 的角色是用來在層之間傳遞資料的強型別物件。

TableAdapter 設定向導一開始會提示您選取要使用的資料庫。 下拉式清單會顯示伺服器總管中的那些資料庫。 如果您未將 Northwind 資料庫新增至伺服器總管，此時您可以按一下 [新增連接] 按鈕來執行此動作。

[![從下拉式清單中選擇 Northwind 資料庫](creating-a-data-access-layer-vb/_static/image12.png)](creating-a-data-access-layer-vb/_static/image11.png)

**圖 5**：從下拉式清單中選擇 Northwind 資料庫（[按一下以查看完整大小的影像](creating-a-data-access-layer-vb/_static/image13.png)）

選取資料庫並按一下 [下一步] 之後，系統會詢問您是否要將連接字串儲存在 `Web.config` 檔案中。 藉由儲存連接字串，您將可避免在 TableAdapter 類別中硬式編碼，以在未來連接字串資訊變更時簡化專案。 如果您選擇將連接字串儲存在設定檔中，它會放在 [`<connectionStrings>`] 區段中，您可以[選擇性地](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx)將它加密以提高安全性，或稍後透過 IIS GUI 管理工具中的新 [ASP.NET 2.0] 屬性頁修改，這對系統管理員更是理想的選擇。

[![將連接字串儲存至 web.config](creating-a-data-access-layer-vb/_static/image15.png)](creating-a-data-access-layer-vb/_static/image14.png)

**圖 6**：將連接字串儲存至 `Web.config` （[按一下以查看完整大小的影像](creating-a-data-access-layer-vb/_static/image16.png)）

接下來，我們需要定義第一個強型別 DataTable 的架構，並提供在擴展強型別資料集時，用於 TableAdapter 的第一個方法。 這兩個步驟的完成方式是建立查詢，以傳回資料表中我們想要反映在 DataTable 中的資料行。 在嚮導的結尾，我們會提供方法名稱給此查詢。 完成之後，就可以從我們的展示層叫用這個方法。 方法會執行已定義的查詢，並填入強型別的 DataTable。

若要開始定義 SQL 查詢，我們必須先指出要如何讓 TableAdapter 發出查詢。 我們可以使用特定 SQL 語句、建立新的預存程式，或使用現有的預存程式。 在這些教學課程中，我們將使用特定 SQL 語句。 如需使用預存程式的範例，請參閱[Brian Noyes](http://briannoyes.net/)的文章

[![使用特定 SQL 語句來查詢資料](creating-a-data-access-layer-vb/_static/image18.png)](creating-a-data-access-layer-vb/_static/image17.png)

**圖 7**：使用臨機操作 SQL 語句來查詢資料（[按一下以查看完整大小的影像](creating-a-data-access-layer-vb/_static/image19.png)）

此時，我們可以手動輸入 SQL 查詢。 在 TableAdapter 中建立第一個方法時，您通常會想要讓查詢傳回必須在對應 DataTable 中表示的那些資料行。 我們可以藉由建立查詢來傳回 `Products` 資料表中的所有資料行和所有資料列來完成這項操作：

[![在文字方塊中輸入 SQL 查詢](creating-a-data-access-layer-vb/_static/image21.png)](creating-a-data-access-layer-vb/_static/image20.png)

**圖 8**：在文字方塊中輸入 SQL 查詢（[按一下以查看完整大小的影像](creating-a-data-access-layer-vb/_static/image22.png)）

或者，使用 [查詢產生器] 並以圖形方式建立查詢，如 [圖 9] 所示。

[![透過查詢編輯器以圖形方式建立查詢](creating-a-data-access-layer-vb/_static/image24.png)](creating-a-data-access-layer-vb/_static/image23.png)

**圖 9**：透過查詢編輯器以圖形方式建立查詢（[按一下以查看完整大小的影像](creating-a-data-access-layer-vb/_static/image25.png)）

建立查詢之後，在移至下一個畫面之前，請按一下 [Advanced Options] 按鈕。 在網站專案中，預設會選取 [產生 Insert、Update 和 Delete 語句] 唯一的 [advanced] 選項;如果您從類別庫或 Windows 專案執行此嚮導，也會一併選取 [使用開放式平行存取] 選項。 請暫時不要勾選 [使用開放式平行存取] 選項。 我們將在未來的教學課程中檢查開放式平行存取。

[![只選取 [產生 Insert、Update 和 Delete 語句] 選項](creating-a-data-access-layer-vb/_static/image27.png)](creating-a-data-access-layer-vb/_static/image26.png)

**圖 10**：只選取 [產生 Insert]、[Update] 和 [Delete 語句] 選項（[按一下以查看完整大小的影像](creating-a-data-access-layer-vb/_static/image28.png)）

驗證 advanced 選項之後，請按 [下一步] 繼續前往最後一個畫面。 在這裡，我們會要求您選取要新增至 TableAdapter 的方法。 填入資料的模式有兩種：

- 以這種方法**填入 datatable** ：建立的方法會採用 DataTable 做為參數，並根據查詢結果填入它。 例如，ADO.NET DataAdapter 類別會使用其 `Fill()` 方法來執行此模式。
- 傳回具有這個方法的**datatable** 。此方法會為您建立並填滿 datatable，並傳回做為方法傳回值。

您可以讓 TableAdapter 執行其中一種或兩種模式。 您也可以重新命名此處提供的方法。 讓我們將這兩個核取方塊保留為已核取，即使在這些教學課程中，我們只會使用第二個模式。 此外，讓我們將而不是泛型 `GetData` 方法重新命名為 `GetProducts`。

若已核取，則最後一個核取方塊 "GenerateDBDirectMethods" 會建立 TableAdapter `Insert()`、`Update()`和 `Delete()` 方法。 如果您將此選項保留為未核取，則必須透過 TableAdapter 的唯一 `Update()` 方法來完成所有更新，這會採用具類型的資料集、DataTable、單一 DataRow 或 Datarow 的陣列。 （如果您已從 [圖 9] 中的 [advanced] 屬性取消核取 [產生 Insert、Update 和 Delete 語句] 選項，則此核取方塊的設定將不會有任何作用。）讓我們將此核取方塊保留為已選取。

[![將方法名稱從 [GetProducts] 變更為 []](creating-a-data-access-layer-vb/_static/image30.png)](creating-a-data-access-layer-vb/_static/image29.png)

**圖 11**：將方法名稱從 `GetData` 變更為 `GetProducts` （[按一下以查看完整大小的影像](creating-a-data-access-layer-vb/_static/image31.png)）

按一下 [完成] 以完成嚮導。 在嚮導關閉之後，我們會回到 [DataSet 設計工具]，其中會顯示我們剛才建立的 DataTable。 您可以查看 `Products` DataTable 中的資料行清單（`ProductID`、`ProductName`等等），以及 `ProductsTableAdapter` 的方法（`Fill()` 和 `GetProducts()`）。

[![Products DataTable 和 ProductsTableAdapter 已加入至具類型的資料集](creating-a-data-access-layer-vb/_static/image33.png)](creating-a-data-access-layer-vb/_static/image32.png)

**圖 12**： `Products` DataTable 和 `ProductsTableAdapter` 已加入至具類型的資料集（[按一下以查看完整大小的影像](creating-a-data-access-layer-vb/_static/image34.png)）

此時，我們有一個具類型的資料集，其中具有單一 DataTable （`Northwind.Products`）和強型別的 DataAdapter 類別（`NorthwindTableAdapters.ProductsTableAdapter`），並具有 `GetProducts()` 方法。 這些物件可以用來從程式碼存取所有產品的清單，例如：

[!code-vb[Main](creating-a-data-access-layer-vb/samples/sample1.vb)]

這段程式碼不需要我們撰寫一位資料存取特定的程式碼。 我們不需要具現化任何 ADO.NET 類別，我們不需要參考任何連接字串、SQL 查詢或預存程式。 相反地，TableAdapter 會為我們提供低層級的資料存取程式碼。

這個範例中使用的每個物件也都是強型別，可讓 Visual Studio 提供 IntelliSense 和編譯時間型別檢查。 而且所有由 TableAdapter 傳回的 Datatable，都可以系結至 ASP.NET 資料 Web 控制項，例如 GridView、DetailsView、DropDownList、CheckBoxList 和其他幾個。 下列範例說明如何將 `GetProducts()` 方法傳回的 DataTable 系結至 GridView，只要在 `Page_Load` 事件處理常式內的三行程式碼中缺乏說明致。

AllProducts .aspx

[!code-aspx[Main](creating-a-data-access-layer-vb/samples/sample2.aspx)]

AllProducts .aspx

[!code-vb[Main](creating-a-data-access-layer-vb/samples/sample3.vb)]

[![顯示在 GridView 中的產品清單](creating-a-data-access-layer-vb/_static/image36.png)](creating-a-data-access-layer-vb/_static/image35.png)

**圖 13**：產品清單會顯示在 GridView 中（[按一下以觀看完整大小的影像](creating-a-data-access-layer-vb/_static/image37.png)）

雖然此範例需要在 ASP.NET 網頁的 `Page_Load` 事件處理常式中撰寫三行程式碼，但在未來的教學課程中，我們將探討如何使用 ObjectDataSource，以宣告的方式從 DAL 抓取資料。 有了 ObjectDataSource，我們就不需要撰寫任何程式碼，而且也會取得分頁和排序支援！

## <a name="step-3-adding-parameterized-methods-to-the-data-access-layer"></a>步驟3：將參數化方法加入至資料存取層

此時，我們的 `ProductsTableAdapter` 類別有一個方法，`GetProducts()`，它會傳回資料庫中的所有產品。 雖然能夠使用所有產品都非常有用，但有時候我們會想要取得特定產品的相關資訊，或屬於特定類別的所有產品。 若要在資料存取層中加入這類功能，我們可以將參數化方法加入至 TableAdapter。

讓我們新增 `GetProductsByCategoryID(categoryID)` 方法。 若要將新的方法加入 DAL，請回到 DataSet 設計工具，以滑鼠右鍵按一下 [`ProductsTableAdapter`] 區段，然後選擇 [加入查詢]。

![以滑鼠右鍵按一下 TableAdapter，然後選擇 [加入查詢]](creating-a-data-access-layer-vb/_static/image38.png)

**圖 14**：以滑鼠右鍵按一下 TableAdapter，然後選擇 [加入查詢]

我們會先提示我們是否要使用特定 SQL 語句或新的或現有的預存程式來存取資料庫。 讓我們選擇再次使用特定 SQL 語句。 接下來，我們會詢問您想要使用哪種類型的 SQL 查詢。 因為我們想要傳回屬於指定類別的所有產品，所以我們想要撰寫會傳回資料列的 `SELECT` 語句。

[![選擇建立會傳回資料列的 SELECT 語句](creating-a-data-access-layer-vb/_static/image40.png)](creating-a-data-access-layer-vb/_static/image39.png)

**圖 15**：選擇建立會傳回資料列的 `SELECT` 語句（[按一下以查看完整大小的影像](creating-a-data-access-layer-vb/_static/image41.png)）

下一個步驟是定義用來存取資料的 SQL 查詢。 因為我們想要只傳回屬於特定類別的產品，所以我使用 `GetProducts()`的相同 `SELECT` 語句，但新增下列 `WHERE` 子句： `WHERE CategoryID = @CategoryID`。 `@CategoryID` 參數會向 TableAdapter wizard 指示，我們所建立的方法將需要對應類型的輸入參數（也就是可為 null 的整數）。

[![輸入查詢，只傳回指定分類中的產品](creating-a-data-access-layer-vb/_static/image43.png)](creating-a-data-access-layer-vb/_static/image42.png)

**圖 16**：輸入只傳回指定分類中之產品的查詢（[按一下以觀看完整大小的影像](creating-a-data-access-layer-vb/_static/image44.png)）

在最後一個步驟中，我們可以選擇要使用的資料存取模式，以及自訂所產生之方法的名稱。 在填滿模式中，讓我們將名稱變更為 `FillByCategoryID`，並針對傳回 DataTable 傳回模式（`GetX` 方法），讓我們使用 `GetProductsByCategoryID`。

[![選擇 TableAdapter 方法的名稱](creating-a-data-access-layer-vb/_static/image46.png)](creating-a-data-access-layer-vb/_static/image45.png)

**圖 17**：選擇 TableAdapter 方法的名稱（[按一下以查看完整大小的影像](creating-a-data-access-layer-vb/_static/image47.png)）

完成 wizard 之後，[DataSet 設計工具] 會包含新的 TableAdapter 方法。

![產品現在可以依類別進行查詢](creating-a-data-access-layer-vb/_static/image48.png)

**圖 18**：產品現在可以依類別進行查詢

請花點時間使用相同的技巧來新增 `GetProductByProductID(productID)` 方法。

這些參數化查詢可以直接從 DataSet 設計工具進行測試。 以滑鼠右鍵按一下 TableAdapter 中的方法，然後選擇 [預覽資料]。 接下來，輸入要用於參數的值，然後按一下 [預覽]。

[會顯示屬於飲料類別的產品 ![](creating-a-data-access-layer-vb/_static/image50.png)](creating-a-data-access-layer-vb/_static/image49.png)

**圖 19**：顯示屬於飲料類別的產品（[按一下以觀看完整大小的影像](creating-a-data-access-layer-vb/_static/image51.png)）

使用 DAL 中的 `GetProductsByCategoryID(categoryID)` 方法，我們現在可以建立 ASP.NET 網頁，只顯示指定分類中的產品。 下列範例會顯示 [飲料] 分類中的所有產品，其 `CategoryID` 為1。

飲料 .aspx

[!code-aspx[Main](creating-a-data-access-layer-vb/samples/sample4.aspx)]

飲料 .aspx

[!code-vb[Main](creating-a-data-access-layer-vb/samples/sample5.vb)]

[會顯示 [飲料] 類別中的產品 ![](creating-a-data-access-layer-vb/_static/image53.png)](creating-a-data-access-layer-vb/_static/image52.png)

**圖 20**：顯示飲料類別中的產品（[按一下以觀看完整大小的影像](creating-a-data-access-layer-vb/_static/image54.png)）

## <a name="step-4-inserting-updating-and-deleting-data"></a>步驟4：插入、更新和刪除資料

有兩種模式通常用於插入、更新和刪除資料。 第一種模式是所謂的「資料庫直接模式」，其中包括建立方法，在叫用時，將 `INSERT`、`UPDATE`或 `DELETE` 命令發行至在單一資料庫記錄上運作的資料庫。 這類方法通常會以一系列的純量值（整數、字串、布林值、日期時間等等）來傳遞，並對應至要插入、更新或刪除的值。 例如，使用 `Products` 資料表的這個模式時，delete 方法會採用整數參數，指出要刪除之記錄的 `ProductID`，而 insert 方法會接受 `ProductName`的字串、`UnitPrice`的十進位數、`UnitsOnStock`的整數等等。

[![每個插入、更新和刪除要求都會立即傳送至資料庫](creating-a-data-access-layer-vb/_static/image56.png)](creating-a-data-access-layer-vb/_static/image55.png)

**圖 21**：每個插入、更新和刪除要求都會立即傳送至資料庫（[按一下以查看完整大小的影像](creating-a-data-access-layer-vb/_static/image57.png)）

另一個稱為「批次更新」模式的模式，就是在一個方法呼叫中更新整個資料集、DataTable 或 Datarow 的集合。 使用此模式時，開發人員會刪除、插入及修改 DataTable 中的 Datarow，然後將這些 Datarow 或 DataTable 傳遞至更新方法。 然後，這個方法會列舉傳入的 Datarow，判斷它們是否已修改、加入或刪除（透過 DataRow 的[RowState 屬性](https://msdn.microsoft.com/library/system.data.datarow.rowstate.aspx)值），並針對每一筆記錄發出適當的資料庫要求。

[當叫用 Update 方法時，![所有變更都會與資料庫同步處理](creating-a-data-access-layer-vb/_static/image59.png)](creating-a-data-access-layer-vb/_static/image58.png)

**圖 22**：叫用 Update 方法時，所有的變更都會與資料庫同步處理（[按一下以查看完整大小的影像](creating-a-data-access-layer-vb/_static/image60.png)）

根據預設，TableAdapter 會使用批次更新模式，但也支援 DB 直接模式。 因為我們在建立 TableAdapter 時，從 [Advanced] 屬性選取 [產生 Insert、Update 和 Delete 語句] 選項，所以 `ProductsTableAdapter` 包含會執行批次更新模式的 `Update()` 方法。 具體而言，TableAdapter 包含可以傳遞具類型資料集、強型別 DataTable 或一或多個 Datarow 的 `Update()` 方法。 如果您在第一次建立 TableAdapter 時已核取 [GenerateDBDirectMethods] 核取方塊，則 DB 直接模式也會透過 `Insert()`、`Update()`和 `Delete()` 方法來執行。

這兩種資料修改模式都會使用 TableAdapter 的 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 屬性，對資料庫發出其 `INSERT`、`UPDATE`和 `DELETE` 命令。 您可以藉由按一下 DataSet 設計工具中的 TableAdapter，然後前往屬性視窗，來檢查和修改 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 屬性。 （請確定您已選取 TableAdapter，而且 `ProductsTableAdapter` 物件是在屬性視窗的下拉式清單中選取的）。

[![TableAdapter 具有 InsertCommand、UpdateCommand 和 DeleteCommand 屬性](creating-a-data-access-layer-vb/_static/image62.png)](creating-a-data-access-layer-vb/_static/image61.png)

**圖 23**： TableAdapter 具有 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 屬性（[按一下以查看完整大小的影像](creating-a-data-access-layer-vb/_static/image63.png)）

若要檢查或修改任何資料庫命令屬性，請按一下 [`CommandText`] 子屬性，這會顯示 [查詢產生器]。

[![在查詢產生器中設定 INSERT、UPDATE 和 DELETE 子句](creating-a-data-access-layer-vb/_static/image65.png)](creating-a-data-access-layer-vb/_static/image64.png)

**圖 24**：在查詢產生器中設定 `INSERT`、`UPDATE`和 `DELETE` 語句（[按一下以查看完整大小的影像](creating-a-data-access-layer-vb/_static/image66.png)）

下列程式碼範例示範如何使用批次更新模式，將所有未中止且具有25個單位或更少的產品的價格加倍：

[!code-vb[Main](creating-a-data-access-layer-vb/samples/sample6.vb)]

下列程式碼說明如何使用 DB direct 模式，以程式設計方式刪除特定產品，然後更新一個，然後再新增一個：

[!code-vb[Main](creating-a-data-access-layer-vb/samples/sample7.vb)]

## <a name="creating-custom-insert-update-and-delete-methods"></a>建立自訂插入、更新和刪除方法

DB 直接方法所建立的 `Insert()`、`Update()`和 `Delete()` 方法可能有點麻煩，特別是針對具有許多資料行的資料表。 查看先前的程式碼範例時，如果沒有 IntelliSense 的協助，就不會特別清楚 `Products` 資料表資料行對應至 `Update()` 和 `Insert()` 方法的每個輸入參數。 有時候，我們只想要更新單一資料行或兩個，或想要自訂的 `Insert()` 方法，這可能會傳回新插入之記錄的 `IDENTITY` （自動遞增）欄位的值。

若要建立這類自訂方法，請回到 DataSet 設計工具。 以滑鼠右鍵按一下 TableAdapter，然後選擇 [加入查詢]，返回 [TableAdapter wizard]。 在第二個畫面上，我們可以指定要建立的查詢類型。 讓我們建立一個方法，它會加入新的產品，然後傳回新加入記錄的 `ProductID`值。 因此，選擇建立 `INSERT` 查詢。

[![建立方法，以將新的資料列加入 Products 資料表](creating-a-data-access-layer-vb/_static/image68.png)](creating-a-data-access-layer-vb/_static/image67.png)

**圖 25**：建立方法以將新的資料列加入 `Products` 資料表（[按一下以查看完整大小的影像](creating-a-data-access-layer-vb/_static/image69.png)）

在下一個畫面上，會顯示 `InsertCommand`的 `CommandText`。 藉由在查詢結尾加入 `SELECT SCOPE_IDENTITY()` 來擴大此查詢，這會傳回在相同範圍內的 `IDENTITY` 資料行中所插入的最後一個識別值。 （如需 `SCOPE_IDENTITY()` 的詳細資訊，以及您可能想要[使用範圍\_身分識別（），而不是 @@IDENTITY](http://weblogs.sqlteam.com/travisl/archive/2003/10/29/405.aspx)，請參閱[技術檔](https://msdn.microsoft.com/library/ms190315.aspx)。）請確定您在加入 `SELECT` 語句之前，以分號結束 `INSERT` 語句。

[![擴大查詢，以傳回 SCOPE_IDENTITY （）值](creating-a-data-access-layer-vb/_static/image71.png)](creating-a-data-access-layer-vb/_static/image70.png)

**圖 26**：擴大查詢以傳回 `SCOPE_IDENTITY()` 值（[按一下以查看完整大小的影像](creating-a-data-access-layer-vb/_static/image72.png)）

最後，將新方法命名為 `InsertProduct`。

[![將新的方法名稱設定為 InsertProduct](creating-a-data-access-layer-vb/_static/image74.png)](creating-a-data-access-layer-vb/_static/image73.png)

**圖 27**：將新的方法名稱設定為 `InsertProduct` （[按一下以查看完整大小的影像](creating-a-data-access-layer-vb/_static/image75.png)）

當您返回 DataSet 設計工具時，您會看到 `ProductsTableAdapter` 包含新的方法，`InsertProduct`。 如果這個新方法沒有 `Products` 資料表中每個資料行的參數，您可能會忘記使用分號來終止 `INSERT` 語句。 設定 `InsertProduct` 方法，並確定您有以分號分隔 `INSERT` 和 `SELECT` 語句。

根據預設，insert 方法會發出非查詢方法，這表示它們會傳回受影響的資料列數目。 不過，我們希望 `InsertProduct` 方法傳回查詢所傳回的值，而不是受影響的資料列數目。 若要完成此動作，請將 `InsertProduct` 方法的 `ExecuteMode` 屬性調整為 [`Scalar`]。

[![將 ExecuteMode 屬性變更為純量](creating-a-data-access-layer-vb/_static/image77.png)](creating-a-data-access-layer-vb/_static/image76.png)

**圖 28**：將 [`ExecuteMode`] 屬性變更為 [`Scalar`] （[按一下以查看完整大小的影像](creating-a-data-access-layer-vb/_static/image78.png)）

下列程式碼會示範這個新的 `InsertProduct` 方法的運作方式：

[!code-vb[Main](creating-a-data-access-layer-vb/samples/sample8.vb)]

## <a name="step-5-completing-the-data-access-layer"></a>步驟5：完成資料存取層

請注意，`ProductsTableAdapters` 類別會從 `Products` 資料表傳回 `CategoryID` 和 `SupplierID` 值，但不包含來自 `CategoryName` 資料表的 `Categories` 資料行或來自 `CompanyName` 資料表的 `Suppliers` 資料行，不過，這可能是我們想要在顯示產品資訊時顯示的資料行。 我們可以擴充 TableAdapter 的初始方法 `GetProducts()`，以同時包含 `CategoryName` 和 `CompanyName` 的資料行值，這會更新強型別的 DataTable 以包含這些新的資料行。

不過，這可能會發生問題，因為 TableAdapter 用來插入、更新和刪除資料的方法是以這個初始方法為基礎。 幸好，用於插入、更新和刪除的自動產生方法不會受到 `SELECT` 子句中的子查詢影響。 藉由將查詢新增至 `Categories` 並 `Suppliers` 做為子查詢，而不是 `JOIN`，我們不需要重新撰寫修改資料的方法。 以滑鼠右鍵按一下 `ProductsTableAdapter` 中的 [`GetProducts()`] 方法，然後選擇 [設定]。 然後，調整 `SELECT` 子句，使其看起來像這樣：

[!code-sql[Main](creating-a-data-access-layer-vb/samples/sample9.sql)]

[![更新 GetProducts （）方法的 SELECT 語句](creating-a-data-access-layer-vb/_static/image80.png)](creating-a-data-access-layer-vb/_static/image79.png)

**圖 29**：更新 `GetProducts()` 方法的 `SELECT` 語句（[按一下以查看完整大小的影像](creating-a-data-access-layer-vb/_static/image81.png)）

更新 `GetProducts()` 方法以使用這個新查詢之後，DataTable 會包含兩個新的資料行： `CategoryName` 和 `SupplierName`。

![Products DataTable 有兩個新的資料行](creating-a-data-access-layer-vb/_static/image82.png)

**圖 30**： `Products` DataTable 有兩個新的資料行

也請花點時間更新 `GetProductsByCategoryID(categoryID)` 方法中的 `SELECT` 子句。

如果您使用 `JOIN` 語法來更新 `GetProducts()` `SELECT`，DataSet 設計工具將無法自動產生方法，以使用 DB direct 模式來插入、更新和刪除資料庫資料。 相反地，您必須手動建立它們，就像我們稍早在本教學課程中的 `InsertProduct` 方法所做的一樣。 此外，如果您想要使用批次更新模式，則必須提供 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 屬性值。

## <a name="adding-the-remaining-tableadapters"></a>新增其餘的 Tableadapter

到目前為止，我們只探討了如何針對單一資料庫資料表使用單一 TableAdapter。 不過，Northwind 資料庫包含數個相關的資料表，我們需要在 web 應用程式中使用。 具類型的資料集可以包含多個相關的 Datatable。 因此，若要完成 DAL，我們必須在這些教學課程中，為我們將使用的其他資料表新增 Datatable。 若要將新的 TableAdapter 加入至具類型的資料集，請開啟 DataSet 設計工具，在設計工具中按一下滑鼠右鍵，然後選擇 [新增/TableAdapter]。 這會建立新的 DataTable 和 TableAdapter，並逐步引導您完成我們稍早在本教學課程中所檢查的 wizard。

請花幾分鐘的時間，使用下列查詢建立下列 Tableadapter 和方法。 請注意，`ProductsTableAdapter` 中的查詢包含用來抓取每個產品類別目錄和供應商名稱的子查詢。 此外，如果您已經跟著做過，就已經加入了 `ProductsTableAdapter` 類別的 `GetProducts()` 和 `GetProductsByCategoryID(categoryID)` 方法。

- **ProductsTableAdapter**

  - **GetProducts**： 

      [!code-sql[Main](creating-a-data-access-layer-vb/samples/sample10.sql)]
  - **GetProductsByCategoryID**： 

      [!code-sql[Main](creating-a-data-access-layer-vb/samples/sample11.sql)]
  - **GetProductsBySupplierID**： 

      [!code-sql[Main](creating-a-data-access-layer-vb/samples/sample12.sql)]
  - **GetProductByProductID**： 

      [!code-sql[Main](creating-a-data-access-layer-vb/samples/sample13.sql)]
- **CategoriesTableAdapter**

  - **GetCategories**： 

      [!code-sql[Main](creating-a-data-access-layer-vb/samples/sample14.sql)]
  - **GetCategoryByCategoryID**： 

      [!code-sql[Main](creating-a-data-access-layer-vb/samples/sample15.sql)]
- **SuppliersTableAdapter**

  - **GetSuppliers**： 

      [!code-sql[Main](creating-a-data-access-layer-vb/samples/sample16.sql)]
  - **GetSuppliersByCountry**： 

      [!code-sql[Main](creating-a-data-access-layer-vb/samples/sample17.sql)]
  - **GetSupplierBySupplierID**： 

      [!code-sql[Main](creating-a-data-access-layer-vb/samples/sample18.sql)]
- **EmployeesTableAdapter**

  - **GetEmployees**： 

      [!code-sql[Main](creating-a-data-access-layer-vb/samples/sample19.sql)]
  - **GetEmployeesByManager**： 

      [!code-sql[Main](creating-a-data-access-layer-vb/samples/sample20.sql)]
  - **GetEmployeeByEmployeeID**： 

      [!code-sql[Main](creating-a-data-access-layer-vb/samples/sample21.sql)]

[加入四個 Tableadapter 之後，![DataSet 設計工具](creating-a-data-access-layer-vb/_static/image84.png)](creating-a-data-access-layer-vb/_static/image83.png)

**圖 31**：已加入四個 tableadapter 之後的 DataSet 設計工具（[按一下以查看完整大小的影像](creating-a-data-access-layer-vb/_static/image85.png)）

## <a name="adding-custom-code-to-the-dal"></a>將自訂程式碼新增至 DAL

加入至具類型資料集的 Tableadapter 和 Datatable 會表示為 XML 架構定義檔（`Northwind.xsd`）。 您可以用滑鼠右鍵按一下 方案總管中的 `Northwind.xsd` 檔案，然後選擇 查看程式碼，以查看此架構資訊。

[![Northwinds 具類型資料集的 XML 架構定義（XSD）檔案](creating-a-data-access-layer-vb/_static/image87.png)](creating-a-data-access-layer-vb/_static/image86.png)

**圖 32**： Northwinds 具類型資料集的 XML 架構定義（XSD）檔案（[按一下以查看完整大小的影像](creating-a-data-access-layer-vb/_static/image88.png)）

在編譯或執行時間（ C#如有需要）時，此架構資訊會在設計階段轉譯為或 Visual Basic 程式碼，此時您可以使用偵錯工具逐步執行。 若要查看這個自動產生的程式碼，請移至類別檢視並向下切入至 TableAdapter 或具類型的資料集類別。 如果您在螢幕上看不到類別檢視，請移至 [View] 功能表並從該處選取，或按 Ctrl + Shift + C。 您可以從類別檢視查看具類型資料集和 TableAdapter 類別的屬性、方法和事件。 若要查看特定方法的程式碼，請按兩下類別檢視中的方法名稱，或在其上按一下滑鼠右鍵，然後選擇 [移至定義]。

![從類別檢視選取 [移至定義]，檢查自動產生的程式碼](creating-a-data-access-layer-vb/_static/image89.png)

**圖 33**：從類別檢視選取 [移至定義]，檢查自動產生的程式碼

雖然自動產生的程式碼可以是很好的時間，但程式碼通常非常通用，而且需要自訂以符合應用程式的獨特需求。 不過，擴充自動產生的程式碼的風險是，產生程式碼的工具可能會決定何時「重新產生」並覆寫您的自訂。 有了 .NET 2.0 的新部分類別概念，就可以輕鬆地將類別分割成多個檔案。 這可讓我們將自己的方法、屬性和事件新增至自動產生的類別，而不必擔心 Visual Studio 覆寫我們的自訂。

為了示範如何自訂 DAL，讓我們將 `GetProducts()` 方法新增至 `SuppliersRow` 類別。 `SuppliersRow` 類別代表 `Suppliers` 資料表中的單一記錄;每個供應商可以提供零到多個產品，因此 `GetProducts()` 會傳回指定供應商的這些產品。 若要完成這項工作，請在名為 `SuppliersRow.vb` 的 `App_Code` 資料夾中建立新的類別檔案，並新增下列程式碼：

[!code-vb[Main](creating-a-data-access-layer-vb/samples/sample22.vb)]

這個部分類別會指示編譯器在建立 `Northwind.SuppliersRow` 類別時，加入我們剛剛定義的 `GetProducts()` 方法。 如果您建立專案，然後回到類別檢視，您會看到 `GetProducts()` 現在列為 `Northwind.SuppliersRow`的方法。

![GetProducts （）方法現在是 SuppliersRow 類別的一部分](creating-a-data-access-layer-vb/_static/image90.png)

**圖 34**： `GetProducts()` 方法現在是 `Northwind.SuppliersRow` 類別的一部分

`GetProducts()` 方法現在可以用來列舉特定供應商的產品集合，如下列程式碼所示：

[!code-vb[Main](creating-a-data-access-layer-vb/samples/sample23.vb)]

這項資料也可以顯示在任何 ASP 中。NET 的資料 Web 控制項。 下列頁面會使用具有兩個欄位的 GridView 控制項：

- 顯示每個供應商名稱的 BoundField，以及
- 包含 BulletedList 控制項的 TemplateField，其系結至每個供應商的 `GetProducts()` 方法所傳回的結果。

我們將在未來的教學課程中，檢查如何顯示這類主版詳細資料包表。 目前，此範例的設計目的是要說明如何使用加入至 `Northwind.SuppliersRow` 類別的自訂方法。

SuppliersAndProducts .aspx

[!code-aspx[Main](creating-a-data-access-layer-vb/samples/sample24.aspx)]

SuppliersAndProducts .aspx

[!code-vb[Main](creating-a-data-access-layer-vb/samples/sample25.vb)]

[![供應商的公司名稱列在左欄中，其產品位於右邊](creating-a-data-access-layer-vb/_static/image92.png)](creating-a-data-access-layer-vb/_static/image91.png)

**圖 35**：供應商的公司名稱列在左欄中，其產品位於右側（[按一下以查看完整大小的影像](creating-a-data-access-layer-vb/_static/image93.png)）

## <a name="summary"></a>總結

建立 web 應用程式時，必須是您在開始建立展示層之前的第一個步驟。 有了 Visual Studio，根據具類型的資料集建立 DAL 是一項可在10-15 分鐘內完成的工作，而不需要撰寫一行程式碼。 繼續進行的教學課程將以此 DAL 為基礎。 在[下一個教學](creating-a-business-logic-layer-vb.md)課程中，我們將定義一些商務規則，並瞭解如何在不同的商業邏輯層中執行。

快樂的程式設計！

## <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [在 VS 2005 和 ASP.NET 2.0 中使用強型別 Tableadapter 和 Datatable 建立 DAL](https://weblogs.asp.net/scottgu/435498)
- [設計資料層元件和透過層級傳遞資料](https://msdn.microsoft.com/library/ms978496.aspx)
- [使用 Visual Studio 2005 DataSet 設計工具建立資料存取層](http://www.theserverside.net/articles/showarticle.tss?id=DataSetDesigner)
- [加密 ASP.NET 2.0 應用程式中的設定資訊](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx)
- [TableAdapter 概觀](https://msdn.microsoft.com/library/bz9tthwx.aspx)
- [使用具類型的資料集](https://msdn.microsoft.com/library/esbykkzb.aspx)
- [在 Visual Studio 2005 和 ASP.NET 2.0 中使用強型別資料存取](http://aspnet.4guysfromrolla.com/articles/020806-1.aspx)
- [如何擴充 TableAdapter 方法](https://blogs.msdn.com/vbteam/archive/2005/05/04/ExtendingTableAdapters.aspx)
- [從預存程式中取出純量資料](http://aspnet.4guysfromrolla.com/articles/062905-1.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>本教學課程中所含主題的影片訓練

- [ASP.NET 應用程式中的資料存取層](../../../videos/data-access/adonet-data-services/data-access-layers-in-aspnet-applications.md)
- [如何將資料集手動系結至 Datagrid](../../../videos/data-access/adonet-data-services/how-to-manually-bind-a-dataset-to-a-datagrid.md)
- [如何從 ASP 應用程式使用資料集和篩選](../../../videos/data-access/adonet-data-services/how-to-work-with-datasets-and-filters-from-an-asp-application.md)

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Ron 環保、Hilton Giesenow、Dennis Patterson、Liz Shulok、Abel Gomez 和 Carlos Santos。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](master-pages-and-site-navigation-cs.md)
> [下一頁](creating-a-business-logic-layer-vb.md)
