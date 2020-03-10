---
uid: web-forms/overview/data-access/caching-data/caching-data-in-the-architecture-cs
title: 在架構中快取資料C#（） |Microsoft Docs
author: rick-anderson
description: 在上一個教學課程中，我們已瞭解如何在展示層套用快取。 在本教學課程中，我們將學習如何利用我們的分層 architectu 。
ms.author: riande
ms.date: 05/30/2007
ms.assetid: d29a7c41-0628-4a23-9dfc-bfea9c6c1054
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-in-the-architecture-cs
msc.type: authoredcontent
ms.openlocfilehash: 192cadb8e2f862ac2a97a36b375e247b281ece93
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78551167"
---
# <a name="caching-data-in-the-architecture-c"></a>在架構中快取資料 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_59_CS.exe)或[下載 PDF](caching-data-in-the-architecture-cs/_static/datatutorial59cs1.pdf)

> 在上一個教學課程中，我們已瞭解如何在展示層套用快取。 在本教學課程中，我們將學習如何利用我們的多層式架構，在商務邏輯層快取資料。 我們藉由擴充架構以包含快取層來完成這項操作。

## <a name="introduction"></a>簡介

如我們在先前的教學課程中所見，快取 ObjectDataSource 的資料就像設定幾個屬性一樣簡單。 可惜的是，ObjectDataSource 會在展示層套用快取，這會將快取原則與 ASP.NET 網頁緊密耦合。 建立多層式架構的其中一個原因是允許中斷這類聯繫性。 例如，商務邏輯層會將商務邏輯與 ASP.NET 網頁分開，而資料存取層則會將資料存取的細節分離。 這種分離商務邏輯和資料存取的細節是個比較好的部分，因為它可讓系統更容易閱讀、更容易維護，而且更有彈性地進行變更。 它也可讓開發人員在展示層上進行領域知識和部門的工作，而不需要熟悉資料庫的詳細資料，就能完成工作。 將快取原則與展示層分離，可提供類似的優點。

在本教學課程中，我們將擴充我們的架構，以包含採用我們的快取原則的快取*層*（或簡稱 CL）。 快取層會包含一個 `ProductsCL` 類別，可讓您使用 `GetProducts()`、`GetProductsByCategoryID(categoryID)`等方法來存取產品資訊，而叫用時，會先嘗試從快取取得資料。 如果快取是空的，這些方法會在 BLL 中叫用適當的 `ProductsBLL` 方法，進而從 DAL 取得資料。 `ProductsCL` 方法會快取從 BLL 抓取的資料，然後再將它傳回。

如 [圖 1] 所示，CL 位於簡報和商務邏輯層之間。

![Caching 層（CL）是我們架構中的另一層](caching-data-in-the-architecture-cs/_static/image1.png)

**圖 1**： Caching 層（CL）是我們架構中的另一層

## <a name="step-1-creating-the-caching-layer-classes"></a>步驟1：建立快取層類別

在本教學課程中，我們將建立一個非常簡單的 CL，其中有一個只有少數方法的單一類別 `ProductsCL`。 為整個應用程式建立完整的快取層，需要建立 `CategoriesCL`、`EmployeesCL`和 `SuppliersCL` 類別，並針對 BLL 中的每個資料存取或修改方法，在這些快取層類別中提供方法。 如同 BLL 和 DAL，快取層應該最好實作為個別的類別庫專案;不過，我們會將它實作為 [`App_Code`] 資料夾中的類別。

為了更清楚地區分 CL 類別與 DAL 和 BLL 類別，讓 s 在 `App_Code` 資料夾中建立新的子資料夾。 以滑鼠右鍵按一下 方案總管中的 `App_Code` 資料夾，選擇 新增資料夾，然後將新資料夾命名為 `CL`。 建立此資料夾之後，請將名為 `ProductsCL.cs`的新類別新增至其中。

![新增名為 CL 的新資料夾和名為 ProductsCL.cs 的類別](caching-data-in-the-architecture-cs/_static/image2.png)

**圖 2**：新增名為 `CL` 的新資料夾，以及名為 `ProductsCL.cs` 的類別

`ProductsCL` 類別應該包含一組相同的資料存取和修改方法，如同在其對應的商務邏輯層級（`ProductsBLL`）中找到。 我們不會建立所有這些方法，而是只在這裡建立幾個，以瞭解 CL 所使用的模式。 特別的是，我們會在步驟3中新增 `GetProducts()` 和 `GetProductsByCategoryID(categoryID)` 方法，並在步驟4中加入 `UpdateProduct` 多載。 您可以在休閒中新增其餘的 `ProductsCL` 方法和 `CategoriesCL`、`EmployeesCL`和 `SuppliersCL` 類別。

## <a name="step-2-reading-and-writing-to-the-data-cache"></a>步驟2：讀取和寫入資料快取

在上一個教學課程中探索的 ObjectDataSource 快取功能會在內部使用 ASP.NET 資料快取，來儲存從 BLL 取得的資料。 您也可以從 ASP.NET 網頁的程式碼後置類別，或從 web 應用程式架構中的類別，以程式設計方式存取資料快取。 若要從 ASP.NET 網頁的程式碼後置類別讀取及寫入資料快取，請使用下列模式：

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample1.cs)]

[`Cache` 類別](https://msdn.microsoft.com/library/system.web.caching.cache.aspx)的[`Insert` 方法](https://msdn.microsoft.com/library/system.web.caching.cache.insert.aspx)有數個多載。 `Cache["key"] = value` 和 `Cache.Insert(key, value)` 是同義的，而且會使用指定的索引鍵將專案新增至快取，但不含已定義的到期。 一般來說，我們想要在將專案新增至快取時，指定到期時間、以時間為基礎的到期日，或兩者都是。 使用其中一個 `Insert` 方法的多載，以提供相依性或以時間為基礎的到期資訊。

快取層的方法必須先檢查要求的資料是否在快取中，如果是，則從該處傳回它。 如果要求的資料不在快取中，則必須叫用適當的 BLL 方法。 它的傳回值應該快取然後傳回，如下列順序圖所示。

![快取層方法會傳回快取中的資料（如果有的話）](caching-data-in-the-architecture-cs/_static/image3.png)

**圖 3**：快取層的方法會從快取傳回資料（如果有的話）

[圖 3] 中所描述的順序是使用下列模式在 CL 類別中完成：

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample2.cs)]

在這裡， *type*是儲存在快取 `Northwind.ProductsDataTable`中的資料類型，例如， *key*是唯一識別快取專案的索引鍵。 如果具有指定之索引*鍵*的專案不在快取中，則會 `null`*實例*，而且會從適當的 BLL 方法抓取資料，並將其新增至快取。 當達到 `return instance` 時，*實例*會包含資料的參考，不論是從快取或從 BLL 提取。

從快取存取資料時，請務必使用上述模式。 下列模式（第一眼）看起來相當於，其中包含引進競爭條件的細微差異。 競爭情況很容易進行調試，因為它們會偶爾顯示，而且很容易重現。

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample3.cs)]

在此秒中，不正確的程式碼片段的差異在於，不會將快取專案的參考儲存在本機變數中，而是直接在條件陳述式*和*`return`中存取資料快取。 假設到達此程式碼時，`Cache["key"]` 不`null`，但在到達 `return` 語句之前，系統會從快取中收回索引*鍵*。 在這種罕見的情況下，程式碼會傳回 `null` 值，而不是預期類型的物件。

> [!NOTE]
> 資料快取是安全線程，因此您不需要同步處理簡單讀取或寫入的執行緒存取。 不過，如果您需要對快取中需要不可部分完成的資料執行多項作業，您必須負責實行鎖定或一些其他機制，以確保執行緒安全性。 如需詳細資訊，請參閱[同步存取 ASP.NET Cache](http://www.ddj.com/184406369) 。

您可以使用[`Remove` 方法](https://msdn.microsoft.com/library/system.web.caching.cache.remove.aspx)，以程式設計方式從資料快取中收回專案，如下所示：

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample4.cs)]

## <a name="step-3-returning-product-information-from-theproductsclclass"></a>步驟3：從`ProductsCL`類別傳回產品資訊

在本教學課程中，我們會執行兩個方法，以從 `ProductsCL` 類別傳回產品資訊： `GetProducts()` 和 `GetProductsByCategoryID(categoryID)`。 如同商務邏輯層中的 `ProductsBL` 類別，CL 中的 `GetProducts()` 方法會傳回所有產品的相關資訊做為 `Northwind.ProductsDataTable` 物件，而 `GetProductsByCategoryID(categoryID)` 會從指定的分類傳回所有產品。

下列程式碼顯示 `ProductsCL` 類別中的部分方法：

[!code-vb[Main](caching-data-in-the-architecture-cs/samples/sample5.vb)]

首先，請注意套用至類別和方法的 `DataObject` 和 `DataObjectMethodAttribute` 屬性。 這些屬性會將資訊提供給 ObjectDataSource s wizard，指出應該在 wizard s 步驟中顯示的類別和方法。 因為 CL 類別和方法會從展示層中的 ObjectDataSource 存取，所以我新增了這些屬性，以增強設計階段體驗。 如需這些屬性及其效果的完整描述，請參閱[建立商務邏輯層](../introduction/creating-a-business-logic-layer-cs.md)教學課程。

在 `GetProducts()` 和 `GetProductsByCategoryID(categoryID)` 方法中，從 `GetCacheItem(key)` 方法傳回的資料會指派給本機變數。 `GetCacheItem(key)` 方法（我們將在稍後檢查）會根據指定的索引*鍵*傳回快取中的特定專案。 如果在快取中找不到這類資料，則會從對應的 `ProductsBLL` 類別方法中抓取，然後使用 `AddCacheItem(key, value)` 方法將其新增至快取。

`GetCacheItem(key)` 和 `AddCacheItem(key, value)` 方法會分別使用資料快取、讀取和寫入值的介面。 `GetCacheItem(key)` 方法是兩者中較簡單的方法。 它只會使用傳入的索引*鍵*傳回 Cache 類別的值：

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample6.cs)]

`GetCacheItem(key)` 不會使用提供的索引*鍵值*，而是會呼叫 `GetCacheKey(key)` 方法，這會傳回前面加上 ProductsCache-的索引*鍵*。 `AddCacheItem(key, value)` 方法也會使用 `MasterCacheKeyArray`（保存字串 ProductsCache），如我們稍後所見。

從 ASP.NET 網頁的程式碼後置類別中，您可以使用 `Page` 類別[`Cache` 屬性](https://msdn.microsoft.com/library/system.web.ui.page.cache.aspx)來存取資料快取，並允許如步驟2中所述的語法，如 `Cache["key"] = value`。 從架構中的類別，您可以使用 `HttpRuntime.Cache` 或 `HttpContext.Current.Cache`來存取資料快取。 [Peter Johnson](https://weblogs.asp.net/pjohnson/default.aspx)的 Blog 專案[HttpRuntime. 快取與 HttpCoNtext](https://weblogs.asp.net/pjohnson/httpruntime-cache-vs-httpcontext-current-cache) 。快取注意使用 `HttpRuntime` 而不是 `HttpContext.Current`時的輕微效能優勢。因此，`ProductsCL` 會使用 `HttpRuntime`。

> [!NOTE]
> 如果您的架構是使用類別庫專案來執行，則您將需要加入 `System.Web` 元件的參考，才能使用[HttpRuntime](https://msdn.microsoft.com/library/system.web.httpruntime.aspx)和[HttpCoNtext](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)類別。

如果在快取中找不到此專案，則 `ProductsCL` 類別的方法會從 BLL 取得資料，並使用 `AddCacheItem(key, value)` 方法將其加入至快取。 若要將*值*新增至快取，我們可以使用下列程式碼，其使用60秒的到期時間：

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample7.cs)]

`DateTime.Now.AddSeconds(CacheDuration)` 會指定未來的以時間為基礎的到期60秒，而[`System.Web.Caching.Cache.NoSlidingExpiration`](https://msdn.microsoft.com/library/system.web.caching.cache.noslidingexpiration(vs.80).aspx)則表示沒有任何滑動到期日。 雖然這個 `Insert` 方法多載具有絕對和滑動到期的輸入參數，但是您只能提供這兩個的其中一個。 如果您嘗試同時指定絕對時間和時間範圍，`Insert` 方法將會擲回 `ArgumentException` 例外狀況。

> [!NOTE]
> 這項 `AddCacheItem(key, value)` 方法的執行目前有一些缺點。 我們會在步驟4中解決這些問題，並加以解決。

## <a name="step-4-invalidating-the-cache-when-the-data-is-modified-through-the-architecture"></a>步驟4：透過架構修改資料時，將快取失效

除了資料抓取方法，快取層也必須提供與 BLL 相關的方法，以插入、更新和刪除資料。 CL s 資料修改方法不會修改快取的資料，而是會呼叫 BLL 的對應資料修改方法，然後讓快取失效。 如我們在先前的教學課程中所見，這與 ObjectDataSource 在啟用快取功能並叫用其 `Insert`、`Update`或 `Delete` 方法時所套用的行為相同。

下列 `UpdateProduct` 多載說明如何在 CL 中執行資料修改方法：

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample8.cs)]

會叫用適當的資料修改商務邏輯層方法，但在傳回其回應之前，我們需要讓快取失效。 可惜的是，將快取設為無效，因為 `ProductsCL` 類別 `GetProducts()` 和 `GetProductsByCategoryID(categoryID)` 方法都會使用不同的索引鍵將專案新增至快取，而 `GetProductsByCategoryID(categoryID)` 方法會為每個唯一的*類別*類型新增不同的快取專案。

當您使快取失效時，我們必須移除 `ProductsCL` 類別可能已加入的*所有*專案。 這可以藉由將快取相依性與在 `AddCacheItem(key, value)` 方法中新增至快取的每個專案產生*關聯，來*完成這項作業。 一般而言，快取相依性可以是快取中的另一個專案、檔案系統上的檔案，或是來自 Microsoft SQL Server 資料庫的資料。 當相依性變更或從快取中移除時，與它相關聯的快取專案會自動從快取中收回。 在本教學課程中，我們想要在快取中建立額外的專案，做為透過 `ProductsCL` 類別新增之所有專案的快取相依性。 如此一來，只要移除快取相依性，就可以從快取中移除所有這些專案。

讓 s 更新 `AddCacheItem(key, value)` 方法，讓透過這個方法新增至快取的每個專案都與單一快取相依性相關聯：

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample9.cs)]

`MasterCacheKeyArray` 是保存單一值（ProductsCache）的字串陣列。 首先，快取專案會新增至快取，並指派目前的日期和時間。 如果快取專案已經存在，就會更新。 接下來，會建立快取相依性。 [`CacheDependency` 類別](https://msdn.microsoft.com/library/system.web.caching.cachedependency(VS.80).aspx)的函式有許多多載，但此處使用的多載需要兩個 `string` 陣列輸入。 第一個會指定要當做相依性使用的一組檔案。 由於我們不想要使用任何檔案型相依性，因此第一個輸入參數會使用 `null` 的值。 第二個輸入參數會指定要當做相依性使用的一組快取索引鍵。 在這裡，我們會指定單一相依性，`MasterCacheKeyArray`。 然後，`CacheDependency` 會傳遞至 `Insert` 方法。

透過這項修改來 `AddCacheItem(key, value)`，invaliding 快取就像移除相依性一樣簡單。

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample10.cs)]

## <a name="step-5-calling-the-caching-layer-from-the-presentation-layer"></a>步驟5：從展示層呼叫快取層

快取層級的類別和方法可以使用我們在這些教學課程中所檢查的技術來處理資料。 若要說明如何使用快取的資料，請將變更儲存至 `ProductsCL` 類別，然後在 [`Caching`] 資料夾中開啟 [`FromTheArchitecture.aspx`] 頁面，並加入 GridView。 從 GridView 的智慧標籤，建立新的 ObjectDataSource。 在 wizard 的第一個步驟中，您應該會看到 `ProductsCL` 類別，做為下拉式清單中的其中一個選項。

[![ProductsCL 類別包含在 [商務物件] 下拉式清單中](caching-data-in-the-architecture-cs/_static/image5.png)](caching-data-in-the-architecture-cs/_static/image4.png)

**圖 4**： [`ProductsCL`] 類別包含在 [商務物件] 下拉式清單中（[按一下以查看完整大小的影像](caching-data-in-the-architecture-cs/_static/image6.png)）

選取 `ProductsCL`之後，按 [下一步]。 [選取] 索引標籤中的下拉式清單有兩個專案-`GetProducts()` 和 `GetProductsByCategoryID(categoryID)` 而且 [更新] 索引標籤具有唯一的 `UpdateProduct` 多載。 從 更新 索引標籤的 選取 索引標籤和 `UpdateProducts` 方法選擇 `GetProducts()` 方法，然後按一下 完成

[![ProductsCL 類別 s 方法列于下拉式清單中](caching-data-in-the-architecture-cs/_static/image8.png)](caching-data-in-the-architecture-cs/_static/image7.png)

**圖 5**： `ProductsCL` 類別 s 的方法會列在下拉式清單中（[按一下以查看完整大小的影像](caching-data-in-the-architecture-cs/_static/image9.png)）

完成 wizard 之後，Visual Studio 會將 ObjectDataSource 的 `OldValuesParameterFormatString` 屬性設定為 `original_{0}`，並將適當的欄位新增至 GridView。 將 `OldValuesParameterFormatString` 屬性變更回其預設值 `{0}`，然後將 GridView 設定為支援分頁、排序和編輯。 由於 CL 使用的 `UploadProducts` 多載只會接受已編輯的產品名稱和價格，因此限制 GridView 只能編輯這些欄位。

在先前的教學課程中，我們定義了 GridView 以包含 `ProductName`、`CategoryName`和 `UnitPrice` 欄位的欄位。 您可以隨意複寫此格式和結構，在這種情況下，GridView 和 ObjectDataSource 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](caching-data-in-the-architecture-cs/samples/sample11.aspx)]

此時，我們有一個使用快取層的頁面。 若要查看作用中的快取，請在 `ProductsCL` 類別 s `GetProducts()` 和 `UpdateProduct` 方法中設定中斷點。 請造訪瀏覽器中的頁面，並在排序和分頁時逐步執行程式碼，以便查看從快取中提取的資料。 然後更新記錄，並記下快取已失效，因此當資料重新系結至 GridView 時，就會從 BLL 抓取該快取。

> [!NOTE]
> 本文隨附的下載中所提供的快取層並未完成。 它只包含一個類別，`ProductsCL`，只運動幾個方法。 此外，只有單一的 ASP.NET 網頁會使用 CL （`~/Caching/FromTheArchitecture.aspx`），其他人仍會直接參考 BLL。 如果您打算在應用程式中使用 CL，展示層的所有呼叫都應該移至 CL，這會要求 CL 類別和方法涵蓋展示層目前所使用之 BLL 中的類別和方法。

## <a name="summary"></a>總結

雖然可以使用 ASP.NET 2.0 s SqlDataSource 和 ObjectDataSource 控制項在展示層套用快取，但最好的快取責任會委派給架構中的個別層。 在本教學課程中，我們建立了位於展示層和商務邏輯層之間的快取層。 快取層必須提供存在於 BLL 中的一組相同類別和方法，並從展示層呼叫。

我們在此探討的快取層範例，而先前的教學課程呈現了*被動的載入*。 使用被動式載入時，只有在提出資料的要求，且快取中遺漏資料時，才會將資料載入快取中。 資料也可以*主動載入*至快取中，這是在實際需要資料之前，將資料載入快取的技術。 在下一個教學課程中，我們會看到當我們查看如何在應用程式啟動時將靜態值儲存至快取中的主動式載入範例。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Teresa Murph。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](caching-data-with-the-objectdatasource-cs.md)
> [下一頁](caching-data-at-application-startup-cs.md)
