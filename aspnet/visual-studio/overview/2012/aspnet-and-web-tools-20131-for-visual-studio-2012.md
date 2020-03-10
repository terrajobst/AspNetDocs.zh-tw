---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: Visual Studio 2012 的 ASP.NET 和 Web 工具2013.1 版本資訊 |Microsoft Docs
author: microsoft
description: 本檔說明 Visual Studio 2012 的 ASP.NET 和 Web 工具2013.1 版本。
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 260af1018064d60d80cbb1002001f28c4daffffd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578439"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>適用於 Visual Studio 2012 的 ASP.NET 和 Web 工具 2013.1 版本資訊

由[Microsoft](https://github.com/microsoft)

> 本檔說明 Visual Studio 2012 的 ASP.NET 和 Web 工具2013.1 版本。

## <a name="contents"></a>內容

- [安裝注意事項](#install)
- [軟體需求](#requirements)
- Visual Studio 2012 ASP.NET 和 Web 工具2013.1 的新功能

    - [啟動程序](#bootstrap)
    - [範本](#templates)

        - [ASP.NET MVC 5 範本](#mvc5template)
        - [ASP.NET Web API 2 範本](#apitemplate)
        - [專案範本](#itemtemplate)
    - [Entity Framework 6](#ef6)
    - [ASP.NET 的樣板](#scaffold)
    - [Razor 編輯器](#razor)
    - [NuGet 2.7](#nuget)
- 已知問題和重大變更

    - [ASP.NET 的樣板](#issuescaffolding)

        - [MVC 和 Web API 架構-HTTP 404，找不到錯誤](#404issue)
        - [Visual Studio Express 2012 for Web 會在新增 scaffold 專案後停止運作](#expressissue)
    - [ASP.NET Razor 3](#issuerazor)

        - [使用 [流覽] 或 F5 來查看 cshtml 檔案會導致伺服器錯誤](#browseissue)
        - [Url 重寫和波狀符號（~）](#rewriteissue)
    - [範本](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a>安裝注意事項

[安裝](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids)適用于 Visual Studio 2012 的 ASP.NET 和 Web 工具2013.1。

<a id="requirements"></a>
## <a name="software-requirements"></a>軟體需求

您必須有 Visual Studio 2012 或 Visual Studio Express 2012 for Web。

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>Visual Studio 2012 ASP.NET 和 Web 工具2013.1 的新功能

<a id="bootstrap"></a>
### <a name="bootstrap"></a>從中

當您 scaffold MVC 5 控制器和 views 時，views 的標記會使用[啟動](http://getbootstrap.com/)程式。

<a id="templates"></a>
### <a name="templates"></a>範本

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a>ASP.NET MVC 5 範本

我們已加入新的 MVC 5 範本。 它會參考最新的 MVC 5 NuGet 套件，您可以使用 [樣板] 來新增控制器和 views。

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a>ASP.NET Web API 2 範本

我們已新增 Web API 2 範本。 它會參考最新的 Web API 2 NuGet 套件，您可以使用樣板來新增控制器和視圖。

<a id="itemtemplate"></a>
#### <a name="item-templates"></a>項目範本

我們新增了 MVC 5 views、Web Pages （Razor 3）和 Web API 2 控制器的新專案範本。 它們會在加入新專案時，將相關的 NuGet 套件安裝到專案。

<a id="ef6"></a>
### <a name="entity-framework-6"></a>Entity Framework 6

當您使用 Entity Framework scaffold MVC 或 Web API 控制器時，我們會使用 Framework 6。 如需 Entity Framework 的詳細資訊，請參閱[Entity Framework 版本歷程記錄](https://msdn.com/data/jj574253)。

您也可以下載並安裝適用于 Visual Studio 2012 的 Entity Framework 6 工具。 請參閱[Get Entity Framework](https://msdn.com/data/ee712906#tooling)。

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET 的樣板

ASP.NET 樣板是用於 ASP.NET Web 應用程式的程式碼產生架構。 它可讓您輕鬆地將未定案程式碼加入至您的專案，以與資料模型互動。

在舊版的 Visual Studio 中，架構僅限於 ASP.NET MVC 專案。 透過此更新，您現在可以使用任何 ASP.NET 專案的樣板，包括 Web Forms。 此更新不支援產生 Web form 專案的頁面，但您仍然可以將 MVC 相依性新增至專案，以使用具有 Web form 的樣板。 在未來的更新中，將會新增針對 Web form 產生網頁的支援。

使用 [樣板] 時，我們會確保專案中已安裝所有必要的相依性。 例如，如果您從 ASP.NET Web form 專案開始，然後使用樣板來新增 Web API 控制器，則會自動將所需的 NuGet 套件和參考新增至您的專案。

若要將 MVC 樣板加入至 Web form 專案，請加入**新的 Scaffold 專案**，然後在交談視窗中選取 [ **MVC 5**相依性]。 有兩個適用于樣板 MVC 的選項;最小和完整。 如果您選取 [最低]，則只會將 ASP.NET MVC 的 NuGet 套件和參考新增至您的專案。 如果您選取 [完整] 選項，則會加入最少的相依性，以及 MVC 專案所需的內容檔案。

支援架構的非同步控制器會使用 Entity Framework 6 的新異步功能。

如需詳細資訊和教學課程，請參閱 ASP.NET 架構的[總覽](../2013/aspnet-scaffolding-overview.md)。 這些教學課程會顯示具有 Visual Studio 2013 的樣板，但它們也適用于 Visual Studio 2012 的 ASP.NET 和 Web 工具2013.1。

<a id="razor"></a>
### <a name="razor-editor"></a>Razor 編輯器

在此更新中，Visual Studio 2012 現在支援 Razor 3 工具/編輯。

<a id="nuget"></a>
### <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7 包含一組豐富的新功能，在[NuGet 2.7 版本](http://docs.nuget.org/docs/release-notes/nuget-2.7)資訊中有詳細的說明。

此版本的 NuGet 不需要使用者明確允許 NuGet 還原遺失的套件。 安裝 NuGet 2.7 時，使用者會隱含地同意自動還原遺失的套件。 使用者可以透過 Visual Studio 中的 NuGet 設定明確選擇不進行套件還原。 這種變更可簡化封裝還原的運作方式。

## <a name="known-issues-and-breaking-changes"></a>已知問題和重大變更

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET 的樣板

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC 和 Web API 架構-HTTP 404，找不到錯誤

如果您在將 scaffold 專案新增至專案時遇到錯誤，您的專案可能會處於不一致的狀態。 所做的部分變更會復原，但其他變更（例如已安裝的 NuGet 套件）將不會復原。 如果復原路由設定變更，使用者在流覽至 scaffold 專案時，會收到 HTTP 404 錯誤。

若要修正 MVC 的這個錯誤，請加入新的 scaffold 專案，然後選取 [MVC 5 相依性] （最小或完整）。 此程式會將所有必要的變更新增至您的專案。

若要修正 Web API 的這個錯誤：

1. 將下列 WebApiConfig 類別新增至您的專案。

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. 依照下列方式，在 WebApiConfig 中註冊應用程式\_Start 方法：

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a>Visual Studio Express 2012 for Web 會在新增 scaffold 專案後停止運作

如果 Visual Studio Express 2012 for Web 會在使用 Entity Framework 新增 scaffold 專案後停止運作（例如具有動作的 Web API 2 控制器，使用 Entity Framework），可能是 Visual Studio Express 無法載入元件的原生映射。相依于 System.web. Extensions。

若要更正此問題，請將 Visual Studio Express 設定為使用 System.web 副檔名的 MSIL 映射：

1. 在系統管理員模式中開啟命令提示字元。
2. 前往%ProgramFiles%\Microsoft Visual Studio 11.0 \ Common7\IDE 或% ProgramFiles （x86）% \ Microsoft Visual Studio 11.0 \ Common7\IDE （適用于64位 Windows）。
3. 在文字編輯器中開啟 VWDExpress。
4. 在 &lt;設定&gt;/&lt;執行時間&gt; 元素底下新增下列程式程式碼：  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. 重新開機 Web 的 Visual Studio Express 2012。

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a>ASP.NET Razor 3

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a>使用 [流覽] 或 F5 來查看 cshtml 檔案會導致伺服器錯誤

當您在 Visual Studio 2012 中建立 MVC 5 專案時（或在 Visual Studio 2012 中開啟以 Visual Studio 2013 建立的 MVC 5 專案）並嘗試使用 [流覽方式] 或 F5 來查看 cshtml 檔案時，您會收到錯誤訊息，指出 **'/' 應用程式中的伺服器錯誤**。 伺服器嘗試流覽至 `http://localhost:XXXX/Views/../XXXX.cshtml`

若要解決此問題，請將專案中的 [**起始動作**] 設定變更為 [**特定頁面**]。 您不需要提供頁面的值。

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

進行這項變更之後，選取 [F5] 以流覽至您應用程式的根目錄（`http://localhost:XXXX`）。 這個行為與 Visual Studio 2013 中的 MVC 5 專案行為不同，因為**目前的頁面**設定會啟動開啟的頁面。

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a>Url 重寫和波狀符號（~）

升級至 ASP.NET Razor 3 或 ASP.NET MVC 5 之後，如果您使用 URL 重寫，波狀符號（~）標記法可能無法再正常運作。 URL 重寫會影響 HTML 專案中的波狀符號（~）標記法（例如 &lt;A/&gt;、&lt;SCRIPT/&gt;、&lt;LINK/&gt;），因此波狀波不會再對應到根目錄。

例如，如果您將**asp.net/content**的要求重寫為**asp.net**，&lt;href = "~/content/"/&gt; 的 href 屬性會解析為 **/content/content/** ，而不是 **/** 。 若要抑制這項變更，您可以在每個網頁或 global.asax 的**應用程式\_BeginRequest**中，將**IIS\_WasUrlRewritten**內容設定為 false。

<a id="templateissue"></a>
### <a name="templates"></a>範本

當您在 Windows 8.1 或 Windows Server 2012 R2 上建立具有 Visual Studio 2012 的 ASP.NET MVC 專案時，Visual Studio 會顯示錯誤訊息，指出「設定 Web [url] ASP.NET 4.5 失敗」。

![設定錯誤](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

您會看到此錯誤，因為 Visual Studio 2012 不會在安裝于這些 Windows 版本時啟用 ASP.NET 4.5 功能。 若要啟用 ASP.NET 4.5，請執行 [[開啟或關閉 Windows 功能](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)] 中所述的步驟。

![開啟或關閉 Windows 功能](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

或者，您可以透過命令列啟用 ASP.NET 4.5。

1. 在系統管理員模式中開啟命令提示字元。
2. 執行下列命令以啟用 ASP.NET 4.5。  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
