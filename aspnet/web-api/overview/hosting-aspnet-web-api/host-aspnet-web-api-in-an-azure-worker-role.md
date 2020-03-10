---
uid: web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
title: Azure 背景工作角色中的主機 ASP.NET Web API 2-ASP.NET 4。x
author: MikeWasson
description: 教學課程：使用 OWIN 自我裝載 Web API 架構，在 Azure 背景工作角色中裝載 ASP.NET Web API。
ms.author: riande
ms.date: 04/02/2014
ms.custom: seoapril2019
ms.assetid: 6980ee2e-d6b0-4a08-8fb6-ab96362dd0e3
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: ec9904e0bff090be0f504036ae73977cfca0cb31
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556627"
---
# <a name="host-aspnet-web-api-2-in-an-azure-worker-role"></a>Azure 背景工作角色中的主機 ASP.NET Web API 2

由[Mike Wasson](https://github.com/MikeWasson)

> 本教學課程說明如何使用 OWIN 自我裝載 Web API 架構，在 Azure 背景工作角色中裝載 ASP.NET Web API。
>
> [Open Web Interface for .net](http://owin.org/) （OWIN）會定義 .net Web 服務器和 Web 應用程式之間的抽象概念。 OWIN 會將 web 應用程式與伺服器分離，讓 OWIN 非常適合用於在您自己的進程中自我裝載 web 應用程式（在 IIS 之外），例如在 Azure 背景工作角色中。
>
> 在本教學課程中，您將使用 HttpListener 套件，它提供了用於自我裝載 OWIN 應用程式的 HTTP 伺服器。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - Web API 2
> - [Azure SDK for .NET 2。3](https://azure.microsoft.com/downloads/)

## <a name="create-a-microsoft-azure-project"></a>建立 Microsoft Azure 專案

使用系統管理員許可權啟動 Visual Studio。 您需要有系統管理員許可權，才能使用 Azure 計算模擬器在本機上進行應用程式的 debug。

**在 [檔案**] 功能表上，按一下 [**新增**]，然後按一下 [**專案**]。 從 **已安裝**的範本C# 的 視覺效果 底下，按一下 **雲端**，然後按一下  **Windows Azure 雲端服務** 將專案命名為 "Azureapp.java"，然後按一下 **[確定]** 。

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image2.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image1.png)

在 [**新的 Windows Azure 雲端服務**] 對話方塊中，按兩下 [背景**工作角色**]。 保留預設名稱（"WorkerRole1"）。 此步驟會將背景工作角色新增至解決方案。 按一下 [確定]。

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image4.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image3.png)

所建立的 Visual Studio 解決方案包含兩個專案：

- &quot;Azureapp.java&quot; 定義 Azure 應用程式的角色和設定。
- &quot;WorkerRole1&quot; 包含背景工作角色的程式碼。

一般而言，Azure 應用程式可以包含多個角色，雖然本教學課程使用單一角色。

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-web-api-and-owin-packages"></a>新增 Web API 和 OWIN 套件

從 [**工具**] 功能表中，按一下 [ **NuGet 套件管理員**]，然後按一下 [**套件管理員主控台**]。

在 [Package Manager Console] 視窗中，輸入下列命令：

[!code-console[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a>新增 HTTP 端點

在方案總管中，展開 [Azureapp.java] 專案。 展開 [角色] 節點，以滑鼠右鍵按一下 [WorkerRole1]，然後選取 [**屬性**]。

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image6.png)

按一下 **[端點]** ，然後按一下 **[新增端點]** 。

在 [**通訊協定**] 下拉式清單中，選取 [HTTP]。 在 [**公用埠**] 和 [**私人埠**] 中，輸入80。 這些連接埠號碼可以不同。 公用埠是用戶端將要求傳送至角色時所使用的。

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image8.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image7.png)

## <a name="configure-web-api-for-self-host"></a>設定適用于自我裝載的 Web API

在方案總管中，以滑鼠右鍵按一下 WorkerRole1 專案，然後選取 [**新增** / **類別**] 以加入新的類別。 將類別命名為 `Startup`。

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image9.png)

以下列內容取代此檔案中的所有重複使用的程式碼：

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample2.cs)]

## <a name="add-a-web-api-controller"></a>新增 Web API 控制器

接下來，新增 Web API 控制器類別。 以滑鼠右鍵按一下 [WorkerRole1] 專案，然後選取 [**新增** / **類別**]。 將類別命名為 TestController。 以下列內容取代此檔案中的所有重複使用的程式碼：

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample3.cs)]

為了簡單起見，此控制器只會定義兩個會傳回純文字的 GET 方法。

## <a name="start-the-owin-host"></a>啟動 OWIN 主機

開啟 WorkerRole.cs 檔案。 這個類別會定義背景工作角色啟動和停止時所執行的程式碼。

加入下列 using 陳述式：

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample4.cs)]

將**IDisposable**成員新增至 `WorkerRole` 類別：

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample5.cs)]

在 `OnStart` 方法中，新增下列程式碼以啟動主機：

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample6.cs?highlight=5)]

**WebApp**方法啟動 OWIN 主機。 `Startup` 類別的名稱是方法的型別參數。 依照慣例，主機會呼叫這個類別的 `Configure` 方法。

覆寫 `OnStop` 以處置 *\_應用程式*實例：

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample7.cs)]

以下是 WorkerRole.cs 的完整程式碼：

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample8.cs)]

建立解決方案，然後按 F5 在 Azure 計算模擬器中本機執行應用程式。 根據您的防火牆設定，您可能需要允許模擬器通過防火牆。

> [!NOTE]
> 如果您收到類似下面的例外狀況，請參閱[這篇 blog 文章](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx)以取得因應措施。 「無法載入檔案或元件 ' Owin，Version = 2.0.2.0，Culture = 中性，PublicKeyToken = 31bf3856ad364e35 ' 或其相依性的其中之一。 找不到元件的資訊清單定義與元件參考不符。 （來自 HRESULT 的例外狀況：0x80131040）」

計算模擬器會將本機 IP 位址指派給端點。 您可以藉由查看計算模擬器 UI 來尋找 IP 位址。 以滑鼠右鍵按一下工作列通知區域中的模擬器圖示，然後選取 [**顯示計算模擬器 UI**]。

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image11.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image10.png)

尋找 [服務部署]、[部署 [識別碼]]、[服務詳細資料] 底下的 IP 位址。 開啟網頁瀏覽器並流覽至 HTTP://<em>address</em>/test/1，其中<em>address</em>是計算模擬器所指派的 IP 位址;例如，`http://127.0.0.1:80/test/1`。 您應該會看到來自 Web API 控制器的回應：

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image12.png)

## <a name="deploy-to-azure"></a>部署到 Azure

在此步驟中，您必須擁有 Azure 帳戶。 如果您還沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資訊，請參閱[Microsoft Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。

在方案總管中，以滑鼠右鍵按一下 [Azureapp.java] 專案。 選取 [發行]。

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image13.png)

如果您未登入您的 Azure 帳戶，請按一下 [登**入**]。

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image15.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image14.png)

登入之後，請選擇訂用帳戶，然後按 **[下一步]** 。

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image17.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image16.png)

輸入雲端服務的名稱，然後選擇 [區域]。 按一下 [建立]。

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image18.png)

按一下 [發行]。

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image20.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image19.png)

[Azure 活動記錄] 視窗會顯示部署的進度。 部署應用程式時，請流覽至 http://appname.cloudapp.net/test/1。

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image21.png)

## <a name="additional-resources"></a>其他資源

- [Katana 專案概觀](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)
- [GitHub 上的 Katana 專案](https://github.com/aspnet/AspNetKatana)
