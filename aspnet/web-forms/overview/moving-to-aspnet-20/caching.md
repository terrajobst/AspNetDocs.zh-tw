---
uid: web-forms/overview/moving-to-aspnet-20/caching
title: 快取 |Microsoft Docs
author: microsoft
description: 瞭解快取對於執行良好的 ASP.NET 應用程式非常重要。 ASP.NET 1.x 提供三種不同的快取選項。輸出快取,。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 2bb109d2-e299-46ea-9054-fa0263b59165
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/caching
msc.type: authoredcontent
ms.openlocfilehash: 4f0b021ca6ca151544dd9fb0587ed9e0cf14ff65
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78575933"
---
# <a name="caching"></a>快取

由[Microsoft](https://github.com/microsoft)

> 瞭解快取對於執行良好的 ASP.NET 應用程式非常重要。 ASP.NET 1.x 提供三種不同的快取選項。輸出快取、片段快取和快取 API。

瞭解快取對於執行良好的 ASP.NET 應用程式非常重要。 ASP.NET 1.x 提供三種不同的快取選項。輸出快取、片段快取和快取 API。 ASP.NET 2.0 提供這三種方法，但它會新增一些重要的額外功能。 有數個新的快取相依性，而開發人員現在也可以選擇建立自訂快取相依性。 ASP.NET 2.0 也大幅改善了快取的設定。

## <a name="new-features"></a>新功能

## <a name="cache-profiles"></a>快取設定檔

快取設定檔可讓開發人員定義特定的快取設定，以套用至個別頁面。 例如，如果您有一些應該在12小時後從快取中過期的頁面，您可以輕鬆地建立可套用至這些頁面的快取設定檔。 若要新增新的快取設定檔，請使用設定檔中的 &lt;outputCacheSettings&gt; 區段。 例如，以下是名為*twoday*的快取設定檔設定，其會將快取期間設定為12小時。

[!code-xml[Main](caching/samples/sample1.xml)]

若要將此快取設定檔套用至特定頁面，請使用 @ OutputCache 指示詞的 CacheProfile 屬性，如下所示：

[!code-aspx[Main](caching/samples/sample2.aspx)]

## <a name="custom-cache-dependencies"></a>自訂快取相依性

ASP.NET 1.x 開發人員完成自訂快取相依性。 在 ASP.NET 1.x 中，CacheDependency 類別是密封的，可防止開發人員從其中衍生自己的類別。 在 ASP.NET 2.0 中，已移除這項限制，開發人員可以免費開發自己的自訂快取相依性。 CacheDependency 類別可讓您根據檔案、目錄或快取金鑰來建立自訂快取相依性。

例如，下列程式碼會根據名為 config.xml 的檔案（位於 Web 應用程式的根目錄中），建立新的自訂快取相依性：

[!code-csharp[Main](caching/samples/sample3.cs)]

在此案例中，當 config.xml 檔案變更時，快取的專案會失效。

您也可以使用快取索引鍵來建立自訂快取相依性。 使用此方法時，移除快取索引鍵會使快取的資料失效。 下面這個範例可說明這點：

[!code-csharp[Main](caching/samples/sample4.cs)]

若要使上面所插入的專案失效，只要移除插入快取中的專案以作為快取索引鍵。

[!code-csharp[Main](caching/samples/sample5.cs)]

請注意，做為快取索引鍵之專案的索引鍵必須與新增至快取索引鍵陣列的值相同。

## <a name="polling-based-sql-cache-dependenciesalso-called-table-based-dependencies"></a>以輪詢為基礎的 SQL 快取相依性（也稱為以資料表為基礎的相依性）

SQL Server 7 和2000針對 SQL 快取相依性使用以輪詢為基礎的模型。 以輪詢為基礎的模型會在資料庫資料表上使用觸發程式，這會在資料表中的資料變更時觸發。 該觸發程式會更新通知資料表中 ASP.NET 定期檢查的**changeId**欄位。 如果**changeId**欄位已更新，ASP.NET 會知道資料已變更，而且會使快取的資料失效。

> [!NOTE]
> SQL Server 2005 也可以使用以輪詢為基礎的模型，但因為輪詢式模型不是最有效率的模型，所以建議使用以查詢為基礎的模型（稍後會討論）與 SQL Server 2005。

為了讓 SQL 快取相依性使用以輪詢為基礎的模型正常運作，資料表必須啟用通知。 您可以使用 SqlCacheDependencyAdmin 類別，或使用 aspnet\_regsql，以程式設計方式完成這項作業。

下列命令列會針對 SQL 快取相依性，在名為*dbase*的 SQL Server 實例上註冊 Northwind 資料庫中的 Products 資料表。

[!code-console[Main](caching/samples/sample6.cmd)]

以下是上述命令中使用之命令列參數的說明：

| **命令列參數** | **目的** |
| --- | --- |
| -S *server* | 指定伺服器名稱。 |
| -ed | 指定應該啟用 SQL 快取相依性的資料庫。 |
| -d*資料庫\_名稱* | 指定應該針對 SQL 快取相依性啟用的資料庫名稱。 |
| -E | 指定在連接到資料庫時，aspnet\_regsql 應該使用 Windows 驗證。 |
| -et | 指定我們要啟用 SQL 快取相依性的資料庫資料表。 |
| -t*資料表\_名稱* | 指定要啟用 SQL 快取相依性的資料庫資料表名稱。 |

> [!NOTE]
> 還有其他適用于 aspnet\_regsql 的參數。 如需完整清單，請執行 aspnet\_regsql-？ 從命令列。

當此命令執行時，會對 SQL Server 資料庫進行下列變更：

- 新增**AspNet\_SqlCacheTablesForChangeNotification**資料表。 此資料表針對資料庫中已啟用 SQL 快取相依性的每個資料表，各包含一個資料列。
- 下列預存程式會建立在資料庫內：

| AspNet\_SqlCachePollingStoredProcedure | 查詢 AspNet\_SqlCacheTablesForChangeNotification 資料表，並傳回針對 SQL 快取相依性啟用的所有資料表，以及每個資料表的 changeId 值。 這個預存程式用於輪詢，以判斷資料是否已變更。 |
| --- | --- |
| AspNet\_SqlCacheQueryRegisteredTablesStoredProcedure | 藉由查詢 AspNet\_SqlCacheTablesForChangeNotification 資料表並傳回針對 SQL 快取相依性啟用的所有資料表，傳回針對 SQL 快取相依性啟用的所有資料表。 |
| AspNet\_SqlCacheRegisterTableStoredProcedure | 藉由在通知資料表中新增必要的專案並新增觸發程式，註冊 SQL 快取相依性的資料表。 |
| AspNet\_SqlCacheUnRegisterTableStoredProcedure | 移除通知資料表中的專案並移除觸發程式，以取消註冊 SQL 快取相依性的資料表。 |
| AspNet\_SqlCacheUpdateChangeIdStoredProcedure | 藉由遞增已變更資料表的 changeId 來更新通知資料表。 ASP.NET 會使用此值來判斷資料是否已變更。 如下所示，這個預存程式是由啟用資料表時所建立的觸發程式執行。 |

- 針對資料表建立名為 **_table\_Name_\_AspNet\_SqlCacheNotification\_觸發**程式的 SQL Server 觸發程式。 在資料表上執行 INSERT、UPDATE 或 DELETE 時，此觸發程式會執行 AspNet\_SqlCacheUpdateChangeIdStoredProcedure。
- 名為**aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess**的 SQL Server 角色會新增至資料庫。

**Aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess** SQL Server 角色具有 Aspnet\_SQLCACHEPOLLINGSTOREDPROCEDURE 的 EXEC 許可權。 為了讓輪詢模型能夠正常運作，您必須將您的處理帳戶新增至 aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess 角色。 Aspnet\_regsql 工具不會為您執行此動作。

### <a name="configuring-polling-based-sql-cache-dependencies"></a>設定以輪詢為基礎的 SQL 快取相依性

設定以輪詢為基礎的 SQL 快取相依性時，需要執行幾個步驟。 第一個步驟是啟用資料庫和資料表，如上所述。 完成該步驟之後，設定的其餘部分如下所示：

- 正在設定 ASP.NET 設定檔。
- 設定 SqlCacheDependency

### <a name="configuring-the-aspnet-configuration-file"></a>正在設定 ASP.NET 設定檔

除了新增先前課程模組中所討論的連接字串之外，您還必須使用 &lt;sqlCacheDependency&gt; 元素來設定 &lt;快取&gt; 元素，如下所示：

[!code-xml[Main](caching/samples/sample7.xml)]

這項設定會啟用*pubs*資料庫的 SQL 快取相依性。 請注意，&lt;sqlCacheDependency&gt; 元素中的 pollTime 屬性預設為60000毫秒或1分鐘。 （此值不能小於500毫秒）。在此範例中，&lt;新增&gt; 元素會新增新的資料庫，並覆寫 pollTime，並將它設定為9000000毫秒。

#### <a name="configuring-the-sqlcachedependency"></a>設定 SqlCacheDependency

下一個步驟是設定 SqlCacheDependency。 完成這項工作的最簡單方式是在 @ Outcache 指示詞中指定 SqlDependency 屬性的值，如下所示：

[!code-aspx[Main](caching/samples/sample8.aspx)]

在上述 @ OutputCache 指示詞中，會針對*pubs*資料庫中的*作者*資料表設定 SQL 快取相依性。 可以設定多個相依性，方法是以分號分隔，如下所示：

[!code-aspx[Main](caching/samples/sample9.aspx)]

設定 SqlCacheDependency 的另一種方法是以程式設計方式執行這項操作。 下列程式碼會在*pubs*資料庫的*作者*資料表上建立新的 SQL 快取相依性。

[!code-csharp[Main](caching/samples/sample10.cs)]

以程式設計方式定義 SQL 快取相依性的其中一個優點，就是您可以處理可能發生的任何例外狀況。 例如，如果您嘗試為尚未啟用通知的資料庫定義 SQL 快取相依性，則會擲回**system.web.caching.databasenotenabledfornotificationexception**例外狀況。 在這種情況下，您可以呼叫**SqlCacheDependencyAdmin. EnableNotifications**方法，並將資料庫名稱傳遞給它，藉此嘗試啟用資料庫的通知。

同樣地，如果您嘗試針對尚未啟用通知的資料表定義 SQL 快取相依性，則會擲回**system.web.caching.tablenotenabledfornotificationexception** 。 接著，您可以呼叫**SqlCacheDependencyAdmin. EnableTableForNotifications**方法，將資料庫名稱和資料表名稱傳遞給它。

下列程式碼範例說明如何在設定 SQL 快取相依性時，適當地設定例外狀況處理。

[!code-csharp[Main](caching/samples/sample11.cs)]

詳細資訊： [https://msdn.microsoft.com/library/t9x04ed2.aspx](https://msdn.microsoft.com/library/t9x04ed2.aspx)

## <a name="query-based-sql-cache-dependencies-sql-server-2005-only"></a>以查詢為基礎的 SQL 快取相依性（僅限 SQL Server 2005）

針對 SQL 快取相依性使用 SQL Server 2005 時，不需要以輪詢為基礎的模型。 搭配 SQL Server 2005 使用時，SQL 快取相依性會直接透過 SQL 連線與 SQL Server 實例進行通訊（不需要進一步設定）使用 SQL Server 2005 查詢通知。

啟用查詢式通知最簡單的方式，就是將資料來源物件的**SqlCacheDependency**屬性設定為**CommandNotification** ，並將**EnableCaching**屬性設定為**true**，以宣告方式執行此動作。 使用此方法時，不需要任何程式碼。 如果針對資料來源執行之命令的結果變更，將會使快取資料失效。

下列範例會設定 SQL 快取相依性的資料來源控制項：

[!code-aspx[Main](caching/samples/sample12.aspx)]

在此情況下，如果**SelectCommand**中指定的查詢傳回的結果與原先的不同，則快取的結果會無效。

您也可以將 **@ OutputCache**指示詞的**SqlDependency**屬性設定為**COMMANDNOTIFICATION**，以指定啟用 SQL 快取相依性的所有資料來源。 下列範例說明這種情況。

[!code-aspx[Main](caching/samples/sample13.aspx)]

> [!NOTE]
> 如需 SQL Server 2005 中查詢通知的詳細資訊，請參閱 SQL Server 線上叢書。

設定以查詢為基礎之 SQL 快取相依性的另一種方法是使用 SqlCacheDependency 類別，以程式設計方式來執行這項操作。 下列程式碼範例將說明如何完成這項作業。

[!code-csharp[Main](caching/samples/sample14.cs)]

詳細資訊： [https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp](https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp)

## <a name="post-cache-substitution"></a>快取後的替代

快取頁面可能會大幅增加 Web 應用程式的效能。 不過，在某些情況下，您需要快取大部分的頁面，而頁面中的某些片段則是動態的。 例如，如果您建立的新聞故事頁面在設定的時段內完全是靜態的，您可以設定要快取的整個頁面。 如果您想要包含在每個頁面要求上變更的輪替廣告橫幅，則包含廣告的頁面部分必須是動態的。 若要讓您快取頁面，但動態取代某些內容，您可以使用 ASP.NET 快取後的替代。 在快取後的替換之後，整個頁面會以標示為豁免快取的特定部分來快取輸出。 在廣告橫幅的範例中，AdRotator 控制項可讓您利用快取後的替代功能，以動態方式為每個使用者和每個頁面重新整理建立廣告。

有三種方式可執行快取後的替代：

- 以宣告方式使用替代控制項。
- 以程式設計方式使用替代控制項 API。
- 隱含地使用 AdRotator 控制項。

### <a name="substitution-control"></a>替代控制項

ASP.NET 替代控制項會指定動態建立的快取頁面區段，而不是快取。 您可以將替代控制項放在頁面上您想要顯示動態內容的位置。 在執行時間，替代控制項會呼叫您以 [方法名稱] 屬性指定的方法。 方法必須傳回字串，然後取代替代控制項的內容。 方法必須是包含頁面或 UserControl 控制項的靜態方法。 使用替代控制項會導致用戶端的可快取性變更為伺服器的可快取性，因此不會在用戶端上快取該頁面。 這可確保對頁面的未來要求再次呼叫方法，以產生動態內容。

### <a name="substitution-api"></a>替代 API

若要以程式設計方式建立快取頁面的動態內容，您可以在頁面程式碼中呼叫[WriteSubstitution](https://msdn.microsoft.com/library/system.web.httpresponse.writesubstitution.aspx)方法，並將方法的名稱當做參數傳遞給它。 處理動態內容建立的方法會採用單一[HttpCoNtext](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)參數，並傳回字串。 傳回字串是將在指定位置取代的內容。 呼叫 WriteSubstitution 方法而不是以宣告方式使用替代控制項的優點是，您可以呼叫任何任意物件的方法，而不是呼叫頁面或 UserControl 物件的靜態方法。

呼叫 WriteSubstitution 方法會導致用戶端的可快取性變更為伺服器的可快取性，因此不會在用戶端上快取該頁面。 這可確保對頁面的未來要求再次呼叫方法，以產生動態內容。

### <a name="adrotator-control"></a>AdRotator 控制項

AdRotator 伺服器控制項會在內部執行快取後替代的支援。 如果您在頁面上放置 AdRotator 控制項，它會在每個要求上轉譯唯一的廣告，而不論是否快取父頁面。 因此，包含 AdRotator 控制項的頁面只會快取伺服器端。

## <a name="controlcachepolicy-class"></a>ControlCachePolicy 類別

ControlCachePolicy 類別可讓您使用使用者控制項，以程式設計方式控制片段快取。 ASP.NET 會將使用者控制項內嵌在[BasePartialCachingControl](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.aspx)實例內。 BasePartialCachingControl 類別代表已啟用輸出快取的使用者控制項。

當您存取[PartialCachingControl](https://msdn.microsoft.com/library/system.web.ui.partialcachingcontrol.aspx)控制項的[BasePartialCachingControl. CachePolicy](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.cachepolicy.aspx)屬性時，一律會收到有效的 ControlCachePolicy 物件。 不過，如果您存取[usercontrol](https://msdn.microsoft.com/library/system.web.ui.usercontrol.aspx)控制項的[CachePolicy](https://msdn.microsoft.com/library/system.web.ui.usercontrol.cachepolicy.aspx)屬性，只有在 BasePartialCachingControl 控制項已包裝使用者控制項時，才會收到有效的 ControlCachePolicy 物件。 如果未包裝，屬性所傳回的 ControlCachePolicy 物件將會在您嘗試操作它時擲回例外狀況，因為它沒有相關聯的 BasePartialCachingControl。 若要判斷 UserControl 實例是否支援快取，而不會產生例外狀況，請檢查[SupportsCaching](https://msdn.microsoft.com/library/system.web.ui.controlcachepolicy.supportscaching.aspx)屬性。

使用 ControlCachePolicy 類別是您可以啟用輸出快取的數種方式之一。 下列清單說明可用來啟用輸出快取的方法：

- 使用[@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx)指示詞，在宣告式案例中啟用輸出快取。
- 您可以使用[PartialCachingAttribute](https://msdn.microsoft.com/library/system.web.ui.partialcachingattribute.aspx)屬性，在程式碼後置檔案中啟用使用者控制項的快取。
- 在程式設計的案例中，使用 ControlCachePolicy 類別來指定快取設定，而這些實例是使用先前的其中一個方法，並使用[TemplateControl](https://msdn.microsoft.com/library/system.web.ui.templatecontrol.loadcontrol.aspx)以動態方式載入的已啟用快取功能的 BasePartialCachingControl 實例。

ControlCachePolicy 實例只能在控制項生命週期的 Init 和可呈現階段之間成功操作。 如果您在預先呈現的階段之後修改 ControlCachePolicy 物件，ASP.NET 會擲回例外狀況，因為在轉譯控制項之後所做的任何變更，都無法實際影響快取設定（在轉譯階段會快取控制項）。 最後，使用者控制項實例（也就是它的 ControlCachePolicy 物件）只有在實際呈現時，才可供程式設計操作之用。

## <a name="changes-to-caching-configuration---the-ltcachinggt-element"></a>快取設定的變更-&lt;快取&gt; 元素

ASP.NET 2.0 中的快取設定有幾項變更。 &lt;快取&gt; 元素是 ASP.NET 2.0 中的新功能，可讓您在設定檔中進行快取設定變更。 下列是可用的屬性。

| **目** | **說明** |
| --- | --- |
| **高速** | 選擇性項目。 定義全域應用程式快取設定。 |
| **outputCache** | 選擇性項目。 指定應用程式範圍的輸出快取設定。 |
| **outputCacheSettings** | 選擇性項目。 指定可套用至應用程式中頁面的輸出快取設定。 |
| **sqlCacheDependency** | 選擇性項目。 設定 ASP.NET 應用程式的 SQL 快取相依性。 |

### <a name="the-ltcachegt-element"></a>&lt;cache&gt; 元素

&lt;cache&gt; 元素中提供下列屬性：

| **屬性** | **說明** |
| --- | --- |
| **disableMemoryCollection** | 選擇性 **Boolean** 屬性。 取得或設定值，指出是否停用電腦處於記憶體不足壓力時所發生的快取記憶體集合。 |
| **disableExpiration** | 選擇性 **Boolean** 屬性。 取得或設定值，指出是否停用快取到期時間。 停用時，快取的專案不會過期，而且過期快取專案的背景清除也不會發生。 |
| **privateBytesLimit** | 選擇性的**Int64**屬性。 取得或設定值，指出在快取開始排清過期的專案並嘗試回收記憶體之前，應用程式的私用位元組大小上限。 這項限制包括快取所使用的記憶體，以及執行中應用程式的一般記憶體額外負荷。 設定為零表示 ASP.NET 會使用自己的啟發學習法來判斷何時開始回收記憶體。 |
| **percentagePhysicalMemoryUsedLimit** | 選擇性的**Int32**屬性。 取得或設定值，指出應用程式在快取開始排清過期專案並嘗試回收記憶體之前可使用的電腦實體記憶體百分比上限。此記憶體使用量同時包含快取所使用的記憶體當做執行中應用程式的一般記憶體使用量。 設定為零表示 ASP.NET 會使用自己的啟發學習法來判斷何時開始回收記憶體。 |
| **privateBytesPollTime** | 選擇性的**TimeSpan**屬性。 取得或設定值，指出輪詢應用程式的私用位元組記憶體使用量之間的時間間隔。 |

### <a name="the-ltoutputcachegt-element"></a>&lt;outputCache&gt; 元素

下列屬性適用于 &lt;outputCache&gt; 元素。

|       <strong>屬性</strong>        |                                                                                                                                                                                                                                                       <strong>說明</strong>                                                                                                                                                                                                                                                       |
|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   <strong>enableOutputCache</strong>    |                                                                                                                                                          選擇性 <strong>Boolean</strong> 屬性。 啟用/停用頁面輸出快取。 如果停用，不論程式設計或宣告式設定為何，都不會快取任何頁面。 預設值為 true。                                                                                                                                                           |
|  <strong>enableFragmentCache</strong>   |                                                選擇性 <strong>Boolean</strong> 屬性。 啟用/停用應用程式片段快取。 如果停用，不論使用的是[@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx)指示詞或快取設定檔，都不會快取任何頁面。 包含快取控制標頭，指出上游 proxy 伺服器和瀏覽器用戶端不應該嘗試快取頁面輸出。 預設值為 <strong>false</strong>。                                                 |
| <strong>sendCacheControlHeader</strong> |                                                                                                                                                      選擇性 <strong>Boolean</strong> 屬性。 取得或設定值，指出快取<strong>控制項：私</strong>用標頭是否依預設由輸出快取模組傳送。 預設值為 <strong>false</strong>。                                                                                                                                                      |
|      <strong>omitVaryStar</strong>      | 選擇性 <strong>Boolean</strong> 屬性。 啟用/停用在回應中傳送 Http "<strong>Vary： \</strong ><em>" 標頭的功能。預設設定為 [false</em>] 時，會針對輸出快取的頁面傳送 "* Vary： \*<strong>" 標頭。傳送 Vary 標頭時，會根據 Vary 標頭中指定的內容，允許快取不同的版本。例如，[<em>差異]：使用者代理程式</em>會根據發出要求的使用者代理程式，儲存不同版本的頁面。預設值為 * * false</strong>。 |

### <a name="the-ltoutputcachesettingsgt-element"></a>&lt;outputCacheSettings&gt; 元素

&lt;outputCacheSettings&gt; 元素允許依照先前所述的方式建立快取設定檔。 &lt;outputCacheSettings&gt; 元素的唯一子項目是用於設定快取設定檔的 &lt;outputCacheProfiles&gt; 專案。

### <a name="the-ltsqlcachedependencygt-element"></a>&lt;sqlCacheDependency&gt; 元素

下列屬性適用于 &lt;sqlCacheDependency&gt; 元素。

| **屬性** | **說明** |
| --- | --- |
| **後** | 必要的**布林值**屬性。 指出是否正在輪詢變更。 |
| **pollTime** | 選擇性的**Int32**屬性。 設定 SqlCacheDependency 輪詢資料庫資料表是否有變更的頻率。 這個值會對應到連續 pollings 之間的毫秒數。 不能設定為小於500毫秒。 預設值為1分鐘。 |

### <a name="more-information"></a>詳細資訊

關於快取設定，還有一些您應該注意的額外資訊。

- 如果未設定背景工作進程的私用位元組限制，快取將會使用下列其中一項限制： 

    - x86 2GB：800MB 或60% 的實體 RAM，以較少者為准
    - x86 3GB：1800MB 或60% 的實體 RAM，以較少者為准
    - x64： 1 tb 或60% 的實體 RAM，以較少者為准
- 如果同時設定了工作者進程私用位元組限制和 &lt;快取 privateBytesLimit/&gt;，快取將會使用兩者的最小值。
- 就像1.x，我們會捨棄快取專案並呼叫 GC。收集的原因有兩個： 

    - 我們非常接近私用位元組限制
    - 可用的記憶體接近或小於10%
- 您可以將 &lt;cache percentagePhysicalMemoryUseLimit/&gt; 設定為100，以有效地停用記憶體不足的 trim 和快取。
- 與1.x 不同的是，2.0 會暫止修剪，並在最後一個 GC 時收集呼叫。Collect 不會減少私用位元組或受控堆積的大小，超過1% 的（快取）記憶體限制。

## <a name="lab1-custom-cache-dependencies"></a>Lab1：自訂快取相依性

1. 建立新網站。
2. 新增名為 cache .xml 的 XML 檔案，並將它儲存至 Web 應用程式的根目錄。
3. 在 default.aspx 的程式碼後置中，將下列程式碼新增至頁面\_載入方法： 

    [!code-csharp[Main](caching/samples/sample15.cs)]
4. 將下列內容新增至原始檔視圖中的 default.aspx 頂端： 

    [!code-aspx[Main](caching/samples/sample16.aspx)]
5. 流覽 default.aspx。 這段時間的意思是什麼？
6. 重新整理瀏覽器。 這段時間的意思是什麼？
7. 開啟 cache .xml 並新增下列程式碼： 

    [!code-xml[Main](caching/samples/sample17.xml)]
8. 儲存 cache .xml。
9. 重新整理瀏覽器。 這段時間的意思是什麼？
10. 說明更新時間的原因，而不是顯示先前快取的值：

## <a name="lab-2-using-polling-based-cache-dependencies"></a>實驗室2：使用以輪詢為基礎的快取相依性

這個實驗室會使用您在上一個課程模組中建立的專案，允許透過 GridView 和 DetailsView 控制項編輯 Northwind 資料庫中的資料。

1. 在 Visual Studio 2005 中開啟專案。
2. 針對 Northwind 資料庫執行 aspnet\_regsql 公用程式，以啟用資料庫和 Products 資料表。 從 Visual Studio 命令提示字元中使用下列命令： 

    [!code-console[Main](caching/samples/sample18.cmd)]
3. 將下列內容新增至您的 web.config 檔案： 

    [!code-xml[Main](caching/samples/sample19.xml)]
4. 加入名為 showdata 的新 webform。
5. 將下列 @ outputcache 指示詞新增至 showdata 頁面： 

    [!code-aspx[Main](caching/samples/sample20.aspx)]
6. 將下列程式碼加入至頁面\_載入 showdata： 

    [!code-html[Main](caching/samples/sample21.html)]
7. 將新的 SqlDataSource 控制項加入至 showdata，並將它設定為使用 Northwind 資料庫連接。 按 [下一步]。
8. 選取 [ProductName 和 ProductID] 核取方塊，然後按 [下一步]。
9. 按一下 [完成]。
10. 在 [showdata] 頁面中新增 GridView。
11. 從下拉式清單中選擇 [SqlDataSource1]。
12. 儲存並流覽 showdata。 請記下顯示的時間。
