---
uid: web-api/overview/security/external-authentication-services
title: 外部驗證服務與 ASP.NET Web API （C#） |Microsoft Docs
author: rmcmurray
description: 描述如何在 ASP.NET Web API 中使用外部驗證服務。
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 3bb8eb15-b518-44f5-a67d-a27e051aedc6
msc.legacyurl: /web-api/overview/security/external-authentication-services
msc.type: authoredcontent
ms.openlocfilehash: b2571552a3f8040ff42bfa0a9fa48981f71a1e4b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555472"
---
# <a name="external-authentication-services-with-aspnet-web-api-c"></a><span data-ttu-id="2b3d9-103">外部驗證服務與 ASP.NET Web API （C#）</span><span class="sxs-lookup"><span data-stu-id="2b3d9-103">External Authentication Services with ASP.NET Web API (C#)</span></span>

<span data-ttu-id="2b3d9-104">Visual Studio 2017 和 ASP.NET 4.7.2 中，展開 [[單一頁面應用程式](../../../single-page-application/index.md)（SPA）] 和 [ [Web API](../../index.md)服務] 的安全性選項，以與外部驗證服務整合，其中包括數個 OAuth/OpenID 和社交媒體驗證服務： Microsoft 帳戶、Twitter、Facebook 和 Google。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-104">Visual Studio 2017 and ASP.NET 4.7.2 expand the security options for [Single Page Applications](../../../single-page-application/index.md) (SPA) and [Web API](../../index.md) services to integrate with external authentication services, which include several OAuth/OpenID and social media authentication services: Microsoft Accounts, Twitter, Facebook, and Google.</span></span>  

### <a name="in-this-walkthrough"></a><span data-ttu-id="2b3d9-105">在本逐步解說中</span><span class="sxs-lookup"><span data-stu-id="2b3d9-105">In this Walkthrough</span></span>

- [<span data-ttu-id="2b3d9-106">使用外部驗證服務</span><span class="sxs-lookup"><span data-stu-id="2b3d9-106">Using External Authentication Services</span></span>](#USING)
- [<span data-ttu-id="2b3d9-107">建立範例 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="2b3d9-107">Creating the Sample Web Application</span></span>](#SAMPLE)
- [<span data-ttu-id="2b3d9-108">啟用 Facebook 驗證</span><span class="sxs-lookup"><span data-stu-id="2b3d9-108">Enabling Facebook Authentication</span></span>](#FACEBOOK)
- [<span data-ttu-id="2b3d9-109">啟用 Google 驗證</span><span class="sxs-lookup"><span data-stu-id="2b3d9-109">Enabling Google Authentication</span></span>](#GOOGLE)
- [<span data-ttu-id="2b3d9-110">啟用 Microsoft 驗證</span><span class="sxs-lookup"><span data-stu-id="2b3d9-110">Enabling Microsoft Authentication</span></span>](#MICROSOFT)
- [<span data-ttu-id="2b3d9-111">啟用 Twitter 驗證</span><span class="sxs-lookup"><span data-stu-id="2b3d9-111">Enabling Twitter Authentication</span></span>](#TWITTER)
- [<span data-ttu-id="2b3d9-112">其他資訊</span><span class="sxs-lookup"><span data-stu-id="2b3d9-112">Additional Information</span></span>](#MOREINFO)

    - [<span data-ttu-id="2b3d9-113">結合外部驗證服務</span><span class="sxs-lookup"><span data-stu-id="2b3d9-113">Combining External Authentication Services</span></span>](#COMBINE)
    - [<span data-ttu-id="2b3d9-114">設定 IIS Express 使用完整功能變數名稱</span><span class="sxs-lookup"><span data-stu-id="2b3d9-114">Configuring IIS Express to use a Fully Qualified Domain Name</span></span>](#FQDN)
    - [<span data-ttu-id="2b3d9-115">如何取得 Microsoft 驗證的應用程式設定</span><span class="sxs-lookup"><span data-stu-id="2b3d9-115">How to Obtain your Application Settings for Microsoft Authentication</span></span>](#OBTAIN)
    - [<span data-ttu-id="2b3d9-116">選擇性：停用本機註冊</span><span class="sxs-lookup"><span data-stu-id="2b3d9-116">Optional: Disable Local Registration</span></span>](#DISABLE)

### <a name="prerequisites"></a><span data-ttu-id="2b3d9-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2b3d9-117">Prerequisites</span></span>

<span data-ttu-id="2b3d9-118">若要遵循此逐步解說中的範例，您必須具有下列各項：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-118">To follow the examples in this walkthrough, you need to have the following:</span></span>

- <span data-ttu-id="2b3d9-119">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="2b3d9-119">Visual Studio 2017</span></span>
- <span data-ttu-id="2b3d9-120">具有下列其中一種社交媒體驗證服務之應用程式識別碼和秘密金鑰的開發人員帳戶：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-120">A developer account with the application identifier and secret key for one of the following social media authentication services:</span></span>

  - <span data-ttu-id="2b3d9-121">Microsoft 帳戶（[https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070)）</span><span class="sxs-lookup"><span data-stu-id="2b3d9-121">Microsoft Accounts ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))</span></span>
  - <span data-ttu-id="2b3d9-122">Twitter （[https://dev.twitter.com/](https://dev.twitter.com/)）</span><span class="sxs-lookup"><span data-stu-id="2b3d9-122">Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))</span></span>
  - <span data-ttu-id="2b3d9-123">Facebook （[https://developers.facebook.com/](https://developers.facebook.com/)）</span><span class="sxs-lookup"><span data-stu-id="2b3d9-123">Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))</span></span>
  - <span data-ttu-id="2b3d9-124">Google （[https://developers.google.com/](https://developers.google.com)）</span><span class="sxs-lookup"><span data-stu-id="2b3d9-124">Google ([https://developers.google.com/](https://developers.google.com))</span></span>

<a id="USING"></a>
## <a name="using-external-authentication-services"></a><span data-ttu-id="2b3d9-125">使用外部驗證服務</span><span class="sxs-lookup"><span data-stu-id="2b3d9-125">Using External Authentication Services</span></span>

<span data-ttu-id="2b3d9-126">Web 開發人員目前可使用的眾多外部驗證服務，可在建立新的 web 應用程式時，協助減少開發時間。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-126">The abundance of external authentication services that are currently available to web developers help to reduce development time when creating new web applications.</span></span> <span data-ttu-id="2b3d9-127">Web 使用者通常會有許多適用于熱門 web 服務和社交媒體網站的現有帳戶，因此當 web 應用程式從外部 web 服務或社交媒體網站執行驗證服務時，它會節省開發時間已花在建立驗證的執行。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-127">Web users typically have several existing accounts for popular web services and social media websites, therefore when a web application implements the authentication services from an external web service or social media website, it saves the development time that would have been spent creating an authentication implementation.</span></span> <span data-ttu-id="2b3d9-128">使用外部驗證服務可讓使用者不必為您的 web 應用程式建立另一個帳戶，也不必記住另一個使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-128">Using an external authentication service saves end users from having to create another account for your web application, and also from having to remember another username and password.</span></span>

<span data-ttu-id="2b3d9-129">在過去，開發人員有兩個選擇：建立自己的驗證執行，或瞭解如何將外部驗證服務整合到其應用程式中。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-129">In the past, developers have had two choices: create their own authentication implementation, or learn how to integrate an external authentication service into their applications.</span></span> <span data-ttu-id="2b3d9-130">在最基本的層級上，下圖說明的是使用者代理程式（網頁瀏覽器）的簡單要求流程，它會向已設定為使用外部驗證服務的 web 應用程式要求資訊：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-130">At the most basic level, the following diagram illustrates a simple request flow for a user agent (web browser) that is requesting information from a web application that is configured to use an external authentication service:</span></span>

[![](external-authentication-services/_static/image2.png "Click to Expand the Image")](external-authentication-services/_static/image1.png)

<span data-ttu-id="2b3d9-131">在上圖中，使用者代理程式（或此範例中的網頁瀏覽器）會向 web 應用程式提出要求，將 web 瀏覽器重新導向至外部驗證服務。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-131">In the preceding diagram, the user agent (or web browser in this example) makes a request to a web application, which redirects the web browser to an external authentication service.</span></span> <span data-ttu-id="2b3d9-132">使用者代理程式會將其認證傳送給外部驗證服務，而且如果使用者代理程式已成功驗證，則外部驗證服務會將使用者代理程式重新導向至具有某種形式之權杖的原始 web 應用程式，其中使用者代理程式會傳送至 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-132">The user agent sends its credentials to the external authentication service, and if the user agent has successfully authenticated, the external authentication service will redirect the user agent to the original web application with some form of token which the user agent will send to the web application.</span></span> <span data-ttu-id="2b3d9-133">Web 應用程式會使用此權杖來確認外部驗證服務已成功驗證使用者代理程式，而 web 應用程式可能會使用此權杖來收集有關使用者代理程式的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-133">The web application will use the token to verify that the user agent has been successfully authenticated by the external authentication service, and the web application may use the token to gather more information about the user agent.</span></span> <span data-ttu-id="2b3d9-134">一旦應用程式處理完使用者代理程式的資訊，web 應用程式就會根據其授權設定，將適當的回應傳回給使用者代理程式。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-134">Once the application is done processing the user agent's information, the web application will return the appropriate response to the user agent based on its authorization settings.</span></span>

<span data-ttu-id="2b3d9-135">在第二個範例中，使用者代理程式會與 web 應用程式和外部授權伺服器協調，而 web 應用程式會執行與外部授權伺服器的其他通訊，以取得使用者的其他相關資訊。代理程式</span><span class="sxs-lookup"><span data-stu-id="2b3d9-135">In this second example, the user agent negotiates with the web application and external authorization server, and the web application performs additional communication with the external authorization server to retrieve additional information about the user agent:</span></span>

[![](external-authentication-services/_static/image4.png "Click to Expand the Image")](external-authentication-services/_static/image3.png)

<span data-ttu-id="2b3d9-136">Visual Studio 2017 和 ASP.NET 4.7.2 藉由提供下列驗證服務的內建整合，讓開發人員更容易與外部驗證服務整合：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-136">Visual Studio 2017 and ASP.NET 4.7.2 make integration with external authentication services easier for developers by providing built-in integration for the following authentication services:</span></span>

- <span data-ttu-id="2b3d9-137">Facebook</span><span class="sxs-lookup"><span data-stu-id="2b3d9-137">Facebook</span></span>
- <span data-ttu-id="2b3d9-138">Google</span><span class="sxs-lookup"><span data-stu-id="2b3d9-138">Google</span></span>
- <span data-ttu-id="2b3d9-139">Microsoft 帳戶（Windows Live ID 帳戶）</span><span class="sxs-lookup"><span data-stu-id="2b3d9-139">Microsoft Accounts (Windows Live ID accounts)</span></span>
- <span data-ttu-id="2b3d9-140">Twitter</span><span class="sxs-lookup"><span data-stu-id="2b3d9-140">Twitter</span></span>

<span data-ttu-id="2b3d9-141">本逐步解說中的範例將示範如何使用 Visual Studio 2017 隨附的新 ASP.NET Web 應用程式範本，設定每個支援的外部驗證服務。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-141">The examples in this walkthrough will demonstrate how to configure each of the supported external authentication services by using the new ASP.NET Web Application template that ships with Visual Studio 2017.</span></span>

> [!NOTE]
> <span data-ttu-id="2b3d9-142">如有必要，您可能需要將您的 FQDN 新增至外部驗證服務的設定。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-142">If necessary, you may need to add your FQDN to the settings for your external authentication service.</span></span> <span data-ttu-id="2b3d9-143">這項需求是以部分外部驗證服務的安全性限制為基礎，而這些服務需要應用程式設定中的 FQDN，以符合您的用戶端所使用的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-143">This requirement is based on security constraints for some external authentication services which require the FQDN in your application settings to match the FQDN that is used by your clients.</span></span> <span data-ttu-id="2b3d9-144">（針對每個外部驗證服務，這項操作的步驟會大不相同; 您必須查閱每個外部驗證服務的檔，以查看這是否為必要，以及如何設定這些設定）。如果您需要設定 IIS Express 以使用 FQDN 來測試此環境，請參閱本逐步解說稍後的設定[IIS Express 以使用完整功能變數名稱](#FQDN)一節。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-144">(The steps for this will vary greatly for each external authentication service; you will need to consult the documentation for each external authentication service to see if this is required and how to configure these settings.) If you need to configure IIS Express to use an FQDN for testing this environment, see the [Configuring IIS Express to use a Fully Qualified Domain Name](#FQDN) section later in this walkthrough.</span></span>

<a id="SAMPLE"></a>
## <a name="create-a-sample-web-application"></a><span data-ttu-id="2b3d9-145">建立範例 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="2b3d9-145">Create a Sample Web Application</span></span>

<span data-ttu-id="2b3d9-146">下列步驟將引導您使用 ASP.NET Web 應用程式範本來建立範例應用程式，而您將在本逐步解說稍後針對每個外部驗證服務使用此範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-146">The following steps will lead you through creating a sample application by using the ASP.NET Web Application template, and you will use this sample application for each of the external authentication services later in this walkthrough.</span></span>

<span data-ttu-id="2b3d9-147">啟動 Visual Studio 2017，然後從 [開始] 頁面選取 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-147">Start Visual Studio 2017 and select **New Project** from the Start page.</span></span> <span data-ttu-id="2b3d9-148">或者，**從 [檔案**] 功能表選取 [**新增**]，然後選取 [**專案**]。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-148">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<!-- [![](external-authentication-services/_static/image6.png "Click to Expand the Image")](external-authentication-services/_static/image5.png) -->

<span data-ttu-id="2b3d9-149">當 [**新增專案**] 對話方塊顯示時，請選取 [**已安裝**] 和 [展開**視覺效果C#** ]。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-149">When the **New Project** dialog box is displayed, select **Installed** and expand **Visual C#**.</span></span> <span data-ttu-id="2b3d9-150">在 **[ C#視覺效果**] 底下，選取 [ **Web**]。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-150">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="2b3d9-151">在專案範本清單中，選取 [ **ASP.NET Web 應用程式（.Net Framework）** ]。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-151">In the list of project templates, select **ASP.NET Web Application (.Net Framework)**.</span></span> <span data-ttu-id="2b3d9-152">輸入專案的 [名稱]，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-152">Enter a name for your project and click **OK**.</span></span>

[![](external-authentication-services/_static/image71.png "Click to Expand the Image")](external-authentication-services/_static/image71.png)

<span data-ttu-id="2b3d9-153">顯示**新的 ASP.NET 專案**時，請選取 [**單頁] 應用程式**範本，然後按一下 [**建立專案**]。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-153">When the **New ASP.NET Project** is displayed, select the **Single Page Application** template and click **Create Project**.</span></span>

[![](external-authentication-services/_static/image72.png "Click to Expand the Image")](external-authentication-services/_static/image72.png)

<span data-ttu-id="2b3d9-154">等候 Visual Studio 2017 建立您的專案。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-154">Wait as Visual Studio 2017 creates your project.</span></span>

<!-- [![](external-authentication-services/_static/image12.png "Click to Expand the Image")](external-authentication-services/_static/image11.png) -->

<span data-ttu-id="2b3d9-155">當 Visual Studio 2017 完成建立專案時，請開啟位於**應用程式\_[啟動**] 資料夾中的*Startup.Auth.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-155">When Visual Studio 2017 has finished creating your project, open the *Startup.Auth.cs* file that is located in the **App\_Start** folder.</span></span>

<span data-ttu-id="2b3d9-156">當您第一次建立專案時，不會在*Startup.Auth.cs*檔案中啟用任何外部驗證服務;下圖說明您的程式碼可能會類似的部分，其中區段會針對您啟用外部驗證服務的位置，以及任何相關的設定，以搭配您的 ASP.NET 應用程式使用 Microsoft 帳戶、Twitter、Facebook 或 Google 驗證：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-156">When you first create the project, none of the external authentication services are enabled in *Startup.Auth.cs* file; the following illustrates what your code might resemble, with the sections highlighted for where you would enable an external authentication service and any relevant settings in order to use Microsoft Accounts, Twitter, Facebook, or Google authentication with your ASP.NET application:</span></span>

[!code-csharp[Main](external-authentication-services/samples/sample1.cs)]

<span data-ttu-id="2b3d9-157">當您按 F5 來建立及檢查 web 應用程式時，它會顯示登入畫面，您會在其中看到未定義任何外部驗證服務。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-157">When you press F5 to build and debug your web application, it will display a login screen where you will see that no external authentication services have been defined.</span></span>

[![](external-authentication-services/_static/image73.png "Click to Expand the Image")](external-authentication-services/_static/image73.png)

<span data-ttu-id="2b3d9-158">在下列各節中，您將瞭解如何在 Visual Studio 2017 中啟用 ASP.NET 所提供的每個外部驗證服務。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-158">In the following sections, you will learn how to enable each of the external authentication services that are provided with ASP.NET in Visual Studio 2017.</span></span>

<a id="FACEBOOK"></a>
## <a name="enabling-facebook-authentication"></a><span data-ttu-id="2b3d9-159">啟用 Facebook 驗證</span><span class="sxs-lookup"><span data-stu-id="2b3d9-159">Enabling Facebook authentication</span></span>

<span data-ttu-id="2b3d9-160">使用 Facebook 驗證時，您必須建立 Facebook 開發人員帳戶，而您的專案將需要來自 Facebook 的應用程式識別碼和秘密金鑰才能運作。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-160">Using Facebook authentication requires you to create a Facebook developer account, and your project will require an application ID and secret key from Facebook in order to function.</span></span> <span data-ttu-id="2b3d9-161">如需建立 Facebook 開發人員帳戶以及取得應用程式識別碼和秘密金鑰的相關資訊，請參閱[https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-161">For information about creating a Facebook developer account and obtaining your application ID and secret key, see [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span></span>

<span data-ttu-id="2b3d9-162">取得應用程式識別碼和秘密金鑰後，請使用下列步驟來為您的 web 應用程式啟用 Facebook 驗證：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-162">Once you have obtained your application ID and secret key, use the following steps to enable Facebook authentication for your web application:</span></span>

1. <span data-ttu-id="2b3d9-163">當您的專案在 Visual Studio 2017 中開啟時，請開啟*Startup.Auth.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-163">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="2b3d9-164">找出程式碼的 Facebook 驗證區段：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-164">Locate the Facebook authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample2.cs)]
3. <span data-ttu-id="2b3d9-165">移除 &quot;//&quot; 字元，將反白顯示的程式程式碼取消批註，然後新增您的應用程式識別碼和秘密金鑰。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-165">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your application ID and secret key.</span></span> <span data-ttu-id="2b3d9-166">加入這些參數之後，您就可以重新編譯專案：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-166">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample3.cs)]
4. <span data-ttu-id="2b3d9-167">當您按 F5 在網頁瀏覽器中開啟 web 應用程式時，您會看到 Facebook 已定義為外部驗證服務：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-167">When you press F5 to open your web application in your web browser, you will see that Facebook has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image74.png "Click to Expand the Image")](external-authentication-services/_static/image74.png)
5. <span data-ttu-id="2b3d9-168">當您按一下 [ **facebook** ] 按鈕時，您的瀏覽器會被重新導向至 facebook 登入頁面：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-168">When you click the **Facebook** button, your browser will be redirected to the Facebook login page:</span></span>

    [![](external-authentication-services/_static/image22.png "Click to Expand the Image")](external-authentication-services/_static/image21.png)
6. <span data-ttu-id="2b3d9-169">輸入 Facebook 認證並按一下 [**登入**] 之後，您的網頁瀏覽器將會重新導向回您的 web 應用程式，這會提示您輸入要與 Facebook 帳戶產生關聯的**使用者名稱**：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-169">After you enter your Facebook credentials and click **Log in**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Facebook account:</span></span>

    [![](external-authentication-services/_static/image24.png "Click to Expand the Image")](external-authentication-services/_static/image23.png)
7. <span data-ttu-id="2b3d9-170">輸入您的使用者名稱並按一下 [**註冊**] 按鈕之後，您的 web 應用程式將會顯示您 Facebook 帳戶的預設**首頁**：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-170">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Facebook account:</span></span>

    [![](external-authentication-services/_static/image26.png "Click to Expand the Image")](external-authentication-services/_static/image25.png)

<a id="GOOGLE"></a>
## <a name="enabling-google-authentication"></a><span data-ttu-id="2b3d9-171">啟用 Google 驗證</span><span class="sxs-lookup"><span data-stu-id="2b3d9-171">Enabling Google Authentication</span></span>

<span data-ttu-id="2b3d9-172">使用 Google 驗證時，您必須建立 Google 開發人員帳戶，而您的專案將需要來自 Google 的應用程式識別碼和秘密金鑰才能運作。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-172">Using Google authentication requires you to create a Google developer account, and your project will require an application ID and secret key from Google in order to function.</span></span> <span data-ttu-id="2b3d9-173">如需建立 Google 開發人員帳戶以及取得應用程式識別碼和秘密金鑰的詳細資訊，請參閱[https://developers.google.com](https://developers.google.com)。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-173">For information about creating a Google developer account and obtaining your application ID and secret key, see [https://developers.google.com](https://developers.google.com).</span></span>

<span data-ttu-id="2b3d9-174">若要為您的 web 應用程式啟用 Google 驗證，請使用下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-174">To enable Google authentication for your web application, use the following steps:</span></span>

1. <span data-ttu-id="2b3d9-175">當您的專案在 Visual Studio 2017 中開啟時，請開啟*Startup.Auth.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-175">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="2b3d9-176">找出下列程式碼的 Google 驗證區段：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-176">Locate the Google authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample4.cs)]
3. <span data-ttu-id="2b3d9-177">移除 &quot;//&quot; 字元，將反白顯示的程式程式碼取消批註，然後新增您的應用程式識別碼和秘密金鑰。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-177">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your application ID and secret key.</span></span> <span data-ttu-id="2b3d9-178">加入這些參數之後，您就可以重新編譯專案：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-178">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample5.cs)]
4. <span data-ttu-id="2b3d9-179">當您按 F5 在網頁瀏覽器中開啟 web 應用程式時，您會看到 Google 已定義為外部驗證服務：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-179">When you press F5 to open your web application in your web browser, you will see that Google has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image75.png "Click to Expand the Image")](external-authentication-services/_static/image75.png)
5. <span data-ttu-id="2b3d9-180">當您按一下 [ **google** ] 按鈕時，您的瀏覽器會被重新導向至 google 登入頁面：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-180">When you click the **Google** button, your browser will be redirected to the Google login page:</span></span>

    [![](external-authentication-services/_static/image32.png "Click to Expand the Image")](external-authentication-services/_static/image31.png)
6. <span data-ttu-id="2b3d9-181">輸入您的 Google 認證並按一下 [登**入**] 之後，Google 會提示您確認您的 web 應用程式是否具有存取 Google 帳戶的許可權：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-181">After you enter your Google credentials and click **Sign in**, Google will prompt you to verify that your web application has permissions to access your Google account:</span></span>

    [![](external-authentication-services/_static/image34.png "Click to Expand the Image")](external-authentication-services/_static/image33.png)
7. <span data-ttu-id="2b3d9-182">當您按一下 [**接受**] 時，您的網頁瀏覽器將會重新導向回您的 web 應用程式，這會提示您輸入要與 Google 帳戶產生關聯的**使用者名稱**：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-182">When you click **Accept**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Google account:</span></span>

    [![](external-authentication-services/_static/image36.png "Click to Expand the Image")](external-authentication-services/_static/image35.png)
8. <span data-ttu-id="2b3d9-183">輸入您的使用者名稱並按一下 [**註冊**] 按鈕之後，您的 web 應用程式將會顯示您 Google 帳戶的預設**首頁**：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-183">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Google account:</span></span>

    [![](external-authentication-services/_static/image38.png "Click to Expand the Image")](external-authentication-services/_static/image37.png)

<a id="MICROSOFT"></a>
## <a name="enabling-microsoft-authentication"></a><span data-ttu-id="2b3d9-184">啟用 Microsoft 驗證</span><span class="sxs-lookup"><span data-stu-id="2b3d9-184">Enabling Microsoft Authentication</span></span>

<span data-ttu-id="2b3d9-185">Microsoft 驗證會要求您建立開發人員帳戶，而且需要用戶端識別碼和用戶端密碼才能運作。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-185">Microsoft authentication requires you to create a developer account, and it requires a client ID and client secret in order to function.</span></span> <span data-ttu-id="2b3d9-186">如需建立 Microsoft 開發人員帳戶及取得用戶端識別碼和用戶端密碼的詳細資訊，請參閱[https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070)。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-186">For information about creating a Microsoft developer account and obtaining your client ID and client secret, see [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070).</span></span>

<span data-ttu-id="2b3d9-187">取得取用者金鑰和取用者秘密後，請使用下列步驟來為您的 web 應用程式啟用 Microsoft 驗證：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-187">Once you have obtained your consumer key and consumer secret, use the following steps to enable Microsoft authentication for your web application:</span></span>

1. <span data-ttu-id="2b3d9-188">當您的專案在 Visual Studio 2017 中開啟時，請開啟*Startup.Auth.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-188">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="2b3d9-189">找出 [Microsoft 驗證] 區段中的程式碼：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-189">Locate the Microsoft authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample6.cs)]
3. <span data-ttu-id="2b3d9-190">移除 &quot;//&quot; 字元，將反白顯示的程式程式碼取消批註，然後新增您的用戶端識別碼和用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-190">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your client ID and client secret.</span></span> <span data-ttu-id="2b3d9-191">加入這些參數之後，您就可以重新編譯專案：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-191">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample7.cs)]
4. <span data-ttu-id="2b3d9-192">當您按 F5 在網頁瀏覽器中開啟 web 應用程式時，您會看到 Microsoft 已定義為外部驗證服務：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-192">When you press F5 to open your web application in your web browser, you will see that Microsoft has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image42.png "Click to Expand the Image")](external-authentication-services/_static/image41.png)
5. <span data-ttu-id="2b3d9-193">當您按一下 [ **microsoft** ] 按鈕時，您的瀏覽器會被重新導向至 microsoft 登入頁面：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-193">When you click the **Microsoft** button, your browser will be redirected to the Microsoft login page:</span></span>

    [![](external-authentication-services/_static/image44.png "Click to Expand the Image")](external-authentication-services/_static/image43.png)
6. <span data-ttu-id="2b3d9-194">在您輸入 Microsoft 認證並按一下 [登**入**] 之後，系統會提示您確認您的 web 應用程式是否有許可權可以存取您的 Microsoft 帳戶：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-194">After you enter your Microsoft credentials and click **Sign in**, you will be prompted to verify that your web application has permissions to access your Microsoft account:</span></span>

    [![](external-authentication-services/_static/image46.png "Click to Expand the Image")](external-authentication-services/_static/image45.png)
7. <span data-ttu-id="2b3d9-195">當您按一下 **[是]** 時，您的網頁瀏覽器會重新導向回您的 web 應用程式，這會提示您輸入要與您的 Microsoft 帳戶建立關聯的**使用者名稱**：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-195">When you click **Yes**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Microsoft account:</span></span>

    [![](external-authentication-services/_static/image48.png "Click to Expand the Image")](external-authentication-services/_static/image47.png)
8. <span data-ttu-id="2b3d9-196">輸入您的使用者名稱並按一下 [**註冊**] 按鈕之後，您的 web 應用程式將會顯示 Microsoft 帳戶的預設**首頁**：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-196">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Microsoft account:</span></span>

    [![](external-authentication-services/_static/image50.png "Click to Expand the Image")](external-authentication-services/_static/image49.png)

<a id="TWITTER"></a>
## <a name="enabling-twitter-authentication"></a><span data-ttu-id="2b3d9-197">啟用 Twitter 驗證</span><span class="sxs-lookup"><span data-stu-id="2b3d9-197">Enabling Twitter Authentication</span></span>

<span data-ttu-id="2b3d9-198">Twitter 驗證會要求您建立開發人員帳戶，而且需要取用者金鑰和取用者密碼才能運作。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-198">Twitter authentication requires you to create a developer account, and it requires a consumer key and consumer secret in order to function.</span></span> <span data-ttu-id="2b3d9-199">如需建立 Twitter 開發人員帳戶，以及取得取用者金鑰和取用者秘密的詳細資訊，請參閱[https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-199">For information about creating a Twitter developer account and obtaining your consumer key and consumer secret, see [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span></span>

<span data-ttu-id="2b3d9-200">取得取用者金鑰和取用者秘密後，請使用下列步驟來為您的 web 應用程式啟用 Twitter 驗證：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-200">Once you have obtained your consumer key and consumer secret, use the following steps to enable Twitter authentication for your web application:</span></span>

1. <span data-ttu-id="2b3d9-201">當您的專案在 Visual Studio 2017 中開啟時，請開啟*Startup.Auth.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-201">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="2b3d9-202">找出下列程式碼的 Twitter 驗證區段：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-202">Locate the Twitter authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample8.cs)]
3. <span data-ttu-id="2b3d9-203">移除 &quot;//&quot; 字元，將反白顯示的程式程式碼取消批註，然後新增您的取用者金鑰和取用者密碼。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-203">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your consumer key and consumer secret.</span></span> <span data-ttu-id="2b3d9-204">加入這些參數之後，您就可以重新編譯專案：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-204">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample9.cs)]
4. <span data-ttu-id="2b3d9-205">當您按 F5 在網頁瀏覽器中開啟 web 應用程式時，您會看到 Twitter 已定義為外部驗證服務：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-205">When you press F5 to open your web application in your web browser, you will see that Twitter has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image54.png "Click to Expand the Image")](external-authentication-services/_static/image53.png)
5. <span data-ttu-id="2b3d9-206">當您按一下 [ **twitter** ] 按鈕時，您的瀏覽器會被重新導向至 twitter 登入頁面：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-206">When you click the **Twitter** button, your browser will be redirected to the Twitter login page:</span></span>

    [![](external-authentication-services/_static/image56.png "Click to Expand the Image")](external-authentication-services/_static/image55.png)
6. <span data-ttu-id="2b3d9-207">輸入您的 Twitter 認證並按一下 [**授權應用程式**] 之後，您的網頁瀏覽器將會重新導向回您的 web 應用程式，這會提示您輸入要與您的 Twitter 帳戶產生關聯的**使用者名稱**：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-207">After you enter your Twitter credentials and click **Authorize app**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Twitter account:</span></span>

    [![](external-authentication-services/_static/image58.png "Click to Expand the Image")](external-authentication-services/_static/image57.png)
7. <span data-ttu-id="2b3d9-208">輸入您的使用者名稱並按一下 [**註冊**] 按鈕之後，您的 web 應用程式將會顯示您 Twitter 帳戶的預設**首頁**：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-208">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Twitter account:</span></span>

    [![](external-authentication-services/_static/image60.png "Click to Expand the Image")](external-authentication-services/_static/image59.png)

<a id="MOREINFO"></a>
## <a name="additional-information"></a><span data-ttu-id="2b3d9-209">其他資訊</span><span class="sxs-lookup"><span data-stu-id="2b3d9-209">Additional Information</span></span>

<span data-ttu-id="2b3d9-210">如需建立使用 OAuth 和 OpenID 之應用程式的詳細資訊，請參閱下列 Url：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-210">For additional information about creating applications that use OAuth and OpenID, see the following URLs:</span></span>

- [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)
- [https://go.microsoft.com/fwlink/?LinkID=243995](https://go.microsoft.com/fwlink/?LinkID=243995)

<a id="COMBINE"></a>
### <a name="combining-external-authentication-services"></a><span data-ttu-id="2b3d9-211">結合外部驗證服務</span><span class="sxs-lookup"><span data-stu-id="2b3d9-211">Combining External Authentication Services</span></span>

<span data-ttu-id="2b3d9-212">如需更大的彈性，您可以同時定義多個外部驗證服務-這可讓您的 web 應用程式使用者從任何已啟用的外部驗證服務使用帳戶：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-212">For greater flexibility, you can define multiple external authentication services at the same time - this allows your web application's users to use an account from any of the enabled external authentication services:</span></span>

[![](external-authentication-services/_static/image62.png "Click to Expand the Image")](external-authentication-services/_static/image61.png)

<a id="FQDN"></a>
### <a name="configure-iis-express-to-use-a-fully-qualified-domain-name"></a><span data-ttu-id="2b3d9-213">設定 IIS Express 使用完整功能變數名稱</span><span class="sxs-lookup"><span data-stu-id="2b3d9-213">Configure IIS Express to use a fully qualified domain name</span></span>

<span data-ttu-id="2b3d9-214">某些外部驗證提供者不支援使用 HTTP 位址（如 `http://localhost:port/`）來測試您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-214">Some external authentication providers do not support testing your application by using an HTTP address like `http://localhost:port/`.</span></span> <span data-ttu-id="2b3d9-215">若要解決這個問題，您可以將靜態完整功能變數名稱（FQDN）對應新增至您的 HOSTS 檔案，並在 Visual Studio 2017 中設定您的專案選項，以使用 FQDN 進行測試/的偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-215">To work around this issue, you can add a static Fully Qualified Domain Name (FQDN) mapping to your HOSTS file and configure your project options in Visual Studio 2017 to use the FQDN for testing/debugging.</span></span> <span data-ttu-id="2b3d9-216">若要這樣做，請使用下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-216">To do so, use the following steps:</span></span>

- <span data-ttu-id="2b3d9-217">新增靜態 FQDN 對應您的 HOSTS 檔案：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-217">Add a static FQDN mapping your HOSTS file:</span></span>

  1. <span data-ttu-id="2b3d9-218">在 Windows 中開啟提升許可權的命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-218">Open an elevated command prompt in Windows.</span></span>
  2. <span data-ttu-id="2b3d9-219">輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-219">Type the following command:</span></span>

      <span data-ttu-id="2b3d9-220"><kbd>記事本%WinDir%\system32\drivers\etc\hosts</kbd></span><span class="sxs-lookup"><span data-stu-id="2b3d9-220"><kbd>notepad %WinDir%\system32\drivers\etc\hosts</kbd></span></span>
  3. <span data-ttu-id="2b3d9-221">將類似下列的專案新增至 HOSTS 檔案：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-221">Add an entry like the following to the HOSTS file:</span></span>

      <span data-ttu-id="2b3d9-222"><kbd>127.0.0.1 www.wingtiptoys.com</kbd></span><span class="sxs-lookup"><span data-stu-id="2b3d9-222"><kbd>127.0.0.1 www.wingtiptoys.com</kbd></span></span>
  4. <span data-ttu-id="2b3d9-223">儲存並關閉主機檔案。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-223">Save and close your HOSTS file.</span></span>

- <span data-ttu-id="2b3d9-224">將您的 Visual Studio 專案設定為使用 FQDN：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-224">Configure your Visual Studio project to use the FQDN:</span></span>

  1. <span data-ttu-id="2b3d9-225">當您的專案在 Visual Studio 2017 中開啟時，請按一下 [**專案**] 功能表，然後選取專案的屬性。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-225">When your project is open in Visual Studio 2017, click the **Project** menu, and then select your project's properties.</span></span> <span data-ttu-id="2b3d9-226">例如，您可以選取 [ **WebApplication1 屬性**]。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-226">For example, you might select **WebApplication1 Properties**.</span></span>
  2. <span data-ttu-id="2b3d9-227">選取 [ **Web** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-227">Select the **Web** tab.</span></span>
  3. <span data-ttu-id="2b3d9-228">輸入您的 [<strong>專案 Url</strong>] 的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-228">Enter your FQDN for the <strong>Project Url</strong>.</span></span> <span data-ttu-id="2b3d9-229">例如，如果這是您新增至主機檔案的 FQDN 對應，您會輸入<kbd><http://www.wingtiptoys.com></kbd> 。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-229">For example, you would enter <kbd><http://www.wingtiptoys.com></kbd> if that was the FQDN mapping that you added to your HOSTS file.</span></span>

- <span data-ttu-id="2b3d9-230">設定 IIS Express 以使用應用程式的 FQDN：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-230">Configure IIS Express to use the FQDN for your application:</span></span>

    1. <span data-ttu-id="2b3d9-231">在 Windows 中開啟提升許可權的命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-231">Open an elevated command prompt in Windows.</span></span>
    2. <span data-ttu-id="2b3d9-232">輸入下列命令以變更至您的 IIS Express 資料夾：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-232">Type the following command to change to your IIS Express folder:</span></span>

        <span data-ttu-id="2b3d9-233"><kbd>cd/d &quot;%ProgramFiles%\IIS Express&quot;</kbd></span><span class="sxs-lookup"><span data-stu-id="2b3d9-233"><kbd>cd /d &quot;%ProgramFiles%\IIS Express&quot;</kbd></span></span>
    3. <span data-ttu-id="2b3d9-234">輸入下列命令，將 FQDN 新增至您的應用程式：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-234">Type the following command to add the FQDN to your application:</span></span>

        <span data-ttu-id="2b3d9-235"><kbd>appcmd.exe set config-section： system.web/sites/+&quot;[name = ' WebApplication1 ']。系結。[protocol = ' HTTP '，bindingInformation = ' \*：80： www. wingtiptoys .com ']&quot;/commit： apphost</kbd></span><span class="sxs-lookup"><span data-stu-id="2b3d9-235"><kbd>appcmd.exe set config -section:system.applicationHost/sites /+&quot;[name='WebApplication1'].bindings.[protocol='http',bindingInformation='\*:80:www.wingtiptoys.com']&quot; /commit:apphost</kbd></span></span>

  <span data-ttu-id="2b3d9-236">其中， **WebApplication1**是您專案的名稱，而**bindingInformation**包含您要用於測試的通訊埠編號和 FQDN。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-236">Where **WebApplication1** is the name of your project and **bindingInformation** contains the port number and FQDN that you want to use for your testing.</span></span>

<a id="OBTAIN"></a>
### <a name="how-to-obtain-your-application-settings-for-microsoft-authentication"></a><span data-ttu-id="2b3d9-237">如何取得 Microsoft 驗證的應用程式設定</span><span class="sxs-lookup"><span data-stu-id="2b3d9-237">How to Obtain your Application Settings for Microsoft Authentication</span></span>

<span data-ttu-id="2b3d9-238">將應用程式連結到 Windows Live for Microsoft 驗證是一個簡單的流程。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-238">Linking an application to Windows Live for Microsoft Authentication is a simple process.</span></span> <span data-ttu-id="2b3d9-239">如果您尚未將應用程式連結至 Windows Live，可以使用下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-239">If you have not already linked an application to Windows Live, you can use the following steps:</span></span>

1. <span data-ttu-id="2b3d9-240">流覽至[https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070)並在出現提示時輸入您的 Microsoft 帳戶名稱和密碼，然後按一下 [登**入**]：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-240">Browse to [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070) and enter your Microsoft account name and password when prompted, then click **Sign in**:</span></span>

   <!--  [![](external-authentication-services/_static/image64.png "Click to Expand the Image")](external-authentication-services/_static/image63.png) -->
2. <span data-ttu-id="2b3d9-241">選取 [**新增應用程式**]，並在出現提示時輸入應用程式的名稱，然後按一下 [**建立**]：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-241">Select **Add an app** and enter the name of your application when prompted, and then click **Create**:</span></span>

    [![](external-authentication-services/_static/image79.png "Click to Expand the Image")](external-authentication-services/_static/image79.png)
3. <span data-ttu-id="2b3d9-242">在 [**名稱**] 底下選取您的應用程式，其應用程式屬性頁面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-242">Select your app under **Name** and its application properties page appears.</span></span>

4. <span data-ttu-id="2b3d9-243">輸入應用程式的重新導向網域。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-243">Enter the redirect domain for your application.</span></span> <span data-ttu-id="2b3d9-244">複製 [**應用程式識別碼**]，然後在 [**應用程式**密碼] 底下，選取 [**產生密碼**]。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-244">Copy the **Application ID** and, under **Application Secrets**, select **Generate Password**.</span></span> <span data-ttu-id="2b3d9-245">複製顯示的密碼。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-245">Copy the password that appears.</span></span> <span data-ttu-id="2b3d9-246">應用程式識別碼和密碼是您的用戶端識別碼和用戶端秘密。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-246">The application ID and password are your client ID and client secret.</span></span> <span data-ttu-id="2b3d9-247">選取 **[確定]** ，然後按一下 [**儲存**]。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-247">Select **Ok** and then **Save**.</span></span>

    [![](external-authentication-services/_static/image77.png "Click to Expand the Image")](external-authentication-services/_static/image77.png)

<a id="DISABLE"></a>
### <a name="optional-disable-local-registration"></a><span data-ttu-id="2b3d9-248">選擇性：停用本機註冊</span><span class="sxs-lookup"><span data-stu-id="2b3d9-248">Optional: Disable Local Registration</span></span>

<span data-ttu-id="2b3d9-249">目前的 ASP.NET 本機註冊功能不會防止自動化程式（bot）建立成員帳戶;例如，藉由使用 bot 預防和驗證技術（例如[CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md)）。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-249">The current ASP.NET local registration functionality does not prevent automated programs (bots) from creating member accounts; for example, by using a bot-prevention and validation technology like [CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md).</span></span> <span data-ttu-id="2b3d9-250">因此，您應該移除登入頁面上的 [本機登入表單] 和 [註冊] 連結。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-250">Because of this, you should remove the local login form and registration link on the login page.</span></span> <span data-ttu-id="2b3d9-251">若要這麼做，請開啟專案中的 *\_Login. cshtml*  頁面，然後將 本機登入 面板和 註冊 連結的行加上批註。</span><span class="sxs-lookup"><span data-stu-id="2b3d9-251">To do so, open the *\_Login.cshtml* page in your project, and then comment out the lines for the local login panel and the registration link.</span></span> <span data-ttu-id="2b3d9-252">產生的頁面看起來應該如下列程式碼範例所示：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-252">The resulting page should look like the following code sample:</span></span>

[!code-html[Main](external-authentication-services/samples/sample10.html)]

<span data-ttu-id="2b3d9-253">一旦停用 [本機登入] 面板和註冊連結，您的登入頁面只會顯示您已啟用的外部驗證提供者：</span><span class="sxs-lookup"><span data-stu-id="2b3d9-253">Once the local login panel and the registration link have been disabled, your login page will only display the external authentication providers that you have enabled:</span></span>

[![](external-authentication-services/_static/image70.png "Click to Expand the Image")](external-authentication-services/_static/image69.png)
