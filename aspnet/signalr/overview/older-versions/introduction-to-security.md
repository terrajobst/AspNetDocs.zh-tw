---
uid: signalr/overview/older-versions/introduction-to-security
title: SignalR 安全性簡介（SignalR 1.x） |Microsoft Docs
author: bradygaster
description: 說明開發 SignalR 應用程式時，您必須考慮的安全性問題。
ms.author: bradyg
ms.date: 10/17/2013
ms.assetid: 715a4059-d307-4631-abbb-c789c95d6eb4
msc.legacyurl: /signalr/overview/older-versions/introduction-to-security
msc.type: authoredcontent
ms.openlocfilehash: 34172c0a2a15a7ab0d782704d5831ce236f5c989
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536726"
---
# <a name="introduction-to-signalr-security-signalr-1x"></a>SignalR 安全性簡介 (SignalR 1.x)

由一[Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文說明開發 SignalR 應用程式時必須考慮的安全性問題。

## <a name="overview"></a>概觀

本文件包含下列章節：

- [SignalR 安全性概念](#concepts)

    - [驗證與授權](#authentication)
    - [連接權杖](#connectiontoken)
    - [重新連接時重新加入群組](#rejoingroup)
- [SignalR 如何防止跨網站偽造要求](#csrf)
- [SignalR 安全性建議](#recommendations)

    - [安全通訊端層（SSL）通訊協定](#ssl)
    - [請勿使用群組做為安全性機制](#groupsecurity)
    - [安全地處理來自用戶端的輸入](#input)
    - [使用作用中連線協調使用者狀態的變更](#reconcile)
    - [自動產生的 JavaScript proxy 檔案](#autogen)
    - [例外狀況](#exceptions)

<a id="concepts"></a>

## <a name="signalr-security-concepts"></a>SignalR 安全性概念

<a id="authentication"></a>

### <a name="authentication-and-authorization"></a>驗證與授權

SignalR 是設計來整合到應用程式的現有驗證結構中。 它不會提供驗證使用者的任何功能。 相反地，您會在應用程式中以平常的方式驗證使用者，然後在您的 SignalR 程式碼中使用驗證的結果。 例如，您可以使用 ASP.NET 表單驗證來驗證您的使用者，然後在您的中樞內，強制執行哪些使用者或角色獲授權可以呼叫方法。 在您的中樞中，您也可以將驗證資訊（例如使用者名稱或使用者是否屬於角色）傳遞給用戶端。

SignalR 提供[授權](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx)屬性，以指定哪些使用者可以存取中樞或方法。 您會將授權屬性套用至中樞中的中樞或特定方法。 如果沒有授權屬性，中樞上的所有公用方法都可供連線至中樞的用戶端使用。 如需中樞的詳細資訊，請參閱[SignalR 中樞的驗證和授權](../security/hub-authorization.md)。

`Authorize` 屬性僅適用于中樞。 若要在使用 `PersistentConnection` 時強制執行授權規則，您必須覆寫 `AuthorizeRequest` 方法。 如需持續連線的詳細資訊，請參閱[SignalR 持續連線的驗證和授權](../security/persistent-connection-authorization.md)。

<a id="connectiontoken"></a>

### <a name="connection-token"></a>連接權杖

SignalR 藉由驗證寄件者的身分識別，來降低執行惡意命令的風險。 用戶端和伺服器會在每個要求之間傳遞連接權杖，其中包含已驗證使用者的連接識別碼和使用者名稱。 連接識別碼是唯一的識別碼，會在建立新的連接時由伺服器隨機產生，並在連接期間保存。 使用者名稱是由 web 應用程式的驗證機制所提供。 連接權杖會受到加密和數位簽章的保護。

![](introduction-to-security/_static/image2.png)

針對每個要求，伺服器會驗證權杖的內容，以確保要求來自指定的使用者。 使用者名稱必須對應到連接識別碼。藉由驗證連線識別碼和使用者名稱，SignalR 可防止惡意使用者輕鬆地模擬另一位使用者。 如果伺服器無法驗證連線 token，要求就會失敗。

![](introduction-to-security/_static/image4.png)

因為連線識別碼是驗證程式的一部分，所以您不應該向其他使用者顯示某個使用者的連線識別碼，或將此值儲存在用戶端上，例如在 cookie 中。

<a id="rejoingroup"></a>

### <a name="rejoining-groups-when-reconnecting"></a>重新連接時重新加入群組

根據預設，SignalR 應用程式會在中斷連線時，自動將使用者重新指派給適當的群組，例如在連接逾時之前中斷連接並重新建立連線。重新連線時，用戶端會傳遞包含連線識別碼和指派群組的群組 token。 群組權杖會經過數位簽署和加密。 用戶端會在重新連線後保留相同的連接識別碼;因此，從重新連線的用戶端傳遞的連接識別碼必須符合用戶端使用的先前連線識別碼。 此驗證可防止惡意使用者在重新連線時，將要求傳遞至加入未經授權的群組。

不過，請務必注意，群組權杖不會過期。 如果使用者屬於過去的群組，但已從該群組中禁止，該使用者可能可以模擬包含禁止群組的群組 token。 如果您需要安全地管理哪些使用者屬於哪些群組，您需要將該資料儲存在伺服器上，例如在資料庫中。 然後，將邏輯新增至您的應用程式，以在伺服器上驗證使用者是否屬於群組。 如需驗證群組成員資格的範例，請參閱[使用群組](../guide-to-the-api/working-with-groups.md)。

只有在暫時中斷之後，連接重新連線時，才會套用自動重新加入群組。 如果使用者離開應用程式或應用程式重新開機來中斷連線，您的應用程式必須處理如何將該使用者新增至正確的群組。 如需詳細資訊，請參閱[使用群組](../guide-to-the-api/working-with-groups.md)。

<a id="csrf"></a>

## <a name="how-signalr-prevents-cross-site-request-forgery"></a>SignalR 如何防止跨網站偽造要求

跨網站偽造要求（CSRF）是一種攻擊，惡意網站會將要求傳送至使用者目前登入的弱點網站。 SignalR 會讓惡意網站非常不太可能建立 SignalR 應用程式的有效要求，而避免 CSRF。

### <a name="description-of-csrf-attack"></a>CSRF 攻擊的描述

以下是 CSRF 攻擊的範例：

1. 使用者使用表單驗證登入 `www.example.com`。
2. 伺服器會驗證使用者。 伺服器的回應包含驗證 cookie。
3. 若未登出，使用者會造訪惡意網站。 這個惡意網站包含下列 HTML 表單： 

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

   請注意，表單動作會張貼到易受攻擊的網站，而不是惡意網站。 這是 CSRF 的「跨網站」部分。
4. 使用者按一下 [提交] 按鈕。 瀏覽器會在要求中包含驗證 cookie。
5. 此要求會在 example.com 伺服器上以使用者的驗證內容執行，並可執行已驗證使用者允許執行的任何動作。

雖然此範例需要使用者按一下表單按鈕，但惡意的網頁也可以輕鬆地執行腳本，將 AJAX 要求傳送至您的 SignalR 應用程式。 此外，使用 SSL 並不會防止 CSRF 攻擊，因為惡意網站可以傳送「HTTPs://」要求。

一般來說，使用 cookie 進行驗證的網站可能會發生 CSRF 攻擊，因為瀏覽器會將所有相關的 cookie 傳送至目的地網站。 不過，CSRF 攻擊並不限於利用 cookie。 例如，基本和摘要式驗證也很容易受到攻擊。 使用者使用基本或摘要式驗證登入之後，瀏覽器會自動傳送認證，直到會話結束為止。

### <a name="csrf-mitigations-taken-by-signalr"></a>SignalR 所採用的 CSRF 緩和措施

SignalR 會採取下列步驟，以防止惡意網站對您的 SignalR 應用程式建立有效的要求。 預設會採取這些步驟，而且不需要在您的程式碼中執行任何動作。

- **停用跨網域要求**  
 根據預設，SignalR 應用程式中的跨網域要求會停用，以防止使用者從外部網域呼叫 SignalR 端點。 來自外部網域的任何要求都會自動視為無效，而且會被封鎖。 建議您保留此預設行為;否則，惡意網站可以誘騙使用者傳送命令給您的網站。 如果您需要使用跨網域要求，請參閱[如何建立跨網域連接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。
- **在查詢字串中傳遞連接 token，而不是 cookie**  
 SignalR 會將連接 token 傳遞為查詢字串值，而不是 cookie。 藉由不將連線權杖儲存為 cookie，瀏覽器在遇到惡意程式碼時，不會不慎轉送連接標記。 此外，連接權杖不會保存在目前的連接之外。 因此，惡意使用者無法以另一個使用者的驗證認證來提出要求。
- **驗證連接權杖**  
 如連線[權杖](#connectiontoken)一節中所述，伺服器知道哪個連接識別碼與每個已驗證的使用者相關聯。 伺服器不會處理來自不符合使用者名稱之連線識別碼的任何要求。 惡意使用者不太可能猜到有效的要求，因為惡意使用者必須知道使用者名稱和目前隨機產生的連接識別碼。當連接結束時，該連接識別碼就會變成無效。 匿名使用者不應該有任何機密資訊的存取權。

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a>SignalR 安全性建議

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a>安全通訊端層（SSL）通訊協定

SSL 通訊協定會使用加密來保護用戶端與伺服器之間的資料傳輸。 如果您的 SignalR 應用程式會在用戶端與伺服器之間傳輸機密資訊，請使用 SSL 進行傳輸。 如需設定 SSL 的詳細資訊，請參閱[如何在 IIS 7 上設定 ssl](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)。

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a>請勿使用群組做為安全性機制

群組是一種方便收集相關使用者的方式，但不是限制存取機密資訊的安全機制。 當使用者可以在重新連線期間自動重新加入群組時，更是如此。 相反地，請考慮將特殊許可權使用者新增至角色，並將中樞方法的存取限制為只有該角色的成員。 如需根據角色限制存取的範例，請參閱[SignalR 中樞的驗證和授權](../security/hub-authorization.md)。 如需在重新連接時檢查使用者對群組存取權的範例，請參閱[使用群組](../guide-to-the-api/working-with-groups.md)。

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a>安全地處理來自用戶端的輸入

所有要用於廣播至其他用戶端的用戶端輸入，都必須經過編碼，以確保惡意使用者不會傳送腳本給其他使用者。 最好是在接收用戶端而非伺服器上編碼訊息，因為您的 SignalR 應用程式可能會有許多不同類型的用戶端。 因此，HTML 編碼適用于 web 用戶端，但不適用於其他類型的用戶端。 例如，用來顯示聊天訊息的 web 用戶端方法，會藉由呼叫 `html()` 函式，安全地處理使用者名稱和訊息。

[!code-html[Main](introduction-to-security/samples/sample2.html?highlight=3-4)]

<a id="reconcile"></a>

### <a name="reconciling-a-change-in-user-status-with-an-active-connection"></a>使用作用中連線協調使用者狀態的變更

如果使用者的驗證狀態在作用中連接存在時變更，使用者將會收到錯誤訊息，指出「使用者識別在使用中的 SignalR 連線期間無法變更」。 在這種情況下，您的應用程式應該重新連接到伺服器，以確保連接識別碼和使用者名稱的協調。 例如，如果您的應用程式允許使用者在使用中連接存在時登出，則連接的使用者名稱將不再符合下一個要求所傳入的名稱。 您會想要在使用者登出之前停止連線，然後再重新開機。

不過，請務必注意，大部分的應用程式都不需要手動停止和啟動連接。 如果您的應用程式在登出之後將使用者重新導向至另一個頁面（例如 Web form 應用程式或 MVC 應用程式中的預設行為），或在登出後重新整理目前的頁面，則使用中的連接會自動中斷連線，而且不會需要任何額外的動作。

下列範例顯示如何在使用者狀態變更時停止和啟動連接。

[!code-html[Main](introduction-to-security/samples/sample3.html)]

或者，如果您的網站使用具有表單驗證的滑動到期日，則使用者的驗證狀態可能會變更，而且沒有任何活動可以讓驗證 cookie 有效。 在此情況下，使用者將會登出，而使用者名稱將不再符合連接權杖中的使用者名稱。 若要修正這個問題，您可以新增一些定期要求 web 伺服器上資源的腳本，讓驗證 cookie 保持有效。 下列範例顯示如何每隔30分鐘要求資源。

[!code-javascript[Main](introduction-to-security/samples/sample4.js)]

<a id="autogen"></a>

### <a name="automatically-generated-javascript-proxy-files"></a>自動產生的 JavaScript proxy 檔案

如果您不想要在每個使用者的 JavaScript proxy 檔案中包含所有的中樞和方法，您可以停用自動產生檔案。 如果您有多個中樞和方法，但不想讓每位使用者都知道所有方法，您可以選擇此選項。 您可以藉由將**EnableJavaScriptProxies**設定為**false**來停用自動產生。

[!code-csharp[Main](introduction-to-security/samples/sample5.cs)]

如需 JavaScript proxy 檔案的詳細資訊，請參閱[產生的 proxy 和它為您提供的功能](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。 <a id="exceptions"></a>

### <a name="exceptions"></a>例外狀況

您應該避免將例外狀況物件傳遞給用戶端，因為物件可能會向用戶端公開機密資訊。 相反地，請在顯示相關錯誤訊息的用戶端上呼叫方法。

[!code-csharp[Main](introduction-to-security/samples/sample6.cs)]
