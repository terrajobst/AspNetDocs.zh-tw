---
uid: signalr/overview/performance/signalr-connection-density-testing-with-crank
title: 使用迅速地建立 SignalR 連接密度測試 |Microsoft Docs
author: bradygaster
description: 使用曲軸的 SignalR 連線密度測試
ms.author: bradyg
ms.date: 02/22/2015
ms.assetid: 148d9ca7-1af1-44b6-a9fb-91e261b9b463
msc.legacyurl: /signalr/overview/performance/signalr-connection-density-testing-with-crank
msc.type: authoredcontent
ms.openlocfilehash: 901e039fbb81651ed18d560c99745b7e7f716e01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558335"
---
# <a name="signalr-connection-density-testing-with-crank"></a>使用曲軸的 SignalR 連線密度測試

由[Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文說明如何使用迅速地建立工具來測試具有多個模擬用戶端的應用程式。

當您的應用程式在其主控環境（Azure web 角色、IIS 或使用 Owin 的自我裝載）中執行之後，您就可以使用迅速地建立工具來測試應用程式對高階連接密度的回應。 裝載環境可以是 Internet Information Services （IIS）伺服器、Owin 主機或 Azure web 角色。 （注意：效能計數器無法在 Azure App Service Web Apps 上使用，因此您將無法從連接密度測試取得效能資料）。

連接密度是指可以在伺服器上建立的同時 TCP 連線數目。 每個 TCP 連線都會產生自己的額外負荷，而開啟大量的閒置連線最後會造成記憶體瓶頸。

[SignalR 程式碼基](https://github.com/signalr/signalr)底包含一個稱為**迅速地建立**的負載測試工具。 您可以在 GitHub 上[的 Dev 分支](https://github.com/SignalR/signalr/tree/dev)中找到最新版本的迅速地建立。 您可以在[這裡](https://github.com/SignalR/SignalR/archive/dev.zip)下載 SignalR 程式碼基底之 Dev 分支的 Zip 封存。

迅速地建立可以用來完全使伺服器的記憶體飽和，以便計算伺服器硬體上可能的閒置連接總數。 或者，您也可以使用迅速地建立，在特定的記憶體不足壓力之下，將伺服器負載測試，方法是在達到特定的計數或特定的記憶體閾值之前，先加速連接。

測試時，請務必使用遠端用戶端，以避免任何資源競爭（例如 TCP 連線和記憶體）。 監視用戶端，以確保它們不會遇到任何可能導致伺服器無法達到其完整容量（記憶體或 CPU）的瓶頸。 您可能需要增加用戶端數目，才能完全載入伺服器。

### <a name="running-a-connection-density-test"></a>執行連接密度測試

本節說明在 SignalR 應用程式上執行連接密度測試所需的步驟。

1. 下載並建立[SignalR 程式碼基底的開發分支](https://github.com/SignalR/SignalR/archive/dev.zip)。 在命令提示字元中，流覽至 &lt;專案目錄&gt;\src\Microsoft.AspNet.SignalR.Crank\bin\debug。
2. 將您的應用程式部署到其預定的裝載環境。 記下您的應用程式所使用的端點;例如，在[消費者入門教學](../getting-started/tutorial-getting-started-with-signalr.md)課程中建立的應用程式中，端點會 `http://<yourhost>:8080/signalr`。
3. 在伺服器上安裝[SignalR 效能計數器](signalr-performance.md#perfcounters)。 如果您的應用程式正在 Azure 上執行，請參閱[在 Azure Web 角色中使用 SignalR 效能計數器](using-signalr-performance-counters-in-an-azure-web-role.md)。

在您下載並建立程式碼基底，並在您的主機上安裝效能計數器之後，您可以在 [`src\Microsoft.AspNet.SignalR.Crank\bin\Debug`] 資料夾中找到迅速地建立命令列工具。

迅速地建立工具的可用選項包括：

- **/？** ：顯示說明畫面。 如果省略**Url**參數，也會顯示可用的選項。
- **/Url**： SignalR 連接的 Url。 這是必要參數。 若為使用預設對應的 SignalR 應用程式，路徑的結尾會是 "/signalr"。
- **/傳輸**：所使用的傳輸名稱。 預設值為 [`auto`]，這會選取最佳的可用通訊協定。 選項包括 `WebSockets`、`ServerSentEvents`和 `LongPolling` （`ForeverFrame` 不是迅速地建立的選項，因為會使用 .NET 用戶端，而不是 Internet Explorer）。 如需 SignalR 如何選取傳輸的詳細資訊，請參閱[傳輸和回退](../getting-started/introduction-to-signalr.md#transports)。
- **/BatchSize**：每個批次中新增的用戶端數目。 預設值為 50。
- **/ConnectInterval**：新增連接之間的間隔（以毫秒為單位）。 預設值為 500。
- **/Connections**：用來對應用程式進行負載測試的連接數目。 預設值為100000。
- **/ConnectTimeout**：中止測試之前的超時（以秒為單位）。 預設值為300。
- **MinServerMBytes**：到達的最小伺服器 mb。 預設值為 500。
- **SendBytes**：傳送至伺服器的承載大小（以位元組為單位）。 預設值為 0。
- **SendInterval**：訊息到伺服器之間的延遲（以毫秒為單位）。 預設值為 500。
- **SendTimeout**：訊息到伺服器的超時時間（以毫秒為單位）。 預設值為300。
- **ControllerUrl**：一個用戶端將裝載控制器中樞的 Url。 預設值為 null （不控制器中樞）。 當迅速地建立會話啟動時，就會啟動控制器中樞;控制器中樞與迅速地建立之間沒有進一步的連絡人。
- **NumClients**：要連接到應用程式的模擬用戶端數目。 預設值為一個。
- **Logfile**：用於測試回合之記錄檔的檔案名。 預設為 `crank.csv`。
- **SampleInterval**：效能計數器樣本之間的時間（以毫秒為單位）。 預設值為 1000。
- **SignalRInstance**：伺服器上效能計數器的實例名稱。 預設值是使用用戶端線上狀態。

### <a name="example"></a>範例

下列命令會在 Azure 上測試名為 `pfsignalr` 的網站，其裝載在埠8080上的應用程式，並使用名為 "ControllerHub" 的中樞，並使用100連接。

`crank /Connections:100 /Url:http://pfsignalr.cloudapp.net:8080/signalr`
