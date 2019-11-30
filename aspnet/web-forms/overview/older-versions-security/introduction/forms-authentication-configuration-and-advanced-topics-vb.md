---
uid: web-forms/overview/older-versions-security/introduction/forms-authentication-configuration-and-advanced-topics-vb
title: 表單驗證設定和 Advanced 主題（VB） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將檢查各種形式的驗證設定，並瞭解如何透過 forms 元素加以修改。 這將需要詳細的 。
ms.author: riande
ms.date: 01/14/2008
ms.assetid: 829d2f56-5c48-445b-b826-3418a450c788
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/forms-authentication-configuration-and-advanced-topics-vb
msc.type: authoredcontent
ms.openlocfilehash: 4d77816a489a4fa16cd70ec4214cd2f8ee563029
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74632165"
---
# <a name="forms-authentication-configuration-and-advanced-topics-vb"></a>表單驗證組態和進階主題 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/ASPNET_Security_Tutorial_03_VB.zip)或[下載 PDF](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial03_AuthAdvanced_vb.pdf)

> 在本教學課程中，我們將檢查各種形式的驗證設定，並瞭解如何透過 forms 元素加以修改。 這將需要詳細的探討自訂表單驗證票證的超時值、使用具有自訂 URL 的登入頁面（例如 login .aspx 而不是 Login .aspx）和無 cookie 的表單驗證票證。

## <a name="introduction"></a>簡介

在[上一個教學](an-overview-of-forms-authentication-vb.md)課程中，我們探討了在 ASP.NET 應用程式中執行表單驗證所需的步驟，從在 web.config 中指定 configuration 設定來建立登入頁面，以顯示已驗證和匿名使用者的不同內容。 回想一下，我們已設定網站使用表單驗證，方法是將 &lt;authentication&gt; 元素的 mode 屬性設為 Forms。 &lt;authentication&gt; 元素可以選擇性地包含 &lt;表單&gt; 子專案，而您可以在其中指定表單驗證設定的種類。

在本教學課程中，我們將檢查各種形式的驗證設定，並瞭解如何透過 &lt;forms&gt; 元素加以修改。 這將需要詳細的探討自訂表單驗證票證的超時值、使用具有自訂 URL 的登入頁面（例如 login .aspx 而不是 Login .aspx）和無 cookie 的表單驗證票證。 我們也會更仔細地檢查表單驗證票證的構成，並查看 ASP.NET 採取的預防措施，以確保票證的資料不受檢查和篡改的保護。 最後，我們將探討如何在表單驗證票證中儲存額外的使用者資料，以及如何透過自訂主體物件來建立此資料的模型。

## <a name="step-1-examining-the-ltformsgt-configuration-settings"></a>步驟1：檢查 &lt;表單&gt; 設定

ASP.NET 中的表單驗證系統提供許多設定，可依應用程式逐一進行自訂。 這包括如下的設定：表單驗證票證的存留期;套用到票證的保護類型;在何種情況下會使用無 cookie 驗證票證;登入頁面的路徑;和其他資訊。 若要修改預設值，請將[&lt;表單&gt; 元素](https://msdn.microsoft.com/library/1d3t3c61.aspx)新增為[&lt;authentication&gt;](https://msdn.microsoft.com/library/532aee0e.aspx)專案的子系，並指定您想要自訂為 XML 屬性的屬性值，如下所示：

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample1.xml)]

[表 1] 摘要說明可透過 &lt;forms&gt; 元素自訂的屬性。 因為 web.config 是一個 XML 檔案，所以左欄中的屬性名稱會區分大小寫。

| <strong>屬性</strong> |                                                                                                                                                                                                                                     <strong>說明</strong>                                                                                                                                                                                                                                      |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         cookie         |                                                                                                                這個屬性會指定在哪些條件下，驗證票證會儲存在 cookie 中，而不是內嵌在 URL 中。 允許的值為： UseCookies;UseUri;檢測和 UseDeviceProfile （預設值）。 步驟2會更詳細地檢查這項設定。                                                                                                                |
|         defaultUrl         |                                                                                                                                                         指出如果查詢字串中沒有指定 RedirectUrl 值，使用者在登入頁面後重新導向至的 URL。 預設值為 default.aspx。                                                                                                                                                         |
|           domain           | 當使用以 cookie 為基礎的驗證票證時，此設定會指定 cookie 的網域值。 預設值為空字串，這會導致瀏覽器使用其發行所在的網域（例如 www.yourdomain.com）。 在此情況下，對子域進行要求時，<strong>不</strong>會傳送 cookie，例如 admin.yourdomain.com。 如果您想要將 cookie 傳遞給所有子域，您需要自訂網域屬性，將其設定為 yourdomain.com。 |
|  enableCrossAppRedirects   |                                                                                                                                                                   布林值，指出當重新導向至相同伺服器上其他 web 應用程式中的 Url 時，是否要記住已驗證的使用者。 預設為 false。                                                                                                                                                                   |
|          loginUrl          |                                                                                                                                                                                                                      登入頁面的 URL。 預設值為 login .aspx。                                                                                                                                                                                                                      |
|            {2&gt;名稱&lt;2}            |                                                                                                                                                                                                   使用以 cookie 為基礎的驗證票證時，是 cookie 的名稱。 預設為.ASPXAUTH.                                                                                                                                                                                                   |
|            path            |                                                                             當使用以 cookie 為基礎的驗證票證時，此設定會指定 cookie 的 path 屬性。 Path 屬性可讓開發人員將 cookie 的範圍限制為特定的目錄階層。 預設值為/，會通知瀏覽器將驗證票證 cookie 傳送至對網域提出的任何要求。                                                                              |
|         保護 - protection         |                                                                                                                                            指出用來保護表單驗證票證的技術。 允許的值為： All （預設值）;加密無和驗證。 步驟3會詳細討論這些設定。                                                                                                                                            |
|         requireSSL         |                                                                                                                                                                                布林值，指出是否需要 SSL 連線才能傳輸驗證 cookie。 預設值為 false。                                                                                                                                                                                |
|     slidingExpiration      |                                                                                                 布林值，指出每次使用者在單一會話中造訪網站時，是否重設驗證 cookie 的超時時間。 預設值為 True。 在指定票證的超時值一節中，將會更詳細地討論驗證票證超時原則。                                                                                                 |
|          逾時           |                                                                                                                               指定驗證票證 cookie 到期的時間（以分鐘為單位）。 預設值是 30。 在指定票證的超時值一節中，將會更詳細地討論驗證票證超時原則。                                                                                                                               |

**表 1**： &lt;表單&gt; 元素屬性的摘要

在 ASP.NET 2.0 和更高的範圍中，預設的表單驗證值會在 .NET Framework 的 FormsAuthenticationConfiguration 類別中硬式編碼。 任何修改都必須以應用程式為基礎，在 web.config 檔案中套用。 這與 ASP.NET 1.x 不同，其中預設的表單驗證值會儲存在 machine.config 檔案中（因此可透過編輯 machine.config 進行修改）。 在 ASP.NET 1.x 的主題中，值得一提的是，有一些表單驗證系統設定在 ASP.NET 2.0 中具有不同的預設值，而不是 ASP.NET 1.x。 如果您要從 ASP.NET 1.x 環境遷移應用程式，請務必留意這些差異。 如需差異清單，請參閱[&lt;表單&gt; 元素技術檔](https://msdn.microsoft.com/library/1d3t3c61.aspx)。

> [!NOTE]
> 數種形式的驗證設定，例如 timeout、網域和路徑，會指定產生的表單驗證票證 cookie 的詳細資料。 如需 cookie、其使用方式和其各種屬性的詳細資訊，請閱讀[此 cookie 教學](http://www.quirksmode.org/js/cookies.html)課程。

### <a name="specifying-the-tickets-timeout-value"></a>指定票證的超時值

表單驗證票證是代表身分識別的權杖。 使用以 cookie 為基礎的驗證票證時，此權杖會以 cookie 的形式保存，並在每個要求中傳送至 web 伺服器。 擁有權杖，基本上就是宣告、我的使用者*名稱*、我已經登入，而且會使用，以便在頁面流覽時記住使用者的身分識別。

表單驗證票證不僅包含使用者的身分識別，還包含可協助確保權杖完整性和安全性的資訊。 畢竟，我們不希望惡意使用者能夠建立假冒權杖，或是以某種 underhanded 的方式修改合法 token。

票證中包含的其中一項資訊是*到期*日，也就是票證不再有效的日期和時間。 每次又稱為 formsauthenticationmodule 檢查驗證票證時，它會確保票證的到期時間尚未通過。 如果有，則會忽略票證，並將使用者識別為匿名。 這種防護措施有助於防範重新執行攻擊。 如果駭客能夠取得使用者的有效驗證票證（也許是藉由取得電腦的實體存取權並透過 cookie 進行對應），他們就可以使用此竊取的驗證票證，將要求傳送到伺服器，而不會過期。取得專案。 雖然到期不會防止這種情況，但它會限制在這種情況下，這類攻擊可能會成功的時段。

> [!NOTE]
> 步驟3會詳細說明表單驗證系統用來保護驗證票證的其他技術。

建立驗證票證時，表單驗證系統會藉由查閱 timeout 設定來判斷其到期日。 如表1所示，timeout 設定的預設值為30分鐘，這表示當表單驗證票證建立時，其到期日會設定為未來的日期和時間30分鐘。

到期日會定義表單驗證票證到期時的絕對時間。 但是，開發人員通常會想要執行滑動到期，每次使用者重提網站時都會重設一個。 此行為取決於 slidingExpiration 設定。 如果設定為 true （預設值），則每次又稱為 formsauthenticationmodule 驗證使用者時，就會更新票證的到期日。 如果設定為 false，就不會在每個要求上更新到期日，因而導致票證在第一次建立票證的過去分鐘數剛好過期。

> [!NOTE]
> 儲存在驗證票證中的到期日是絕對日期和時間值，如8月2日 2008 11:34 AM。 此外，日期和時間會相對於 web 伺服器的當地時間。 這項設計決策在日光節約時間（DST）上可能會有一些有趣的副作用，也就是美國的時鐘在一小時後移動時（假設 web 伺服器裝載于觀察日光節約時間的地區設定）。 請考慮在 DST 開始時間接近30分鐘到期的 ASP.NET 網站會發生什麼事（位於上午2:00）。 假設造訪者登入位於2008年3月11日上午1:55 的網站。 這會產生「表單驗證票證」，其會在2008年3月11日上午2:25 （未來30分鐘）到期。 不過，一旦 2:00 AM 擲回，時鐘就會因為 DST 而跳到 3:00 AM。 當使用者在登入後6分鐘（上午3:01）載入新的頁面時，又稱為 formsauthenticationmodule 會注意到票證已過期，並將使用者重新導向至登入頁面。 如需此和其他驗證票證超時奇觀以及因應措施的詳細討論，請挑選一份 Stefan Schackow 的*專業 ASP.NET 2.0 安全性、成員資格和角色管理*（ISBN：978-0-7645-9698-8）。

[圖 1] 說明當 slidingExpiration 設定為 false 且 timeout 設定為30時的工作流程。 請注意，在登入時產生的驗證票證包含到期日，而此值不會在後續要求時更新。 如果又稱為 formsauthenticationmodule 發現票證已過期，則會將它捨棄，並將要求視為匿名。

[![當 slidingExpiration 為 false 時，表單驗證票證的到期圖形表示](forms-authentication-configuration-and-advanced-topics-vb/_static/image2.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image1.png)

**圖 01**：當 slidingExpiration 為 false 時，表單驗證票證到期的圖形表示（[按一下以查看完整大小的影像](forms-authentication-configuration-and-advanced-topics-vb/_static/image3.png)）

[圖 2] 顯示當 slidingExpiration 設定為 true，且 timeout 設定為30時的工作流程。 收到已驗證的要求（具有未過期的票證）時，其到期日會更新為未來的超時分鐘數。

[當 slidingExpiration 為 true 時，![表單驗證票證的圖形標記法](forms-authentication-configuration-and-advanced-topics-vb/_static/image5.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image4.png)

**圖 02**：當 slidingExpiration 為 true 時，表單驗證票證的圖形表示（[按一下以查看完整大小的影像](forms-authentication-configuration-and-advanced-topics-vb/_static/image6.png)）

使用以 cookie 為基礎的驗證票證（預設值）時，此討論會變得更加困惑，因為 cookie 也可以指定自己的 expiries。 Cookie 的到期（或缺少）會指示瀏覽器何時應終結 cookie。 如果 cookie 缺少到期日，則會在瀏覽器關閉時將其損毀。 不過，如果有到期日，cookie 就會一直儲存在使用者的電腦上，直到到期指定的日期和時間為止。 當瀏覽器終結 cookie 時，它就不會再傳送到 web 伺服器。 因此，cookie 的銷毀類似于使用者登出網站。

> [!NOTE]
> 當然，使用者可能會主動移除儲存在電腦上的任何 cookie。 在 Internet Explorer 7 中，您可以移至 [工具]、[選項]，然後按一下 [流覽歷程記錄] 區段中的 [刪除] 按鈕。 從該處按一下 [刪除 cookie] 按鈕。

表單驗證系統會根據傳入*persistCookie*參數的值，建立以會話為基礎或以過期為基礎的 cookie。 回想一下，FormsAuthentication 類別的 GetAuthCookie、SetAuthCookie 和 RedirectFromLoginPage 方法會採用兩個輸入參數： *username*和*persistCookie*。 我們在前一個教學課程中建立的登入頁面包含 [記住我] 核取方塊，決定是否已建立持續性 cookie。 持續性 cookie 是以過期為基礎;非持續性 cookie 是以會話為基礎。

已討論的 timeout 和 slidingExpiration 概念，對會話和到期的 cookie 都套用相同的。 執行中只有一個次要差異：當使用以過期為基礎的 cookie，並將 slidingTimeout 設定為 true 時，只有在經過超過一半的指定時間時，才會更新 cookie 的到期日。

讓我們更新我們的網站驗證票證超時原則，讓票證在一小時後（60分鐘）就會使用滑動到期時間。 若要對此變更產生影響，請更新 Web.config 檔案，將 &lt;forms&gt; 元素新增至 &lt;authentication&gt; 專案，並加上下列標記：

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample2.xml)]

### <a name="using-an-login-page-url-other-than-loginaspx"></a>使用 Login 以外的登入頁面 URL

由於又稱為 formsauthenticationmodule 會自動將未經授權的使用者重新導向至登入頁面，因此它必須知道登入頁面的 URL。 這個 URL 是由 &lt;表單&gt; 專案中的 loginUrl 屬性所指定，而且預設為 login .aspx。 如果您要移植現有的網站，您可能已經有一個具有不同 URL 的登入頁面，其中一個已由搜尋引擎加上書簽並編制索引。 您可以改為修改 loginUrl 屬性，以指向您的登入頁面，而不是將現有的登入頁面重新命名為 [登入 .aspx] 和 [中斷連結] 和 [使用者書簽]。

例如，如果您的登入頁面命名為 login .aspx，而且位於使用者目錄中，則您可以將 loginUrl 設定值指向 ~/Users/SignIn.aspx，如下所示：

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample3.xml)]

因為我們目前的應用程式已經有名為 Login 的登入頁面，所以不需要在 &lt;forms&gt; 元素中指定自訂值。

## <a name="step-2-using-cookieless-forms-authentication-tickets"></a>步驟2：使用無 Cookie 的表單驗證票證

根據預設，表單驗證系統會決定是否要將其驗證票證儲存在 cookie 集合中，或根據造訪網站的使用者代理程式將其內嵌在 URL 中。 所有主流桌面瀏覽器（例如 Internet Explorer、Firefox、Opera 和 Safari）都支援 cookie，但並非所有行動裝置都有。

表單驗證系統所使用的 cookie 原則取決於 &lt;forms&gt; 元素中的無 cookie 設定，可以指派四個值的其中一個：

- UseCookies-指定一律會使用以 cookie 為基礎的驗證票證。
- UseUri-指出永遠不會使用以 cookie 為基礎的驗證票證。
- 自動偵測-如果裝置設定檔不支援 cookie，則不會使用以 cookie 為基礎的驗證票證;如果裝置設定檔支援 cookie，則會使用探查機制來判斷是否已啟用 cookie。
- UseDeviceProfile-預設值;只有在裝置設定檔支援 cookie 時，才會使用 cookie 型驗證票證。 未使用任何探查機制。

[自動偵測] 和 [UseDeviceProfile] 設定會依賴*裝置設定檔*，查明是否要使用 cookie 型或無 cookie 驗證票證。 ASP.NET 會維護各種裝置及其功能的資料庫，例如它們是否支援 cookie、支援的 JavaScript 版本等等。 每次裝置從 web 伺服器要求網頁時，它會沿著用來識別裝置類型的*使用者代理程式*HTTP 標頭傳送該網頁。 ASP.NET 會自動將提供的使用者代理字串與其資料庫中指定的對應設定檔進行比對。

> [!NOTE]
> 此裝置功能的資料庫會儲存在一些符合[瀏覽器定義檔案架構](https://msdn.microsoft.com/library/ms228122.aspx)的 XML 檔案中。 預設的裝置設定檔位於%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG\Browsers。 您也可以將自訂檔案新增至應用程式的 [瀏覽器] 資料夾\_。 如需詳細資訊，請參閱[如何：在 ASP.NET Web Pages 中偵測瀏覽器類型](https://msdn.microsoft.com/library/3yekbd5b.aspx)。

由於預設設定為 UseDeviceProfile，因此當裝置瀏覽器的設定檔不支援 cookie 時，將會使用無 cookie 的表單驗證票證。

### <a name="encoding-the-authentication-ticket-in-the-url"></a>將 URL 中的驗證票證編碼

Cookie 是一個自然媒體，可將每個要求中的資訊納入特定網站，這也是為什麼當流覽裝置支援時，預設的表單驗證設定會使用 cookie。 如果不支援 cookie，則必須使用替代方法，將來自用戶端的驗證票證傳遞至伺服器。 在無 cookie 環境中使用的常見因應措施是將 URL 中的 cookie 資料編碼。

查看這類資訊如何內嵌在 URL 中的最佳方式，就是強制網站使用無 cookie 的驗證票證。 這可以藉由將無 cookie 設定設定為 UseUri 來完成：

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample4.xml)]

完成此變更之後，請透過瀏覽器造訪網站。 以匿名使用者的身分造訪時，Url 看起來就像以前一樣。 例如，造訪 default.aspx 網頁時，我的瀏覽器網址列會顯示下列 URL：

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/default.aspx`

不過，登入時，表單驗證票證會內嵌至 URL。 例如，流覽登入頁面並以 Sam 身分登入之後，我會回到 default.aspx 頁面，但這次的 URL 是：

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/(F(jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-FyMaLXJfow\_Vd9GZkB2Cv-rfezq0gKadKX0YPZCkA2))/default.aspx`

表單驗證票證已內嵌在 URL 中。 字串（F （jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-FyMaLXJfow\_Vd9GZkB2Cv-rfezq0gKadKX0YPZCkA2）代表十六進位編碼的驗證票證資訊，而且是通常儲存在 cookie 內的相同資料。

為了讓無 cookie 驗證票證能夠正常執行，系統必須將頁面上的所有 Url 編碼，以包含驗證票證資料，否則當使用者按一下連結時，將會遺失驗證票證。 幸好，此內嵌邏輯會自動執行。 若要示範這種功能，請開啟 default.aspx 頁面並加入 HyperLink 控制項，分別將其 Text 和 NavigateUrl 屬性設定為 Test Link 和 SomePage。 我們的專案中真的沒有一個名為 SomePage 的頁面。

將變更儲存至 default.aspx，然後透過瀏覽器造訪。 登入網站，以將表單驗證票證內嵌在 URL 中。 接下來，從 default.aspx 中，按一下 [測試連結] 連結。 發生了什麼事？ 如果沒有名為 SomePage 的頁面存在，則會發生404錯誤，但這裡並不重要。 相反地，請將焦點放在瀏覽器的網址列上。 請注意，其中包含 URL 中的表單驗證票證！

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/(F(jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-FyMaLXJfow\_Vd9GZkB2Cv-rfezq0gKadKX0YPZCkA2))/SomePage.aspx`

連結中的 URL SomePage 已自動轉換成包含驗證票證的 URL-我們不需要撰寫舔的程式碼！ 表單驗證票證會自動內嵌至任何不是以 HTTP://或/開頭之超連結的 URL 中。 超連結是否會出現在回應的呼叫中，並不重要。重新導向、超連結控制項或錨點 HTML 專案中（亦即，&lt;href = "..."&gt;...&lt;/a&gt;）。 只要 URL 不像 http://www.someserver.com/SomePage.aspx 或/SomePage.aspx，就會為我們內嵌表單驗證票證。

> [!NOTE]
> 無 cookie 的表單驗證票證會與以 cookie 為基礎的驗證票證遵循相同的超時原則。 不過，無 cookie 驗證票證較容易重新執行攻擊，因為驗證票證直接內嵌在 URL 中。 想像一下造訪網站、登入，然後以電子郵件將 URL 貼到同事的使用者。 如果同事在達到到期前按一下該連結，則會以傳送電子郵件的使用者身分登入！

## <a name="step-3-securing-the-authentication-ticket"></a>步驟3：保護驗證票證

表單驗證票證會透過網路傳輸，不論是在 cookie 中，或直接內嵌在 URL 內。 除了身分識別資訊之外，驗證票證也可以包含使用者資料（如我們在步驟4中所見）。 因此，票證的資料必須從窺探的角度加密，而且更重要的是，表單驗證系統可以保證票證不會遭到篡改。

為確保票證資料的隱私權，表單驗證系統可以加密票證資料。 無法加密票證資料會以純文字形式透過網路傳送可能的機密資訊。

為了保證票證的真實性，表單驗證系統必須*驗證*票證。 驗證是確保特定資料片段尚未修改的動作，並可透過 *[訊息驗證碼（MAC）](http://en.wikipedia.org/wiki/Message_authentication_code)* 來完成。 簡言之，MAC 是一小部分的資訊，可識別需要驗證的資料（在此案例中為票證）。 如果已修改 MAC 所代表的資料，則 MAC 和資料將不會相符。 此外，駭客也很難進行修改資料的運算，並產生自己的 MAC 來對應修改過的資料。

建立（或修改）票證時，表單驗證系統會建立 MAC，並將它附加至票證的資料。 當後續的要求抵達時，表單驗證系統會比較 MAC 和票證資料，以驗證票證資料的真實性。 [圖 3] 以圖形方式說明此工作流程。

[![透過 MAC 確保票證的真實性](forms-authentication-configuration-and-advanced-topics-vb/_static/image8.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image7.png)

**圖 03**：透過 MAC 確保票證的真實性（[按一下以觀看完整大小的影像](forms-authentication-configuration-and-advanced-topics-vb/_static/image9.png)）

套用至驗證票證的安全性措施取決於 &lt;forms&gt; 元素中的保護設定。 保護設定可能會指派給下列三個值的其中一個：

- All-此票證會經過加密和數位簽署（預設值）。
- 套用加密-只會套用加密-不會產生 MAC。
- 無-不會加密票證，也不會進行數位簽署。
- 驗證-產生 MAC，但票證資料是透過網路以純文字傳送。

Microsoft 強烈建議使用 [全部] 設定。

### <a name="setting-the-validation-and-decryption-keys"></a>設定驗證和解密金鑰

表單驗證系統用來加密和驗證驗證票證的加密和雜湊演算法，可以透過 Web.config 中的[&lt;machineKey&gt; 元素](https://msdn.microsoft.com/library/w8h3skw9.aspx)進行自訂。[表 2] 概述 &lt;machineKey&gt; 元素的屬性及其可能的值。

| **屬性** | **說明** |
| --- | --- |
| 解密 | 表示用於加密的演算法。 這個屬性可以有下列四個值的其中一個：-Auto-default。根據 Decryptionkey 機屬性的長度來決定演算法。 -AES-使用[進階加密標準（AES）](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard)演算法。 -DES-使用[資料加密標準（DES）](http://en.wikipedia.org/wiki/Data_Encryption_Standard)此演算法視為運算弱式，不應使用。 -3DES-使用[三](http://en.wikipedia.org/wiki/Triple_DES)重 des 演算法，其運作方式為三次。 |
| Decryptionkey 機 | 加密演算法所使用的秘密金鑰。 這個值必須是適當長度的十六進位字串（根據解密中的值）、自動產生，或以 IsolateApps 附加的任何值。 新增 IsolateApps 會指示 ASP.NET 對每個應用程式使用唯一的值。 預設值為 [自動產生]、[IsolateApps]。 |
| 驗證 | 表示用於驗證的演算法。 此屬性可以有下列四個值的其中一個：-AES-使用進階加密標準（AES）演算法。 -MD5-使用[訊息摘要5（MD5）](http://en.wikipedia.org/wiki/MD5)演算法。 -SHA1-使用[SHA1](http://en.wikipedia.org/wiki/Sha1)演算法（預設值）。 -3DES-使用三重 DES 演算法。 |
| validationKey | 驗證演算法所使用的秘密金鑰。 這個值必須是適當長度的十六進位字串（根據驗證中的值）、自動產生，或以 IsolateApps 附加的任何值。 新增 IsolateApps 會指示 ASP.NET 對每個應用程式使用唯一的值。 預設值為 [自動產生]、[IsolateApps]。 |

**表 2**： &lt;MachineKey&gt; 元素屬性

這些加密和驗證選項的完整討論，以及各種演算法的優缺點，已超出本教學課程的範圍。 如需深入瞭解這些問題，包括要使用的加密和驗證演算法、要使用的金鑰長度，以及如何產生這些金鑰，請參閱*專業 ASP.NET 2.0 安全性、成員資格和角色管理*。

根據預設，用於加密和驗證的金鑰會針對每個應用程式自動產生，而這些金鑰會儲存在本地安全機構（LSA）中。 簡單地說，預設設定會保證 web 伺服器上的唯一索引鍵，以及每個應用程式的基礎。 因此，在下列兩種情況下，此預設行為將無法運作：

- **Web**伺服陣列-在[web](http://en.wikipedia.org/wiki/Web_farm)伺服陣列案例中，單一 web 應用程式會裝載于多部 web 伺服器上，以因應擴充性和冗余的目的。 每個連入要求都會分派到伺服器陣列中的伺服器，這表示在使用者會話的存留期內，可能會使用不同的伺服器來處理其各種要求。 因此，每部伺服器都必須使用相同的加密和驗證金鑰，如此一來，在一部伺服器上建立、加密及驗證的表單驗證票證，才能在伺服陣列中的不同伺服器上進行解密和驗證。
- **跨應用程式票證共用**-單一 web 伺服器可以裝載多個 ASP.NET 應用程式。 如果您需要這些不同的應用程式共用單一表單驗證票證，其加密和驗證金鑰必須相符。

在 web 伺服陣列中工作或跨相同伺服器上的應用程式共用驗證票證時，您必須在受影響的應用程式中設定 &lt;machineKey&gt; 元素，使其 Decryptionkey 機和 validationKey 值相符。

雖然上述案例都不適用於我們的範例應用程式，但仍可指定明確的 Decryptionkey 機和 validationKey 值，並定義要使用的演算法。 將 &lt;machineKey&gt; 設定新增至 web.config 檔案：

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample5.xml)]

如需詳細資訊，請參閱[如何：在 ASP.NET 2.0 中設定 MachineKey](https://msdn.microsoft.com/library/ms998288.aspx)。

> [!NOTE]
> Decryptionkey 機和 validationKey 值取自[Steve Gibson](http://www.grc.com/stevegibson.htm)的 [[最佳密碼] 網頁](https://www.grc.com/passwords.htm)，這會在每一頁上產生64的隨機十六進位字元。 若要降低這些金鑰進入生產應用程式的可能性，建議您從 [最佳密碼] 頁面，將上述金鑰取代為隨機產生的金鑰。

## <a name="step-4-storing-additional-user-data-in-the-ticket"></a>步驟4：在票證中儲存額外的使用者資料

許多 web 應用程式會顯示目前登入之使用者的頁面顯示資訊，或以此為基礎。 例如，網頁可能會顯示使用者的名稱，以及她上次登入每個頁面右上角的日期。 表單驗證票證會儲存目前登入的使用者名稱，但當需要任何其他資訊時，頁面必須移至使用者存放區（通常是資料庫），以查閱未儲存在驗證票證中的資訊。

有了一些程式碼，我們就可以在表單驗證票證中儲存額外的使用者資訊。 這類資料可透過[FormsAuthenticationTicket 類別](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.aspx)的[UserData 屬性](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.userdata.aspx)來表示。 這很適合用來放入通常需要的使用者相關的少量資訊。 [UserData] 屬性中指定的值會納入為驗證票證 cookie 的一部分，如同其他票證欄位，會根據表單驗證系統的設定來加密和驗證。 根據預設，UserData 是空字串。

為了將使用者資料儲存在驗證票證中，我們需要在登入頁面中撰寫一些程式碼來抓取使用者特定資訊，並將它儲存在票證中。 由於 UserData 是 String 類型的屬性，因此儲存在其中的資料必須正確地序列化為字串。 例如，假設我們的使用者存放區包含每位使用者的出生日期和雇主的名稱，而我們想要在驗證票證中儲存這兩個屬性值。 我們可以將使用者的生日字串與管道（|）串連，後面接著雇主名稱，藉此將這些值序列化成字串。 如果使用者是在1974年8月15日（適用于 Northwind 商貿），我們會指派字串： 1974-08-15 | 中的 UserData 屬性。Northwind 商貿。

只要我們需要存取儲存在票證中的資料，我們就可以抓取目前要求的 FormsAuthenticationTicket，並還原序列化 UserData 屬性來達到此目的。 在「出生日期」和「雇主名稱」範例的案例中，我們會根據分隔符號（|）將 UserData 字串分割成兩個子字串。

[![額外的使用者資訊可儲存在驗證票證中](forms-authentication-configuration-and-advanced-topics-vb/_static/image11.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image10.png)

**圖 04**：其他使用者資訊可以儲存在驗證票證中（[按一下以觀看完整大小的影像](forms-authentication-configuration-and-advanced-topics-vb/_static/image12.png)）

### <a name="writing-information-to-userdata"></a>將資訊寫入到 UserData

可惜的是，將使用者特有的資訊新增至表單驗證票證，並不像預期般簡單。 FormsAuthenticationTicket 類別的 UserData 屬性是唯讀的，而且只能透過 FormsAuthenticationTicket 類別的函式來指定。 在此函式中指定 UserData 屬性時，我們也需要提供票證的其他值：使用者名稱、問題日期、到期日等等。 當我們在先前的教學課程中建立登入頁面時，FormsAuthentication 類別會為我們處理。 將 UserData 新增至 FormsAuthenticationTicket 時，我們必須撰寫程式碼來複寫 FormsAuthentication 類別已提供的許多功能。

讓我們來探索使用 UserData 的必要程式碼，方法是更新 Login .aspx 頁面，將使用者的其他資訊記錄到驗證票證。 假設我們的使用者存放區包含使用者適用之公司的相關資訊及其職稱，而我們想要在驗證票證中取得這項資訊。 更新 Login .aspx 頁面的 LoginButton Click 事件處理常式，以便程式碼看起來如下所示：

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample6.vb)]

讓我們一次逐步執行此程式碼一行。 方法一開始會定義四個字串陣列：使用者、密碼、公司名稱和 titleAtCompany。 這些陣列包含系統中使用者帳戶的使用者名稱、密碼、公司名稱和標題，其中有三個： Scott、Jisun 和 Sam。 在實際的應用程式中，會從使用者存放區中查詢這些值，而不是在頁面的原始程式碼中進行硬式編碼。

在上一個教學課程中，如果提供的認證有效，我們只會呼叫 FormsAuthentication. RedirectFromLoginPage （UserName. Text，RememberMe），這會執行下列步驟：

1. 已建立表單驗證票證
2. 已將票證寫入適當的存放區。 若為以 cookie 為基礎的驗證票證，則會使用瀏覽器的 cookie 集合;若為無 cookie 驗證票證，票證資料會序列化為 URL
3. 將使用者重新導向至適當的頁面

這些步驟會在上述程式碼中複寫。 首先，最後要儲存在 UserData 屬性中的字串是藉由結合公司名稱和標題來形成，並將兩個值與一個管道字元（|）分隔。

Dim userDataString As String = String. Concat （公司名稱（i），"|"，titleAtCompany （i））

接下來，會叫用 FormsAuthentication. GetAuthCookie 方法，它會建立驗證票證、根據設定進行加密和驗證，並將其放在 HttpCookie 物件中。

Dim authCookie As HttpCookie = FormsAuthentication. GetAuthCookie （UserName. Text，RememberMe. Checked）

為了使用內嵌在 cookie 內的 FormAuthenticationTicket，我們需要呼叫 FormAuthentication 類別的[解密方法](https://msdn.microsoft.com/library/system.web.security.formsauthentication.decrypt.aspx)，並傳入 cookie 值。

Dim ticket As FormsAuthenticationTicket = FormsAuthentication （authCookie 值）

然後，我們會根據現有的 FormsAuthenticationTicket 值，建立*新*的 FormsAuthenticationTicket 實例。 不過，這個新的票證包含使用者特定的資訊（userDataString）。

Dim newTicket As FormsAuthenticationTicket = New FormsAuthenticationTicket （ticket）。版本、票證。名稱、票證。IssueDate，票證。到期日，票證。IsPersistent、userDataString）

然後，我們會藉由呼叫[encrypt 方法](https://msdn.microsoft.com/library/system.web.security.formsauthentication.encrypt.aspx)來加密（並驗證）新的 FormsAuthenticationTicket 實例，並將這個經過加密（並經過驗證）的資料放回 authCookie 中。

authCookie。 Value = FormsAuthentication （newTicket）

最後，authCookie 會新增至回應。 Cookie 集合和 GetRedirectUrl 方法會被呼叫，以決定要傳送給使用者的適當頁面。

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample7.vb)]

所有此程式碼都是必要的，因為 UserData 屬性是唯讀的，而 FormsAuthentication 類別並未提供任何方法來指定其 GetAuthCookie、SetAuthCookie 或 RedirectFromLoginPage 方法中的 UserData 資訊。

> [!NOTE]
> 我們剛才檢查的程式碼會在以 cookie 為基礎的驗證票證中儲存使用者特定資訊。 負責將表單驗證票證序列化至 URL 的類別，是 .NET Framework 的內部。 短時間內，您無法將使用者資料儲存在無 cookie 的表單驗證票證中。

### <a name="accessing-the-userdata-information"></a>存取 UserData 資訊

此時，每個使用者的公司名稱和標題都會在登入時儲存在表單驗證票證的 UserData 屬性中。 此資訊可以從任何頁面上的驗證票證存取，而不需要使用者存放區。 為了說明如何從 UserData 屬性中抓取此資訊，讓我們更新 default.aspx，使其歡迎訊息不僅包含使用者的名稱，也包括其適用的公司及其職稱。

目前，default.aspx 包含具有名為 WelcomeBackMessage 之標籤控制項的 AuthenticatedMessagePanel 面板。 只有已驗證的使用者才會看到此面板。 更新 default.aspx 頁面中的程式碼\_載入事件處理常式，使其看起來如下所示：

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample8.vb)]

如果 IsAuthenticated 為 True，則 WelcomeBackMessage 的 Text 屬性會先設定為 [歡迎使用]、[使用者*名稱*]。 然後，User. Identity 屬性會轉換成 FormsIdentity 物件，讓我們可以存取基礎 FormsAuthenticationTicket。 一旦有了 FormsAuthenticationTicket，我們就會將 UserData 屬性還原序列化為公司名稱和標題。 這是藉由在管道字元上分割字串來完成。 公司名稱和標題會顯示在 [WelcomeBackMessage] 標籤中。

[圖 5] 顯示此顯示動作的螢幕擷取畫面。 以 Scott 的身分登入，會顯示包含 Scott 公司和標題的歡迎後消息。

[顯示目前登入之使用者的公司和標題 ![](forms-authentication-configuration-and-advanced-topics-vb/_static/image14.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image13.png)

**圖 05**：顯示目前登入的使用者公司和標題（[按一下以觀看完整大小的影像](forms-authentication-configuration-and-advanced-topics-vb/_static/image15.png)）

> [!NOTE]
> 驗證票證的 UserData 屬性作為使用者存放區的快取。 就像任何快取一樣，修改基礎資料時需要更新它。 例如，如果有可讓使用者更新其設定檔的網頁，則必須重新整理 UserData 屬性中快取的欄位，以反映使用者所做的變更。

## <a name="step-5-using-a-custom-principal"></a>步驟5：使用自訂主體

在每個傳入要求中，又稱為 formsauthenticationmodule 會嘗試驗證使用者。 如果未過期的驗證票證存在，又稱為 formsauthenticationmodule 會將 HttpCoNtext 使用者屬性指派給新的 GenericPrincipal 物件。 這個 GenericPrincipal 物件具有 FormsIdentity 類型的身分識別，其中包含表單驗證票證的參考。 GenericPrincipal 類別包含實 IPrincipal 的類別所需的最小功能，它只具有 Identity 屬性和 IsInRole 方法。

主體物件有兩個責任：表示使用者所屬的角色，以及提供身分識別資訊。 這會分別透過 IPrincipal 介面的*IsInRole （「* 人」）方法和識別屬性來完成。 GenericPrincipal 類別可讓您透過其函式指定角色名稱的字串陣列;其*IsInRole （人員*）方法只會檢查字串陣列*中是否有傳入的用項*。 當又稱為 formsauthenticationmodule 建立 GenericPrincipal 時，它會將空字串陣列傳遞至 GenericPrincipal 的函式。 因此，任何對 IsInRole 的呼叫一律會傳回 False。

GenericPrincipal 類別符合大部分以表單為基礎的驗證案例的需求，其中不使用角色。 對於預設角色處理不足的情況，或當您需要將自訂 IIdentity 物件與使用者建立關聯時，您可以在驗證工作流程期間建立自訂 IPrincipal 物件，並將它指派給 HttpCoNtext 使用者屬性。

> [!NOTE]
> 如我們在未來的教學課程中所見，ASP。NET 的 Roles framework 已啟用它會建立[RolePrincipal](https://msdn.microsoft.com/library/system.web.security.roleprincipal.aspx)類型的自訂主體物件，並覆寫表單驗證建立的 GenericPrincipal 物件。 它會執行這項工作，以自訂主體的 IsInRole 方法，以與角色架構的 API 互動。

因為我們還不在意角色，所以在這個位置建立自訂主體的唯一理由，就是將自訂 IIdentity 物件與主體建立關聯。 在步驟4中，我們探討了在驗證票證的 UserData 屬性中儲存額外的使用者資訊，特別是使用者的公司名稱和標題。 不過，只有透過驗證票證才可存取 UserData 資訊，而只是以序列化字串的形式，這表示每當我們想要查看儲存在票證中的使用者資訊時，我們需要剖析 UserData 屬性。

我們可以藉由建立一個可執行 IIdentity 的類別，並包含 [公司名稱] 和 [標題] 屬性來改善開發人員體驗。 如此一來，開發人員就可以直接透過 [公司名稱] 和 [標題] 屬性存取目前登入的使用者公司名稱和標題，而不需要知道如何剖析 UserData 屬性。

### <a name="creating-the-custom-identity-and-principal-classes"></a>建立自訂身分識別和主體類別

在本教學課程中，我們將在應用程式中建立自訂主體和身分識別物件\_Code 資料夾。 首先，將應用程式\_Code 資料夾新增至您的專案-在方案總管中的專案名稱上按一下滑鼠右鍵，選取 [新增 ASP.NET 資料夾] 選項，然後選擇 [應用程式\_代碼]。 應用程式\_Code 資料夾是特殊的 ASP.NET 資料夾，其中包含網站特定的類別檔案。

> [!NOTE]
> 只有在透過網站專案模型管理您的專案時，才應該使用 App\_程式碼資料夾。 如果您使用[Web 應用程式專案模型](https://msdn.microsoft.com/asp.net/Aa336618.aspx)，請建立標準資料夾，並將類別加入至其中。 例如，您可以新增名為 [類別] 的新資料夾，並將您的程式碼放在該處。

接下來，將兩個新的類別檔案新增至應用程式\_Code 資料夾，一個名為 CustomIdentity，另一個名為 CustomPrincipal。

[![將 CustomIdentity 和 CustomPrincipal 類別新增至您的專案](forms-authentication-configuration-and-advanced-topics-vb/_static/image17.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image16.png)

**圖 06**：將 CustomIdentity 和 CustomPrincipal 類別新增至您的專案（[按一下以查看完整大小的影像](forms-authentication-configuration-and-advanced-topics-vb/_static/image18.png)）

CustomIdentity 類別負責執行 IIdentity 介面，以定義 AuthenticationType、IsAuthenticated 和 Name 屬性。 除了這些必要的屬性之外，我們也想要公開基礎表單驗證票證，以及使用者的公司名稱和標題的屬性。 在 CustomIdentity 類別中輸入下列程式碼。

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample9.vb)]

請注意，類別包含 FormsAuthenticationTicket 成員變數（\_票證），而且必須透過此函式提供此票證資訊。 此票證資料是用來傳回身分識別的名稱。其 UserData 屬性會經過剖析，以傳回 [公司名稱] 和 [標題] 屬性的值。

接下來，建立 CustomPrincipal 類別。 由於我們並不在意角色，因此 CustomPrincipal 類別的函式只接受 CustomIdentity 物件;其 IsInRole 方法一律會傳回 False。

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample10.vb)]

### <a name="assigning-a-customprincipal-object-to-the-incoming-requests-security-context"></a>將 CustomPrincipal 物件指派給連入要求的安全性內容

我們現在有一個類別，它會擴充預設 IIdentity 規格以包含 [公司名稱] 和 [標題] 屬性，以及使用自訂身分識別的自訂主體類別。 我們已準備好逐步執行 ASP.NET 管線，並將自訂主體物件指派給連入要求的安全性內容。

ASP.NET 管線會接受傳入要求，並透過幾個步驟進行處理。 在每個步驟中，會引發特定事件，讓開發人員可以利用 ASP.NET 管線，並在其生命週期中的特定時間點修改要求。 例如，又稱為 formsauthenticationmodule 會等候 ASP.NET 引發[AuthenticateRequest 事件](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)，此時它會檢查驗證票證的連入要求。 如果找到驗證票證，則會建立 GenericPrincipal 物件，並將其指派給 HttpCoNtext 使用者屬性。

在 AuthenticateRequest 事件之後，ASP.NET 管線會引發[PostAuthenticateRequest 事件](https://msdn.microsoft.com/library/system.web.httpapplication.postauthenticaterequest.aspx)，我們可以在這裡將又稱為 formsauthenticationmodule 所建立的 GenericPrincipal 物件取代為 CustomPrincipal 物件的實例。 [圖 7] 說明此工作流程。

[![GenericPrincipal 由 PostAuthenticationRequest 事件中的 CustomPrincipal 所取代](forms-authentication-configuration-and-advanced-topics-vb/_static/image20.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image19.png)

**圖 07**： PostAuthenticationRequest 事件中的 CustomPrincipal 會取代 GenericPrincipal （[按一下以查看完整大小的影像](forms-authentication-configuration-and-advanced-topics-vb/_static/image21.png)）

為了要執行程式碼以回應 ASP.NET 管線事件，我們可以在 global.asax 中建立適當的事件處理常式，或建立我們自己的 HTTP 模組。 在本教學課程中，我們將在 global.asax 中建立事件處理常式。 首先，將 global.asax 加入您的網站。 在方案總管中，以滑鼠右鍵按一下專案名稱，並加入名為 global 的全域應用程式類別的專案。

[![將 global.asax 檔案新增至您的網站](forms-authentication-configuration-and-advanced-topics-vb/_static/image23.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image22.png)

**圖 08**：將 Global.asax 檔案新增至您的網站（[按一下以觀看完整大小的影像](forms-authentication-configuration-and-advanced-topics-vb/_static/image24.png)）

預設的 global.asax 範本包含數個 ASP.NET 管線事件的事件處理常式，包括開始、結束和[錯誤事件](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx)等等。 請隨意移除這些事件處理常式，因為此應用程式不需要它們。 我們感興趣的事件是 PostAuthenticateRequest。 更新您的 global.asax 檔案，讓其標記看起來如下所示：

[!code-aspx[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample11.aspx)]

每當 ASP.NET 執行時間引發 PostAuthenticateRequest 事件時，就會執行應用程式\_OnPostAuthenticateRequest 方法，這會在每個傳入的頁面要求上發生一次。 事件處理常式一開始會先檢查使用者是否經過驗證，並通過表單驗證驗證。 若是如此，就會建立新的 CustomIdentity 物件，並在其函式中傳遞目前要求的驗證票證。 之後，就會建立 CustomPrincipal 物件，並在其函式中傳遞剛建立的 CustomIdentity 物件。 最後，會將目前要求的安全性內容指派給新建立的 CustomPrincipal 物件。

請注意，最後一個步驟是將 CustomPrincipal 物件與要求的安全性內容產生關聯-將主體指派給兩個屬性： HttpCoNtext. User 和 Thread.currentprincipal。 這兩個指派是必要的，因為在 ASP.NET 中處理安全性內容的方式。 .NET Framework 會將安全性內容與每個執行中的執行緒產生關聯;這種資訊是透過[Thread 物件](https://msdn.microsoft.com/library/system.threading.thread.aspx)的[thread.currentprincipal 屬性](https://msdn.microsoft.com/library/system.threading.thread.currentcontext.aspx)，以 IPrincipal 物件的形式提供。 令人困惑的是，ASP.NET 有自己的安全性內容資訊（HttpCoNtext）。

在某些情況下，會在判斷安全性內容時檢查 Thread.currentprincipal 屬性。在其他情況下，則會使用 HttpCoNtext。 例如，.NET 中有一些安全性功能，可讓開發人員以宣告方式指出哪些使用者或角色可以具現化類別，或叫用特定方法（請參閱[使用 PrincipalPermissionAttributes 將授權規則新增至商務和資料層](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)）。 在幕後，這些宣告式技術會透過 Thread.currentprincipal 屬性來判斷安全性內容。

在其他案例中，會使用 HttpCoNtext. User 屬性。 例如，在上一個教學課程中，我們使用這個屬性來顯示目前登入的使用者名稱。 很明顯地，Thread.currentprincipal 和 HttpCoNtext 等使用者屬性中的安全性內容資訊必須相符。

ASP.NET 執行時間會自動為我們同步處理這些屬性值。 不過，此同步處理會在 AuthenticateRequest 事件之後，但在 PostAuthenticateRequest 事件*之前*發生。 因此，在 PostAuthenticateRequest 事件中新增自訂主體時，我們必須確定手動指派 Thread.currentprincipal 或 Thread.currentprincipal 和 HttpCoNtext。使用者將不會同步。如需此問題的詳細討論，請參閱[CoNtext. thread.currentprincipal。](http://leastprivilege.com/2005/11/23/context-user-vs-thread-currentprincipal/)

### <a name="accessing-the-companyname-and-title-properties"></a>存取 [公司名稱] 和 [標題] 屬性

每當要求抵達並分派至 ASP.NET 引擎時，就會引發 global.asax 中的應用程式\_OnPostAuthenticateRequest 事件處理常式。 如果要求已由又稱為 formsauthenticationmodule 成功驗證，則事件處理常式會根據表單驗證票證，建立具有 CustomIdentity 物件的新 CustomPrincipal 物件。 有了這個邏輯，存取目前登入之使用者的公司名稱和標題的相關資訊相當簡單。

回到 default.aspx 的頁面\_載入事件處理常式，在步驟4中，我們撰寫了程式碼來抓取表單驗證票證，並剖析 UserData 屬性以顯示使用者的公司名稱和標題。 現在使用 CustomPrincipal 和 CustomIdentity 物件，就不需要剖析票證的 UserData 屬性的值。 相反地，只要取得 CustomIdentity 物件的參考，並使用其 [公司名稱] 和 [標題] 屬性即可：

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample12.vb)]

## <a name="summary"></a>總結

在本教學課程中，我們已檢查如何透過 Web.config 自訂表單驗證系統的設定。我們探討了如何處理驗證票證的到期日，以及如何使用加密和驗證保護措施來保護票證，使其無法進行檢查和修改。 最後，我們討論過使用驗證票證的 UserData 屬性，將其他使用者資訊儲存在票證本身，以及如何使用自訂主體和身分識別物件，以更方便開發人員的方式來公開這項資訊。

本教學課程將說明如何在 ASP.NET 中檢查表單驗證。 下一個教學課程會開始我們的成員資格架構旅程。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [剖析表單驗證](http://aspnet.4guysfromrolla.com/articles/072005-1.aspx)
- [說明： ASP.NET 2.0 中的表單驗證](https://msdn.microsoft.com/library/aa480476.aspx)
- [如何：保護 ASP.NET 2.0 中的表單驗證](https://msdn.microsoft.com/library/ms998310.aspx)
- [Professional ASP.NET 2.0 安全性、成員資格和角色管理](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html)（ISBN：978-0-7645-9698-8）
- [保護登入控制項](https://msdn.microsoft.com/library/ms178346.aspx)
- [&lt;authentication&gt; 元素](https://msdn.microsoft.com/library/532aee0e.aspx)
- [&lt;驗證的 &lt;表單&gt; 元素&gt;](https://msdn.microsoft.com/library/1d3t3c61.aspx)
- [&lt;machineKey&gt; 元素](https://msdn.microsoft.com/library/w8h3skw9.aspx)
- [瞭解表單驗證票證和 Cookie](https://support.microsoft.com/kb/910443)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>本教學課程中所含主題的影片訓練

- [如何變更表單驗證屬性](../../../videos/authentication/how-to-change-the-forms-authentication-properties.md)
- [如何在 ASP.NET 應用程式中設定並使用無 Cookie 驗證](../../../videos/authentication/how-to-setup-and-use-cookie-less-authentication-in-an-aspnet-application.md)
- [ASP 表單登入重新配置](../../../videos/authentication/asp-forms-login-relocation.md)
- [表單登入自訂金鑰組態](../../../videos/authentication/forms-login-custom-key-configuration.md)
- [將自訂資料新增至驗證方法](../../../videos/authentication/add-custom-data-to-the-authentication-method.md)
- [使用自訂的主體物件](../../../videos/authentication/use-custom-principal-objects.md)

### <a name="about-the-author"></a>關於作者

Scott Mitchell，自1998起，有多個 ASP/ASP. NET 書籍和創辦人的4GuysFromRolla.com。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是 *[在24小時內讓自己的 ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 。 Scott 可以在[mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)或透過他在[http://ScottOnWriting.NET](http://scottonwriting.net/)的 blog。

### <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Alicja Maziarz。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在[mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com)的那一行下拉式。

> [!div class="step-by-step"]
> [上一篇](an-overview-of-forms-authentication-vb.md)
