---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: 使用 CAPTCHA 防止 Bot 使用您的 ASP.NET Web Razor）網站 |Microsoft Docs
author: microsoft
description: 本文說明如何使用 ReCaptcha （安全性措施）來防止自動化程式（bot）在 ASP.NET Web Pages （Razor）中執行工作 。
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 2647a3155893a3dfb3214795a5f9cf1e8931fa91
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78547044"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a>使用 CAPTCHA 防止 Bot 使用您的 ASP.NET Web Razor）網站

由[Microsoft](https://github.com/microsoft)

> 本文說明如何使用 ReCaptcha （安全性措施）來防止自動化程式（bot）在 ASP.NET Web Pages （Razor）網站中執行工作。
> 
> **您將瞭解的內容：** 
> 
> - 如何將 CAPTCHA 測試新增至您的網站。
> 
> 以下是文章中引進的 ASP.NET 功能：
> 
> - `ReCaptcha` helper。
> 
> > [!NOTE]
> > 本文中的資訊適用于 ASP.NET Web Pages 1.0 和 Web Pages 2。

## <a name="about-captchas"></a>關於 CAPTCHAs

每當您讓使用者在您的網站中註冊，或只是輸入名稱和 URL （例如，針對 blog 留言），您可能會收到大量的假名稱。 這些通常是由自動化程式（bot）所留下，會嘗試在每個可以找到的網站中留下 Url。 （常見的動機是張貼產品的 Url 以供銷售。）

當使用者註冊或輸入其名稱和網站時，您可以使用*CAPTCHA*來驗證使用者，藉此確保使用者是真正的人員，而不是電腦程式。 CAPTCHA 代表完全自動化的公用 Turing 測試，以告訴電腦和人類的與眾不同之處。 CAPTCHA 是一種*挑戰-回應*測試，使用者會在這種情況中執行一些動作，讓人員可以輕鬆執行，而不需要執行自動化程式。 最常見的 CAPTCHA 類型是您會看到一些失真字母，並要求您輸入它們的位置。 （扭曲應該會讓 bot 難以破解字母）。

## <a name="adding-a-recaptcha-test"></a>新增 ReCaptcha 測試

在 ASP.NET 網頁中，您可以使用 `ReCaptcha` helper 來呈現以 ReCaptcha 服務（[http://recaptcha.net](http://recaptcha.net)）為基礎的 CAPTCHA 測試。 `ReCaptcha` 協助程式會顯示兩個失真單字的影像，使用者必須在驗證頁面之前正確輸入。 使用者回應是由 ReCaptcha.Net 服務進行驗證。

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. 在 ReCaptcha.Net （[http://recaptcha.net](http://recaptcha.net)）註冊您的網站。 當您完成註冊時，將會取得公開金鑰和私密金鑰。
2. 如在[ASP.NET Web Pages 網站中安裝協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，將 ASP.NET Web Helper 程式庫新增至您的網站（如果尚未這麼做）。
3. 如果您還沒有 *\_AppStart. cshtml*檔案，請在網站的根資料夾中建立名為 *\_AppStart*的檔案。
4. 在 *\_AppStart*中新增下列 `Recaptcha` 協助程式設定： 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. 使用您自己的公開和私密金鑰來設定 `PublicKey` 和 `PrivateKey` 屬性。
6. 儲存 *\_AppStart* ，並將它關閉。
7. 在網站的根資料夾中，建立名為*Recaptcha*的新頁面。
8. 以下列內容取代現有的內容： 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. 在瀏覽器中執行*Recaptcha。* 如果 `PrivateKey` 值有效，頁面就會顯示 [ReCaptcha] 控制項和一個按鈕。 如果您未在 *\_AppStart*中全域設定金鑰，此頁面會顯示錯誤。 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. 輸入測試的文字。 如果您通過 ReCaptcha 測試，就會看到該效果的訊息。 否則，您會看到錯誤訊息，而且 ReCaptcha 控制項會重新顯示。

> [!NOTE]
> 如果您的電腦位於使用 proxy 伺服器的網域上，您可能需要設定*web.config*檔案的 `defaultproxy` 元素。 下列範例顯示已設定 `defaultproxy` 專案的*web.config*檔案，讓 ReCaptcha 服務能夠正常執行。
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他資源

- [針對 ASP.NET Web Pages 網站自訂全網站行為](https://go.microsoft.com/fwlink/?LinkId=202906)
- [ReCaptcha 網站](https://www.google.com/recaptcha)
