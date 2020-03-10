---
uid: identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory
title: 使用 Azure Active Directory ASP.NET 4.x 開發 ASP.NET 應用程式
author: Rick-Anderson
description: 適用于 Azure Active Directory 的 Microsoft ASP.NET 工具可讓您輕鬆地針對裝載于 Azure 上的 web 應用程式啟用驗證。 您可以使用 Azure 驗證 。
ms.author: riande
ms.date: 08/14/2014
ms.assetid: 457d7eaf-ee76-4ceb-9082-c7c1721435ad
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory
msc.type: authoredcontent
ms.openlocfilehash: 28425ea8d1312dfc6e14df9677396f2cbcf6f16d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583850"
---
# <a name="developing-aspnet-apps-with-azure-active-directory"></a>使用 Azure Active Dirctory 開發 ASP.NET 應用程式

依[Rick Anderson](https://twitter.com/RickAndMSFT)

適用于 Azure Active Directory 的 Microsoft ASP.NET 工具可簡化[Azure](https://www.windowsazure.com/home/features/web-sites/)上裝載之 web 應用程式的驗證啟用。 您可以使用 Azure 驗證，從您的組織驗證 Office 365 使用者、從內部部署 Active Directory 同步處理的公司帳戶，或在您自己的自訂 Azure Active Directory 網域中建立的使用者。 啟用 Windows Azure 驗證會設定您的應用程式使用單一[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/)租使用者來驗證使用者。

本教學課程將說明如何建立 ASP.NET 應用程式，其已設定為使用[Azure Active Directory](https://msdn.microsoft.com/library/azure/mt168838.aspx) （Azure AD）登入。 您也將瞭解如何呼叫圖形 API 來取得目前已登入使用者的相關資訊，以及如何將應用程式部署至 Azure。

## <a name="prerequisites"></a>必要條件

1. 適用于 Web 或 [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) 的 [Visual Studio Express 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013#d-2013-express) 。
2. 需要[Visual Studio 2013 Update 4](https://www.microsoft.com/download/details.aspx?id=44921) -Update 3 或更新版本。
3. 一個 Azure 帳戶。 如果您還沒有帳戶，[請按一下這裡](https://azure.microsoft.com/pricing/free-trial/)取得免費試用版。

## <a name="add-a-global-administrator-to-your-active-directory"></a>將全域管理員新增至您的 Active Directory

1. 登入 [Azure 管理入口網站](https://manage.windowsazure.com/)。
2. 所有 Azure 帳戶都包含**預設目錄**-按一下它，然後按一下頁面頂端的 [**使用者**] 索引標籤（請參閱下圖）。
3. 按一下 [新增使用者]。
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image1.png)
4. 建立具有**全域管理員**角色的新使用者。 按一下頂端功能表中的 [**使用者**]，然後按一下命令列上的 [**新增使用者**] 按鈕。
5. 在 [新增**使用者**] 對話方塊中，輸入新使用者的名稱，然後按一下向右箭號。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image2.png)
6. 輸入使用者名稱，並將角色設定為**全域管理員**。 全域管理員需要替代的電子郵件地址，才能進行密碼復原。 完成後，請按一下向右箭號。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image3.png)
7. 在對話方塊的下一個頁面上，按一下 [**建立**]。 系統會為新使用者建立暫時密碼，並顯示在對話方塊中。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image4.png)

   儲存密碼，您將必須在第一次登入之後變更密碼。 下圖顯示新的系統管理員帳戶。 您必須使用 Azure Active Directory 來登入您的應用程式，而不是此頁面上顯示的 Microsoft 帳戶。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image5.png)

## <a name="create-an-aspnet-application"></a>建立 ASP.NET 應用程式

下列步驟會使用[適用于 Web 的 Visual Studio Express 2013](https://www.microsoft.com/download/details.aspx?id=40747)，而且需要[Visual Studio 2013 Update 3](https://www.microsoft.com/download/details.aspx?id=43721)。

1. 在 Visual Studio 中，依**序按一下 [** 檔案] 和 [**新增專案**]。 在 [**新增專案**] 對話方塊中，從C#左側功能表中選取 [Visual Web 專案]，然後按一下 **[確定]** 。 如果您不想要應用程式的功能，您可能也會想要取消核取 [**將 Application Insights 新增至專案**]。
2. 在 [**新增 ASP.NET 專案**] 對話方塊中，選取 [ **MVC**]，然後按一下 [**變更驗證**]。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image6.png)
3. 在 [**變更驗證**] 對話方塊中，選取 [**組織帳戶**]。 這些選項可用來自動向 Azure AD 註冊您的應用程式，以及自動設定您的應用程式以與 Azure AD 整合。 您不需要使用 [**變更驗證**] 對話方塊來註冊及設定您的應用程式，但這樣做會更輕鬆。 例如，如果您使用 Visual Studio 2012，您仍然可以在 Azure 管理入口網站中手動註冊應用程式，並更新其設定以與 Azure AD 整合。
   在下拉式功能表中，選取 [**雲端-單一組織**] 和 [**單一登入]、[讀取目錄資料**]。 輸入 Azure AD 目錄的網域（例如，在下列映射中） *aricka0yahoo.onmicrosoft.com*，然後按一下 **[確定]** 。 您可以從 azure 入口網站上預設目錄的 [網域] 索引標籤中取得功能變數名稱（請參閱下一個影像）。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image7.png)

   下圖顯示來自 Azure 入口網站的功能變數名稱。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image8.png)

    > [!NOTE]
    > 您可以按一下 [**更多選項**]，選擇性地設定將在 Azure AD 中註冊的應用程式識別碼 URI。 [應用程式識別碼 URI] 是應用程式的唯一識別碼，會在 Azure AD 中註冊，並在與 Azure AD 通訊時供應用程式用來識別自己的身分。 如需應用程式識別碼 URI 和已註冊應用程式之其他屬性的詳細資訊，請參閱[這個主題](https://msdn.microsoft.com/library/azure/dn499820.aspx#BKMK_Registering)。 按一下 [應用程式識別碼 URI] 欄位下方的核取方塊，您也可以選擇覆寫使用相同應用程式識別碼 URI 之 Azure AD 中的現有註冊。
4. 按一下 **[確定**] 之後，就會出現登入對話方塊，您必須使用全域管理員帳戶（而不是與您的訂用帳戶相關聯的 Microsoft 帳戶）登入。 如果您稍早建立了新的系統管理員帳戶，則必須變更密碼，然後使用新密碼重新登入。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image9.png)
5. 成功驗證之後，[**新增 ASP.NET 專案**] 對話方塊會顯示您的驗證選擇（**組織**）和新應用程式註冊所在的目錄（下圖中的*aricka0yahoo.onmicrosoft.com* ）。 在此資訊底下，選取標示為 **[主機在雲端中**] 的核取方塊。 如果選取此核取方塊，專案將會布建為 Azure web 應用程式，並將于稍後啟用以方便發行。 按一下 [確定]。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image10.png)
6. [**設定 Azure 網站**] 對話方塊隨即出現，並使用自動產生的網站名稱和區域。 另請注意您目前在對話方塊中登入的帳戶。 您想要確保此帳戶是您的 Azure 訂用帳戶所連接的帳戶，通常是 Microsoft 帳戶。

    > [!NOTE]
    > 此專案需要資料庫。 您必須選取其中一個現有的資料庫，或建立一個新的。 資料庫是必要的，因為專案已經使用本機資料庫檔案來儲存少量的驗證設定資料。 當您將應用程式部署至 Azure 網站時，此資料庫不會隨部署封裝，因此您必須選擇可在雲端中存取的資料庫。 按一下 [確定]。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image11.png)
7. 將會建立專案，而且您的驗證選項和 web 應用程式選項會自動以專案設定。 完成此程式之後，請按 **^ F5**在本機執行專案。 您將必須使用您的組織帳戶登入。 提供您稍早建立之帳戶的使用者名稱和密碼，然後按一下 [登**入**]。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image12.png)
8. 成功登入之後，ASP.NET 網站會顯示您已透過在頁面右上角顯示使用者名稱的方式進行驗證。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image13.png)

   如果您收到錯誤：值不能為 null 或空白。 參數名稱： Linktext> ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image14.png)

   請參閱本教學課程結尾的[debug](#dbg)一節。

## <a name="basics-of-the-graph-api"></a>圖形 API 的基本概念

[圖形 API](https://msdn.microsoft.com/library/azure/hh974476.aspx)是用來在 Azure AD 目錄中的物件上執行 CRUD 和其他作業的程式設計介面。 如果您在 Visual Studio 2013 中建立新專案時選取 [組織帳戶] 選項進行驗證，則您的應用程式將已設定為呼叫圖形 API。 本節將簡短說明圖形 API 的運作方式。

1. 在執行中的應用程式中，按一下頁面右上方的已登入使用者名稱。 這會帶您前往 [使用者設定檔] 頁面，這是主控制器上的動作。 您會發現資料表包含您稍早建立之系統管理員帳戶的相關使用者資訊。 這項資訊會儲存在您的目錄中，並在頁面載入時呼叫圖形 API 來取得此資訊。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image15.png)
2. 返回 Visual Studio 並展開 [**控制器**] 資料夾，然後開啟**HomeController.cs**檔案。 您會看到一個**UserProfile （）** 動作，其中包含用來抓取權杖的程式碼，然後呼叫圖形 API。 這段程式碼複製如下：

    [!code-csharp[Main](developing-aspnet-apps-with-windows-azure-active-directory/samples/sample1.cs?highlight=22)]

    若要呼叫圖形 API，您必須先取得權杖。 取得權杖時，必須將其字串值附加至圖形 API 的所有後續要求的授權標頭中。 上述大部分程式碼會處理 Azure AD 的驗證詳細資料，以取得權杖、使用權杖來呼叫圖形 API，然後再轉換回應，以便在視圖中顯示。

    討論的最相關部分是下列醒目提示的程式程式碼： `UserProfile profile = JsonConvert.DeserializeObject<UserProfile>(responseString);`。 這一行代表已從 JSON 回應還原序列化並在視圖中顯示的使用者名稱。

    您可以使用 HttpClient 呼叫圖形 API 並自行處理原始資料，但更簡單的方法是使用[Graph 用戶端程式庫（可透過 NuGet](http://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient/)取得）。 用戶端程式庫會為您處理原始的 HTTP 要求並轉換傳回的資料，讓您更輕鬆地在 .NET 環境中使用圖形 API。 請參閱 GitHub 上的相關圖形 API 程式碼範例[。](https://github.com/AzureADSamples)

## <a name="deploy-the-application-to-azure"></a>將應用程式部署至 Azure

下列步驟將說明如何將應用程式部署至 Azure。 在先前的步驟中，您已將新的專案與 Azure 上的 web 應用程式連線，因此只需幾個步驟就可以發佈。

1. 在 Visual Studio 中，以滑鼠右鍵按一下專案，然後選取 [**發佈**]。 [**發行 Web** ] 對話方塊隨即出現，並顯示每個設定。 按 [**下一步]** 按鈕以移至 [**設定**] 頁面。 系統可能會提示您進行驗證;請務必使用您的 Azure 訂用帳戶（通常是 Microsoft 帳戶），而不是您稍早建立的組織帳戶進行驗證。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image16.png)
2. 勾選 [**啟用組織驗證**] 選項。 在 [**網域**] 欄位中，輸入您目錄的網域。 從 [**存取層級**] 下拉式選單中，選取 [**單一登入]、[讀取目錄資料**]。 您會發現，您所使用的先前資料庫已填入 [**資料庫**] 區段中。 按一下 [發行]。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image17.png)
3. Visual Studio 會開始部署您的網站，然後會出現新的瀏覽器視窗。 系統可能會提示您再次向您的目錄進行驗證。 經過驗證之後，系統會將您重新導向至 Azure 上新發佈的網站。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image18.png)

<a id="dbg"></a>
## <a name="debugging-the-app"></a>偵錯工具

如果您收到下列錯誤訊息：值不能為 null 或空白。 參數名稱： Linktext>

![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image19.png)

以下列內容取代*Views\Shared\\_LoginPartial. cshtml*檔案中的程式碼：

[!code-cshtml[Main](developing-aspnet-apps-with-windows-azure-active-directory/samples/sample2.cshtml?highlight=1-8,15-16)]

執行應用程式之後，如果登入的使用者顯示「Null 使用者」，請登出，然後使用您稍早建立的 Active Directory 帳戶重新登入。

Rick Rainey [深入探討，這是一種要遵循的絕佳教學課程：使用 Azure AD](http://rickrainey.com/2014/08/19/deep-dive-azure-websites-and-organizational-authentication-using-azure-ad/)的 Azure 網站和組織驗證。

## <a name="more-information"></a>更多資訊

- [深入了解：使用 Azure AD](http://rickrainey.com/2014/08/19/deep-dive-azure-websites-and-organizational-authentication-using-azure-ad/) 的 Azure 網站和組織驗證
- [Azure AD 圖形 API 總覽](https://msdn.microsoft.com/library/azure/hh974476.aspx)
- [Azure AD 中的驗證案例](https://msdn.microsoft.com/library/azure/dn499820.aspx)
- [GitHub 上的 Azure AD 程式碼範例](https://github.com/AzureADSamples)
