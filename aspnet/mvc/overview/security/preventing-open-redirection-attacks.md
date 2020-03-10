---
uid: mvc/overview/security/preventing-open-redirection-attacks
title: 防止開啟重新導向攻擊C#（） |Microsoft Docs
author: jongalloway
description: 本教學課程說明如何在 ASP.NET MVC 應用程式中防止開啟重新導向攻擊。 本教學課程將討論已進行的變更 。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 69fb02e0-f5b7-4c35-878c-fa87164fc785
msc.legacyurl: /mvc/overview/security/preventing-open-redirection-attacks
msc.type: authoredcontent
ms.openlocfilehash: cfa635d4fd14d031993c5b452325cbe334f82dc2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78538168"
---
# <a name="preventing-open-redirection-attacks-c"></a>預防開啟重新導向攻擊 (C#)

依[Jon Galloway](https://github.com/jongalloway)

> 本教學課程說明如何在 ASP.NET MVC 應用程式中防止開啟重新導向攻擊。 本教學課程會討論在 ASP.NET MVC 3 的 AccountController 中所做的變更，並示範如何將這些變更套用至現有的 ASP.NET MVC 1.0 和2應用程式。

## <a name="what-is-an-open-redirection-attack"></a>什麼是開放式重新導向攻擊？

重新導向至透過要求（例如 querystring 或表單資料）指定之 URL 的任何 web 應用程式，可能會遭到篡改，以將使用者重新導向至外部的惡意 URL。 這種篡改稱為開放式重新導向攻擊。

每當您的應用程式邏輯重新導向至指定的 URL 時，您都必須確認重新導向 URL 未遭到篡改。 ASP.NET MVC 1.0 和 ASP.NET MVC 2 的預設 AccountController 中使用的登入，容易受到開放式重新導向攻擊。 幸好，您可以輕鬆地更新現有的應用程式，以使用 ASP.NET MVC 3 Preview 的更正。

若要瞭解此弱點，讓我們看看登入重新導向在預設的 ASP.NET MVC 2 Web 應用程式專案中的運作方式。 在此應用程式中，嘗試流覽具有 [授權] 屬性的控制器動作，會將未經授權的使用者重新導向至/Account/LogOn view。 此重新導向至/Account/LogOn 會包含 returnUrl querystring 參數，讓使用者可以在成功登入之後，傳回給原始要求的 URL。

在下面的螢幕擷取畫面中，我們可以看到嘗試在未登入的情況下存取/Account/ChangePassword 視圖，會導致重新導向至/Account/LogOn？ReturnUrl =% 2fAccount% 2fChangePassword% 2f。

[![](preventing-open-redirection-attacks/_static/image2.png)](preventing-open-redirection-attacks/_static/image1.png)

**圖 01**：具有開啟重新導向的登入頁面

由於不會驗證 ReturnUrl querystring 參數，因此攻擊者可以修改它，以將任何 URL 位址插入參數中，以進行開啟的重新導向攻擊。 為了示範這一點，我們可以將 ReturnUrl 參數修改為[http://bing.com](http://bing.com)，因此產生的登入 URL 將會是/Account/LogOn？ReturnUrl =<http://www.bing.com/>。 成功登入網站後，我們會被重新導向至[http://bing.com](http://bing.com)。 由於此重新導向並未經過驗證，因此可以改為指向嘗試誘騙使用者的惡意網站。

### <a name="a-more-complex-open-redirection-attack"></a>更複雜的開放式重新導向攻擊

開啟重新導向攻擊特別危險，因為攻擊者知道我們正嘗試登入特定網站，這讓我們容易遭受[網路釣魚攻擊](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx)。 例如，攻擊者可能會將惡意電子郵件傳送給網站使用者，以嘗試捕獲他們的密碼。 讓我們看看如何在 NerdDinner 網站上執行這項作業。 （請注意，live NerdDinner 網站已更新為防止開啟重新導向攻擊）。

首先，攻擊者會將 NerdDinner 上登入頁面的連結傳送給我們，其中包含重新導向至其偽造的網頁：

[http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn](http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn)

請注意，傳回的 URL 會指向 nerddiner.com，這在「晚餐」中遺漏了「n」。 在此範例中，這是攻擊者所控制的網域。 當我們存取上述連結時，就會進入合法的 NerdDinner.com 登入頁面。

[![](preventing-open-redirection-attacks/_static/image4.png)](preventing-open-redirection-attacks/_static/image3.png)

**圖 02**：具有開啟重新導向的 NerdDinner 登入頁面

當我們正確登入時，ASP.NET MVC AccountController 的登入動作會將我們重新導向至 returnUrl querystring 參數中指定的 URL。 在此情況下，這是攻擊者所輸入的 URL，也就是[http://nerddiner.com/Account/LogOn](http://nerddiner.com/Account/LogOn)。 除非我們非常關注，否則我們很可能不會注意到這一點，特別是因為攻擊者已小心確定其偽造的頁面看起來與合法的登入頁面完全一樣。 此登入頁面包含一則錯誤訊息，要求我們再次登入。 笨拙我們，我們必須輸入密碼。

[![](preventing-open-redirection-attacks/_static/image6.png)](preventing-open-redirection-attacks/_static/image5.png)

**圖 03**：偽造的 NerdDinner 登入畫面

當我們重新輸入使用者名稱和密碼時，偽造的登入頁面會儲存資訊，並將我們傳回到合法的 NerdDinner.com 網站。 此時，NerdDinner.com 網站已驗證我們，因此偽造的登入頁面可以直接重新導向至該頁面。 最終結果是攻擊者有使用者名稱和密碼，但我們不知道我們已提供給他們。

## <a name="looking-at-the-vulnerable-code-in-the-accountcontroller-logon-action"></a>查看 AccountController 登入動作中的弱點程式碼

ASP.NET MVC 2 應用程式中登入動作的程式碼如下所示。 請注意，成功登入時，控制器會傳回 returnUrl 的重新導向。 您可以看到不會針對 returnUrl 參數執行任何驗證。

**清單1– `AccountController.cs` 中的 ASP.NET MVC 2 登入動作**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample1.cs)]

現在讓我們來看一下 ASP.NET MVC 3 登入動作的變更。 這個程式碼已變更為驗證 returnUrl 參數，方法是在名為 `IsLocalUrl()`的 System.web helper 類別中呼叫新的方法。

**清單2– `AccountController.cs` 中的 ASP.NET MVC 3 登入動作**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample2.cs)]

這已變更為藉由呼叫 System.web helper 類別中的新方法來驗證傳回 URL 參數，`IsLocalUrl()`。

## <a name="protecting-your-aspnet-mvc-10-and-mvc-2-applications"></a>保護您的 ASP.NET MVC 1.0 和 MVC 2 應用程式

我們可以藉由新增 IsLocalUrl （） helper 方法並更新登入動作來驗證 returnUrl 參數，以利用現有 ASP.NET MVC 1.0 和2個應用程式中的 ASP.NET MVC 3 變更。

UrlHelper IsLocalUrl （）方法實際上只會呼叫 System.web 中的方法，因為 ASP.NET Web Pages 應用程式也會使用此驗證。

**[清單 3] –來自 ASP.NET MVC 3 UrlHelper `class` 的 IsLocalUrl （）方法**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample3.cs)]

IsUrlLocalToHost 方法包含實際的驗證邏輯，如 [清單 4] 所示。

**從 System.web RequestExtensions 類別列出4– IsUrlLocalToHost （）方法**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample4.cs)]

在我們的 ASP.NET MVC 1.0 或2應用程式中，我們會在 AccountController 中新增 IsLocalUrl （）方法，但建議您盡可能將它新增至個別的 helper 類別。 我們會對 ASP.NET MVC 3 版本的 IsLocalUrl （）進行兩個小變更，使其可在 AccountController 內正常執行。 首先，我們會將它從公用方法變更為私用方法，因為控制器中的公用方法可以當作控制器動作來存取。 第二，我們將修改對應用程式主機檢查 URL 主機的呼叫。 該呼叫會使用 UrlHelper 類別中的本機 RequestCoNtext 欄位。 而不是使用此。RequestCoNtext，我們將使用此 Url。Request. Url. 主機。 下列程式碼顯示已修改的 IsLocalUrl （）方法，以便與 ASP.NET MVC 1.0 和2應用程式中的控制器類別搭配使用。

**[清單5– IsLocalUrl （）] 方法，其已修改以與 MVC 控制器類別搭配使用**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample5.cs)]

現在已備妥 IsLocalUrl （）方法，我們可以從登入動作呼叫它，以驗證 returnUrl 參數，如下列程式碼所示。

**[清單 6]-驗證 returnUrl 參數的已更新登入方法**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample6.cs)]

現在，我們可以嘗試使用外部傳回 URL 來登入，藉以測試開啟的重新導向攻擊。 讓我們使用/Account/LogOn 嗎？ReturnUrl = 再次<http://www.bing.com/>。

[![](preventing-open-redirection-attacks/_static/image8.png)](preventing-open-redirection-attacks/_static/image7.png)

**圖 04**：測試已更新的登入動作

成功登入之後，我們會被重新導向至主/索引控制器動作，而不是外部 URL。

[![](preventing-open-redirection-attacks/_static/image10.png)](preventing-open-redirection-attacks/_static/image9.png)

**圖 05**：開啟重新導向攻擊失效

## <a name="summary"></a>總結

當重新導向 Url 當做應用程式 URL 中的參數傳遞時，可能會發生開啟重新導向攻擊。 ASP.NET MVC 3 範本包含可防止開啟重新導向攻擊的程式碼。 您可以在 ASP.NET MVC 1.0 和2個應用程式的修改中新增此程式碼。 若要在登入 ASP.NET 1.0 和2個應用程式時防止開啟重新導向攻擊，請新增 IsLocalUrl （）方法，並驗證登入動作中的 returnUrl 參數。
