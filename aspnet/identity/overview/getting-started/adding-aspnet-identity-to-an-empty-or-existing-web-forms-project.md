---
uid: identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project
title: 將 ASP.NET Identity 新增至空白或現有的 Web form 專案-ASP.NET 4。x
author: raquelsa
description: 本教學課程說明如何將 ASP.NET Identity （ASP.NET 的成員資格系統）新增至 ASP.NET 應用程式。 當您建立新的 Web form 或 MVC 時 。
ms.author: riande
ms.date: 01/22/2019
ms.assetid: 1cbc0ed2-5bd6-4b62-8d34-4c193dcd8b25
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: 8e82951d57f0b8052ee3f6530a7470be7d030206
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584123"
---
# <a name="adding-aspnet-identity-to-an-empty-or-existing-web-forms-project"></a>將 ASP.NET Identity 新增至空的或現有的 Web Form 專案

> 本教學課程說明如何將[ASP.NET Identity](introduction-to-aspnet-identity.md) （ASP.NET 的新成員資格系統）新增至 ASP.NET 應用程式。
> 
> 當您使用個別帳戶在 Visual Studio 2017 RTM 中建立新的 Web form 或 MVC 專案時，Visual Studio 會安裝所有必要的套件，並為您新增所有必要的類別。 本教學課程將說明將 ASP.NET Identity 支援加入現有 Web Forms 專案或新的空白專案的步驟。 我將概述您需要安裝的所有 NuGet 套件，以及您需要新增的類別。 我將探討用來註冊新使用者和登入的範例 Web 表單，同時強調所有主要進入點 Api 以進行使用者管理和驗證。 這個範例會針對以 Entity Framework 為基礎的 SQL 資料儲存體，使用 ASP.NET Identity 預設的執行。 本教學課程中，我們將使用 LocalDB 作為 SQL database。
> 

## <a name="get-started-with-aspnet-identity"></a>開始使用 ASP.NET Identity

1. 從安裝和執行[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)開始。
2. 從 [開始] 頁面選取 [**新增專案**]，或者您可以使用功能表並依**序選取 [** 檔案] 和 [**新增專案**]。
3. 在左窗格中，依序展開 [**視覺效果C#** ] 和 [ **web**]，然後選取 [ **ASP.NET Web 應用程式（.net Framework）** ]。 將專案命名為 "WebFormsIdentity"，然後選取 **[確定]** 。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image17.png)
4. 在 [**新增 ASP.NET 專案**] 對話方塊中，選取 [**空白**] 範本。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image2.png)  
  
   請注意，[**變更驗證**] 按鈕已停用，而且此範本未提供任何驗證支援。 Web Forms、MVC 和 Web API 範本可讓您選取驗證方法。

## <a name="add-identity-packages-to-your-app"></a>將身分識別套件新增至您的應用程式

在方案總管中，以滑鼠右鍵按一下您的專案，然後選取 [**管理 NuGet 套件**]。 搜尋**EntityFramework**套件，並安裝。 
  
![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image15.png)
  
請注意，此封裝將會安裝相依性套件： **EntityFramework**和**Microsoft ASP.NET 身分識別核心**。

## <a name="add-a-web-form-to-register-users"></a>新增 web 表單以註冊使用者

1. 在**方案總管**中，以滑鼠右鍵按一下您的專案，然後依序選取 [**新增**] 和 [ **Web 表單**]。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image4.png)
2. 在 [**指定專案的名稱**] 對話方塊中，為新的 web 表單**註冊**命名，然後選取 **[確定]** 。
3. 將產生的*Register .aspx*檔案中的標記取代為下列程式碼。 程式碼變更已醒目提示。 

    [!code-html[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample1.aspx?highlight=9,12-40)]

    > [!NOTE]
    > 這只是當您建立新的 ASP.NET Web form 專案時，所建立的*Register .aspx*檔案的簡化版本。 上述標記會新增表單欄位和按鈕來註冊新的使用者。
4. 開啟*Register.aspx.cs*檔案，並以下列程式碼取代檔案的內容：

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample2.cs)]

    > [!NOTE] 
    > 
    > 1. 上述程式碼是*Register.aspx.cs*檔案的簡化版本，當您建立新的 ASP.NET Web Forms 專案時會建立此檔案。
    > 2. *IdentityUser*類別是*IUser*介面的預設 EntityFramework 執行。 *IUser*介面是 ASP.NET Identity 核心上使用者的最基本介面。
    > 3. *UserStore*類別是使用者存放區的預設 EntityFramework 執行。 這個類別會實 ASP.NET Identity 核心的最基本介面： *IUserStore*、 *IUserLoginStore*、 *IUserClaimStore*和*IUserRoleStore*。
    > 4. *UserManager*類別會公開使用者相關的 api，其會自動將變更儲存至*UserStore*。
    > 5. *IdentityResult*類別代表身分識別作業的結果。
5. 在**方案總管**中，以滑鼠右鍵按一下您的專案，然後選取 [**新增**]、[**新增 ASP.NET 資料夾**] 和 [**應用程式\_資料**]。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image5.png)
6. 開啟*web.config*檔案，並為我們將用來儲存使用者資訊的資料庫新增連接字串專案。 資料庫將會在執行時間透過 EntityFramework 識別實體來建立。 當您建立新的 Web form 專案時，連接字串類似于為您建立的。 反白顯示的程式碼會顯示您應該新增的標記：

    [!code-xml[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample3.xml?highlight=11-14)]
    
    > [!NOTE] 
    > 若為 Visual Studio 2015 或更高版本，請將 `(localdb)\v11.0` 取代為連接字串中的 `(localdb)\MSSQLLocalDB`。
    
7. 以滑鼠右鍵按一下專案*中的 [* 檔案] [登錄]，然後選取 [**設定為起始頁**]。 按 Ctrl + F5 以建立並執行 web 應用程式。 輸入新的 [使用者名稱] 和 [密碼]，然後選取 [**註冊**]。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image6.png)  

    > [!NOTE]
    > ASP.NET Identity 支援驗證，在此範例中，您可以確認來自身分識別核心套件的使用者和密碼驗證程式的預設行為。 使用者的預設驗證程式（`UserValidator`）有一個屬性 `AllowOnlyAlphanumericUserNames`，其預設值設為 `true`。 密碼的預設驗證程式（`MinimumLengthValidator`）可確保密碼至少有6個字元。 這些驗證程式是 `UserManager` 的屬性，如果您想要擁有自訂驗證，可以覆寫這些內容。

## <a name="verify-the-localdb-identity-database-and-tables-generated-by-entity-framework"></a>確認 LocalDb 識別資料庫和產生的資料表 Entity Framework

1. 在 [ **View** ] 功能表中，選取 [**伺服器總管**]。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image7.png)
2. 展開 **[DefaultConnection （WebFormsIdentity）** ]，展開 [**資料表]** ，以滑鼠右鍵按一下**AspNetUsers** ，然後選取 [**顯示資料表資料**]。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image8.png)  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image9.png)

## <a name="configure-the-application-for-owin-authentication"></a>設定應用程式以進行 OWIN authentication

此時，我們只新增了建立使用者的支援。 現在，我們將示範如何新增驗證以登入使用者。 ASP.NET Identity 使用 Microsoft OWIN Authentication 中介軟體進行表單驗證。 OWIN Cookie 驗證是以 Cookie 和宣告為基礎的驗證機制，可供[OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx)或 IIS 上裝載的任何架構使用。 使用此模型，可以跨多個架構使用相同的驗證套件，包括 ASP.NET MVC 和 Web Forms。 如需有關專案 Katana 以及如何在主機上執行中介軟體的詳細資訊，請參閱[使用 Katana 專案消費者入門](https://msdn.microsoft.com/magazine/dn451439.aspx)。

## <a name="install-authentication-packages-to-your-application"></a>將驗證套件安裝到您的應用程式

1. 在方案總管中，以滑鼠右鍵按一下您的專案，然後選取 [**管理 NuGet 套件**]。 搜尋***Owin***套件，並安裝。 
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image16.png)

2. 搜尋並安裝***Owin SystemWeb***套件。

    > [!NOTE]
    > **Owin**套件包含一組 Owin 擴充功能類別，可用來管理和設定 ASP.NET Identity 核心套件所使用的 Owin authentication 中介軟體。
    > **SystemWeb**套件包含 Owin 伺服器，可讓 Owin 型應用程式使用 ASP.NET 要求管線在 IIS 上執行。 如需詳細資訊，請參閱[IIS 整合式管線中的 OWIN 中介軟體](../../../aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline.md)。

## <a name="add-owin-startup-and-authentication-configuration-classes"></a>新增 OWIN 啟動和驗證設定類別

1. 在**方案總管**中，以滑鼠右鍵按一下您的專案，然後依**序選取 [新增]** 和 [**加入新專案**]。 在 [搜尋文字方塊] 對話方塊中，輸入 "*owin*"。 將類別命名為「*啟動*」，然後選取 [**新增**]。 
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image11.png)
2. 在 Startup.cs 檔案中，新增如下所示的反白顯示程式碼，以設定 OWIN cookie 驗證。

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample4.cs?highlight=1,3,15-19)]

    > [!NOTE]
    > 此類別包含用來指定 OWIN 啟動類別的 `OwinStartup` 屬性。 每個 OWIN 應用程式都有一個啟動類別，您可以在其中指定應用程式管線的元件。 如需此模型的詳細資訊，請參閱[OWIN 啟動類別偵測](../../../aspnet/overview/owin-and-katana/owin-startup-class-detection.md)。

## <a name="add-web-forms-for-registering-and-signing-in-users"></a>新增用於註冊和登入使用者的 web 表單

1. 開啟*Register.aspx.cs*檔案，並新增下列程式碼，以在註冊成功時登入使用者。

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample5.cs)]

    > [!NOTE] 
    > 
    > - 由於 ASP.NET Identity 和 OWIN Cookie 驗證是以宣告為基礎的系統，因此架構會要求應用程式開發人員為使用者產生[ClaimsIdentity](https://msdn.microsoft.com/library/microsoft.identitymodel.claims.claimsidentity.aspx) 。 ClaimsIdentity 包含使用者所有宣告的相關資訊，例如使用者所屬的角色。 您也可以在這個階段為使用者新增更多宣告。
    > - 您可以使用 OWIN 中的 AuthenticationManager 來登入使用者，並呼叫 `SignIn` 並傳入 ClaimsIdentity，如上所示。 這段程式碼也會登入使用者，並產生 cookie。 此呼叫類似于[FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)模組所使用的[FormAuthentication. SetAuthCookie](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) 。
2. 在**方案總管**中，以滑鼠右鍵按一下您的專案，然後依序選取 [**新增**] 和 [ **Web 表單**]。 為 web 表單**登**入命名。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image12.png)
3. 將*登入 .aspx*檔案的內容取代為下列程式碼：

    [!code-aspx[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample6.aspx)]
4. 以下列內容取代*Login.aspx.cs*檔案的內容：

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample7.cs)]

    > [!NOTE] 
    > 
    > - `Page_Load` 現在會檢查目前使用者的狀態，並根據其 `Context.User.Identity.IsAuthenticated` 狀態採取動作。
    >   **顯示已登入的使用者名稱**： Microsoft ASP.NET 身分識別架構已在[IIdentity](https://msdn.microsoft.com/library/system.security.principal.iidentity.aspx)上新增擴充方法，可讓您取得已登入使用者的 `UserName` 和 `UserId`。 這些擴充方法會在 `Microsoft.AspNet.Identity.Core` 元件中定義。 這些擴充方法是[HttpCoNtext.User.Identity.Name](https://msdn.microsoft.com/library/system.web.httpcontext.user.aspx)的取代。
    > - 登入方法： `This` 方法會取代此範例中先前的 `CreateUser_Click` 方法，並在成功建立使用者之後，立即登入使用者。   
    >   Microsoft OWIN Framework 在 `System.Web.HttpContext` 上新增了擴充方法，可讓您取得 `IOwinContext`的參考。 這些擴充方法會在 `Microsoft.Owin.Host.SystemWeb` 元件中定義。 `OwinContext` 類別會公開 `IAuthenticationManager` 屬性，其代表目前要求上可用的驗證中介軟體功能。 您可以使用 OWIN 中的 `AuthenticationManager` 登入使用者，並呼叫 `SignIn` 並傳入 `ClaimsIdentity`，如上所示。 由於 ASP.NET Identity 和 OWIN Cookie 驗證是以宣告為基礎的系統，因此架構會要求應用程式為使用者產生 `ClaimsIdentity`。 `ClaimsIdentity` 包含使用者所有宣告的相關資訊，例如使用者所屬的角色。 您也可以在這個階段為使用者新增更多宣告，這段程式碼也會登入使用者並產生 cookie。 此呼叫類似于[FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)模組所使用的[FormAuthentication. SetAuthCookie](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) 。
    > - `SignOut` 方法：從 OWIN 取得 `AuthenticationManager` 的參考，並呼叫 `SignOut`。 這類似于[FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)模組所使用的[FormsAuthentication. SignOut](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx)方法。
5. 按**Ctrl + F5**以建立並執行 web 應用程式。 輸入新的 [使用者名稱] 和 [密碼]，然後選取 [**註冊**]。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image13.png)  
   注意：此時會建立新的使用者並登入。
6. 選取 [**登出**] 按鈕。 系統會將您重新導向至 [登入] 表單。
7. 輸入不正確使用者名稱或密碼，然後選取 [**登入**] 按鈕。 
   `UserManager.Find` 方法會傳回 null，且會顯示錯誤訊息：「*不正確使用者名稱或密碼*」。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image14.png)
