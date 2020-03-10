---
uid: web-pages/overview/getting-started/aspnet-web-pages-razor-faq
title: ASP.NET Web Pages （Razor）常見問題 |Microsoft Docs
author: Rick-Anderson
description: 本文列出一些有關 ASP.NET Web Pages （Razor）和 WebMatrix 的常見問題。 教學課程中使用的軟體版本 ASP.NET Web Pages （R 。
ms.author: riande
ms.date: 02/07/2014
ms.assetid: b137bd04-25e1-47cb-9d96-ef2e179ecf1f
msc.legacyurl: /web-pages/overview/getting-started/aspnet-web-pages-razor-faq
msc.type: authoredcontent
ms.openlocfilehash: 6fa1b668e915af856a693e79eafb7180ed504dc2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640928"
---
# <a name="aspnet-web-pages-razor-faq"></a><span data-ttu-id="90298-104">ASP.NET Web Pages (Razor) 常見問題集</span><span class="sxs-lookup"><span data-stu-id="90298-104">ASP.NET Web Pages (Razor) FAQ</span></span>

<span data-ttu-id="90298-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="90298-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> > [!NOTE] 
> > <span data-ttu-id="90298-106">不再建議使用 WebMatrix 做為 ASP.NET Web Pages 的整合式開發環境。</span><span class="sxs-lookup"><span data-stu-id="90298-106">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="90298-107">使用[Visual Studio](xref:aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio)或[Visual Studio Code](https://code.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="90298-107">Use [Visual Studio](xref:aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>
>
> <span data-ttu-id="90298-108">本文列出一些有關 ASP.NET Web Pages （Razor）和 WebMatrix 的常見問題。</span><span class="sxs-lookup"><span data-stu-id="90298-108">This article lists some frequently asked questions about ASP.NET Web Pages (Razor) and WebMatrix.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="90298-109">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="90298-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="90298-110">ASP.NET Web Pages （Razor）3</span><span class="sxs-lookup"><span data-stu-id="90298-110">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="90298-111">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="90298-111">Visual Studio 2013</span></span>
> - <span data-ttu-id="90298-112">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="90298-112">WebMatrix 3</span></span>
>   
> 
> <span data-ttu-id="90298-113">本教學課程也適用于 ASP.NET Web Pages 2、WebMatrix 2 和 Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="90298-113">This tutorial also works with ASP.NET Web Pages 2, WebMatrix 2, and Visual Studio 2012.</span></span>

- [<span data-ttu-id="90298-114">ASP.NET Web Pages、ASP.NET Web form 和 ASP.NET MVC 之間有何差異？</span><span class="sxs-lookup"><span data-stu-id="90298-114">What's the difference between ASP.NET Web Pages, ASP.NET Web Forms, and ASP.NET MVC?</span></span>](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [<span data-ttu-id="90298-115">我需要 WebMatrix 才能使用網頁嗎？</span><span class="sxs-lookup"><span data-stu-id="90298-115">Do I need WebMatrix in order to work with Web Pages?</span></span>](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [<span data-ttu-id="90298-116">我可以在網頁頁面上使用 ASP.NET Web Forms 控制項嗎？</span><span class="sxs-lookup"><span data-stu-id="90298-116">Can I use ASP.NET Web Forms controls on a Web Pages page?</span></span>](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [<span data-ttu-id="90298-117">我可以在不使用 WebMatrix 的情況下部署 ASP.NET Web Pages 網站嗎？</span><span class="sxs-lookup"><span data-stu-id="90298-117">Can I deploy an ASP.NET Web Pages site without using WebMatrix?</span></span>](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [<span data-ttu-id="90298-118">我是否必須使用 WebSecurity helper 來支援登入？</span><span class="sxs-lookup"><span data-stu-id="90298-118">Do I have to use the WebSecurity helper to support logins?</span></span>](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [<span data-ttu-id="90298-119">ASP.NET Web Pages 支援 HTML5 嗎？</span><span class="sxs-lookup"><span data-stu-id="90298-119">Does ASP.NET Web Pages support HTML5?</span></span>](#Does_ASP.NET_Web_Pages_support_HTML5)
- [<span data-ttu-id="90298-120">我可以搭配網頁使用 JavaScript 和 jQuery 嗎？</span><span class="sxs-lookup"><span data-stu-id="90298-120">Can I use JavaScript and jQuery with Web Pages?</span></span>](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [<span data-ttu-id="90298-121">其他資源</span><span class="sxs-lookup"><span data-stu-id="90298-121">Additional Resources</span></span>](#AdditionalResources)

<span data-ttu-id="90298-122">如有關于錯誤和其他問題的問題，請參閱[ASP.NET Web Pages （Razor）疑難排解指南](https://go.microsoft.com/fwlink/?LinkId=253001)。</span><span class="sxs-lookup"><span data-stu-id="90298-122">For questions about errors and other issues, see the [ASP.NET Web Pages (Razor) Troubleshooting Guide](https://go.microsoft.com/fwlink/?LinkId=253001).</span></span>

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a><span data-ttu-id="90298-123">ASP.NET Web Pages、ASP.NET Web form 和 ASP.NET MVC 之間有何差異？</span><span class="sxs-lookup"><span data-stu-id="90298-123">What's the difference between ASP.NET Web Pages, ASP.NET Web Forms, and ASP.NET MVC?</span></span>

<span data-ttu-id="90298-124">這三個都是建立動態 web 應用程式的 ASP.NET 技術：</span><span class="sxs-lookup"><span data-stu-id="90298-124">All three are ASP.NET technologies for creating dynamic web applications:</span></span>

- <span data-ttu-id="90298-125">ASP.NET Web Pages 著重于將動態（伺服器端）程式碼和資料庫存取權新增至 HTML 網頁，並提供簡單和輕量語法的功能。</span><span class="sxs-lookup"><span data-stu-id="90298-125">ASP.NET Web Pages focuses on adding dynamic (server-side) code and database access to HTML pages, and features simple and lightweight syntax.</span></span>
- <span data-ttu-id="90298-126">ASP.NET Web Forms 是以頁面物件模型和傳統視窗類型控制項（按鈕、清單等）為基礎。</span><span class="sxs-lookup"><span data-stu-id="90298-126">ASP.NET Web Forms is based on a page object model and traditional window-type controls (buttons, lists, etc.).</span></span> <span data-ttu-id="90298-127">Web form 使用以事件為基礎的模型，熟悉以用戶端為基礎的（Windows form）開發工作。</span><span class="sxs-lookup"><span data-stu-id="90298-127">Web Forms uses an event-based model that's familiar to those who've worked with client-based (Windows forms) development.</span></span>
- <span data-ttu-id="90298-128">ASP.NET MVC 會實現 ASP.NET 的模型視圖控制器模式。</span><span class="sxs-lookup"><span data-stu-id="90298-128">ASP.NET MVC implements the model-view-controller pattern for ASP.NET.</span></span> <span data-ttu-id="90298-129">重點在於「關注點分離」（處理、資料和 UI 層）。</span><span class="sxs-lookup"><span data-stu-id="90298-129">The emphasis is on "separation of concerns" (processing, data, and UI layers).</span></span>

<span data-ttu-id="90298-130">這三種架構完全受到支援，並繼續由 ASP.NET 小組開發。</span><span class="sxs-lookup"><span data-stu-id="90298-130">All three frameworks are fully supported and continue to be developed by the ASP.NET team.</span></span> <span data-ttu-id="90298-131">一般而言，選擇要使用的架構取決於您的背景和 ASP.NET 體驗。</span><span class="sxs-lookup"><span data-stu-id="90298-131">In general, the choice of which framework to use depends on your background and experience with ASP.NET.</span></span>

<span data-ttu-id="90298-132">具體而言，ASP.NET Web Pages 的設計，是為了讓已經知道 HTML 的人能夠輕鬆地將伺服器處理新增至他們的網頁。</span><span class="sxs-lookup"><span data-stu-id="90298-132">ASP.NET Web Pages in particular was designed to make it easy for people who already know HTML to add server processing to their pages.</span></span> <span data-ttu-id="90298-133">這是適用于學生、業餘人士、一般人對程式設計新手的絕佳選擇。</span><span class="sxs-lookup"><span data-stu-id="90298-133">It's a good choice for students, hobbyists, people in general who are new to programming.</span></span> <span data-ttu-id="90298-134">對於擁有 non-ASP.NET web 技術經驗的開發人員而言，這也是不錯的選擇。</span><span class="sxs-lookup"><span data-stu-id="90298-134">It can also be a good choice for developers who have experience with non-ASP.NET web technologies.</span></span>

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a><span data-ttu-id="90298-135">我需要 WebMatrix 才能使用網頁嗎？</span><span class="sxs-lookup"><span data-stu-id="90298-135">Do I need WebMatrix in order to work with Web Pages?</span></span>

<span data-ttu-id="90298-136">不會。</span><span class="sxs-lookup"><span data-stu-id="90298-136">No.</span></span> <span data-ttu-id="90298-137">不再建議使用 WebMatrix 做為 ASP.NET Web Pages 的整合式開發環境。</span><span class="sxs-lookup"><span data-stu-id="90298-137">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="90298-138">使用[Visual Studio](program-asp-net-web-pages-in-visual-studio.md)或[Visual Studio Code](https://code.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="90298-138">Use [Visual Studio](program-asp-net-web-pages-in-visual-studio.md) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>

<span data-ttu-id="90298-139">如果您不想要使用 Visual Studio 或 Visual Studio Code，您可以使用[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)個別安裝元件產品。</span><span class="sxs-lookup"><span data-stu-id="90298-139">If you don't want to use either Visual Studio or Visual Studio Code, you can install the component products individually using [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span> <span data-ttu-id="90298-140">您需要下列產品：</span><span class="sxs-lookup"><span data-stu-id="90298-140">You need the following products:</span></span>

- <span data-ttu-id="90298-141">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="90298-141">Microsoft .NET Framework 4.5</span></span>
- <span data-ttu-id="90298-142">ASP.NET MVC 5 （也會安裝 ASP.NET Web Pages framework）</span><span class="sxs-lookup"><span data-stu-id="90298-142">ASP.NET MVC 5 (which installs the ASP.NET Web Pages framework as well)</span></span>
- <span data-ttu-id="90298-143">IIS Express （web 伺服器）</span><span class="sxs-lookup"><span data-stu-id="90298-143">IIS Express (the web server)</span></span>
- <span data-ttu-id="90298-144">Microsoft SQL Server Compact 4.0 （資料庫）</span><span class="sxs-lookup"><span data-stu-id="90298-144">Microsoft SQL Server Compact 4.0 (the database)</span></span>

<span data-ttu-id="90298-145">您可以使用文字編輯器來編輯*cshtml* （或*vbhtml*）頁面。</span><span class="sxs-lookup"><span data-stu-id="90298-145">You can use a text editor to edit *.cshtml* (or *.vbhtml*) pages.</span></span>

<span data-ttu-id="90298-146">不使用工具管理 SQL Server Compact 資料庫（ *.sdf*檔案）會有點困難。</span><span class="sxs-lookup"><span data-stu-id="90298-146">Managing SQL Server Compact databases (*.sdf* files) without a tool is a bit harder.</span></span> <span data-ttu-id="90298-147">Visual Studio 用來管理 *.sdf*資料庫的 containds 工具。</span><span class="sxs-lookup"><span data-stu-id="90298-147">Visual Studio containds tools for managing *.sdf* databases.</span></span> <span data-ttu-id="90298-148">您也可以在程式碼中執行 SQL 命令，以執行許多 SQL Server 管理工作。</span><span class="sxs-lookup"><span data-stu-id="90298-148">You can also run SQL commands in code to perform many SQL Server management tasks.</span></span>

<span data-ttu-id="90298-149">若要在不使用整合式開發環境（IDE）的情況下測試*cshtml*頁面，您可以將它們部署到即時伺服器。</span><span class="sxs-lookup"><span data-stu-id="90298-149">To test *.cshtml* pages without using an integrated development environment (IDE), you can deploy them to a live server.</span></span> <span data-ttu-id="90298-150">（請參閱[我可以部署 ASP.NET Web Pages 網站而不使用 WebMatrix 嗎？](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)）</span><span class="sxs-lookup"><span data-stu-id="90298-150">(See [Can I deploy an ASP.NET Web Pages site without using WebMatrix?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix))</span></span>

### <a name="running-iis-express-without-using-an-ide"></a><span data-ttu-id="90298-151">在不使用 IDE 的情況下執行 IIS Express</span><span class="sxs-lookup"><span data-stu-id="90298-151">Running IIS Express without using an IDE</span></span>

<span data-ttu-id="90298-152">如果您在電腦上將 IIS Express 安裝為 web 伺服器，您可以使用它來測試頁面。</span><span class="sxs-lookup"><span data-stu-id="90298-152">If you install IIS Express on your computer as a web server, you can use that to test the pages.</span></span> <span data-ttu-id="90298-153">您可以從命令列執行 IIS Express，並將它與特定埠號碼產生關聯。</span><span class="sxs-lookup"><span data-stu-id="90298-153">You can run IIS Express from the command line and associate it with a specific port number.</span></span> <span data-ttu-id="90298-154">然後，當您在瀏覽器中要求*cshtml*檔案時，您可以指定該埠。</span><span class="sxs-lookup"><span data-stu-id="90298-154">You then specify that port when you request *.cshtml* files in your browser.</span></span>

<span data-ttu-id="90298-155">在 Windows 中，以系統管理員許可權開啟命令提示字元，並變更為*C:\Program Files\IIS Express。*</span><span class="sxs-lookup"><span data-stu-id="90298-155">In Windows, open a command prompt with administrator privileges and change to *C:\Program Files\IIS Express.*</span></span> <span data-ttu-id="90298-156">（若是64位系統，請使用*C:\Program Files （x86） \IIS Express 資料夾）。* 然後，使用您網站的實際路徑輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="90298-156">(For 64-bit systems, use the folder *C:\Program Files (x86)\IIS Express.)* Then enter the following command, using the actual path to your site:</span></span>

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

<span data-ttu-id="90298-157">您可以使用其他進程尚未保留的任何埠號碼。</span><span class="sxs-lookup"><span data-stu-id="90298-157">You can use any port number that isn't already reserved by some other process.</span></span> <span data-ttu-id="90298-158">（1024以上的埠號碼通常是免費的）。針對 `path` 值，請使用 *. cshtml*檔案所在之網站資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="90298-158">(Port numbers above 1024 are typically free.) For the `path` value, use the path of the website folder where the *.cshtml* files are.</span></span>

<span data-ttu-id="90298-159">執行此命令來設定 IIS Express 以提供您的頁面之後，您可以開啟瀏覽器並流覽至*cshtml*檔案。</span><span class="sxs-lookup"><span data-stu-id="90298-159">After you run this command to set up IIS Express to serve your pages, you can open a browser and browse to a *.cshtml* file.</span></span> <span data-ttu-id="90298-160">使用如下所示的 URL：</span><span class="sxs-lookup"><span data-stu-id="90298-160">Use a URL like the following:</span></span>

`http://localhost:35896/default.cshtml`

<span data-ttu-id="90298-161">如需 IIS Express 命令列選項的說明，請在命令列中輸入 `iisexpress.exe /?`。</span><span class="sxs-lookup"><span data-stu-id="90298-161">For help with IIS Express command line options, enter `iisexpress.exe /?` at the command line.</span></span>

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a><span data-ttu-id="90298-162">我可以在網頁頁面上使用 ASP.NET Web Forms 控制項嗎？</span><span class="sxs-lookup"><span data-stu-id="90298-162">Can I use ASP.NET Web Forms controls on a Web Pages page?</span></span>

<span data-ttu-id="90298-163">不會。</span><span class="sxs-lookup"><span data-stu-id="90298-163">No.</span></span> <span data-ttu-id="90298-164">Web form 控制項（如[CheckBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox)控制項、[驗證控制項](https://msdn.microsoft.com/library/bwd43d0x)和[GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview)控制項）只適用于 web form 頁面（ *.aspx*檔案）。</span><span class="sxs-lookup"><span data-stu-id="90298-164">Web Forms controls like the [CheckBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox) control, the [validation controls](https://msdn.microsoft.com/library/bwd43d0x), and the [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview) control only work in Web Forms pages (*.aspx* files).</span></span> <span data-ttu-id="90298-165">這些控制項需要 Web Forms 頁面架構。</span><span class="sxs-lookup"><span data-stu-id="90298-165">These controls require the Web Forms page framework.</span></span>

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a><span data-ttu-id="90298-166">我可以在不使用 WebMatrix 的情況下部署 ASP.NET Web Pages 網站嗎？</span><span class="sxs-lookup"><span data-stu-id="90298-166">Can I deploy an ASP.NET Web Pages site without using WebMatrix?</span></span>

<span data-ttu-id="90298-167">可以。</span><span class="sxs-lookup"><span data-stu-id="90298-167">Yes.</span></span> <span data-ttu-id="90298-168">您可以手動將網站檔案複製到伺服器（通常是使用 FTP）。</span><span class="sxs-lookup"><span data-stu-id="90298-168">You can manually copy website files to a server (typically by using FTP).</span></span> <span data-ttu-id="90298-169">如果您執行手動複製，則也必須複製支援 SQL Server Compact 的檔案（資料庫）。</span><span class="sxs-lookup"><span data-stu-id="90298-169">If you perform a manual copy, you also have to copy the files that support SQL Server Compact (the database).</span></span> <span data-ttu-id="90298-170">如需詳細資訊，請參閱在[不使用工具的情況下部署網頁應用程式](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317)的 blog 專案。</span><span class="sxs-lookup"><span data-stu-id="90298-170">For details, see the blog entry [Deploying Web Pages applications without a tool](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317).</span></span>

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a><span data-ttu-id="90298-171">我是否必須使用 WebSecurity helper 來支援登入？</span><span class="sxs-lookup"><span data-stu-id="90298-171">Do I have to use the WebSecurity helper to support logins?</span></span>

<span data-ttu-id="90298-172">不會。</span><span class="sxs-lookup"><span data-stu-id="90298-172">No.</span></span> <span data-ttu-id="90298-173">屬於 ASP.NET Web Pages 一部分的 `SimpleMembership` 提供者就是其中一個選項。</span><span class="sxs-lookup"><span data-stu-id="90298-173">The `SimpleMembership` provider that is part of ASP.NET Web Pages is one option.</span></span> <span data-ttu-id="90298-174">也可以使用屬於 ASP.NET 一部分的安全性提供者（您可以在 Web form 中用來處理）。</span><span class="sxs-lookup"><span data-stu-id="90298-174">The security providers that are part of ASP.NET (that you might be used to working with in Web Forms) are also available.</span></span> <span data-ttu-id="90298-175">例如，您可以在 ASP.NET Web Pages 中使用表單驗證，就像在 Web Forms 中一樣。</span><span class="sxs-lookup"><span data-stu-id="90298-175">For example, you can use forms authentication in ASP.NET Web Pages just as you would in Web Forms.</span></span> <span data-ttu-id="90298-176">如需如何使用表單驗證的其中一個範例，Microsoft 支援服務請參閱[如何使用C#.Net 在 ASP.NET 應用程式中執行以表單為基礎的驗證](https://support.microsoft.com/kb/301240)一文。</span><span class="sxs-lookup"><span data-stu-id="90298-176">For one example of how to use forms authentication, see the Microsoft Support article [How To Implement Forms-Based Authentication in Your ASP.NET Application by Using C#.NET](https://support.microsoft.com/kb/301240).</span></span> <span data-ttu-id="90298-177">若要下載簡單的範例，請參閱[ASP.NET 版本的 < 登入 &amp; 密碼](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm)。</span><span class="sxs-lookup"><span data-stu-id="90298-177">To download a simple example, see [ASP.NET version of "Login &amp; Password](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm).</span></span>

<span data-ttu-id="90298-178">如需如何使用 Windows 驗證的相關資訊，請參閱[在 ASP.NET Web Pages 中使用 windows 驗證](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298)的 blog 文章。</span><span class="sxs-lookup"><span data-stu-id="90298-178">For information about how to use Windows authentication, see the blog post [Using Windows authentication in ASP.NET Web Pages](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298).</span></span>

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a><span data-ttu-id="90298-179">ASP.NET Web Pages 支援 HTML5 嗎？</span><span class="sxs-lookup"><span data-stu-id="90298-179">Does ASP.NET Web Pages support HTML5?</span></span>

<span data-ttu-id="90298-180">可以。</span><span class="sxs-lookup"><span data-stu-id="90298-180">Yes.</span></span> <span data-ttu-id="90298-181">您使用 ASP.NET Web Pages （ *. cshtml*或*vbhtml*頁面）建立的頁面基本上是 HTML 頁面，其中包含在伺服器上執行的程式碼，然後才呈現頁面。</span><span class="sxs-lookup"><span data-stu-id="90298-181">The pages you create with ASP.NET Web Pages (*.cshtml* or *.vbhtml* pages) are essentially HTML pages that also contain code that runs on the server, before the page is rendered.</span></span> <span data-ttu-id="90298-182">只要使用者的瀏覽器支援 HTML5，您就可以使用 [ *cshtml* ] 或 [ *vbhtml* ] 頁面中的 html5 元素。</span><span class="sxs-lookup"><span data-stu-id="90298-182">As long as the user's browser supports HTML5, you can use HTML5 elements in a *.cshtml* or *.vbhtml* page.</span></span>

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a><span data-ttu-id="90298-183">我可以搭配網頁使用 JavaScript 和 jQuery 嗎？</span><span class="sxs-lookup"><span data-stu-id="90298-183">Can I use JavaScript and jQuery with Web Pages?</span></span>

<span data-ttu-id="90298-184">當然可以。</span><span class="sxs-lookup"><span data-stu-id="90298-184">Absolutely.</span></span> <span data-ttu-id="90298-185">您使用 ASP.NET Web Pages （ *. cshtml*或*vbhtml*頁面）建立的頁面只是包含伺服器程式碼的 HTML 網頁。</span><span class="sxs-lookup"><span data-stu-id="90298-185">The pages you create with ASP.NET Web Pages (*.cshtml* or *.vbhtml* pages) are just HTML pages with server code in them.</span></span> <span data-ttu-id="90298-186">因此，您可以在一般 HTML 網頁中使用 JavaScript 或 jQuery 來執行的任何動作，也可以在*cshtml*或*vbhtml*頁面中執行。</span><span class="sxs-lookup"><span data-stu-id="90298-186">Therefore, anything you can do in a normal HTML page by using JavaScript or jQuery you can also do in a *.cshtml* or *.vbhtml* page.</span></span>

<span data-ttu-id="90298-187">WebMatrix 中的**入門網站**範本包含許多 jQuery 程式庫。</span><span class="sxs-lookup"><span data-stu-id="90298-187">The **Starter Site** template in WebMatrix contains a number of jQuery libraries.</span></span> <span data-ttu-id="90298-188">如果您使用該範本建立網站，[*腳本*] 資料夾中會包含 jquery core 程式庫（*jquery-1.7.2.min.js 1.6.2）* 和 jquery 驗證的程式庫（*jquery. validate. 驗證 .js*等等）。</span><span class="sxs-lookup"><span data-stu-id="90298-188">If you create a site by using that template, the *Scripts* folder contains a jQuery core library (*jquery-1.6.2.js)* and libraries for jQuery validation (*jquery.validate.js*, etc.).</span></span>

<span data-ttu-id="90298-189">以下是一些會說明如何搭配 ASP.NET Web Pages 使用 jQuery 的方式的 blog 文章：</span><span class="sxs-lookup"><span data-stu-id="90298-189">Here are some blog posts that illustrate ways to use jQuery with ASP.NET Web Pages:</span></span>

- <span data-ttu-id="90298-190">透過 Rachel Appel[將 jQuery 的使用方式新增至 ASP.NET Web Pages](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/)</span><span class="sxs-lookup"><span data-stu-id="90298-190">[Adding jQuery Goodness to ASP.NET Web Pages using WebMatrix](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/) by Rachel Appel</span></span>
- <span data-ttu-id="90298-191">[5 分鐘： WebMatrix + JQUERY UI + json + jquery 範本](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/)By Jonas Eriksson</span><span class="sxs-lookup"><span data-stu-id="90298-191">[5 min: WebMatrix + jQuery UI + json + jQuery templates](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/) by Jonas Eriksson</span></span>
- <span data-ttu-id="90298-192">Mike Brind 的[WebMatrix 和 JQuery 表單](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms)</span><span class="sxs-lookup"><span data-stu-id="90298-192">[WebMatrix And jQuery Forms](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms) by Mike Brind</span></span>

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="90298-193">其他資源</span><span class="sxs-lookup"><span data-stu-id="90298-193">Additional Resources</span></span>

[<span data-ttu-id="90298-194">ASP.NET Web Pages (Razor) 疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="90298-194">ASP.NET Web Pages (Razor) Troubleshooting Guide</span></span>](https://go.microsoft.com/fwlink/?LinkId=253001)

<span data-ttu-id="90298-195">ASP.NET 網站上的[WebMatrix 和 ASP.NET Web Pages 論壇](https://forums.asp.net/1224.aspx/1?WebMatrix)</span><span class="sxs-lookup"><span data-stu-id="90298-195">[WebMatrix and ASP.NET Web Pages forum](https://forums.asp.net/1224.aspx/1?WebMatrix) on the ASP.NET website</span></span>
