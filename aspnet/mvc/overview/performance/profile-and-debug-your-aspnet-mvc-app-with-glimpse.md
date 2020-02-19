---
uid: mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
title: 使用粗略的分析和 ASP.NET MVC 應用程式Microsoft Docs
author: Rick-Anderson
description: 「一覽」是一系列蓬勃發展且持續成長的開放原始碼 NuGet 套件，提供詳細的效能、偵錯工具和診斷資訊，讓您 ASP.NET 。
ms.author: riande
ms.date: 03/26/2015
ms.assetid: c205805f-efdd-4fa7-9616-f26eab180611
msc.legacyurl: /mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
msc.type: authoredcontent
ms.openlocfilehash: d3689147a3bc3aa1f4180c377d2483a94bdd95a9
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457657"
---
# <a name="profile-and-debug-your-aspnet-mvc-app-with-glimpse"></a>使用 Glimpse 分析 ASP.NET MVC 應用程式以對其進行偵錯

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> 「一覽」是蓬勃發展且持續成長的開放原始碼 NuGet 套件系列，提供 ASP.NET 應用程式的詳細效能、偵錯工具和診斷資訊。 在每一頁的底部，安裝、輕量、超高，並顯示關鍵效能計量是很簡單的。 當您需要瞭解伺服器上的狀況時，它可讓您向下切入至您的應用程式。 我們建議您在整個開發週期（包括您的 Azure 測試環境）中使用它，以提供非常重要的資訊。 雖然[Fiddler](http://www.telerik.com/fiddler)和[F-12 開發工具](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx)提供用戶端視圖，但還是會從伺服器提供詳細的觀點。 本教學課程將著重于使用 ASP.NET MVC 和 EF 封裝，但有許多其他套件可供使用。 在可能的情況下，我會連結到適當的[粗略](http://getglimpse.com/Docs/)檔，協助維護。 「一覽」是一個開放原始碼專案，您也可以參與原始程式碼和檔。

- [安裝一覽](#ig)
- [啟用對 localhost 的粗略](#eg)
- [[時間軸] 索引標籤](#Time)
- [模型繫結](#mb)
- [路由](#route)
- [使用 Azure 上的粗略操作](#da)
- [其他資源](#addRes)

<a id="ig"></a>
## <a name="installing-glimpse"></a>安裝一覽

您可以從 NuGet 套件管理員主控台，或從 [**管理 NuGet 套件**] 主控台安裝。 在此示範中，我將安裝 Mvc5 和 EF6 套件：

![從 NuGet Dlg 安裝一覽](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image1.png)

搜尋*粗略的 EF*

![從 NuGet 安裝 dlg 的 EF](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image2.png)

藉由選取 [**已安裝的套件**]，您可以看到已安裝的「粗略相依模組」：

![已安裝從 DLg 開始進行封裝](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image3.png)

下列命令會從套件管理員主控台安裝 MVC5 和 EF6 模組：

[!code-console[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample1.cmd)]

<a id="eg"></a>
## <a name="enable-glimpse-for-localhost"></a>啟用對 localhost 的粗略

流覽至 http://localhost:&lt;p 埠 o #&gt;/glimpse.axd，然後按一下 [<strong>開啟</strong>] 按鈕。

![粗略頁面](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image4.png)

如果您有顯示 [我的最愛] 列，您可以拖放 [粗略] 按鈕，並將其新增為 bookmarklets：

![熟悉 bookmarklets 的 IE](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image5.png)

您現在可以流覽您的應用程式，並在頁面底部顯示**標題顯示**（抬頭顯示器）。

![具有抬頭顯示器的連絡人管理員頁面](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image6.png)

[一覽[抬頭顯示器] 頁面](http://getglimpse.com/Docs/Heads-up-Display)會詳細說明上面顯示的計時資訊。 抬頭顯示器所顯示的不顯眼效能資料，可以立即通知您問題，然後才進入測試週期。 按一下右下角的 &quot;g&quot; 會顯示 [一覽] 面板：

![一覽面板](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image7.png)

在上圖中，已選取 [[執行]](http://getglimpse.com/Docs/Execution-Tab)索引標籤，它會顯示管線中動作和篩選準則的計時詳細資料。 您可以看到我的[停止監看篩選計時器](http://www.nuget.org/packages/StopWatch/)在管線的第6階段開始。 雖然我的輕量計時器可以提供有用的設定檔/時間資料，但它卻遺漏了授權和呈現視圖所花費的所有時間。 您可以在設定檔中閱讀關於我[的計時器，以及將 ASP.NET MVC 應用程式一直到 Azure 的時間](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx)。 [索引標籤] 頁面會提供每個索引標籤上詳細[資訊的連結](http://getglimpse.com/Docs/Tabs)。

<a id="Time"></a>
## <a name="the-timeline-tab"></a>[時間軸] 索引標籤

我已修改 Tom 作者: dykstra 的未完成[EF 6/MVC 5 教學](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)課程，並將下列程式碼變更為講師控制器：

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample2.cs?highlight=1,20-31)]

上述程式碼可讓我傳入查詢字串（`eager`），以控制資料的積極式或明確載入。 在下圖中，會使用明確載入，而 [計時] 頁面會顯示在 `Index` 動作方法中載入的每個註冊：

![明確式載入](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image8.png)

在下列程式碼中，會指定 [積極]，並在呼叫 `Index` view 之後提取每個註冊：

![指定了積極的](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image9.png)

您可以將滑鼠停留在某個時間區段上，以取得詳細的計時資訊：

![將滑鼠暫留以查看詳細計時](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image10.png)

<a id="mb"></a>
## <a name="model-binding"></a>模型繫結

[[模型](http://getglimpse.com/Docs/Model-Binding-Tab)系結] 索引標籤可提供豐富的資訊，協助您瞭解如何系結表單變數，以及為何某些不會如預期般系結。 下圖顯示 **？** 圖示，您可以按一下它來顯示該功能的粗略說明頁面。

![查看模型系結視圖](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image11.png)

<a id="route"></a>
## <a name="routes"></a>路由

 [粗略路由] 索引標籤可協助您進行調試和瞭解路由。 在下圖中，已選取 [產品路線] （並以綠色顯示「一覽」慣例）。 ![選取的產品名稱](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) 路由條件約束、區域和資料權杖也會顯示。 如需詳細資訊，請參閱[在 ASP.NET MVC 5 中](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx)查看[路由](http://getglimpse.com/Docs/Routes-Tab)和屬性路由。 

<a id="da"></a>
## <a name="using-glimpse-on-azure"></a>使用 Azure 上的粗略操作

[粗略的預設安全性原則] 只允許從本機主機顯示資料。 您可以變更此安全性原則，讓您可以在遠端伺服器（例如 Azure 上的 web 應用程式）上查看此資料。 針對 Azure 上的測試環境，請在*web.config*檔案底部新增反白顯示的標記，以讓您大致瞭解：

[!code-xml[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample3.xml?highlight=2-6)]

透過這種變更，任何使用者都可以在遠端網站上看到您的資料。 請考慮將上述標記新增至發行設定檔，使它只會在您使用該發行設定檔（例如，您的 Azure 測試組態檔）時部署。為了限制流覽資料，我們會新增 `canViewGlimpseData` 角色，而且只允許此角色中的使用者查看資料的外觀。

移除*GlimpseSecurityPolicy.cs*檔案中的批註，並將[IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx)呼叫從 `Administrator` 變更為 `canViewGlimpseData` 角色：

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample4.cs?highlight=6)]

> [!WARNING]
> 安全性-所提供的豐富資料可以公開應用程式的安全性。 Microsoft 尚未執行「粗略」的安全性審核，以用於生產應用程式。

如需新增角色的相關資訊，請參閱我的[部署具有成員資格、OAuth 和 SQL Database 的安全 ASP.NET MVC 5 web 應用程式](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)教學課程。

<a id="addRes"></a>
## <a name="additional-resources"></a>其他資源

- [將具有成員資格、OAuth 和 SQL Database 的 Secure ASP.NET MVC 5 應用程式部署至 Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)
- [一覽設定]-設定索引標籤、執行時間原則、記錄[等的檔](http://getglimpse.com/Docs/Configuration)頁面。
