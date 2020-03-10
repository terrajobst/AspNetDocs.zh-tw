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
# <a name="data-source-controls"></a><span data-ttu-id="4730d-104">資料來源控制項</span><span class="sxs-lookup"><span data-stu-id="4730d-104">Data Source Controls</span></span>

<span data-ttu-id="4730d-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="4730d-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="4730d-106">ASP.NET 1.x 中的 DataGrid 控制項在 Web 應用程式中標記為數據存取的絕佳改進。</span><span class="sxs-lookup"><span data-stu-id="4730d-106">The DataGrid control in ASP.NET 1.x marked a great improvement in data access in Web applications.</span></span> <span data-ttu-id="4730d-107">不過，它並不是方便使用者使用。</span><span class="sxs-lookup"><span data-stu-id="4730d-107">However, it wasn't as user-friendly as it could have been.</span></span> <span data-ttu-id="4730d-108">它仍然需要大量的程式碼，才能從它取得很有用的功能。</span><span class="sxs-lookup"><span data-stu-id="4730d-108">It still required a considerable amount of code to obtain much useful functionality from it.</span></span> <span data-ttu-id="4730d-109">這就是所有資料存取在1.x 中的模式。</span><span class="sxs-lookup"><span data-stu-id="4730d-109">Such is the model in all data access endeavors in 1.x.</span></span>

<span data-ttu-id="4730d-110">ASP.NET 1.x 中的 DataGrid 控制項在 Web 應用程式中標記為數據存取的絕佳改進。</span><span class="sxs-lookup"><span data-stu-id="4730d-110">The DataGrid control in ASP.NET 1.x marked a great improvement in data access in Web applications.</span></span> <span data-ttu-id="4730d-111">不過，它並不是方便使用者使用。</span><span class="sxs-lookup"><span data-stu-id="4730d-111">However, it wasn't as user-friendly as it could have been.</span></span> <span data-ttu-id="4730d-112">它仍然需要大量的程式碼，才能從它取得很有用的功能。</span><span class="sxs-lookup"><span data-stu-id="4730d-112">It still required a considerable amount of code to obtain much useful functionality from it.</span></span> <span data-ttu-id="4730d-113">這就是所有資料存取在1.x 中的模式。</span><span class="sxs-lookup"><span data-stu-id="4730d-113">Such is the model in all data access endeavors in 1.x.</span></span>

<span data-ttu-id="4730d-114">ASP.NET 2.0 使用資料來源控制項來解決這種情況。</span><span class="sxs-lookup"><span data-stu-id="4730d-114">ASP.NET 2.0 addresses this with in part with data source controls.</span></span> <span data-ttu-id="4730d-115">ASP.NET 2.0 中的資料來源控制項為開發人員提供了宣告式模型，可供您用來抓取資料、顯示資料和編輯資料。</span><span class="sxs-lookup"><span data-stu-id="4730d-115">The data source controls in ASP.NET 2.0 provide developers with a declarative model for retrieving data, displaying data, and editing data.</span></span> <span data-ttu-id="4730d-116">資料來源控制項的目的是要提供一致的資料標記法給資料繫結控制項，而不論這些資料的來源為何。</span><span class="sxs-lookup"><span data-stu-id="4730d-116">The purpose of data source controls is to provide a consistent representation of data to data-bound controls regardless of the source of those data.</span></span> <span data-ttu-id="4730d-117">ASP.NET 2.0 中資料來源控制項的核心是 DataSourceControl 抽象類別。</span><span class="sxs-lookup"><span data-stu-id="4730d-117">At the heart of the data source controls in ASP.NET 2.0 is the DataSourceControl abstract class.</span></span> <span data-ttu-id="4730d-118">DataSourceControl 類別提供 IDataSource 介面和 IListSource 介面的基底實作為，後者可讓您將資料來源控制項指派為資料繫結控制項的 DataSource （透過新的 DataSourceId 屬性）稍後會討論），並將其中的資料公開為清單。</span><span class="sxs-lookup"><span data-stu-id="4730d-118">The DataSourceControl class provides a base implementation of the IDataSource interface and the IListSource interface, the latter of which allows you to assign the data source control as the DataSource of a data-bound control (via the new DataSourceId property discussed later) and expose the data therein as a list.</span></span> <span data-ttu-id="4730d-119">資料來源控制項中的每個資料清單都會公開為 DataSourceView 物件。</span><span class="sxs-lookup"><span data-stu-id="4730d-119">Each list of data from a data source control is exposed as a DataSourceView object.</span></span> <span data-ttu-id="4730d-120">對 DataSourceView 實例的存取是由 IDataSource 介面提供。</span><span class="sxs-lookup"><span data-stu-id="4730d-120">Access to the DataSourceView instances is provided by the IDataSource interface.</span></span> <span data-ttu-id="4730d-121">例如，GetViewNames 方法會傳回 ICollection，讓您列舉與特定資料來源控制項相關聯的 DataSourceViews，而 GetView 方法可讓您依名稱存取特定的 DataSourceView 實例。</span><span class="sxs-lookup"><span data-stu-id="4730d-121">For example, the GetViewNames method returns an ICollection that allows you to enumerate the DataSourceViews associated with a particular data source control, and the GetView method allows you to access a particular DataSourceView instance by name.</span></span>

<span data-ttu-id="4730d-122">資料來源控制項沒有使用者介面。</span><span class="sxs-lookup"><span data-stu-id="4730d-122">Data source controls have no user-interface.</span></span> <span data-ttu-id="4730d-123">它們會實作為伺服器控制項，讓它們可以支援宣告式語法，並在需要時能夠存取頁面狀態。</span><span class="sxs-lookup"><span data-stu-id="4730d-123">They are implemented as server controls so that they can support declarative syntax and so that they have access to page state if desired.</span></span> <span data-ttu-id="4730d-124">資料來源控制項不會將任何 HTML 標籤呈現給用戶端。</span><span class="sxs-lookup"><span data-stu-id="4730d-124">Data source controls do not render any HTML markup to the client.</span></span>

> [!NOTE]
> <span data-ttu-id="4730d-125">如您稍後所見，使用資料來源控制項也會取得快取的優點。</span><span class="sxs-lookup"><span data-stu-id="4730d-125">As you'll see later, there are also caching benefits obtained by using data source controls.</span></span>

## <a name="storing-connection-strings"></a><span data-ttu-id="4730d-126">儲存連接字串</span><span class="sxs-lookup"><span data-stu-id="4730d-126">Storing Connection Strings</span></span>

<span data-ttu-id="4730d-127">在我們開始探討如何設定資料來源控制項之前，我們應該先討論 ASP.NET 2.0 中有關連接字串的新功能。</span><span class="sxs-lookup"><span data-stu-id="4730d-127">Before we get into looking at how to configure data source controls, we should cover a new capability in ASP.NET 2.0 concerning connection strings.</span></span> <span data-ttu-id="4730d-128">ASP.NET 2.0 引進了設定檔案中的新區段，可讓您輕鬆地儲存可在執行時間動態讀取的連接字串。</span><span class="sxs-lookup"><span data-stu-id="4730d-128">ASP.NET 2.0 introduces a new section in the configuration file that allows you to easily store connection strings that can be read dynamically at runtime.</span></span> <span data-ttu-id="4730d-129">&lt;connectionStrings&gt; 區段可讓您輕鬆地儲存連接字串。</span><span class="sxs-lookup"><span data-stu-id="4730d-129">The &lt;connectionStrings&gt; section makes it easy to store connection strings.</span></span>

<span data-ttu-id="4730d-130">下列程式碼片段會加入新的連接字串。</span><span class="sxs-lookup"><span data-stu-id="4730d-130">The snippet below adds a new connection string.</span></span>

[!code-xml[Main](data-source-controls/samples/sample1.xml)]

> [!NOTE]
> <span data-ttu-id="4730d-131">就如同 &lt;appSettings&gt; 區段，&lt;connectionStrings&gt; 區段會出現在設定檔中 &lt;system.web&gt; 區段之外。</span><span class="sxs-lookup"><span data-stu-id="4730d-131">Just as with the &lt;appSettings&gt; section, the &lt;connectionStrings&gt; section appears outside of the &lt;system.web&gt; section in the configuration file.</span></span>

<span data-ttu-id="4730d-132">若要使用這個連接字串，您可以在設定伺服器控制項的 ConnectionString 屬性時，使用下列語法。</span><span class="sxs-lookup"><span data-stu-id="4730d-132">To use this connection string, you can use the following syntax when setting the ConnectionString attribute of a server control.</span></span>

[!code-aspx[Main](data-source-controls/samples/sample2.aspx)]

<span data-ttu-id="4730d-133">&lt;connectionStrings&gt; 區段也可以加密，如此就不會公開機密資訊。</span><span class="sxs-lookup"><span data-stu-id="4730d-133">The &lt;connectionStrings&gt; section can also be encrypted so that sensitive information is not exposed.</span></span> <span data-ttu-id="4730d-134">這項功能將會在稍後的課程模組中討論。</span><span class="sxs-lookup"><span data-stu-id="4730d-134">That ability will be covered in a later module.</span></span>

## <a name="caching-data-sources"></a><span data-ttu-id="4730d-135">快取資料來源</span><span class="sxs-lookup"><span data-stu-id="4730d-135">Caching Data Sources</span></span>

<span data-ttu-id="4730d-136">每個 DataSourceControl 都會提供四個屬性來設定快取;EnableCaching、CacheDuration、CacheExpirationPolicy 和 CacheKeyDependency。</span><span class="sxs-lookup"><span data-stu-id="4730d-136">Each DataSourceControl provides four properties for configuring caching; EnableCaching, CacheDuration, CacheExpirationPolicy, and CacheKeyDependency.</span></span>

## <a name="enablecaching"></a><span data-ttu-id="4730d-137">EnableCaching</span><span class="sxs-lookup"><span data-stu-id="4730d-137">EnableCaching</span></span>

<span data-ttu-id="4730d-138">EnableCaching 是布林值屬性，可決定是否啟用資料來源控制項的快取。</span><span class="sxs-lookup"><span data-stu-id="4730d-138">EnableCaching is a Boolean property that determines whether or not caching is enabled for the data source control.</span></span>

## <a name="cacheduration-property"></a><span data-ttu-id="4730d-139">CacheDuration 屬性</span><span class="sxs-lookup"><span data-stu-id="4730d-139">CacheDuration Property</span></span>

<span data-ttu-id="4730d-140">CacheDuration 屬性會設定快取保持有效的秒數。</span><span class="sxs-lookup"><span data-stu-id="4730d-140">The CacheDuration property sets the number of seconds that the cache remains valid.</span></span> <span data-ttu-id="4730d-141">將此屬性設定為**0**會使快取保持有效，直到明確失效為止。</span><span class="sxs-lookup"><span data-stu-id="4730d-141">Setting this property to **0** causes the cache to remain valid until explicitly invalidated.</span></span>

## <a name="cacheexpirationpolicy-property"></a><span data-ttu-id="4730d-142">CacheExpirationPolicy 屬性</span><span class="sxs-lookup"><span data-stu-id="4730d-142">CacheExpirationPolicy Property</span></span>

<span data-ttu-id="4730d-143">CacheExpirationPolicy 屬性可以設定為 [**絕對**] 或 [**滑動**]。</span><span class="sxs-lookup"><span data-stu-id="4730d-143">The CacheExpirationPolicy property can be set to either **Absolute** or **Sliding**.</span></span> <span data-ttu-id="4730d-144">將它設定為 [絕對] 表示資料快取的最大時間量是 CacheDuration 屬性所指定的秒數。</span><span class="sxs-lookup"><span data-stu-id="4730d-144">Setting it to Absolute means that the maximum amount of time that the data will be cached is the number of seconds specified by the CacheDuration property.</span></span> <span data-ttu-id="4730d-145">藉由將它設定為滑動，每次執行作業時，就會重設到期時間。</span><span class="sxs-lookup"><span data-stu-id="4730d-145">By setting it to Sliding, the expiration time is reset when each operation is performed.</span></span>

## <a name="cachekeydependency-property"></a><span data-ttu-id="4730d-146">CacheKeyDependency 屬性</span><span class="sxs-lookup"><span data-stu-id="4730d-146">CacheKeyDependency Property</span></span>

<span data-ttu-id="4730d-147">如果為 CacheKeyDependency 屬性指定了字串值，ASP.NET 將會根據該字串來設定新的快取相依性。</span><span class="sxs-lookup"><span data-stu-id="4730d-147">If a string value is specified for the CacheKeyDependency property, ASP.NET will set up a new cache dependency based on that string.</span></span> <span data-ttu-id="4730d-148">這可讓您只需變更或移除 CacheKeyDependency，即可明確地使快取失效。</span><span class="sxs-lookup"><span data-stu-id="4730d-148">This allows you to explicitly invalidate the cache by simply changing or removing the CacheKeyDependency.</span></span>

<span data-ttu-id="4730d-149">**重要**事項：如果已啟用模擬，而且資料來源和/或資料內容的存取是以用戶端身分識別為基礎，建議您將 EnableCaching 設定為 False，以停用快取。</span><span class="sxs-lookup"><span data-stu-id="4730d-149">**Important**: If impersonation is enabled and access to the data source and/or content of data are based upon client identity, it is recommended that caching be disabled by setting EnableCaching to False.</span></span> <span data-ttu-id="4730d-150">如果在此案例中啟用快取，而使用者不是原本要求資料發出要求的使用者，則不會強制執行資料來源的授權。</span><span class="sxs-lookup"><span data-stu-id="4730d-150">If caching is enabled in this scenario and a user other than the user who originally requested the data issues a request, authorization to the data source is not enforced.</span></span> <span data-ttu-id="4730d-151">資料只會從快取中提供。</span><span class="sxs-lookup"><span data-stu-id="4730d-151">The data will simply be served from cache.</span></span>

## <a name="the-sqldatasource-control"></a><span data-ttu-id="4730d-152">SqlDataSource 控制項</span><span class="sxs-lookup"><span data-stu-id="4730d-152">The SqlDataSource Control</span></span>

<span data-ttu-id="4730d-153">SqlDataSource 控制項可讓開發人員存取儲存在支援 ADO.NET 之任何關係資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="4730d-153">The SqlDataSource control allows a developer to access data stored in any relational database that supports ADO.NET.</span></span> <span data-ttu-id="4730d-154">它可以使用 SqlClient 提供者來存取 SQL Server 資料庫、system.string 提供者、system.string 提供者，或 OracleClient 提供者，以存取 Oracle （data）。</span><span class="sxs-lookup"><span data-stu-id="4730d-154">It can use the System.Data.SqlClient provider to access a SQL Server database, the System.Data.OleDb provider, the System.Data.Odbc provider, or the System.Data.OracleClient provider to access Oracle.</span></span> <span data-ttu-id="4730d-155">因此，SqlDataSource 當然不只能用來存取 SQL Server 資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="4730d-155">Therefore, the SqlDataSource is certainly not only used for accessing data in a SQL Server database.</span></span>

<span data-ttu-id="4730d-156">若要使用 SqlDataSource，您只需要提供 ConnectionString 屬性的值，並指定 SQL 命令或預存程式即可。</span><span class="sxs-lookup"><span data-stu-id="4730d-156">In order to use the SqlDataSource, you simply provide a value for the ConnectionString property and specify a SQL command or stored procedure.</span></span> <span data-ttu-id="4730d-157">SqlDataSource 控制項會負責處理基礎 ADO.NET 架構。</span><span class="sxs-lookup"><span data-stu-id="4730d-157">The SqlDataSource control takes care of working with the underlying ADO.NET architecture.</span></span> <span data-ttu-id="4730d-158">它會開啟連接、查詢資料來源或執行預存程式、傳回資料，然後為您關閉連接。</span><span class="sxs-lookup"><span data-stu-id="4730d-158">It opens the connection, queries the data source or executes the stored procedure, returns the data, and then closes the connection for you.</span></span>

> [!NOTE]
> <span data-ttu-id="4730d-159">由於 DataSourceControl 類別會自動為您關閉連接，因此應該減少流失資料庫連接所產生的客戶呼叫數目。</span><span class="sxs-lookup"><span data-stu-id="4730d-159">Because the DataSourceControl class automatically closes the connection for you, it should reduce the number of customer calls generated by leaking database connections.</span></span>

<span data-ttu-id="4730d-160">下列程式碼片段會使用儲存在設定檔中的連接字串，將 DropDownList 控制項系結至 SqlDataSource 控制項，如上所示。</span><span class="sxs-lookup"><span data-stu-id="4730d-160">The code snippet below binds a DropDownList control to a SqlDataSource control using the connection string that is stored in the configuration file as shown above.</span></span>

[!code-aspx[Main](data-source-controls/samples/sample3.aspx)]

<span data-ttu-id="4730d-161">如上圖所示，SqlDataSource 的 DataSourceMode 屬性會指定資料來源的模式。</span><span class="sxs-lookup"><span data-stu-id="4730d-161">As illustrated above, the DataSourceMode property of the SqlDataSource specifies the mode for the data source.</span></span> <span data-ttu-id="4730d-162">在上述範例中，DataSourceMode 設定為 DataReader。</span><span class="sxs-lookup"><span data-stu-id="4730d-162">In the example above, the DataSourceMode is set to DataReader.</span></span> <span data-ttu-id="4730d-163">在此情況下，SqlDataSource 會使用順向和唯讀資料指標傳回 IDataReader 物件。</span><span class="sxs-lookup"><span data-stu-id="4730d-163">In that case, the SqlDataSource will return an IDataReader object using a forward-only and read-only cursor.</span></span> <span data-ttu-id="4730d-164">所傳回的指定物件類型是由所使用的提供者所控制。</span><span class="sxs-lookup"><span data-stu-id="4730d-164">The specified type of object that is returned is controlled by the provider that is used.</span></span> <span data-ttu-id="4730d-165">在此情況下，我會使用 web.config 檔案的 &lt;connectionStrings&gt; 區段中所指定的 SqlClient 提供者。</span><span class="sxs-lookup"><span data-stu-id="4730d-165">In this case, I'm using the System.Data.SqlClient provider as specified in the &lt;connectionStrings&gt; section of the web.config file.</span></span> <span data-ttu-id="4730d-166">因此，傳回的物件會是 SqlDataReader 類型。</span><span class="sxs-lookup"><span data-stu-id="4730d-166">Therefore, the object that is returned will be of type SqlDataReader.</span></span> <span data-ttu-id="4730d-167">藉由指定資料集的 DataSourceMode 值，資料可以儲存在伺服器上的資料集。</span><span class="sxs-lookup"><span data-stu-id="4730d-167">By specifying a DataSourceMode value of DataSet, the data can be stored in a DataSet on the server.</span></span> <span data-ttu-id="4730d-168">此模式可讓您新增排序、分頁等功能。如果我已將 SqlDataSource 資料系結至 GridView 控制項，我就選擇了資料集模式。</span><span class="sxs-lookup"><span data-stu-id="4730d-168">This mode allows you to add features such as sorting, paging, etc. If I had been data-binding the SqlDataSource to a GridView control, I would have chosen the DataSet mode.</span></span> <span data-ttu-id="4730d-169">不過，在 DropDownList 的情況下，DataReader 模式是正確的選擇。</span><span class="sxs-lookup"><span data-stu-id="4730d-169">However, in the case of a DropDownList, the DataReader mode is the correct choice.</span></span>

> [!NOTE]
> <span data-ttu-id="4730d-170">當快取 SqlDataSource 或 AccessDataSource 時，DataSourceMode 屬性必須設定為 DataSet。</span><span class="sxs-lookup"><span data-stu-id="4730d-170">When caching a SqlDataSource or an AccessDataSource, the DataSourceMode property must be set to DataSet.</span></span> <span data-ttu-id="4730d-171">如果您啟用 DataSourceMode 為 DataReader 的快取，就會發生例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4730d-171">An exception will occur if you enable caching with a DataSourceMode of DataReader.</span></span>

## <a name="sqldatasource-properties"></a><span data-ttu-id="4730d-172">SqlDataSource 屬性</span><span class="sxs-lookup"><span data-stu-id="4730d-172">SqlDataSource Properties</span></span>

<span data-ttu-id="4730d-173">以下是 SqlDataSource 控制項的一些屬性。</span><span class="sxs-lookup"><span data-stu-id="4730d-173">The following are some of the properties of the SqlDataSource control.</span></span>

### <a name="cancelselectonnullparameter"></a><span data-ttu-id="4730d-174">CancelSelectOnNullParameter</span><span class="sxs-lookup"><span data-stu-id="4730d-174">CancelSelectOnNullParameter</span></span>

<span data-ttu-id="4730d-175">布林值，指定如果其中一個參數為 null 時，是否取消 select 命令。</span><span class="sxs-lookup"><span data-stu-id="4730d-175">A Boolean value that specifies whether a select command is canceled if one of the parameters is null.</span></span> <span data-ttu-id="4730d-176">預設為 true。</span><span class="sxs-lookup"><span data-stu-id="4730d-176">True by default.</span></span>

### <a name="conflictdetection"></a><span data-ttu-id="4730d-177">ConflictDetection</span><span class="sxs-lookup"><span data-stu-id="4730d-177">ConflictDetection</span></span>

<span data-ttu-id="4730d-178">在多個使用者可能同時更新資料來源的情況下，ConflictDetection 屬性會決定 SqlDataSource 控制項的行為。</span><span class="sxs-lookup"><span data-stu-id="4730d-178">In a situation where multiple users may be updating a data source at the same time, the ConflictDetection property determines the behavior of the SqlDataSource control.</span></span> <span data-ttu-id="4730d-179">這個屬性會評估為 ConflictOptions 列舉的其中一個值。</span><span class="sxs-lookup"><span data-stu-id="4730d-179">This property evaluates to one of the values of the ConflictOptions enumeration.</span></span> <span data-ttu-id="4730d-180">這些值為**CompareAllValues**和**OverwriteChanges**。</span><span class="sxs-lookup"><span data-stu-id="4730d-180">Those values are **CompareAllValues** and **OverwriteChanges**.</span></span> <span data-ttu-id="4730d-181">如果設定為 OverwriteChanges，則最後一個將資料寫入資料來源的人員會覆寫任何先前的變更。</span><span class="sxs-lookup"><span data-stu-id="4730d-181">If set to OverwriteChanges, the last person to write data to the data source overwrites any previous changes.</span></span> <span data-ttu-id="4730d-182">不過，如果 ConflictDetection 屬性設定為 CompareAllValues，則會建立 SelectCommand 所傳回之資料行的參數，並使用參數來保存每個資料行中的原始值，讓 SqlDataSource 能夠判斷值是否已在執行 SelectCommand 後變更。</span><span class="sxs-lookup"><span data-stu-id="4730d-182">However, if the ConflictDetection property is set to CompareAllValues, parameters get created for the columns returned by the SelectCommand and parameters are also created to hold the original values in each of those columns allowing the SqlDataSource to determine whether or not the values have changed since the SelectCommand was executed.</span></span>

### <a name="deletecommand"></a><span data-ttu-id="4730d-183">DeleteCommand</span><span class="sxs-lookup"><span data-stu-id="4730d-183">DeleteCommand</span></span>

<span data-ttu-id="4730d-184">設定或取得從資料庫刪除資料列時所使用的 SQL 字串。</span><span class="sxs-lookup"><span data-stu-id="4730d-184">Sets or gets the SQL string used when deleting rows from the database.</span></span> <span data-ttu-id="4730d-185">這可以是 SQL 查詢或預存程式名稱。</span><span class="sxs-lookup"><span data-stu-id="4730d-185">This can either be a SQL query or a stored procedure name.</span></span>

### <a name="deletecommandtype"></a><span data-ttu-id="4730d-186">DeleteCommandType</span><span class="sxs-lookup"><span data-stu-id="4730d-186">DeleteCommandType</span></span>

<span data-ttu-id="4730d-187">設定或取得 delete 命令的類型，也就是 SQL 查詢（文字）或預存程式（StoredProcedure）。</span><span class="sxs-lookup"><span data-stu-id="4730d-187">Sets or gets the type of delete command, either a SQL query (Text) or a stored procedure (StoredProcedure).</span></span>

### <a name="deleteparameters"></a><span data-ttu-id="4730d-188">DeleteParameters</span><span class="sxs-lookup"><span data-stu-id="4730d-188">DeleteParameters</span></span>

<span data-ttu-id="4730d-189">傳回與 SqlDataSource 控制項相關聯之 SqlDataSourceView 物件的 DeleteCommand 所使用的參數。</span><span class="sxs-lookup"><span data-stu-id="4730d-189">Returns the parameters that are used by the DeleteCommand of the SqlDataSourceView object associated with the SqlDataSource control.</span></span>

### <a name="oldvaluesparameterformatstring"></a><span data-ttu-id="4730d-190">OldValuesParameterFormatString</span><span class="sxs-lookup"><span data-stu-id="4730d-190">OldValuesParameterFormatString</span></span>

<span data-ttu-id="4730d-191">當 ConflictDetection 屬性設定為 CompareAllValues 時，這個屬性會用來指定原始值參數的格式。</span><span class="sxs-lookup"><span data-stu-id="4730d-191">This property is used to specify the format of the original value parameters in cases where the ConflictDetection property is set to CompareAllValues.</span></span> <span data-ttu-id="4730d-192">預設為 {0}，這表示原始值參數會採用與原始參數相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="4730d-192">The default is {0} which means that original value parameters will take the same name as the original parameter.</span></span> <span data-ttu-id="4730d-193">換句話說，如果功能變數名稱是「員工名稱」，則原始值參數會 @EmployeeID。</span><span class="sxs-lookup"><span data-stu-id="4730d-193">In other words, if the field name is EmployeeID, the original value parameter would be @EmployeeID.</span></span>

### <a name="selectcommand"></a><span data-ttu-id="4730d-194">SelectCommand</span><span class="sxs-lookup"><span data-stu-id="4730d-194">SelectCommand</span></span>

<span data-ttu-id="4730d-195">設定或取得用來從資料庫中取出資料的 SQL 字串。</span><span class="sxs-lookup"><span data-stu-id="4730d-195">Sets or gets the SQL string that is used to retrieve data from the database.</span></span> <span data-ttu-id="4730d-196">這可以是 SQL 查詢或預存程式名稱。</span><span class="sxs-lookup"><span data-stu-id="4730d-196">This can either be a SQL query or a stored procedure name.</span></span>

### <a name="selectcommandtype"></a><span data-ttu-id="4730d-197">SelectCommandType</span><span class="sxs-lookup"><span data-stu-id="4730d-197">SelectCommandType</span></span>

<span data-ttu-id="4730d-198">設定或取得 select 命令的類型，也就是 SQL 查詢（文字）或預存程式（StoredProcedure）。</span><span class="sxs-lookup"><span data-stu-id="4730d-198">Sets or gets the type of select command, either a SQL query (Text) or a stored procedure (StoredProcedure).</span></span>

### <a name="selectparameters"></a><span data-ttu-id="4730d-199">SelectParameters</span><span class="sxs-lookup"><span data-stu-id="4730d-199">SelectParameters</span></span>

<span data-ttu-id="4730d-200">傳回與 SqlDataSource 控制項相關聯之 SqlDataSourceView 物件的 SelectCommand 所使用的參數。</span><span class="sxs-lookup"><span data-stu-id="4730d-200">Returns the parameters that are used by the SelectCommand of the SqlDataSourceView object associated with the SqlDataSource control.</span></span>

### <a name="sortparametername"></a><span data-ttu-id="4730d-201">SortParameterName</span><span class="sxs-lookup"><span data-stu-id="4730d-201">SortParameterName</span></span>

<span data-ttu-id="4730d-202">取得或設定預存程式參數的名稱，這是在排序資料來源控制項所抓取的資料時使用的。</span><span class="sxs-lookup"><span data-stu-id="4730d-202">Gets or sets the name of a stored procedure parameter that is used when sorting data retrieved by the data source control.</span></span> <span data-ttu-id="4730d-203">只有當 SelectCommandType 設定為 StoredProcedure 時才有效。</span><span class="sxs-lookup"><span data-stu-id="4730d-203">Valid only when SelectCommandType is set to StoredProcedure.</span></span>

### <a name="sqlcachedependency"></a><span data-ttu-id="4730d-204">SqlCacheDependency</span><span class="sxs-lookup"><span data-stu-id="4730d-204">SqlCacheDependency</span></span>

<span data-ttu-id="4730d-205">以分號分隔的字串，指定用於 SQL Server 快取相依性中的資料庫和資料表。</span><span class="sxs-lookup"><span data-stu-id="4730d-205">A semi-colon delimited string specifying the databases and tables used in a SQL Server cache dependency.</span></span> <span data-ttu-id="4730d-206">（稍後的課程模組中將會討論 SQL 快取相依性）。</span><span class="sxs-lookup"><span data-stu-id="4730d-206">(SQL cache dependencies will be discussed in a later module.)</span></span>

### <a name="updatecommand"></a><span data-ttu-id="4730d-207">UpdateCommand</span><span class="sxs-lookup"><span data-stu-id="4730d-207">UpdateCommand</span></span>

<span data-ttu-id="4730d-208">設定或取得在更新資料庫中的資料時所使用的 SQL 字串。</span><span class="sxs-lookup"><span data-stu-id="4730d-208">Sets or gets the SQL string that is used when updating data in the database.</span></span> <span data-ttu-id="4730d-209">這可以是 SQL 查詢或預存程式名稱。</span><span class="sxs-lookup"><span data-stu-id="4730d-209">This can either be a SQL query or a stored procedure name.</span></span>

### <a name="updatecommandtype"></a><span data-ttu-id="4730d-210">UpdateCommandType</span><span class="sxs-lookup"><span data-stu-id="4730d-210">UpdateCommandType</span></span>

<span data-ttu-id="4730d-211">設定或取得 update 命令的類型，也就是 SQL 查詢（文字）或預存程式（StoredProcedure）。</span><span class="sxs-lookup"><span data-stu-id="4730d-211">Sets or gets the type of update command, either a SQL query (Text) or a stored procedure (StoredProcedure).</span></span>

### <a name="updateparameters"></a><span data-ttu-id="4730d-212">UpdateParameters</span><span class="sxs-lookup"><span data-stu-id="4730d-212">UpdateParameters</span></span>

<span data-ttu-id="4730d-213">傳回與 SqlDataSource 控制項相關聯之 SqlDataSourceView 物件的 UpdateCommand 所使用的參數。</span><span class="sxs-lookup"><span data-stu-id="4730d-213">Returns the parameters that are used by the UpdateCommand of the SqlDataSourceView object associated with the SqlDataSource control.</span></span>

## <a name="the-accessdatasource-control"></a><span data-ttu-id="4730d-214">AccessDataSource 控制項</span><span class="sxs-lookup"><span data-stu-id="4730d-214">The AccessDataSource Control</span></span>

<span data-ttu-id="4730d-215">AccessDataSource 控制項會衍生自 SqlDataSource 類別，用來將資料系結至 Microsoft Access 資料庫。</span><span class="sxs-lookup"><span data-stu-id="4730d-215">The AccessDataSource control derives from the SqlDataSource class and is used to data-bind to a Microsoft Access database.</span></span> <span data-ttu-id="4730d-216">AccessDataSource 控制項的 ConnectionString 屬性是唯讀屬性。</span><span class="sxs-lookup"><span data-stu-id="4730d-216">The ConnectionString property for the AccessDataSource control is a read-only property.</span></span> <span data-ttu-id="4730d-217">資料檔案屬性會用來指向 Access 資料庫，而不是使用 ConnectionString 屬性，如下所示。</span><span class="sxs-lookup"><span data-stu-id="4730d-217">Instead of using the ConnectionString property, the DataFile property is used to point to the Access Database as shown below.</span></span>

[!code-aspx[Main](data-source-controls/samples/sample4.aspx)]

<span data-ttu-id="4730d-218">AccessDataSource 一律會將基底 SqlDataSource 的 ProviderName 設定為 System.object，並使用 Microsoft OLE DB 提供者連接到資料庫。</span><span class="sxs-lookup"><span data-stu-id="4730d-218">The AccessDataSource will always set the ProviderName of the base SqlDataSource to System.Data.OleDb and connects to the database using the Microsoft.Jet.OLEDB.4.0 OLE DB provider.</span></span> <span data-ttu-id="4730d-219">您無法使用 AccessDataSource 控制項連接到受密碼保護的 Access 資料庫。</span><span class="sxs-lookup"><span data-stu-id="4730d-219">You cannot use the AccessDataSource control to connect to a password-protected Access database.</span></span> <span data-ttu-id="4730d-220">如果您必須連接到受密碼保護的資料庫，您應該使用 SqlDataSource 控制項。</span><span class="sxs-lookup"><span data-stu-id="4730d-220">If you have to connect to a password protected database, you should use the SqlDataSource control.</span></span>

> [!NOTE]
> <span data-ttu-id="4730d-221">儲存在網站內的 Access 資料庫應該放在應用程式\_資料目錄中。</span><span class="sxs-lookup"><span data-stu-id="4730d-221">Access databases stored within the Web site should be placed in the App\_Data directory.</span></span> <span data-ttu-id="4730d-222">ASP.NET 不允許流覽此目錄中的檔案。</span><span class="sxs-lookup"><span data-stu-id="4730d-222">ASP.NET does not allow files in this directory to be browsed.</span></span> <span data-ttu-id="4730d-223">使用 Access 資料庫時，您必須將應用程式的讀取和寫入權限授與給進程帳戶\_資料目錄。</span><span class="sxs-lookup"><span data-stu-id="4730d-223">You will need to grant the process account Read and Write permissions to the App\_Data directory when using Access databases.</span></span>

## <a name="the-xmldatasource-control"></a><span data-ttu-id="4730d-224">XmlDataSource 控制項</span><span class="sxs-lookup"><span data-stu-id="4730d-224">The XmlDataSource Control</span></span>

<span data-ttu-id="4730d-225">XmlDataSource 是用來將 XML 資料系結至資料繫結控制項。</span><span class="sxs-lookup"><span data-stu-id="4730d-225">The XmlDataSource is used to data-bind XML data to data-bound controls.</span></span> <span data-ttu-id="4730d-226">您可以使用 [資料檔案] 屬性系結至 XML 檔案，也可以使用 Data 屬性系結至 XML 字串。</span><span class="sxs-lookup"><span data-stu-id="4730d-226">You can bind to an XML file using the DataFile property or you can bind to an XML string using the Data property.</span></span> <span data-ttu-id="4730d-227">XmlDataSource 會將 XML 屬性公開為可系結欄位。</span><span class="sxs-lookup"><span data-stu-id="4730d-227">The XmlDataSource exposes XML attributes as bindable fields.</span></span> <span data-ttu-id="4730d-228">如果您需要系結至不是以屬性工作表示的值，就必須使用 XSL 轉換。</span><span class="sxs-lookup"><span data-stu-id="4730d-228">In cases where you need to bind to values that are not represented as attributes, you will need to use an XSL transform.</span></span> <span data-ttu-id="4730d-229">您也可以使用 XPath 運算式來篩選 XML 資料。</span><span class="sxs-lookup"><span data-stu-id="4730d-229">You can also use XPath expressions to filter XML data.</span></span>

<span data-ttu-id="4730d-230">請考慮下列 XML 檔案：</span><span class="sxs-lookup"><span data-stu-id="4730d-230">Consider the following XML file:</span></span>

[!code-xml[Main](data-source-controls/samples/sample5.xml)]

<span data-ttu-id="4730d-231">請注意，XmlDataSource 會使用*人員/人員*的 XPath 屬性，只篩選 &lt;Person&gt; 節點。</span><span class="sxs-lookup"><span data-stu-id="4730d-231">Notice that the XmlDataSource uses an XPath property of *People/Person* in order to filter on just the &lt;Person&gt; nodes.</span></span> <span data-ttu-id="4730d-232">然後，DropDownList 會使用 DataTextField 屬性，將資料系結至 LastName 屬性。</span><span class="sxs-lookup"><span data-stu-id="4730d-232">The DropDownList then data-binds to the LastName attribute using the DataTextField property.</span></span>

<span data-ttu-id="4730d-233">雖然 XmlDataSource 控制項主要是用來將資料系結至唯讀的 XML 資料，但您還是可以編輯 XML 資料檔案。</span><span class="sxs-lookup"><span data-stu-id="4730d-233">While the XmlDataSource control is primarily used to data-bind to read-only XML data, it is possible to edit the XML data file.</span></span> <span data-ttu-id="4730d-234">請注意，在這種情況下，自動插入、更新及刪除 XML 檔案中的資訊，並不會因為它與其他資料來源控制項一樣自動進行。</span><span class="sxs-lookup"><span data-stu-id="4730d-234">Note that in such cases, automatic insertion, updating, and deletion of information in the XML file does not happen automatically as it does with other data source controls.</span></span> <span data-ttu-id="4730d-235">相反地，您必須使用 XmlDataSource 控制項的下列方法，撰寫程式碼來手動編輯資料。</span><span class="sxs-lookup"><span data-stu-id="4730d-235">Instead, you will have to write code to manually edit the data using the following methods of the XmlDataSource control.</span></span>

### <a name="getxmldocument"></a><span data-ttu-id="4730d-236">GetXmlDocument</span><span class="sxs-lookup"><span data-stu-id="4730d-236">GetXmlDocument</span></span>

<span data-ttu-id="4730d-237">抓取包含 XmlDataSource 所抓取之 XML 程式碼的已承載物件。</span><span class="sxs-lookup"><span data-stu-id="4730d-237">Retrieves an XmlDocument object containing the XML code retrieved by the XmlDataSource.</span></span>

### <a name="save"></a><span data-ttu-id="4730d-238">儲存</span><span class="sxs-lookup"><span data-stu-id="4730d-238">Save</span></span>

<span data-ttu-id="4730d-239">將記憶體中的 Xml 儲存回資料來源。</span><span class="sxs-lookup"><span data-stu-id="4730d-239">Saves the in-memory XmlDocument back to the data source.</span></span>

<span data-ttu-id="4730d-240">請務必瞭解，只有在符合下列兩個條件時，Save 方法才會有效：</span><span class="sxs-lookup"><span data-stu-id="4730d-240">It's important to realize that the Save method will only work when the following two conditions are met:</span></span>

1. <span data-ttu-id="4730d-241">XmlDataSource 會使用 [資料檔案] 屬性來系結至 XML 檔案，而不是要系結至記憶體中 XML 資料的 [Data] 屬性。</span><span class="sxs-lookup"><span data-stu-id="4730d-241">The XmlDataSource is using the DataFile property to bind to an XML file instead of the Data property to bind to in-memory XML data.</span></span>
2. <span data-ttu-id="4730d-242">不會透過 Transform 或 TransformFile 屬性來指定轉換。</span><span class="sxs-lookup"><span data-stu-id="4730d-242">No transformation is specified via the Transform or TransformFile property.</span></span>

<span data-ttu-id="4730d-243">另請注意，當多位使用者同時呼叫 Save 方法時，可能會產生非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="4730d-243">Note also that the Save method can yield unexpected results when called by multiple users concurrently.</span></span>

## <a name="the-objectdatasource-control"></a><span data-ttu-id="4730d-244">ObjectDataSource 控制項</span><span class="sxs-lookup"><span data-stu-id="4730d-244">The ObjectDataSource Control</span></span>

<span data-ttu-id="4730d-245">目前為止所涵蓋的資料來源控制項，是兩層式應用程式的絕佳選擇，其中資料來源控制項會直接與資料存放區進行通訊。</span><span class="sxs-lookup"><span data-stu-id="4730d-245">The data source controls that we have covered up to this point are excellent choices for two-tier applications where the data source control communicates directly to the data store.</span></span> <span data-ttu-id="4730d-246">不過，許多真實世界的應用程式都是多層式應用程式，其中資料來源控制項可能需要與商務物件通訊，而後者又會與資料層通訊。</span><span class="sxs-lookup"><span data-stu-id="4730d-246">However, many real-world applications are multi-tier applications where a data source control might need to communicate to a business object which, in turn, communicates with the data layer.</span></span> <span data-ttu-id="4730d-247">在這些情況下，ObjectDataSource 會適當地填滿帳單。</span><span class="sxs-lookup"><span data-stu-id="4730d-247">In these situations, the ObjectDataSource fills the bill nicely.</span></span> <span data-ttu-id="4730d-248">ObjectDataSource 會與來源物件搭配運作。</span><span class="sxs-lookup"><span data-stu-id="4730d-248">The ObjectDataSource works in conjunction with a source object.</span></span> <span data-ttu-id="4730d-249">如果您的物件有實例方法，而不是靜態方法（在 Visual Basic 中共用），ObjectDataSource 控制項會建立來源物件的實例、呼叫指定的方法，以及處置該物件實例的所有範圍。</span><span class="sxs-lookup"><span data-stu-id="4730d-249">The ObjectDataSource control will create an instance of the source object, call the specified method, and dispose of the object instance all within the scope of a single request, if your object has instance methods instead of static methods (Shared in Visual Basic).</span></span> <span data-ttu-id="4730d-250">因此，您的物件必須是無狀態。</span><span class="sxs-lookup"><span data-stu-id="4730d-250">Therefore, your object must be stateless.</span></span> <span data-ttu-id="4730d-251">也就是說，您的物件應該在單一要求的範圍內取得並釋放所有必要的資源。</span><span class="sxs-lookup"><span data-stu-id="4730d-251">That is, your object should acquire and release all required resources within the span of a single request.</span></span> <span data-ttu-id="4730d-252">您可以藉由處理 ObjectDataSource 控制項的 ObjectCreating 事件來控制來源物件的建立方式。</span><span class="sxs-lookup"><span data-stu-id="4730d-252">You can control how the source object is created by handling the ObjectCreating event of the ObjectDataSource control.</span></span> <span data-ttu-id="4730d-253">您可以建立來源物件的實例，然後將 ObjectDataSourceEventArgs 類別的 ObjectInstance 屬性設定為該實例。</span><span class="sxs-lookup"><span data-stu-id="4730d-253">You can create an instance of the source object, and then set the ObjectInstance property of the ObjectDataSourceEventArgs class to that instance.</span></span> <span data-ttu-id="4730d-254">ObjectDataSource 控制項將會使用在 ObjectCreating 事件中建立的實例，而不是自行建立實例。</span><span class="sxs-lookup"><span data-stu-id="4730d-254">The ObjectDataSource control will use the instance that is created in the ObjectCreating event instead of creating an instance on its own.</span></span>

<span data-ttu-id="4730d-255">如果 ObjectDataSource 控制項的來源物件公開公用靜態方法（在 Visual Basic 中共用），可以呼叫這些方法來抓取和修改資料，則 ObjectDataSource 控制項會直接呼叫這些方法。</span><span class="sxs-lookup"><span data-stu-id="4730d-255">If the source object for an ObjectDataSource control exposes public static methods (Shared in Visual Basic) that can be called to retrieve and modify data, an ObjectDataSource control will call those methods directly.</span></span> <span data-ttu-id="4730d-256">如果 ObjectDataSource 控制項必須建立來源物件的實例，才能進行方法呼叫，物件必須包含不接受任何參數的公用函式。</span><span class="sxs-lookup"><span data-stu-id="4730d-256">If an ObjectDataSource control must create an instance of the source object in order to make method calls, the object must include a public constructor that takes no parameters.</span></span> <span data-ttu-id="4730d-257">當 ObjectDataSource 控制項建立來源物件的新實例時，會呼叫這個函式。</span><span class="sxs-lookup"><span data-stu-id="4730d-257">The ObjectDataSource control will call this constructor when it creates a new instance of the source object.</span></span>

<span data-ttu-id="4730d-258">如果來源物件未包含沒有參數的公用函式，您可以建立來源物件的實例，以供 ObjectCreating 事件中的 ObjectDataSource 控制項使用。</span><span class="sxs-lookup"><span data-stu-id="4730d-258">If the source object does not contain a public constructor without parameters, you can create an instance of the source object that will be used by the ObjectDataSource control in the ObjectCreating event.</span></span>

## <a name="specifying-object-methods"></a><span data-ttu-id="4730d-259">指定物件方法</span><span class="sxs-lookup"><span data-stu-id="4730d-259">Specifying Object Methods</span></span>

<span data-ttu-id="4730d-260">ObjectDataSource 控制項的來源物件可以包含用來選取、插入、更新或刪除資料的任意數目方法。</span><span class="sxs-lookup"><span data-stu-id="4730d-260">The source object for an ObjectDataSource control can contain any number of methods that are used to select, insert, update, or delete data.</span></span> <span data-ttu-id="4730d-261">這些方法是由 ObjectDataSource 控制項根據方法的名稱來呼叫，如使用 ObjectDataSource 控制項的 SelectMethod、InsertMethod、UpdateMethod 或 DeleteMethod 屬性所識別。</span><span class="sxs-lookup"><span data-stu-id="4730d-261">These methods are called by the ObjectDataSource control based on the name of the method, as identified by using either the SelectMethod, InsertMethod, UpdateMethod, or DeleteMethod property of the ObjectDataSource control.</span></span> <span data-ttu-id="4730d-262">來源物件也可以包含選擇性的 SelectCount 方法，此方法是由 ObjectDataSource 控制項使用 SelectCountMethod 屬性來識別，而此方法會傳回資料來源的物件總數計數。</span><span class="sxs-lookup"><span data-stu-id="4730d-262">The source object can also include an optional SelectCount method, which is identified by the ObjectDataSource control using the SelectCountMethod property, that returns the count of the total number of objects at the data source.</span></span> <span data-ttu-id="4730d-263">ObjectDataSource 控制項會在呼叫了 Select 方法以取得資料來源中的記錄總數，以便在分頁時使用，以呼叫 SelectCount 方法。</span><span class="sxs-lookup"><span data-stu-id="4730d-263">The ObjectDataSource control will call the SelectCount method after a Select method has been called to retrieve the total number of records at the data source for use when paging.</span></span>

## <a name="lab-using-data-source-controls"></a><span data-ttu-id="4730d-264">使用資料來源控制項的實驗室</span><span class="sxs-lookup"><span data-stu-id="4730d-264">Lab Using Data Source Controls</span></span>

## <a name="exercise-1---displaying-data-with-the-sqldatasource-control"></a><span data-ttu-id="4730d-265">練習 1-使用 SqlDataSource 控制項顯示資料</span><span class="sxs-lookup"><span data-stu-id="4730d-265">Exercise 1 - Displaying Data with the SqlDataSource Control</span></span>

<span data-ttu-id="4730d-266">下列練習會使用 SqlDataSource 控制項來連接至 Northwind 資料庫。</span><span class="sxs-lookup"><span data-stu-id="4730d-266">The following exercise uses the SqlDataSource control to connect to the Northwind database.</span></span> <span data-ttu-id="4730d-267">它假設您可以存取 SQL Server 2000 實例上的 Northwind 資料庫。</span><span class="sxs-lookup"><span data-stu-id="4730d-267">It assumes that you have access to the Northwind database on a SQL Server 2000 instance.</span></span>

1. <span data-ttu-id="4730d-268">建立新的 ASP.NET 網站。</span><span class="sxs-lookup"><span data-stu-id="4730d-268">Create a new ASP.NET Web site.</span></span>
2. <span data-ttu-id="4730d-269">新增 web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="4730d-269">Add a new web.config file.</span></span>

    1. <span data-ttu-id="4730d-270">以滑鼠右鍵按一下方案總管中的專案，然後按一下 [加入新專案]。</span><span class="sxs-lookup"><span data-stu-id="4730d-270">Right-click on the project in Solution Explorer and click Add New Item.</span></span>
    2. <span data-ttu-id="4730d-271">從範本清單中選擇 [Web 設定檔]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="4730d-271">Choose Web Configuration File from the list of templates and click Add.</span></span>
3. <span data-ttu-id="4730d-272">編輯 &lt;connectionStrings&gt; 區段，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4730d-272">Edit the &lt;connectionStrings&gt; section as follows:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample6.aspx)]
4. <span data-ttu-id="4730d-273">切換至程式碼視圖，並將 ConnectionString 屬性和 SelectCommand 屬性新增至 &lt;asp： SqlDataSource&gt; 控制項，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4730d-273">Switch to Code view and add a ConnectionString attribute and a SelectCommand attribute to the &lt;asp:SqlDataSource&gt; control as follows:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample7.aspx)]
5. <span data-ttu-id="4730d-274">從設計檢視新增 GridView 控制項。</span><span class="sxs-lookup"><span data-stu-id="4730d-274">From Design view, add a new GridView control.</span></span>
6. <span data-ttu-id="4730d-275">從 [GridView 工作] 功能表的 [選擇資料來源] 下拉式清單中，選擇 [SqlDataSource1]。</span><span class="sxs-lookup"><span data-stu-id="4730d-275">From the Choose Data Source dropdown in the GridView Tasks menu, choose SqlDataSource1.</span></span>
7. <span data-ttu-id="4730d-276">以滑鼠右鍵按一下 default.aspx，然後從功能表中選擇 [在瀏覽器中查看]。</span><span class="sxs-lookup"><span data-stu-id="4730d-276">Right-click on Default.aspx and choose View in Browser from the menu.</span></span> <span data-ttu-id="4730d-277">當系統提示您儲存時，按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="4730d-277">Click Yes when prompted to save.</span></span>
8. <span data-ttu-id="4730d-278">GridView 會顯示 Products 資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="4730d-278">The GridView displays the data from the Products table.</span></span>

## <a name="exercise-2---editing-data-with-the-sqldatasource-control"></a><span data-ttu-id="4730d-279">練習 2-使用 SqlDataSource 控制項編輯資料</span><span class="sxs-lookup"><span data-stu-id="4730d-279">Exercise 2 - Editing Data with the SqlDataSource Control</span></span>

<span data-ttu-id="4730d-280">下列練習示範如何使用宣告式語法來系結 DropDownList 控制項的資料，並可讓您編輯 DropDownList 控制項中顯示的資料。</span><span class="sxs-lookup"><span data-stu-id="4730d-280">The following exercise demonstrates how to data bind a DropDownList control using the declarative syntax and allows you to edit the data presented in the DropDownList control.</span></span>

1. <span data-ttu-id="4730d-281">在設計檢視中，從 default.aspx 刪除 GridView 控制項。</span><span class="sxs-lookup"><span data-stu-id="4730d-281">In Design view, delete the GridView control from Default.aspx.</span></span> 

    <span data-ttu-id="4730d-282">**重要**：將 SqlDataSource 控制項保留在頁面上。</span><span class="sxs-lookup"><span data-stu-id="4730d-282">**Important**: Leave the SqlDataSource control on the page.</span></span>
2. <span data-ttu-id="4730d-283">將 DropDownList 控制項新增至 default.aspx。</span><span class="sxs-lookup"><span data-stu-id="4730d-283">Add a DropDownList control to Default.aspx.</span></span>
3. <span data-ttu-id="4730d-284">切換至來源視圖。</span><span class="sxs-lookup"><span data-stu-id="4730d-284">Switch to Source view.</span></span>
4. <span data-ttu-id="4730d-285">將 DataSourceId、DataTextField 和 DataValueField 屬性新增至 &lt;asp： DropDownList&gt; 控制項，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4730d-285">Add a DataSourceId, DataTextField, and DataValueField attribute to the &lt;asp:DropDownList&gt; control as follows:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample8.aspx)]
5. <span data-ttu-id="4730d-286">儲存 default.aspx，並在瀏覽器中查看。</span><span class="sxs-lookup"><span data-stu-id="4730d-286">Save Default.aspx and view it in the browser.</span></span> <span data-ttu-id="4730d-287">請注意，DropDownList 包含 Northwind 資料庫中的所有產品。</span><span class="sxs-lookup"><span data-stu-id="4730d-287">Note that the DropDownList contains all of the products from the Northwind database.</span></span>
6. <span data-ttu-id="4730d-288">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="4730d-288">Close the browser.</span></span>
7. <span data-ttu-id="4730d-289">在 default.aspx 的來源視圖中，在 DropDownList 控制項下方新增 TextBox 控制項。</span><span class="sxs-lookup"><span data-stu-id="4730d-289">In Source view of Default.aspx, add a new TextBox control below the DropDownList control.</span></span> <span data-ttu-id="4730d-290">將文字方塊的 [ID] 屬性變更為 [txtProductName]。</span><span class="sxs-lookup"><span data-stu-id="4730d-290">Change the ID property of the TextBox to txtProductName.</span></span>
8. <span data-ttu-id="4730d-291">在 TextBox 控制項底下，加入新的按鈕控制項。</span><span class="sxs-lookup"><span data-stu-id="4730d-291">Under the TextBox control, add a new Button control.</span></span> <span data-ttu-id="4730d-292">將按鈕的 [ID] 屬性變更為 [btnUpdate]，並將 [Text] 屬性變更為 [**更新產品名稱**]。</span><span class="sxs-lookup"><span data-stu-id="4730d-292">Change the ID property of the Button to btnUpdate and the Text property to **Update Product Name**.</span></span>
9. <span data-ttu-id="4730d-293">在 default.aspx 的來源視圖中，將 UpdateCommand 屬性和兩個新 UpdateParameters 新增至 SqlDataSource 標記，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4730d-293">In Source view of Default.aspx, add an UpdateCommand property and two new UpdateParameters to the SqlDataSource tag as follows:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample9.aspx)]

    > [!NOTE]
    > <span data-ttu-id="4730d-294">請注意，此程式碼中已加入兩個更新參數（ProductName 和 ProductID）。</span><span class="sxs-lookup"><span data-stu-id="4730d-294">Note that there are two update parameters (ProductName and ProductID) added in this code.</span></span> <span data-ttu-id="4730d-295">這些參數會對應至 [txtProductName] 文字方塊的 [Text] 屬性，以及 ddlProducts DropDownList 的 [SelectedValue] 屬性。</span><span class="sxs-lookup"><span data-stu-id="4730d-295">These parameters are mapped to the Text property of the txtProductName TextBox and the SelectedValue property of the ddlProducts DropDownList.</span></span>
10. <span data-ttu-id="4730d-296">切換至設計檢視，然後按兩下按鈕控制項加入事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="4730d-296">Switch to Design view and double-click on the Button control to add an event handler.</span></span>
11. <span data-ttu-id="4730d-297">將下列程式碼新增至 btnUpdate\_按一下 [程式碼]：</span><span class="sxs-lookup"><span data-stu-id="4730d-297">Add the following code to the btnUpdate\_Click code:</span></span> 

    [!code-csharp[Main](data-source-controls/samples/sample10.cs)]
12. <span data-ttu-id="4730d-298">以滑鼠右鍵按一下 default.aspx，然後選擇在瀏覽器中進行查看。</span><span class="sxs-lookup"><span data-stu-id="4730d-298">Right-click on Default.aspx and choose to view it in the browser.</span></span> <span data-ttu-id="4730d-299">出現提示時，按一下 [是] 以儲存所有變更。</span><span class="sxs-lookup"><span data-stu-id="4730d-299">Click Yes when prompted to save all changes.</span></span>
13. <span data-ttu-id="4730d-300">ASP.NET 2.0 部分類別允許在執行時間進行編譯。</span><span class="sxs-lookup"><span data-stu-id="4730d-300">ASP.NET 2.0 partial classes allow for compilation at runtime.</span></span> <span data-ttu-id="4730d-301">您不需要建立應用程式，就能看到程式碼變更生效。</span><span class="sxs-lookup"><span data-stu-id="4730d-301">It is not necessary to build an application in order to see code changes take effect.</span></span>
14. <span data-ttu-id="4730d-302">從 DropDownList 中選取產品。</span><span class="sxs-lookup"><span data-stu-id="4730d-302">Select a product from the DropDownList.</span></span>
15. <span data-ttu-id="4730d-303">在文字方塊中輸入所選產品的新名稱，然後按一下 [更新] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4730d-303">Enter a new name for the selected product in the TextBox and then click the Update button.</span></span>
16. <span data-ttu-id="4730d-304">產品名稱會在資料庫中更新。</span><span class="sxs-lookup"><span data-stu-id="4730d-304">The product name is updated in the database.</span></span>

## <a name="exercise-3-using-the-objectdatasource-control"></a><span data-ttu-id="4730d-305">使用 ObjectDataSource 控制項的練習3</span><span class="sxs-lookup"><span data-stu-id="4730d-305">Exercise 3 Using the ObjectDataSource Control</span></span>

<span data-ttu-id="4730d-306">此練習將示範如何使用 ObjectDataSource 控制項和來源物件，與 Northwind 資料庫互動。</span><span class="sxs-lookup"><span data-stu-id="4730d-306">This exercise will demonstrate how to use the ObjectDataSource control and a source object to interact with the Northwind database.</span></span>

1. <span data-ttu-id="4730d-307">以滑鼠右鍵按一下方案總管中的專案，然後按一下 [加入新專案]。</span><span class="sxs-lookup"><span data-stu-id="4730d-307">Right-click on the project in Solution Explorer and click on Add New Item.</span></span>
2. <span data-ttu-id="4730d-308">在 [範本] 清單中選取 [Web 表單]。</span><span class="sxs-lookup"><span data-stu-id="4730d-308">Select Web Form in the templates list.</span></span> <span data-ttu-id="4730d-309">將 [名稱] 變更為 [default.aspx]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="4730d-309">Change the name to object.aspx and click Add.</span></span>
3. <span data-ttu-id="4730d-310">以滑鼠右鍵按一下方案總管中的專案，然後按一下 [加入新專案]。</span><span class="sxs-lookup"><span data-stu-id="4730d-310">Right-click on the project in Solution Explorer and click on Add New Item.</span></span>
4. <span data-ttu-id="4730d-311">在 [範本] 清單中選取 [類別]。</span><span class="sxs-lookup"><span data-stu-id="4730d-311">Select Class in the templates list.</span></span> <span data-ttu-id="4730d-312">將類別的名稱變更為 NorthwindData.cs，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="4730d-312">Change the name of the class to NorthwindData.cs and click Add.</span></span>
5. <span data-ttu-id="4730d-313">出現提示時，按一下 [是]，將類別新增至應用程式\_Code 資料夾。</span><span class="sxs-lookup"><span data-stu-id="4730d-313">Click Yes when prompted to add the class to the App\_Code folder.</span></span>
6. <span data-ttu-id="4730d-314">將下列程式碼新增至 NorthwindData.cs 檔案：</span><span class="sxs-lookup"><span data-stu-id="4730d-314">Add the following code to the NorthwindData.cs file:</span></span> 

    [!code-csharp[Main](data-source-controls/samples/sample11.cs)]
7. <span data-ttu-id="4730d-315">將下列程式碼加入至物件 .aspx 的來源視圖：</span><span class="sxs-lookup"><span data-stu-id="4730d-315">Add the following code to the Source view of object.aspx:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample12.aspx)]
8. <span data-ttu-id="4730d-316">儲存所有檔案並流覽物件 .aspx。</span><span class="sxs-lookup"><span data-stu-id="4730d-316">Save all files and browse object.aspx.</span></span>
9. <span data-ttu-id="4730d-317">藉由查看詳細資料、編輯員工、新增員工和刪除員工，來與介面互動。</span><span class="sxs-lookup"><span data-stu-id="4730d-317">Interact with the interface by viewing details, editing employees, adding employees, and deleting employees.</span></span>
