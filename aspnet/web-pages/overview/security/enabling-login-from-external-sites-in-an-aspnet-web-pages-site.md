---
uid: web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
title: 使用 ASP.NET Web Pages （Razor）網站中的外部網站登入 |Microsoft Docs
author: Rick-Anderson
description: 本文說明如何使用 Facebook、Google、Twitter、Yahoo 和其他網站登入您的 ASP.NET Web Pages （Razor）網站，也就是如何支援 。
ms.author: riande
ms.date: 02/21/2014
ms.assetid: ef852096-a5bf-47b3-9945-125cde065093
msc.legacyurl: /web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 860b75422c3df1d191ed861344963bfc19270e8f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638751"
---
# <a name="logging-in-using-external-sites-in-an-aspnet-web-pages-razor-site"></a>使用 ASP.NET Web Pages （Razor）網站中的外部網站登入

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本文說明如何使用 Facebook、Google、Twitter、Yahoo 和其他網站登入您的 ASP.NET Web Pages （Razor）網站，也就是如何在您的網站中支援 OAuth 和 OpenID。
> 
> 您將學到什麼：
> 
> - 當您使用 WebMatrix 入門網站範本時，如何啟用其他網站的登入。
> 
> 這是本文中引進的 ASP.NET 功能：
> 
> - `OAuthWebSecurity` helper。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - ASP.NET Web Pages （Razor）2
> - WebMatrix 3

ASP.NET Web Pages 包含[OAuth](http://oauth.net/)和[OpenID](http://openid.net/)提供者的支援。 使用這些提供者，您可以讓使用者使用他們在 Facebook、Twitter、Microsoft 和 Google 的現有認證來登入您的網站。 例如，若要使用 Facebook 帳戶登入，使用者可以直接選擇 Facebook 圖示，這會將他們重新導向至他們輸入其使用者資訊的 Facebook 登入頁面。 然後，他們可以在您的網站上建立 Facebook 登入與其帳戶的關聯。 網頁成員資格功能的相關加強之處在于，使用者可以在您的網站上建立多個登入（包括來自社交網路網站的登入）與單一帳戶的關聯。

此圖顯示「**入門網站**」範本的登入頁面，使用者可以在其中選擇 Facebook、Twitter、Google 或 Microsoft 圖示，以使用外部帳戶進行登入：

![外部提供者](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image1.png)

您可以藉由在**入門網站**範本中取消批註幾行程式碼，來啟用 OAuth 和 OpenID 成員資格。 您用來處理 OAuth 和 OpenID 提供者的方法和屬性是在 `WebMatrix.Security.OAuthWebSecurity` 類別中。 **入門網站**範本包含完整的成員資格基礎結構、登入頁面、成員資格資料庫，以及您需要的所有程式碼，讓使用者可以使用本機認證或其他網站登入您的網站。

本節提供一個範例，說明如何讓使用者從外部網站登入以**入門網站**範本為基礎的網站。 建立入門網站之後，您可以執行此動作（詳細資料請遵循）：

- 針對使用 OAuth 提供者（Facebook、Twitter 和 Microsoft）的網站，您可以在外部網站上建立應用程式。 這會提供您需要的應用程式金鑰，以便叫用這些網站的登入功能。
- 針對使用 OpenID 提供者（Google）的網站，您不需要建立應用程式。 針對所有這些網站，您必須擁有一個帳戶，才能登入並建立開發人員應用程式。

    > [!NOTE]
    > Microsoft 應用程式只接受工作網站的即時 URL，因此您無法使用本機網站 URL 來測試登入。
- 編輯網站中的一些檔案，以指定適當的驗證提供者，並將登入提交至您要使用的網站。

本文提供下列工作的個別指示：

- [啟用 Google 登入](#To_enable_Google_logins)
- [啟用 Facebook 登入](#To_enable_Facebook_logins)
- [啟用 Twitter 登入](#To_enable_Twitter_logins)

<a id="To_enable_Google_logins"></a>
## <a name="enabling-google-logins"></a>啟用 Google 登入

1. 建立或開啟以 WebMatrix 入門網站範本為基礎的 ASP.NET Web Pages 網站。
2. 開啟 *\_AppStart*  頁面，並取消批註下列程式程式碼。 

    [!code-css[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample1.css)]

### <a name="testing-google-login"></a>測試 Google 登入

1. 執行您網站的*預設. cshtml*頁面，然後選擇 [**登入**] 按鈕。
2. 在 [*登*入] 頁面的 **[使用另一個服務登入**] 區段中，選擇 [ **Google** ] 或 [ **Yahoo** ] [提交] 按鈕。 這個範例會使用 Google 登入。 

    網頁會將要求重新導向至 Google 登入頁面。

    ![Google 登入](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image2.png)
3. 輸入現有 Google 帳戶的認證。
4. 如果 Google 詢問您是否要允許*Localhost*使用帳戶中的資訊，請按一下 [**允許**]。

    程式碼會使用 Google 權杖來驗證使用者，然後回到網站上的這個頁面。 此頁面可讓使用者將其 Google 登入與您網站上的現有帳戶產生關聯，或者可以在您的網站上註冊新的帳戶，以將外部登入與建立關聯。

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image3.png)
5. 選擇 [**關聯**] 按鈕。 瀏覽器會回到您應用程式的首頁。

<a id="To_enable_Facebook_logins"></a>
## <a name="enabling-facebook-logins"></a>啟用 Facebook 登入

1. 前往[Facebook 開發人員網站](https://developers.facebook.com/apps)（如果您尚未登入，請登入）。
2. 選擇 [**建立新的應用程式**] 按鈕，然後遵循提示來命名和建立新的應用程式。
3. 在 [**選取您的應用程式將如何與 Facebook 整合**] 區段中，選擇 [**網站**] 區段。
4. 在 [**網站 url** ] 欄位中填入您的網站 url （例如 `http://www.example.com`）。 [**網域**] 欄位是選擇性的;您可以使用這個來提供整個網域（例如*example.com*）的驗證。 

    > [!NOTE]
    > 如果您是在本機電腦上使用類似 `http://localhost:12345` 的 URL 執行網站（其中數位是本機埠號碼），您可以將此值新增至 [**網站 URL** ] 欄位，以測試您的網站。 不過，每當您本機網站的埠號碼變更時，您都必須更新應用程式的**網站 URL**欄位。
5. 選擇 [**儲存變更**] 按鈕。
6. 再次選擇 [**應用**程式] 索引標籤，然後查看應用程式的 [起始頁]。
7. 複製應用程式的「**應用程式識別碼**」和「**應用程式密碼**」值，並將其貼到暫存的文字檔中。 您會將這些值傳遞至您網站程式碼中的 Facebook 提供者。
8. 結束 Facebook 開發人員網站。

現在您會變更網站中的兩個頁面，讓使用者能夠使用他們的 Facebook 帳戶登入網站。

1. 建立或開啟以 WebMatrix 入門網站範本為基礎的 ASP.NET Web Pages 網站。
2. 開啟 *\_AppStart*  頁面，並將 Facebook OAuth 提供者的程式碼取消批註。 取消批註程式碼區塊如下所示： 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample2.cs)]
3. 將 Facebook 應用程式的 [**應用程式識別碼**] 值複製為 `appId` 參數的值（在引號內）。
4. 複製 Facebook 應用程式中的**應用程式密碼**值，做為 `appSecret` 參數值。
5. 儲存並關閉檔案。

### <a name="testing-facebook-login"></a>測試 Facebook 登入

1. 執行網站的 [*預設. cshtml* ] 頁面，然後選擇 [**登**入] 按鈕。
2. 在 [*登*入] 頁面的 [**使用另一個服務登入**] 區段中，選擇 [ **Facebook** ] 圖示。 

    網頁會將要求重新導向至 Facebook 登入頁面。

    ![oauth-2](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image4.png)
3. 登入 Facebook 帳戶。 

    程式碼會使用 Facebook 權杖來驗證您的身分，然後返回頁面，您可以在其中將 Facebook 登入與網站登入產生關聯。 您的使用者名稱或電子郵件地址會填入表單上的 [**電子郵件**] 欄位中。

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image5.png)
4. 選擇 [**關聯**] 按鈕。 

    瀏覽器會回到首頁，而且您已登入。

<a id="To_enable_Twitter_logins"></a>
## <a name="enabling-twitter-logins"></a>啟用 Twitter 登入

1. 流覽至[Twitter 開發人員網站](https://dev.twitter.com/)。
2. 選擇 [**建立應用程式**] 連結，然後登入網站。
3. 在 [**建立應用程式**] 表單上，填寫 [**名稱**] 和 [**描述**] 欄位。
4. 在 [**網站**] 欄位中，輸入您網站的 URL （例如，`http://www.example.com`）。 

    > [!NOTE]
    > 如果您要在本機測試您的網站（使用如 `http://localhost:12345`的 URL），Twitter 可能不會接受 URL。 不過，您可能可以使用本機回送 IP 位址（例如 `http://127.0.0.1:12345`）。 這可簡化在本機測試應用程式的流程。 不過，每次本機網站的埠號碼變更時，您都必須更新應用程式的 [**網站**] 欄位。
5. 在 [**回呼 URL** ] 欄位中，輸入您的網站中要讓使用者在登入 Twitter 之後返回的頁面 URL。 例如，若要將使用者傳送至入門網站的首頁（可辨識其登入狀態），請輸入您在 [**網站**] 欄位中輸入的相同 URL。
6. 接受條款，然後選擇 [**建立您的 Twitter 應用程式**] 按鈕。
7. 在 [**我的應用程式**] 登陸頁面上，選擇您所建立的應用程式。
8. 在 [**詳細資料**] 索引標籤上，流覽至底部，然後選擇 [**建立我的存取權 Token** ] 按鈕。
9. 在 [**詳細資料**] 索引標籤上，複製應用程式的取用**者金鑰**和取用**者密碼**值，並將其貼到暫存文字檔中。 您會將這些值傳遞至您網站程式碼中的 Twitter 提供者。
10. 結束 Twitter 網站。

現在您會變更網站中的兩個頁面，讓使用者能夠使用其 Twitter 帳戶登入網站。

1. 建立或開啟以 WebMatrix 入門網站範本為基礎的 ASP.NET Web Pages 網站。
2. 開啟 [ *\_AppStart* ] 頁面，並取消批註 Twitter OAuth 提供者的程式碼。 取消批註程式碼區塊看起來像這樣： 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample3.cs)]
3. 將 Twitter 應用程式的取用**者金鑰**值複製為 `consumerKey` 參數的值（在引號內）。
4. 將 Twitter 應用程式的取用**者秘密**值複製為 `consumerSecret` 參數的值。
5. 儲存並關閉檔案。

### <a name="testing-twitter-login"></a>測試 Twitter 登入

1. 執行您網站的*預設. cshtml*頁面，然後選擇 [**登**入] 按鈕。
2. 在 [*登*入] 頁面的 [**使用另一個服務登入**] 區段中，選擇**Twitter**圖示。 

    網頁會將要求重新導向至您所建立之應用程式的 Twitter 登入頁面。

    ![oauth-4](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image6.png)
3. 登入 Twitter 帳戶。
4. 程式碼會使用 Twitter 權杖來驗證使用者，然後將您返回頁面，您可以在其中將登入與您的網站帳戶建立關聯。 您的姓名或電子郵件地址會填入表單上的 [**電子郵件**] 欄位中。

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image7.png)
5. 選擇 [**關聯**] 按鈕。 

    瀏覽器會回到首頁，而且您已登入。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他資源

- [自訂全網站行為](https://go.microsoft.com/fwlink/?LinkId=202906)
- [新增 ASP.NET Web Pages 網站的安全性和成員資格](https://go.microsoft.com/fwlink/?LinkID=202904)
