---
uid: web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
title: ASP.NET Web Pages （Razor）疑難排解指南 |Microsoft Docs
author: Rick-Anderson
description: 本文描述使用 ASP.NET Web Pages （Razor）時可能發生的問題，以及一些建議的解決方案。 軟體版本 ASP.NET Web Pag 。
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 2a2c1833-0bfe-4e2e-9cc0-341b52c7b121
msc.legacyurl: /web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
msc.type: authoredcontent
ms.openlocfilehash: fc03767c16f46c1e282d24ee3a7df2409a7c38bb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78585761"
---
# <a name="aspnet-web-pages-razor-troubleshooting-guide"></a>ASP.NET Web Pages (Razor) 疑難排解指南

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本文描述使用 ASP.NET Web Pages （Razor）時可能發生的問題，以及一些建議的解決方案。
> 
> ## <a name="software-versions"></a>軟體版本
> 
> 
> - ASP.NET Web Pages （Razor）3
>   
> 
> 本教學課程也適用于 ASP.NET Web Pages 2 和 ASP.NET Web Pages 1.0。

本主題包含下列各節：

- [執行頁面的問題](#Issues_Running_.cshtml_Pages)
- [Razor 程式碼的問題](#IssuesWithRazorCode)
- [安全性和成員資格的問題](#membership)
- [傳送電子郵件的問題](#email)
- [其他資源](#AdditionalResources)

如需一般問題，請參閱[ASP.NET Web Pages （Razor）常見問題](https://go.microsoft.com/fwlink/?LinkId=253000)。

<a id="Issues_Running_.cshtml_Pages"></a>
## <a name="issues-with-running-pages"></a>執行頁面的問題

各種不同的問題可能會導致*cshtml*和*vbhtml*頁面無法正常運作。 本節列出常見的錯誤訊息和可能的原因。

### <a name="http-error-403---forbidden-access-is-denied"></a>HTTP 錯誤 403-禁止：拒絕存取

*您無權使用您提供的認證來查看此目錄或網頁。*

如果伺服器未執行正確的 .NET Framework 版本，就會發生此錯誤。 請確定執行伺服器（本機或遠端）的電腦至少已安裝 .NET Framework 4。 也請確定應用程式本身已設定為執行正確的版本。

如果您在 WebMatrix 中工作時在本機看到此問題，請按一下 [**網站**] 工作區，然後在 treeview 中按一下 [**設定**]。 在 [**選取 .NET Framework 版本**] 清單中，選取 [ **.Net 4 （整合式）** ]。 如果已設定此版本，請嘗試以系統管理員身分執行 WebMatrix。

請確定您網站的根目錄中至少有一個*cshtml*檔案。

如果網頁伺服器位於遠端伺服器上時看到此錯誤，請洽詢伺服器管理員。 請確定伺服器已安裝 .NET Framework 4 或更新版本。 也請確定應用程式是在設定為使用該版本 the.NET Framework 的應用程式集區中執行。

如果您可以控制伺服器，請確定它正在執行正確的 .NET Framework 版本。 您也可以執行 `aspnet_regiis -iru` 命令來嘗試修復安裝。 （例如，如果您在安裝 .NET Framework 之後安裝 IIS，則 IIS 將不會正確設定為執行 ASP.NET 網頁。）如需詳細資訊，請參閱[ASP.NET IIS 註冊工具（Aspnet\_regiis）](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx)。

### <a name="http-error-40314---forbidden"></a>HTTP 錯誤 403.14-禁止

*網頁伺服器已設定為不列出此目錄的內容。*

如果您要求受保護的資源（例如*web.config*檔案），或在受保護的資料夾（例如*應用程式\_資料*或*應用程式\_碼*）中，就會發生此錯誤。

### <a name="http-error-40417---not-found"></a>HTTP 錯誤 404.17-找不到

*要求的內容似乎是腳本，因此靜態檔案處理常式不會提供服務。*

如果伺服器未正確設定為使用 .NET Framework 4 或更新版本，因而無法辨識 `@{ }` 區塊中的程式碼，就會發生此錯誤。 請參閱稍早的 < *HTTP 錯誤 403-禁止的描述：拒絕存取*。

### <a name="http-error-4047---not-found"></a>HTTP 錯誤 404.7-找不到

*要求篩選模組設定為拒絕副檔名*

如果伺服器上已明確封鎖 *. cshtml*或*vbhtml*延伸模組，就會發生這個錯誤。 這個問題的徵兆是，當 Url 不包含副檔名，但包含 *. cshtml*或*vbhtml*的 url 無法使用時，就會執行。 可能的解決方法是在*網站的 web.config*檔案中重新啟用延伸模組。 下列範例顯示如何啟用 *.* # 副檔名。

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample1.xml?highlight=5-6)]

### <a name="http-error-4048---not-found"></a>HTTP 錯誤 404.8-找不到

*要求篩選模組設定為拒絕包含 hiddenSegment 區段之 URL 中的路徑。*

如果您要求受保護的資源（例如*web.config*檔案），或在受保護的資料夾（例如*應用程式\_資料*或*應用程式\_碼*）中，就會發生此錯誤。

### <a name="this-type-of-page-is-not-served-server-error-in--application"></a>未提供此類型的頁面（'/' 應用程式中的伺服器錯誤）

請參閱稍早的 HTTP 錯誤404.17 說明。

<a id="IssuesWithRazorCode"></a>
## <a name="issues-with-razor-code"></a>Razor 程式碼的問題

### <a name="the-name-class-does-not-exist-in-the-current-context"></a>名稱 '*class*' 不存在於目前的內容中

通常，您會看到此錯誤的原因是 `class` 參考協助程式，但未安裝 helper。 例如，如果您嘗試使用協助程式，但未從 NuGet 安裝套件，您將會看到此錯誤。 使用 WebMatrix 中的圖庫來尋找並安裝協助程式。

如果已安裝協助程式，但頁面仍無法辨識，請嘗試新增 [將 `using` 語句加入至程式碼]。 在 `using` 語句中，參考包含 helper 的命名空間。 例如，ASP.NET Web helper 套件中的基本協助程式位於 `System.Web.Helpers` 命名空間中。 在您要使用 helper 的頁面頂端，新增下列程式程式碼：

`@using Microsoft.Web.Helpers;`

<a id="membership"></a>
## <a name="issues-with-security-and-membership"></a>安全性和成員資格的問題

如果您使用 ASP.NET Web Pages （Razor）中的內建安全性（成員資格）系統，您可能會遇到下列問題。

### <a name="to-call-this-method-the-membershipprovider-property-must-be-an-instance-of-extendedmembershipprovider"></a>若要呼叫此方法，"成員資格. Provider" 屬性必須是 "ExtendedMembershipProvider" 的實例。

此錯誤可能表示未設定任何 `AspNetSqlMembershipProvider` 類別。 （徵兆是網站在本機運作正常，但當您將此錯誤發行至主機服務提供者的伺服器時，會擲回此錯誤）。此問題的一個修正是將下列內容新增至網站的*web.config*檔案，明確啟用簡單的成員資格：

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample2.xml?highlight=6)]

<a id="email"></a>
## <a name="issues-with-sending-email"></a>傳送電子郵件的問題

傳送電子郵件的問題可能會很難進行 debug。 最初的問題可能是您無法連接到 SMTP 伺服器。 如果連接成功，請 ASP.NET 將訊息交給 SMTP 伺服器。 不過，可能會有訊息本身的問題，而導致 SMTP 伺服器無法傳送它。

如果您的應用程式未成功傳送電子郵件，請嘗試下列動作：

- SMTP 伺服器名稱通常類似 `smtp.provider.com` 或 `smtp.provider.net`。 不過，如果您將網站發佈至主機服務提供者，該點的 SMTP 伺服器名稱可能會 `localhost`。 發生這種情況的原因是，當您發佈，而且您的網站在提供者的伺服器上執行之後，SMTP 伺服器可能會從您的應用程式觀點來看。 伺服器名稱的這項變更可能表示您必須在發佈程式中變更 SMTP 伺服器名稱。
- 埠號碼通常是25。 不過，某些提供者會要求您使用埠587或其他通訊埠。 向 SMTP 伺服器的擁有者確認他們預期使用的埠號碼。
- 請確定您使用正確的認證。 如果您已將您的網站發佈至主控提供者，請使用提供者特別指出的認證做為電子郵件。 這些認證可能與您用來發佈的認證不同。
- 有時候您不需要認證。 如果您是使用個人 ISP 來傳送電子郵件，您的電子郵件提供者可能已經知道您的認證。 發行之後，您可能需要使用與在本機電腦上測試時不同的認證。
- 如果您的電子郵件提供者使用加密，請將 `WebMail.EnableSsl` 設定為 `true`。

如果傳送電子郵件時發生錯誤，您可能會看到標準的 ASP.NET 錯誤訊息，如下所示：

![當電子郵件發生問題時 ASP.NET 錯誤訊息](aspnet-web-pages-razor-troubleshooting-guide/_static/image1.png)

您也可以使用 `try-catch` 區塊來偵測傳送電子郵件的問題，如下列範例所示。 當您使用 `try-catch` 區塊時，ASP.NET 不會顯示其標準錯誤訊息。 相反地，您可以在區塊的 `catch` 部分中捕捉錯誤。

[!code-cshtml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample3.cshtml)]

請以適當的值取代 `your-SMTP-server-name`，依此類推。 某些您可能會看到的錯誤訊息包括下列各項：

- *無法傳送郵件。*

    -或-

    *連線嘗試失敗，因為連接的合作物件在一段時間內未正確回應，或建立的連線失敗，因為連接的主機無法回應*

    此錯誤通常表示應用程式無法連接到 SMTP 伺服器。 檢查伺服器名稱和埠號碼。
- *信箱無法使用。伺服器回應為： 5.1.0 &lt;someuser@invaliddomain&gt; 寄件者拒絕：不正確寄件者網域*

    此訊息可能表示 `From` 位址不正確或遺失。
- *指定的字串不是電子郵件地址所需的格式。*

    此錯誤可能表示 `To` 或 `From` 屬性的值無法辨識為電子郵件地址。 （ASP.NET 無法檢查電子郵件地址是否有效，只有其格式正確，如 *name@domain.com* 。）

> [!NOTE]
> 將頁面發行至即時網站之前，請先移除顯示錯誤的標記（`@errorMessage`）。 讓使用者看得到從伺服器取得的錯誤訊息並不是個好主意。

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>其他資源

[ASP.NET Web Pages (Razor) 常見問題集](https://go.microsoft.com/fwlink/?LinkId=253000)

ASP.NET 網站上的[WebMatrix 和 ASP.NET Web Pages](https://forums.asp.net/1224.aspx/1?WebMatrix)論壇
