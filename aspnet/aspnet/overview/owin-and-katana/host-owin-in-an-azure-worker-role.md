---
uid: aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
title: Azure 背景工作角色中的主機 OWIN |Microsoft Docs
author: MikeWasson
description: 本教學課程說明如何在 Microsoft Azure 背景工作角色中自我裝載 OWIN。 Open Web Interface for .NET （OWIN）會定義 .NET Web 服務器之間的抽象概念 。
ms.author: riande
ms.date: 04/11/2014
ms.assetid: 07aa855a-92ee-4d43-ba66-5bfd7de20ee6
msc.legacyurl: /aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: 59d2e0d549427093f8a2424b17af81169b78ef30
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584613"
---
# <a name="host-owin-in-an-azure-worker-role"></a>將 OWIN 裝載在 Azure 背景工作角色中

由[Mike Wasson](https://github.com/MikeWasson)

> 本教學課程說明如何在 Microsoft Azure 背景工作角色中自我裝載 OWIN。
>
> [Open Web Interface for .net](http://owin.org/) （OWIN）會定義 .net Web 服務器和 Web 應用程式之間的抽象概念。 OWIN 會將 web 應用程式與伺服器分離，讓 OWIN 非常適合用於在您自己的進程中自我裝載 web 應用程式（在 IIS 之外），例如在 Azure 背景工作角色中。
>
> 在本教學課程中，您將瞭解如何在 Microsoft Azure 背景工作角色內自我裝載 OWIN 應用程式。 若要深入瞭解背景工作角色，請參閱[Azure 執行模型](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices)。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - [Azure SDK for .NET 2。3](https://azure.microsoft.com/downloads/)
> - [Owin. Selfhost 2.1。0](http://www.nuget.org/packages/Microsoft.Owin.SelfHost/2.1.0)

## <a name="create-a-microsoft-azure-project"></a>建立 Microsoft Azure 專案

使用系統管理員許可權啟動 Visual Studio。 您需要有系統管理員許可權，才能使用 Azure 計算模擬器在本機上進行應用程式的 debug。

**在 [檔案**] 功能表上，按一下 [**新增**]，然後按一下 [**專案**]。 從 **已安裝**的範本C# 的 視覺效果 底下，按一下 **雲端**，然後按一下  **Windows Azure 雲端服務** 將專案命名為 "Azureapp.java"，然後按一下 **[確定]** 。

[![](host-owin-in-an-azure-worker-role/_static/image2.png)](host-owin-in-an-azure-worker-role/_static/image1.png)

在 [**新的 Windows Azure 雲端服務**] 對話方塊中，按兩下 [背景**工作角色**]。 保留預設名稱（"WorkerRole1"）。 此步驟會將背景工作角色新增至解決方案。 按一下 [確定]。

[![](host-owin-in-an-azure-worker-role/_static/image4.png)](host-owin-in-an-azure-worker-role/_static/image3.png)

所建立的 Visual Studio 解決方案包含兩個專案：

- &quot;Azureapp.java&quot; 定義 Azure 應用程式的角色和設定。
- &quot;WorkerRole1&quot; 包含背景工作角色的程式碼。

一般而言，Azure 應用程式可以包含多個角色，雖然本教學課程使用單一角色。

![](host-owin-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-owin-self-host-packages"></a>新增 OWIN 自我裝載套件

從 [**工具**] 功能表中，按一下 [ **NuGet 套件管理員**]，然後按一下 [**套件管理員主控台**]。

在 [Package Manager Console] 視窗中，輸入下列命令：

[!code-console[Main](host-owin-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a>新增 HTTP 端點

在方案總管中，展開 [Azureapp.java] 專案。 展開 [角色] 節點，以滑鼠右鍵按一下 [WorkerRole1]，然後選取 [**屬性**]。

![](host-owin-in-an-azure-worker-role/_static/image6.png)

按一下 **[端點]** ，然後按一下 **[新增端點]** 。

在 [**通訊協定**] 下拉式清單中，選取 [HTTP]。 在 [**公用埠**] 和 [**私人埠**] 中，輸入80。 這些連接埠號碼可以不同。 公用埠是用戶端將要求傳送至角色時所使用的。

[![](host-owin-in-an-azure-worker-role/_static/image8.png)](host-owin-in-an-azure-worker-role/_static/image7.png)

## <a name="create-the-owin-startup-class"></a>建立 OWIN 啟動類別

在方案總管中，以滑鼠右鍵按一下 WorkerRole1 專案，然後選取 [**新增** / **類別**] 以加入新的類別。 將類別命名為 `Startup`。

將所有的重複使用程式碼取代為下列內容：

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample2.cs)]

`UseWelcomePage` 擴充方法會將簡單的 HTML 網頁新增至您的應用程式，以確認網站是否正常運作。

## <a name="start-the-owin-host"></a>啟動 OWIN 主機

開啟 WorkerRole.cs 檔案。 這個類別會定義背景工作角色啟動和停止時所執行的程式碼。

加入下列 using 陳述式：

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample3.cs)]

將**IDisposable**成員新增至 `WorkerRole` 類別：

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample4.cs)]

在 `OnStart` 方法中，新增下列程式碼以啟動主機：

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample5.cs?highlight=5)]

**WebApp**方法啟動 OWIN 主機。 `Startup` 類別的名稱是方法的型別參數。 依照慣例，主機會呼叫這個類別的 `Configure` 方法。

覆寫 `OnStop` 以處置 *\_應用程式*實例：

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample6.cs)]

以下是 WorkerRole.cs 的完整程式碼：

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample7.cs)]

建立解決方案，然後按 F5 在 Azure 計算模擬器中本機執行應用程式。 根據您的防火牆設定，您可能需要允許模擬器通過防火牆。

計算模擬器會將本機 IP 位址指派給端點。 您可以藉由查看計算模擬器 UI 來尋找 IP 位址。 以滑鼠右鍵按一下工作列通知區域中的模擬器圖示，然後選取 [**顯示計算模擬器 UI**]。

[![](host-owin-in-an-azure-worker-role/_static/image10.png)](host-owin-in-an-azure-worker-role/_static/image9.png)

尋找 [服務部署]、[部署 [識別碼]]、[服務詳細資料] 底下的 IP 位址。 開啟網頁瀏覽器，並流覽至 HTTP：\/\/*address*，其中*address*是計算模擬器所指派的 IP 位址;例如，`http://127.0.0.1:80`。 您應該會看到 [OWIN 歡迎使用] 頁面：

![](host-owin-in-an-azure-worker-role/_static/image11.png)

## <a name="deploy-to-azure"></a>部署到 Azure

在此步驟中，您必須擁有 Azure 帳戶。 如果您還沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資訊，請參閱[Microsoft Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。

在方案總管中，以滑鼠右鍵按一下 [Azureapp.java] 專案。 選取 [發行]。

![](host-owin-in-an-azure-worker-role/_static/image12.png)

如果您未登入您的 Azure 帳戶，請按一下 [登**入**]。

[![](host-owin-in-an-azure-worker-role/_static/image14.png)](host-owin-in-an-azure-worker-role/_static/image13.png)

登入之後，請選擇訂用帳戶，然後按 **[下一步]** 。

[![](host-owin-in-an-azure-worker-role/_static/image16.png)](host-owin-in-an-azure-worker-role/_static/image15.png)

輸入雲端服務的名稱，然後選擇 [區域]。 按一下 [建立]。

![](host-owin-in-an-azure-worker-role/_static/image17.png)

按一下 [發行]。

[![](host-owin-in-an-azure-worker-role/_static/image19.png)](host-owin-in-an-azure-worker-role/_static/image18.png)

[Azure 活動記錄] 視窗會顯示部署的進度。 部署應用程式時，流覽至 `http://appname.cloudapp.net/`，其中*appname*是您的雲端服務名稱。

## <a name="additional-resources"></a>其他資源

- [Katana 專案概觀](an-overview-of-project-katana.md)
- [GitHub 上的 Katana 專案](https://github.com/aspnet/AspNetKatana/)
