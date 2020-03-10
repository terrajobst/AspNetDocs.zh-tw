---
uid: web-api/overview/security/working-with-ssl-in-web-api
title: 在 Web API 中使用 SSL |Microsoft Docs
author: MikeWasson
description: 說明如何搭配 ASP.NET Web API 使用 SSL，包括使用 SSL 用戶端憑證。
ms.author: riande
ms.date: 02/22/2019
ms.assetid: 97f6164f-59cf-45c0-b820-e4aa29b45396
msc.legacyurl: /web-api/overview/security/working-with-ssl-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 31589b3713b1f1a9b98d12906bfef81f8bf5e3f9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598634"
---
# <a name="working-with-ssl-in-web-api"></a>在 Web API 中使用 SSL

由[Mike Wasson](https://github.com/MikeWasson)

有數個常見的驗證配置不會受到一般 HTTP 的保護。 尤其是，基本驗證和表單驗證會傳送未加密的認證。 為了安全，這些驗證配置*必須*使用 SSL。 此外，您還可以使用 SSL 用戶端憑證來驗證用戶端。

## <a name="enabling-ssl-on-the-server"></a>在伺服器上啟用 SSL

若要在 IIS 7 或更新版本中設定 SSL：

- 建立或取得憑證。 若要進行測試，您可以建立自我簽署憑證。
- 新增 HTTPS 系結。

如需詳細資訊，請參閱[如何在 IIS 7 上設定 SSL](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)。

若要進行本機測試，您可以從 Visual Studio 啟用 IIS Express 中的 SSL。 在 屬性視窗中，將  **SSL 已啟用** 設定為  **True**。 記下 [ **SSL URL**] 的值;使用此 URL 來測試 HTTPS 連接。

![](working-with-ssl-in-web-api/_static/image1.png)

### <a name="enforcing-ssl-in-a-web-api-controller"></a>在 Web API 控制器中強制執行 SSL

如果您同時有 HTTPS 和 HTTP 系結，用戶端仍然可以使用 HTTP 來存取網站。 您可能會允許某些資源透過 HTTP 提供，而其他資源則需要 SSL。 在此情況下，請使用動作篩選準則來要求保護資源的 SSL。 下列程式碼顯示會檢查 SSL 的 Web API 驗證篩選︰

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample1.cs)]

將此篩選新增至任何需要 SSL 的 Web API 動作︰

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample2.cs)]

## <a name="ssl-client-certificates"></a>SSL 用戶端憑證

SSL 會使用公開金鑰基礎結構憑證來提供驗證。 伺服器必須提供可向用戶端驗證服務器的憑證。 用戶端不常提供憑證給伺服器，但這是驗證用戶端的一個選項。 若要使用用戶端憑證搭配 SSL，您需要有方法將已簽署的憑證散發給您的使用者。 對於許多應用程式類型而言，這並不是很好的使用者體驗，但在某些環境（例如企業）中，這可能是可行的。

| 優點 | 缺點 |
| --- | --- |
| -憑證認證比使用者名稱/密碼更強。 -SSL 提供完整的安全通道，其中包含驗證、訊息完整性和訊息加密。 | -您必須取得並管理 PKI 憑證。 -用戶端平臺必須支援 SSL 用戶端憑證。 |

若要設定 IIS 以接受用戶端憑證，請開啟 IIS 管理員，然後執行下列步驟：

1. 按一下樹狀檢視中的 [網站] 節點。
2. 按兩下中間窗格中的 [ **SSL 設定**] 功能。
3. 在 [**用戶端憑證**] 底下，選取下列其中一個選項： 

    - **接受**： IIS 會接受來自用戶端的憑證，但不需要一個。
    - **需要**：需要用戶端憑證。 （若要啟用此選項，您也必須選取 [需要 SSL]）

您也可以在 Applicationhost.config 檔案中設定這些選項：

[!code-xml[Main](working-with-ssl-in-web-api/samples/sample3.xml)]

**目的 sslnegotiatecert**旗標表示 iis 會接受來自用戶端的憑證，但不需要它（相當於 IIS 管理員中的 [接受] 選項）。 若要要求憑證，請設定**在**旗標。 若要進行測試，您也可以在本機 applicationhost.config 的 IIS Express 中設定這些選項。設定檔，位於 "Documents\IISExpress\config"。

### <a name="creating-a-client-certificate-for-testing"></a>建立用於測試的用戶端憑證

基於測試目的，您可以使用[MakeCert](/windows/desktop/SecCrypto/makecert)來建立用戶端憑證。 首先，建立測試根目錄授權單位：

[!code-console[Main](working-with-ssl-in-web-api/samples/sample4.cmd)]

Makecert 會提示您輸入私密金鑰的密碼。

接下來，將憑證新增至測試伺服器的「受信任的根憑證授權單位」存放區，如下所示：

1. 開啟 MMC。
2. 在 **[** 檔案] 底下，選取 [**新增/移除嵌入式管理單元**]。
3. 選取 [**電腦帳戶**]。
4. 選取 [**本機電腦**]，然後完成嚮導。
5. 在流覽窗格中，展開 [信任的根憑證授權單位] 節點。
6. 在 [**動作**] 功能表上，指向 [**所有**工作]，然後按一下 [匯**入**] 以啟動 [憑證匯入嚮導]。
7. 流覽至憑證檔案（TempCA. .cer）。
8. 按一下 [**開啟**]，然後按 **[下一步**] 並完成嚮導。 （系統會提示您重新輸入密碼。）

現在，建立由第一個憑證簽署的用戶端憑證：

[!code-console[Main](working-with-ssl-in-web-api/samples/sample5.cmd)]

### <a name="using-client-certificates-in-web-api"></a>在 Web API 中使用用戶端憑證

在伺服器端上，您可以藉由在要求訊息上呼叫[GetClientCertificate](https://msdn.microsoft.com/library/system.net.http.httprequestmessageextensions.getclientcertificate.aspx)來取得用戶端憑證。 如果沒有用戶端憑證，此方法會傳回 null。 否則，它會傳回**X509Certificate2**實例。 使用此物件來取得憑證的資訊，例如簽發者和主旨。 然後您可以使用此資訊進行驗證和/或授權。

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample6.cs)]
