---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
title: 使用 ASP.NET Web API 2.2 建立 OData v4 端點 |Microsoft Docs
author: MikeWasson
description: 開放式資料通訊協定（OData）是 web 的資料存取通訊協定。 OData 透過 CRUD 作業提供統一的方式來查詢和運算元據集 。
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 1e1927c0-ded1-4752-80fd-a146628d2f09
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
msc.type: authoredcontent
ms.openlocfilehash: 81d134cbd3231b9a0d5537ccbd1bbfe6419254af
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598732"
---
# <a name="create-an-odata-v4-endpoint-using-aspnet-web-api"></a>使用 ASP.NET Web API 建立 OData v4 端點 

> 開放式資料通訊協定（OData）是 web 的資料存取通訊協定。 OData 透過 CRUD 作業（建立、讀取、更新和刪除）提供統一的方式來查詢和運算元據集。
>
> ASP.NET Web API 支援通訊協定的 v3 和 v4。 您甚至可以有一個與 v3 端點並存執行的 v4 端點。
>
> 本教學課程說明如何建立支援 CRUD 作業的 OData v4 端點。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
>
> - Web API 5。2
> - OData v4
> - Visual Studio 2017 （請[在這裡](https://visualstudio.microsoft.com/downloads/)下載 Visual Studio 2017）
> - Entity Framework 6
> - .NET 4.7。2
>
> ## <a name="tutorial-versions"></a>教學課程版本
>
> 針對 OData 第3版，請參閱[建立 odata V3 端點](../odata-v3/creating-an-odata-endpoint.md)。

## <a name="create-the-visual-studio-project"></a>建立 Visual Studio 專案

在 Visual Studio 中，從 **[檔案**] 功能表選取 [**新增**&gt;**專案**]。

展開 **已安裝** &gt; **Visual C#**  &gt; **web**，然後選取  **ASP.NET Web 應用程式（.NET Framework）**  範本。 將專案命名為 &quot;ProductService&quot;。

[![](create-an-odata-v4-endpoint/_static/image7.png)](create-an-odata-v4-endpoint/_static/image7.png)

選取 [確定]。

[![](create-an-odata-v4-endpoint/_static/image8.png)](create-an-odata-v4-endpoint/_static/image8.png)

選取 [空白] 範本。 在 [**新增資料夾和核心參考：** ] 底下，選取 [ **Web API**]。 選取 [確定]。

## <a name="install-the-odata-packages"></a>安裝 OData 封裝

從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**] &gt; [**套件管理員主控台**]。 在 [套件管理員主控台] 視窗中，輸入：

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample1.cmd)]

此命令會安裝最新的 OData NuGet 套件。

## <a name="add-a-model-class"></a>新增模型類別

「*模型*」是代表您應用程式中資料實體的物件。

在 [方案總管] 中，於 Models 資料夾上按一下滑鼠右鍵。 從內容功能表中，選取 [**新增**&gt;**類別**]。

[![](create-an-odata-v4-endpoint/_static/image6.png)](create-an-odata-v4-endpoint/_static/image5.png)

> [!NOTE]
> 依照慣例，模型類別會放在 [模型] 資料夾中，但您不需要在自己的專案中遵循此慣例。

將類別命名為 `Product`。 在 Product.cs 檔案中，將重複使用的程式碼取代為下列內容：

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample2.cs)]

`Id` 屬性是實體索引鍵。 用戶端可以依索引鍵查詢實體。 例如，若要取得識別碼為5的產品，則 URI 為 `/Products(5)`。 `Id` 屬性也會是後端資料庫中的主要金鑰。

## <a name="enable-entity-framework"></a>啟用 Entity Framework

在本教學課程中，我們將使用 Entity Framework （EF） Code First 來建立後端資料庫。

> [!NOTE]
> Web API OData 不需要 EF。 使用可將資料庫實體轉譯成模型的任何資料存取層。

首先，安裝 EF 的 NuGet 套件。 從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**] &gt; [**套件管理員主控台**]。 在 [套件管理員主控台] 視窗中，輸入：

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample3.cmd)]

開啟 web.config 檔案，並在**configSections**元素後面的**configuration**元素內新增下列區段。

[!code-xml[Main](create-an-odata-v4-endpoint/samples/sample4.xml?highlight=6)]

此設定會加入 LocalDB 資料庫的連接字串。 當您在本機執行應用程式時，將會使用此資料庫。

接下來，將名為 `ProductsContext` 的類別新增至 [模型] 資料夾：

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample5.cs)]

在此函數中，`"name=ProductsContext"` 會提供連接字串的名稱。

## <a name="configure-the-odata-endpoint"></a>設定 OData 端點

開啟檔案應用程式\_Start/WebApiConfig. cs。 新增下列**using**語句：

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample6.cs)]

然後將下列程式碼新增至**Register**方法：

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample7.cs)]

這段程式碼會執行兩項工作：

- 建立實體資料模型（EDM）。
- 新增路由。

EDM 是資料的抽象模型。 EDM 是用來建立服務元資料檔案。 **ODataConventionModelBuilder**類別會使用預設命名慣例來建立 EDM。 這種方法需要最少的程式碼。 如果您想要更充分掌控 EDM，您可以使用**用**類別來明確地新增屬性、索引鍵和導覽屬性來建立 edm。

*路由*會告知 Web API 如何將 HTTP 要求路由傳送至端點。 若要建立 OData v4 路由，請呼叫**MapODataServiceRoute**擴充方法。

如果您的應用程式有多個 OData 端點，請為每個端點建立個別的路由。 為每個路由提供唯一的路由名稱和前置詞。

## <a name="add-the-odata-controller"></a>新增 OData 控制器

*控制器*是處理 HTTP 要求的類別。 您會針對 OData 服務中的每個實體集建立個別的控制器。 在本教學課程中，您將為 `Product` 實體建立一個控制器。

在方案總管中，以滑鼠右鍵按一下 [控制器] 資料夾，然後選取 [**新增**&gt;**類別**]。 將類別命名為 `ProductsController`。

> [!NOTE]
> 此 OData v3 教學課程的版本會使用「**新增控制器**」架構。 目前沒有 OData v4 的樣板。

將 ProductsController.cs 中的重複使用程式碼取代為下列程式碼。

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample8.cs)]

控制器會使用 `ProductsContext` 類別，以使用 EF 來存取資料庫。 請注意，控制器會覆寫**dispose**方法來處置**ProductsCoNtext**。

這是控制器的起點。 接下來，我們將新增所有 CRUD 作業的方法。

## <a name="query-the-entity-set"></a>查詢實體集

將下列方法新增至 `ProductsController`。

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample9.cs)]

`Get` 方法的無參數版本會傳回整個產品集合。 具有索引*鍵*參數的 `Get` 方法會依其索引鍵（在此案例中為 `Id` 屬性）查閱產品。

**[EnableQuery]** 屬性可讓用戶端使用查詢選項（例如 $filter、$sort 和 $page）來修改查詢。 如需詳細資訊，請參閱[支援 OData 查詢選項](../supporting-odata-query-options.md)。

## <a name="add-an-entity-to-the-entity-set"></a>將實體新增至實體集

若要讓用戶端將新產品新增至資料庫，請將下列方法新增至 `ProductsController`。

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample10.cs)]

## <a name="update-an-entity"></a>更新實體

OData 支援兩種不同的語義來更新實體、PATCH 和 PUT。

- PATCH 會執行部分更新。 用戶端只會指定要更新的屬性。
- PUT 會取代整個實體。

PUT 的缺點是用戶端必須傳送實體中所有屬性的值，包括不會變更的值。 [OData 規格](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719)會指出建議的修補程式。

在任何情況下，以下是 PATCH 和 PUT 方法的程式碼：

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample11.cs)]

在修補程式的情況下，控制器會使用**差異&lt;t&gt;** 類型來追蹤變更。

## <a name="delete-an-entity"></a>刪除實體

若要讓用戶端從資料庫中刪除產品，請將下列方法新增至 `ProductsController`。

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample12.cs)]
