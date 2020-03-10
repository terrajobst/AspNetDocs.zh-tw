---
uid: web-api/overview/security/basic-authentication
title: ASP.NET Web API 中的基本驗證 |Microsoft Docs
author: MikeWasson
description: 描述在 ASP.NET Web API 中使用基本驗證。
ms.author: riande
ms.date: 10/02/2014
ms.assetid: 41423767-0021-47c3-9e53-0021b457c39f
msc.legacyurl: /web-api/overview/security/basic-authentication
msc.type: authoredcontent
ms.openlocfilehash: 1470bd4b5abd5199b9a5105973b053812d643351
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555724"
---
# <a name="basic-authentication-in-aspnet-web-api"></a>ASP.NET Web API 中的基本驗證

由[Mike Wasson](https://github.com/MikeWasson)

基本驗證是在 RFC 2617 中定義，也就是[HTTP 驗證：基本和摘要式存取驗證](http://www.ietf.org/rfc/rfc2617.txt)。

缺點

- 使用者認證會在要求中傳送。
- 認證會以純文字傳送。
- 認證會與每個要求一起傳送。
- 無法登出，除非結束瀏覽器會話。
- 容易遭受跨網站偽造要求（CSRF）;需要反 CSRF 量值。

優點

- 網際網路標準。
- 受到所有主要瀏覽器的支援。
- 相對簡單的通訊協定。

基本驗證的運作方式如下：

1. 如果要求需要驗證，伺服器會傳回401（未經授權）。 回應包含 WWW 驗證標頭，指出伺服器支援基本驗證。
2. 用戶端會使用 Authorization 標頭中的用戶端認證來傳送另一個要求。 認證會格式化為字串 "name： password"，以 base64 編碼。 認證不會加密。

基本驗證是在「領域」的內容中執行。 伺服器會在 WWW 驗證標頭中包含領域的名稱。 使用者的認證在該領域內是有效的。 領域的確切範圍是由伺服器所定義。 例如，您可以定義數個領域來分割資源。

![](basic-authentication/_static/image1.png)

因為認證會以未加密的形式傳送，基本驗證只會透過 HTTPS 保護。 請參閱[在 WEB API 中使用 SSL](working-with-ssl-in-web-api.md)。

基本驗證也容易遭受 CSRF 攻擊。 在使用者輸入認證之後，瀏覽器會在會話的持續時間內，自動將這些要求傳送至相同的網域。 這包括 AJAX 要求。 請參閱[防止跨網站偽造要求（CSRF）攻擊](preventing-cross-site-request-forgery-csrf-attacks.md)。

## <a name="basic-authentication-with-iis"></a>使用 IIS 進行基本驗證

IIS 支援基本驗證，但有一點要注意：使用者會針對其 Windows 認證進行驗證。 這表示使用者必須擁有伺服器網域上的帳戶。 對於公開的網站，您通常會想要針對 ASP.NET 成員資格提供者進行驗證。

若要使用 IIS 啟用基本驗證，請在 ASP.NET 專案的 web.config 中將驗證模式設定為 "Windows"：

[!code-xml[Main](basic-authentication/samples/sample1.xml)]

在此模式中，IIS 會使用 Windows 認證來進行驗證。 此外，您必須在 IIS 中啟用基本驗證。 在 IIS 管理員中，移至 [功能] [視圖]，選取 [驗證]，然後啟用 [基本驗證]

![](basic-authentication/_static/image2.png)

在您的 Web API 專案中，為任何需要驗證的控制器動作新增 `[Authorize]` 屬性。

用戶端會藉由在要求中設定 Authorization 標頭來驗證本身。 瀏覽器用戶端會自動執行此步驟。 Nonbrowser 用戶端將需要設定標頭。

## <a name="basic-authentication-with-custom-membership"></a>使用自訂成員資格進行基本驗證

如前所述，內建于 IIS 中的基本驗證會使用 Windows 認證。 這表示您需要在主控伺服器上為您的使用者建立帳戶。 但若是網際網路應用程式，使用者帳戶通常會儲存在外部資料庫中。

下列程式碼說明如何執行基本驗證的 HTTP 模組。 您可以藉由取代 `CheckPassword` 方法（在此範例中為虛擬方法），輕鬆地插入 ASP.NET 成員資格提供者。

在 Web API 2 中，您應該考慮撰寫[驗證篩選器](authentication-filters.md)或[OWIN 中介軟體](../../../aspnet/overview/owin-and-katana/index.md)，而不是 HTTP 模組。

[!code-csharp[Main](basic-authentication/samples/sample2.cs)]

若要啟用 HTTP 模組，請將下列內容新增至**system.webserver**區段中的 web.config 檔案：

[!code-xml[Main](basic-authentication/samples/sample3.xml?highlight=4)]

將 "YourAssemblyName" 取代為元件的名稱（不包括 "dll" 副檔名）。

您應該停用其他驗證配置，例如表單或 Windows 驗證。
