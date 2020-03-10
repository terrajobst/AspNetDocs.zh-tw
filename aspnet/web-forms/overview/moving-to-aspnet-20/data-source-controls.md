---
uid: web-forms/overview/moving-to-aspnet-20/data-source-controls
title: 資料來源控制項 |Microsoft Docs
author: microsoft
description: ASP.NET 1.x 中的 DataGrid 控制項在 Web 應用程式中標記為數據存取的絕佳改進。 不過，它並不是使用者易記的，
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 78fd0e92-f9c6-4e96-a5e9-0375b307a828
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-source-controls
msc.type: authoredcontent
ms.openlocfilehash: a2e2cfbec3e5aebf42a2de30bab7d45b4b610298
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639409"
---
# <a name="data-source-controls"></a>資料來源控制項

由[Microsoft](https://github.com/microsoft)

> ASP.NET 1.x 中的 DataGrid 控制項在 Web 應用程式中標記為數據存取的絕佳改進。 不過，它並不是方便使用者使用。 它仍然需要大量的程式碼，才能從它取得很有用的功能。 這就是所有資料存取在1.x 中的模式。

ASP.NET 1.x 中的 DataGrid 控制項在 Web 應用程式中標記為數據存取的絕佳改進。 不過，它並不是方便使用者使用。 它仍然需要大量的程式碼，才能從它取得很有用的功能。 這就是所有資料存取在1.x 中的模式。

ASP.NET 2.0 使用資料來源控制項來解決這種情況。 ASP.NET 2.0 中的資料來源控制項為開發人員提供了宣告式模型，可供您用來抓取資料、顯示資料和編輯資料。 資料來源控制項的目的是要提供一致的資料標記法給資料繫結控制項，而不論這些資料的來源為何。 ASP.NET 2.0 中資料來源控制項的核心是 DataSourceControl 抽象類別。 DataSourceControl 類別提供 IDataSource 介面和 IListSource 介面的基底實作為，後者可讓您將資料來源控制項指派為資料繫結控制項的 DataSource （透過新的 DataSourceId 屬性）稍後會討論），並將其中的資料公開為清單。 資料來源控制項中的每個資料清單都會公開為 DataSourceView 物件。 對 DataSourceView 實例的存取是由 IDataSource 介面提供。 例如，GetViewNames 方法會傳回 ICollection，讓您列舉與特定資料來源控制項相關聯的 DataSourceViews，而 GetView 方法可讓您依名稱存取特定的 DataSourceView 實例。

資料來源控制項沒有使用者介面。 它們會實作為伺服器控制項，讓它們可以支援宣告式語法，並在需要時能夠存取頁面狀態。 資料來源控制項不會將任何 HTML 標籤呈現給用戶端。

> [!NOTE]
> 如您稍後所見，使用資料來源控制項也會取得快取的優點。

## <a name="storing-connection-strings"></a>儲存連接字串

在我們開始探討如何設定資料來源控制項之前，我們應該先討論 ASP.NET 2.0 中有關連接字串的新功能。 ASP.NET 2.0 引進了設定檔案中的新區段，可讓您輕鬆地儲存可在執行時間動態讀取的連接字串。 &lt;connectionStrings&gt; 區段可讓您輕鬆地儲存連接字串。

下列程式碼片段會加入新的連接字串。

[!code-xml[Main](data-source-controls/samples/sample1.xml)]

> [!NOTE]
> 就如同 &lt;appSettings&gt; 區段，&lt;connectionStrings&gt; 區段會出現在設定檔中 &lt;system.web&gt; 區段之外。

若要使用這個連接字串，您可以在設定伺服器控制項的 ConnectionString 屬性時，使用下列語法。

[!code-aspx[Main](data-source-controls/samples/sample2.aspx)]

&lt;connectionStrings&gt; 區段也可以加密，如此就不會公開機密資訊。 這項功能將會在稍後的課程模組中討論。

## <a name="caching-data-sources"></a>快取資料來源

每個 DataSourceControl 都會提供四個屬性來設定快取;EnableCaching、CacheDuration、CacheExpirationPolicy 和 CacheKeyDependency。

## <a name="enablecaching"></a>EnableCaching

EnableCaching 是布林值屬性，可決定是否啟用資料來源控制項的快取。

## <a name="cacheduration-property"></a>CacheDuration 屬性

CacheDuration 屬性會設定快取保持有效的秒數。 將此屬性設定為**0**會使快取保持有效，直到明確失效為止。

## <a name="cacheexpirationpolicy-property"></a>CacheExpirationPolicy 屬性

CacheExpirationPolicy 屬性可以設定為 [**絕對**] 或 [**滑動**]。 將它設定為 [絕對] 表示資料快取的最大時間量是 CacheDuration 屬性所指定的秒數。 藉由將它設定為滑動，每次執行作業時，就會重設到期時間。

## <a name="cachekeydependency-property"></a>CacheKeyDependency 屬性

如果為 CacheKeyDependency 屬性指定了字串值，ASP.NET 將會根據該字串來設定新的快取相依性。 這可讓您只需變更或移除 CacheKeyDependency，即可明確地使快取失效。

**重要**事項：如果已啟用模擬，而且資料來源和/或資料內容的存取是以用戶端身分識別為基礎，建議您將 EnableCaching 設定為 False，以停用快取。 如果在此案例中啟用快取，而使用者不是原本要求資料發出要求的使用者，則不會強制執行資料來源的授權。 資料只會從快取中提供。

## <a name="the-sqldatasource-control"></a>SqlDataSource 控制項

SqlDataSource 控制項可讓開發人員存取儲存在支援 ADO.NET 之任何關係資料庫中的資料。 它可以使用 SqlClient 提供者來存取 SQL Server 資料庫、system.string 提供者、system.string 提供者，或 OracleClient 提供者，以存取 Oracle （data）。 因此，SqlDataSource 當然不只能用來存取 SQL Server 資料庫中的資料。

若要使用 SqlDataSource，您只需要提供 ConnectionString 屬性的值，並指定 SQL 命令或預存程式即可。 SqlDataSource 控制項會負責處理基礎 ADO.NET 架構。 它會開啟連接、查詢資料來源或執行預存程式、傳回資料，然後為您關閉連接。

> [!NOTE]
> 由於 DataSourceControl 類別會自動為您關閉連接，因此應該減少流失資料庫連接所產生的客戶呼叫數目。

下列程式碼片段會使用儲存在設定檔中的連接字串，將 DropDownList 控制項系結至 SqlDataSource 控制項，如上所示。

[!code-aspx[Main](data-source-controls/samples/sample3.aspx)]

如上圖所示，SqlDataSource 的 DataSourceMode 屬性會指定資料來源的模式。 在上述範例中，DataSourceMode 設定為 DataReader。 在此情況下，SqlDataSource 會使用順向和唯讀資料指標傳回 IDataReader 物件。 所傳回的指定物件類型是由所使用的提供者所控制。 在此情況下，我會使用 web.config 檔案的 &lt;connectionStrings&gt; 區段中所指定的 SqlClient 提供者。 因此，傳回的物件會是 SqlDataReader 類型。 藉由指定資料集的 DataSourceMode 值，資料可以儲存在伺服器上的資料集。 此模式可讓您新增排序、分頁等功能。如果我已將 SqlDataSource 資料系結至 GridView 控制項，我就選擇了資料集模式。 不過，在 DropDownList 的情況下，DataReader 模式是正確的選擇。

> [!NOTE]
> 當快取 SqlDataSource 或 AccessDataSource 時，DataSourceMode 屬性必須設定為 DataSet。 如果您啟用 DataSourceMode 為 DataReader 的快取，就會發生例外狀況。

## <a name="sqldatasource-properties"></a>SqlDataSource 屬性

以下是 SqlDataSource 控制項的一些屬性。

### <a name="cancelselectonnullparameter"></a>CancelSelectOnNullParameter

布林值，指定如果其中一個參數為 null 時，是否取消 select 命令。 預設為 true。

### <a name="conflictdetection"></a>ConflictDetection

在多個使用者可能同時更新資料來源的情況下，ConflictDetection 屬性會決定 SqlDataSource 控制項的行為。 這個屬性會評估為 ConflictOptions 列舉的其中一個值。 這些值為**CompareAllValues**和**OverwriteChanges**。 如果設定為 OverwriteChanges，則最後一個將資料寫入資料來源的人員會覆寫任何先前的變更。 不過，如果 ConflictDetection 屬性設定為 CompareAllValues，則會建立 SelectCommand 所傳回之資料行的參數，並使用參數來保存每個資料行中的原始值，讓 SqlDataSource 能夠判斷值是否已在執行 SelectCommand 後變更。

### <a name="deletecommand"></a>DeleteCommand

設定或取得從資料庫刪除資料列時所使用的 SQL 字串。 這可以是 SQL 查詢或預存程式名稱。

### <a name="deletecommandtype"></a>DeleteCommandType

設定或取得 delete 命令的類型，也就是 SQL 查詢（文字）或預存程式（StoredProcedure）。

### <a name="deleteparameters"></a>DeleteParameters

傳回與 SqlDataSource 控制項相關聯之 SqlDataSourceView 物件的 DeleteCommand 所使用的參數。

### <a name="oldvaluesparameterformatstring"></a>OldValuesParameterFormatString

當 ConflictDetection 屬性設定為 CompareAllValues 時，這個屬性會用來指定原始值參數的格式。 預設為 {0}，這表示原始值參數會採用與原始參數相同的名稱。 換句話說，如果功能變數名稱是「員工名稱」，則原始值參數會 @EmployeeID。

### <a name="selectcommand"></a>SelectCommand

設定或取得用來從資料庫中取出資料的 SQL 字串。 這可以是 SQL 查詢或預存程式名稱。

### <a name="selectcommandtype"></a>SelectCommandType

設定或取得 select 命令的類型，也就是 SQL 查詢（文字）或預存程式（StoredProcedure）。

### <a name="selectparameters"></a>SelectParameters

傳回與 SqlDataSource 控制項相關聯之 SqlDataSourceView 物件的 SelectCommand 所使用的參數。

### <a name="sortparametername"></a>SortParameterName

取得或設定預存程式參數的名稱，這是在排序資料來源控制項所抓取的資料時使用的。 只有當 SelectCommandType 設定為 StoredProcedure 時才有效。

### <a name="sqlcachedependency"></a>SqlCacheDependency

以分號分隔的字串，指定用於 SQL Server 快取相依性中的資料庫和資料表。 （稍後的課程模組中將會討論 SQL 快取相依性）。

### <a name="updatecommand"></a>UpdateCommand

設定或取得在更新資料庫中的資料時所使用的 SQL 字串。 這可以是 SQL 查詢或預存程式名稱。

### <a name="updatecommandtype"></a>UpdateCommandType

設定或取得 update 命令的類型，也就是 SQL 查詢（文字）或預存程式（StoredProcedure）。

### <a name="updateparameters"></a>UpdateParameters

傳回與 SqlDataSource 控制項相關聯之 SqlDataSourceView 物件的 UpdateCommand 所使用的參數。

## <a name="the-accessdatasource-control"></a>AccessDataSource 控制項

AccessDataSource 控制項會衍生自 SqlDataSource 類別，用來將資料系結至 Microsoft Access 資料庫。 AccessDataSource 控制項的 ConnectionString 屬性是唯讀屬性。 資料檔案屬性會用來指向 Access 資料庫，而不是使用 ConnectionString 屬性，如下所示。

[!code-aspx[Main](data-source-controls/samples/sample4.aspx)]

AccessDataSource 一律會將基底 SqlDataSource 的 ProviderName 設定為 System.object，並使用 Microsoft OLE DB 提供者連接到資料庫。 您無法使用 AccessDataSource 控制項連接到受密碼保護的 Access 資料庫。 如果您必須連接到受密碼保護的資料庫，您應該使用 SqlDataSource 控制項。

> [!NOTE]
> 儲存在網站內的 Access 資料庫應該放在應用程式\_資料目錄中。 ASP.NET 不允許流覽此目錄中的檔案。 使用 Access 資料庫時，您必須將應用程式的讀取和寫入權限授與給進程帳戶\_資料目錄。

## <a name="the-xmldatasource-control"></a>XmlDataSource 控制項

XmlDataSource 是用來將 XML 資料系結至資料繫結控制項。 您可以使用 [資料檔案] 屬性系結至 XML 檔案，也可以使用 Data 屬性系結至 XML 字串。 XmlDataSource 會將 XML 屬性公開為可系結欄位。 如果您需要系結至不是以屬性工作表示的值，就必須使用 XSL 轉換。 您也可以使用 XPath 運算式來篩選 XML 資料。

請考慮下列 XML 檔案：

[!code-xml[Main](data-source-controls/samples/sample5.xml)]

請注意，XmlDataSource 會使用*人員/人員*的 XPath 屬性，只篩選 &lt;Person&gt; 節點。 然後，DropDownList 會使用 DataTextField 屬性，將資料系結至 LastName 屬性。

雖然 XmlDataSource 控制項主要是用來將資料系結至唯讀的 XML 資料，但您還是可以編輯 XML 資料檔案。 請注意，在這種情況下，自動插入、更新及刪除 XML 檔案中的資訊，並不會因為它與其他資料來源控制項一樣自動進行。 相反地，您必須使用 XmlDataSource 控制項的下列方法，撰寫程式碼來手動編輯資料。

### <a name="getxmldocument"></a>GetXmlDocument

抓取包含 XmlDataSource 所抓取之 XML 程式碼的已承載物件。

### <a name="save"></a>儲存

將記憶體中的 Xml 儲存回資料來源。

請務必瞭解，只有在符合下列兩個條件時，Save 方法才會有效：

1. XmlDataSource 會使用 [資料檔案] 屬性來系結至 XML 檔案，而不是要系結至記憶體中 XML 資料的 [Data] 屬性。
2. 不會透過 Transform 或 TransformFile 屬性來指定轉換。

另請注意，當多位使用者同時呼叫 Save 方法時，可能會產生非預期的結果。

## <a name="the-objectdatasource-control"></a>ObjectDataSource 控制項

目前為止所涵蓋的資料來源控制項，是兩層式應用程式的絕佳選擇，其中資料來源控制項會直接與資料存放區進行通訊。 不過，許多真實世界的應用程式都是多層式應用程式，其中資料來源控制項可能需要與商務物件通訊，而後者又會與資料層通訊。 在這些情況下，ObjectDataSource 會適當地填滿帳單。 ObjectDataSource 會與來源物件搭配運作。 如果您的物件有實例方法，而不是靜態方法（在 Visual Basic 中共用），ObjectDataSource 控制項會建立來源物件的實例、呼叫指定的方法，以及處置該物件實例的所有範圍。 因此，您的物件必須是無狀態。 也就是說，您的物件應該在單一要求的範圍內取得並釋放所有必要的資源。 您可以藉由處理 ObjectDataSource 控制項的 ObjectCreating 事件來控制來源物件的建立方式。 您可以建立來源物件的實例，然後將 ObjectDataSourceEventArgs 類別的 ObjectInstance 屬性設定為該實例。 ObjectDataSource 控制項將會使用在 ObjectCreating 事件中建立的實例，而不是自行建立實例。

如果 ObjectDataSource 控制項的來源物件公開公用靜態方法（在 Visual Basic 中共用），可以呼叫這些方法來抓取和修改資料，則 ObjectDataSource 控制項會直接呼叫這些方法。 如果 ObjectDataSource 控制項必須建立來源物件的實例，才能進行方法呼叫，物件必須包含不接受任何參數的公用函式。 當 ObjectDataSource 控制項建立來源物件的新實例時，會呼叫這個函式。

如果來源物件未包含沒有參數的公用函式，您可以建立來源物件的實例，以供 ObjectCreating 事件中的 ObjectDataSource 控制項使用。

## <a name="specifying-object-methods"></a>指定物件方法

ObjectDataSource 控制項的來源物件可以包含用來選取、插入、更新或刪除資料的任意數目方法。 這些方法是由 ObjectDataSource 控制項根據方法的名稱來呼叫，如使用 ObjectDataSource 控制項的 SelectMethod、InsertMethod、UpdateMethod 或 DeleteMethod 屬性所識別。 來源物件也可以包含選擇性的 SelectCount 方法，此方法是由 ObjectDataSource 控制項使用 SelectCountMethod 屬性來識別，而此方法會傳回資料來源的物件總數計數。 ObjectDataSource 控制項會在呼叫了 Select 方法以取得資料來源中的記錄總數，以便在分頁時使用，以呼叫 SelectCount 方法。

## <a name="lab-using-data-source-controls"></a>使用資料來源控制項的實驗室

## <a name="exercise-1---displaying-data-with-the-sqldatasource-control"></a>練習 1-使用 SqlDataSource 控制項顯示資料

下列練習會使用 SqlDataSource 控制項來連接至 Northwind 資料庫。 它假設您可以存取 SQL Server 2000 實例上的 Northwind 資料庫。

1. 建立新的 ASP.NET 網站。
2. 新增 web.config 檔案。

    1. 以滑鼠右鍵按一下方案總管中的專案，然後按一下 [加入新專案]。
    2. 從範本清單中選擇 [Web 設定檔]，然後按一下 [新增]。
3. 編輯 &lt;connectionStrings&gt; 區段，如下所示： 

    [!code-aspx[Main](data-source-controls/samples/sample6.aspx)]
4. 切換至程式碼視圖，並將 ConnectionString 屬性和 SelectCommand 屬性新增至 &lt;asp： SqlDataSource&gt; 控制項，如下所示： 

    [!code-aspx[Main](data-source-controls/samples/sample7.aspx)]
5. 從設計檢視新增 GridView 控制項。
6. 從 [GridView 工作] 功能表的 [選擇資料來源] 下拉式清單中，選擇 [SqlDataSource1]。
7. 以滑鼠右鍵按一下 default.aspx，然後從功能表中選擇 [在瀏覽器中查看]。 當系統提示您儲存時，按一下 [是]。
8. GridView 會顯示 Products 資料表中的資料。

## <a name="exercise-2---editing-data-with-the-sqldatasource-control"></a>練習 2-使用 SqlDataSource 控制項編輯資料

下列練習示範如何使用宣告式語法來系結 DropDownList 控制項的資料，並可讓您編輯 DropDownList 控制項中顯示的資料。

1. 在設計檢視中，從 default.aspx 刪除 GridView 控制項。 

    **重要**：將 SqlDataSource 控制項保留在頁面上。
2. 將 DropDownList 控制項新增至 default.aspx。
3. 切換至來源視圖。
4. 將 DataSourceId、DataTextField 和 DataValueField 屬性新增至 &lt;asp： DropDownList&gt; 控制項，如下所示： 

    [!code-aspx[Main](data-source-controls/samples/sample8.aspx)]
5. 儲存 default.aspx，並在瀏覽器中查看。 請注意，DropDownList 包含 Northwind 資料庫中的所有產品。
6. 關閉瀏覽器。
7. 在 default.aspx 的來源視圖中，在 DropDownList 控制項下方新增 TextBox 控制項。 將文字方塊的 [ID] 屬性變更為 [txtProductName]。
8. 在 TextBox 控制項底下，加入新的按鈕控制項。 將按鈕的 [ID] 屬性變更為 [btnUpdate]，並將 [Text] 屬性變更為 [**更新產品名稱**]。
9. 在 default.aspx 的來源視圖中，將 UpdateCommand 屬性和兩個新 UpdateParameters 新增至 SqlDataSource 標記，如下所示： 

    [!code-aspx[Main](data-source-controls/samples/sample9.aspx)]

    > [!NOTE]
    > 請注意，此程式碼中已加入兩個更新參數（ProductName 和 ProductID）。 這些參數會對應至 [txtProductName] 文字方塊的 [Text] 屬性，以及 ddlProducts DropDownList 的 [SelectedValue] 屬性。
10. 切換至設計檢視，然後按兩下按鈕控制項加入事件處理常式。
11. 將下列程式碼新增至 btnUpdate\_按一下 [程式碼]： 

    [!code-csharp[Main](data-source-controls/samples/sample10.cs)]
12. 以滑鼠右鍵按一下 default.aspx，然後選擇在瀏覽器中進行查看。 出現提示時，按一下 [是] 以儲存所有變更。
13. ASP.NET 2.0 部分類別允許在執行時間進行編譯。 您不需要建立應用程式，就能看到程式碼變更生效。
14. 從 DropDownList 中選取產品。
15. 在文字方塊中輸入所選產品的新名稱，然後按一下 [更新] 按鈕。
16. 產品名稱會在資料庫中更新。

## <a name="exercise-3-using-the-objectdatasource-control"></a>使用 ObjectDataSource 控制項的練習3

此練習將示範如何使用 ObjectDataSource 控制項和來源物件，與 Northwind 資料庫互動。

1. 以滑鼠右鍵按一下方案總管中的專案，然後按一下 [加入新專案]。
2. 在 [範本] 清單中選取 [Web 表單]。 將 [名稱] 變更為 [default.aspx]，然後按一下 [新增]。
3. 以滑鼠右鍵按一下方案總管中的專案，然後按一下 [加入新專案]。
4. 在 [範本] 清單中選取 [類別]。 將類別的名稱變更為 NorthwindData.cs，然後按一下 [新增]。
5. 出現提示時，按一下 [是]，將類別新增至應用程式\_Code 資料夾。
6. 將下列程式碼新增至 NorthwindData.cs 檔案： 

    [!code-csharp[Main](data-source-controls/samples/sample11.cs)]
7. 將下列程式碼加入至物件 .aspx 的來源視圖： 

    [!code-aspx[Main](data-source-controls/samples/sample12.aspx)]
8. 儲存所有檔案並流覽物件 .aspx。
9. 藉由查看詳細資料、編輯員工、新增員工和刪除員工，來與介面互動。
