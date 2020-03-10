---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
title: 使用 ASP.NET MVC 搭配不同版本的 IIS （VB） |Microsoft Docs
author: microsoft
description: 在本教學課程中，您將瞭解如何使用不同版本 Internet Information Services 的 ASP.NET MVC 和 URL 路由。 您將瞭解不同的策略 。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 1c1283b2-6956-4937-b568-d30de432ce23
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
msc.type: authoredcontent
ms.openlocfilehash: b754175c853c20eec6be3521376b62d62f33106d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581834"
---
# <a name="using-aspnet-mvc-with-different-versions-of-iis-vb"></a>使用 ASP.NET MVC 與不同版本的 IIS (VB)

由[Microsoft](https://github.com/microsoft)

> 在本教學課程中，您將瞭解如何使用不同版本 Internet Information Services 的 ASP.NET MVC 和 URL 路由。 您會瞭解使用 ASP.NET MVC 搭配 IIS 7.0 （傳統模式）、IIS 6.0 和舊版 IIS 的不同策略。

ASP.NET MVC 架構相依于 ASP.NET 路由，以將瀏覽器要求路由至控制器動作。 為了充分利用 ASP.NET 路由，您可能必須在 web 伺服器上執行其他設定步驟。 這全都取決於應用程式的 Internet Information Services （IIS）版本和要求處理模式。

以下是不同版本 IIS 的摘要：

- IIS 7.0 （整合模式）-不需要特殊設定即可使用 ASP.NET 路由。
- IIS 7.0 （傳統模式）-您需要執行特殊設定以使用 ASP.NET 路由。
- IIS 6.0 或以下-您需要執行特殊設定，才能使用 ASP.NET 路由。

最新版本的 IIS 是7.5 版（在 Win7 上）。 Iis 的 iis 7 包含在 Windows Server 2008 和 VISTA/SP1 及更新版本中。 您也可以在任何版本的 Vista 作業系統（Home Basic 除外）上安裝 IIS 7.0 （請參閱[https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)）。

IIS 7.0 支援兩種模式來處理要求。 您可以使用整合模式或傳統模式。 在整合模式中使用 IIS 7.0 時，您不需要執行任何特殊的設定步驟。 不過，在傳統模式中使用 IIS 7.0 時，您必須執行其他設定。

Microsoft Windows Server 2003 包含 IIS 6.0。 當您使用 Windows Server 2003 作業系統時，無法將 IIS 6.0 升級至 IIS 7.0。 使用 IIS 6.0 時，您必須執行額外的設定步驟。

Microsoft Windows XP Professional 包含 IIS 5.1。 使用 IIS 5.1 時，您必須執行額外的設定步驟。

最後，Microsoft Windows 2000 和 Microsoft Windows 2000 Professional 包含 IIS 5.0。 使用 IIS 5.0 時，您必須執行額外的設定步驟。

## <a name="integrated-versus-classic-mode"></a>整合式與傳統模式

IIS 7.0 可以使用兩種不同的要求處理模式來處理要求：整合式和傳統。 整合模式可提供更佳的效能和更多功能。 包括傳統模式，以提供與舊版 IIS 的回溯相容性。

要求處理模式取決於應用程式集區。 藉由判斷與應用程式相關聯的應用程式集區，您可以判斷特定 web 應用程式正在使用哪種處理模式。 請依照下列步驟：

1. 啟動 Internet Information Services 管理員
2. 在 [連線] 視窗中，選取應用程式
3. 在 [動作] 視窗中，按一下 [**基本設定**] 連結以開啟 [編輯應用程式] 對話方塊（請參閱 [圖 1]）
4. 記下所選的應用程式集區。

根據預設，IIS 會設定為支援兩個應用程式集區： **DefaultAppPool**和**傳統 .net AppPool**。 如果已選取 [DefaultAppPool]，則您的應用程式會以整合式要求處理模式執行。 如果選取了傳統的 .NET AppPool，您的應用程式就會在傳統要求處理模式下執行。

[![[新增專案] 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.png)

**圖 1**：偵測要求處理模式（[按一下以查看完整大小的影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.png)）

請注意，您可以在 [編輯應用程式] 對話方塊中修改要求處理模式。 按一下 [選取] 按鈕，並變更與應用程式相關聯的應用程式集區。 請注意，將 ASP.NET 應用程式從 [傳統] 變更為 [整合模式] 時，會發生相容性問題。 如需詳細資訊，請參閱下列文章：

- 在 Windows Vista 和 Windows Server 上將 ASP.NET 1.1 升級至 IIS 7.0 2008-- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)

- ASP.NET 與 IIS 7.0 整合- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)

如果 ASP.NET 應用程式正在使用 DefaultAppPool，則您不需要執行任何額外的步驟，即可讓 ASP.NET 路由（因而 ASP.NET MVC）得以正常操作。 不過，如果 ASP.NET 應用程式設定為使用傳統的 .NET AppPool，然後繼續閱讀，則您會有更多的工作要執行。

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a>搭配舊版 IIS 使用 ASP.NET MVC

如果您需要使用比 IIS 7.0 更舊的 IIS 版本的 ASP.NET MVC，或需要在傳統模式中使用 IIS 7.0，則您有兩個選項。 首先，您可以修改路由表以使用副檔名。 例如，您會要求類似/Store.aspx/Details. 的 URL，而不是要求/Store/Details 之類的 URL。

第二個選項是建立一個名為*萬用字元腳本對應*的東西。 萬用字元腳本對應可讓您將每個要求對應到 ASP.NET 架構。

如果您沒有 web 伺服器的存取權（例如，您的 ASP.NET MVC 應用程式是由網際網路服務提供者所裝載），則您必須使用第一個選項。 如果您不想修改 Url 的外觀，而且可以存取您的 web 伺服器，則可以使用第二個選項。

我們將在下列各節中詳細探討每個選項。

## <a name="adding-extensions-to-the-route-table"></a>將擴充功能新增至路由表

取得 ASP.NET 路由以使用舊版 IIS 的最簡單方式，就是修改 global.asax 檔案中的路由表。 [清單 1] 中的預設和未修改的 global.asax 檔案會設定一個名為「預設路由」的路由。

**清單 1-global.asax （未修改）**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample1.vb)]

[清單 1] 中設定的預設路由可讓您路由 Url，如下所示：

/Home/Index

/Product/Details/3

/Product

可惜的是，較舊版本的 IIS 不會將這些要求傳遞至 ASP.NET 架構。 因此，這些要求將不會路由傳送至控制器。 例如，如果您對 URL/Home/Index 提出瀏覽器要求，則會出現 [圖 2] 中的錯誤頁面。

[![[新增專案] 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.png)

**圖 2**：收到404找不到錯誤（[按一下以觀看完整大小的影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.png)）

較舊版本的 IIS 只會將特定要求對應至 ASP.NET framework。 要求必須是具有正確副檔名的 URL。 例如，/SomePage.aspx 的要求會對應至 ASP.NET 架構。 不過，/SomePage.htm 的要求不會。

因此，若要讓 ASP.NET 路由能夠正常執行，我們必須修改預設路由，使其包含對應至 ASP.NET 架構的副檔名。

這是使用名為 `registermvc.wsf`的腳本來完成。 它隨附于 `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`中的 ASP.NET MVC 1 版本，但從 ASP.NET 2 開始，此腳本已移至 ASP.NET 的未來，可從[http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978)取得。

執行此腳本會向 IIS 註冊新的. mvc 延伸模組。 註冊 mvc 副檔名之後，您可以修改 global.asax 檔案中的路由，讓路由使用 mvc 副檔名。

[清單 2] 中修改的 global.asax 檔案可與舊版的 IIS 搭配運作。

**清單 2-global.asax （使用延伸模組修改）**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample2.vb)]

重要事項：請記得在變更 global.asax 檔案之後，再次建立您的 ASP.NET MVC 應用程式。

[清單 2] 中的 global.asax 檔案有兩項重要的變更。 現在 global.asax 中定義了兩個路由。 預設路由的 URL 模式（第一個路由）現在看起來像這樣：

{controller}. mvc/{action}/{id}

新增 mvc 副檔名會變更 ASP.NET 路由模組所攔截的檔案類型。 透過這項變更，ASP.NET MVC 應用程式現在會路由傳送如下的要求：

/Home.mvc/Index/

/Product.mvc/Details/3

/Product.mvc/

第二個路由（根路由）是新的。 根路由的此 URL 模式是空字串。 需要此路由，才能比對對您的應用程式根目錄提出的要求。 例如，根路由會符合如下所示的要求：

[http://www.YourApplication.com/](http://www.YourApplication.com/)

對您的路由表進行這些修改之後，您必須確定應用程式中的所有連結都與這些新的 URL 模式相容。 換句話說，請確定您所有的連結都包含 mvc 副檔名。 如果您使用 Html.actionlink （） helper 方法來產生連結，則不需要進行任何變更。

除了使用 registermvc，您也可以將新的延伸模組新增至 IIS，並手動對應至 ASP.NET 架構。 自行新增擴充功能時，請確定未核取標示為 [**確認檔案存在**] 的核取方塊。

## <a name="hosted-server"></a>主控伺服器

您不一定可以存取您的網頁伺服器。 例如，如果您使用網際網路主控提供者裝載 ASP.NET MVC 應用程式，則您不一定會有 IIS 的存取權。

在這種情況下，您應該使用對應至 ASP.NET 架構的其中一個現有副檔名。 對應至 ASP.NET 的副檔名範例包括 .aspx、axd 和 ashx 延伸模組。

例如，在 [清單 3] 中修改的 global.asax 檔案使用 .aspx 副檔名，而不是 mvc 副檔名。

**清單 3-global.asax （以 .aspx 副檔名修改）**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample3.vb)]

[清單 3] 中的 global.asax 檔案與先前的 global.asax 檔案完全相同，不同之處在于它使用 .aspx 副檔名，而不是 mvc 副檔名。 您不需要在遠端 web 伺服器上執行任何安裝程式，就能使用 .aspx 副檔名。

## <a name="creating-a-wildcard-script-map"></a>建立萬用字元腳本對應

如果您不想要修改 ASP.NET MVC 應用程式的 Url，而且可以存取您的 web 伺服器，則您會有額外的選項。 您可以建立萬用字元腳本對應，將 web 伺服器的所有要求對應到 ASP.NET 架構。 如此一來，您就可以使用預設的 ASP.NET MVC 路由表搭配 IIS 7.0 （在傳統模式中）或 IIS 6.0。

請注意，此選項會使 IIS 攔截對網頁伺服器提出的每個要求。 這包括對影像、傳統 ASP 網頁和 HTML 網頁的要求。 因此，啟用萬用字元腳本對應至 ASP.NET 會對效能造成影響。

以下是針對 IIS 7.0 啟用萬用字元腳本對應的方式：

1. 在 [連接] 視窗中選取您的應用程式
2. 請確定已選取 [**功能**] 視圖
3. 按兩下 [**處理常式**對應] 按鈕
4. 按一下 [**新增萬用字元腳本對應**] 連結（請參閱 [圖 3]）
5. 輸入 aspnet\_isapi .dll 檔案的路徑（您可以從 PageHandlerFactory 腳本對應複製此路徑）
6. 輸入 MVC 的名稱
7. 按一下 [**確定]** 按鈕

[![[新增專案] 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.png)

**圖 3**：使用 IIS 7.0 建立萬用字元腳本對應（[按一下以觀看完整大小的影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image6.png)）

請遵循下列步驟，以使用 IIS 6.0 建立萬用字元腳本對應：

1. 以滑鼠右鍵按一下網站，然後選取 [屬性]
2. 選取 [**主目錄**] 索引標籤
3. 按一下 [**設定**] 按鈕
4. 選取 [**對應**] 索引標籤
5. 按一下 [**插入**] 按鈕（請參閱 [圖 4]）
6. 將 aspnet\_的路徑貼到 [可執行檔] 欄位中（您可以從 .aspx 檔案的腳本對應複製此路徑）
7. 取消核取標示為 [**確認檔案存在**] 的核取方塊
8. 按一下 [**確定]** 按鈕

[![[新增專案] 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image7.png)

**圖 4**：使用 IIS 6.0 建立萬用字元腳本對應（[按一下以觀看完整大小的影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image8.png)）

啟用萬用字元腳本對應之後，您必須修改 global.asax 檔案中的路由表，使其包含根路由。 否則，當您對應用程式的根頁面提出要求時，您會看到 [圖 5] 中的錯誤頁面。 您可以使用 [清單 4] 中已修改的 global.asax 檔案。

[![[新增專案] 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image9.png)

**圖 5**：遺漏根路由錯誤（[按一下以查看完整大小的影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image10.png)）

**清單 4-global.asax （使用根路由修改）**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample4.vb)]

啟用 IIS 7.0 或 IIS 6.0 的萬用字元腳本對應之後，您可以建立與預設路由表搭配使用的要求，如下所示：

/

/Home/Index

/Product/Details/3

/Product

## <a name="summary"></a>總結

本教學課程的目的是要說明在使用舊版 IIS （或傳統模式的 IIS 7.0）時，您可以如何使用 ASP.NET MVC。 我們討論了兩種取得 ASP.NET 路由以使用舊版 IIS 的方法：修改預設路由表或建立萬用字元腳本對應。

第一個選項會要求您修改 ASP.NET MVC 應用程式中使用的 Url。 第一個選項的其中一個非常重要的優點是，您不需要存取 web 伺服器，就可以修改路由表。 這表示您可以使用這個第一個選項，即使是在裝載與網際網路主控公司的 ASP.NET MVC 應用程式時也一樣。

第二個選項是建立萬用字元腳本對應。 第二個選項的優點是您不需要修改 Url。 第二個選項的缺點是，它可能會影響 ASP.NET MVC 應用程式的效能。

> [!div class="step-by-step"]
> [上一篇](using-asp-net-mvc-with-different-versions-of-iis-cs.md)
