---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
title: 單一登入（使用 Azure 建立真實世界的雲端應用程式） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 電子書建立真實世界的雲端應用程式，是以 Scott Guthrie 所開發的簡報為基礎。 它會說明13個模式和實務，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 7d82d5e9-0619-4f22-9e03-32a6d52940a5
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
msc.type: authoredcontent
ms.openlocfilehash: 7e32f444dc38132296cffd45ac658f5abf51f314
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74585273"
---
# <a name="single-sign-on-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="298a7-104">單一登入（使用 Azure 建立真實世界的雲端應用程式）</span><span class="sxs-lookup"><span data-stu-id="298a7-104">Single Sign-On (Building Real-World Cloud Apps with Azure)</span></span>

<span data-ttu-id="298a7-105">由[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="298a7-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="298a7-106">[下載 Fix It 專案](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下載電子書](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="298a7-106">[Download Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="298a7-107">**使用 Azure 電子書建立真實世界的雲端應用程式**，是以 Scott Guthrie 所開發的簡報為基礎。</span><span class="sxs-lookup"><span data-stu-id="298a7-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="298a7-108">其中說明13種模式和作法，可協助您成功開發雲端 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="298a7-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="298a7-109">如需電子書的相關資訊，請參閱[第一章](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="298a7-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="298a7-110">當您開發雲端應用程式時，需要考慮許多安全性問題，但在此系列中，我們只著重于單一登入。</span><span class="sxs-lookup"><span data-stu-id="298a7-110">There are many security issues to think about when you're developing a cloud app, but for this series we'll focus on just one: single sign-on.</span></span> <span data-ttu-id="298a7-111">人們常問的一個問題是：「我主要為公司的員工建立應用程式;如何在雲端中裝載這些應用程式，並讓他們能夠使用我的員工在內部部署環境中所知道和使用的相同安全性模型，以執行裝載于防火牆內的應用程式？</span><span class="sxs-lookup"><span data-stu-id="298a7-111">A question people often ask is this: "I'm primarily building apps for the employees of my company; how do I host these apps in the cloud and still enable them to use the same security model that my employees know and use in the on-premises environment when they're running apps that are hosted inside the firewall?"</span></span> <span data-ttu-id="298a7-112">我們啟用此案例的其中一種方式，稱為 Azure Active Directory （Azure AD）。</span><span class="sxs-lookup"><span data-stu-id="298a7-112">One of the ways we enable this scenario is called Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="298a7-113">Azure AD 可讓您透過網際網路提供企業營運（LOB）應用程式，讓您也可以將這些應用程式提供給商務合作夥伴。</span><span class="sxs-lookup"><span data-stu-id="298a7-113">Azure AD enables you to make enterprise line-of-business (LOB) apps available over the Internet, and it enables you to make these apps available to business partners as well.</span></span>

## <a name="introduction-to-azure-ad"></a><span data-ttu-id="298a7-114">Azure AD 簡介</span><span class="sxs-lookup"><span data-stu-id="298a7-114">Introduction to Azure AD</span></span>

<span data-ttu-id="298a7-115">[Azure AD](https://docs.microsoft.com/azure/active-directory/)在雲端中提供[Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="298a7-115">[Azure AD](https://docs.microsoft.com/azure/active-directory/) provides [Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx) in the cloud.</span></span> <span data-ttu-id="298a7-116">主要功能包括下列各項：</span><span class="sxs-lookup"><span data-stu-id="298a7-116">Key features include the following:</span></span>

- <span data-ttu-id="298a7-117">它會與內部部署 Active Directory 整合。</span><span class="sxs-lookup"><span data-stu-id="298a7-117">It integrates with on-premises Active Directory.</span></span>
- <span data-ttu-id="298a7-118">它可讓您使用您的應用程式進行單一登入。</span><span class="sxs-lookup"><span data-stu-id="298a7-118">It enables single sign-on with your apps.</span></span>
- <span data-ttu-id="298a7-119">它支援開放式標準，例如[SAML](http://en.wikipedia.org/wiki/SAML_2.0)、 [WS-送](http://en.wikipedia.org/wiki/WS-Federation)出和[OAuth 2.0](http://oauth.net/2/)。</span><span class="sxs-lookup"><span data-stu-id="298a7-119">It supports open standards such as [SAML](http://en.wikipedia.org/wiki/SAML_2.0), [WS-Fed](http://en.wikipedia.org/wiki/WS-Federation), and [OAuth 2.0](http://oauth.net/2/).</span></span>
- <span data-ttu-id="298a7-120">它支援 Enterprise [Graph REST API](https://msdn.microsoft.com/library/hh974476.aspx)。</span><span class="sxs-lookup"><span data-stu-id="298a7-120">It supports Enterprise [Graph REST API](https://msdn.microsoft.com/library/hh974476.aspx).</span></span>

<span data-ttu-id="298a7-121">假設您有內部部署 Windows Server Active Directory 環境，可用來讓員工登入內部網路應用程式：</span><span class="sxs-lookup"><span data-stu-id="298a7-121">Suppose you have an on-premises Windows Server Active Directory environment that you use to enable employees to sign on to Intranet apps:</span></span>

![](single-sign-on/_static/image1.png)

<span data-ttu-id="298a7-122">Azure AD 可讓您在雲端中建立目錄。</span><span class="sxs-lookup"><span data-stu-id="298a7-122">What Azure AD enables you to do is create a directory in the cloud.</span></span> <span data-ttu-id="298a7-123">這是一項免費功能，而且很容易設定。</span><span class="sxs-lookup"><span data-stu-id="298a7-123">It's a free feature and easy to set up.</span></span>

<span data-ttu-id="298a7-124">它可以完全獨立于內部部署 Active Directory;您可以將任何想要的人放在其中，並在網際網路應用程式中進行驗證。</span><span class="sxs-lookup"><span data-stu-id="298a7-124">It can be entirely independent from your on-premises Active Directory; you can put anyone you want in it and authenticate them in Internet apps.</span></span>

![Windows Azure Active Directory](single-sign-on/_static/image2.png)

<span data-ttu-id="298a7-126">或者，您也可以將它與您的內部部署 AD 整合。</span><span class="sxs-lookup"><span data-stu-id="298a7-126">Or you can integrate it with your on-premises AD.</span></span>

![AD 與 WAAD 整合](single-sign-on/_static/image3.png)

<span data-ttu-id="298a7-128">現在，可以在內部部署驗證的所有員工也可以透過網際網路進行驗證，而不需要開啟防火牆或在您的資料中心部署任何新的伺服器。</span><span class="sxs-lookup"><span data-stu-id="298a7-128">Now all the employees who can authenticate on-premises can also authenticate over the Internet – without you having to open up a firewall or deploy any new servers in your data center.</span></span> <span data-ttu-id="298a7-129">您可以繼續利用您知道並使用的所有現有 Active Directory 環境，讓您的內部應用程式單一登入功能。</span><span class="sxs-lookup"><span data-stu-id="298a7-129">You can continue to leverage all the existing Active Directory environment that you know and use today to give your internal apps single-sign on capability.</span></span>

<span data-ttu-id="298a7-130">在 AD 與 Azure AD 之間進行此連線之後，您也可以讓 web 應用程式和行動裝置在雲端中驗證您的員工，而且您可以啟用協力廠商應用程式（例如 Office 365、SalesForce.com 或 Google apps）以接受您的員工的認證。</span><span class="sxs-lookup"><span data-stu-id="298a7-130">Once you've made this connection between AD and Azure AD, you can also enable your web apps and your mobile devices to authenticate your employees in the cloud, and you can enable third-party apps, such as Office 365, SalesForce.com, or Google apps, to accept your employees' credentials.</span></span> <span data-ttu-id="298a7-131">如果您使用的是 Office 365，表示您已經設定 Azure AD，因為 Office 365 會使用 Azure AD 進行驗證和授權。</span><span class="sxs-lookup"><span data-stu-id="298a7-131">If you're using Office 365, you're already set up with Azure AD because Office 365 uses Azure AD for authentication and authorization.</span></span>

![協力廠商應用程式](single-sign-on/_static/image4.png)

<span data-ttu-id="298a7-133">這種方法的優點是，每當您的組織新增或刪除使用者，或使用者變更密碼時，您就會使用您目前在內部部署環境中使用的相同程式。</span><span class="sxs-lookup"><span data-stu-id="298a7-133">The beauty of this approach is that any time your organization adds or deletes a user, or a user changes a password, you use the same process that you use today in your on-premises environment.</span></span> <span data-ttu-id="298a7-134">您的所有內部部署 AD 變更都會自動傳播到雲端環境。</span><span class="sxs-lookup"><span data-stu-id="298a7-134">All of your on-premises AD changes are automatically propagated to the cloud environment.</span></span>

<span data-ttu-id="298a7-135">如果您的公司使用或移至 Office 365，好消息是您會自動設定 Azure AD，因為 Office 365 會使用 Azure AD 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="298a7-135">If your company is using or moving to Office 365, the good news is that you'll have Azure AD set up automatically because Office 365 uses Azure AD for authentication.</span></span> <span data-ttu-id="298a7-136">因此，您可以輕鬆地在自己的應用程式中使用 Office 365 所使用的相同驗證。</span><span class="sxs-lookup"><span data-stu-id="298a7-136">So you can easily use in your own apps the same authentication that Office 365 uses.</span></span>

## <a name="set-up-an-azure-ad-tenant"></a><span data-ttu-id="298a7-137">設定 Azure AD 租使用者</span><span class="sxs-lookup"><span data-stu-id="298a7-137">Set up an Azure AD tenant</span></span>

<span data-ttu-id="298a7-138">Azure AD 目錄稱為 Azure AD[租](https://technet.microsoft.com/library/jj573650.aspx)使用者，而設定租使用者相當簡單。</span><span class="sxs-lookup"><span data-stu-id="298a7-138">an Azure AD directory is called an Azure AD [tenant](https://technet.microsoft.com/library/jj573650.aspx), and setting up a tenant is pretty easy.</span></span> <span data-ttu-id="298a7-139">我們會示範如何在 Azure 管理入口網站中完成，以說明概念，但當然也像是其他入口網站功能，您也可以使用腳本或管理 API 來執行此作業。</span><span class="sxs-lookup"><span data-stu-id="298a7-139">We'll show you how it's done in the Azure Management Portal in order to illustrate the concepts, but of course like the other portal functions you can also do it by using a script or management API.</span></span>

<span data-ttu-id="298a7-140">在管理入口網站中，按一下 [Active Directory] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="298a7-140">In the management portal click the Active Directory tab.</span></span>

![入口網站中的 WAAD](single-sign-on/_static/image5.png)

<span data-ttu-id="298a7-142">您的 Azure 帳戶會自動有一個 Azure AD 租使用者，而且您可以按一下頁面底部的 [**新增**] 按鈕，以建立其他目錄。</span><span class="sxs-lookup"><span data-stu-id="298a7-142">You automatically have one Azure AD tenant for your Azure account, and you can click the **Add** button at the bottom of the page to create additional directories.</span></span> <span data-ttu-id="298a7-143">例如，您可能會想要一個用於測試環境，另一個用於生產環境。</span><span class="sxs-lookup"><span data-stu-id="298a7-143">You might want one for a test environment and one for production, for example.</span></span> <span data-ttu-id="298a7-144">請仔細考慮您為新目錄命名的內容。</span><span class="sxs-lookup"><span data-stu-id="298a7-144">Think carefully about what you name a new directory.</span></span> <span data-ttu-id="298a7-145">如果您使用目錄的名稱，然後再為其中一位使用者再次使用您的名稱，這可能會造成混淆。</span><span class="sxs-lookup"><span data-stu-id="298a7-145">If you use your name for the directory and then you use your name again for one of the users, that can be confusing.</span></span>

![加入目錄](single-sign-on/_static/image6.png)

<span data-ttu-id="298a7-147">入口網站具有在此環境內建立、刪除及管理使用者的完整支援。</span><span class="sxs-lookup"><span data-stu-id="298a7-147">The portal has full support for creating, deleting, and managing users within this environment.</span></span> <span data-ttu-id="298a7-148">例如，若要新增使用者，請移至 [**使用者**] 索引標籤，然後按一下 [**新增使用者**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="298a7-148">For example, to add a user go to the **Users** tab and click the **Add User** button.</span></span>

![[新增使用者] 按鈕](single-sign-on/_static/image7.png)

![[新增使用者] 對話方塊](single-sign-on/_static/image8.png)

<span data-ttu-id="298a7-151">您可以建立僅存在於此目錄中的新使用者，或者您可以在此目錄中將 Microsoft 帳戶註冊為使用者，或在此目錄中註冊為使用者，或從另一個 Azure AD 目錄登錄或使用者。</span><span class="sxs-lookup"><span data-stu-id="298a7-151">You can create a new user who exists only in this directory, or you can register a Microsoft Account as a user in this directory, or register or a user from another Azure AD directory as a user in this directory.</span></span> <span data-ttu-id="298a7-152">（在實際目錄中，預設網域會是 ContosoTest.onmicrosoft.com。</span><span class="sxs-lookup"><span data-stu-id="298a7-152">(In a real directory, the default domain would be ContosoTest.onmicrosoft.com.</span></span> <span data-ttu-id="298a7-153">您也可以使用自己選擇的網域，例如 contoso.com。）</span><span class="sxs-lookup"><span data-stu-id="298a7-153">You can also use a domain of your own choosing, like contoso.com.)</span></span>

![使用者類型](single-sign-on/_static/image9.png)

![[新增使用者] 對話方塊](single-sign-on/_static/image10.png)

<span data-ttu-id="298a7-156">您可以將使用者指派給角色。</span><span class="sxs-lookup"><span data-stu-id="298a7-156">You can assign the user to a role.</span></span>

![使用者設定檔](single-sign-on/_static/image11.png)

<span data-ttu-id="298a7-158">並使用暫時密碼建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="298a7-158">And the account is created with a temporary password.</span></span>

![暫時密碼](single-sign-on/_static/image12.png)

<span data-ttu-id="298a7-160">您以這種方式建立的使用者可以立即使用此雲端目錄登入您的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="298a7-160">The users you create this way can immediately log in to your web apps using this cloud directory.</span></span>

<span data-ttu-id="298a7-161">不過，「企業單一登入」的絕佳功能是 [**目錄整合**] 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="298a7-161">What's great for enterprise single sign-on, though, is the **Directory Integration** tab:</span></span>

![[目錄整合] 索引標籤](single-sign-on/_static/image13.png)

<span data-ttu-id="298a7-163">如果您啟用目錄整合，並[下載工具](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)，您可以將此雲端目錄與您已在組織內使用的現有內部部署 Active Directory 同步。</span><span class="sxs-lookup"><span data-stu-id="298a7-163">If you enable directory integration, and [download a tool](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx), you can sync this cloud directory with your existing on-premises Active Directory that you're already using inside your organization.</span></span> <span data-ttu-id="298a7-164">然後，儲存在您目錄中的所有使用者都會顯示在此雲端目錄中。</span><span class="sxs-lookup"><span data-stu-id="298a7-164">Then all of the users stored in your directory will show up in this cloud directory.</span></span> <span data-ttu-id="298a7-165">您的雲端應用程式現在可以使用現有的 Active Directory 認證來驗證您的所有員工。</span><span class="sxs-lookup"><span data-stu-id="298a7-165">Your cloud apps can now authenticate all of your employees using their existing Active Directory credentials.</span></span> <span data-ttu-id="298a7-166">而且這一切都是免費的–同步處理工具和 Azure AD 本身。</span><span class="sxs-lookup"><span data-stu-id="298a7-166">And all this is free – both the sync tool and Azure AD itself.</span></span>

<span data-ttu-id="298a7-167">此工具是便於使用的 wizard，您可以從這些螢幕擷取畫面查看。</span><span class="sxs-lookup"><span data-stu-id="298a7-167">The tool is a wizard that is easy to use, as you can see from these screen shots.</span></span> <span data-ttu-id="298a7-168">這些不是完整的指示，只是示範基本程式的範例。</span><span class="sxs-lookup"><span data-stu-id="298a7-168">These are not complete instructions, just an example showing you the basic process.</span></span> <span data-ttu-id="298a7-169">如需更詳細的「作法」資訊，請參閱本章結尾的 Resources （[資源](#resources)）一節中的連結。</span><span class="sxs-lookup"><span data-stu-id="298a7-169">For more detailed how-to-do-it information, see the links in the [Resources](#resources) section at the end of the chapter.</span></span>

![WAAD 同步處理工具設定向導](single-sign-on/_static/image14.png)

<span data-ttu-id="298a7-171">按 **[下一步]** ，然後輸入您的 Azure Active Directory 認證。</span><span class="sxs-lookup"><span data-stu-id="298a7-171">Click **Next**, and then enter your Azure Active Directory credentials.</span></span>

![WAAD 同步處理工具設定向導](single-sign-on/_static/image15.png)

<span data-ttu-id="298a7-173">按 **[下一步]** ，然後輸入您的內部部署 AD 認證。</span><span class="sxs-lookup"><span data-stu-id="298a7-173">Click **Next**, and then enter your on-premises AD credentials.</span></span>

![WAAD 同步處理工具設定向導](single-sign-on/_static/image16.png)

<span data-ttu-id="298a7-175">按 **[下一步]** ，然後指出您是否想要將 AD 密碼雜湊儲存在雲端中。</span><span class="sxs-lookup"><span data-stu-id="298a7-175">Click **Next**, and then indicate if you want to store a hash of your AD passwords in the cloud.</span></span>

![WAAD 同步處理工具設定向導](single-sign-on/_static/image17.png)

<span data-ttu-id="298a7-177">您可以儲存在雲端中的密碼雜湊是單向雜湊;實際的密碼永遠不會儲存在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="298a7-177">The password hash that you can store in the cloud is a one-way hash; actual passwords are never stored in Azure AD.</span></span> <span data-ttu-id="298a7-178">如果您決定不將雜湊儲存在雲端中，您必須使用[Active Directory 同盟服務](https://technet.microsoft.com/library/hh831502.aspx)（ADFS）。</span><span class="sxs-lookup"><span data-stu-id="298a7-178">If you decide against storing hashes in the cloud, you'll have to use [Active Directory Federation Services](https://technet.microsoft.com/library/hh831502.aspx) (ADFS).</span></span> <span data-ttu-id="298a7-179">[選擇是否要使用 ADFS 時，還有其他因素需要考慮](https://technet.microsoft.com/library/jj573653.aspx)。</span><span class="sxs-lookup"><span data-stu-id="298a7-179">There are also [other factors to consider when choosing whether or not to use ADFS](https://technet.microsoft.com/library/jj573653.aspx).</span></span> <span data-ttu-id="298a7-180">ADFS 選項需要一些額外的設定步驟。</span><span class="sxs-lookup"><span data-stu-id="298a7-180">The ADFS option requires a few additional configuration steps.</span></span>

<span data-ttu-id="298a7-181">如果您選擇將雜湊儲存在雲端中，您就完成了，而且當您按 **[下一步]** 時，工具就會開始同步處理目錄。</span><span class="sxs-lookup"><span data-stu-id="298a7-181">If you choose to store hashes in the cloud, you're done, and the tool starts synchronizing directories when you click **Next**.</span></span>

![WAAD 同步處理工具設定向導](single-sign-on/_static/image18.png)

<span data-ttu-id="298a7-183">幾分鐘後您就完成了。</span><span class="sxs-lookup"><span data-stu-id="298a7-183">And in a few minutes you're done.</span></span>

![WAAD 同步處理工具設定向導](single-sign-on/_static/image19.png)

<span data-ttu-id="298a7-185">在 Windows 2003 或更新版本的組織中，您只需要在一個網域控制站上執行此功能。</span><span class="sxs-lookup"><span data-stu-id="298a7-185">You only have to run this on one domain controller in the organization, on Windows 2003 or higher.</span></span> <span data-ttu-id="298a7-186">而不需要重新開機。</span><span class="sxs-lookup"><span data-stu-id="298a7-186">And no need to reboot.</span></span> <span data-ttu-id="298a7-187">當您完成時，您的所有使用者都在雲端中，而且您可以使用 SAML、OAuth 或 WS-ADDRESSING，從任何 web 或行動應用程式進行單一登入。</span><span class="sxs-lookup"><span data-stu-id="298a7-187">When you're done, all of your users are in the cloud and you can do single sign-on from any web or mobile application, using SAML, OAuth, or WS-Fed.</span></span>

<span data-ttu-id="298a7-188">有時候我們會詢問您如何保護這一點– Microsoft 是否將它用於自己的機密商務資料？</span><span class="sxs-lookup"><span data-stu-id="298a7-188">Sometimes we get asked about how secure this is – does Microsoft use it for their own sensitive business data?</span></span> <span data-ttu-id="298a7-189">答案是肯定的。</span><span class="sxs-lookup"><span data-stu-id="298a7-189">And the answer is yes we do.</span></span> <span data-ttu-id="298a7-190">例如，如果您移至[https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/)的內部 Microsoft SharePoint 網站，系統會提示您登入。</span><span class="sxs-lookup"><span data-stu-id="298a7-190">For example, if you go to the internal Microsoft SharePoint site at [https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/), you get prompted to log in.</span></span>

![Office 365 登入](single-sign-on/_static/image20.png)

<span data-ttu-id="298a7-192">Microsoft 已啟用 ADFS，因此當您輸入 Microsoft ID 時，您會被重新導向至 ADFS 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="298a7-192">Microsoft has enabled ADFS, so when you enter a Microsoft ID, you get redirected to an ADFS log-in page.</span></span>

![ADFS 登入](single-sign-on/_static/image21.png)

<span data-ttu-id="298a7-194">當您輸入儲存在內部 Microsoft AD 帳戶中的認證之後，就可以存取此內部應用程式。</span><span class="sxs-lookup"><span data-stu-id="298a7-194">And once you enter credentials stored in an internal Microsoft AD account, you have access to this internal application.</span></span>

![MS SharePoint 網站](single-sign-on/_static/image22.png)

<span data-ttu-id="298a7-196">我們會使用 AD 登入伺服器，主要是因為我們已在 Azure AD 變成可用之前先設定 ADFS，但登入程式正在通過雲端中的 Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="298a7-196">We're using an AD sign-in server mainly because we already had ADFS set up before Azure AD became available, but the log-in process is going through an Azure AD directory in the cloud.</span></span> <span data-ttu-id="298a7-197">我們將重要的檔、原始檔控制、效能管理檔案、銷售報告等等放在雲端，並使用這個完全相同的解決方案來保護它們。</span><span class="sxs-lookup"><span data-stu-id="298a7-197">We put our important documents, source control, performance management files, sales reports, and more, in the cloud and are using this exact same solution to secure them.</span></span>

## <a name="create-an-aspnet-app-that-uses-azure-ad-for-single-sign-on"></a><span data-ttu-id="298a7-198">建立使用 Azure AD 進行單一登入的 ASP.NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="298a7-198">Create an ASP.NET app that uses Azure AD for single sign-on</span></span>

<span data-ttu-id="298a7-199">Visual Studio 可讓您輕鬆地建立使用 Azure AD 進行單一登入的應用程式，如您在幾個螢幕擷取畫面中所見。</span><span class="sxs-lookup"><span data-stu-id="298a7-199">Visual Studio makes it really easy to create an app that uses Azure AD for single sign-on, as you can see from a few screen shots.</span></span>

<span data-ttu-id="298a7-200">當您建立新的 ASP.NET 應用程式（MVC 或 Web Forms）時，預設的驗證方法會是 ASP.NET Identity。</span><span class="sxs-lookup"><span data-stu-id="298a7-200">When you create a new ASP.NET application, either MVC or Web Forms, the default authentication method is ASP.NET Identity.</span></span> <span data-ttu-id="298a7-201">若要將其變更為 Azure AD，請按一下 [**變更驗證**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="298a7-201">To change that to Azure AD, you click a **Change Authentication** button.</span></span>

![變更驗證](single-sign-on/_static/image23.png)

<span data-ttu-id="298a7-203">選取 [組織帳戶]，輸入您的功能變數名稱，然後選取 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="298a7-203">Select Organizational Accounts, enter your domain name, and then select Single Sign On.</span></span>

![[設定驗證] 對話方塊](single-sign-on/_static/image24.png)

<span data-ttu-id="298a7-205">您也可以將目錄資料的讀取或讀取/寫入權限授與應用程式。</span><span class="sxs-lookup"><span data-stu-id="298a7-205">You can also give the app read or read/write permission for directory data.</span></span> <span data-ttu-id="298a7-206">如果您這麼做，它可以使用[Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx)查閱使用者的電話號碼、找出他們是否在辦公室、上次登入的時間等等。</span><span class="sxs-lookup"><span data-stu-id="298a7-206">If you do that, it can use the [Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx) to look up users' phone number, find out if they're in the office, when they last logged on, etc.</span></span>

<span data-ttu-id="298a7-207">這就是您必須 Visual Studio 要求 Azure AD 租使用者之系統管理員的認證，然後再為新的應用程式設定您的專案和 Azure AD 租使用者。</span><span class="sxs-lookup"><span data-stu-id="298a7-207">That's all you have to do - Visual Studio asks for the credentials for an administrator for your Azure AD tenant, and then it configures both your project and your Azure AD tenant for the new application.</span></span>

<span data-ttu-id="298a7-208">當您執行專案時，您會看到登入頁面，而且您可以使用 Azure AD 目錄中使用者的認證來登入。</span><span class="sxs-lookup"><span data-stu-id="298a7-208">When you run the project, you'll see a sign-in page, and you can sign in with credentials of a user in your Azure AD directory.</span></span>

![組織帳戶登入](single-sign-on/_static/image25.png)

![已登入](single-sign-on/_static/image26.png)

<span data-ttu-id="298a7-211">當您將應用程式部署至 Azure 時，您只需要選取 [**啟用組織驗證**] 核取方塊，再一次 Visual Studio 會為您處理所有設定。</span><span class="sxs-lookup"><span data-stu-id="298a7-211">When you deploy the app to Azure, all you have to do is select an **Enable Organizational Authentication** check box, and once again Visual Studio takes care of all the configuration for you.</span></span>

![發行網站](single-sign-on/_static/image27.png)

<span data-ttu-id="298a7-213">這些螢幕擷取畫面來自完整的逐步教學課程，說明如何建立使用 Azure AD 驗證的應用程式：[使用 Azure Active Directory 開發 ASP.NET 應用程式](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="298a7-213">These screen shots come from a complete step-by-step tutorial that shows how to build an app that uses Azure AD authentication: [Developing ASP.NET Apps with Azure Active Directory](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md).</span></span>

## <a name="summary"></a><span data-ttu-id="298a7-214">總結</span><span class="sxs-lookup"><span data-stu-id="298a7-214">Summary</span></span>

<span data-ttu-id="298a7-215">在本章中，您會看到 Azure Active Directory、Visual Studio 和 ASP.NET，可讓您輕鬆地在網際網路應用程式中為貴組織的使用者設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="298a7-215">In this chapter you saw that Azure Active Directory, Visual Studio, and ASP.NET, make it easy to set up single sign-on in Internet applications for your organization's users.</span></span> <span data-ttu-id="298a7-216">您的使用者可以使用他們用來登入的相同認證（使用內部網路中的 Active Directory）登入網際網路應用程式。</span><span class="sxs-lookup"><span data-stu-id="298a7-216">Your users can sign on in Internet apps using the same credentials they use to sign on using Active Directory in your internal network.</span></span>

<span data-ttu-id="298a7-217">[下一章](data-storage-options.md)探討適用于雲端應用程式的資料儲存體選項。</span><span class="sxs-lookup"><span data-stu-id="298a7-217">The [next chapter](data-storage-options.md) looks at the data storage options available for a cloud app.</span></span>

<a id="resources"></a>
## <a name="resources"></a><span data-ttu-id="298a7-218">資源</span><span class="sxs-lookup"><span data-stu-id="298a7-218">Resources</span></span>

<span data-ttu-id="298a7-219">如需詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="298a7-219">For more information, see the following resources:</span></span>

- <span data-ttu-id="298a7-220">[Azure Active Directory 檔](https://docs.microsoft.com/azure/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="298a7-220">[Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="298a7-221">Windowsazure.com 網站上 Azure AD 檔的入口網站頁面。</span><span class="sxs-lookup"><span data-stu-id="298a7-221">Portal page for Azure AD documentation on the windowsazure.com site.</span></span> <span data-ttu-id="298a7-222">如需逐步教學課程，請參閱**開發**一節。</span><span class="sxs-lookup"><span data-stu-id="298a7-222">For step by step tutorials, see the **Develop** section.</span></span>
- <span data-ttu-id="298a7-223">[Azure 多重要素驗證](https://docs.microsoft.com/azure/multi-factor-authentication/)。</span><span class="sxs-lookup"><span data-stu-id="298a7-223">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/).</span></span> <span data-ttu-id="298a7-224">適用于 Azure 中多因素驗證之檔的入口網站頁面。</span><span class="sxs-lookup"><span data-stu-id="298a7-224">Portal page for documentation about multi-factor authentication in Azure.</span></span>
- <span data-ttu-id="298a7-225">[組織帳戶驗證選項](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions)。</span><span class="sxs-lookup"><span data-stu-id="298a7-225">[Organizational account authentication options](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions).</span></span> <span data-ttu-id="298a7-226">[Visual Studio 2013 新增-專案] 對話方塊中 Azure AD 驗證選項的說明。</span><span class="sxs-lookup"><span data-stu-id="298a7-226">Explanation of the Azure AD authentication options in the Visual Studio 2013 new-project dialog.</span></span>
- <span data-ttu-id="298a7-227">[Microsoft 模式和實務-同盟身分識別模式](https://msdn.microsoft.com/library/dn589790.aspx)。</span><span class="sxs-lookup"><span data-stu-id="298a7-227">[Microsoft Patterns and Practices - Federated Identity Pattern](https://msdn.microsoft.com/library/dn589790.aspx).</span></span>
- <span data-ttu-id="298a7-228">[做法：安裝 Azure Active Directory 同步處理工具](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)。</span><span class="sxs-lookup"><span data-stu-id="298a7-228">[HowTo: Install the Azure Active Directory Sync Tool](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx).</span></span>
- <span data-ttu-id="298a7-229">[Active Directory 同盟服務2.0 內容對應](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx)。</span><span class="sxs-lookup"><span data-stu-id="298a7-229">[Active Directory Federation Services 2.0 Content Map](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx).</span></span> <span data-ttu-id="298a7-230">ADFS 2.0 相關檔的連結。</span><span class="sxs-lookup"><span data-stu-id="298a7-230">Links to documentation about ADFS 2.0.</span></span>
- <span data-ttu-id="298a7-231">[Windows Azure AD 應用程式中以角色為基礎和以 ACL 為基礎的授權](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1)。</span><span class="sxs-lookup"><span data-stu-id="298a7-231">[Role-Based and ACL-Based Authorization in a Windows Azure AD Application](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1).</span></span> <span data-ttu-id="298a7-232">範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="298a7-232">Sample application.</span></span>
- <span data-ttu-id="298a7-233">[Azure Active Directory 圖形 API 的 blog](https://blogs.msdn.com/b/aadgraphteam/)。</span><span class="sxs-lookup"><span data-stu-id="298a7-233">[Azure Active Directory Graph API blog](https://blogs.msdn.com/b/aadgraphteam/).</span></span>
- <span data-ttu-id="298a7-234">在混合式身分[識別基礎結構的 BYOD 和目錄整合中存取控制](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=)。</span><span class="sxs-lookup"><span data-stu-id="298a7-234">[Access Control in BYOD and Directory Integration in a Hybrid Identity Infrastructure](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=).</span></span> <span data-ttu-id="298a7-235">Gayana Bagdasaryan 的 Tech Ed 2014 研討會影片。</span><span class="sxs-lookup"><span data-stu-id="298a7-235">Tech Ed 2014 session video by Gayana Bagdasaryan.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="298a7-236">[上一頁](web-development-best-practices.md)
> [下一頁](data-storage-options.md)</span><span class="sxs-lookup"><span data-stu-id="298a7-236">[Previous](web-development-best-practices.md)
[Next](data-storage-options.md)</span></span>
