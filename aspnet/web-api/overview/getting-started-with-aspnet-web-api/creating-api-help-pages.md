---
uid: web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
title: 建立 ASP.NET Web API 的說明頁面-ASP.NET 4。x
author: MikeWasson
description: 本教學課程與程式碼示範如何建立 ASP.NET 4.x 中 ASP.NET Web API 的說明頁面。
ms.author: riande
ms.date: 04/01/2013
ms.custom: seoapril2019
ms.assetid: 0150e67b-c50d-4613-83ea-7b4ef8cacc5a
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
msc.type: authoredcontent
ms.openlocfilehash: 8308dab8bd66aa8f5a3c5fb4133fc7a3df78f671
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556872"
---
# <a name="creating-help-pages-for-aspnet-web-api"></a>建立 ASP.NET Web API 的說明頁面

由[Mike Wasson](https://github.com/MikeWasson)

本教學課程與程式碼示範如何建立 ASP.NET 4.x 中 ASP.NET Web API 的說明頁面。

當您建立 Web API 時，建立說明頁通常會很有説明，讓其他開發人員知道如何呼叫您的 API。 您可以手動建立所有檔，但最好盡可能自動增加。 為了讓這項工作更容易，ASP.NET Web API 在執行時間提供自動產生說明頁面的程式庫。

![](creating-api-help-pages/_static/image1.png)

## <a name="creating-api-help-pages"></a>建立 API 說明頁面

安裝[ASP.NET 和 Web 工具2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=282650)。 此更新會將說明頁面整合到 Web API 專案範本中。

接下來，建立新的 ASP.NET MVC 4 專案，然後選取 [Web API] 專案範本。 專案範本會建立名為 `ValuesController`的範例 API 控制器。 此範本也會建立 API 說明頁面。 [說明] 頁面的所有程式碼檔案都會放在專案的 [區域] 資料夾中。

![](creating-api-help-pages/_static/image2.png)

當您執行應用程式時，首頁會包含 [API 說明] 頁面的連結。 從首頁中，相對路徑為/Help。

![](creating-api-help-pages/_static/image3.png)

此連結會將您帶入 API 摘要頁面。

![](creating-api-help-pages/_static/image4.png)

此頁面的 MVC 視圖會定義在區域/HelpPage/Views/Help/Index. cshtml 中。 您可以編輯此頁面來修改版面配置、簡介、標題、樣式等等。

頁面的主要部分是以控制器分組的 Api 資料表。 系統會使用**IApiExplorer**介面，以動態方式產生資料表專案。 （稍後我會詳細討論此介面）。如果您加入新的 API 控制器，則資料表會在執行時間自動更新。

[API] 欄位會列出 HTTP 方法和相對 URI。 [描述] 資料行包含每個 API 的檔。 一開始，檔只是預留位置文字。 在下一節中，我將示範如何從 XML 批註新增檔。

每個 API 都有頁面的連結，其中包含更詳細的資訊，包括範例要求和回應主體。

![](creating-api-help-pages/_static/image5.png)

## <a name="adding-help-pages-to-an-existing-project"></a>將說明頁面加入至現有的專案

您可以使用 NuGet 套件管理員，將說明頁面新增至現有的 Web API 專案。 從不同于「Web API」範本的專案範本開始，此選項很有用。

從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。 在 [[套件管理員主控台](http://docs.nuget.org/docs/start-here/using-the-package-manager-console)] 視窗中，輸入下列其中一個命令：

針對**C#** 應用程式： `Install-Package Microsoft.AspNet.WebApi.HelpPage`

針對**Visual Basic**應用程式： `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`

有兩個套件，一個用於C# ，一個用於 Visual Basic。 請務必使用符合您專案的對應項。

此命令會安裝必要的元件，並加入說明頁面（位於 [區域]/[HelpPage] 資料夾）的 MVC views。 您必須手動新增 [說明] 頁面的連結。 URI 為/Help。 若要在 razor 視圖中建立連結，請新增下列內容：

[!code-cshtml[Main](creating-api-help-pages/samples/sample1.cshtml)]

此外，請務必註冊區域。 在 global.asax 檔案中，將下列程式碼新增至**應用程式\_Start**方法（如果尚未這麼做）：

[!code-csharp[Main](creating-api-help-pages/samples/sample2.cs?highlight=4)]

## <a name="adding-api-documentation"></a>新增 API 檔

根據預設，說明頁面會有檔的預留位置字串。 您可以使用[XML 檔批註](https://msdn.microsoft.com/library/b2s063f7.aspx)來建立檔。 若要啟用這項功能，請開啟檔案區域/HelpPage/應用程式\_Start/HelpPageConfig，並取消批註下列程式程式碼：

[!code-csharp[Main](creating-api-help-pages/samples/sample3.cs)]

現在啟用 XML 檔。 在方案總管中，以滑鼠右鍵按一下專案，然後選取 [**屬性**]。 選取 [**組建**] 頁面。

![](creating-api-help-pages/_static/image6.png)

在 [**輸出**] 下，檢查**XML**檔檔案。 在編輯方塊中，輸入 "App\_Data/xml"。

![](creating-api-help-pages/_static/image7.png)

接下來，開啟 `ValuesController` API 控制器的程式碼，其定義于/Controllers/ValuesController.cs。 將一些檔批註新增至控制器方法。 例如:

[!code-csharp[Main](creating-api-help-pages/samples/sample4.cs)]

> [!NOTE]
> 提示：如果您將插入號放在方法上方的那一行，並輸入三個正斜線，Visual Studio 會自動插入 XML 元素。 然後您可以填入空白。

現在，再次建立並執行應用程式，並流覽至 [說明] 頁面。 檔字串應該會出現在 API 資料表中。

![](creating-api-help-pages/_static/image8.png)

[說明] 頁面會在執行時間從 XML 檔案讀取字串。 （當您部署應用程式時，請務必部署 XML 檔案）。

## <a name="under-the-hood"></a>幕後

[說明] 頁面是以**ApiExplorer**類別為基礎，這是 Web API 架構的一部分。 **ApiExplorer**類別會提供用來建立說明頁的原始材料。 針對每個 API， **ApiExplorer**包含描述 API 的**ApiDescription** 。 基於此目的，「API」會定義為 HTTP 方法和相對 URI 的組合。 例如，以下是一些不同的 Api：

- 取得/api/Products
- 取得/api/Products/{id}
- 張貼/api/Products

如果控制器動作支援多個 HTTP 方法，則**ApiExplorer**會將每個方法視為不同的 API。

若要隱藏**ApiExplorer**中的 API，請將**ApiExplorerSettings**屬性新增至動作，並將*IgnoreApi*設定為 true。

[!code-csharp[Main](creating-api-help-pages/samples/sample5.cs)]

您也可以將此屬性新增至控制器，以排除整個控制器。

ApiExplorer 類別會從**IDocumentationProvider**介面取得檔字串。 如您稍早所見，說明頁面程式庫提供了從 XML 檔字串取得檔的**IDocumentationProvider** 。 此程式碼位於/Areas/HelpPage/XmlDocumentationProvider.cs。 您可以撰寫自己的**IDocumentationProvider**，以從另一個來源取得檔。 若要連線，請呼叫**SetDocumentationProvider**擴充方法（定義于**HelpPageConfigurationExtensions** ）

**ApiExplorer**會自動呼叫**IDocumentationProvider**介面，以取得每個 API 的檔字串。 它會將它們儲存在**ApiDescription**和**ApiParameterDescription**物件的**檔**屬性中。

## <a name="next-steps"></a>後續步驟

您不限於此處顯示的說明頁面。 事實上， **ApiExplorer**並不限於建立說明頁面。 Yao Huang Lin 已經撰寫了一些絕佳的 blog 文章，讓您有現成的想法：

- [將簡單的測試用戶端新增至 ASP.NET Web API 說明頁面](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/02/adding-a-simple-test-client-to-asp-net-web-api-help-page.aspx)
- [讓 ASP.NET Web API 的說明頁面在自我裝載的服務上工作](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/20/making-asp-net-web-api-help-page-work-on-self-hosted-services.aspx)
- [ASP.NET Web API 的設計階段產生說明頁面（或用戶端）](https://blogs.msdn.com/b/yaohuang1/archive/2013/01/20/design-time-generation-of-help-page-or-proxy-for-asp-net-web-api.aspx)
- [Advanced Help Page 自訂專案](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/10/asp-net-web-api-help-page-part-3-advanced-help-page-customizations.aspx)
