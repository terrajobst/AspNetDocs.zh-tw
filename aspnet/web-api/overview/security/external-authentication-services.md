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
# <a name="external-authentication-services-with-aspnet-web-api-c"></a>外部驗證服務與 ASP.NET Web API （C#）

Visual Studio 2017 和 ASP.NET 4.7.2 中，展開 [[單一頁面應用程式](../../../single-page-application/index.md)（SPA）] 和 [ [Web API](../../index.md)服務] 的安全性選項，以與外部驗證服務整合，其中包括數個 OAuth/OpenID 和社交媒體驗證服務： Microsoft 帳戶、Twitter、Facebook 和 Google。  

### <a name="in-this-walkthrough"></a>在本逐步解說中

- [使用外部驗證服務](#USING)
- [建立範例 Web 應用程式](#SAMPLE)
- [啟用 Facebook 驗證](#FACEBOOK)
- [啟用 Google 驗證](#GOOGLE)
- [啟用 Microsoft 驗證](#MICROSOFT)
- [啟用 Twitter 驗證](#TWITTER)
- [其他資訊](#MOREINFO)

    - [結合外部驗證服務](#COMBINE)
    - [設定 IIS Express 使用完整功能變數名稱](#FQDN)
    - [如何取得 Microsoft 驗證的應用程式設定](#OBTAIN)
    - [選擇性：停用本機註冊](#DISABLE)

### <a name="prerequisites"></a>Prerequisites

若要遵循此逐步解說中的範例，您必須具有下列各項：

- Visual Studio 2017
- 具有下列其中一種社交媒體驗證服務之應用程式識別碼和秘密金鑰的開發人員帳戶：

  - Microsoft 帳戶（[https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070)）
  - Twitter （[https://dev.twitter.com/](https://dev.twitter.com/)）
  - Facebook （[https://developers.facebook.com/](https://developers.facebook.com/)）
  - Google （[https://developers.google.com/](https://developers.google.com)）

<a id="USING"></a>
## <a name="using-external-authentication-services"></a>使用外部驗證服務

Web 開發人員目前可使用的眾多外部驗證服務，可在建立新的 web 應用程式時，協助減少開發時間。 Web 使用者通常會有許多適用于熱門 web 服務和社交媒體網站的現有帳戶，因此當 web 應用程式從外部 web 服務或社交媒體網站執行驗證服務時，它會節省開發時間已花在建立驗證的執行。 使用外部驗證服務可讓使用者不必為您的 web 應用程式建立另一個帳戶，也不必記住另一個使用者名稱和密碼。

在過去，開發人員有兩個選擇：建立自己的驗證執行，或瞭解如何將外部驗證服務整合到其應用程式中。 在最基本的層級上，下圖說明的是使用者代理程式（網頁瀏覽器）的簡單要求流程，它會向已設定為使用外部驗證服務的 web 應用程式要求資訊：

[![](external-authentication-services/_static/image2.png "Click to Expand the Image")](external-authentication-services/_static/image1.png)

在上圖中，使用者代理程式（或此範例中的網頁瀏覽器）會向 web 應用程式提出要求，將 web 瀏覽器重新導向至外部驗證服務。 使用者代理程式會將其認證傳送給外部驗證服務，而且如果使用者代理程式已成功驗證，則外部驗證服務會將使用者代理程式重新導向至具有某種形式之權杖的原始 web 應用程式，其中使用者代理程式會傳送至 web 應用程式。 Web 應用程式會使用此權杖來確認外部驗證服務已成功驗證使用者代理程式，而 web 應用程式可能會使用此權杖來收集有關使用者代理程式的詳細資訊。 一旦應用程式處理完使用者代理程式的資訊，web 應用程式就會根據其授權設定，將適當的回應傳回給使用者代理程式。

在第二個範例中，使用者代理程式會與 web 應用程式和外部授權伺服器協調，而 web 應用程式會執行與外部授權伺服器的其他通訊，以取得使用者的其他相關資訊。代理程式

[![](external-authentication-services/_static/image4.png "Click to Expand the Image")](external-authentication-services/_static/image3.png)

Visual Studio 2017 和 ASP.NET 4.7.2 藉由提供下列驗證服務的內建整合，讓開發人員更容易與外部驗證服務整合：

- Facebook
- Google
- Microsoft 帳戶（Windows Live ID 帳戶）
- Twitter

本逐步解說中的範例將示範如何使用 Visual Studio 2017 隨附的新 ASP.NET Web 應用程式範本，設定每個支援的外部驗證服務。

> [!NOTE]
> 如有必要，您可能需要將您的 FQDN 新增至外部驗證服務的設定。 這項需求是以部分外部驗證服務的安全性限制為基礎，而這些服務需要應用程式設定中的 FQDN，以符合您的用戶端所使用的 FQDN。 （針對每個外部驗證服務，這項操作的步驟會大不相同; 您必須查閱每個外部驗證服務的檔，以查看這是否為必要，以及如何設定這些設定）。如果您需要設定 IIS Express 以使用 FQDN 來測試此環境，請參閱本逐步解說稍後的設定[IIS Express 以使用完整功能變數名稱](#FQDN)一節。

<a id="SAMPLE"></a>
## <a name="create-a-sample-web-application"></a>建立範例 Web 應用程式

下列步驟將引導您使用 ASP.NET Web 應用程式範本來建立範例應用程式，而您將在本逐步解說稍後針對每個外部驗證服務使用此範例應用程式。

啟動 Visual Studio 2017，然後從 [開始] 頁面選取 [**新增專案**]。 或者，**從 [檔案**] 功能表選取 [**新增**]，然後選取 [**專案**]。

<!-- [![](external-authentication-services/_static/image6.png "Click to Expand the Image")](external-authentication-services/_static/image5.png) -->

當 [**新增專案**] 對話方塊顯示時，請選取 [**已安裝**] 和 [展開**視覺效果C#** ]。 在 **[ C#視覺效果**] 底下，選取 [ **Web**]。 在專案範本清單中，選取 [ **ASP.NET Web 應用程式（.Net Framework）** ]。 輸入專案的 [名稱]，然後按一下 **[確定]** 。

[![](external-authentication-services/_static/image71.png "Click to Expand the Image")](external-authentication-services/_static/image71.png)

顯示**新的 ASP.NET 專案**時，請選取 [**單頁] 應用程式**範本，然後按一下 [**建立專案**]。

[![](external-authentication-services/_static/image72.png "Click to Expand the Image")](external-authentication-services/_static/image72.png)

等候 Visual Studio 2017 建立您的專案。

<!-- [![](external-authentication-services/_static/image12.png "Click to Expand the Image")](external-authentication-services/_static/image11.png) -->

當 Visual Studio 2017 完成建立專案時，請開啟位於**應用程式\_[啟動**] 資料夾中的*Startup.Auth.cs*檔案。

當您第一次建立專案時，不會在*Startup.Auth.cs*檔案中啟用任何外部驗證服務;下圖說明您的程式碼可能會類似的部分，其中區段會針對您啟用外部驗證服務的位置，以及任何相關的設定，以搭配您的 ASP.NET 應用程式使用 Microsoft 帳戶、Twitter、Facebook 或 Google 驗證：

[!code-csharp[Main](external-authentication-services/samples/sample1.cs)]

當您按 F5 來建立及檢查 web 應用程式時，它會顯示登入畫面，您會在其中看到未定義任何外部驗證服務。

[![](external-authentication-services/_static/image73.png "Click to Expand the Image")](external-authentication-services/_static/image73.png)

在下列各節中，您將瞭解如何在 Visual Studio 2017 中啟用 ASP.NET 所提供的每個外部驗證服務。

<a id="FACEBOOK"></a>
## <a name="enabling-facebook-authentication"></a>啟用 Facebook 驗證

使用 Facebook 驗證時，您必須建立 Facebook 開發人員帳戶，而您的專案將需要來自 Facebook 的應用程式識別碼和秘密金鑰才能運作。 如需建立 Facebook 開發人員帳戶以及取得應用程式識別碼和秘密金鑰的相關資訊，請參閱[https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)。

取得應用程式識別碼和秘密金鑰後，請使用下列步驟來為您的 web 應用程式啟用 Facebook 驗證：

1. 當您的專案在 Visual Studio 2017 中開啟時，請開啟*Startup.Auth.cs*檔案。

2. 找出程式碼的 Facebook 驗證區段：

    [!code-csharp[Main](external-authentication-services/samples/sample2.cs)]
3. 移除 &quot;//&quot; 字元，將反白顯示的程式程式碼取消批註，然後新增您的應用程式識別碼和秘密金鑰。 加入這些參數之後，您就可以重新編譯專案：

    [!code-csharp[Main](external-authentication-services/samples/sample3.cs)]
4. 當您按 F5 在網頁瀏覽器中開啟 web 應用程式時，您會看到 Facebook 已定義為外部驗證服務：

    [![](external-authentication-services/_static/image74.png "Click to Expand the Image")](external-authentication-services/_static/image74.png)
5. 當您按一下 [ **facebook** ] 按鈕時，您的瀏覽器會被重新導向至 facebook 登入頁面：

    [![](external-authentication-services/_static/image22.png "Click to Expand the Image")](external-authentication-services/_static/image21.png)
6. 輸入 Facebook 認證並按一下 [**登入**] 之後，您的網頁瀏覽器將會重新導向回您的 web 應用程式，這會提示您輸入要與 Facebook 帳戶產生關聯的**使用者名稱**：

    [![](external-authentication-services/_static/image24.png "Click to Expand the Image")](external-authentication-services/_static/image23.png)
7. 輸入您的使用者名稱並按一下 [**註冊**] 按鈕之後，您的 web 應用程式將會顯示您 Facebook 帳戶的預設**首頁**：

    [![](external-authentication-services/_static/image26.png "Click to Expand the Image")](external-authentication-services/_static/image25.png)

<a id="GOOGLE"></a>
## <a name="enabling-google-authentication"></a>啟用 Google 驗證

使用 Google 驗證時，您必須建立 Google 開發人員帳戶，而您的專案將需要來自 Google 的應用程式識別碼和秘密金鑰才能運作。 如需建立 Google 開發人員帳戶以及取得應用程式識別碼和秘密金鑰的詳細資訊，請參閱[https://developers.google.com](https://developers.google.com)。

若要為您的 web 應用程式啟用 Google 驗證，請使用下列步驟：

1. 當您的專案在 Visual Studio 2017 中開啟時，請開啟*Startup.Auth.cs*檔案。

2. 找出下列程式碼的 Google 驗證區段：

    [!code-csharp[Main](external-authentication-services/samples/sample4.cs)]
3. 移除 &quot;//&quot; 字元，將反白顯示的程式程式碼取消批註，然後新增您的應用程式識別碼和秘密金鑰。 加入這些參數之後，您就可以重新編譯專案：

    [!code-csharp[Main](external-authentication-services/samples/sample5.cs)]
4. 當您按 F5 在網頁瀏覽器中開啟 web 應用程式時，您會看到 Google 已定義為外部驗證服務：

    [![](external-authentication-services/_static/image75.png "Click to Expand the Image")](external-authentication-services/_static/image75.png)
5. 當您按一下 [ **google** ] 按鈕時，您的瀏覽器會被重新導向至 google 登入頁面：

    [![](external-authentication-services/_static/image32.png "Click to Expand the Image")](external-authentication-services/_static/image31.png)
6. 輸入您的 Google 認證並按一下 [登**入**] 之後，Google 會提示您確認您的 web 應用程式是否具有存取 Google 帳戶的許可權：

    [![](external-authentication-services/_static/image34.png "Click to Expand the Image")](external-authentication-services/_static/image33.png)
7. 當您按一下 [**接受**] 時，您的網頁瀏覽器將會重新導向回您的 web 應用程式，這會提示您輸入要與 Google 帳戶產生關聯的**使用者名稱**：

    [![](external-authentication-services/_static/image36.png "Click to Expand the Image")](external-authentication-services/_static/image35.png)
8. 輸入您的使用者名稱並按一下 [**註冊**] 按鈕之後，您的 web 應用程式將會顯示您 Google 帳戶的預設**首頁**：

    [![](external-authentication-services/_static/image38.png "Click to Expand the Image")](external-authentication-services/_static/image37.png)

<a id="MICROSOFT"></a>
## <a name="enabling-microsoft-authentication"></a>啟用 Microsoft 驗證

Microsoft 驗證會要求您建立開發人員帳戶，而且需要用戶端識別碼和用戶端密碼才能運作。 如需建立 Microsoft 開發人員帳戶及取得用戶端識別碼和用戶端密碼的詳細資訊，請參閱[https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070)。

取得取用者金鑰和取用者秘密後，請使用下列步驟來為您的 web 應用程式啟用 Microsoft 驗證：

1. 當您的專案在 Visual Studio 2017 中開啟時，請開啟*Startup.Auth.cs*檔案。

2. 找出 [Microsoft 驗證] 區段中的程式碼：

    [!code-csharp[Main](external-authentication-services/samples/sample6.cs)]
3. 移除 &quot;//&quot; 字元，將反白顯示的程式程式碼取消批註，然後新增您的用戶端識別碼和用戶端密碼。 加入這些參數之後，您就可以重新編譯專案：

    [!code-csharp[Main](external-authentication-services/samples/sample7.cs)]
4. 當您按 F5 在網頁瀏覽器中開啟 web 應用程式時，您會看到 Microsoft 已定義為外部驗證服務：

    [![](external-authentication-services/_static/image42.png "Click to Expand the Image")](external-authentication-services/_static/image41.png)
5. 當您按一下 [ **microsoft** ] 按鈕時，您的瀏覽器會被重新導向至 microsoft 登入頁面：

    [![](external-authentication-services/_static/image44.png "Click to Expand the Image")](external-authentication-services/_static/image43.png)
6. 在您輸入 Microsoft 認證並按一下 [登**入**] 之後，系統會提示您確認您的 web 應用程式是否有許可權可以存取您的 Microsoft 帳戶：

    [![](external-authentication-services/_static/image46.png "Click to Expand the Image")](external-authentication-services/_static/image45.png)
7. 當您按一下 **[是]** 時，您的網頁瀏覽器會重新導向回您的 web 應用程式，這會提示您輸入要與您的 Microsoft 帳戶建立關聯的**使用者名稱**：

    [![](external-authentication-services/_static/image48.png "Click to Expand the Image")](external-authentication-services/_static/image47.png)
8. 輸入您的使用者名稱並按一下 [**註冊**] 按鈕之後，您的 web 應用程式將會顯示 Microsoft 帳戶的預設**首頁**：

    [![](external-authentication-services/_static/image50.png "Click to Expand the Image")](external-authentication-services/_static/image49.png)

<a id="TWITTER"></a>
## <a name="enabling-twitter-authentication"></a>啟用 Twitter 驗證

Twitter 驗證會要求您建立開發人員帳戶，而且需要取用者金鑰和取用者密碼才能運作。 如需建立 Twitter 開發人員帳戶，以及取得取用者金鑰和取用者秘密的詳細資訊，請參閱[https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)。

取得取用者金鑰和取用者秘密後，請使用下列步驟來為您的 web 應用程式啟用 Twitter 驗證：

1. 當您的專案在 Visual Studio 2017 中開啟時，請開啟*Startup.Auth.cs*檔案。

2. 找出下列程式碼的 Twitter 驗證區段：

    [!code-csharp[Main](external-authentication-services/samples/sample8.cs)]
3. 移除 &quot;//&quot; 字元，將反白顯示的程式程式碼取消批註，然後新增您的取用者金鑰和取用者密碼。 加入這些參數之後，您就可以重新編譯專案：

    [!code-csharp[Main](external-authentication-services/samples/sample9.cs)]
4. 當您按 F5 在網頁瀏覽器中開啟 web 應用程式時，您會看到 Twitter 已定義為外部驗證服務：

    [![](external-authentication-services/_static/image54.png "Click to Expand the Image")](external-authentication-services/_static/image53.png)
5. 當您按一下 [ **twitter** ] 按鈕時，您的瀏覽器會被重新導向至 twitter 登入頁面：

    [![](external-authentication-services/_static/image56.png "Click to Expand the Image")](external-authentication-services/_static/image55.png)
6. 輸入您的 Twitter 認證並按一下 [**授權應用程式**] 之後，您的網頁瀏覽器將會重新導向回您的 web 應用程式，這會提示您輸入要與您的 Twitter 帳戶產生關聯的**使用者名稱**：

    [![](external-authentication-services/_static/image58.png "Click to Expand the Image")](external-authentication-services/_static/image57.png)
7. 輸入您的使用者名稱並按一下 [**註冊**] 按鈕之後，您的 web 應用程式將會顯示您 Twitter 帳戶的預設**首頁**：

    [![](external-authentication-services/_static/image60.png "Click to Expand the Image")](external-authentication-services/_static/image59.png)

<a id="MOREINFO"></a>
## <a name="additional-information"></a>其他資訊

如需建立使用 OAuth 和 OpenID 之應用程式的詳細資訊，請參閱下列 Url：

- [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)
- [https://go.microsoft.com/fwlink/?LinkID=243995](https://go.microsoft.com/fwlink/?LinkID=243995)

<a id="COMBINE"></a>
### <a name="combining-external-authentication-services"></a>結合外部驗證服務

如需更大的彈性，您可以同時定義多個外部驗證服務-這可讓您的 web 應用程式使用者從任何已啟用的外部驗證服務使用帳戶：

[![](external-authentication-services/_static/image62.png "Click to Expand the Image")](external-authentication-services/_static/image61.png)

<a id="FQDN"></a>
### <a name="configure-iis-express-to-use-a-fully-qualified-domain-name"></a>設定 IIS Express 使用完整功能變數名稱

某些外部驗證提供者不支援使用 HTTP 位址（如 `http://localhost:port/`）來測試您的應用程式。 若要解決這個問題，您可以將靜態完整功能變數名稱（FQDN）對應新增至您的 HOSTS 檔案，並在 Visual Studio 2017 中設定您的專案選項，以使用 FQDN 進行測試/的偵錯工具。 若要這樣做，請使用下列步驟：

- 新增靜態 FQDN 對應您的 HOSTS 檔案：

  1. 在 Windows 中開啟提升許可權的命令提示字元。
  2. 輸入下列命令：

      <kbd>記事本%WinDir%\system32\drivers\etc\hosts</kbd>
  3. 將類似下列的專案新增至 HOSTS 檔案：

      <kbd>127.0.0.1 www.wingtiptoys.com</kbd>
  4. 儲存並關閉主機檔案。

- 將您的 Visual Studio 專案設定為使用 FQDN：

  1. 當您的專案在 Visual Studio 2017 中開啟時，請按一下 [**專案**] 功能表，然後選取專案的屬性。 例如，您可以選取 [ **WebApplication1 屬性**]。
  2. 選取 [ **Web** ] 索引標籤。
  3. 輸入您的 [<strong>專案 Url</strong>] 的 FQDN。 例如，如果這是您新增至主機檔案的 FQDN 對應，您會輸入<kbd><http://www.wingtiptoys.com></kbd> 。

- 設定 IIS Express 以使用應用程式的 FQDN：

    1. 在 Windows 中開啟提升許可權的命令提示字元。
    2. 輸入下列命令以變更至您的 IIS Express 資料夾：

        <kbd>cd/d &quot;%ProgramFiles%\IIS Express&quot;</kbd>
    3. 輸入下列命令，將 FQDN 新增至您的應用程式：

        <kbd>appcmd.exe set config-section： system.web/sites/+&quot;[name = ' WebApplication1 ']。系結。[protocol = ' HTTP '，bindingInformation = ' *：80： www. wingtiptoys .com ']&quot;/commit： apphost</kbd>

  其中， **WebApplication1**是您專案的名稱，而**bindingInformation**包含您要用於測試的通訊埠編號和 FQDN。

<a id="OBTAIN"></a>
### <a name="how-to-obtain-your-application-settings-for-microsoft-authentication"></a>如何取得 Microsoft 驗證的應用程式設定

將應用程式連結到 Windows Live for Microsoft 驗證是一個簡單的流程。 如果您尚未將應用程式連結至 Windows Live，可以使用下列步驟：

1. 流覽至[https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070)並在出現提示時輸入您的 Microsoft 帳戶名稱和密碼，然後按一下 [登**入**]：

   <!--  [![](external-authentication-services/_static/image64.png "Click to Expand the Image")](external-authentication-services/_static/image63.png) -->
2. 選取 [**新增應用程式**]，並在出現提示時輸入應用程式的名稱，然後按一下 [**建立**]：

    [![](external-authentication-services/_static/image79.png "Click to Expand the Image")](external-authentication-services/_static/image79.png)
3. 在 [**名稱**] 底下選取您的應用程式，其應用程式屬性頁面隨即出現。

4. 輸入應用程式的重新導向網域。 複製 [**應用程式識別碼**]，然後在 [**應用程式**密碼] 底下，選取 [**產生密碼**]。 複製顯示的密碼。 應用程式識別碼和密碼是您的用戶端識別碼和用戶端秘密。 選取 **[確定]** ，然後按一下 [**儲存**]。

    [![](external-authentication-services/_static/image77.png "Click to Expand the Image")](external-authentication-services/_static/image77.png)

<a id="DISABLE"></a>
### <a name="optional-disable-local-registration"></a>選擇性：停用本機註冊

目前的 ASP.NET 本機註冊功能不會防止自動化程式（bot）建立成員帳戶;例如，藉由使用 bot 預防和驗證技術（例如[CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md)）。 因此，您應該移除登入頁面上的 [本機登入表單] 和 [註冊] 連結。 若要這麼做，請開啟專案中的 *\_Login. cshtml*  頁面，然後將 本機登入 面板和 註冊 連結的行加上批註。 產生的頁面看起來應該如下列程式碼範例所示：

[!code-html[Main](external-authentication-services/samples/sample10.html)]

一旦停用 [本機登入] 面板和註冊連結，您的登入頁面只會顯示您已啟用的外部驗證提供者：

[![](external-authentication-services/_static/image70.png "Click to Expand the Image")](external-authentication-services/_static/image69.png)
