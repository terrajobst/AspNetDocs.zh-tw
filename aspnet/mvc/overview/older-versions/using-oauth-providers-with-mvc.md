---
uid: mvc/overview/older-versions/using-oauth-providers-with-mvc
title: 搭配使用 OAuth 提供者與 MVC 4 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程會示範如何建立 ASP.NET MVC 4 web 應用程式，讓使用者能夠以來自外部提供者的認證登入，例如 Facebo 。
ms.author: riande
ms.date: 06/19/2013
ms.assetid: 7a87f16f-0e19-4f15-a88a-094ae866c4a2
msc.legacyurl: /mvc/overview/older-versions/using-oauth-providers-with-mvc
msc.type: authoredcontent
ms.openlocfilehash: 5dfd1305376a62f4987caea242ca0f6aac1018e9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539078"
---
# <a name="using-oauth-providers-with-mvc-4"></a>使用 OAuth 提供者與 MVC 4

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本教學課程會示範如何建立 ASP.NET MVC 4 web 應用程式，讓使用者能夠使用來自外部提供者（例如 Facebook、Twitter、Microsoft 或 Google）的認證進行登入，然後將這些提供者的一些功能整合到您的web 應用程式。 為了簡單起見，本教學課程著重于使用 Facebook 的認證。
> 
> 若要在 ASP.NET MVC 5 web 應用程式中使用外部認證，請參閱[使用 Facebook 和 Google OAuth2 和 OpenID 登入建立 ASP.NET MVC 5 應用](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)程式。
> 
> 在您的網站中啟用這些認證可提供顯著的優點，因為數百萬名使用者已經有這些外部提供者的帳戶。 如果您不需要建立和記住一組新的認證，這些使用者可能更傾向于註冊您的網站。 此外，在使用者透過這些提供者的其中之一登入之後，您可以從提供者併入社交作業。

## <a name="what-youll-build"></a>您將建立的內容

本教學課程中有兩個主要目標：

1. 讓使用者能夠使用 OAuth 提供者的認證進行登入。
2. 從提供者取出帳戶資訊，並將該資訊與您網站的帳戶註冊進行整合。

雖然本教學課程中的範例著重于使用 Facebook 做為驗證提供者，但您可以修改程式碼來使用任何提供者。 執行任何提供者的步驟，與您在本教學課程中會看到的步驟非常類似。 當您直接呼叫提供者的 API 集時，您只會注意到顯著的差異。

## <a name="prerequisites"></a>Prerequisites

- [適用于 Web 的](https://www.microsoft.com/visualstudio/eng/downloads#d-2012-express) [Microsoft Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads#vs)或 Microsoft Visual Studio Express 2012

或

- Microsoft Visual Studio 2010 SP1 或[Visual Web Developer Express 2010 SP1](https://www.microsoft.com/visualstudio/eng/downloads#d-2010-express)
- [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)

此外，本主題假設您有 ASP.NET MVC 和 Visual Studio 的基本知識。 如果您需要 ASP.NET MVC 4 的簡介，請參閱[ASP.NET mvc 4 簡介](getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)。

## <a name="create-the-project"></a>建立專案

在 Visual Studio 中，建立新的 ASP.NET MVC 4 Web 應用程式，並將它命名 &quot;OAuthMVC&quot;。 您可以將目標設為 .NET Framework 4.5 或4。

![建立專案](using-oauth-providers-with-mvc/_static/image1.png)

在 [新增 ASP.NET MVC 4 專案] 視窗中，選取 [**網際網路應用程式**]，並將**Razor**保留為 view engine。

![選取網際網路應用程式](using-oauth-providers-with-mvc/_static/image2.png)

## <a name="enable-a-provider"></a>啟用提供者

當您使用 網際網路應用程式 範本建立 MVC 4 web 應用程式時，系統會在應用程式\_開始 資料夾中，使用名為 AuthConfig.cs 的檔案來建立專案。

![AuthConfig 檔案](using-oauth-providers-with-mvc/_static/image3.png)

AuthConfig 檔案包含用來註冊外部驗證提供者之用戶端的程式碼。 根據預設，此程式碼會加上批註，因此不會啟用任何外部提供者。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample1.cs)]

您必須將此程式碼取消批註，才能使用外部驗證用戶端。 您只會取消批註您想要包含在網站中的提供者。 在本教學課程中，您只會啟用 Facebook 認證。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample2.cs)]

請注意，在上述範例中，方法會針對註冊參數包含空字串。 如果您嘗試立即執行應用程式，應用程式會擲回引數例外狀況，因為參數不允許空字串。 若要提供有效的值，您必須向外部提供者註冊您的網站，如下一節所示。

## <a name="registering-with-an-external-provider"></a>向外部提供者註冊

若要使用外部提供者的認證來驗證使用者，您必須向提供者註冊您的網站。 當您註冊網站時，您會收到註冊用戶端時所要包含的參數（例如金鑰或識別碼，以及密碼）。 您必須擁有您想要使用之提供者的帳戶。

本教學課程不會顯示向這些提供者註冊所需執行的所有步驟。 這些步驟通常並不容易。 若要成功註冊您的網站，請遵循這些網站上提供的指示。 若要開始註冊您的網站，請參閱開發人員網站，以取得：

- [Facebook](https://developers.facebook.com/)
- [Google](https://developers.google.com/)
- [Microsoft](http://manage.dev.live.com/)
- [Twitter](https://dev.twitter.com/)

向 Facebook 註冊您的網站時，您可以提供網站網域的 &quot;localhost&quot; 和 URL 的 `&quot; http://localhost/&quot;`，如下圖所示。 使用 localhost 可與大部分的提供者搭配運作，但目前不適用於 Microsoft 提供者。 針對 Microsoft 提供者，您必須包含有效的網站 URL。

![註冊網站](using-oauth-providers-with-mvc/_static/image4.png)

在上圖中，已移除應用程式識別碼、應用程式密碼及連絡人電子郵件的值。 當您實際註冊網站時，這些值將會存在。 您會想要記下 [應用程式識別碼] 和 [應用程式密碼] 的值，因為您會將其新增至您的應用程式。

## <a name="creating-test-users"></a>建立測試使用者

如果您不介意使用現有的 Facebook 帳戶來測試您的網站，可以略過本節。

您可以在 Facebook 應用程式管理頁面中，輕鬆地為您的應用程式建立測試使用者。 您可以使用這些測試帳戶來登入您的網站。 若要建立測試使用者，請按一下左側流覽窗格中的 [**角色**] 連結，然後按一下 [**建立**] 連結。

![建立測試使用者](using-oauth-providers-with-mvc/_static/image5.png)

Facebook 網站會自動建立您要求的測試帳戶數目。

## <a name="adding-application-id-and-secret-from-the-provider"></a>從提供者新增應用程式識別碼和密碼

既然您已從 Facebook 接收識別碼和秘密，請回到 AuthConfig 檔案，並將它們新增為參數值。 以下顯示的值不是真正的值。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample3.cs)]

## <a name="log-in-with-external-credentials"></a>使用外部認證登入

這就是在您的網站中啟用外部認證所需執行的動作。 執行您的應用程式，然後按一下右上角的 [登入] 連結。 此範本會自動辨識您已註冊 Facebook 做為提供者，並包含提供者的按鈕。 如果您註冊多個提供者，則會自動包含每一個提供者的按鈕。

![外部登入](using-oauth-providers-with-mvc/_static/image6.png)

本教學課程未涵蓋如何自訂外部提供者的 [登入] 按鈕。 如需相關資訊，請參閱[使用 OAuth/OpenID 自訂登入 UI](https://blogs.msdn.com/b/pranav_rastogi/archive/2012/08/24/customizing-the-login-ui-when-using-oauth-openid.aspx)。

按一下 [Facebook] 按鈕以使用 Facebook 認證登入。 當您選取其中一個外部提供者時，系統會將您重新導向至該網站，並提示該服務登入。

下圖顯示 Facebook 的登入畫面。 它會注意到您使用 Facebook 帳戶來登入名為 oauthmvcexample 的網站。

![facebook 驗證](using-oauth-providers-with-mvc/_static/image7.png)

以 Facebook 認證登入之後，頁面會通知使用者該網站將可存取基本資訊。

![要求許可權](using-oauth-providers-with-mvc/_static/image8.png)

選取 [**移至應用程式**] 之後，使用者必須註冊網站。 下圖顯示使用者以 Facebook 認證登入後的註冊頁面。 使用者名稱通常會預先填入提供者的名稱。

![註冊](using-oauth-providers-with-mvc/_static/image9.png)

按一下 [**註冊**] 以完成註冊。 關閉瀏覽器。

您可以看到新的帳戶已新增至您的資料庫。 在伺服器總管中，開啟**DefaultConnection**資料庫，並開啟 [**資料表]** 資料夾。

![資料庫資料表](using-oauth-providers-with-mvc/_static/image10.png)

以滑鼠右鍵按一下 [ **UserProfile** ] 資料表，然後選取 [**顯示資料表資料**]。

![顯示資料](using-oauth-providers-with-mvc/_static/image11.png)

您會看到您新增的帳戶。 查看**網頁\_OAuthMembership**資料表中的資料。 您會看到更多與您剛新增之帳戶的外部提供者相關的資料。

如果您只想要啟用外部驗證，就大功告成了。 不過，您可以進一步將提供者的資訊整合到新的使用者註冊程式中，如下列各節所示。

## <a name="create-models-for-additional-user-information"></a>建立其他使用者資訊的模型

如您在先前各節中所注意，您不需要取得任何額外的資訊，讓內建帳戶註冊能夠正常執行。 不過，大部分的外部提供者會傳回使用者的其他相關資訊。 下列各節顯示如何保留該資訊，並將它儲存至資料庫。 具體而言，您會保留使用者完整名稱的值、使用者個人網頁的 URI，以及指出 Facebook 是否已驗證帳戶的值。

您將使用[Code First 移轉](https://msdn.microsoft.com/data/jj591621)來新增資料表，以儲存額外的使用者資訊。 您要將資料表加入現有的資料庫中，因此您必須先建立目前資料庫的快照集。 藉由建立目前資料庫的快照集，您可以在稍後建立只包含新資料表的遷移。 若要建立目前資料庫的快照集：

1. 開啟 [**套件管理員主控台**]
2. 執行命令**啟用-遷移**
3. 執行命令**新增-遷移初始– IgnoreChanges**
4. 執行命令**update-database**

現在，您將加入新的屬性。 在 [模型] 資料夾中，開啟 AccountModels.cs 檔案，並尋找 RegisterExternalLoginModel 類別。 RegisterExternalLoginModel 類別包含從驗證提供者傳回的值。 新增名為 FullName 和 Link 的屬性，如下所示。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample4.cs?highlight=9-13)]

此外，在 AccountModels.cs 中，新增名為 ExtraUserInformation 的新類別。 此類別代表將在資料庫中建立的新資料表。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample5.cs)]

在 UsersCoNtext 類別中，新增下列反白顯示的程式碼，以建立新類別的 DbSet 屬性。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample6.cs?highlight=9)]

您現在已準備好建立新的資料表。 再次開啟 [套件管理員主控台]，這次：

1. 執行命令**新增-遷移 AddExtraUserInformation**
2. 執行命令**update-database**

新的資料表現在存在於資料庫中。

## <a name="retrieve-the-additional-data"></a>取得其他資料

有兩種方式可取得其他使用者資料。 第一種方式是在驗證要求期間保留傳回的使用者資料（根據預設值）。 第二種方式是特別呼叫提供者 API，並要求詳細資訊。 「FullName」和「連結」的值會由 Facebook 自動回傳。 值，指出 Facebook 是否已通過對 Facebook API 的呼叫來驗證帳戶。 首先，您將填入 [FullName] 和 [連結] 的值，之後您將會取得已驗證的值。

若要取出其他使用者資料，請開啟 [**控制器**] 資料夾中的**AccountController.cs**檔案。

此檔案包含用來記錄、註冊和管理帳戶的邏輯。 特別要注意的是名為**ExternalLoginCallback**和**ExternalLoginConfirmation**的方法。 在這些方法中，您可以加入程式碼，以自訂應用程式的外部登入作業。 **ExternalLoginCallback**方法的第一行包含：

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample7.cs)]

在**VerifyAuthentication**方法傳回的**AuthenticationResult**物件的**ExtraData**屬性中，會傳回額外的使用者資料。 Facebook 用戶端會在**ExtraData**屬性中包含下列值：

- id
- 名稱
- 連結
- gender
- accesstoken

其他提供者在 ExtraData 屬性中將會有類似但稍微不同的資料。

如果使用者不熟悉您的網站，您將會抓取一些額外的資料，並將該資料傳遞給確認視圖。 只有在使用者不熟悉您的網站時，才會執行方法中的最後一個程式碼區塊。 取代下列程式程式碼：

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample8.cs)]

改用這行︰

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample9.cs)]

這種變更只會包含 FullName 和 Link 屬性的值。

在**ExternalLoginConfirmation**方法中，修改下面反白顯示的程式碼，以儲存額外的使用者資訊。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample10.cs?highlight=4,7-13)]

## <a name="adjusting-the-view"></a>調整視圖

您從提供者取得的其他使用者資料將會顯示在 [註冊] 頁面中。

在  **Views** /**帳戶** 資料夾中，開啟**ExternalLoginConfirmation**。 在 [使用者名稱] 的現有欄位底下，新增 [FullName]、[連結] 和 [PictureLink] 的欄位。

[!code-cshtml[Main](using-oauth-providers-with-mvc/samples/sample11.cshtml)]

您現在已準備好執行應用程式，並使用儲存的其他資訊來註冊新的使用者。 您的帳戶必須尚未向網站註冊。 您可以使用不同的測試帳戶，或刪除**UserProfile**和網頁中的資料列， **\_OAuthMembership**資料表來尋找您想要重複使用的帳戶。 藉由刪除這些資料列，您將可確保帳戶已再次註冊。

執行應用程式，並註冊新的使用者。 請注意，這次 [確認] 頁面包含更多的值。

![註冊](using-oauth-providers-with-mvc/_static/image12.png)

完成註冊之後，請關閉瀏覽器。 查看資料庫，以注意**ExtraUserInformation**資料表中的新值。

## <a name="install-nuget-package-for-facebook-api"></a>安裝 Facebook API 的 NuGet 套件

Facebook 提供您可以呼叫以執行作業的[API](https://developers.facebook.com/docs/reference/apis/) 。 您可以藉由傳送 HTTP 要求，或使用安裝可協助傳送這些要求的 NuGet 套件來呼叫 Facebook API。 本教學課程中會顯示使用 NuGet 套件，但不一定要安裝 NuGet 套件。 本教學課程說明如何使用 Facebook C# SDK 套件。 還有其他可協助呼叫 Facebook API 的 NuGet 套件。

從 [**管理 NuGet 封裝**] 視窗中，選取C# [Facebook SDK] 套件。

![安裝套件](using-oauth-providers-with-mvc/_static/image13.png)

您將使用 Facebook C# SDK 來呼叫需要使用者存取權杖的作業。 下一節將說明如何取得存取權杖。

## <a name="retrieve-access-token"></a>取得存取權杖

在驗證使用者的認證之後，大部分的外部提供者都會傳回存取權杖。 此存取權杖非常重要，因為它可讓您呼叫僅適用于已驗證使用者的作業。 因此，當您想要提供更多功能時，抓取和儲存存取權杖是不可或缺的。

視外部提供者而定，存取權杖在有限的時間內可能有效。 為確保您擁有有效的存取權杖，您會在每次使用者登入時將它取出，並將其儲存為會話值，而不是將它儲存到資料庫。

在**ExternalLoginCallback**方法中，存取權杖也會在**AuthenticationResult**物件的**ExtraData**屬性中傳回。 將反白顯示的程式碼新增至**ExternalLoginCallback** ，以將存取權杖儲存在**Session**物件中。 每次使用者以 Facebook 帳戶登入時，就會執行此程式碼。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample12.cs?highlight=11-14)]

雖然此範例會從 Facebook 取得存取權杖，您可以透過名為 &quot;accesstoken&quot;的相同金鑰，從任何外部提供者抓取存取權杖。

## <a name="logging-off"></a>登出

預設的**登出**方法會將使用者登出您的應用程式，但不會將使用者登出外部提供者。 若要將使用者登出 Facebook，並在使用者登出之後防止權杖保存，您可以將下列反白顯示的程式碼新增至 AccountController 中的**登出**方法。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample13.cs?highlight=6-14)]

您在 `next` 參數中提供的值是使用者登出 Facebook 後要使用的 URL。 在您的本機電腦上進行測試時，您會為本機網站提供正確的埠號碼。 在生產環境中，您會提供預設頁面，例如 contoso.com。

## <a name="retrieve-user-information-that-requires-the-access-token"></a>取得需要存取權杖的使用者資訊

既然您已儲存存取權杖並已安裝 Facebook C# SDK 套件，您可以一起使用它們來要求 facebook 中的其他使用者資訊。 在**ExternalLoginConfirmation**方法中，藉由傳遞存取權杖的值來建立**FacebookClient**類別的實例。 針對目前的已驗證使用者，要求**已驗證**屬性的值。 [**已驗證**] 屬性會指出 Facebook 是否已透過其他方式驗證帳戶，例如傳送訊息至行動電話。 將此值儲存在資料庫中。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample14.cs?highlight=7-18,25)]

您必須為使用者刪除資料庫中的記錄，或使用不同的 Facebook 帳戶。

執行應用程式，並註冊新的使用者。 查看 [ **ExtraUserInformation** ] 資料表以查看 [已驗證] 屬性的值。

## <a name="conclusion"></a>結論

在本教學課程中，您已建立與 Facebook 整合的網站，以進行使用者驗證和註冊資料。 您已瞭解 MVC 4 web 應用程式所設定的預設行為，以及如何自訂該預設行為。

## <a name="related-topics"></a>相關主題

- [使用驗證和 SQL DB 建立 ASP.NET MVC 應用程式並部署至 Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)
